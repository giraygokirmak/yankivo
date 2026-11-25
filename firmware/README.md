# Firmware

Bu klasör, ESP32-WROOM / NodeMCU-32S üzerinde çalışacak firmware için ayrılmıştır.

Şu anda derlenebilir firmware bulunmamaktadır. İlk uygulama kapsamı:

1. [Donanım pinlerindeki](../hardware/README.md) I²S saat ve veri hatlarını doğrulamak.
2. Mikrofon ve MAX98357A sürücülerini ayrı testlerle çalıştırmak.
3. Amfi GPIO27 kontrolünü ve ses döngüsünü eklemek.
4. Güvenli Wi-Fi akışı ve yapılandırma katmanını uygulamak.
5. Doğrulanmış derleme/yükleme komutlarını ve örnek yapılandırmayı burada belgelemek.

Ağ ve gizli anahtarlar kaynak dosyalarına veya Git geçmişine yazılmamalıdır.
