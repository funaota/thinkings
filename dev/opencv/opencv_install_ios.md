# OpenCVのiosビルドがfailedしまくる問題

CocoaPodsに頼ってビルドするととても簡単でいい感じなのですが
今回はGstreamerを使用したかったので、CocoaPodsの方法だとインストールできませんでした。

てか、iOSでOpenCV付属のgstreamer使えるかどうかは微妙なのでこれから検証ですが
一応、opencv2.framework/Headers/videoio.hppにCAP_GSTREAMER = 1800という可能性を見つけることができたので
こちらの方法で行くしかありませんでした（CocoaPodsの方だとなかった）

で、自前でbuildする方法でインストールしようとしたのですがバグルバグル笑
http://docs.opencv.org/2.4/doc/tutorials/introduction/ios_install/ios_install.html

やばかったです

Xcode Version 7.3
OpenCV 3.1.1-ios-fixed（branch name）

でやってみました。
全然、ios-fixedしてねーじゃんと思ったのですが、きっと違うところを直したんでしょうね笑

実際に出たエラーはこんな感じ

```

imac:OmniTex takujifunao$ python opencv/platforms/ios/build_framework.py ios
Executing: ['cmake', '-GXcode', '-DAPPLE_FRAMEWORK=ON', '-DCMAKE_INSTALL_PREFIX=install', '-DCMAKE_BUILD_TYPE=Release', '-DCMAKE_TOOLCHAIN_FILE=/Users/takujifunao/Desktop/OmniTex/opencv/platforms/ios/cmake/Toolchains/Toolchain-iPhoneOS_Xcode.cmake', '-DENABLE_NEON=ON', '/Users/takujifunao/Desktop/OmniTex/opencv', '-DCMAKE_C_FLAGS=-fembed-bitcode', '-DCMAKE_CXX_FLAGS=-fembed-bitcode'] in /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS
-- Setting up iPhoneOS toolchain
-- iPhoneOS toolchain loaded
-- Setting up iPhoneOS toolchain
-- iPhoneOS toolchain loaded
-- The CXX compiler identification is AppleClang 7.3.0.7030029
-- The C compiler identification is AppleClang 7.3.0.7030029
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - failed
-- Detecting CXX compile features
-- Detecting CXX compile features - failed
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - failed
-- Detecting C compile features
-- Detecting C compile features - failed
-- Performing Test HAVE_CXX_FSIGNED_CHAR
-- Performing Test HAVE_CXX_FSIGNED_CHAR - Failed
-- Performing Test HAVE_C_FSIGNED_CHAR
-- Performing Test HAVE_C_FSIGNED_CHAR - Failed
-- Performing Test HAVE_CXX_W
-- Performing Test HAVE_CXX_W - Failed
-- Performing Test HAVE_C_W
-- Performing Test HAVE_C_W - Failed
-- Performing Test HAVE_CXX_WALL
-- Performing Test HAVE_CXX_WALL - Failed
-- Performing Test HAVE_C_WALL
-- Performing Test HAVE_C_WALL - Failed
-- Performing Test HAVE_CXX_WERROR_RETURN_TYPE
-- Performing Test HAVE_CXX_WERROR_RETURN_TYPE - Failed
-- Performing Test HAVE_C_WERROR_RETURN_TYPE
-- Performing Test HAVE_C_WERROR_RETURN_TYPE - Failed
-- Performing Test HAVE_CXX_WERROR_NON_VIRTUAL_DTOR
-- Performing Test HAVE_CXX_WERROR_NON_VIRTUAL_DTOR - Failed
-- Performing Test HAVE_C_WERROR_NON_VIRTUAL_DTOR
-- Performing Test HAVE_C_WERROR_NON_VIRTUAL_DTOR - Failed
-- Performing Test HAVE_CXX_WERROR_ADDRESS
-- Performing Test HAVE_CXX_WERROR_ADDRESS - Failed
-- Performing Test HAVE_C_WERROR_ADDRESS
-- Performing Test HAVE_C_WERROR_ADDRESS - Failed
-- Performing Test HAVE_CXX_WERROR_SEQUENCE_POINT
-- Performing Test HAVE_CXX_WERROR_SEQUENCE_POINT - Failed
-- Performing Test HAVE_C_WERROR_SEQUENCE_POINT
-- Performing Test HAVE_C_WERROR_SEQUENCE_POINT - Failed
-- Performing Test HAVE_CXX_WFORMAT
-- Performing Test HAVE_CXX_WFORMAT - Failed
-- Performing Test HAVE_C_WFORMAT
-- Performing Test HAVE_C_WFORMAT - Failed
-- Performing Test HAVE_CXX_WERROR_FORMAT_SECURITY
-- Performing Test HAVE_CXX_WERROR_FORMAT_SECURITY - Failed
-- Performing Test HAVE_C_WERROR_FORMAT_SECURITY
-- Performing Test HAVE_C_WERROR_FORMAT_SECURITY - Failed
-- Performing Test HAVE_CXX_WMISSING_DECLARATIONS
-- Performing Test HAVE_CXX_WMISSING_DECLARATIONS - Failed
-- Performing Test HAVE_C_WMISSING_DECLARATIONS
-- Performing Test HAVE_C_WMISSING_DECLARATIONS - Failed
-- Performing Test HAVE_CXX_WMISSING_PROTOTYPES
-- Performing Test HAVE_CXX_WMISSING_PROTOTYPES - Failed
-- Performing Test HAVE_C_WMISSING_PROTOTYPES
-- Performing Test HAVE_C_WMISSING_PROTOTYPES - Failed
-- Performing Test HAVE_CXX_WSTRICT_PROTOTYPES
-- Performing Test HAVE_CXX_WSTRICT_PROTOTYPES - Failed
-- Performing Test HAVE_C_WSTRICT_PROTOTYPES
-- Performing Test HAVE_C_WSTRICT_PROTOTYPES - Failed
-- Performing Test HAVE_CXX_WUNDEF
-- Performing Test HAVE_CXX_WUNDEF - Failed
-- Performing Test HAVE_C_WUNDEF
-- Performing Test HAVE_C_WUNDEF - Failed
-- Performing Test HAVE_CXX_WINIT_SELF
-- Performing Test HAVE_CXX_WINIT_SELF - Failed
-- Performing Test HAVE_C_WINIT_SELF
-- Performing Test HAVE_C_WINIT_SELF - Failed
-- Performing Test HAVE_CXX_WPOINTER_ARITH
-- Performing Test HAVE_CXX_WPOINTER_ARITH - Failed
-- Performing Test HAVE_C_WPOINTER_ARITH
-- Performing Test HAVE_C_WPOINTER_ARITH - Failed
-- Performing Test HAVE_CXX_WSHADOW
-- Performing Test HAVE_CXX_WSHADOW - Failed
-- Performing Test HAVE_C_WSHADOW
-- Performing Test HAVE_C_WSHADOW - Failed
-- Performing Test HAVE_CXX_WSIGN_PROMO
-- Performing Test HAVE_CXX_WSIGN_PROMO - Failed
-- Performing Test HAVE_C_WSIGN_PROMO
-- Performing Test HAVE_C_WSIGN_PROMO - Failed
-- Performing Test HAVE_CXX_WNO_NARROWING
-- Performing Test HAVE_CXX_WNO_NARROWING - Failed
-- Performing Test HAVE_C_WNO_NARROWING
-- Performing Test HAVE_C_WNO_NARROWING - Failed
-- Performing Test HAVE_CXX_WNO_DELETE_NON_VIRTUAL_DTOR
-- Performing Test HAVE_CXX_WNO_DELETE_NON_VIRTUAL_DTOR - Failed
-- Performing Test HAVE_C_WNO_DELETE_NON_VIRTUAL_DTOR
-- Performing Test HAVE_C_WNO_DELETE_NON_VIRTUAL_DTOR - Failed
-- Performing Test HAVE_CXX_WNO_UNNAMED_TYPE_TEMPLATE_ARGS
-- Performing Test HAVE_CXX_WNO_UNNAMED_TYPE_TEMPLATE_ARGS - Failed
-- Performing Test HAVE_C_WNO_UNNAMED_TYPE_TEMPLATE_ARGS
-- Performing Test HAVE_C_WNO_UNNAMED_TYPE_TEMPLATE_ARGS - Failed
-- Performing Test HAVE_CXX_FDIAGNOSTICS_SHOW_OPTION
-- Performing Test HAVE_CXX_FDIAGNOSTICS_SHOW_OPTION - Failed
-- Performing Test HAVE_C_FDIAGNOSTICS_SHOW_OPTION
-- Performing Test HAVE_C_FDIAGNOSTICS_SHOW_OPTION - Failed
-- Performing Test HAVE_CXX_QUNUSED_ARGUMENTS
-- Performing Test HAVE_CXX_QUNUSED_ARGUMENTS - Failed
-- Performing Test HAVE_C_QUNUSED_ARGUMENTS
-- Performing Test HAVE_C_QUNUSED_ARGUMENTS - Failed
-- Performing Test HAVE_CXX_WNO_SEMICOLON_BEFORE_METHOD_BODY
-- Performing Test HAVE_CXX_WNO_SEMICOLON_BEFORE_METHOD_BODY - Failed
-- Performing Test HAVE_C_WNO_SEMICOLON_BEFORE_METHOD_BODY
-- Performing Test HAVE_C_WNO_SEMICOLON_BEFORE_METHOD_BODY - Failed
-- Performing Test HAVE_CXX_FNO_OMIT_FRAME_POINTER
-- Performing Test HAVE_CXX_FNO_OMIT_FRAME_POINTER - Failed
-- Performing Test HAVE_C_FNO_OMIT_FRAME_POINTER
-- Performing Test HAVE_C_FNO_OMIT_FRAME_POINTER - Failed
-- Performing Test HAVE_CXX_MFPU_NEON
-- Performing Test HAVE_CXX_MFPU_NEON - Failed
-- Performing Test HAVE_C_MFPU_NEON
-- Performing Test HAVE_C_MFPU_NEON - Failed
-- Performing Test HAVE_CXX_FVISIBILITY_HIDDEN
-- Performing Test HAVE_CXX_FVISIBILITY_HIDDEN - Failed
-- Performing Test HAVE_C_FVISIBILITY_HIDDEN
-- Performing Test HAVE_C_FVISIBILITY_HIDDEN - Failed
-- Performing Test HAVE_CXX_FVISIBILITY_INLINES_HIDDEN
-- Performing Test HAVE_CXX_FVISIBILITY_INLINES_HIDDEN - Failed
-- Performing Test HAVE_C_FVISIBILITY_INLINES_HIDDEN
-- Performing Test HAVE_C_FVISIBILITY_INLINES_HIDDEN - Failed
-- Looking for fseeko
-- Looking for fseeko - not found
-- Looking for unistd.h
-- Looking for unistd.h - not found
-- Looking for sys/types.h
-- Looking for sys/types.h - not found
-- Looking for stdint.h
-- Looking for stdint.h - not found
-- Looking for stddef.h
-- Looking for stddef.h - not found
-- Check size of off64_t
-- Check size of off64_t - failed
-- Performing Test HAVE_C_WNO_SHORTEN_64_TO_32
-- Performing Test HAVE_C_WNO_SHORTEN_64_TO_32 - Failed
-- Performing Test HAVE_C_WNO_ATTRIBUTES
-- Performing Test HAVE_C_WNO_ATTRIBUTES - Failed
-- Performing Test HAVE_C_WNO_STRICT_PROTOTYPES
-- Performing Test HAVE_C_WNO_STRICT_PROTOTYPES - Failed
-- Performing Test HAVE_C_WNO_MISSING_PROTOTYPES
-- Performing Test HAVE_C_WNO_MISSING_PROTOTYPES - Failed
-- Performing Test HAVE_C_WNO_MISSING_DECLARATIONS
-- Performing Test HAVE_C_WNO_MISSING_DECLARATIONS - Failed
-- Performing Test HAVE_C_WNO_CAST_ALIGN
-- Performing Test HAVE_C_WNO_CAST_ALIGN - Failed
-- Performing Test HAVE_C_WNO_SHADOW
-- Performing Test HAVE_C_WNO_SHADOW - Failed
-- Performing Test HAVE_C_WNO_UNUSED
-- Performing Test HAVE_C_WNO_UNUSED - Failed
-- Performing Test HAVE_C_WNO_UNUSED_PARAMETER
-- Performing Test HAVE_C_WNO_UNUSED_PARAMETER - Failed
-- The ASM compiler identification is Clang
-- Found assembler: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
-- math lib 'libm' not found; floating point support disabled
-- Looking for linux/videodev.h
-- Looking for linux/videodev.h - not found
-- Looking for linux/videodev2.h
-- Looking for linux/videodev2.h - not found
-- Looking for sys/videoio.h
-- Looking for sys/videoio.h - not found
-- Could NOT find Doxygen (missing:  DOXYGEN_EXECUTABLE) 
-- To enable PlantUML support, set PLANTUML_JAR environment variable or pass -DPLANTUML_JAR=<filepath> option to cmake
-- Could NOT find PythonInterp (missing:  PYTHON_EXECUTABLE) (Required is at least version "2.7")
-- Could NOT find PythonInterp (missing:  PYTHON_EXECUTABLE) (Required is at least version "2.6")
-- Could NOT find PythonInterp (missing:  PYTHON_EXECUTABLE) (Required is at least version "3.4")
-- Could NOT find PythonInterp (missing:  PYTHON_EXECUTABLE) (Required is at least version "3.2")
-- Could NOT find JNI (missing:  JAVA_AWT_LIBRARY JAVA_JVM_LIBRARY JAVA_INCLUDE_PATH JAVA_INCLUDE_PATH2 JAVA_AWT_INCLUDE_PATH) 
-- Processing WORLD modules...
--     module opencv_core...
--     module opencv_flann...
--     module opencv_imgproc...
--     module opencv_ml...
--     module opencv_photo...
--     module opencv_video...
--     module opencv_imgcodecs...
--     module opencv_shape...
--     module opencv_videoio...
--     module opencv_highgui...
--     module opencv_objdetect...
--     module opencv_features2d...
--     module opencv_calib3d...
--     module opencv_stitching...
--     module opencv_videostab...
-- Processing WORLD modules... DONE
-- Performing Test HAVE_OBJCXX_FOBJC_EXCEPTIONS
-- Performing Test HAVE_OBJCXX_FOBJC_EXCEPTIONS - Failed
-- Performing Test HAVE_CXX_WNO_DEPRECATED_DECLARATIONS
-- Performing Test HAVE_CXX_WNO_DEPRECATED_DECLARATIONS - Failed
-- 
-- General configuration for OpenCV 3.1.0 =====================================
--   Version control:               unknown
-- 
--   Platform:
--     Host:                        Darwin 15.0.0 x86_64
--     Target:                      iOS
--     CMake:                       3.6.1
--     CMake generator:             Xcode
--     CMake build tool:            /usr/bin/xcodebuild
--     Xcode:                       7.3
-- 
--   C/C++:
--     Built as dynamic libs?:      NO
--     C++ Compiler:                /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang++  (ver 7.3.0.7030029)
--     C++ flags (Release):         -fembed-bitcode -stdlib=libc++ -fvisibility=hidden -fvisibility-inlines-hidden -Wno-unused-function -Wno-overloaded-virtual -fPIC   -DNDEBUG -O3 -fomit-frame-pointer -ffast-math  -DNDEBUG
--     C++ flags (Debug):           -fembed-bitcode -stdlib=libc++ -fvisibility=hidden -fvisibility-inlines-hidden -Wno-unused-function -Wno-overloaded-virtual -fPIC   -g  -O0 -DDEBUG -D_DEBUG
--     C Compiler:                  /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang
--     C flags (Release):           -fembed-bitcode -fPIC   -O3 -DNDEBUG  -DNDEBUG
--     C flags (Debug):             -fembed-bitcode -fPIC   -g  -O0 -DDEBUG -D_DEBUG
--     Linker flags (Release):
--     Linker flags (Debug):
--     Precompiled headers:         NO
--     Extra dependencies:          -framework Accelerate -framework AVFoundation -framework CoreGraphics -framework CoreImage -framework CoreMedia -framework CoreVideo -framework QuartzCore -framework AssetsLibrary stdc++
--     3rdparty dependencies:       libjpeg libpng zlib
-- 
--   OpenCV modules:
--     To be built:                 core flann imgproc ml photo video imgcodecs shape videoio highgui objdetect features2d calib3d stitching videostab world
--     Disabled:                    -
--     Disabled by dependency:      -
--     Unavailable:                 cudaarithm cudabgsegm cudacodec cudafeatures2d cudafilters cudaimgproc cudalegacy cudaobjdetect cudaoptflow cudastereo cudawarping cudev java python2 superres ts viz
-- 
--   GUI: 
--     Cocoa:                       YES
--     OpenGL support:              NO
--     VTK support:                 NO
-- 
--   Media I/O: 
--     ZLib:                        build (ver 1.2.8)
--     JPEG:                        build (ver 90)
--     WEBP:                        NO
--     PNG:                         build (ver 1.6.19)
--     TIFF:                        NO
--     JPEG 2000:                   NO
--     OpenEXR:                     NO
--     GDAL:                        NO
-- 
--   Video I/O:
--     AVFoundation:                YES
--     GStreamer:                   NO
--     QuickTime:                   NO
--     QTKit:                       NO
--     V4L/V4L2:                    NO/NO
--     XIMEA:                       NO
--     gPhoto2:                     NO
-- 
--   Parallel framework:            GCD
-- 
--   Other third-party libraries:
--     Use IPP:                     NO
--     Use VA:                      NO
--     Use Intel VA-API/OpenCL:     NO
--     Use Eigen:                   YES (ver 3.2.9)
--     Use Cuda:                    NO
--     Use OpenCL:                  NO
--     Use custom HAL:              NO
-- 
--   Python 2:
--     Interpreter:                 NO
-- 
--   Python 3:
--     Interpreter:                 NO
-- 
--   Python (for build):            NO
-- 
--   Java:
--     ant:                         NO
--     JNI:                         NO
--     Java wrappers:               NO
--     Java tests:                  NO
-- 
--   Matlab:                        NO
-- 
--   Documentation:
--     Doxygen:                     NO
--     PlantUML:                    NO
-- 
--   Tests and samples:
--     Tests:                       NO
--     Performance tests:           NO
--     C/C++ Examples:              NO
-- 
--   Install path:                  /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/install
-- 
--   cvconfig.h is in:              /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS
-- -----------------------------------------------------------------
-- 
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS
Executing: ['xcodebuild', 'IPHONEOS_DEPLOYMENT_TARGET=6.0', 'ARCHS=armv7', '-sdk', 'iphoneos', '-configuration', 'Release', '-parallelizeTargets', '-jobs', '4', '-target', 'ALL_BUILD', 'build'] in /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS
User defaults from command line:
    IDEBuildOperationMaxNumberOfConcurrentCompileTasks = 4

Build settings from command line:
    ARCHS = armv7
    IPHONEOS_DEPLOYMENT_TARGET = 6.0
    SDKROOT = iphoneos9.3

Build Preparation
Build task concurrency set to 4 via user default IDEBuildOperationMaxNumberOfConcurrentCompileTasks

=== BUILD AGGREGATE TARGET ZERO_CHECK OF PROJECT OpenCV WITH CONFIGURATION Release ===

Check dependencies

Write auxiliary files
write-file /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-3DEAEFE211744121BE8B01AC.sh
chmod 0755 /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-3DEAEFE211744121BE8B01AC.sh

PhaseScriptExecution CMake\ Rules /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-3DEAEFE211744121BE8B01AC.sh
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    /bin/sh -c /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-3DEAEFE211744121BE8B01AC.sh
echo ""

make -f /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/CMakeScripts/ReRunCMake.make
make[1]: `/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/CMakeFiles/cmake.check_cache' is up to date.

=== BUILD TARGET libjpeg OF PROJECT OpenCV WITH CONFIGURATION Release ===
Check dependencies

Write auxiliary files
/bin/mkdir -p /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7
write-file /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7/libjpeg.LinkFileList

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7/jaricom.o 3rdparty/libjpeg/jaricom.c normal armv7 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch armv7 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wno-shorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg -I/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources/armv7 -I/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7/jaricom.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7/jaricom.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg/jaricom.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/armv7-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/armv7/jaricom.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

..........

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jcdctmgr.o 3rdparty/libjpeg/jcdctmgr.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -O1 -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jcdctmgr.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jcdctmgr.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg/jcdctmgr.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jcdctmgr.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jchuff.o 3rdparty/libjpeg/jchuff.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jchuff.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jchuff.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/libjpeg/jchuff.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/libjpeg/OpenCV.build/Release-iphoneos/libjpeg.build/Objects-normal/arm64/jchuff.o

=== BUILD AGGREGATE TARGET ZERO_CHECK OF PROJECT OpenCV WITH CONFIGURATION Release ===

Check dependencies

Write auxiliary files
write-file /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-4178F7A66E394A6FBF7A0718.sh
chmod 0755 /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-4178F7A66E394A6FBF7A0718.sh

PhaseScriptExecution CMake\ Rules /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-4178F7A66E394A6FBF7A0718.sh
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    /bin/sh -c /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/OpenCV.build/Release-iphoneos/ZERO_CHECK.build/Script-4178F7A66E394A6FBF7A0718.sh
echo ""

make -f /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/CMakeScripts/ReRunCMake.make
make[1]: `/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/CMakeFiles/cmake.check_cache' is up to date.

=== BUILD TARGET zlib OF PROJECT OpenCV WITH CONFIGURATION Release ===

Check dependencies

Write auxiliary files
/bin/mkdir -p /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64
write-file /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/zlib.LinkFileList

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/adler32.o 3rdparty/zlib/adler32.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/adler32.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/adler32.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/adler32.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/adler32.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/crc32.o 3rdparty/zlib/crc32.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/crc32.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/crc32.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/crc32.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/crc32.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/compress.o 3rdparty/zlib/compress.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/compress.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/compress.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/compress.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/compress.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/deflate.o 3rdparty/zlib/deflate.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/deflate.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/deflate.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/deflate.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/deflate.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzclose.o 3rdparty/zlib/gzclose.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzclose.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzclose.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzclose.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzclose.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzlib.o 3rdparty/zlib/gzlib.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzlib.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzlib.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzlib.o
clang: warning: argument unused during compilation: '-fembed-bitcode-marker'
/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c:256:24: error: implicit declaration of function 'lseek' is invalid in C99 [-Werror,-Wimplicit-function-declaration]
        state->start = LSEEK(state->fd, 0, SEEK_CUR);
                       ^
/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c:14:17: note: expanded from macro 'LSEEK'
#  define LSEEK lseek
                ^
/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c:256:24: note: did you mean 'fseek'?
/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c:14:17: note: expanded from macro 'LSEEK'
#  define LSEEK lseek
                ^
In file included from /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzlib.c:6:
In file included from /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzguts.h:21:
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk/usr/include/stdio.h:251:6: note: 'fseek' declared here
int      fseek(FILE *, long, int);
         ^
1 error generated.

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzread.o 3rdparty/zlib/gzread.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzread.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzread.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzread.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzread.o

CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzwrite.o 3rdparty/zlib/gzwrite.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/takujifunao/Desktop/OmniTex/opencv
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin:/Users/takujifunao/.nodebrew/current/bin:/Users/takujifunao/.rbenv/shims:/Users/takujifunao/.rbenv/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang -x c -arch arm64 -fmessage-length=256 -fdiagnostics-show-note-include-stack -fmacro-backtrace-limit=0 -fcolor-diagnostics -Wno-trigraphs -fpascal-strings -O3 -Wno-missing-field-initializers -Wno-missing-prototypes -Wno-return-type -Wno-missing-braces -Wparentheses -Wswitch -Wno-unused-function -Wno-unused-label -Wno-unused-parameter -Wno-unused-variable -Wunused-value -Wno-empty-body -Wno-uninitialized -Wno-unknown-pragmas -Wno-shadow -Wno-four-char-constants -Wno-conversion -Wno-constant-conversion -Wno-int-conversion -Wno-bool-conversion -Wno-enum-conversion -Wshorten-64-to-32 -Wpointer-sign -Wno-newline-eof -DCMAKE_INTDIR=\"Release-iphoneos\" -DNO_FSEEKO -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.3.sdk -fstrict-aliasing -Wdeprecated-declarations -miphoneos-version-min=6.0 -Wno-sign-conversion -fembed-bitcode-marker -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release/include -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources/arm64 -I/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/DerivedSources -Wmost -Wno-four-char-constants -Wno-unknown-pragmas -F/Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/lib/Release -fembed-bitcode -fPIC -fPIC -DNDEBUG -DNDEBUG -MMD -MT dependencies -MF /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzwrite.d --serialize-diagnostics /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzwrite.dia -c /Users/takujifunao/Desktop/OmniTex/opencv/3rdparty/zlib/gzwrite.c -o /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzwrite.o

** BUILD FAILED **


The following build commands failed:
	CompileC /Users/takujifunao/Desktop/OmniTex/ios/build/arm64-iPhoneOS/3rdparty/zlib/OpenCV.build/Release-iphoneos/zlib.build/Objects-normal/arm64/gzlib.o 3rdparty/zlib/gzlib.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler
(1 failure)
============================================================
ERROR: Command '['xcodebuild', 'IPHONEOS_DEPLOYMENT_TARGET=6.0', 'ARCHS=arm64', '-sdk', 'iphoneos', '-configuration', 'Release', '-parallelizeTargets', '-jobs', '4', '-target', 'ALL_BUILD', 'build']' returned non-zero exit status 65
============================================================
Traceback (most recent call last):
  File "opencv/platforms/ios/build_framework.py", line 87, in build
    self._build(outdir)
  File "opencv/platforms/ios/build_framework.py", line 81, in _build
    self.buildOne(t[0], t[1], mainBD, cmake_flags)
  File "opencv/platforms/ios/build_framework.py", line 139, in buildOne
    execute(buildcmd + ["-target", "ALL_BUILD", "build"], cwd = builddir)
  File "opencv/platforms/ios/build_framework.py", line 34, in execute
    retcode = check_call(cmd, cwd = cwd)
  File "/usr/local/Cellar/python/2.7.12/Frameworks/Python.framework/Versions/2.7/lib/python2.7/subprocess.py", line 541, in check_call
    raise CalledProcessError(retcode, cmd)
CalledProcessError: Command '['xcodebuild', 'IPHONEOS_DEPLOYMENT_TARGET=6.0', 'ARCHS=arm64', '-sdk', 'iphoneos', '-configuration', 'Release', '-parallelizeTargets', '-jobs', '4', '-target', 'ALL_BUILD', 'build']' returned non-zero exit status 65
```

長すぎるので上部を割愛しましたが

とりあえず、failedの嵐が出ます。

で、今回一応ビルドできた方法をまとめておこうと思います。

## まず、３つのファイルにheaderを追加する

なんかのバグで３つのファイルにheader.hが足りてないみたいです笑

- opencv/3rdparty/zlib/gzlib.c
- opencv/3rdparty/zlib/gzread.c
- opencv/3rdparty/zlib/gzwrite.c

に

```
#include "unistd.h"

```
を追加する。

## 次に、cd opencv/platforms/ios/ でディレクトリを移動

## ここで、 sudo python build_framwwork.py ios

というように、sudo付きで実行！

これで一応僕の場合はビルドができました（めっちゃ時間がかかりましたが笑）

ぜひ、試してみてください。