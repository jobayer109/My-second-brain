
# Frontend

### Input Field
```html
<div>
  <label
    className="block text-gray-700 text-sm font-bold mb-1"
    htmlFor="thumbnail_image_link"
  >
    Thumbnail Image
  </label>
  <input
    type="file"
    id="thumbnail_image_link"
    name="thumbnail_image_link"
    onChange={handleThumbnailImageChange}
    className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
  />
</div>
```

### HTTP POST Request:
```js
const handleThumbnailImageChange = (e) => {
  const file = e.target.files[0];
  const formData = new FormData();
  formData.append("thumbnail_image_link", file);
  
  // Post the image to the backend
  axios
    .post("/upload-thumbnail-image", formData)
    .then((response) => {
      setIntroData((prevState) => ({
        ...prevState,
        thumbnail_image_link: response.data.url,
      }));
    })
    .catch((error) => {
      console.error("Error uploading thumbnail image:", error);
    });
};

```

# Backend (Express)
```js
const express = require('express');
const multer = require('multer');
const app = express();

// Set up multer for file storage
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, './uploads/'); 
  },
  filename: (req, file, cb) => {
    cb(null, Date.now() + '-' + file.originalname); 
  },
});

const upload = multer({ storage: storage });

app.post('/upload-thumbnail-image', upload.single('thumbnail_image_link'), (req, res) => {
  try {
    const file = req.file;

    const imageUrl = `http://localhost:3000/uploads/${file.filename}`;
    res.json({ url: imageUrl });
  } catch (error) {
    console.error('Error uploading image:', error);
    res.status(500).json({ error: 'Failed to upload image' });
  }
});


