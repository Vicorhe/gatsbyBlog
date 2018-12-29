---
title: How to Take Consistent Images with an Industrial Camera
category: "computer vision"
cover: consistent_thumbnail.jpg
---

This guide doesn’t just apply to industrial cameras, so long as the camera allows you to fine tune certain parameters discussed bellow.

Most cameras nowadays come with some degree of ‘smart’ adjustments. These adjustments are meant to optimize the image in real time. Some of the automatic adjustments made are exposure time, white balance, ISO or analog gain, and aperture settings.

Camera sensors consist of sensor elements that are analog components that build up charge as more photons hit them. There is a reset and read operation on these sensors. Exposure time is the time allotted to read the entire frame. Exposure time is adjusted to account for the overall lighting level of the picture you intend to take. Lower ambient lighting levels will require longer exposure times to get a decently lit image.

White balance is made to account for the biases in the lighting source of your target, to create a more true to sight image. For example, in reef aquarium photography, the common light sources are LED or T5 fluorescents fixtures which emit a drowning blue hue allowing coral colors to pop. This heavy bias in the blue spectrum often requires white balancing in order to not take a completely blue image while preserving the vivid coral colors. 

ISO and analog gain control the light sensitivity of the camera sensor. The cost of higher sensitivity is degraded images which show more grain. The smaller ISO ratings required more light, but had a finer grain and created better images. Larger ISO numbers required much less light, but looked grainy. Higher quality images required a low ISO rating. ISO and gain are for all practical purposes the same thing. So there’s little point in adjusting both of them. Choose one. 

Some cameras allow for a digital adjustment of aperture. In the case of typical industrial cameras, aperture isa adjusted manually on the lenses. Aperture controls the amount of light passing through to the sensor by control the area of passage in the middle of lens. Lower aperture means more light is allowed through, and the main effects are lower depth of field and brighter images. Higher aperture means less light is allowed through, and the main effects are greater depth of field and darker images. The brightness effects are presented assuming that all other factors are held constant. 

Consequently, modern cameras often tailor the camera parameters to the specific snap shot, leading to differences between images of the same objects just fractions of a second apart. Two images, meant to be identical, may have different camera parameters and, subsequently, slight differences in image quality.

This becomes an issue when your task is to classify images based on minute color differences. For instance, a slight shift exposure time to lead to capturing a brighter or darker image, resulting in a color difference sufficient to overpower the difference in colors between color shades.

Therefore it is vital that we control camera parameters to ensure consistent images across snap shots and across operation time shifts.

How does one take consistent images?
- disable auto exposure, fix exposure time
- disable auto white balance, fix white balance
- disable exposure modes (if applicable), fix ISO or analog gain (if the option is available) 
- fix aperture
- fix image capturing peripherals, light source, working distance, ect.

As to which values to set the camera parameters to, that depends on your use case and should involve rigorous testing. 

It’s a good strategy to query the results of the auto-XXX procedures and then fix those values from now on.

Here are some additional pointers that may help:
- For ISO, a simple rule of thumb is that 100 and 200 are reasonable values for daytime, while 400 and 800 are better for low light. 
- To determine a reasonable value for exposure time you can query the exposure time attribute for as a result of auto exposure.
- To fix the white balance, apply white balance once from your built in camera operation, remember the red gain, green gain, and blue gain, then set each of these gains accordingly. (Note: this is how my MindVision industrial camera handles white balance.),
- If you are looking for an affordable industrial camera alternative, try the picamera module for raspberry pi, it offers all the above degree of controllability and even more detailed guides at their official docs.

