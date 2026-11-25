# Donanım ve bağlantılar

## Hedef donanım

- ESP32-WROOM tabanlı NodeMCU-32S
- Google AIY Voice HAT

> Aşağıdaki eşleme mevcut proje notundaki hedef bağlantıyı belgeler; test edilmiş bir PCB
> şeması veya üretim onayı değildir. İlk enerji vermeden önce kart revizyonunu ve sinyal
> yönlerini ölçerek doğrula.

## NodeMCU-32S ↔ Voice HAT

| NodeMCU-32S | Voice HAT fiziksel pini | İşlev | Yön |
|---|---|---|---|
| GPIO26 | Pin 12 | I²S bit saati (`BCLK`) | ESP32 → HAT |
| GPIO25 | Pin 35 | I²S kelime saati (`LRCLK` / `WS`) | ESP32 → HAT |
| GPIO22 | Pin 40 | I²S veri çıkışı (`DOUT`) | ESP32 → MAX98357A |
| GPIO34 | Pin 38 | I²S veri girişi (`DIN`) | Mikrofon → ESP32 |
| GPIO27 | Pin 36 | Amfi etkin / kapatma kontrolü | ESP32 → HAT |
| 3V3 | Pin 17 | 3,3 V hattı | Güç |
| VIN / 5V | Pin 2 **veya** 4 | HAT 5 V beslemesi | Güç |
| GND | Pin 6 | Ortak referans | Güç |

## Firmware pin tanımları için adlandırma

| Sabit | GPIO | Not |
|---|---:|---|
| `I2S_BCLK` | 26 | ESP32 çıkışı |
| `I2S_LRCLK` | 25 | ESP32 çıkışı |
| `I2S_DOUT` | 22 | Amfiye seri veri |
| `I2S_DIN` | 34 | Yalnız giriş; mikrofondan seri veri |
| `AMP_ENABLE` | 27 | Kart revizyonuna göre aktif seviyeyi doğrula |

Tarif edilen bağlantılarda iki I²S veri yönü birlikte kullanılır. Gerçek sürücü tasarımında
saat paylaşımı, tam çift yönlü veri yolu ve kullanılan mikrofon kartının faz/slot ayarları
ayrıca doğrulanmalıdır.

## Güvenlik ve doğrulama

- Enerji bağlantılarını kartlar enerjisizken yap.
- 5 V pini için pin 2 ve pin 4’ten **yalnızca birini** kullan.
- 3,3 V sinyalleri ile 5 V hatlarını karıştırma; GPIO’lara 5 V uygulama.
- USB ve harici 5 V beslemesini birlikte kullanırken NodeMCU kartının güç yolunu kontrol et.
- GPIO34 giriş pinidir; amfi kontrolü veya veri çıkışı olarak kullanılamaz.
- Beslemeyi ilk kez vermeden önce VIN/5V–GND ve 3V3–GND arasında kısa devre kontrolü yap.
- Mikrofon, amfi ve hoparlörü ayrı aşamalar olarak doğrula; ardından çift yönlü akışı test et.

## Üretilecek teknik çıktılar

- Kart revizyonlarına göre şema ve bağlantı diyagramı
- Hoparlör gücü ve güç kaynağı bütçesi
- Gürültü/EMI için GND ve besleme yerleşimi
- Muhafaza, mikrofon açıklığı ve hoparlör montajı
