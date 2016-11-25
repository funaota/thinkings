
## opencvのインストール前の準備

brew info opencv3にて、インストールしないといけないものを表示します。

※ちなみにHomebrewが入ってない場合はとりあえずインストールしてください。

```
$ brew doctor
$ brew update
$ brew tap homebrew/science
$ brew info opencv3
```

brew info opencv3するとこんな感じで出てきます


```
imac:Cellar takujifunao$ brew info opencv3
homebrew/science/opencv3: stable 3.1.0 (bottled), HEAD [keg-only]
Open source computer vision library, version 3
http://opencv.org/
/usr/local/Cellar/opencv3/3.1.0_3 (281 files, 119.7M)
  Poured from bottle on 2016-08-01 at 19:57:08
From: https://github.com/Homebrew/homebrew-science/blob/master/opencv3.rb
==> Dependencies
Build: cmake ✘, pkg-config ✘
Required: jpeg ✔, libpng ✔, libtiff ✔
Recommended: eigen ✔, openexr ✔, homebrew/python/numpy ✔
Optional: ffmpeg ✘, gphoto2 ✘, gstreamer ✘, jasper ✘, libdc1394 ✘, openni ✘, openni2 ✘, qt ✘, qt5 ✘, tbb ✘, vtk ✘
```

で、この『✘』がついてるやつをインストールします

```
$ brew install cmake
$ brew install pkg-config
```

※Optionalのやつはやらなくて大丈夫です


## opencv3のインストール

```
brew install opencv3 --c++11 --with-contrib --with-opengl --with-qt5
```

これでとりあえずopencvのインストールは終了


## xcodeの設定（pathを通す）

Build Setting →　HEADER_SEARCH_PATHSに以下の文を`recursive`で追加します。

```
/usr/local/Cellar/opencv3/
```

**recursive**で追加するのが大事です


Build Setting →　LIBRARY_SEARCH_PATHSに以下の文を追加します

```
/usr/local/Cellar/opencv3/3.1.0_3/lib
```


これでほぼ完成です。

## Build Phasesにlibを追加します

Build Phases　→　Link Binary with Librariesに使用するライブラリを追加します。

## デモ

最後にデモします

Link Binary with Librariesに、

 - libopencv_core.3.1.dylib
 - libopencv_highgui.3.1.dylib

これを追加します。

それで、main.cppに以下の文を追加して実行します

```
#include <iostream>
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>

int main(int argc, const char * argv[])
{
    cv::Mat img(cv::Size(320, 240), CV_8UC3, cv::Scalar(60, 150, 80));
    cv::namedWindow("OpenCV3!", cv::WINDOW_AUTOSIZE);
    cv::imshow("OpenCV3!", img);
    
    cv::waitKey(0);
}
```

これで緑の色したwindowが出たら成功です！

### ちなみに作成したプロジェクトは、OS X →　Command Line Toolです〜！！ 



