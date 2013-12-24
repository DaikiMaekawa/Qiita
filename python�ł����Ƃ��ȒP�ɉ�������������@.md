pythonで手軽に音声合成したいならeSpeakがおすすめです。

#eSpeakとは

多言語に対応したオープンソースのスピーチシンセサイザー。

英語はもちろんのこと、スペイン語、ドイツ語、中国語など幅広く対応しています。(残念ながら日本語未対応)

[対応言語一覧はこちら](http://espeak.sourceforge.net/languages.html)

一応日本語に対応させる方法も存在するようです　
　→　http://ja.nishimotz.com/espeak

#インストール方法
    sudo aptitude install python-espeak

#テストプログラム

Hello Worldを発声するプログラム

```py:helloworld.py
from espeak import espeak
espeak.synth("Hello World")
```
