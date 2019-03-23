# Wemos D1 Mini ve Oled Ekrana Çizdirme

Merhaba,

Wemos D1 Mini’in shieldlerinden [oled
ekran](https://tr.aliexpress.com/store/product/OLED-Shield-for-WeMos-D1-mini-0-66-inch-64X48-IIC-I2C/1331105_32627787079.html)
üzerinde micropython ile çizim işlemlerini inceleyeceğiz.

![](https://cdn-images-1.medium.com/max/800/1*RMjApKHBbp4Aq_iRDiJgwA.png)

### Text yazdırma

**text** fonksiyonunu kullanarak bir satır yazı yazdırabiliriz. Bu fonksiyon
aşağıdaki parametreleri alır

* **String tipinde metin**
* **Yazı X pozisyonu**
* **Yazı Y pozisyonu**
* **Opsiyonel olarak metin rengi** (0 = siyah, 1 = beyaz, varsayılan beyaz’dır)

    import ssd1306
    from machine import I2C, Pin
    i2c = I2C(sda=Pin(4), scl=Pin(5))
    display = ssd1306.SSD1306_I2C(64, 48, i2c)
    display.fill(0)
    display.text(‘Merhaba’,5,5)
    display.text(‘Yavuz’,5,15)
    display.show()

Aşağıdaki invert komutu ile de renkleri tersine çevirebiliriz.

    display.invert(True)

### Çizgi Çizdirme

Önce iki nokta arasına çizdi çizme fonksiyonunu tanımlayalım.

    def draw_line(display, x0, y0, x1, y1):
        deltax = x1 — x0
        deltay = y1 — y0
        error = -1.0
        deltaerr = abs(deltay / deltax) 
        y = y0
        for x in range(int(x0), int(x1)-1):
            # plot(x,y)
            display.pixel(x, y, 1)
            # print(x, y)
           error = error + deltaerr
           if error >= 0.0:
               y = y + 1
               error = error — 1.0

Daha sonra tanımladığımız fonksiyon yazdımıyla belirttiğimiz koordinatlar
arasına çizgi çizdirelim.


### Resim Çizdirme

Çizdirmek istediğiniz resmi önce
[buradan](http://www.digole.com/tools/PicturetoC_Hex_converter.php) 48x48
şeklinde boyutlandırarak hex formatına çevirelim ve logo değişkenine atalayım.

Resmi ekrana ortalamak için soldan x değerine 10 piksellik bir boşluk ekleyerek
aşağıdaki şekilde çizdirebiliriz.





#### Diğer resim örnekleri

Wemos D1 mini üzerindeki micropython örnek çalışmalarımın kaynak kodlarını
[buradan](https://github.com/yavuzKomecoglu/wemos-mini-d1) erişebilirsiniz.

* [IoT](https://medium.com/tag/iot?source=post)
* [Micropython](https://medium.com/tag/micropython?source=post)
* [Wemosd1mini](https://medium.com/tag/wemosd1mini?source=post)
* [Medium Turkish](https://medium.com/tag/medium-turkish?source=post)
* [Nesnelerin Interneti](https://medium.com/tag/nesnelerin-interneti?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)
