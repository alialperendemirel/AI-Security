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


# Gözetimli Öğrenme: Sınıflandırma (Classification)

- **Temel Mantık:** Çıktının sonlu ve ayrık sayıda kategoriden (sınıftan) biri olduğu gözetimli öğrenme türüdür. Sürekli sayılar yerine belirli etiketleri tahmin eder (Örn: 0 veya 1; Kedi veya Köpek).
- **Regresyon vs. Sınıflandırma:**
  - **Regresyon:** Sonsuz sayıda olası sürekli değer tahmin eder ($150.000$, $183.500$ vb.).
  - **Sınıflandırma:** Yalnızca sonlu sayıda ayrık sınıf/kategori tahmin eder ($0$, $1$, $2$ gibi; ara değerler almaz).
- **Çıktı Türleri:**
  - **İkili Sınıflandırma (*Binary Classification*):** İki olası durum (Örn: İyi huylu tümör = $0$, Kötü huylu tümör = $1$).
  - **Çoklu Sınıflandırma (*Multi-class Classification*):** İkiden fazla durum (Örn: Tip 1 Kanser, Tip 2 Kanser, Kanser Değil).
- **Çoklu Girdi (*Multiple Features*):** Tahmin tek bir değişkene (örn. tümör boyutu) bağlı olmak zorunda değildir; birden fazla özellik (yaş, tümör kalınlığı, hücre şekli vb.) modele girdi olarak verilebilir.
- **Karar Sınırı (*Decision Boundary*):** Algoritma, girdilerin oluşturduğu uzayda sınıfları birbirinden ayıran en uygun sınır çizgisini/eğrisini öğrenir.
- **Gelecek Konu:** Makine Öğreniminin ikinci ana dalı olan **Gözetimsiz Öğrenme (*Unsupervised Learning*)**.




# Gözetimsiz Öğrenme (Unsupervised Learning) & Kümeleme (Clustering)

- **Temel Mantık:** Veri setinde hedef çıktı / doğru cevap ($y$ etiketi) bulunmaz; modele yalnızca girdi verileri ($x$) verilir. Algoritma, insan müdahalesi veya önceden tanımlanmış etiketler olmadan verideki gizli desenleri, yapıları, benzerlikleri ve farklılıkları kendi kendine keşfeder.
- **Gözetimli vs. Gözetimsiz:**
  - **Gözetimli:** "Bu $x$ girdisinin doğru cevabı $y$'dir, kuralı öğren."
  - **Gözetimsiz:** "Elimizde sadece $x$ verileri var; aralarındaki ilişkiyi ve grupları kendin bul."
- **Kümeleme (Clustering):** Etiketlenmemiş verileri benzerlik özelliklerine göre otomatik olarak alt gruplara (kümelere) ayıran en yaygın gözetimsiz öğrenme türüdür.
- **Kullanım Örnekleri:**
  - **Haber Gruplandırma (Google News):** Her gün binlerce haber metnini tarayarak ortak kelimeler ve bağlamlara göre aynı konudaki haberleri otomatik tek başlık altında toplama.
  - **Genetik / DNA Analizi:** İnsanların gen ekspresyon verilerini inceleyerek önceden tanımlanmamış biyolojik alt tipleri ve genetik benzerlik gruplarını keşfetme.
  - **Pazar Bölümleme (Market Segmentation):** Müşteri veya kullanıcı veritabanını ilgi alanlarına, hedeflerine veya davranışlarına göre otomatik segmentlere ayırma.
- **Gelecek Konu:** Kümeleme dışındaki diğer **gözetimsiz öğrenme yöntemleri**.


# Gözetimsiz Öğrenme Türleri & Karşılaştırma

- **Temel Tanım:** Algoritmaya hedef çıktı ($y$ etiketleri) verilmez; yalnızca girdi verisi ($x$) sunulur. Algoritma veri içerisindeki gizli yapıyı, örüntüleri veya sıradışı durumları keşfeder.
- **Temel Gözetimsiz Öğrenme Türleri:**
  - **Kümeleme (*Clustering*):** Benzer veri noktalarını otomatik olarak alt gruplara ayırır (Örn: Benzer haberlerin gruplanması, müşteri pazar bölümlemesi).
  - **Anomali Tespiti (*Anomaly Detection*):** Normal dağılıma uymayan olağandışı verileri tespit eder (Örn: Finansal işlemlerde sahtekarlık/dolandırıcılık tespiti).
  - **Boyut İndirgeme (*Dimensionality Reduction*):** Çok değişkenli/büyük veri setlerini, bilgi kaybını minimum tutarak daha az boyutlu (daha sıkıştırılmış) bir forma dönüştürür.

---

### Gözetimli vs. Gözetimsiz Öğrenme Karşılaştırma Örnekleri

| Problem Örneği | Öğrenme Türü | Neden? |
| :--- | :--- | :--- |
| **Spam Filtreleme** | **Gözetimli** (*Supervised*) | E-postalar önceden "spam" / "spam değil" şeklinde etiketlenmiştir ($x \rightarrow y$). |
| **Haber Gruplandırma** | **Gözetimsiz** (*Unsupervised*) | Etiket olmadan, haber metinleri benzerliklerine göre kümelenir. |
| **Pazar Bölümleme** | **Gözetimsiz** (*Unsupervised*) | Müşteri segmentleri önceden tanımlanmamıştır; algoritma benzer kullanıcıları gruplar. |
| **Diyabet Teşhisi** | **Gözetimli** (*Supervised*) | Hastanın diyabetli olup olmadığı önceden etiketlenmiş bir sınıflandırma problemidir. |

---

- **Gelecek Konu:** Makine Öğreniminde Uygulama Ortamı: **Jupyter Notebook Kullanımı**.
