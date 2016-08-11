# OpenCVのiosビルドがfailedしまくる問題

CocoaPodsに頼ってビルドするととても簡単でいい感じなのですが
今回はGstreamerを使用したかったので、CocoaPodsの方法だとインストールできませんでした。

てか、iOSでOpenCV付属のgstreamer使えるかどうかは微妙なのでこれから検証ですが
一応、opencv2.framework/Headers/videoio.hppにCAP_GSTREAMER = 1800という可能性を見つけることができたので
こちらの方法で行くしかありませんでした（CocoaPodsの方だとなかった）

で、自前の方法でインストールしようとしたのですがバグルバグル笑
やばかったです

Xcode Version 7.3
OpenCV 3.1.1-ios-fixed（branch name）

でやってみました。
全然、ios-fixedしてねーじゃんと思ったのですが、きっと違うところを直したんでしょうね笑

実際に出たエラーはこんな感じ


