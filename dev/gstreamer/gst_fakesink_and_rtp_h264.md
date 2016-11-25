
H.264 RTP Streaming
http://labs.isee.biz/index.php/Example_GStreamer_Pipelines

## SEND

```
gst-launch-1.0 v4l2src ! image/jpeg ! jpegdec ! queue ! videoscale ! video/x-raw ! queue ! omxh264enc target-bitrate=15000000 control-rate=variable ! 'video/x-h264,stream-format=(string)byte-stream' ! h264parse ! rtph264pay config-interval=1 ! udpsink host=192.168.100.102 port=5003
```

## RECIEVE

```
udpsrc port=5003 caps=application/x-rtp,media=(string)video,payload=(int)96,clock-rate=(int)90000,encoding-name=H264 ! rtpjitterbuffer ! rtph264depay ! video/x-h264 ! h264parse ! video/x-h264 ! vtdec ! fakesink sync=1
```
