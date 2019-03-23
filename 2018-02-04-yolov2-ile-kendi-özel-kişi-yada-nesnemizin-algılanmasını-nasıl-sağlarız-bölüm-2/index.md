# YOLOv2 ile Kendi Özel Kişi ya da Nesnemizin Algılanmasını Nasıl Sağlarız? —
Bölüm 2

Merhaba,<br> Öncelikle gerçek zamanlı nesne tespiti kütüphanesi YOLO’nun
kurulumu ve demonun çalıştırılması hakkındaki yazıyı
[buradan](https://medium.com/deep-learning-turkiye/yolov2-ile-gerÃ§ek-zamanlÄ±-nesne-tespiti-bÃ¶lÃ¼m-1-kurulum-ve-demo-f3d0c72e4a28)
inceleyebilirsiniz.

Bu yazıda **Mustafa Kemal Atatürk**’ün profil resimlerini tespit etmeye
çalışalım.

Aşağıda anlatılan adımları sırasıyla ve sabırla uygulayalım.

### Veriseti Görsellerini Oluşturma

Google görsellerden indirdiğimiz Atatürk resimlerini **data** klasörü altına
**ataturk_dataset **adıyla yeni klasör oluşturarak kaydedelim.

![](https://cdn-images-1.medium.com/max/800/1*raH2-DOYyOxVtnoxBiseQQ.png)

### Tanınmak İstenen Kişiyi/Nesneyi Çerçeve İçerisine Alma

YOLO ile nesne tespiti yapabilmek için, indirdiğimiz resimler içerisindeki
tanımak istediğimiz kişi ya da nesnenin çerçevesini (bounding box) belirlememiz
gerekiyor.<br> Bunun için [BBox Label
Tool](https://github.com/yavuzKomecoglu/BBox-Label-Tool) aracını kullanıyoruz.
Github reposunu kendi bilgisayarımıza klonlayarak, **main.py **içerisinde
[128.satır](https://github.com/yavuzKomecoglu/BBox-Label-Tool/blob/master/main.py#L128)daki
dosya yolunu, BBox Label Tool’unu indirdiğimiz klasörün tam yolunu belirterek
değiştirelim.


Ben aşağıdaki şekilde düzenledim:


Ayrıca BBox Label Tool, **.JPEG** uzantılı resim dosyalarını aramasına karşın,
bizim resim dosyalarımız** .jpg** olduğundan dolayı **main.py** içerisinde
**.JPEG** değerlerinin hepsini **.jpg** olarak güncelleyelim.

BBox Label Tool klasöründe bulunan 3 klasörün (Examples — Images — Labels)
altına rakamla “002” isminde yeni klasörler açalım ve son olarak Images klasörü
altında oluşturduğumuz “002” klasörü içersine (**BBox-Label-Tool/Images/002**)
oluşturduğumuz verisetimizin resimlerini taşıyalım.

Şimdi tüm resimler etiketlenmeye hazır durumda. BBox Label Tool’u çalıştıralım.


**Image Dir** alanına yeni oluşturduğumuz klasörün adı olan 002 yi yazıp Load
dediğimizde **BBox-Label-Tool/Images/002 **klasörü altındaki resimler
yüklenecektir.<br> Resim üzerinde tanımak istediğimiz kişi veya nesneyi en küçük
çerçeve içine alınacak şekilde işaretleyelim ve sonraki resme geçelim.

Sonraki resime geçildiğinde **BBox-Label-Tool/Labels/002 **klasörü altına resim
dosyasının adıyla .txt dosyası oluşturulduğunu göreceksiniz. Bu dosya
içerisinde, resim üzerinde işaretlediğimiz çerçevenin piksel kordinatlarını
aşağıdaki gibi göreceksiniz.

    1
    317 174 404 273

Bizim şu anda tek bir etiketimiz olduğu için 002 adında tek bir klasörümüz oldu.
Eğer birden fazla etiketimiz var ise her bir etiket için ayrı klasörler
olmalıdır.

### Kişi/Nesne Çerçeve Bilgisini YOLO’ya Uygun Hale Dönüştürme

BBox Label Tool ile oluşturduğumuz .txt dosyaları içerisindeki koordinat
bilgisini YOLO pek sevmiyor :)

Bu .txt’ler içerisindeki değerleri YOLO’nun sevdiği aşağıdaki formata
dönüştürmemiz ve piksel değeri yerine 0–1 arasında oran belirtmemiz gerekiyor.

    [kategori numarası] [nesnenin merkez noktasının X değeri] [nesnenin merkez noktasının Y değeri] [nesnenin genişliğinin X değeri] [nesnenin genişliğinin Y değeri]

`0 0.540909090909 0.184505606524 0.297727272727 0.328236493374`

Bu formata dönüştürmek için Guanghan Ning’nin yazdığı scriptinden
yararlanacağız. İlgili **convert.py** script dosyasını
[buradan](https://github.com/yavuzKomecoglu/BBox-Label-Tool/blob/master/convert.py)
indirebilirsiniz.<br> **Convert.py** dosyasını aşağıdaki şekilde düzenleyelim;

* 15.satırı **classes = [“002”]** şeklinde (etiket değerimiz)
* 34.satırı **mypath = “/home/yavuz/myprojects/BBox-Label-Tool/Labels/002/”**
şeklinde (BBox Label Tool etiketlediğimiz koordinatların kaydedildiği klasör)
* 35. satırı **outpath = “/home/yavuz/darknet/data/ataturk_dataset/”** şeklinde
(YOLO darknet kütüphanesinin bulunduğu klasör altındaki yeni verisetimizin
bulunduğu klasör)
* 37.satırı **cls = “002”** şeklinde (etiket değerimiz)

**Convert.py** dosyamızı düzenledikten sonra çalıştırıyoruz.

     

Convert.py işlemi sorunsuz şekilde tamamlandıysa, 35.satırdaki belirttiğimiz
çıktı yoluna (**“/home/yavuz/darknet/data/ataturk_dataset/”**) YOLO’nun uygun
bulduğu formata dönüştürerek yeni .txt dosyaları oluşturduğunu göreceksiniz.

### Eğitim ve Test Veri Kümesini Oluşturma

Şimdi oluşturduğumuz verisetinden, hangilerinin eğitim için hangilerinin test
için kullanılması gerektiğini belirtmemiz gerekiyor.

Eğitmek için oluşturduğumuz resim ve YOLO’ya uygun formatta düzenlenmiş
koordinat bilgilerini içeren .txt dosyalarının bulunduğu klasör
(**“/home/yavuz/darknet/data/ataturk_dataset/”**) altına, eğitim ve test
kümelerimizi ayırmamıza yarayacak olan scripti
[buradan](https://github.com/yavuzKomecoglu/darknet/blob/master/scripts/process.py)
indirelim.

İndirdiğimiz **process.py** scriptinin dosyasının 7. satırındaki** path_data
**değerini** ‘data/ataturk_dataset/’ **olarak resim ve .txt dosyalarının
bulunduğu veriseti klasörümüz ile değiştirelim.

Scriptimizi çalıştıralım.

    /darknet/data/ataturk_dataset$ sudo python process.py

Script sonunda **‘data/ataturk_dataset/’** altına test.txt ve train.txt
dosyaları oluşturulmuş ve yüzde 10 oranında görselin dosya yolunun test.txt
dosyası içerisine yazıldığını göreceksiniz.

### YOLO için Yapılandırma Dosyalarını Hazırlama

Oluşturduğumuz verisetimiz için cfg klasörü altında **obj.data, obj.names,
yolo-obj.cfg** dosyaları oluşturmamız gerekiyor. <br> Yeni bir**
ataturk-obj.data **dosyası oluşturalım ve aşağıdaki şekilde düzenleyelim. <br>
.data dosyası; kaç sınıf eğiteceğimizi, test ve doğrulama kümelerinin dosya
yollarını, eğiteceğimiz sınıfın etiket adının bulunduğu dosyanın yolunu ve
eğitim sırasındaki yedek dosyalarının bulunacağı klasör bilgisini içeriyor.


Yeni bir **ataturk-obj.names** oluşturalım ve içerisine etiket adını yazalım.


Son olarak hali hazırda var olan **yolo-voc.cfg** dosyasının bir kopyasını
oluşturup dosya adını **ataturk-yolo-voc.cfg** değiştirelim.

**ataturk-yolo-voc.cfg** ağ dosyasını aşağıdaki şekilde düzenleyelim.

* 3. satırdaki **batch** değerini 64 olarak güncelleyelim (siz istediğiniz şekilde
ayarlayabilirsiniz)
* 4. satırdaki **subdivisions** değerini 8 olarak güncelleyelim (siz gpu ve cpu
işlemci sayınıza göre ayarlayabilirsiniz)
* 237. satırdaki (classes + 5)*5 formülüne uygun olarak bizim sınıf sayımız 1
olduğundan dolayı (1+5)*5 = 30 olduğundan **filters=30** olarak güncelleyelim
* 244.satıdaki **classes** değerini bizim sınıf sayımız 1 olduğundan 1 olarak
güncelleyelim.

Eğitim işlemini başlatmamız için son bir adım kaldı.

Sıfırdan eğitmek yerine ImageNet veriseti ile önceden eğitilmiş ağırlıkları
kullanarak eğitimimizi başlatacağız.<br> Ağırlık dosyasını
[buradan](https://pjreddie.com/media/files/darknet19_448.conv.23) indirelim.

### Eğitim (Training)

darknet ana klasörü altında, ataturk-obj.data, ataturk-yolo-voc.cfg ağ dosyamızı
ve darknet19_448.conv.23 ağırlık dosyamızı belirterek eğitim işlemini aşağıdaki
komut ile başlatabiliriz.

    sudo ./darknet detector train cfg/ataturk-obj.data cfg/ataturk-yolo-voc.cfg darknet19_448.conv.23

### Eğitim Nerede Durdurulmalı?

Eğitim sırasında elde edilen sonuçlar arasından ortalama hata değerini (avg)
oldukça düşük (0.08 ler gibi) olduğunda ve artık belli bir süre hiç düşmüyor ise
eğitimi durdurabiliriz. <br> Ortalama hata değerini düşmesi uzun zaman
alacaktır. GPU ile derlenmemiş YOLO kütüphanesi ile eğitim yapılaması tavsiye
edilmez.

> 23: 381.962219, **398.613525 avg,** 0.000000 rate, 2.577178 seconds, 1472 images

### Eğitim Ağırlık Dosyaları

Eğitim sırasında her 100 adımda bir **ataturk-yolo-voc_300.weights** şeklinde
backup klasörü altına ağırlık dosyalarını kaydetmektedir.<br> **900.
iterasyondan sonra ağırlıkları yedek almamaktadır! **<br> **Bu sorunu çözmek
için** darknet/examples/**detector.c** 136. satırı aşağıdaki şekilde
düzenleyebilirsiniz. Bu değişikliğin çalışması için Darknet’i yeniden derlememiz
gerekmektedir.

    if(i%10000==0 || (i < 1000 && i%100 == 0))

Yerine

    if(i%1000==0 || (i < 5000 && i%100 == 0))

Şeklinde değiştirebiliriz.

### Eğitilmiş Modeli Test Etme

Test ve train veriseti içerisinde bulunmayan başka bir resim indirelim ve en son
kaydedilen ataturk-yolo-voc_900.weights ağırlık dosyasını kullanarak örnek
resmin içerisindeki Atatürk’ü tanıyarak çerçeve içerisine alıp alamayacağını
test edelim.

    sudo ./darknet detector test cfg/ataturk-obj.data cfg/ataturk-yolo-voc.cfg backup/ataturk-yolo-voc_900.weights data/ataturk-test.png

Soru ve görüşlerinizi aşağıdaki yorum bölümüne yazabilirsiniz.

Referanslar:

* [https://pjreddie.com/darknet/install/](https://pjreddie.com/darknet/install/)
* [https://pjreddie.com/darknet/yolo/](https://pjreddie.com/darknet/yolo/)
* [https://arxiv.org/abs/1612.08242](https://arxiv.org/abs/1612.08242) *(YOLO9000:
Better, Faster, Stronger)*

* [Deep Learning](https://medium.com/tag/deep-learning?source=post)
* [Computer Vision](https://medium.com/tag/computer-vision?source=post)
* [Artificial
Intelligence](https://medium.com/tag/artificial-intelligence?source=post)
* [Machine Learning](https://medium.com/tag/machine-learning?source=post)
* [Yolo](https://medium.com/tag/yolo?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

