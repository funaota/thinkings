下記のURLから**develのついた**お好みのバージョンをダウンロードする  
https://gstreamer.freedesktop.org/data/pkg/


pkgを開いて、インストールする.  
すると


以下のPathにiOS用のGstreamerができてるからそこからドラッグアンドドロップしたりする  
/Library/Frameworks/GStreamer.framework/

もし、use of undeclared identifier asset 的なエラーが出たら

```
sudo rm /Library/Frameworks/GStreamer.framework/Headers/assert.h
```