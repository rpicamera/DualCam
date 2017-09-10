# DualCam
Dual Cameras system. Based on the mjpeg inherited from rpi-cam-web-interface. It gives an opportunity to set up a VR live system using raspberry Pi zero and Pi 3B. 

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
        patern = re.compile();
        filelist = patern.findall(string)
        filename = filelist[len(filelist)-1]
        rsp = urlopen(media_dir+filename)
        image = rsp.read()        
