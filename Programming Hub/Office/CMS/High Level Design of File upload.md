
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




