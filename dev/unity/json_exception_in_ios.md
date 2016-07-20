## LitJsonを使っている時

```
JsonException: Can't assign value '180' (type System.Int32) to type LitJson.JsonData
```

とか

```
JsonException: Can't assign value '0.33' (type System.Double) to type LitJson.JsonData
```

みたいなエラーが出たら

JsonMapper.Registerにhogeからhoge2に変換する時はこんな感じにするよと定義を追加してあげれば解決する

つまり、最初のエラーの場合、System.Int32をLitJson.JsonDataに変換できませんよ

ということなので

intからLitJson.JsonDataに変換する時には

intをとりあえず、stringに変えちゃえばいいよ！と登録すればエラーがなくなるはずでさ

```
JsonMapper.RegisterImporter<int, LitJson.JsonData> ((int value) => {
			return (string)value.ToString();
		});
```

こんな感じ