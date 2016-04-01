This repo extends the [FSL Community BSP](https://github.com/Freescale/fsl-community-bsp-platform)
with an additional [Yocto](https://www.yoctoproject.org/) layer to support the i.MX6 based [MarS Board](http://www.embest-tech.com/shop/star/marsboard.html)

Full docs are in the [wiki](https://github.com/FrankBau/meta-marsboard-bsp/wiki)


Test Setup
==========
Board connected via USB to a linux host using minicom.
`image-multimedia-full` boots from the microSD card

Test Cases
==========

Video Playback on HDMI
----------------------
A 1080p clip is played (audio+video) on HDMI with sound with about 5% CPU load:

`gst-play-1.0 data/big_buck_bunny_1080p_h264.mp4`

Video Recording from USB Webcam
-------------------------------
An UVC compliant webcam with motionJPEG output was used (Microsoft LifeCam Studio).
The video stream is re-coded in H.264 and wrapped in an good old .avi container.
The .avi file can be viewed using gst-play-1.0 cam.avi.

`gst-launch-1.0 v4l2src device=/dev/video0 ! 'image/jpeg,width=640,height=480' ! imxvpudec ! imxipuvideotransform ! imxvpuenc_h264 ! avimux ! filesink location=cam.avi`

