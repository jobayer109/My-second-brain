
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
const fs = require('fs');
const app = express();

// Set up multer for file uploads
const upload = multer({
  dest: './uploads/', // Temporary upload directory
  limits: { fileSize: 10 * 1024 * 1024 }, // 10 MB file size limit
});

app.post('/upload-thumbnail-image', upload.single('thumbnail_image_link'), (req, res) => {
  try {
    const file = req.file;
    const filePath = file.path;
    const fileOriginalName = file.originalname;
    const fileExtension = fileOriginalName.split('.').pop();

    // Generate a unique filename
    const uniqueFilename = `${Date.now()}.${fileExtension}`;

    // Move the file to a permanent storage location
    const permanentStoragePath = `./uploads/${uniqueFilename}`;
    fs.renameSync(filePath, permanentStoragePath);

    // Return the URL of the uploaded image
    const imageUrl = `http://localhost:3000/uploads/${uniqueFilename}`;
    res.json({ url: imageUrl });
  } catch (error) {
    console.error('Error uploading image:', error);
    res.status(500).json({ error: 'Failed to upload image' });
  }
});

// Serve static files from the uploads directory
app.use('/uploads', express.static('uploads'));

app.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});

```