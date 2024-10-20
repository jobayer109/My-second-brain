```js
const bodyParser = require("body-parser");
const cors = require("cors");
const express = require("express");
const multer = require("multer");
const pool = require("./db.js");
const { v4: uuidv4 } = require("uuid");
  
const app = express();

app.use(cors());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public"));

const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, "./public/uploads");
  },
  filename: (req, file, cb) => {
    const fileName = `${uuidv4()}-${file.originalname}`;
    cb(null, fileName);
  },
});
  

// File upload for description field_________________________________________

const upload = multer({ storage: storage });

  

app.post("/des-image", upload.single("image"), (req, res) => {

  const file = req.file;

  if (!file) {

    return res.status(400).json({ message: "No file uploaded" });

  }

  

  const imageUrl = `http://localhost:5000/uploads/${file.filename}`;

  res.status(200).json({ url: imageUrl });

});

  

// Intro post endpoint________________________________________________________

app.post("/intro", upload.single("thumbnail_image_link"), async (req, res) => {

  try {

    const { body, file } = req;

    console.log("file", file);

  

    const {

      classId,

      title,

      sub_title,

      thumbnail_video_link,

      live_class_link,

      recording_link,

      recap_link,

      description,

      isactive,

      ispublic,

    } = req.body;

  

    const id = uuidv4();

  

    const thumbnail_image_link = file

      ? `http://localhost:5000/uploads/${file.filename}`

      : body.thumbnailImageLink;

  

    const insertQuery = {

      text: `

        INSERT INTO intro (

          id,

          classId,

          title,

          sub_title,

          thumbnail_video_link,

          thumbnail_image_link,

          live_class_link,

          recording_link,

          recap_link,

          description,

          isactive,

          ispublic

        ) VALUES ($1, $2, $3, $4, $5, $6, $7, $8, $9, $10, $11, $12)

        RETURNING *

      `,

      values: [

        id,

        classId,

        title,

        sub_title,

        thumbnail_video_link,

        thumbnail_image_link,

        live_class_link,

        recording_link,

        recap_link,

        description,

        isactive,

        ispublic,

      ],

    };

    try {

      await pool.query(insertQuery);

    } catch (err) {

      console.error(err);

      return res.status(500).json({ message: "Error uploading file" });

    }

  

    res.json({

      message: "File uploaded successfully",

      body,

      file: file ? { ...file, thumbnail_image_link } : null,

    });

  } catch (err) {

    console.error(err);

    res.status(500).json({ message: "Error uploading file" });

  }

});

  

const port = 5000;

app.listen(port, () => {

  console.log(`Server started on port http://localhost:${port}`);

});
```