# Android（galaxy s5）のルート化の方法です

## 昔のルート化は簡単だったみたい

昔は、SuperSuっていうアプリを１発入れてボタン押せば
後はadbで

```
# androidの中に入って
$ adb shell 

# rootになる
$ su -
```

これで簡単にルートの権限を取れたみたいですが最近のOS VERSIONにはアプリが対応してないみたいなので今回は昔のOS（4.4.2 KitKat）を焼き直す方法でいきます。

Windowsがないと動かせないソフトウェアを使うので、Macの人はBootとかしてなんとか使ってみてください。

## まず、自分の端末情報を調べる

androidの端末情報を調べてください。

Setting ← about device

とかにあった気がします。

#### Galaxy S5 SM-G900H

とかが今回使った端末の詳しい端末情報です。
後は、この同じ番号に対応してるやつをODINを使って焼き直します。

## 過去のOS versionをダウンロード

ここのリンクのDownload CF-Auto root for the Interntional Galaxy S5 SM-G900H:ってところからダウンロードしてきてください。

http://www.galaxys5update.com/root-samsung-galaxy-s5-sm-g900h-with-cf-auto-root-supersu/


## androidをodin modeで起動して接続

androidはいくつかモードがあります。その中で今回はodin modeというのを使います。

 1. まず電源を落とす
 2. volume down + home + power（電源）を同時に長押し
 3. 画面がついたら、volume upを押してカーソルを合わせ、powerを押して選択

 これでodin modeに入れました。

## odinを使って焼き直し

後は、先ほどダウンロードしたzipファイルを解凍しodinを起動します。

そしたら、それらしいファイルを選択して、Start!!!!!!

これで完成です！！