# Yapay Zeka İçin Temel Matris Matematiği: Teknik Brifing

## 📋 Yönetici Özeti

Bu belge, yapay zeka algoritmalarının temelini oluşturan matris kavramlarını ve bu yapılar üzerindeki matematiksel işlemleri incelemektedir. Yapay zeka öğrenme süreçlerinin kütüphane kullanımına ihtiyaç duymadan, tamamen matematiksel olarak kodlanabilmesi için matrislerin arka plandaki çalışma mantığının kavranması kritik önem taşımaktadır.

Belge; matris tanımlarını, temel aritmetik işlemleri (toplama/çıkarma), skaler çarpımı, Hadamard çarpımını, matris çarpımını (nokta çarpımı) ve eksen tabanlı toplama işlemlerini **somut sayısal örneklerle** ele almaktadır.

---

## 1. Matris Kavramı ve Temel Tanımlar

Matrisler, birden fazla sayının bir çatı altında toplandığı sayı tablolarıdır. Bu yapılar, verilerin ayrı ayrı değişkenlerde tutulması yerine organize bir şekilde yönetilmesini sağlar.

Örnek bir $3 \times 3$ matris:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
$$

### 1.1. Gösterim ve Boyutlandırma

- **İsimlendirme:** Matrisler genellikle büyük harflerle ($A$, $B$, $C$ vb.) tanımlanır.
- **Boyut (Dimension):** Matrisin büyüklüğü, satır (Row) × sütun (Column) sayısı ile belirlenir. Genellikle matris isminin sağ alt köşesinde ($A_{2 \times 2}$) ifade edilir.
- **Notasyon Farklılıkları:** Bazı yabancı kaynaklarda (özellikle Amerika ve Kanada kökenli) matris boyutu doğrudan harfin altına yazılabilir.

| Terim | Tanım |
|---|---|
| Satır (Row) | Matristeki yatay dizilim |
| Sütun (Column) | Matristeki dikey dizilim |
| Element | Matrisin içindeki her bir bireysel sayısal değer |

Yukarıdaki $A$ matrisinde $a_{21} = 4$ (2. satır, 1. sütun elemanı) gibi bir gösterim kullanılır.

---

## 2. Temel Aritmetik İşlemler: Toplama ve Çıkarma

### 2.1. İşlem Şartları

Toplama ve çıkarma işleminin gerçekleştirilebilmesi için her iki matrisin satır ve sütun sayılarının **tamamen eşit** olması gerekir. Boyutları farklı olan matrisler arasında standart toplama/çıkarma işlemi yapılamaz.

### 2.2. Uygulama Yöntemi (Element-Wise) — Örnek

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\quad
B =
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$

**Toplama ($A + B$):**

$$
A + B =
\begin{bmatrix}
1+5 & 2+6 \\
3+7 & 4+8
\end{bmatrix}
=
\begin{bmatrix}
6 & 8 \\
10 & 12
\end{bmatrix}
$$

**Çıkarma ($A - B$):**

$$
A - B =
\begin{bmatrix}
1-5 & 2-6 \\
3-7 & 4-8
\end{bmatrix}
=
\begin{bmatrix}
-4 & -4 \\
-4 & -4
\end{bmatrix}
$$

İşlemler eleman düzeyinde (element-wise) gerçekleştirilir: birinci matrisin $i$. satır $j$. sütunundaki değer ile ikinci matrisin aynı konumundaki değeri toplanır/çıkarılır. Sonuç matrisinin boyutu, işleme giren matrislerle aynı kalır.

### 2.3. Matematiksel Kurallar

- **Değişme Özelliği:** Toplamada geçerlidir → $A + B = B + A$. Çıkarmada geçerli **değildir** → $A - B \neq B - A$.
- **Birleşme Özelliği:** Toplama ve çıkarmada geçerlidir → $(A + B) + C = A + (B + C)$.

---

## 3. Çarpma İşlemi Türleri

Matris matematiğinde üç temel çarpma yöntemi bulunur.

### 3.1. Skaler Çarpma

Bir matrisin, "skaler" adı verilen tek bir gerçek sayı ile çarpılmasıdır. Matrisin içindeki tüm elemanlar ilgili skaler sayı ile tek tek çarpılır; sonuç matrisinin boyutu orijinal matris ile aynıdır.

$$
k = 3, \qquad
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
$$

$$
k \cdot A =
\begin{bmatrix}
3\times1 & 3\times2 \\
3\times3 & 3\times4
\end{bmatrix}
=
\begin{bmatrix}
3 & 6 \\
9 & 12
\end{bmatrix}
$$

### 3.2. Hadamard Çarpımı (Element-Wise Product)

Notasyonel olarak genellikle bir çember ($\circ$) ile gösterilir.

- **Şart:** İşleme giren matrislerin boyutları tamamen aynı olmalıdır.
- **Yöntem:** Aynı indeksteki elemanlar birbiriyle çarpılır.
- **Özellik:** Değişme özelliği vardır → $A \circ B = B \circ A$.

$$
A =
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
\quad
B =
\begin{bmatrix}
5 & 6 \\
7 & 8
\end{bmatrix}
$$

$$
A \circ B =
\begin{bmatrix}
1\times5 & 2\times6 \\
3\times7 & 4\times8
\end{bmatrix}
=
\begin{bmatrix}
5 & 12 \\
21 & 32
\end{bmatrix}
$$

### 3.3. Matris Çarpımı (Nokta Çarpımı / Dot Product)

Yapay zekada en sık kullanılan ve en karmaşık çarpma yöntemidir.

- **Temel Şart:** Birinci matrisin sütun sayısı, ikinci matrisin satır sayısına eşit olmalıdır. Aksi halde işlem tanımsızdır.
- **Sonuç Boyutu:** Birinci matrisin satır sayısı × ikinci matrisin sütun sayısı.
- **Önemli Kural:** Değişme özelliği yoktur → $A \times B \neq B \times A$.

Örnek: $A_{2 \times 3} \times B_{3 \times 2}$ çarpımı, sonuçta $2 \times 2$ boyutlu bir matris üretir.

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}_{2\times3}
\qquad
B =
\begin{bmatrix}
7 & 8 \\
9 & 10 \\
11 & 12
\end{bmatrix}_{3\times2}
$$

Birinci matrisin her satırı, ikinci matrisin her sütunuyla sırasıyla çarpılıp toplanır:

$$
A \times B =
\begin{bmatrix}
(1\cdot7+2\cdot9+3\cdot11) & (1\cdot8+2\cdot10+3\cdot12) \\
(4\cdot7+5\cdot9+6\cdot11) & (4\cdot8+5\cdot10+6\cdot12)
\end{bmatrix}
=
\begin{bmatrix}
58 & 64 \\
139 & 154
\end{bmatrix}_{2\times2}
$$

> ⚠️ **Not:** $B \times A$ burada tanımlı olsa da farklı boyutta ($3\times3$) ve farklı bir sonuç verir — bu yüzden matris çarpımında sıra önemlidir.

---

## 4. İleri Düzey İşlemler ve Kavramlar

### 4.1. Eksenli Toplama (Axis-Based / Broadcasting)

Satır ve sütun sayıları eşit olmayan matrisler arasında belirli bir eksen boyunca yapılan toplama işlemidir; yapay sinir ağlarında (ANN) yaygın kullanılır.

- **Sütun düzeyinde toplama:** Matrislerin sütun sayıları arasında bir kat ilişkisi varsa, küçük matris büyük matrisin üzerine "hayali" olarak tekrarlanarak eklenir.
- **Satır düzeyinde toplama:** Satır sayıları arasında kat ilişkisi/eşleşme olduğunda gerçekleştirilir.

Örnek — bir $2\times3$ matrise, $1\times3$'lük bir "bias" satırının eklenmesi:

$$
A =
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6
\end{bmatrix}_{2\times3}
\qquad
b =
\begin{bmatrix}
10 & 20 & 30
\end{bmatrix}_{1\times3}
$$

$$
A + b =
\begin{bmatrix}
1+10 & 2+20 & 3+30 \\
4+10 & 5+20 & 6+30
\end{bmatrix}
=
\begin{bmatrix}
11 & 22 & 33 \\
14 & 25 & 36
\end{bmatrix}
$$

Burada $b$ satırı, sanki $A$'nın satır sayısı kadar (2 kez) tekrarlanmış gibi davranır.

### 4.2. Çok Boyutlu Matrisler ve Tensörler

Matrisler kendi içlerinde başka matrisleri de barındırabilir; bu duruma "iç içe matrisler" veya "çok boyutlu matrisler" denir.

- **Tensör (Tensor):** Çok boyutlu matris yapılarına verilen isimdir.
- **Boyutlandırma:** Örn. $2 \times 2 \times 2$ gibi gösterimler iç içe geçmiş yapıları ifade eder — aşağıdaki gibi, her biri $2\times2$ olan **iki adet** matrisin üst üste dizilmesiyle oluşur:

$$
T =
\left[
\begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix},
\;
\begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}
\right]_{2\times2\times2}
$$

- **Uygulama:** Bu karmaşık yapılar özellikle Evrişimli Sinir Ağları (CNN) algoritmalarının kodlanmasında kritik rol oynar (örn. renkli bir görüntü, $Y\!ükseklik \times Genişlik \times Renk\,Kanalı$ şeklinde 3 boyutlu bir tensördür).

---

## 5. Hızlı Referans Tablosu

| İşlem | Boyut Şartı | Sonuç Boyutu | Değişme Özelliği |
|---|---|---|---|
| Toplama / Çıkarma | Boyutlar tamamen eşit | Aynı | Toplamada var, çıkarmada yok |
| Skaler Çarpım | Şart yok (tek sayı × matris) | Aynı | Var |
| Hadamard Çarpımı ($\circ$) | Boyutlar tamamen eşit | Aynı | Var |
| Matris Çarpımı ($\times$) | 1. matrisin sütunu = 2. matrisin satırı | (1. matrisin satırı) × (2. matrisin sütunu) | **Yok** |
| Eksenli Toplama | Satır veya sütunda kat ilişkisi | Büyük matrisle aynı | — |

---

## 6. Sonuç ve Metodoloji Notu

Yapay zeka algoritmalarının arka planını anlamak için bu temel matris işlemleri bir "101 dersi" niteliğindedir. Matematiksel operasyonların kütüphane kullanmadan manuel olarak gerçekleştirilmesi, algoritmaların fonksiyonel derinliğini ve veri işleme mantığını kavramayı sağlar. Karmaşık modellerin inşasında (örneğin CNN), bu temel taşlar üzerine inşa edilen tensör yapıları kullanılmaktadır.
