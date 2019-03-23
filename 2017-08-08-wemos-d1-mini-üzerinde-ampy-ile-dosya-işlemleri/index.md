# Wemos D1 Mini üzerinde ampy ile dosya işlemleri

Merhaba,

> Başlamadan önce Wemos D1 Mini ve MicroPython Giriş yazısını
> [buradan](https://medium.com/@komecoglu.yavuz/wemos-d1-mini-ve-micropython-giriÅ-3ecbd894315c)
okuyabilirsiniz.

Wemos D1 mini üzerinde dosya okuma, yazma, kopyalama, silme, çalıştırma gibi
işlemler için [Adafruit’in MicroPython
tool’unu(ampy)](https://github.com/adafruit/ampy) kullanacağız.

Aşağıdaki komut ile yükleme işlemini gerçekleştirelim.

> pip install adafruit-ampy

Daha sonra kurulumu kontrol etmek ve gerçekleştirilebilir komutlar için
aşağıdaki help komutu yazalım.

> ampy — help

Ampy, seri bağlantı üzerinden bir MicroPython kurulu kart ile konuşmaya hazır
durumdadır.

Örneğin, Wemos D1 üzerinde dosyaları listelemek istersek aşağıdaki komutu
kullanabiliriz.

> sudo ampy — port /dev/ttyUSB0 ls

![](https://cdn-images-1.medium.com/max/800/1*Fw-mPUIYoLrM4emyk8Y5ug.png)
<span class="figcaption_hack">Cihaz içerisindeki dosyalar listelendi.</span>

Veya bilgisayarımızdaki bir python kodunu(**test.py**) aşağıdaki şekilde kart
üzerinde çalıştırabiliriz.

> sudo ampy — port /dev/ttyUSB0 run test.py

![](https://cdn-images-1.medium.com/max/800/1*attXEiNKuuKWCMbB6QRf1Q.png)
<span class="figcaption_hack">test.py nin cihaz üzerinde çalıştırıldığındaki çıktısı</span>

Bilgisayarınızdaki bir dosyayı kart üzerine kopyalamak için ise `put` komutunu
kullanırız.

![](https://cdn-images-1.medium.com/max/800/1*ENmYxpD3sn04xJUmsLFulg.png)
<span class="figcaption_hack">test.py cihaz içerisine aktarıldı</span>

Kart üzerindeki bir dosyayı okumak için ise `get` komutunu kullanırız.

![](https://cdn-images-1.medium.com/max/800/1*6Mj-_LIDjwvD0fBwKRI6Gw.png)
<span class="figcaption_hack">cihaz içerisindeki test.py okundu</span>

Kart üzerindeki bir silmek için ise `rm` komutunu kullanırız.

![](https://cdn-images-1.medium.com/max/800/1*OiDi1PtnC58aWCk9WDd1DA.png)
<span class="figcaption_hack">cihaz içerisideki test.py silindi</span>

Kaynak:
[https://learn.adafruit.com/micropython-basics-load-files-and-run-code/overview](https://learn.adafruit.com/micropython-basics-load-files-and-run-code/overview)

* [Nesnelerin Interneti](https://medium.com/tag/nesnelerin-interneti?source=post)
* [IoT](https://medium.com/tag/iot?source=post)
* [Micropython](https://medium.com/tag/micropython?source=post)
* [Esp8266](https://medium.com/tag/esp8266?source=post)
* [Medium Turkish](https://medium.com/tag/medium-turkish?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

