# Wemos D1 Mini Pro Orjinal Firmware Nasıl Geri Yüklenir?

Merhaba,

Eğer cihazımıza micropython gibi farklı bir firmware flashladıysak, sırasıyla
aşağıdaki adımları izleyerek orjinal firmware e dönebiliriz ve Arduino IDEsi ile
çalışabiliriz.

**1.** esptool ile var olan flash ı temizliyoruz. Eğer esptool yüklü değil ise
`pip install esptool` komutu ile yükleyebilirsiniz.

     

**2.** [Espressif SDK
2.1.0](https://github.com/espressif/ESP8266_NONOS_SDK/archive/v2.1.0.zip)'ı
indirelim ve sıkıştırılmış dosyasından çıkartalım. Çıkardığımız
ESP8266_NONOS_SDK-2.1.0 klasörünün içerisindeki bin klasörüne gidelim.

**3.** bin klasörü içerisinde<br> `esptool.py --port <serial-port-of-ESP8266>
write_flash -fm <mode> 0x00000 <nodemcu-firmware>.bin` <br> komutunu port,
flash_mode ve dosya adını kendinize göre düzenleyerek çalıştırınız.<br> Benim
bilgisayarıma göre aşağıdaki şekilde başarıyla çalıştırdım.

    sudo esptool.py — port /dev/ttyUSB0 write_flash -fm dio -fs 16m 0x00000 esp_init_data_default.bin

![](https://cdn-images-1.medium.com/max/1200/1*O7wPe0H10JZWF8SmIj4uTw.png)

Herhangi bir hata ile karşılaşmadıysanız artık Arduino IDEsi ile
çalışabilirsiniz.

Kaynak:

* [https://nodemcu.readthedocs.io/en/master/en/flash/](https://nodemcu.readthedocs.io/en/master/en/flash/)
* [https://github.com/nodemcu/nodemcu-firmware/blob/master/docs/en/flash.md](https://github.com/nodemcu/nodemcu-firmware/blob/master/docs/en/flash.md)
* [http://espressif.com/en/products/hardware/esp8266ex/resources](http://espressif.com/en/products/hardware/esp8266ex/resources)
* [https://github.com/espressif/ESP8266_RTOS_SDK](https://github.com/espressif/ESP8266_RTOS_SDK)

* [IoT](https://medium.com/tag/iot?source=post)
* [Wemosd1mini](https://medium.com/tag/wemosd1mini?source=post)
* [Arduino](https://medium.com/tag/arduino?source=post)
* [Medium Turkish](https://medium.com/tag/medium-turkish?source=post)
* [Nesnelerin Interneti](https://medium.com/tag/nesnelerin-interneti?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

