# Giriş: Makine Öğreniminde Araç ve Sistem Mantığı

- **Araç vs. Ustalık:** Algoritmalar birer alettir (çekiç, matkap vb.). Önemli olan sadece araca sahip olmak değil, hangi problemi çözmek için hangi aracı ve yöntemi kullanacağını bilmektir.
- **Doğru Sistem Tasarımı:** Deneyimli takımlar bile yanlış yaklaşımlar yüzünden aylarca sonuç alamayabilir. Amaç, körü körüne deneme yapmak yerine baştan doğru yaklaşımı ve mimariyi seçmektir.
- **Gelecek Konular:**
  - Gözetimli Öğrenme (*Supervised Learning*)
  - Gözetimsiz Öğrenme (*Unsupervised Learning*)
  - Hangi yaklaşımın ne zaman kullanılacağı
 


# Gözetimli Öğrenme (Supervised Learning) & Regresyon

- **Temel Mantık ($x \rightarrow y$ Eşlemesi):** Modele girdi ($x$) ve bu girdiye karşılık gelen doğru sonuçlar ($y$ / etiketler) verilir. Algoritma bu ikili ilişkiden örüntüyü öğrenerek, daha önce hiç görmediği yeni bir $x$ girdisi aldığında en doğru $y$ çıktısını üretir.
- **Kullanım Örnekleri:**
  - **Spam Filtreleme:** E-posta içeriği ($x$) $\rightarrow$ Spam / Değil ($y$)
  - **Konuşma Tanıma:** Ses kaydı ($x$) $\rightarrow$ Metin ($y$)
  - **Makine Çevirisi:** Kaynak dil ($x$) $\rightarrow$ Hedef dil ($y$)
  - **Online Reklamcılık:** Kullanıcı/reklam verisi ($x$) $\rightarrow$ Tıklanma olasılığı ($y$)
  - **Görsel Denetim:** Üretim bandındaki ürün fotoğrafı ($x$) $\rightarrow$ Kusur/çizik tespiti ($y$)
- **Regresyon (Regression):** Çıktının sürekli (sonsuz olasılıklı sayısal bir değer) olduğu gözetimli öğrenme türüdür (Örn: Evin boyutuna göre satış fiyatını tahmin etme).
- **Gelecek Konu:** Gözetimli öğrenmenin ikinci ana türü olan **Sınıflandırma (*Classification*)**.
