# ubuntuにguiでログインしたのに、すぐにまたログイン画面に戻らされた時の対処法

まず、sshでubuntuに入る

それで、

```
sudo rm .Xauthority .ICEauthority
sudo reboot
```

以上や！