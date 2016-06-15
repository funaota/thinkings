# js in view file

## index

1. inline js
1. require js

----------------------

### inline js

#### in slim

```slim
javascript:
  alert("hello world");
```

#### in erb

```erb
<%= javascript_tag do %>
	alert("hello world");	
<% end %>
```

----------------------

### require js

assets/javascripts以外から読み込む方法

```slim
= javascript_include_tag :src => "https://cdnjs.cloudflare.com/ajax/libs/masonry/3.3.2/masonry.pkgd.min.js"
```
