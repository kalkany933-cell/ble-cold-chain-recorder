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



## 1. BLE Kartı Karşılaştırması

Projenin BLE etiket vericisi için üç farklı geliştirme kartı değerlendirilmiştir: **Seeed XIAO nRF52840, Seeed XIAO ESP32-C3 ve Nordic nRF52 DK (nRF52832)**. Kartlar; çalışma akımı, uyku akımı, besleme gerilimi, haberleşme arayüzleri, BLE desteği ve maliyet açısından karşılaştırılmıştır.

| Özellik | Seeed XIAO nRF52840 | Seeed XIAO ESP32-C3 | Nordic nRF52 DK (nRF52832) |
|---|---|---|---|
| Çalışma akımı | Normal çalışma: 10,38 mA | BLE modem modu: 27 mA'dan az | Çip: 0 dBm BLE TX sırasında 5,3 mA (DC/DC, 3 V) |
| BLE reklam akımı | — | — | — |
| Uyku akımı | Düşük güç modu: 5 µA'dan az | Deep-sleep: yaklaşık 44 µA | Çip: System OFF 0,3 µA (3 V) |
| Besleme | 3,7 V Li-ion pil / USB-C 5 V | BAT: 3,7 V / USB: 5 V | Çip: 1,7–3,6 V / Kart beslemesi: — |
| Haberleşme arayüzleri | I²C, SPI, UART, GPIO, ADC | I²C, SPI, UART, GPIO, ADC | I²C/TWI, SPI, UART, GPIO, ADC |
| BLE desteği | BLE 5.x | BLE 5.0 | BLE |
| Yaklaşık fiyat | — TL | — TL | — TL |

**Teknik Notlar:**

- XIAO nRF52840 ve XIAO ESP32-C3 için belirtilen düşük güç değerleri üretici tarafından açıklanan kart seviyesindeki değerlerdir.
- Nordic nRF52 DK sütununda verilen 5,3 mA ve 0,3 µA değerleri yalnızca nRF52832 mikrodenetleyici çipine aittir. Geliştirme kartındaki diğer bileşenler nedeniyle toplam kart akımı farklı olabilir.
- ESP32-C3 için belirtilen 27 mA değeri BLE modem modu değeridir. Bu değer, BLE reklam paketinin gönderilmesi sırasındaki anlık akım olarak değerlendirilmemelidir.
- BLE reklam akımı; reklam aralığı, yayın gücü, kullanılan kart ve çalışma koşullarına bağlı olarak değişebilir. Bu nedenle reklam akımı için ölçüm yapılması gerekmektedir.

### Kart Seçimi ve Gerekçesi

**Seçilen kart: Seeed XIAO nRF52840**

XIAO nRF52840, projenin düşük güç tüketimi ve BLE üzerinden sıcaklık verisi yayınlama hedefleri açısından uygun bir başlangıç adayı olarak belirlenmiştir.

Seçilme nedenleri:

1. BLE 5.x desteği sayesinde sıcaklık verilerinin kablosuz olarak yayınlanabilmesi.
2. Üretici tarafından belirtilen düşük güç modu tüketiminin 5 µA'dan az olması.
3. 3,7 V Li-ion pil ile çalıştırılabilmesi.
4. I²C arayüzü sayesinde sıcaklık sensörüyle haberleşebilmesi.
5. Küçük boyutları sayesinde taşınabilir bir BLE etiket tasarımına uygun olması.

**Güç tüketimi ve pil ömrü değerlendirmesi:**

Projenin hedeflerinden biri en az 30 günlük pil ömrüne ulaşmaktır. Ancak bu süre yalnızca kartın uyku akımı değerine bakılarak garanti edilemez. Mikrodenetleyicinin aktif çalışma süresi, BLE reklam aralığı, sensör tüketimi ve pil kapasitesi birlikte değerlendirilmelidir.

Bu nedenle prototip aşamasında ortalama akım ölçümü yapılacak ve pil ömrü tahmini gerçek ölçüm sonuçlarına göre hesaplanacaktır.

**Sonuç:** XIAO nRF52840, BLE desteği, düşük güç tüketimi ve pil bağlantı imkânları nedeniyle projenin verici birimi için öncelikli kart olarak seçilmiştir.




## 2. Sıcaklık Sensörü Karşılaştırması

Projenin sıcaklık ölçüm birimi için üç farklı sensör değerlendirilmiştir: **TI TMP117, Sensirion SHT31 ve Maxim DS18B20**. Sensörler; ölçüm doğruluğu, çalışma akımı, uyku akımı, besleme gerilimi, haberleşme arayüzü ve maliyet açısından karşılaştırılmıştır.

| Özellik | TI TMP117 | Sensirion SHT31 | Maxim DS18B20 |
|---|---|---|---|
| Ölçüm doğruluğu | ±0,1 °C maksimum (-20…+50 °C) | ±0,2 °C tipik | ±0,5 °C (-10…+85 °C) |
| Çalışma akımı | 3,5 µA (1 Hz dönüşüm) | Maksimum 1500 µA; ortalama 1,7 µA | 1 mA tipik, 1,5 mA maksimum (dönüşüm) |
| Uyku akımı | 150 nA (shutdown) | Ayrı uyku değeri: — | 750 nA tipik |
| Besleme gerilimi | 1,7–5,5 V | 2,4–5,5 V | 3,0–5,5 V |
| Haberleşme arayüzü | I²C / SMBus | I²C | 1-Wire |
| Yaklaşık fiyat | — TL | — TL | — TL |

### Teknik Değerlendirme

- **TMP117:** Üretici tarafından belirtilen ±0,1 °C maksimum hata değeri, -20…+50 °C sıcaklık aralığı için geçerlidir. 1 Hz dönüşümde 3,5 µA akım tüketmesi düşük güç gereksinimi açısından avantaj sağlar.
- **SHT31:** ±0,2 °C değeri tipik doğruluktur; maksimum hata değeriyle karıştırılmamalıdır. Ortalama akım tüketimi 1,7 µA olarak belirtilmiştir.
- **DS18B20:** -10…+85 °C sıcaklık aralığında ±0,5 °C doğruluk sunar. 1-Wire haberleşme arayüzü kullanır ve dönüşüm sırasında tipik 1 mA akım tüketir.

**Önemli:** Sensörlerin doğruluk değerleri farklı sıcaklık aralıklarında ve farklı üretici tanımlarına göre verilmiştir. Bu nedenle değerler doğrudan aynı koşullarda elde edilmiş ölçüm sonuçları olarak değerlendirilmemelidir.

### Sensör Seçimi ve Gerekçesi

**Seçilen sensör: TI TMP117**

TMP117, projenin sıcaklık ölçüm doğruluğu ve düşük güç tüketimi hedefleri açısından öncelikli sensör olarak belirlenmiştir.

Seçilme nedenleri:

1. -20…+50 °C aralığında ±0,1 °C maksimum hata değerine sahip olması.
2. 1 Hz dönüşümde 3,5 µA düşük akım tüketimi sunması.
3. Shutdown modunda 150 nA akım tüketmesi.
4. I²C arayüzü sayesinde XIAO nRF52840 ile kolayca haberleşebilmesi.
5. Projenin ±1 °C ölçüm doğruluğu hedefinin altında bir üretici hata değeri sunması.

### Sonuç

TMP117, yüksek ölçüm doğruluğu ve düşük güç tüketimi nedeniyle BLE tabanlı soğuk zincir kaydedici projesinin sıcaklık sensörü olarak seçilmiştir.

Prototip aşamasında sensörün ölçümleri referans termometre ile karşılaştırılacak ve gerçek ölçüm hatası belirlenecektir. Böylece projenin ±1 °C doğruluk hedefini karşılayıp karşılamadığı test edilecektir.




## 3. Güncellenmiş Malzeme Listesi (BOM)

Projenin BLE verici birimini oluşturmak ve testlerini gerçekleştirmek için gerekli malzemeler aşağıda listelenmiştir.

| Parça | Adet | Durum | Fiyat (TL) |
|---|---:|---|---:|
| Seeed Studio XIAO nRF52840 BLE geliştirme kartı | 1 | Alınacak | — |
| TMP117 sıcaklık sensörü modülü (I²C) | 1 | Alınacak | — |
| 3,7 V Li-Po şarj edilebilir pil | 1 | Alınacak | — |
| Uygun pil bağlantı kablosu / konnektörü | 1 | Alınacak | — |
| Erkek-erkek jumper kablo | 4 | Elimde | — |
| USB-C veri kablosu | 1 | Alınacak | — |
| Breadboard | 1 | Elimde | — |
| Referans termometre | 1 | Alınacak veya ödünç | — |
| Multimetre | 1 | Elimde | — |
| Akım ölçüm cihazı | 1 | Alınacak veya ödünç | — |

**Malzeme Durumu Özeti**

| Durum | Parça Sayısı |
|---|---:|
| Elimde | 3 |
| Alınacak | 5 |
| Alınacak veya ödünç | 2 |
| **Toplam** | **10** |

**Notlar:**

- Fiyatı henüz belirlenmeyen malzemeler için fiyat alanı boş bırakılmıştır.
- Referans termometre ve akım ölçüm cihazı üniversitenin laboratuvarından ödünç alınabiliyorsa satın alma maliyeti oluşmayacaktır.
- Elimde bulunan malzemeler prototip çalışmalarında kullanılacaktır.
- Satın alınacak malzemelerin fiyatları tedarikçi araştırması sonrasında güncellenecektir.




## Donanım seçimi

- **Seçilen BLE kartı:** Seeed Studio XIAO nRF52840
- **Seçilen sıcaklık sensörü:** Texas Instruments TMP117
- **Sensör bağlantısı:** I²C
- **Kablosuz haberleşme:** Bluetooth Low Energy (BLE) Advertising
- **Güç kaynağı:** 3,7 V Li-Po şarj edilebilir pil (kapasite henüz seçilmedi)
- **Sıcaklık doğruluğu hedefi:** ±1 °C
- **Pil ömrü hedefi:** En az 30 gün

## Proje kapsamı

Bu çalışmada yalnızca sıcaklık ölçümü yapan, ölçüm verisini BLE reklam paketleriyle yayınlayan ve düşük güç tüketimi hedefleyen verici etiket geliştirilecektir.

**Dahil:** TMP117 ile sıcaklık ölçümü, XIAO nRF52840 üzerinde veri işleme, BLE reklam paketi oluşturma ve pil tüketiminin ölçülmesi.

**Hariç:** Telefon uygulaması, bulut, grafik arayüzü, uzun süreli veri hafızası ve alıcı tarafı yazılımı.

## Zaman damgası ve pil bilgisi

- **Zaman damgası:** Harici RTC bulunmadığı için ilk sürümde gerçek tarih-saat yerine mikrodenetleyicinin açılışından itibaren geçen süreyi gösteren sayaç kullanılacaktır. Bu değer gerçek takvim zamanı değildir.
- **Pil gerilimi:** Pil gerilimi, XIAO nRF52840 kartının uygun ADC girişinden, gerekli gerilim bölücü bağlantısı kullanılarak ölçülecektir. Gerilim bölücünün değerleri pilin maksimum gerilimine ve ADC sınırlarına göre belirlenecektir.
- **Pil yüzdesi:** Ölçülen pil gerilimi, kullanılan pilin gerilim-deşarj karakteristiğine göre yaklaşık yüzdeye dönüştürülecektir. Bu değer doğrudan kapasite ölçümü değildir ve kalibrasyon gerektirir.





### Literatür Özeti

Soğuk zincir sistemlerinde sıcaklık takibi ve saklama koşullarının korunması, aşı güvenilirliği açısından önemli bir araştırma konusudur. Sharma ve arkadaşları (2022) güneş enerjili soğutma sistemlerini değerlendirirken Kumar ve arkadaşları (2019), saha koşullarında sıcaklık ihlallerini ve altyapı sorunlarını incelemiştir. Namgyal ve arkadaşları (2016), dijital veri kaydedicilerin manuel izlemeye kıyasla sıcaklık ihlallerini tespit etmedeki önemini ortaya koyan karşılaştırmalı bir çalışma gerçekleştirmiştir. Rao ve arkadaşları (2020) eVIN programının sıcaklık ihlalleri üzerindeki etkisini değerlendirirken Kumar ve arkadaşları (2021) aşı firesi ve altyapı yetersizliklerine odaklanmıştır. Bu çalışmalardan hareketle geliştirilen projede, TMP117 sıcaklık sensörü ve XIAO nRF52840 BLE kartı kullanılarak düşük güç tüketimli, otomatik sıcaklık ölçümü ve kablosuz veri yayını yapan bir etiket tasarlanması; ±1 °C doğruluk ve en az 30 gün pil ömrü hedeflerinin test edilmesi amaçlanmaktadır.
