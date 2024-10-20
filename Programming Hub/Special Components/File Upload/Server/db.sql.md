```js
-- Create database
CREATE DATABASE cmsDB

  
  

-- Create intro table

CREATE TABLE intro (
  id VARCHAR(255) PRIMARY KEY,
  classId INTEGER,
  title VARCHAR(255),
  sub_title TEXT,
  thumbnail_video_link VARCHAR(255),
  thumbnail_image_link VARCHAR(255),
  live_class_link VARCHAR(255),
  recording_link VARCHAR(255),
  recap_link VARCHAR(255),
  description TEXT,
  isactive BOOLEAN,
  ispublic BOOLEAN
);

```

