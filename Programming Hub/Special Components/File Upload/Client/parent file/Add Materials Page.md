```js
import { useState } from "react";
import toast from "react-hot-toast";
import { useParams } from "react-router-dom";
import axios from "./axiosConfig.js";
import IntroForm from "./IntroForm";
import ResourceSection from "./ResourceSection";
  

const AddMaterialPage = () => {
  const [activeTab, setActiveTab] = useState("intro");
  const [isLoading, setIsLoading] = useState(false);
  const { classId } = useParams();

  const [introData, setIntroData] = useState({
    thumbnail_video_link: "",
    thumbnail_image_link: "",
    title: "",
    sub_title: "",
    description: "",
    live_class_link: "",
    recording_link: "",
    recap_link: "",
  });

    const handleSubmit = async (introData) => {
    if (!classId) {
      console.error("Class ID is not available.");
      return;
    }
    setIsLoading(true);

    try {
      // Payload with the extracted classId
      const introDataPayload = {
        ...introData,
        isactive: true,
        ispublic: true,
        classId: classId, // Use the classId from the URL
      };

      const response = await axios.post(`/intro`, introDataPayload, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      });
      console.log("Intro Res:", response.data);
      toast.success("Successfully created!");
      setIsLoading(false);
      setIntroData({
        thumbnail_video_link: "",
        thumbnail_image_link: "",
        title: "",
        sub_title: "",
        description: "",
        live_class_link: "",
        recording_link: "",
        recap_link: "",
      });
    } catch (error) {
      console.error("There was a problem with the submission:", error);
      setIsLoading(false);
    }
  };
  

  return (
    <div className="min-h-screen p-6 bg-gray-100">
      {/* Tab buttons */}
      <div className="flex items-start justify-start mb-6 space-x-2">
        <button
          className={`py-2 px-4 text-sm font-semibold border border-gray-300 shadow-sm rounded-lg focus:outline-none focus:ring-2 focus:ring-gray-500 focus:border-gray-500 ${
            activeTab === "intro"
              ? "bg-gray-500 border-gray-500 text-white"
              : "bg-white border-gray-300 text-gray-600"
          }`}
          onClick={() => setActiveTab("intro")}
        >
          Intro
        </button>
        <button
          className={`py-2 px-4 text-sm font-semibold border border-gray-300 shadow-sm rounded-lg focus:outline-none focus:ring-2 focus:ring-gray-500 focus:border-gray-500 ${
            activeTab === "resources"
              ? "bg-gray-500 border-gray-500 text-white"
              : ""
          }`}
          onClick={() => setActiveTab("resources")}
        >
          Resources
        </button>
      </div>

  

      {/* Tab content */}
      <div className="mt-6">
        {activeTab === "intro" && (
          <div className="bg-white rounded-lg shadow-sm p-4">
            <IntroForm
              introData={introData}
              setIntroData={setIntroData}
              handleSubmit={handleSubmit}
              isLoading={isLoading}
            />
          </div>
        )}
 

        {activeTab === "resources" && (
          <div className="bg-white rounded-lg shadow-sm p-4">
            <ResourceSection />
          </div>
        )}
      </div>
    </div>
  );
};

  
export default AddMaterialPage;
```