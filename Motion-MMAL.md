---
layout: post
title: "raspberrypi-cctv"
slug: "raspi-cctv"
date: 2016-10-07 01:00:00 +0900
categories: blog
---



## Motion-MMAL

### camera test

카메라 테스트

- raspistill -v -o

사진찍기

- raspistill -v -o xxx.jpg

동영상 녹화

- raspivid -t 5000 -o xxx.h264

아래 명령으로 motion 을 설치

- sudo apt-get install motion

설치가 끝나면 아래 명령으로 motion 패키지를 삭제

- sudo apt-get remove motion

- wget <https://www.dropbox.com/s/0gzxtkxhvwgfocs/motion-mmal.tar.gz>

- tar -zxvf motion-mmal.tar.gz

설정 파일을 수정

- sudo nano motion-mmalcam.conf

데몬 설정

- daemon on

이미지 회전 설정 (기울어져서 보이는 경우 수평을 맞추는 작업, 0-90-180-270 중 선택)

- rotate 0

Image resolution 640×480 (이미지 해상도가 높으면 끊김, 시스템 불안정의 원인이 될 수 있음)

- width 640

이미지 캡쳐 (동작이 감지되면 이미지를 저장)

- output_pictures off

비디오 포맷으로 저장

- ffmpeg_output_movies off

모든 네트웍에서 접근이 가능하도록 설정

- stream_localhost off

Motion 실행합니다.

- sudo ./motion -c motion-mmalcam.conf

브라우져 접속

- http://Your_RPi_IP_Address:8081

http://www.softpedia.com/get/Internet/Other-Internet-Related/Motion-JPEG-Player.shtml

### Motion을 데몬(백그라운드 서비스)로 실행

- sudo cp motion /usr/bin/
- sudo cp motion-mmalcam.conf /etc/motion/
- sudo nano /etc/default/motion
  데몬 설정을 yes 로 수정
- sudo service motion start
- sudo service motion stop

###  libavformat.so.53: cannot open

```
sudo apt-get install libavformat-dev
apt-cache search libavformat
sudo apt-get install libpq-dev
```



### So what you need to do is the following; first install all dependencies manually: 

```
sudo apt-get install -y libjpeg-dev libavformat56 libavformat-dev libavcodec56 libavcodec-dev libavutil54 libavutil-dev libc6-dev zlib1g-dev libmysqlclient18 libmysqlclient-dev libpq5 libpq-dev
```



### Then download and untar this modified Motion release: 

```
wget https://www.dropbox.com/s/6ruqgv1h65zufr6/motion-mmal-lowflyerUK-20151114.tar.gz
tar -zxvf motion-mmal-lowflyerUK-20151114.tar.gz
```



### And then to start the program, run: 

```
sudo ./motion -c motion-mmalcam-both.conf
```





```
sudo raspi-config
```



```
sudo nano /etc/default/motion
```



```
sudo nano /etc/modules
```

### Enter the following line at the bottom of the file if it doesn’t already exist, once done save & exit by pressing ctrl+x then y.

```
bcm2835-v4l2
```

`sudo` `modprobe bcm2835-v4l2` 



---

[https://motion-project.github.io/](https://motion-project.github.io/)

[https://github.com/dozencrows/motion/tree/mmal-test](https://github.com/dozencrows/motion/tree/mmal-test)

[https://embeddedday.com/projects/raspberry-pi/a-step-further/install-motion-mmal/](https://embeddedday.com/projects/raspberry-pi/a-step-further/install-motion-mmal/)

[https://pimylifeup.com/raspberry-pi-webcam-server/comment-page-2/](https://pimylifeup.com/raspberry-pi-webcam-server/comment-page-2/)

[https://m.blog.naver.com/PostView.nhn?blogId=scw0531&logNo=220653503111&targetKeyword=&targetRecommendationCode=1](https://m.blog.naver.com/PostView.nhn?blogId=scw0531&logNo=220653503111&targetKeyword=&targetRecommendationCode=1)
