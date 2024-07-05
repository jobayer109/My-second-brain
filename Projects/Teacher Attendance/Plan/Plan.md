### Project Setup and Structure
```plaintext
teacher-attendance/
│
├── client/               // React Front-End
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── App.js
│   │   ├── index.js
│   └── package.json
│
├── server/               // Node.js Back-End
│   ├── config/
│   │   └── db.js        // MongoDB connection
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── app.js
│   └── package.json
│
├── .env                  // Environment variables
└── package.json          // Root package.json to manage scripts

```