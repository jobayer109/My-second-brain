### Possible data structure:
```json
{
  "id": "unique_mcq_id",
  "question": "The text of the question",
  "options": [
    {"id": "option_a_id", "text": "Option A text"},
    {"id": "option_b_id", "text": "Option B text"},
    {"id": "option_c_id", "text": "Option C text"},
    {"id": "option_d_id", "text": "Option D text"}
  ],
  "correctAnswerId": "id_of_the_correct_option"
}

```

---

### CMS Component Development (CRUD):
I will need to create React components within the CMS to handle the CRUD operations for MCQs. This would likely involve:

- __MCQ List Component:__ To display a list of existing MCQs. This could be similar to the existing `ClassList` or `UserTable` components.
- __MCQ Form Component:__ To create new MCQs or edit existing ones. This form would need fields for the question text and multiple options, with a way to designate the correct answer. This could be similar to existing form components like `ClassForm` or `ResourceForm`.
- __MCQ Detail Component (Optional):__ A component to view a single MCQ in detail.

These components will need to interact with the shared backend API to perform the CRUD operations.

**CMS Component Development (CRUD Frontend):**

We will create React components in `pocketschool/src/components/` to handle the CRUD operations for MCQs.

- `MCQList.jsx`: To display a list of MCQs.
- `MCQForm.jsx`: To create and edit MCQs. This form will need to handle the question text, multiple options, and selecting the correct answer.

These components will use Axios to interact with the new backend API endpoints, likely utilizing the existing API service structure in `pocketschool/src/api/`.

---

### Backend Interaction:
Based on the frontend's `quizData.js` and the backend's TypeORM entity structure, we will define a new entity for MCQs. This entity will likely be named `MCQ` and will reside in `server/src/entity/MCQ.ts`. We will also create a separate entity for the options, `QuestionOption`, to manage the relationship effectively in the database.

```typescript
// server/src/entity/MCQ.ts
import { Entity, PrimaryGeneratedColumn, Column, OneToMany, ManyToOne } from 'typeorm';
import { QuestionOption } from './QuestionOption';
import { Course } from './Course'; 

@Entity()
export class MCQ {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  question: string;

  @OneToMany(() => QuestionOption, option => option.mcq)
  options: QuestionOption[];

  @Column('uuid') 
  correctAnswerId: string;

  @ManyToOne(() => Course, course => course.mcqs)
  course: Course;
}
```


```typescript
// server/src/entity/QuestionOption.ts
import { Entity, PrimaryGeneratedColumn, Column, ManyToOne } from 'typeorm';
import { MCQ } from './MCQ';

@Entity()
export class QuestionOption {
  @PrimaryGeneratedColumn('uuid')
  id: string;

  @Column()
  text: string;

  @ManyToOne(() => MCQ, mcq => mcq.options)
  mcq: MCQ;
}
```


The CMS components will use Axios (already a dependency) to make API calls to the shared backend. We will need to define the API endpoints for MCQs (e.g., `/api/mcqs`, `/api/mcqs/:id`). The CMS will send and receive MCQ data in the defined structure.

We will create a new controller for MCQs, likely named `MCQController.ts`, in the `server/src/controllers/` directory. This controller will expose API endpoints for CRUD operations on MCQs, following the pattern seen in existing controllers like `CourseController.ts`.

Endpoints will likely include:

- `GET /api/mcqs`: Get all MCQs (or potentially filtered by course ID)
- `GET /api/mcqs/:id`: Get a single MCQ by ID
- `POST /api/mcqs`: Create a new MCQ
- `PUT /api/mcqs/:id`: Update an existing MCQ
- `DELETE /api/mcqs/:id`: Delete an MCQ

---

### Integration with LMS 
The LMS will access the MCQ data through the same backend API endpoints defined in the `MCQController`. The data structure defined in the backend entities will serve as the contract for data exchange between the backend, CMS, and LMS.

__Proposed Next Steps in ACT MODE:__

1. Define and create the `MCQ` and `QuestionOption` entities in `server/src/entity/`.
2. Create the `MCQController.ts` in `server/src/controllers/` with the necessary CRUD endpoints.
3. Implement the repository methods for MCQs and QuestionOptions in `server/src/repositories/`.
4. Develop the `MCQList.jsx` and `MCQForm.jsx` components in `pocketschool/src/components/`.
5. Implement the API calls in the CMS components to interact with the new backend endpoints.
6. Integrate the new MCQ components into the relevant CMS pages.

---

 