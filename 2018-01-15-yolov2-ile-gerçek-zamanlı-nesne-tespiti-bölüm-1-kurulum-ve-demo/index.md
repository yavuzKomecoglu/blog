# YOLOv2 ile Gerçek Zamanlı Nesne Tespiti — Bölüm 1: Kurulum ve Demo

Merhaba,

Bu yazıda öncelikle açık kaynaklı yapay sinir ağı kütüphanesi olan
[Darknet](https://pjreddie.com/darknet/yolo/) kütüphanesinin kendi
bilgisayarımıza kurulumuna değineceğiz. Sonrasında 2017 yılı itibariyle gerçek
zamanlı olarak en hızlı şekilde nesne tespiti yapabilen **YOLO **(**Y**ou
**O**nly **L**ook **O**nce) algoritmasını, önceden eğitilmiş model kullanarak
nesne tespiti demosunu nasıl çalıştıracağımızı göreceğiz.

### KURULUM

Github üzerinden **Darknet** deposunu git ile klonlayalım ve darknet klasörü
içerisine girelim.


Derleme işlemini başlatmadan önce darknet klasörü içerisindeki
[Makefile](https://github.com/pjreddie/darknet/blob/master/Makefile) dosyasını
inceleyelim. Şimdilik sadece ilk 5 satırı ile ilgileneceğiz.


CUDA destekli NVIDIA ekran kartınız varsa ve GPU üzerinde çalıştırmak
istiyorsanız Makefile dosyasında ilk satırdaki GPU değerini 1 olarak
değiştirmeniz gereklidir.

* GPU ile derlemek istiyorsanız bilgisayarınızda CUDA 8 versiyonu yüklü olmalıdır.
CUDA kurulumu için daha önceki yazıma
[buradan](http://blog.yavuzz.com/post/ubuntu-16-04-de-nvidia-cuda-kurulumu) göz
atabilirsiniz.

Web kameranızdan görüntü almak için Makefile dosyasında, üçüncü satırdaki OPENCV
değerini 1 olarak değiştirmelisiniz.

* OpenCV destekli derleme işlemi için makinanızda OpenCV yüklü ve derlenmiş
olmalıdır. Eğer kurulum yapmadıysanız **“**[Ubuntu Üzerinde OpenCV
Kurulumu](http://blog.yavuzz.com/post/ubuntu-uzerinde-opencv-kurulumu)**”**
başlıklı yazımdaki adımları izleyerek kurulumu gerçekleştirebilirsiniz.

Sadece CPU üzerinde çalıştırmak isterseniz Makefile dosyasında yukarıda
anlatılan değişiklikleri yapmadan derleyebilirsiniz.

`make` komutu çalıştırarak derleme işlemini başlatalım.


NOT: -j8 parametresi opsiyoneldir. Derleme işlemini hızlandırmak için “-j
çekirdek sayısı” parametresini ekleyebilirsiniz.

CPU üzerinde derleme yaptığınızda sorun yaşayacağınızı düşünmüyorum. Ancak GPU
üzerinde ve OpenCV destekli derleme yaparken hata alabilirsiniz. CUDA ve OpenCV
kurulum işlemlerinizi kontrol etmeyi unutmayınız.

Derleme işlemi sorunsuz şekilde tamamlandıysa denemeye geçebiliriz.

### DEMO

Önceden eğitilmiş modelin ağırlık dosyalarını aşağıdaki komut ile indirelim.


Ağırlık dosyasını da yapılandırma dosyalarının olduğu **cfg** klasörü altına
indirdim. Ama dilediğiniz yere indirebilirsiniz.

Data klasörü altındaki örnek **dog.jpg** görselinde nesnenin tanınmasını ve
yerinin saptanmasını istiyorsak, aşağıdaki şekilde ağ dosyasını (**yolo.cfg**),
indirdiğimiz ağırlık dosyasını (**yolo.weights**) ve görselin yolunu parametre
olarak belirterek detect komutunu çalıştırmalıyız.


![](https://cdn-images-1.medium.com/max/800/1*PcDyzo215zagX0iLnI1DAA.png)

![](https://cdn-images-1.medium.com/max/800/1*rJar7gWnKa-3oL4YpTUAdg.png)

İşlem sonunda görsel içerisinde **dog: 82%, car: 26%, truck: 65%, bicycle: 85%**
oranlarında nesneleri içerdiği ve nesnelerin konumlarının **sınırlayıcı kutu
(bounding box)** içerisine alındığını görüyoruz.

**Webcam ile gerçek zamanlı nesne tespiti **için
[[1](https://arxiv.org/pdf/1405.0312.pdf)] [COCO
Veriseti](http://cocodataset.org/#overview)’ni kullanarak **detector demo**
komutunu çalıştırıyoruz

    ./darknet detector demo cfg/coco.data cfg/yolo.cfg  cfg/yolo.weights

![](https://cdn-images-1.medium.com/max/800/1*c4im_3OxZsMPzUdyWz8MDA.jpeg)

**Video üzerinde gerçek zamanlı nesne tespiti **için ise webcam ile
çalıştırdığımız komut sonuna videonun dosya yolunu belirtmemiz yeterli
olacaktır.

     

*****

### ÇALIŞMALARIM

İstanbul trafiğinde çekilmiş olan kısa bir video üzerindeki nesne tespiti
denememi izleyebilirsiniz.

*****

Aşağıda da telefon ile çektiğim başka bir video üzerindeki nesne tespiti denemem
yer almaktadır.

<span class="figcaption_hack">Bilgisayar özellikleri video açıklamalarında mevcuttur.</span>

Soru ve görüşlerinizi aşağıdaki yorum bölümüne yazabilirsiniz.

Referanslar:

* [[1] https://arxiv.org/pdf/1405.0312.pdf](https://arxiv.org/pdf/1405.0312.pdf)
(Microsoft COCO: Common Objects in Context)
* [https://pjreddie.com/darknet/install/](https://pjreddie.com/darknet/install/)
* [https://pjreddie.com/darknet/yolo/](https://pjreddie.com/darknet/yolo/)
* [https://arxiv.org/abs/1612.08242](https://arxiv.org/abs/1612.08242) *(YOLO9000:
Better, Faster, Stronger)*

* [Deep Learning](https://medium.com/tag/deep-learning?source=post)
* [Computer Vision](https://medium.com/tag/computer-vision?source=post)
* [Yolo](https://medium.com/tag/yolo?source=post)
* [Machine Learning](https://medium.com/tag/machine-learning?source=post)
* [Artificial
Intelligence](https://medium.com/tag/artificial-intelligence?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

