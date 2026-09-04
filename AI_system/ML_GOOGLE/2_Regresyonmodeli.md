# REGRESYON MODELİ: Tek Değişkenli Lineer Regresyon ve Maliyet Fonksiyonu

## 1. Temel Notasyonlar ve Terminoloji
- **$x$:** Giriş değişkeni (*feature* / özellik) — Örn: Evin metrekaresi.
- **$y$:** Gerçek hedef değişken (*target* / doğru etiket) — Örn: Evin gerçek satış fiyatı.
- **$\hat{y}$ ($y$-şapka):** Modelin girdi $x$'e karşılık ürettiği tahmini çıktı değeri.
- **$m$:** Eğitim veri setindeki toplam örnek sayısı.
- **$(x^{(i)}, y^{(i)})$:** Veri setindeki $i$'ninci eğitim örneği (Buradaki parantezli $i$ üs alma değil, indis gösterimidir).

---

## 2. Model Fonksiyonu (Tek Değişkenli Lineer Regresyon)
Verideki girdi ve çıktı ilişkisini doğrusal bir çizgi ile modelleme yaklaşımıdır (*Univariate Linear Regression*):

$$f_{w,b}(x) = wx + b$$

- **$w$ (*weight* / ağırlık):** Çizginin eğimini belirler.
- **$b$ (*bias* / y-kesişimi):** Çizginin dikey ekseni kestiği sabit noktayı belirler.
- **Amaç:** Veri noktalarına en uygun düz çizgiyi çizecek $w$ ve $b$ değerlerini bulmaktır.

---

## 3. Maliyet Fonksiyonu (Cost Function / MSE)
Modelin tahminlerinin ($\hat{y}$) gerçek değerlerden ($y$) ne kadar saptığını ölçen fonksiyondur. Regresyonda standart olarak **Hata Kareler Ortalaması** (*Mean Squared Error - MSE*) kullanılır:

$$J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} \left( f_{w,b}(x^{(i)}) - y^{(i)} \right)^2$$

- **Hata Terimi:** $\left(f_{w,b}(x^{(i)}) - y^{(i)}\right)$ farkı ölçülür, negatiflikten kurtulmak ve büyük hataları daha sert cezalandırmak için karesi alınır.
- **Ortalama ($1/m$):** Veri sayısı arttıkça maliyetin yapay şekilde büyümesini engeller.
- **$\frac{1}{2}$ Çarpanı:** İleride türev (gradyan) alma işlemlerinde matematiksel kolaylık sağlamak ve paydadaki 2 ile üssün sadeleşmesi için eklenmiştir.

---

## 4. Maliyet Fonksiyonunun Geometrik Sezgisi

### A. Tek Parametreli Durum ($b = 0 \rightarrow f_w(x) = wx$)
- Model sadece eğim ($w$) üzerinden incelendiğinde, $J(w)$ grafiği **U şeklinde (parabol)** bir eğri oluşturur.
- Çizgi veriye tam oturduğunda hata minimuma ($J(w) \approx 0$) yaklaşır.
- Eğim doğrudan uzaklaştıkça parabolün kolları yukarı doğru hızla tırmanır.

### B. İki Parametreli Durum ($w$ ve $b$)
- **3 Boyutlu Yüzey:** $w$, $b$ taban eksenleri ve yükseklik olarak $J(w,b)$ alındığında, fonksiyon **3 boyutlu bir çorba kasesi / hamak** şeklini alır.
- **Kontür Grafikleri (*Contour Plots*):** Bu 3D kaseyi yatay dilimlere ayırdığımızda eş merkezli elipsler elde edilir.
  - Aynı elips üzerindeki tüm $(w, b)$ çiftleri eşit maliyet değerine ($J$) sahiptir.
  - Elipslerin tam merkezi (kasenin dibi), maliyetin en küçük olduğu **global minimum** noktasıdır.
  - Merkez noktaya karşılık gelen $(w, b)$ değerleri, eğitim verisine en iyi uyan regresyon doğrusunu üretir.

---

<img width="2752" height="1536" alt="Gemini_Generated_Image_ale6zqale6zqale6" src="https://github.com/user-attachments/assets/b73f7ab8-926d-444a-9920-5d2d3b2819bb" />

## 5. Sonraki Adım: Otomatik Optimizasyon
Doğru parametreleri grafikten el yordamıyla aramak karmaşık problemlerde imkansızdır. Bu nedenle $J(w,b)$ değerini otomatik olarak minimuma indiren algoritma kullanılır:
- **Gradient Descent (*Dereceli Azalma*)**
















