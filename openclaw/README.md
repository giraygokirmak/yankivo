# OpenClaw entegrasyonu

Bu klasör, Yanviko cihazları ile OpenClaw arasındaki bağdaştırıcıyı ve protokol sözleşmesini
barındıracaktır.

Şu anda çalışır bir entegrasyon bulunmamaktadır. Uygulamadan önce kullanılacak OpenClaw
sürümü, desteklenen eklenti/araç API’si ve STT/TTS sağlayıcıları belirlenecektir.

Planlanan sorumluluklar:

- Cihaz kaydı ve kimlik doğrulama
- Ses ve kontrol oturumu
- STT → OpenClaw → TTS orkestrasyonu
- Yanıt iptali, zaman aşımı ve bağlantı hataları
- Gizli bilgi içermeyen gözlemlenebilirlik ve entegrasyon testleri

Hedef mimari için [docs/architecture.md](../docs/architecture.md) dosyasına bakın.
