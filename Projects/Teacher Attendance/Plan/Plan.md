### Project structure
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

---
## Packages
#### Front-end (React.js)
- [ ] `npx create-react-app .`
- [ ] `npm install react react-dom`
- [ ] `npm install axios`
- [ ] `npm install firebase`
- [ ] `npm install qrcode.react`
- [ ] `npm install react-qr-reader`


#### Back-end (Node.js & Express.js)
- [ ] `npm install express`
- [ ] `npm install mongoose`
- [ ] `npm install cors`
- [ ] `npm install body-parser`
- [ ] `npm install dotenv`
- [ ] `npm install jsonwebtoken`
- [ ] `npm install bcrypt`
- [ ] `npm install -g nodemon`
- [ ] `npm install concurrently` // To run both the front-end and back-end simultaneously