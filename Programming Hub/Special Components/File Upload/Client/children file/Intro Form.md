```js
import React, { useMemo, useRef, useState } from "react";

import { MdExpandLess, MdExpandMore } from "react-icons/md";

import ReactQuill from "react-quill";

import "react-quill/dist/quill.snow.css";

import axios from "./axiosConfig.js";

  

const IntroForm = ({

  introData,

  setIntroData,

  isLoading = false,

  handleSubmit,

}) => {

  const [isCollapsed, setIsCollapsed] = useState(true);

  const [selectedFile, setSelectedFile] = useState(null);

  const quillRef = useRef(null); // To access Quill instance

  

  // Handle input changes and update the introData

  const handleChange = (e) => {

    const { name, value } = e.target;

    setIntroData((prevData) => ({

      ...prevData,

      [name]: value,

    }));

  };

  

  const handleDescriptionChange = (value) => {

    // Only update description without resetting entire introData

    setIntroData((prevData) => ({

      ...prevData,

      description: value,

    }));

  };

  

  const toggleCollapse = () => {

    setIsCollapsed((prevCollapsed) => !prevCollapsed);

  };

  

  const handleFileChange = (e) => {

    setSelectedFile(e.target.files[0]);

  };

  

  const handleFormSubmit = (e) => {

    e.preventDefault();

  

    const data = {

      ...introData,

      thumbnail_image_link: selectedFile,

      description: introData.description, // Keep description synced

    };

  

    handleSubmit(data);

  };

  

  const handleImageHandler = () => {

    const input = document.createElement("input");

    input.setAttribute("type", "file");

    input.setAttribute("accept", "image/*");

    input.click();

  

    input.onchange = async () => {

      const file = input.files[0];

      const formData = new FormData();

      formData.append("image", file);

  

      try {

        const response = await axios.post(`/des-image`, formData, {

          headers: {

            "Content-Type": "multipart/form-data",

          },

        });

  

        const imageUrl = response.data.url;

        const quill = quillRef.current.getEditor();

        const range = quill.getSelection(true);

  

        // Insert the image

        quill.insertEmbed(range.index, "image", imageUrl);

        // Move the cursor to the next position after the image

        quill.setSelection(range.index + 1, 0);

        // Insert the image URL as text

        quill.insertText(range.index + 1, imageUrl + "\n");

      } catch (error) {

        console.error("Image upload failed:", error);

      }

    };

  };

  

  const modules = useMemo(

    () => ({

      toolbar: {

        container: [

          [{ header: "1" }, { header: "2" }, { font: [] }],

          [{ size: [] }],

          ["bold", "italic", "underline", "strike", "blockquote"],

          [{ list: "ordered" }, { list: "bullet" }],

          ["link", "image"], // Add image button here

          ["clean"],

        ],

        handlers: {

          image: handleImageHandler, // Custom image handler

        },

      },

    }),

    []

  );

  

  const formats = useMemo(

    () => [

      "header",

      "font",

      "size",

      "bold",

      "italic",

      "underline",

      "strike",

      "blockquote",

      "list",

      "bullet",

      "link",

      "image",

    ],

    []

  );

  

  return (

    <div className="w-full mt-8">

      <div

        className="flex justify-between items-center bg-[rgb(114,127,148)] p-2 rounded-t-lg cursor-pointer"

        onClick={toggleCollapse}

      >

        <h2 className="text-2xl text-white font-semibold">

          Add Materials - Intro

        </h2>

        <button className="text-sm text-gray-500 focus:outline-none">

          {isCollapsed ? (

            <MdExpandMore className="text-2xl" />

          ) : (

            <MdExpandLess className="text-2xl" />

          )}

        </button>

      </div>

  

      {!isCollapsed && (

        <div className="bg-white p-4 rounded-lg shadow-md w-full">

          <form onSubmit={handleFormSubmit}>

            <div className="grid grid-cols-1 md:grid-cols-2 gap-4 w-full">

              {/* Thumbnail Video Link */}

              <div>

                <label

                  className="block text-gray-700 text-sm font-bold mb-1"

                  htmlFor="thumbnail_video_link"

                >

                  Thumbnail Video Link

                </label>

                <input

                  type="text"

                  id="thumbnail_video_link"

                  name="thumbnail_video_link"

                  value={introData.thumbnail_video_link}

                  onChange={handleChange}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                  placeholder="Enter video link"

                />

              </div>

  

              {/* Thumbnail Image Link */}

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

                  accept="image/jpeg, image/png"

                  onChange={handleFileChange}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                />

              </div>

  

              {/* Title */}

              <div>

                <label

                  className="block text-gray-700 text-sm font-bold mb-1"

                  htmlFor="title"

                >

                  Title

                </label>

                <input

                  type="text"

                  id="title"

                  name="title"

                  value={introData.title}

                  onChange={handleChange}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                  placeholder="Enter title"

                />

              </div>

  

              {/* Subtitle */}

              <div>

                <label

                  className="block text-gray-700 text-sm font-bold mb-1"

                  htmlFor="sub_title"

                >

                  Sub Title (200 chars max)

                </label>

                <input

                  type="text"

                  id="sub_title"

                  name="sub_title"

                  value={introData.sub_title}

                  onChange={handleChange}

                  maxLength={200}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                  placeholder="Enter subtitle"

                />

              </div>

  

              {/* Live Class Link */}

              <div>

                <label

                  className="block text-gray-700 text-sm font-bold mb-1"

                  htmlFor="live_class_link"

                >

                  Live Class Link

                </label>

                <input

                  type="text"

                  id="live_class_link"

                  name="live_class_link"

                  value={introData.live_class_link}

                  onChange={handleChange}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                  placeholder="Enter live class link"

                />

              </div>

  

              {/* Recording Link */}

              <div>

                <label

                  className="block text-gray-700 text-sm font-bold mb-1"

                  htmlFor="recording_link"

                >

                  Recording Link

                </label>

                <input

                  type="text"

                  id="recording_link"

                  name="recording_link"

                  value={introData.recording_link}

                  onChange={handleChange}

                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"

                  placeholder="Enter recording link"

                />

              </div>

  
              {/* Recap Link */}
              <div>
                <label
                  className="block text-gray-700 text-sm font-bold mb-1"
                  htmlFor="recap_link"
                >
                  Recap Link
                </label>
                <input
                  type="text"
                  id="recap_link"
                  name="recap_link"
                  value={introData.recap_link}
                  onChange={handleChange}
                  className="w-full shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                  placeholder="Enter recap link"
                />
              </div>
            </div>

  
            {/* Description Editor */}
            <div className="mt-4">
              <label
                className="block text-gray-700 text-sm font-bold mb-1"
                htmlFor="description"
              >
                Description
              </label>
              <ReactQuill
                ref={quillRef}
                value={introData.description}
                onChange={handleDescriptionChange}
                modules={modules}
                formats={formats}
              />
            </div>

  
            {/* Submit Button */}
            <div className="flex justify-start mt-6">
              <button
                type="submit"
                disabled={isLoading}
                className="bg-gray-500 hover:bg-gray-600 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              >
                {isLoading ? "Saving..." : "Save Changes"}
             </button>
            </div>
          </form>
        </div>
      )}
    </div>
  );
};

  

export default IntroForm;
```