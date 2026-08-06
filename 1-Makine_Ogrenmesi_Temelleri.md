# 🤖 Makine Öğrenmesi 101: Tek Parametreli Model (Dart Problemi)

**Konu:** Bir bilgisayar "öğrenme" eylemini matematiksel olarak nasıl gerçekleştirir?

**Senaryo:** Çapı (yarıçapı) bilinmeyen bir dart tahtasına atılan rastgele atışların `(x, y)` koordinatlarına ve isabet durumlarına bakarak, makinenin tahtanın yarıçapını kendi kendine keşfetmesi.

---

## 1. Problemin Doğası ve Felsefesi

Makine öğrenmesinde amaç, rastgele girdiler ile bilinen sonuçlar (etiketler) arasındaki gizli ilişkiyi (fonksiyonu/çizgiyi) çizmektir.

| Yaklaşım | Girdi | Çıktı |
|---|---|---|
| **Geleneksel Programlama** | Kuralları (`Yarıçap = 30`) ve veriyi (Atış X, Y) verirsin | Bilgisayar sonucu (İsabet mi?) söyler |
| **Makine Öğrenmesi** | Veriyi (Atış X, Y) ve sonucu (İsabet / Iska) verirsin | Bilgisayar kuralı (Yarıçapı) bulur |

Bu videodaki model, tek parametreli (sadece yarıçapı arayan) en ilkel makine öğrenmesi modelidir.

---

## 2. Temel Kavramlar Sözlüğü (Neyin, Neden Adı Bu?)

Bir sistemi hacklemek veya inşa etmek için önce terminolojisinin altındaki mekaniği bilmek gerekir:

- **Parametre / Ağırlık (Weight):** Makinenin bulmaya çalıştığı asıl değer. Bizim örneğimizde *Yarıçap*. Günümüzdeki "Llama 8 Milyar Parametreli" lafındaki parametre, bu yarıçaptan 8 milyar tane olması demektir.
- **Girdi (Input — x, y):** Olayın özellikleri. Bir atışın `x` ve `y` koordinatları.
- **Mesafe Hesabı (Minkowski / Pisagor):** Bir noktanın merkeze (orijine) uzaklığını bulmak için kuş bakışı (Euclidean) hesap yapılır:

  ```
  Mesafe = sqrt(x^2 + y^2)
  ```

  Eğer 3 boyutlu bir uzay olsaydı formüle `+ z^2` eklenecekti.
- **Kayıp / Hata (Loss):** Modelin tahmini ile gerçek veri arasındaki fark. Makinenin öğrenmesi için hatanın sadece miktarını değil, **yönünü** de bilmesi gerekir (`+` veya `-`).
- **Öğrenme Oranı (Learning Rate):** Model hatasını fark ettiğinde, parametreyi (yarıçapı) tek seferde doğrudan hataya eşitlemez. Eğer eşitlerse, ilk gördüğü ters veride tüm doğru sistemi bozar (buna *overfitting/ezberleme* denir). Bunun yerine, doğru değere ufak ufak, örneğin %1 oranında adımlarla yaklaşır.
- **Epok (Epoch):** Algoritmanın, elindeki tüm veri setinin (tüm atışların) üzerinden baştan sona bir kez geçmesine denir.

---

## 3. Öğrenme Algoritmasının Mantıksal Akışı

Bir makinenin öğrenme (Train / Fit) süreci tamamen bir deneme-yanılma (hata düzeltme) döngüsüdür. Şu adımlarla çalışır:

1. **Rastgele Başla (Random Initialization):** Makine yarıçapı bilmediği için rastgele bir sayı sallar. (Örn: `Yarıçap = 54`)
2. **Mesafe Ölç (Forward Pass):** Veri setindeki ilk atışın `(x, y)` merkeze uzaklığı Pisagor ile hesaplanır. (Örn: Uzaklık `35` çıktı).
3. **Tahmin Et (Predict):** Makine kendi kafasındaki yarıçapa (`54`) bakar. Uzaklık (`35`) < Yarıçap (`54`) olduğu için: *"Bu atış İsabet (1) olmalı"* der.
4. **Gerçekle Yüzleş (Calculate Loss):** Veri setindeki gerçek etikete bakılır. Oysaki atış aslında Iska (`0`) geçmiştir. (Yani gerçek yarıçap `35`'ten küçüktür).
5. **Hatayı Yönlü Hesapla:**

   ```
   Hata = Gerçek (0) - Tahmin (1) = -1
   ```

   - **Neden Yönlü?** Hata `-1` çıktığı için makine şunu anlar: *"Benim yarıçapım çok büyük, küçültmem lazım!"*
   - **Tam tersi olsaydı?** `Gerçek(1) - Tahmin(0) = +1` → *"Yarıçapım çok küçük, büyütmem lazım!"*
6. **Ağırlığı Güncelle (Update Weight):**

   ```
   Yeni Yarıçap = Eski Yarıçap + (Hata * Öğrenme Oranı)
   54 + (-1 * 0.01) = 53.99
   ```

   Yeni yarıçap `53.99` oldu.
7. **Döngüyü Tekrarla (Epochs):** Bu işlem yüzlerce atış için (veri seti) ve yüzlerce kez (Epok) tekrarlandığında, başlangıçta sallanan o `54` sayısı, yavaş yavaş gerçek değer olan `~31.1` seviyelerine oturur.

---

## 4. Python ile Core Mantığın Kodlanması

Bu kod, TensorFlow veya PyTorch gibi devasa kütüphanelerin arka planda, en alt seviyede ne yaptığının saf Python simülasyonudur. Bunu anlayan, yapay zekanın çekirdeğini anlamış demektir.

```python
import math

# Veri seti simülasyonu (Örnek: 1 isabet, 1 ıska atış)
# Yapı: {'x': X_Koor, 'y': Y_Koor, 'isabet': Gerçek_Durum(1 veya 0)}
veriseti = [
    {'x': 10, 'y': 10, 'isabet': 1},  # Merkeze yakın, isabetli atış
    {'x': 40, 'y': 40, 'isabet': 0}   # Merkezden uzak, ıska atış
    # ... burada 200 tane atış olduğunu varsayıyoruz
]

# 1. Modelin parametrelerini başlat (Hiçbir şey bilmiyor)
model_yaricapi = 54.0  # Rastgele sallanan başlangıç değeri (Weight)
ogrenme_orani = 0.01   # Adım büyüklüğü (Learning Rate)

# 2. Eğitim Döngüsü (Training Loop)
for epok in range(100):  # Tüm verinin üzerinden 100 kere geç

    for atis in veriseti:
        gercek_deger = atis['isabet']

        # Pisagor (Minkowski) ile kuş bakışı mesafeyi bul
        mesafe = math.sqrt(atis['x']**2 + atis['y']**2)

        # Tahmin (Activation/Prediction): Mesafe model_yaricapindan küçük mü?
        tahmin = 1 if mesafe <= model_yaricapi else 0

        # Hata yönü ve şiddetini bul (Loss)
        hata = gercek_deger - tahmin

        # Ağırlığı Güncelle (Backpropagation mantığının en ilkel hali)
        # Eğer doğru bildiyse Hata = 0 olur, yarıçap değişmez.
        # Eğer yanlış bildiyse Hata +1 veya -1 olur, yarıçap o yönde güncellenir.
        model_yaricapi = model_yaricapi + (hata * ogrenme_orani)

print(f"Eğitim tamamlandı. Makinenin bulduğu Yarıçap (Model): {model_yaricapi}")
```

---

## 5. Mühendislik ve Güvenlik Perspektifinden Notlar

- **Modelin Fiziksel Boyutu:** Eğittiğimiz bu "model", aslında sadece `float64` tipinde tutulan tek bir sayıdan (`model_yaricapi` değişkeninden) ibarettir. Bellekte kapladığı alan tam olarak **8 Byte**'tır. Bir modeli "kaydetmek" (Save Model) demek, bu ağırlık rakamlarını bir diske `.h5` veya `.pt` dosyası olarak yazmaktan başka bir şey değildir. Bu yüzden LLM'ler gigabaytlarca yer kaplar; çünkü bu float sayılarından (parametrelerden) milyarlarca barındırırlar.

- **Aktivasyon Sınırları ve WAF Benzetmesi:** İleride daha karmaşık nöronlara (sinir ağlarına) geçildiğinde, aslında yapılan şey bu dümdüz olan "yarıçap dairesini", çok daha yamuk, girintili çıkıntılı bir sınır çizgisine (*Decision Boundary*) çevirmektir. Bir Web Application Firewall'ın (WAF) SQL Injection saldırısını normal bir metinden ayırması veya anomali tespiti yapması, boyut sayısı binlere ulaşmış devasa bir uzayda bu sınır çizgisinin doğru yere çekilme işlemidir.

- **Veri Seti Neden Bölünür? (Train/Test Split):** Videonun sonlarına doğru bahsedilen "Test verisi ayırma" mantığı şudur: Modeli 200 atışın 180'i ile eğitirsin (Train), kalan 20 atışı hiç göstermezsin. Eğitim bitince, o görmediği 20 atışı modele sorarsın. Eğer onları da doğru biliyorsa, model "ezberlememiş, olayın mantığını öğrenmiştir" denir. Tek parametreli bu dart modelinde ezberleme (overfit) pek mümkün olmasa da, karmaşık sistemlerde bu test ayrımı hayat kurtarır.
