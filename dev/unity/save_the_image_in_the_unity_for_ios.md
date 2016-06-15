## index

1. iOSで画像を保存する場所を理解
1. iOSで画像を保存する際の注意点
1. UnityとiOSのディレクトリの対応関係
1. Unity内での画像の保存方法
1. Unity内での画像の取得方法
1. （おまけ）iosの画像と動画の保存の仕方

-------------------

### iOSで画像を保存する場所を理解

#### Documents/

- 読み込み可能
- 書き込み可能
- iTunesでバックアップされる。

ユーザー作成のコンテンツ（テキスト、写真）がここに入ります。設定によっては、iTunes経由などで見ることができるので、ユーザーに見られて困るようなファイル(設定ファイルとか)はここに置いておくべきではないです。

http://qiita.com/tototti/items/8646405f47cc56a59722

-------------------

### iOSで画像を保存する際の注意点

iosで画像保存を適当にしているとリジェクトされる
http://iaseteam.eshizuoka.jp/e1068667.html

iCloudバックアップ対象からDocuments/保存画像フォルダを外す作業を行う必要がある

--------------------

### UnityとiOSのディレクトリの対応関係

unityとiosとandroidのディレクトリ対応
http://qiita.com/bokkuri_orz/items/c37b2fd543458a189d4d


--------------------

### Unity内での画像の保存方法

プラットフォームごとのunityでの保存の仕方
https://gist.github.com/cellfusion/9777976

#### Application.persistentDataPath

永続的なデータを保存するパス。
ユーザーデータなど、アプリが再生成できないファイルを配置する。

##### Android(本体)	

/data/data/<アプリのID>/files/

##### Android(SDカード)	

/mnt/sdcard/Android/data/<アプリのID>/files/

##### iOS	

/var/mobile/Applications/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/Documents


--------------------

### Unity内での画像の取得方法

```cs

using UnityEngine;
using System.Collections;
using System.IO;  // ←Directoryクラスを使うにはコレがいる

public class MyClass : MonoBehaviour {
        void Start() {
            string[] path_array = Directory.GetFiles( Application.dataPath , "*.*" );
            int array_num = path_array.Length;
            for( int i = 0; i < array_num; i++ ){
                Debug.Log( path_array[i] );
            }
        }
}

```

これでできそう。  
検証いたしましょう。


--------------------

### （おまけ）iosの画像と動画の保存の仕方

iosの画像と動画の保存の仕方
http://qiita.com/yuch_i/items/812272e53289f5e1fade