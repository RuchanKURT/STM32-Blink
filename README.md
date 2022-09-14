# STM32 Blink Uygulaması
Bu uygulamada STM32F042K6T6 Geliştirme Kartı üzerinde dahili olarak bulunan D13(PB_3) pinine bağlı kart üzerinde LD3 olarak isimlendirilmiş ve kullanıcı tarafından kontrol edilebilen yeşil renkli ledi yakıp söndürme yani Blink uygulaması yapıldı. 
## Donanım
Bu led, dijital D13 pinine bağlı olduğu için program üzerinden bu pini dijital olarak yakıp söndürüldüğü zaman senkron bir şekilde kart üzerindeki dahili ledde yanıp sönmektedir. Bu ledin haricinde kartın üzerinde 2 adet daha led bulunmaktadır. Bu ledlerden biri kart üzerine kod atılma esnasında yeşil-kırmızı olarak yanıp sönerken diğer ledimiz ise karta besleme yapıldığı zaman kırmızı yanan Power (Güç) ledidir.
![alt text](file:///C:/Users/kurtr/OneDrive/Masaüstü/nucleo_f042k6Pinout.jpeg)
## Yazılım
Bu kartı kodlayabilmek için burada STM32 CUBEIDE programı kullanıldı. Kullanıcı tarafından kontrol edilebilen tek led olan LD3’ü programlamaya dönecek olursak STM32 CUBEIDE programını açıp yeni bir proje oluşturuyoruz. Projeye isim verip kullanacağımız Geliştirme Kartını seçtikten sonra karşımıza Sistemin Konfigürasyon Ayarlarını yapacağımız ekran çıkmaktadır. Ledin bağlı olduğu PB_3(D13) pinini GPIO_OUTPUT olarak ayarlıyoruz ve kolay programlama yapabilmek için ‘LED’ ismini veriyoruz. Sonrasında Clock Konfigürasyon ekranından kartımızın çalışacağı frekansı seçip (biz burada 16MHZ seçtik siz kartınızın desteklediği maksimum değeri seçebilirsiniz) kaydediyoruz ve karşımıza kodlarımızı yazacağımız *main.c* dosyası açılıyor. En başta projede kullanılması gereken kütüphanelerin eklendiği *include* kısmında “main.h” kütüphanemiz halihazırda geliyor ve bu proje için ekleme yapmıyoruz. Sonra programımızın sürekli çalışması için *int main()* ana fonksiyonumuz içerisindeki while(1) döngümüzün içine *HAL_GPIO_TogglePin* komutunu yazarak portumuza bağlı pini Toggle etmesini yani o anki durumunu (1/0) değiştirmesini söylüyoruz. Burada fonksiyonumuzun içerisindeki parametrelerde *LED* ibaresi kullanmamızın sebebi Sistem Konfigürasyon Ayarlarından ilgili pinin ismini *LED* olarak ayarlamamız. *HAL_Delay* komutu ile de bu işlemin ne kadar milisaniye sürede gerçekleşeceğini sisteme söylemiş oluyoruz. Bu şekilde bizim D13 pinine bağlı olan yeşil ledimiz sürekli olarak 2 saniye aralıklarla yanıp sönmeye başlıyor. Böylelikle Blink uygulaması gerçekleştirmiş oldu.
```
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  HAL_GPIO_TogglePin(LED_GPIO_Port, LED_Pin);
	  HAL_Delay(2000);
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  ```
