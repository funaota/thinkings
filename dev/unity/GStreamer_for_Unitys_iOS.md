UnityでビルドしたiOSでGStreamerを使用する方法

## ①Pathを通す

- framework search path

```
"~/Library/Developer/GStreamer/iPhone.sdk"
```

- header search path

```
"~/Library/Developer/GStreamer/iPhone.sdk/GStreamer.framework/Headers"
```

## ②GStreamerをimportする

Xcodeのプロジェクト内にGStreamerをドラッグアンドドロップで入れます。
aliasだけでなく、複製します。

## ③GStreamerをinitする

```ob-c:gst_ios_init.h

```

```ob-c:gst_ios_init.m

```

```ob-c:main.mm
#include "gst_ios_init.h"

int main(int argc, char* argv[]){
	@autoreleasepool
	{
		# hogehoge
		gst_ios_init();
	}
	return 0;
}
```

## ④必要なライブラリをimportする

- libresolv.9.tbd
- libstdc++.6.0.9.tbd
- AssetsLibrary.framework
- Security.framework
- AudioTookbox.framework

