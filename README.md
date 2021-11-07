# What is ZIGCAM
ZIGCAM is an application for iOS and PadOS.
ZIGCAM can use NDI to send the camera's video and various associated information to other devices such as a PC.
This allows you to treat your iPhone or iPad like a device with a camera and sensors (e.g. Kinect).

# Version
All information below is written for version 1.0.4.  
Since ZIGCAM is currently being updated frequently, please make sure that the version of ZIGCAM you are using matches the documentation.  
  
# Data
* Camera Image (2D Color Image)
* Depth Image
* People Segmantion Mask
* WorldTracking Data
* Face Tracking Data
* Body Tracking Data
  
Some data can be sent simultaneously.
Image data is sent in NDI, and numeric data is attached and sent in XML format as MetaData in NDI.
NDI Meta data is attached frame by frame and there is no delay.
  
# Devices Support
We strongly recommend iPhones and iPads with LiDAR-equipped A12 or higher chips.
As of November 2021, the following devices are recommended.
  
* iPad PRO 11 inch (2nd gen)
* iPad PRO 11 inch (3rd gen)
* iPad PRO 12.9 inch (4th gen)
* iPad PRO 12.9 inch (5th gen)
* iPhone 12 PRO / PRO MAX
* iPhone 13 PRO / PRO MAX

# Environment
Due to the specification of NDI, the device that uses ZIGCAM and the device that receives the data must be on the same network.  
Although it is possible to use NDI over Wifi, it is recommended to use a wired connection since NDI is very bandwidth intensive.  
  
# Operation
ZIGCAM is very simple and has only two screens.
The first screen shows a preview of the camera, and you can simply press the "Send NDI" button at the bottom. The NDI will now be sent.  
The second screen is the settings screen, which can be accessed by clicking the "Settings" button at the top of the first screen.  
There are several settings, some of which are not available at the same time due to iOS specifications, so there are some buttons and parameters that become unavailable each time you change the settings.  

## Tracking Mode
Select the tracking mode. Currently, there are three modes to choose from.  
## Set Depth Image
Allows you to set whether or not to include depth image in the data to be sent. There is a fee.  
## Set People Segm Image
You can set whether or not to include People Segmentation image in the data you send. There is a fee.  
## Depth Type
In World Tracking, you can choose whether to use LiDAR or predictive data from machine learning to create depth images.  
This option is only available for LiDAR-equipped models.  
## Set Image In
You can choose whether to use the alpha channel or tiling when sending Depth or People Segmentation images.  
## Image Scale
Set the data size to be sent. This is an item to be set as a percentage. Thus, 100 means you can send the full size.  
However, bandwidth is usually an issue, so we recommend setting a smaller size, 50% or less.  
## Depth Scale
The compression rate of Depth.  
Normal Depth images are acquired at 32 bits, but NDI can only handle 8-bit images, so there will be clipping when using the alpha channel. 1 saves the image at full size, but values greater than 1 meter will be clipped.  
## Clip Near
Sets the Clip Near for World Tracking.
## Clip Far
Sets the Clip Far for World Tracking.
## Detect Horizonal Plane
You can set whether or not horizontal planes are also detected in World Tracking mode.  
If they are detected, they will be added to the NDI Metadata.  
## Detect Vertical Plane
You can set whether or not Vertical planes are also detected in World Tracking mode.  
If they are detected, they will be added to the NDI Metadata.  

