# Derin Öğrenme Modellerini Kullanan Bir Web Uygulamasının Geliştirilmesi

Merhaba, <br> Bu yazımızda [Keras](http://keras.io/) ile eğitilen bir derin
öğrenme modelini kullanmak ve test etmek için bir web uygulamasını nasıl
geliştirip ücretsiz olarak host edebiliriz birlikte görelim.

![](https://cdn-images-1.medium.com/max/800/1*pgb3_b9VQq0aMYGYtvCL6A.png)
<span class="figcaption_hack">[https://vision-image-classify.herokuapp.com](https://vision-image-classify.herokuapp.com/)</span>

### Python Flask ile Web Uygulaması

[Flask](http://flask.pocoo.org/), Python tabanlı web uygulamaları
geliştirebileceğiniz mikroçatı(microframework)’dır.

Öncelikle Flask’ı yükleyelim.

     

Yeni bir app.py python dosyası oluşturalım ve aşağıdaki python kodlarını
yazalım.

`@app.route("/")` ile localhost:5000/ adresine istek gönderildiğinde ve `def
main():` fonksiyonu ile dönecek içerik için çağrılacak fonksiyon tanımlanıyor.

Terminalden oluşturduğumuz **app.py** kodumuzu çalıştıralım.

`python app.py`

<span class="figcaption_hack">`app.py`</span>

Terminalde **Running on **[http://127.0.0.1:5000/](http://127.0.0.1:5000/)**
ç**ıktısını gördüğümüzde tarayıcımızdan
[http://localhost:5000/](http://localhost:5000/)** **adresine gittiğimizde
main() fonksiyonunda döndüğümüz string değerini göreceğiz.

### Flask ile HTML Template Kullanma

Yeni bir **templates** klasörü açalım ve templates klasörü içerisine bir
**index.html** dosyası oluşturalım ve aşağıdaki html kodlarını yazalım.

**app.py **python dosyamızda **render_template** paketini import edelim ve**
main() **fonksiyonunu, yeni oluşturduğumuz index.html’i çağırması için aşağıdaki
şekilde yeniden düzenliyoruz.

Terminalden yeniden **app.py’**yi çalıştırdığımızda aşağıdaki gibi html
sayfasını göreceğiz.

Python Flask ile basit bir web uygulamasını bu şekilde geliştirebilirsiniz.

### Derin Öğrenme Web Uygulaması Geliştirme

Şimdi web uygulamamızı geliştirerek derin öğrenme modelini nasıl
çalıştırabileceğimize bakalım.

Gerekli Keras paketlerini, resim sınıflandırma için kullanacağımız ağımız olan
ResNet50 paketini ve ön işlemler için gerekli diğer paketleri ekleyelim.

Resim sınıflandırma için ImageNet veriseti ile eğitilmiş modelimizi ve ağırlık
dosyalarını yükleyelim.

Form post metodu ile gönderilen resim dosyasını modelin uygun giriş formata
getiren bazı ön işlemler uygulandıktan sonra modele gönderilip tahmin
(prediction) sonucunun alındığı ve json formatında geri döndürdüğümüz predict()
fonksiyonunu aşağıdaki gibi tanımlayalım.

Son olarak geriye kalan bu servisi başlatmak.

Uygulamamızın bu hali ile bir REST API olarak kullanabilir durumdayız.

Terminalden uygulamamızı çalıştırdıktan sonra başka bir terminalden
[http://0.0.0.0:5000/predict](http://0.0.0.0:5000/predict)** **adresine örnek
bir resmimizi curl ile post ediyoruz.<br> Örnek olarak amerikan papağını resmini
sınıflandırmaya çalışalım:

Aşağıdaki gibi göndermiş olduğumuz resim modelde sınıflandırarak json sonucunu
bize dönüyor. <br> Sonuçlar arasında en yüksek oranla **%99**
[macaw](https://www.google.com/search?q=macaw&source=lnms&tbm=isch&sa=X&ved=0ahUKEwjSsOTrhtHaAhVFaxQKHc1VDDEQ_AUICigB&biw=1865&bih=962)
olarak sınıflandırma yaptığını görüyoruz.

Şimdi ise yazmış olduğumuz API’yi kullanarak web arayüzünden bir resim dosyayı
seçerek sınıflandırmayı gerçekleştirelim.

Bunun için **index.html** sayfamıza kullanıcının resim yükleyebilmesi için bir
**form** ve **dosya yükleme** elementleri ekleyelim.

Kullanıcı dosya yükleme elementi ile resim dosyasını seçtikten sonra
‘**Gönder**’ buttonuna tıklandığında, [jquery
ajax](http://api.jquery.com/jquery.ajax/) ile seçilen dosyayı **app.py** python
kodunda tanımladığımız predict() fonksiyonunu çağıran REST API’mize POST isteği
gönderelim.

Uygulamanın tüm kaynak kodlarına
[buradan](https://github.com/yavuzKomecoglu/ai-image-recognition-web)
ulaşabilirsiniz.

Uygulamanın canlı demosunu
[buradan](https://vision-image-classify.herokuapp.com/) deneyebilirsiniz.

Kaynak kodları **Keras** kütüphanesi yüklü bir bilgisayara indirerek
çalıştırabilirsiniz.<br> Eğer bu uygulama için yeterli donanımınız yoksa veya
derin öğrenme kütüphaneleri yüklü değil ise online olarak Google Colab üzerinde
[buradan](https://colab.research.google.com/drive/1qhtbob_ZUxGFd8q9xbCy28S8UwXIQNwE)
deneyebilirsiniz.

Uygulamayı herkes tarafından erişilebilen bir web uygulaması olarak yayınlamak
isterseniz yazıyı okumaya devam edebilirsiniz.

### Web Uygulamasını Heroku Üzerinde Yayınlama

[Heroku](https://www.heroku.com/), birçok dil desteği olan, uygulama alt yapısı
sağlayan bir bulut platformudur.

Heroku’ya uygun düzenlemeleri yapmak ve kendiniz heroku uygulaması oluşturmak
isterseniz gerekli adımları [Sıddık Açıl](https://medium.com/@sddkal)’ın
aşağıdaki yazısına göz atabilirsiniz.

Veya herhangi bir işlem yapmadan Heroku üzerinden bir hesap oluşturarak bu
uygulamaya özel olarak hazırladığım aşağıdaki button ile [tek
tıkla](https://heroku.com/deploy?template=https://github.com/yavuzKomecoglu/ai-image-recognition-web)
kendi heroku hesabınız altında hızlıca yayına alabilirsiniz.

![](https://cdn-images-1.medium.com/max/800/1*SfzRiagJO8wCH60szjj9yA.png)
<span class="figcaption_hack">[https://heroku.com/deploy?template=https://github.com/yavuzKomecoglu/ai-image-recognition-web](https://heroku.com/deploy?template=https://github.com/yavuzKomecoglu/ai-image-recognition-web)</span>

*****

Görüşlerinizi aşağıdaki yorum bölümüne yazabilirsiniz.<br> Sorularınızı
Türkiye’nin yapay zeka alanındaki tek soru&cevap platformu olan [Deep Learning
Türkiye’nin Soru&Cevap Sitesi](https://sorucevap.deeplearningturkiye.com/)’nde
sorabilirsiniz.

**Kaynaklar:**

* [http://flask.pocoo.org/](http://flask.pocoo.org/)
* [https://blog.keras.io/building-a-simple-keras-deep-learning-rest-api.html](https://blog.keras.io/building-a-simple-keras-deep-learning-rest-api.html)
* [https://www.pyimagesearch.com/2018/01/29/scalable-keras-deep-learning-rest-api/](https://www.pyimagesearch.com/2018/01/29/scalable-keras-deep-learning-rest-api/)

* [Deep Learning](https://medium.com/tag/deep-learning?source=post)
* [Keras](https://medium.com/tag/keras?source=post)
* [Flask](https://medium.com/tag/flask?source=post)
* [Heroku](https://medium.com/tag/heroku?source=post)
* [Artificial
Intelligence](https://medium.com/tag/artificial-intelligence?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

