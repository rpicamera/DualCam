# DualCam
Dual Cameras system. Based on the mjpeg inherited from rpi-cam-web-interface. It gives an opportunity to set up a VR live system using raspberry Pi zero and Pi 3B. 

## Set up dual cam web interface

1: Install rpi-cam-web-interface in both Raspberry Pis, during the install, change the default name from 'html' to 'picam'.

2: Setup the dual pi system, then, copy the three files in this directory to /var/www/picam/  . 

3: Change the ip address. edit dualcam.html with sudo, change the ip address on line 24. 

4: Test the page: http://<ip>/picam/dualcam.html  it should show two live images. 

## get image from slave side by Python

1.  take image using FIFO from RPi_cam_web_interface

        import requests
        requests.get("http://raspberrypi.local/picam/cmd_pipe.php?cmd=im");

2:  download the image
        
        from urllib import urlopen
        import re
        media_dir = 'http://raspberrypi.local/picam/media/'
        urlpath = urlopen(media_dir)
        string = urlpath.read().decode('utf-8')
        patern = re.compile('([^\"\']*\.jpg)');
        filelist = patern.findall(string)
        filename = filelist[len(filelist)-4]
        rsp = urlopen(media_dir+filename)
        image = rsp.read()        
