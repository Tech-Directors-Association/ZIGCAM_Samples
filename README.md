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
![This is an image](/assets/images/00_main_settings.png)
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

# How to read metadata
You can easily read NDI data, but you may not be able to easily read about NDI metadata.  
However, TouchDesigner and other programs provide an environment for easy reading.  
Check the official NDI documentation to see where the NDI metadata is located on the data.  
NDI's metadata is specified by its developer, NewTek, as XML plain text.  

```xml
<info>
    <app>ZIGCAM</app>
    <ver>1.0.4</ver>
    <time>471821.8482</time>
    <frame>2472</frame>
    <ndi_frame>2425</ndi_frame>
</info>
<settings>
    <tracking_mode>0</tracking_mode>
    <use_depth>1</use_depth>
    <use_pseg>1</use_pseg>
    <depth_type>0</depth_type>
    <set_img>1</set_img>
</settings>
<img_size>
    <color_size>960,720</color_size>
    <depth_size>128,96</depth_size>
    <depth_scale>10.0000</depth_scale>
    <pseg_size>96,128</pseg_size>
</img_size>
<worldtrack>
    <t>-0.4301,-0.2097,-0.3692</t>
    <r>45.9087,-148.4460,0.0154</r>
    <h_fov>64.4967</h_fov>
    <v_fov>50.6455</v_fov>
    <p_mat1>1.5850,0.0000,0.0000,0.0000</p_mat1>
    <p_mat2>0.0000,2.1133,0.0000,0.0000</p_mat2>
    <p_mat3>0.0042,-0.0060,-1.0000,-1.0000</p_mat3>
    <p_mat4>0.0000,0.0000,-0.0010,0.0000</p_mat4>
    <planes>
        <id>0</id>
        <t>0.0383,0.0000,0.0479</t>
        <s>0.7758,0.0000,0.3927</s>
        <id>1</id>
        <t>0.0150,0.0000,0.1480</t>
        <s>0.6020,0.0000,1.1341</s>
        <id>2</id>
        <t>0.0732,0.0000,0.2034</t>
        <s>2.0988,0.0000,0.9925</s>
        <id>3</id>
        <t>-0.1006,0.0000,0.0559</t>
        <s>1.0062,0.0000,0.7826</s>
        <id>4</id>
        <t>-0.0671,0.0000,0.0112</t>
        <s>0.5814,0.0000,0.6037</s>
        <id>5</id>
        <t>-0.0155,0.0000,0.0372</t>
        <s>0.6512,0.0000,0.3721</s>
    </planes>
</worldtrack>
```
There are a lot of them, so I'll just scratch the surface.  

## info
Basic information about ZIGCAM is available here.  
Name, version name, number of NDI frames and which frames on the device were captured.  
This block will always be sent.  
## settings
The settings at the time of ZIGCAM transmission are recorded.  
The "tracking_mode" is an enum containing the tracking mode set in ZIGCAM's Settings: 0 for "WolrdTracking", 1 for "FaceTracking", and 2 for "BodyTracking".  
"set_img" is a way to store additional information; 0 means the data is sent using the alpha channel, 1 means the data is sent using tiling.  
This block will always be sent.  

## img_size
The size of each image is described.  
This tag is only sent when tiling is used.  
## worldtrack
World Tracking information. This tag will be sent only when "World Tracking" is set.  
## facetrack
Face Tracking information. This tag will be sent only when "Face Tracking" is set.  
## bodytrack
Body Tracking information. This tag will be sent only when "Body Tracking" is set.  
  
# ARKit Space Environment
ARKit is Y-up.  
And ARKit's rotation order is Z-X-Y.  

