OXXでGStreamerを使用する方法

## ①Pathを通す

- framework search path

```
/Library/Frameworks/GStreamer.framework/
```

- header search path

```
/Library/Frameworks/GStreamer.framework/Versions/1.0/Headers
```

## ②GStreamerをimportする

Xcodeのプロジェクト内にGStreamerをドラッグアンドドロップで入れます。
aliasだけでなく、複製します。

## ③GStreamerをinitする

#### main.mm
```objective-c

#include <stdio.h>
#include <iostream>
#include <gst/gst.h>

int main(int argc, char * argv[]) {
    gst_init(&argc, &argv);
    return 0;
}



```

## 　④必要なライブラリをimportする

- libresolv.9.tbd
- libstdc++.6.0.9.tbd
- AssetsLibrary.framework
- Security.framework
- AudioTookbox.framework

もし、use of undeclared identifier asset 的なエラーが出たら

```
sudo rm /Library/Frameworks/GStreamer.framework/Headers/assert.h
```


