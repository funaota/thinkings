##### Jqueryのajaxじゃなくて、superagentを使おう！

ReactとRailsで開発していると、先ほども書いたようにインスタンス変数をそのまま渡す的なプレーができません（react-railsで部分的に使うなら可）
なので、データ取得はAPI経由で行う必要があります。

こんな時、今までならJqueryのAjaxで取得していたと思うのですが、せっかくReactになってJqueryから離れようとしているので、Jquery依存じゃない書き方をしていきたいなと思いました。

そこで、使ったのがsuperagent

SuperAgent
https://github.com/visionmedia/superagent

これ鬼便利です。みやすすぎてやばいです。

```js
request
   .get('/search')
   .end(function(err, res){
   		console.log(res.body);
   });
```

この非同期処理を4行で書けるとは、、、

```js
$.ajax({
    url: '/search',
    type: 'GET',
    success: function(data){
    	console.log(data);
    },
    error: function(err){
    	console.log(err);
    }
  })
```

Jqueryのajaxで書くと因みにこんな感じ。（動くか心配、、、）

superagentの方が見やすいのは一目瞭然だと思います。これからは積極的にsuperagent使っていきたいと思います。