# Yanviko mimarisi

Bu belge hedeflenen tasarımı açıklar. Henüz uygulanmış bir iletişim protokolü veya üretim
hazır sistem iddiası taşımaz.

## Sistem bileşenleri

### 1. ESP32 firmware

- I²S mikrofon ve MAX98357A amfi sürücüleri
- Örnekleme, çerçeveleme ve ses tamponları
- Amfi kapatma/açma ve hata durumları
- Wi-Fi ve cihaz kimliği yapılandırması
- Sunucuya ses gönderme, gelen sesi çalma ve bağlantıyı izleme

### 2. OpenClaw bağdaştırıcısı

- Cihaz kimlik doğrulaması ve oturum yaşam döngüsü
- Konuşma-metin (`STT`) ve metin-konuşma (`TTS`) sağlayıcılarının bağlanması
- OpenClaw istek/yanıt akışı ile cihaz oturumu arasında eşleme
- Ses akışı ile sıraya alma, iptal ve zaman aşımı denetimi

OpenClaw’un bulunduğu ortama ve seçilen entegrasyon API’sine göre bağdaştırıcı tasarımı
ayrıca kesinleştirilecektir.

### 3. Ses ve kontrol protokolü

İlk uygulamadan önce aşağıdakiler açık bir sözleşme olarak belgelenmelidir:

| Konu | İzlenecek yaklaşım |
|---|---|
| Taşıma | TLS destekli WebSocket veya eşdeğer güvenli akış |
| Kimlik doğrulama | Gizli anahtarları dışarıda tutulan cihaz jetonu |
| Kontrol mesajları | Sürümlü, şemayla doğrulanan JSON |
| Ses paketleri | Başlık, sıra numarası ve zaman bilgisi içeren ikili çerçeveler |
| Başlangıç biçimi | PCM; bant genişliği gerekirse Opus daha sonra değerlendirilecek |
| Örnekleme | Donanım STT/TTS sağlayıcılarıyla birlikte belirlenecek; varsayılan 16 kHz / 16-bit / mono |
| Dayanıklılık | Kalp atışı, yeniden bağlanma, zaman aşımı ve sınırlı tampon |

Bu değerler bağlayıcı sözleşme değil, ilk prototip için başlangıç kararlarıdır.

## Oturum akışı

1. Cihaz yapılandırmayı ve ses sürücülerini başlatır.
2. Sunucuya kimliği doğrulanmış bir bağlantı kurar ve yeteneklerini bildirir.
3. Mikrofon çerçevelerini gönderir; gerekirse konuşma başlangıç/bitiş bilgisi ekler.
4. Bağdaştırıcı STT, OpenClaw ve TTS aşamalarını yönetir.
5. Yanıt sesi cihaza akıtılır ve amfi yalnızca çalma sırasında etkinleştirilir.
6. Yeni istek, iptal veya bağlantı kaybında mevcut oynatma güvenli biçimde sonlandırılır.

## Güvenlik ilkeleri

- Wi-Fi, sunucu, STT/TTS veya OpenClaw kimlik bilgileri depoya eklenmez.
- Üretim bağlantılarında TLS sertifika doğrulaması devre dışı bırakılmaz.
- Cihaz jetonları gerektiğinde iptal edilebilir ve tek cihaza özel olabilir.
- Mikrofonun ne zaman gönderim yaptığı açıkça görünür olmalıdır.
- Kayıt, gizli anahtar ve kişisel konuşma içeriği loglara yazılmaz.

## Geliştirme aşamaları

- **Aşama 0 — Donanım doğrulaması:** Besleme, pinler, tek yönlü mikrofon ve hoparlör testi.
- **Aşama 1 — Ses döngüsü:** Ağ olmadan mikrofon → amfi döngüsü ve seviye ölçümü.
- **Aşama 2 — Güvenli akış:** Sürümlü protokol, cihaz oturumu ve yeniden bağlanma.
- **Aşama 3 — OpenClaw:** STT/agent/TTS entegrasyonu ve uçtan uca yanıt.
- **Aşama 4 — Ürünleştirme:** Yapılandırma arayüzü, testler, muhafaza ve kurulum rehberi.
