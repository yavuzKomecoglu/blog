# Raspberry Pi 3 üzerinde Intel Movidius Neural Compute Stick ile Derin Öğrenme
Uygulamaları Çalıştırma

Merhaba,<br> Movidius NCS (Neural Compute Stick)’in Raspberry Pi 3 üzerinde
kurulumu ve demo uygulamalarının nasıl çalıştırılacağını görelim.

![](https://cdn-images-1.medium.com/max/800/0*0xdpXOVS_FrndUGt.jpeg)
<span class="figcaption_hack">Intel Movidius Neural Compute Stick & Raspberry Pi 3</span>

[Intel Movidius Neural Compute Stick](https://developer.movidius.com/), USB
portundan takıldığı cihaza, derin öğrenme uygulamalarınızı çalıştırma yeteneği
kazandıran, düşük güç tüketimine sahip ve düşük maliyetli kendi başına yapay
zeka (AI) kitidir.

Movidius NCS (Neural Compute Stick) hakkında daha detaylı bilgi için [M.Ayyüce
Kızrak](https://www.linkedin.com/in/merve-ayyÃ¼ce-kizrak/)’ın “[Intel-Movidius
Neural Compute Stick Nedir ve Nasıl
Kullanılır](https://medium.com/deep-learning-turkiye/intel-movidius-neural-compute-stick-nedir-ve-nasÄ±l-kullanÄ±lÄ±r-85fc9af6dc26)”
başlıklı blog yazısını incelemenizi tavsiye ederim.

<span class="figcaption_hack">Intel Movidius Neural Compute Stick Tanıtım Videosu</span>

### KURULUM

Raspberry Pi üzerine Intel Movidius Neural Compute SDK kurulumu için aşağıdaki
adımları sırasıyla uygulayalım.

### 1. Tensorflow

NCSDK’nın uygulamalarını Tensorflow ve Caffe kütüphanelerini kullanarak
çalıştıracağımızdan ilk olarak Tensorflow’u indirip pip3 ile kurulumunu
aşağıdaki şekilde yapalım.


     

### 2. Neural Compute SDK

Uygulamaları çalıştırmamız için gerekli tüm kütüphaneler ve örnekleri Github
sayfasından klonlayarak aşağıdaki şekilde derleyelim.

     
     
     
     

**NOT:** Bu işlem Raspberry Pi 3 üzerinde saatlerizi alabilir. Kitlendiğinde
veya elektrik kesilip yarım kaldığında ncsdk klasörüne girerek **make install**
komutunu yeniden çalıştırarak derleme işlemine devam edebilirsiniz.

<span class="figcaption_hack">Neural Compute SDK derleme işlemi sonu</span>

Sabırlı bekleyişinizden sonra **Setup is complete** mesajını aldıysanız kurulumu
başarıyla tamamladınız demektir. :)

### 3. OpenCV

Video kamerasından görüntü alma resim ve videolar üzerine işlemler yapılan bazı
örnekler için OpenCV kütüphanesi gerekli olabiliyor.<br> Github sayfasından
klonladığımız **ncsdk** içerisinde **install-opencv.sh** scriptini çalıştırarak
OpenCV kütüphanesinin kurulumunu tamamlayabilirsiniz.

### 4. KURULUM TEST

Kurulumun başarılı şekilde gerçekleştiğini ve Raspberry Pi’nin Movidius NC’ni
tanıyıp üzerinde kodun çalışıp çalışmadığını test edelim.

İndirmiş olduğumuz ncsdk içerisindeki örnek uygulamalar içerisinden python
örneğini aşağıdaki şekilde çalıştıralım.

     

Yukarıdaki ekran görüntüsünde gördüğümüz gibi sorunsuz şekilde
[hello_ncs.py](https://github.com/movidius/ncsdk/blob/master/examples/apps/hello_ncs_py/hello_ncs.py)
örneğini NCS üzerinde çalıştırmış olduk.

### GERÇEK ZAMANLI NESNE TANIMLAMA UYGULAMASI

Movidius NCS için Caffe ve Tensorflow örneklerinin bulunduğu başka bir repo
indirelim ve web cam ile gerçek zamanlı şekilde nesne tanıma uygulaması olan
**live-image-classifier** (canlı resim sınıflandırma) örneğini nasıl
çalıştırabileceğimizi görelim.

**Uygulama için gerekli materyaller;**

* Raspberry Pi 3
* Movidius Neural Compute Stick
* USB Webcam

Aşağıdaki şekilde ncappzoo reposunu indirelim.

    git clone 

**apps** altında **live-image-classifier** klasörüne girelim ve bu örnek için
gerekli olan model dosyaları, ağırlıklar ve graph dosyasının indirilmesi için
**make** komutunu çalıştıralım.

     

Gerekli dosyalar indirildikten sonra örneğimizi çalıştırabiliriz.


Uygulamanın çalışan videosunu aşağıdan izleyebilirsiniz.

<span class="figcaption_hack">Raspberry Pi 3 üzerinde Movidius NCS ile webcam görüntüsünden gerçek zamanlı
nesne tanıma uygulaması</span>

### Webcam yerine Raspberry Pi Kamera Modülünü Kullanma

Kendi resmi **live-image-classifier.py** demosu sadece webcam üzerinden
çalışmaktadır.<br> İlgili örneği, Raspberry Pi kamera modülü ile çalışır şekilde
revize ederek yeni örnek ekledim.<br>
[Buradan](https://github.com/yavuzKomecoglu/ncappzoo/tree/master/apps/live-image-classifier-PiCam)
erişebilirsiniz.

*****

### TEŞEKKÜR

> Derin öğrenme çalışmalarında kullanılması için talebimiz üzerine Movidius Neural
> Compute kitini hızlıca ulaştıran [Mustafa
Aldemir](https://www.linkedin.com/in/mustafaaldemir/) Bey nezdinde Intel
Türkiye’ye ve Movidius NCS’yi taşınabilir projeler gerçekleştirmemiz için
Raspberry Pi 3 desteğinde bulundukları için [Ramazan
Subaşı](https://www.linkedin.com/in/ramazansubasi/) nezdinde de [SAMM
Teknoloji](https://www.samm.com/tr)’ye teşekkürlerimi sunarım.

### GÜNCELLEME

* “Webcam yerine Raspberry Pi Kamera Modülünü Kullanma” başlığı eklendi —
15/04/2018

#### **Kaynaklar**

* [Getting Started with Movidius™ Neural Compute Stick
(Video)](https://www.youtube.com/watch?v=fESFVNcQVVA)
* [https://developer.movidius.com/start](https://developer.movidius.com/start)
* [https://movidius.github.io/ncsdk/](https://movidius.github.io/ncsdk/)
* [https://software.intel.com/en-us/articles/build-an-image-classifier-in-5-steps-on-the-intel-movidius-neural-compute-stick](https://software.intel.com/en-us/articles/build-an-image-classifier-in-5-steps-on-the-intel-movidius-neural-compute-stick)
* [https://movidius.github.io/blog/ncs-apps-on-rpi/](https://movidius.github.io/blog/ncs-apps-on-rpi/)
* [https://towardsdatascience.com/getting-started-with-intel-movidius-d8ba13e7d3ae](https://towardsdatascience.com/getting-started-with-intel-movidius-d8ba13e7d3ae)

* [Raspberry Pi](https://medium.com/tag/raspberry-pi?source=post)
* [Movidius](https://medium.com/tag/movidius?source=post)
* [Deep Learning](https://medium.com/tag/deep-learning?source=post)
* [Neural Networks](https://medium.com/tag/neural-networks?source=post)
* [Artificial
Intelligence](https://medium.com/tag/artificial-intelligence?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

