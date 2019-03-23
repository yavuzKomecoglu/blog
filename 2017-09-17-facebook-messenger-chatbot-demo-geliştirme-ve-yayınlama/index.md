# Facebook Messenger Chatbot Demo Geliştirme ve Yayınlama

Merhaba, <br> Apple Siri, Microsoft Cortana, Amazon Echo(Alexa), Google
Assistant gibi sesli asistanlar her geçen gün hayatımızda yer etmeye başladılar.
Bunlarla birlikte botlar Telegram, Slack, Kik gibi mesajlaşma uygulamaları
chatbot geliştirilmesine imkan verirken, en popüler Facebook Messenger’ın da
geliştiriciler için bot platformunu ve chatbotlara özel uygulama mağazasını
devreye alması yaygınlaşmasında büyük rol oynadı.

Chatbot, kullanıcıların mesajlaşma platformlarında belirlenmiş kurallar
çerçevesinde hizmet eden bir servistir. Kullanıcılar telefonlarda yüzlerce
uygulamalar ile dolaşmak yerine tek bir arayüz ile bir çok servisi
alabiliyorlar. Yapay zeka (doğal dil işleme) desteği ile konuşmaların doğal
akışını taklit edebilme yeteneği kazandırabilirsiniz.

Şimdi Node.js ile facebook messenger chatbotu adım adım nasıl geliştirebiliriz
ve yayına alabiliriz ona bakalım.

Node.js uygulamasını yayınlamak için [Heroku](https://www.heroku.com/)’dan hesap
açarak yeni bir uygulama oluşturalım.

![](https://cdn-images-1.medium.com/max/800/1*w0sWv_sdBY8N7F_cGJaX5Q.png)

Uygulama adını **chatbotweather** olarak belirlediğimiz için oluşturduğumuz
heroku üzerindeki ücretsiz uygulamamızın erişim adresi
[https://chatbotweather.herokuapp.com/](https://chatbotweather.herokuapp.com/)
olacaktır.

[Buradan](https://developers.facebook.com/apps) bir **Facebook Uygulaması**
oluşturalım, bir isim ile iletişim e-postası verelim ve ürün olarak
**Messenger** seçelim.

Yeni oluşturduğunuz veya mevcut bir sayfayı seçerek sayfa erişim token’ı
oluşturalım.

Facebook’un hızlı bir başlangıç için bize sunduğu demo uygulamasını
[buradan](https://github.com/fbsamples/messenger-platform-samples) indirelim.

Örnek uygulama içerisinde config/default.json içerisindeki <br> **appSecret**
parametresini facebook uygulamamazın dashboard bölümündeki **App Secret **değeri
ile,

**pageAccessToken** parametresini 4. madde de bağladığımız sayfadan oluşturulan
**Page Access Token** değeri ile,

**validationToken** parametresini daha sonra facebook uygulamamız ile
chatbotumuz arasındaki etkileşimi sağlamak için **webhooks** bağlantısını
doğrulamak için kendimizin belirlediği bir değer ile(**test_token**),

serverURL parametresini chatbot uygulamamızın yayında olduğu adres
ile([https://chatbotweather.herokuapp.com/](https://chatbotweather.herokuapp.com/))
değiştirelim.

Dilerseniz public/index.html içerisindeki messenger_app_id ve page_id
parametrelerini de değiştirerek chatbota dinamik erişim buttonları
oluşturabilirsiniz.

Değişiklerimizi yaptıktan sonra şimdi Heroku’ya yayınlayalım.<br> Komut
satırından bilgisayarınızda uygulamanızın bulunduğu klasöre gelerek sırasıyla
aşağıdaki git komutları ile Heroku’ya deploy yapalım.

`heroku login`

Heroku hesabınızın kullanıcı adı ve şifresi ile giriş yapalım

`git add .git commit -am "ilk deploy"git push heroku master`

Tekrar facebook uygulama ayarlarına dönüyoruz. Messenger ayarlarından Setup
Webhooks a tıklayarak yayın adres bilgilerini girelim

**Callback URL** olarak Heroku yayın adresimiz/webhook:
[https://chatbotweather.herokuapp.com/webhook](https://chatbotweather.herokuapp.com/webhook)

**Verify Token **olarak uygulamamız içerisinde config/default.json dosyasında
belirlediğimiz **validationToken** değerini: test_token<br> Ve yetki alanlarının
tamamını işaretleyelim.

**Buraya kadar başarılı şekilde geldiksey şimdi chatbotumuzu test etme zamanı**

Facebook sayfamızın mesaj gönderme bölümünden uygulamamızda text mesajlara cevap
olarak tanımlanmış templateleri (image, gif, audio, video, file, button,
generic, receipt, qucik reply) test edebiliriz.

Node.js uygulamamızın **app.js** içerisindeki **receivedMessage **fonksiyonu
içerisindeki** **örnek kodları inceleyerek kendinize göre düzenleyebilirsiniz.
<br> Kullanıcıdan gelen mesaja göre API’lere istekler yaparak cevapları parse
edip uygun templatelerde cevap olarak dönebilirsiniz.

*****

Hızlı şekilde facebook messengerın örnek chatbotunu nasıl yayına alınacağını ve
facebook sayfasına bağlanacağını göstermeye çalıştım.

Sorularınız olursa yorum kısmından iletişime geçebilirsiniz.

İstanbul’daki nöbetçi eczaneleri bulmanıza yardımcı geliştirdiğim [nöbetçi
eczane
chatbotunu](https://medium.com/@komecoglu.yavuz/facebook-messenger-Ã¼zerinden-nÃ¶betÃ§i-eczaneleri-bulma-eeb88b4f42c6)
da inceleyebilirsiniz.

Kaynak:

* [https://newsroom.fb.com/news/2016/04/messenger-platform-at-f8/](https://newsroom.fb.com/news/2016/04/messenger-platform-at-f8/)
* [https://developers.facebook.com/docs/messenger-platform](https://developers.facebook.com/docs/messenger-platform)

* [Chatbots](https://medium.com/tag/chatbots?source=post)
* [Nodejs](https://medium.com/tag/nodejs?source=post)
* [Facebook Messenger](https://medium.com/tag/facebook-messenger?source=post)
* [Heroku](https://medium.com/tag/heroku?source=post)

### [Yavuz Kömeçoğlu](https://medium.com/@komecoglu.yavuz)

🇹🇷 Machine Learning R&D Engineer
[@KodiksBilisim](http://twitter.com/KodiksBilisim) | Deep Learning Enthusiast |
[http://yavuzkomecoglu.com/](http://yavuzkomecoglu.com/)

