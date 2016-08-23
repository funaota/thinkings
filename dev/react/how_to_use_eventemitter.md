##### EventEmitterを使うの大事！

EventEmitter使うの超大事です。

最初はEventEmitter正直よくわからず、callback書けばよくね？みたいな安直な考えで開発を進めていたのですが、前述の通りReact開発は非同期処理の部分が多く出てくるようになります。

最初のうちは全然いいのですが、プロジェクトが大きくなるにつれて、

- 「なんでここ更新されないの？」とか
- 「なんかよくわからんけど真っ白」とか

バグがちょっとずつ出始めます。修正できるっちゃできるくらいのバグなんですが、結構時間がかかったりします。
こういうバグのだいたいが非同期処理の部分だったりするので、どうにかしたいと調べていたら、EventEmitterを使えば全部その問題も解決するという感じだったので全部書き直しました。

流れとしては

①Constants.jsでEVENT名を定数で定める（この作業は最悪なくてもいい）

```js
var keyMirror = require('keymirror');

module.exports = keyMirror({
    NOTEE_CREATE: null,
    NOTEE_CREATE_FAILED: null,
});

```

②Store.jsでEVENT発火ポイントを作成する

```js
function notee_create(content) {
    request
        .post("/notee/api/posts")
        .send(content)
        .end(function(err, res){
            if(err || !res.body){
                NoteeStore.emitChange(NoteeConstants.NOTEE_CREATE_FAILED);
                return false;
            }
            NoteeStore.emitChange(NoteeConstants.NOTEE_CREATE);
        })
}
```

③あとは、Eventが発火した時にどうにかしたい場所を登録する

```js
componentDidMount() {
	NoteeStore.addChangeListener(NoteeConstants.NOTEE_CREATE, this.saveSuccessed);
    NoteeStore.addChangeListener(NoteeConstants.NOTEE_CREATE_FAILED, this.saveFailed);
}
```

これでちゃんと非同期処理が終わった時に、saveSuccessedとかが呼び出されるようになります。