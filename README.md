# What is ZIGCAM?
ZIGCAM is an application for iOS and PadOS.
ZIGCAM can use NDI to send the camera's video and various associated information to other devices such as a PC.
This allows you to treat your iPhone or iPad like a device with a camera and sensors (e.g. Kinect).
  
# What kind of data can be transmitted?
* Camera Image (2D Color Image)
* Depth Image
* People Segmantion Mask
* WorldTracking Data
* Face Tracking Data
* Body Tracking Data
  
Some data can be sent simultaneously.
Image data is sent in NDI, and numeric data is attached and sent in XML format as MetaData in NDI.
NDI Meta data is attached frame by frame and there is no delay.
  
## What devices does it support?
We strongly recommend iPhones and iPads with LiDAR-equipped A12 or higher chips.
As of November 2021, the following devices are recommended.
  
* iPad PRO
* iPhone 12 PRO / PRO MAX
* iPhone 13 PRO / PRO MAX
  
