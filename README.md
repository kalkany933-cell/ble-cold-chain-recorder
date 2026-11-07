# ble-cold-chain-recorder
İlaç ve aşılar için BLE tabanlı sıcaklık takip etiketi
İlaç ve Aşı İçin Soğuk Zincir Kaydedici (BLE Etiket)

Proje

İlaç ve aşıların soğuk zincir koşullarını izlemek amacıyla sıcaklığı ölçen, BLE reklam yayını üzerinden kablosuz olarak alıcıya ileten ve düşük güç tüketimiyle çalışan pilli bir verici etiket geliştirmek.

Kapsam

Bu çalışmada yalnızca sistemin verici (BLE etiket) alt sistemi geliştirilecektir.

Benim sorumluluğumdaki bileşenler:

- Sıcaklık sensörü ile ortam sıcaklığının ölçülmesi.
- Mikrodenetleyici üzerinden sensör verilerinin okunması.
- Sıcaklık bilgisinin BLE reklam paketi biçiminde hazırlanması.
- BLE advertising üzerinden sıcaklık verisinin yayımlanması.
- Uyku ve aktif çalışma akımlarının ölçülmesi.
- Pil ömrünün hesaplanması ve güç tüketiminin değerlendirilmesi.

Kapsam dışında olanlar:

- Telefon uygulaması.
- Veri belleği ve kayıt sistemi.
- Sıcaklık grafiği.
- Bulut sistemi.
- Ekran ve kullanıcı arayüzü.
- Alıcı tarafının yazılım geliştirmesi.

Başarı ölçütleri

Ölçüt| Hedef
Referans termometreye göre sıcaklık ölçüm hatası| ±1 °C veya daha az
Tahmini pil ömrü| En az 30 gün

Başarı ölçütleri laboratuvar ölçümleri ve hesaplamalarla doğrulanacaktır.

Blok şema

             PİL
              |
              v
     BLE MİKRODENETLEYİCİ
              ^
              |
       I²C BAĞLANTISI
              |
       SICAKLIK SENSÖRÜ
              |
              v
       BLE REKLAM YAYINI
              |
              v
       ALICI / TELEFON
       (KAPSAM DIŞI)

Seçilecek kart: ___

Seçilecek sıcaklık sensörü: ___

Sensör bağlantı türü: ___

Not: I²C bağlantısı, TMP117 ön seçimine dayalıdır. Nihai sensör seçimiyle doğrulanacaktır.

Malzeme listesi

Parça| Adet| Kaynak| Fiyat
BLE mikrodenetleyici kartı| 1| Ödünç alınacak / doğrulanacak| ___ TL
Dijital sıcaklık sensörü| 1| Ödünç alınacak / doğrulanacak| ___ TL
Pil| ___| Laboratuvardan / ödünç| ___ TL
Pil yuvası| ___| Laboratuvardan / ödünç| ___ TL
Bağlantı kabloları| ___| Laboratuvardan| ___ TL
Referans termometre| 1| Laboratuvardan / ödünç| ___ TL
Akım ölçüm cihazı| 1| Laboratuvardan / ödünç| ___ TL

Arayüz sözleşmesi

Verici, sıcaklık bilgisini BLE reklam yayını üzerinden alıcı tarafa iletecektir.

Önerilen reklam veri alanı:

Alan| Boyut| Birim / ölçek| Örnek
Sıcaklık| 2 bayt| 0,01 °C| 4,25 °C = 425
Zaman damgası| 4 bayt| Saniye (Unix zamanı)| ___
Pil seviyesi| 1 bayt| %1| ___

Toplam veri alanı: 7 bayt.

Kodlama önerisi:

- Sıcaklık: İşaretli 16 bit tam sayı.
- Zaman damgası: İşaretsiz 32 bit tam sayı.
- Pil seviyesi: İşaretsiz 8 bit tam sayı.

Alıcı tarafı, reklam paketini bu alan sırasına ve veri biçimine göre çözümleyecektir.

Notlar:

- BLE reklam türü: ___
- Üreticiye özel veri tanımlayıcısı: ___
- Bayt sıralaması (endianness): ___
- Zaman damgasının oluşturulma yöntemi: ___
- Pil seviyesinin belirlenme yöntemi: ___

Bu alanlar alıcı tarafıyla birlikte kesinleştirilecektir. Zaman damgası ve pil seviyesi henüz doğrulanmamıştır.

Ölçüm planı

1. Sıcaklık doğruluğu: Sensör ve referans termometre aynı ortamda karşılaştırılacaktır. +2 °C ile +8 °C aralığında ölçümler alınacak ve mutlak hata hesaplanacaktır. Hedef ±1 °C veya daha azdır.

2. BLE yayın testi: Sensörün okuduğu sıcaklık bilgisi reklam paketine dönüştürülecek ve alıcı cihazda doğru çözülüp çözülmediği kontrol edilecektir.

3. Akım ölçümü: Kartın uyku modundaki ve aktif çalışma sırasındaki akımları ayrı ayrı ölçülecektir. Kart üzerindeki regülatör, güç LED'i ve USB devresinin tüketimi de dikkate alınacaktır.

4. Pil ömrü hesabı: Ölçülen uyku ve aktif akımlar, çalışma süreleriyle ağırlıklandırılarak ortalama akım hesaplanacaktır.
   
   Ortalama akım:
   
   "I_ort = (I_uyku × t_uyku + I_aktif × t_aktif) / T"
   
   Tahmini pil ömrü:
   
   "Pil ömrü (gün) = Kullanılabilir pil kapasitesi (mAh) / (I_ort (mA) × 24)"
   
   Hedef en az 30 gündür. Kullanılabilir pil kapasitesi, gerçek akım ölçümleri ve çalışma koşulları doğrulanacaktır.

Durum

Yapılanlar

- Projenin verici alt sistemi olarak kapsamı belirlendi.
- Telefon uygulaması, bellek ve grafik geliştirme kapsam dışında bırakıldı.
- Sıcaklık doğruluğu için ±1 °C hedefi belirlendi.
- Tahmini pil ömrü için en az 30 gün hedefi belirlendi.
- BLE reklam yayını kullanılmasına karar verildi.
- Önerilen reklam veri alanları taslak olarak oluşturuldu.

Sıradaki adım

Laboratuvar envanterini kontrol ederek kullanılabilecek BLE kartını ve sıcaklık sensörünü belirlemek. Ardından sensör bağlantısını kurmak, sıcaklık okuma kodunu geliştirmek ve ilk BLE reklam yayınını gerçekleştirmek.

---

Elle kontrol edilmesi gereken 5 madde

- [ ] Laboratuvarda bulunan BLE kartının modelini doğrula.
- [ ] Kullanılacak sıcaklık sensörünün modelini ve veri sayfasındaki +2…+8 °C doğruluğunu kontrol et.
- [ ] Alıcı tarafıyla BLE reklam paketinin alan sırasını, bayt sıralamasını ve zaman damgası yöntemini kesinleştir.
- [ ] Pil seviyesinin nasıl ölçüleceğini ve pilin kullanılabilir kapasitesini belirle.
- [ ] Referans termometre ve akım ölçüm cihazına laboratuvardan erişilebildiğini doğrula.



Literatür Özeti

Soğuk zincir sistemleri üzerine yapılan çalışmalar, aşıların uygun sıcaklık koşullarında saklanması ve sıcaklık ihlallerinin tespit edilmesinin önemini ortaya koymaktadır. Sharma ve arkadaşları (2022) soğutma sistemlerini değerlendirirken, Kumar ve arkadaşları (2019) saha koşullarında sıcaklık ihlallerini ve altyapı sorunlarını incelemiştir. Namgyal ve arkadaşları (2016), dijital veri kaydedicilerin manuel izlemeye göre daha fazla sıcaklık ihlali tespit edebildiğini göstermiştir. Rao ve arkadaşları (2020) ağ kapsama alanı sorunlarını, Kumar ve arkadaşları (2021) ise soğuk zincir altyapısındaki yetersizlikleri ele almıştır. Bu çalışmaların ortaya koyduğu ihtiyaçlardan hareketle bu projede, sıcaklığı otomatik ölçen, BLE reklam yayınıyla ileten ve düşük güç tüketimi hedefleyen pilli bir verici etiket geliştirilecek; sensör doğruluğu ve tahmini pil ömrü deneysel olarak değerlendirilecektir.
