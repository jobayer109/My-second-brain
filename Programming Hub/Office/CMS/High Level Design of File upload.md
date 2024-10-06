
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