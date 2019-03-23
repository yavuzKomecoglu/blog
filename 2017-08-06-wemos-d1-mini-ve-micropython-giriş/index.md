# Wemos D1 Mini ve Micropython — Giriş

Merhaba, öncelikle Aliexpress’de bulunan [Wemos
Store](https://wemoscc.tr.aliexpress.com/store/1331105)’dan Wemos D1 Mini’yi
satın alabilirsiniz.

![](https://cdn-images-1.medium.com/max/800/1*jKTLutJTI4k2K7i1_IjfFw.png)
<span class="figcaption_hack">Wemos D1 Mini</span>

**Not: Bu yazıdaki aşağıdaki talimatlar Ubuntu üzerinde uygulanmaktadır.**

[https://micropython.org/download/](https://micropython.org/download/#esp8266)
adresine giderek en son micropython sürümünü indirelim.

Bugün itibariyle geçerli sürüm:
[esp8266–20170612-v1.9.1.bin](http://micropython.org/resources/firmware/esp8266-20170612-v1.9.1.bin)

ESP8266 micropython firmware’ünü wemos d1'e yüklememiz için esptool’u
kullanacağız.

> pip install esptool

Wemos D1 güç girişi ile bilgisayarınızın USB girişine bağlayalım.

Tüm serial aygıtları `ls /dev/tty*` komutu ile görebiliriz. Benim bilgisayarımda
wemos d1 usb bağlantısı `/dev/ttyUSB0` şeklinde gözükmektedir.

Micropython’u cihaza yazmadan önce flashı temizleyelim

> sudo esptool.py -p /dev/ttyUSB0 erase_flash

![](https://cdn-images-1.medium.com/max/800/1*RFAZ9omyyV9Wcpnv9p_uJw.png)

Şimdi indirdiğimiz micropython frameworku cihaza flashlayalım.

![](https://cdn-images-1.medium.com/max/1200/1*LCtCfieN7FNlDsn_s9I-0w.png)

Cihazı terminal ekranı üzerinden başlatmak için <br> `sudo apt-get install
screen` komutu ile gerekli paketi yükleyelim.

Aşağıdaki komut ile cihazı terminal üzerinde başlatalım.

> screen /dev/ttyUSB0 115200

İlk anda byük ihtimal boş bir ekran ile karşılaşabilirsiniz. Enter tuşuna
basarak komut girmeye hazır duruma gelmiş olacaktır. Aşağıdaki gibi python
komutlarınızı deneyerek çalıştığını görebilirsiniz.

![](https://cdn-images-1.medium.com/max/800/1*LyVRCn-Npe9-vHXVAD-jgg.png)

Aşağıdaki şekilde cihaz üzerindeki ledi yakıp söndürme örneğini de yapalım.

> >>> from machine import Pin<br> >>> led = Pin(2, Pin.OUT)<br> >>> led(0)<br> >>>
> led(1)

![](https://cdn-images-1.medium.com/max/800/1*qeHEniQKPjeLJOefNIS2rw.png)

[http://blog.yavuzz.com/post/wemos-d1-mini-ve-micropython-giris](http://blog.yavuzz.com/post/wemos-d1-mini-ve-micropython-giris)

* [Nesnelerin Interneti](https://medium.com/tag/nesnelerin-interneti?source=post)
* [IoT](https://medium.com/tag/iot?source=post)
* [Micropython](https://medium.com/tag/micropython?source=post)
* [Esp8266](https://medium.com/tag/esp8266?source=post)
* [Medium Turkish](https://medium.com/tag/medium-turkish?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

