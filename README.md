รวมคำสั่งสำหรับผู้สนใจตัดต่อวีดีโอด้วย Command Line บน Linux โดยใช้ FFMPEG
รวมคำสั่งสำหรับผู้สนใจตัดต่อวีดีโอด้วย Command Line บน Linux โดยใช้ FFMPEG

   ffmpeg เป็นโอเพนซอร์สไลบารี่ในการจัดการเกี่ยวกับไฟล์วีดีโอและไฟล์เสียงต่าง ๆ โดยสามารถทำงานได้หลายแพลตฟอร์ม ไม่ว่าจะเป็น Linux Mac Windows ซึ่งมีผู้พัฒนานำ ffmpeg ไปใช้ในการพัฒนาโปรแกรมตัดต่อวีดีโอคุณภาพดีหลาย ๆ ตัว บทความนนี้จะมีแนะนำการชุดคำสั่งที่ใช้ในการแปลไฟล์ต่าง ๆ ให้ผู้สนใจ ได้ทราบ โดยชุดคำสั่งนี้ได้ทดสอบร่วมกับระบบปฎิบัติการ PCLinuxOS โดย ffmpeg นี้มีความสามารถในการเข้ารหัสและถอดรหัสวีดีโอและไฟล์เสียงต่าง ๆ ได้โดยรองรับไฟล์อาทิเช่น PSP หรือ iPod  และสามารถแปลงไฟล์วีดีโอได้หลาย format เช่นกัน

- คำสั่งสำหรับนำภาพเข้าไปแทรกในไฟล์วีดีโอ

ffmpeg -f image2 -i image%d.jpg video.mpg

โดยคุณสามารถนำไฟล์ภาพต่าง ๆ เข้ามาแทรกในไฟล์วีดีโอได้ เพื่อให้วีดีโอของคุณดูมีลูกเล่นมากยิ่งขึ้น

โดยชุดคำสั่งดังกล่าวจะเป็นการนำไฟล์ที่คำนำหน้าขึ้นต้นว่า image ทั้งหมด เช่น image1.jpg, image2.jpg, ฯลฯ รวมเข้ากับไฟล์วีดีโอชื่อ video.mpg

โดย ffmpeg รองรับไฟล์ภาพหลายสกุลไม่ว่าจะเป็น  PGM, PPM, PAM, PGMYUV, JPEG, GIF, PNG, TIFF, SGI.

- คำสั่งสำหรับแปลงไฟล์ AVI ให้อยู่ในรูปแบบ Mp4 เพื่อใช้กับ iPpod/iPhone

ffmpeg -i sourcevideo.avi input -acodec aac -ab 128kb -vcodec mpeg4 -b 1200kb -mbd 2 -flags +4mv+trell -aic 2 -cmp 2 -subcmp 2 -s 320×180 -title X finalvideo.mp4

รายละเอียด Option ต่าง ๆ:

    * Source : sourcevideo.avi
    * Audio codec : aac
    * Audio bitrate : 128kb/s
    * Video codec : mpeg4
    * Video bitrate : 1200kb/s
    * Video size : 320px par 180px
    * Generated video : finalvideo.mp4

- คำสั่งสำหรับแปลงไฟล์ AVI ให้อยู่ในรูป Mp4 เพื่อใช้กับ  PSP (เพลย์สเตชันพอร์เทเบิล)

ffmpeg -i sourcevideo.avi -b 300 -s 320×240 -vcodec xvid -ab 32 -ar 24000 -acodec aac finalvideo.mp4

รายละเอียด Option ต่าง ๆ :

    * Source : sourcevideo.avi
    * Audio codec : aac
    * Audio bitrate : 32kb/s
    * Video codec : xvid
    * Video bitrate : 1200kb/s
    * Video size : 320px par 180px
    * Generated video : finalvideo.mp4

-  คำสั่งดึงไฟล์ Mp3 ออกจากวีดีโอเพื่อนำไฟล์เสียงไปใช้อย่างเดียว

ffmpeg -i sourcevideo.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 sound.mp3

รายละเอียด Option ต่าง ๆ :

    * Source video : sourcevideo.avi
    * Audio bitrate : 192kb/s
    * output format : mp3
    * Generated sound : sound.mp3

-  คำสั่งแปลง Wav เป็น Mp3 สำหรับใส่เครื่องเล่น Mp3 แบบพกพา

ffmpeg -i sonorigine.avi -vn -ar 44100 -ac 2 -ab 192 -f mp3 sonfinal.mp3

- คำสั่งแปลงข้อมูลจาก .AVI เป็น .MPG เพื่อใช้เล่นกับเครื่องเล่น VCD

ffmpeg -i videoorigine.avi videofinale.mpg

-  คำสั่งแปลงข้อมูลจาก .MPG เป็น .AVI เพื่อใช้เล่นกับเครื่องเล่น DVD

ffmpeg -i videoorigine.mpg videofinale.avi

- คำสั่งแปลงข้อมูลจาก .avi เป็น .gif

ffmpeg -i videoorigine.avi gifanime.gif

- คำสั่งนำเสียงภาคแทรกเข้าไปในวีดีโอ

ffmpeg -i son.wav -i videoorigine.avi videofinale.mpg

- คำสั่งแปลงไฟล์จาก .AVI เป็น .flv เพื่อใช้ในการเล่นผ่านเว็ปไซต์

ffmpeg -i videoorigine.avi -ab 56 -ar 44100 -b 200 -r 15 -s 320×240 -f flv videofinale.flv

- คำสั่งแปลง .AVI เพื่อให้อยู่ในรูป .DV เพื่อจำเก็บลงในม้วน DV

ffmpeg -i videoorigine.avi -s pal -r pal -aspect 4:3 -ar 48000 -ac 2 videofinale.dv

หรือ:

ffmpeg -i videoorigine.avi -target pal-dv videofinale.dv

- คำสั่งแปลง .AVI ให้สามารถนำไปเล่นกับเครื่องเล่น DVD แบบ Widesceen ได้

ffmpeg -i sourcevideo.avi -target pal-dvd -ps 2000000000 -aspect 16:9 finalevideo.mpeg

รายละเอียด Option ต่าง ๆ :

    * target pal-dvd : Output format
    * ps 2000000000 maximum size for the output file, in bits (here, 2 Gb)
    * aspect 16:9 : Widescreen

- คำสั่งแปลง .AVI บีบอัดให้อยู่ในรูปแบบ Divx (เพื่อใช้เล่นกับคอมพิวเตอร์)

ffmpeg -i videoorigine.avi -s 320×240 -vcodec msmpeg4v2 videofinale.avi

- คำสั่งรวมไฟล์เสียง Ogg Theora เข้ากับไฟล์วีดีโอ DVD

ffmpeg -i filmsortiecinelerra.ogm -s 720×576 -vcodec mpeg2video -acodec mp3 filmterminée.mpg

- คำสั่งแปลง .avi ให้เป็น SVCD (mpeg2)

สำหรับเครื่องรับโทรทัศน์ระบบ NTSC :

ffmpeg -i videoorigine.avi -target ntsc-svcd videofinale.mpg

สำหรับเครื่องรับโทรทัศน์ระบบ PAL :

ffmpeg -i videoorigine.avi -target pal-svcd videofinale.mpg

- คำสั่งแปลงไฟล์ .avi ให้เป็น VCD (mpeg2)

สำหรับเครื่องรับโทรทัศน์ระบบ NTSC :

ffmpeg -i videoorigine.avi -target ntsc-vcd videofinale.mpg

สำหรับเครื่องรับโทรทัศน์ระบบ PAL :

ffmpeg -i videoorigine.avi -target pal-vcd video_finale.mpg

ffmpeg -i  http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vcodec mpeg2video -acodec pcm_s16le -ar 48000 -ac 2 output.mxf

หมายเหตุ:สำหรับชุดคำสั่งดังกล่าวสาารถใช้งานร่วมกับระบบปฎิบัติการ Linux ตะกูลอื่นทีมีการติดตั้ง Libary ffmpeg เข้าใป อาทิเช่น Ubuntu,Fedora,Sabayon,Linux TLE9 ฯลฯ



ffmpeg -i  http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vf timecode='00\:00\:00\:00': r=25: x=(w-tw)/2: y=h-(2*lh): fontcolor=white: box=1: boxcolor=0x00000000@1: fontsize=30" frame%05d.jpg" -vsync 0 -an keyframes%03d.jpg



./ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vf "drawtext=fontfile=/Library/Fonts/Verdana.ttf text='%{localtime}': x=(w-tw)/2: y=h-(2*lh): fontcolor=white: box=1: boxcolor=0x00000000@1" image%03d.png


====================
2 Pass
./ffmpeg -i  i.mp4  -pass 1  -passlogfile  text.log  -threads 2 -vcodec libx264  -f mp4   -aspect 16:9  -r 25 -s 480x340 -b:v 512k -minrate 512k -maxrate 512k -bufsize 2048k -an  output.mp4



./ffmpeg -y -i  i.mp4  -pass 2  -passlogfile  text.log  -threads 2 -vcodec libx264  -f mp4   -aspect 16:9  -r 25 -s 480x340 -b:v 512k -minrate 512k -maxrate 512k -bufsize 2048k -acodec copy -absf aac_adtstoasc -b:a 128k -ar 44100 output.mp4

==================

MCOT HD to mp4 (AVC Video,AAC Audio :HD 720 for ipad) (OSX,PC)
./ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -codec:v libx264 -profile:v main -preset slow -b:v 400k -maxrate 1024k -bufsize 800k -vf scale=-1280:720 -threads 0 -acodec copy -absf aac_adtstoasc -b:a 128k "outputIpad1.mp4"

==================================
MCOT HD to mp4 (AVC Video,AAC Audio, Rescal 640x370 Video Bitrate 400 K) (OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -codec:v libx264 -profile:v main -preset slow -b:v 400k -maxrate 400k -bufsize 800k -vf scale=-640:370 -threads 0 -acodec copy -absf aac_adtstoasc output.mp4
===================================
MCOT HD to png Picture (OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vframes 2 p21.png
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vf "scale=640:370" -vframes 2 p21.png
===================================
MCOT HD to mpeg (Mpeg Video,Mpeg Audio) (OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -target pal-svcd videofinale.mpg
============================================
MCOT HD to mp4 (MPeg4 Video,AAC Audio : Quicktime ) (OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vcodec mpeg4 -acodec copy -absf aac_adtstoasc output.mp4
==================================
MCOT HD to mp4 (AVC Video,AAC Audio) (OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vcodec copy -acodec copy -absf aac_adtstoasc "res.mp4"
==================================
MCOT HD to mov (AVC Video,PCM Audio)(OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -acodec pcm_s16be "output11.mov"
==================================
MCOT HD to mov (AVC Video,Mpeg Audio)(OSX,PC)
ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -acodec libmp3lame -ab 192 "output1.mov"https://ffmpeg.org/pipermail/ffmpeg-user/2014-February/019867.html
==================================
FM 100.5  to mp3 (PC,OSX)
ffmpeg -i http://mediaxii.mcot.net:1935/radio/fm1005.stream/playlist.m3u8  -vn -ar 44100 -ac 2 -ab 192 -f mp3 "output.mp3"

ffmpeg -i http://mediaxii.mcot.net:1935/radio/fm1005.stream/playlist.m3u8  -filter:a volumdetec -vn -f null /dev/null


ffmpeg -i http://mediaxi.mcot.net:1935/live/tcr1_ch1_all.smil/playlist.m3u8 -vcodec copy -acodec copy -f mpegts output-file.ts

Stream an H.264 file over UDP/RTP
ffmpeg -re -i input1.ts -vcodec copy -acodec copy -f mpegts "udp://192.168.1.25:5000"
(192.168.1.25 เป็น ip address ของภาพรับ)
การรับใช้ vlc  udp://@:5000
==================================
ffmpeg -f dshow -i input1.ts":audio="Stereo Mix (IDT High Definition" \-vcodec libx264 -preset ultrafast -tune zerolatency -r 10 -async 1 -acodec libmp3lame -ab 24k -ar 22050 -bsf:v h264_mp4toannexb -maxrate 750k -bufsize 3000k -f mpegts udp://192.168.5.215:48550
====================
Installation ffmpeg on centos
if you get package not found, then you will need to add few lines in the yum repository for dag packages installation. Create a file named dag.repo in /etc/yum.repos.d with the following contents on it

[dag]
name=Dag RPM Repository for Red Hat Enterprise Linux
baseurl=http://apt.sw.be/redhat/el$releasever/en/$basearch/dag
gpgcheck=1
enabled=1

then

yum install ffmpeg ffmpeg-devel

To check what audi/video formats are supported

ffmpeg -formats > ffmpeg-format.txt

Open the ffmpeg-formats.txt to see the ooutput

D means decode
E means encode
V means video
A means audio
T = Truncated

============
Opent Multisession vlc
open -n /Applications/VLC.app
===========





ffmpeg -i sample1.mp4 -b 1800k  -minrate 1800k -maxrate 1800k -bufsize 640k -ab 64k -vcodec libx264 -acodec aac -strict -2 -ac 2 -ar 44100 -s 1280x720 -y output1.mp4


ffmpeg -i sample1.mp4 -b 840k  -minrate 840k -maxrate 840k -bufsize 640k -ab 64k -vcodec libx264 -acodec aac -strict -2 -ac 2 -ar 44100 -s 1280x720 -y output2.mp4



ffmpeg -i sample1.mp4 -b 128k  -minrate 128k -maxrate 128k -bufsize 640k -ab 16k -vcodec libx264 -acodec aac -strict -2 -ac 2 -ar 44100 -s 1280x720 -y output3.mp4




<smil>
    <body>
        <switch>
            <video src="mp4:output3.mp4" system-bitrate="128000"/>
            <video src="mp4:output2.mp4" system-bitrate="840000"/>
            <video src="mp4:output1.mp4" system-bitrate="1800000"/>
        </switch>
    </body>
</smil>
