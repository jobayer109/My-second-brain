Okay, here is a detailed step-by-step plan for implementing the MCQ feature, including code suggestions for each part.

__Phase 1: Backend Development (Server Project)__

__Step 1: Create Backend Entities__

- __Task:__ Define the data structure for MCQs and their options using TypeORM entities.

- __Files:__

  - `server/src/entity/MCQ.ts`
  - `server/src/entity/QuestionOption.ts`

- __Code Suggestion (`server/src/entity/MCQ.ts`):__

  ```typescript
  import { Entity, PrimaryGeneratedColumn, Column, OneToMany, ManyToOne } from 'typeorm';
  import { QuestionOption } from './QuestionOption';
  import { Course } from './Course'; // Assuming Course entity exists

  @Entity()
  export class MCQ {
    @PrimaryGeneratedColumn('uuid')
    id: string;

    @Column()
    question: string;

    @OneToMany(() => QuestionOption, option => option.mcq, { cascade: true }) // Added cascade for easier option management
    options: QuestionOption[];

    @Column('uuid')
    correctAnswerId: string;

    @ManyToOne(() => Course, course => course.mcqs)
    course: Course; // Associate MCQs with a Course
  }
  ```

- __Code Suggestion (`server/src/entity/QuestionOption.ts`):__

  ```typescript
  import { Entity, PrimaryGeneratedColumn, Column, ManyToOne } from 'typeorm';
  import { MCQ } from './MCQ';

  @Entity()
  export class QuestionOption {
    @PrimaryGeneratedColumn('uuid')
    id: string;

    @Column()
    text: string;

    @ManyToOne(() => MCQ, mcq => mcq.options, { onDelete: 'CASCADE' }) // Added onDelete cascade
    mcq: MCQ;
  }
  ```

- __Action:__ Create these two files with the provided content.

__Step 2: Create Backend Controller__

- __Task:__ Create a controller to handle incoming API requests for MCQ CRUD operations.

- __File:__ `server/src/controllers/MCQController.ts`

- __Code Suggestion (`server/src/controllers/MCQController.ts` - initial structure):__

  ```typescript
  import { Request, Response, Router } from 'express';
  import { AppDataSource } from '../data-source'; // Assuming your data source is here
  import { MCQ } from '../entity/MCQ';
  import { QuestionOption } from '../entity/QuestionOption';

  const router = Router();
  const mcqRepository = AppDataSource.getRepository(MCQ);
  const optionRepository = AppDataSource.getRepository(QuestionOption);

  // GET all MCQs (or by course)
  router.get('/', async (req: Request, res: Response) => {
    try {
      // Implement logic to fetch MCQs, potentially filtered by courseId from query params
      const mcqs = await mcqRepository.find({ relations: ['options'] }); // Include options
      res.json(mcqs);
    } catch (error) {
      res.status(500).json({ message: 'Error fetching MCQs', error });
    }
  });

  // GET single MCQ by ID
  router.get('/:id', async (req: Request, res: Response) => {
    try {
      const mcq = await mcqRepository.findOne({ where: { id: req.params.id }, relations: ['options'] });
      if (!mcq) {
        return res.status(404).json({ message: 'MCQ not found' });
      }
      res.json(mcq);
    } catch (error) {
      res.status(500).json({ message: 'Error fetching MCQ', error });
    }
  });

  // POST create new MCQ
  router.post('/', async (req: Request, res: Response) => {
    try {
      const { question, options, correctAnswerId, courseId } = req.body;

      // Basic validation (more detailed validation should be added)
      if (!question || !options || !correctAnswerId || !courseId) {
          return res.status(400).json({ message: 'Missing required fields' });
      }

      const newMCQ = mcqRepository.create({ question, correctAnswerId, course: { id: courseId } });

      // Create and associate options
      newMCQ.options = options.map((option: { text: string }) => optionRepository.create({ text: option.text, mcq: newMCQ }));

      await mcqRepository.save(newMCQ);
      res.status(201).json(newMCQ);
    } catch (error) {
      res.status(500).json({ message: 'Error creating MCQ', error });
    }
  });

  // PUT update existing MCQ
  router.put('/:id', async (req: Request, res: Response) => {
    try {
      const { question, options, correctAnswerId, courseId } = req.body;
      const mcq = await mcqRepository.findOne({ where: { id: req.params.id }, relations: ['options'] });

      if (!mcq) {
        return res.status(404).json({ message: 'MCQ not found' });
      }

      // Update basic fields
      mcq.question = question || mcq.question;
      mcq.correctAnswerId = correctAnswerId || mcq.correctAnswerId;
      if (courseId) {
          mcq.course = { id: courseId } as any; // Update course if provided
      }


      // Handle options update (more complex: delete old, create new, or update existing)
      // For simplicity here, we'll assume options are replaced. A more robust solution
      // would compare existing options and update/delete/create as needed.
      if (options) {
           // Remove old options
          await optionRepository.remove(mcq.options);
          // Create new options
          mcq.options = options.map((option: { text: string }) => optionRepository.create({ text: option.text, mcq: mcq }));
      }


      await mcqRepository.save(mcq);
      res.json(mcq);
    } catch (error) {
      res.status(500).json({ message: 'Error updating MCQ', error });
    }
  });

  // DELETE MCQ by ID
  router.delete('/:id', async (req: Request, res: Response) => {
    try {
      const result = await mcqRepository.delete(req.params.id);
      if (result.affected === 0) {
        return res.status(404).json({ message: 'MCQ not found' });
      }
      res.json({ message: 'MCQ deleted successfully' });
    } catch (error) {
      res.status(500).json({ message: 'Error deleting MCQ', error });
    }
  });


  export default router;
  ```

- __Action:__ Create this file with the provided content.

__Step 3: Integrate Backend Routes__

- __Task:__ Add the new MCQ routes to the main application router.

- __File:__ Likely `server/src/routes/index.ts` or `server/src/app.ts` (depending on your routing setup).

- __Code Suggestion (Example for `server/src/routes/index.ts`):__

  ```typescript
  import { Router } from 'express';
  import authRoutes from './authRoutes'; // Assuming you have other routes
  import courseRoutes from './courseRoutes'; // Assuming you have other routes
  import mcqRoutes from '../controllers/MCQController'; // Import the new controller

  const router = Router();

  router.use('/auth', authRoutes);
  router.use('/courses', courseRoutes);
  router.use('/mcqs', mcqRoutes); // Add the new MCQ routes

  export default router;
  ```

- __Action:__ Modify your main routing file to include the `mcqRoutes`.

__Phase 2: Frontend Development (CMS Project)__

__Step 4: Create Frontend API Service__

- __Task:__ Create functions to handle API calls related to MCQs.

- __File:__ `cms/src/api/mcqApi.js` (or integrate into an existing API service file like `cms/src/api/index.js`)

- __Code Suggestion (`cms/src/api/mcqApi.js`):__

  ```javascript
  import axios from 'axios';

  const API_URL = '/api/mcqs'; // Adjust if your API base URL is different

  export const getAllMCQs = async () => {
    try {
      const response = await axios.get(API_URL);
      return response.data;
    } catch (error) {
      console.error('Error fetching MCQs:', error);
      throw error;
    }
  };

  export const getMCQById = async (id) => {
    try {
      const response = await axios.get(`${API_URL}/${id}`);
      return response.data;
    } catch (error) {
      console.error(`Error fetching MCQ with ID ${id}:`, error);
      throw error;
    }
  };

  export const createMCQ = async (mcqData) => {
    try {
      const response = await axios.post(API_URL, mcqData);
      return response.data;
    } catch (error) {
      console.error('Error creating MCQ:', error);
      throw error;
    }
  };

  export const updateMCQ = async (id, mcqData) => {
    try {
      const response = await axios.put(`${API_URL}/${id}`, mcqData);
      return response.data;
    } catch (error) {
      console.error(`Error updating MCQ with ID ${id}:`, error);
      throw error;
    }
  };

  export const deleteMCQ = async (id) => {
    try {
      const response = await axios.delete(`${API_URL}/${id}`);
      return response.data;
    } catch (error) {
      console.error(`Error deleting MCQ with ID ${id}:`, error);
      throw error;
    }
  };
  ```

- __Action:__ Create this file with the provided content or add these functions to your existing API service.

__Step 5: Create CMS List Component__

- __Task:__ Develop a React component to display a list of MCQs.

- __File:__ `cms/src/components/MCQList.jsx`

- __Code Suggestion (`cms/src/components/MCQList.jsx` - basic structure):__

  ```javascript
  import React, { useEffect, useState } from 'react';
  import { getAllMCQs, deleteMCQ } from '../api/mcqApi'; // Adjust path as needed

  const MCQList = () => {
    const [mcqs, setMcqs] = useState([]);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
      const fetchMCQs = async () => {
        try {
          const data = await getAllMCQs();
          setMcqs(data);
        } catch (err) {
          setError(err);
        } finally {
          setLoading(false);
        }
      };
      fetchMCQs();
    }, []);

    const handleDelete = async (id) => {
      try {
        await deleteMCQ(id);
        setMcqs(mcqs.filter(mcq => mcq.id !== id));
      } catch (err) {
        console.error('Error deleting MCQ:', err);
        // Handle error (e.g., show a toast notification)
      }
    };

    if (loading) return <p>Loading MCQs...</p>;
    if (error) return <p>Error loading MCQs: {error.message}</p>;

    return (
      <div>
        <h2>MCQ List</h2>
        {mcqs.length === 0 ? (
          <p>No MCQs found.</p>
        ) : (
          <ul>
            {mcqs.map(mcq => (
              <li key={mcq.id}>
                {mcq.question}
                {/* Add buttons for Edit and Delete */}
                <button onClick={() => handleDelete(mcq.id)}>Delete</button>
                {/* Add Edit button that navigates to the form or opens a modal */}
              </li>
            ))}
          </ul>
        )}
      </div>
    );
  };

  export default MCQList;
  ```

- __Action:__ Create this file with the provided content.

__Step 6: Create CMS Form Component__

- __Task:__ Develop a React component to create and edit MCQs.

- __File:__ `cms/src/components/MCQForm.jsx`

- __Code Suggestion (`cms/src/components/MCQForm.jsx` - basic structure):__

  ```javascript
  import React, { useState, useEffect } from 'react';
  import { createMCQ, getMCQById, updateMCQ } from '../api/mcqApi'; // Adjust path as needed
  import { useParams, useNavigate } from 'react-router-dom'; // Assuming react-router for navigation

  const MCQForm = () => {
    const { id } = useParams(); // Get ID from URL for editing
    const navigate = useNavigate();
    const [formData, setFormData] = useState({
      question: '',
      options: [{ text: '' }, { text: '' }, { text: '' }, { text: '' }], // Start with 4 options
      correctAnswerId: '',
      courseId: '' // Assuming you need to associate with a course
    });
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
    const [isEditing, setIsEditing] = useState(false);

    useEffect(() => {
      if (id) {
        setIsEditing(true);
        const fetchMCQ = async () => {
          try {
            const mcq = await getMCQById(id);
            setFormData({
              question: mcq.question,
              options: mcq.options,
              correctAnswerId: mcq.correctAnswerId,
              courseId: mcq.course ? mcq.course.id : '' // Populate courseId if available
            });
          } catch (err) {
            setError(err);
          } finally {
            setLoading(false);
          }
        };
        fetchMCQ();
      } else {
        setLoading(false);
      }
    }, [id]);

    const handleInputChange = (e) => {
      const { name, value } = e.target;
      setFormData({ ...formData, [name]: value });
    };

    const handleOptionChange = (index, e) => {
      const newOptions = [...formData.options];
      newOptions[index].text = e.target.value;
      setFormData({ ...formData, options: newOptions });
    };

    const handleCorrectAnswerChange = (optionId) => {
      setFormData({ ...formData, correctAnswerId: optionId });
    };

    const handleSubmit = async (e) => {
      e.preventDefault();
      setLoading(true);
      try {
        if (isEditing) {
          await updateMCQ(id, formData);
        } else {
          await createMCQ(formData);
        }
        navigate('/mcqs'); // Navigate back to the list after saving
      } catch (err) {
        setError(err);
        console.error('Error saving MCQ:', err);
        // Handle error
      } finally {
        setLoading(false);
      }
    };

    if (loading) return <p>Loading form...</p>;
    if (error) return <p>Error loading form: {error.message}</p>;

    return (
      <div>
        <h2>{isEditing ? 'Edit MCQ' : 'Create New MCQ'}</h2>
        <form onSubmit={handleSubmit}>
          <div>
            <label htmlFor="question">Question:</label>
            <input
              type="text"
              id="question"
              name="question"
              value={formData.question}
              onChange={handleInputChange}
              required
            />
          </div>
          <div>
            <label htmlFor="courseId">Course ID:</label> {/* Input for associating with a course */}
            <input
              type="text"
              id="courseId"
              name="courseId"
              value={formData.courseId}
              onChange={handleInputChange}
              required
            />
          </div>
          <div>
            <p>Options:</p>
            {formData.options.map((option, index) => (
              <div key={index}>
                <input
                  type="text"
                  value={option.text}
                  onChange={(e) => handleOptionChange(index, e)}
                  placeholder={`Option ${index + 1}`}
                  required
                />
                <input
                  type="radio"
                  name="correctAnswer"
                  checked={formData.correctAnswerId === option.id} // This will need adjustment when creating new options
                  onChange={() => handleCorrectAnswerChange(option.id)} // This will need adjustment
                /> Correct
              </div>
            ))}
            {/* Logic to add/remove options can be added here */}
          </div>
          <button type="submit">Save MCQ</button>
        </form>
      </div>
    );
  };

  export default MCQForm;
  ```

- __Action:__ Create this file with the provided content. Note that handling the `correctAnswerId` for *new* options will require generating temporary IDs or a different approach in the frontend before saving to the backend.

__Step 7: Integrate CMS Components into Pages__

- __Task:__ Add the `MCQList` and `MCQForm` components to relevant pages in the CMS.
- __Files:__ This will depend on your CMS routing and page structure. You might create a new page component like `cms/src/pages/MCQManagementPage.jsx` and add routes for `/mcqs` (list) and `/mcqs/:id` (edit) or `/mcqs/new` (create).
- __Action:__ Modify your CMS routing and page components to include the new MCQ components.

__Phase 3: LMS Integration__

__Step 8: Implement LMS MCQ Display__

- __Task:__ Create components in the LMS to fetch and display MCQs for students.

- __File:__ `lms/src/components/Quiz/MCQDisplay.jsx` (suggested)

- __Code Suggestion (`lms/src/components/Quiz/MCQDisplay.jsx` - basic structure):__

  ```javascript
  import React, { useEffect, useState } from 'react';
  import axios from 'axios'; // Assuming axios is used in LMS as well

  const MCQDisplay = ({ mcqId }) => {
    const [mcq, setMcq] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
    const [selectedOption, setSelectedOption] = useState(null);

    useEffect(() => {
      const fetchMCQ = async () => {
        try {
          const response = await axios.get(`/api/mcqs/${mcqId}`); // Adjust API path
          setMcq(response.data);
        } catch (err) {
          setError(err);
        } finally {
          setLoading(false);
        }
      };
      fetchMCQ();
    }, [mcqId]);

    const handleOptionSelect = (optionId) => {
      setSelectedOption(optionId);
      // You might want to store the selected answer in parent component state
    };

    if (loading) return <p>Loading question...</p>;
    if (error) return <p>Error loading question: {error.message}</p>;
    if (!mcq) return <p>Question not found.</p>;

    return (
      <div>
        <h3>{mcq.question}</h3>
        <ul>
          {mcq.options.map(option => (
            <li key={option.id}>
              <label>
                <input
                  type="radio"
                  name={`mcq-${mcq.id}`}
                  value={option.id}
                  checked={selectedOption === option.id}
                  onChange={() => handleOptionSelect(option.id)}
                />
                {option.text}
              </label>
            </li>
          ))}
        </ul>
        {/* Add logic to check answer or submit quiz */}
      </div>
    );
  };

  export default MCQDisplay;
  ```

- __Action:__ Create this file and integrate it into your LMS quiz or content pages, passing the relevant `mcqId`.

__Phase 4: Refinement and Enhancement__

__Step 9: Implement Validation and Error Handling__

- __Task:__ Add detailed input validation on both frontend and backend. Implement robust error handling.

- __Action:__

  - Enhance validation in `MCQForm.jsx` before submitting data.
  - Add validation logic in `MCQController.ts` (e.g., using a validation library or manual checks).
  - Implement error display in CMS components (e.g., showing validation messages to the user).
  - Add more detailed error logging and handling on the backend.

__Step 10: Implement Testing__

- __Task:__ Write tests for the backend and frontend code.

- __Action:__

  - Set up testing frameworks if not already in place (e.g., Jest for backend/frontend, React Testing Library for frontend components).
  - Write unit tests for controller logic and repository interactions.
  - Write integration tests for API endpoints.
  - Write tests for React components to ensure they render correctly and handle interactions.

__Step 11: Refine LMS Integration__

- __Task:__ Build out the full quiz experience in the LMS.

- __Action:__

  - Develop components to manage a list of MCQs for a quiz or module.
  - Implement logic for submitting answers and displaying results.
  - Consider how to store student answers and quiz scores (this might require new backend entities and API endpoints).
