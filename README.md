# ses-studio

Kendi sesinizin klonuyla Türkçe seslendirme, Google Colab GPU'sunda. Tek defter, tek hücre; Drive gerekmez.

[![Colab'da aç](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ilkayayas/ses-studio-colab/blob/main/SesStudio.ipynb)

Metni veriyorsunuz, her cümle için dört aday üretiliyor, Whisper en doğrusunu seçiyor; beğenmediğiniz cümleyi işaretleyip
yeniden ürettiriyorsunuz. Son onay sizde.

## Kullanım

1. Yukarıdaki bağlantıyla defteri Colab'da açın.
2. **Çalışma zamanı → Çalışma zamanı türünü değiştir →** bir GPU seçin (A100 önerilir; L4 ve T4'te de çalışır, daha yavaş).
3. Hücreyi çalıştırın (yaklaşık 3 dk). Altında sayfa adresi, kullanıcı adı (`ses`) ve şifre çıkar. Her açılışta yeni şifre
   istemiyorsanız hücredeki `SIFRE` alanına kendi şifrenizi yazın.
4. Sayfada **Ses profili** (`.wav` ya da `.zip`) ve **Metin** (düz metin `.txt` ya da `seslendirme.md` tablosu) yükleyin → **Üret**.
5. Cümleleri dinleyin; beğenmediğinizi **Sorunlu** işaretleyin, gerekirse okunuşu düzeltin → **İşaretlileri yeniden üret**.
6. **Onayla ve birleştir** → `ses.wav` indirin.
7. Bitince **Oturumu kapat**. Oturum kapanınca işler silinir; taşımak için **İşi indir (zip)**, yeni oturumda **İş yükle**.
   Sayfa 30 dakika boş kalırsa oturum kendiliğinden kapanır.

Düz metinde boş satır yeni paragraf, iki boş satır yeni bölüm demek. Sık geçen kelimeler için `sozluk.json` yükleyebilirsiniz.

## Kendi ses profiliniz

1. Sessiz bir odada kaydedin; telefon yeter.
2. Okur gibi değil, anlatır gibi konuşun. Model kaydın temposunu da örnek alıyor.
3. Yaklaşık 2 dakikalık kayıt iyi sonuç veriyor; daha kısası da çalışır ama benzerlik düşebilir.
4. WAV yapın (tek kanal, 48 kHz), baştaki ve sondaki sessizliği kesin:
   ```
   ffmpeg -i kayit.m4a -ac 1 -ar 48000 referans.wav
   ```
5. Sayfadaki **Ses profili** alanına yükleyin.
6. Önce kısa bir metinle deneyin; ses size benzemiyorsa önce kaydı değiştirin.

## Etik

Yalnızca kendi sesinizi ya da açıkça izin veren birinin sesini klonlayın. Ürettiğiniz sesin yapay zekâyla yapıldığını belirtin.

## Sınırlar

- Sayfanın adresi her açılışta değişir; hücrenin altındaki güncel adresi kullanın.
- A100 her zaman verilmeyebilir; L4 de iş görür.
- Model 30'dan fazla dili destekliyor; ses-studio yalnız Türkçeyle denendi.
- Model özel isimlerde ve kısaltmalarda arada bir yanılabilir; son onay sizde.

## Model

[VoxCPM2](https://github.com/OpenBMB/VoxCPM) (OpenBMB, Apache 2.0) ve Whisper (large-v3-turbo).
