### Structural Hierarchy
![[deepseek_mermaid_20250515_20dc02.png]]


### Attempt Tracking
![[deepseek_mermaid_20250515_043c46.png]]


![[Pasted image 20250515083555.png]]



## System Architecture

![[deepseek_mermaid_20250515_613895.png]]



## Core Entities

### Entity Relationships
![[deepseek_mermaid_20250515_957ac3.png]]


### Database Schema

**Quizzes Table**
```sql

CREATE TABLE quizzes (  
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),  
    title TEXT NOT NULL,  
    created_at TIMESTAMPTZ DEFAULT NOW()  
);  

CREATE TABLE questions (  
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),  
    quiz_id UUID REFERENCES quizzes(id) ON DELETE CASCADE,  
    text TEXT NOT NULL,  
    type VARCHAR(7) CHECK (type IN ('single', 'multiple')),  
    points DECIMAL NOT NULL  
);  

CREATE TABLE options (  
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),  
    question_id UUID REFERENCES questions(id) ON DELETE CASCADE,  
    text TEXT NOT NULL,  
    is_correct BOOLEAN NOT NULL  
);  
```



## API Endpoints

### Admin Endpoints (CMS)

| Method | Endpoint        | Description     |
| ------ | --------------- | --------------- |
| POST   | `/quizzes`      | Create new quiz |
| PUT    | `/quizzes/{id}` | Update quiz     |
| DELETE | `/quizzes/{id}` | Delete quiz     |

**Full Quiz Creation Endpoint**
```json
{
  "id": "quiz_001",
  "title": "Web Development Fundamentals Quiz",
  "created_at": "2024-03-15T09:00:00Z",
  "questions": [
    {
      "id": "q1",
      "text": "Which of these are valid HTML elements?",
      "type": "multiple",
      "points": 2,
      "options": [
        {
          "id": "q1_o1",
          "text": "<div>",
          "is_correct": true
        },
        {
          "id": "q1_o2",
          "text": "<span>",
          "is_correct": true
        },
        {
          "id": "q1_o3",
          "text": "<container>",
          "is_correct": false
        },
        {
          "id": "q1_o4",
          "text": "<section>",
          "is_correct": true
        }
      ],
      "explanation": "HTML5 introduced semantic elements like <section>"
    },
  ],
  "scoring_rules": {
    "multiple_answers": "partial",
    "negative_marking": false,
    "time_limit": 1800
  }
```

###  Student Endpoints (LMS)

| Method | Method          | Description         |
| ------ | --------------- | ------------------- |
| GET    | `/quizzes/{id}` | Get quiz details    |
| POST   | `/attempts`     | Submit quiz attempt |



## Permission Model
### 5.1 Access Control
```javascript
const permissions = {
  admin: {
    courses: ['create', 'read', 'update', 'delete'],
    quizzes: ['create', 'read', 'update', 'delete'],
    content: ['full_access']
  },
  student: {
    courses: ['read'],
    quizzes: ['read', 'attempt'],
    content: ['read']
  }
};
```
