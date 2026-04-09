---
title: "Kuantum Makine Öğrenmesinde Problem Tipolojisi: Veri Türü × Çıktı Türüne Göre Sınıflandırma"
---

<div class="language-switcher">
  <span class="language-switcher-label">Language:</span>
  <a class="active" href="bolum_0_tr">Türkçe</a>
  <a class="" href="bolum_0_en">English</a>
</div>



Kuantum makine öğrenmesini (QML) sistematik biçimde anlatmanın en net
yollarından biri, girdinin (verinin) hangi dünyadan geldiği ve çıktının
hangi dünyaya ait olduğu üzerinden bir tipoloji kurmaktır. Burada iki
temel eksen vardır:

1.  **Girdi (veri) Turu**

    -   **CC (Classical-Classical Veri** : Klasik bir bilgisayarda
        temsil edilen veri (vektör, görüntü, tablo, zaman serisi).

    -   **QQ (Quantum-Quantum Veri)** : Kuantum durumları veya kuantum
        kanallarıyla temsil edilen veri. Laboratuvarda üretilmiş kuantum
        durumları, çok-kübitli yoğunluk matrisleri, bir kuantum
        devresinin ürettiği durumlar gibi.

2.  **Cikti Turu**

    -   **QC (Quantum $\rightarrow$ Classical çıktı)**: Kuantum
        hesaplama yürür, fakat nihai ürün klasik bir sayı/etiket olur
        (ölçüm ve klasik işlem sonrası ile). Sınıflama etiketi,
        regresyon değeri, olasılık gibi.

    -   **QQ (Quantum $\rightarrow$ Quantum çıktı):** Nihai ürün bir
        kuantum durumu yada kanalıdır. Yani "çıktı" başka bir kuantum
        algoritmasına girdi olacak şekilde kuantum olarak kalır.

Bu iki ekseni birleştirince 4 temel problem sınıfı elde edilir:
$CC \rightarrow QC,\; CC \rightarrow QQ,\; QQ \rightarrow QC,\; QQ \rightarrow QQ$.
Aşağıda bu her bir sinifi bilimsel ama anlaşılır biçimde tartisacagiz.

#### CC $\rightarrow$ QC: Klasik Veriden Kuantum Hesaplamak / Klasik Tahmin Uretmek

Bu sınıf, günümüzde pratik Quantum Makine Ogrenmesi (QML) literatürünün
en yaygın bölümüdür: *Veriler klasik olarak gelir, kuantum devre içinde
işlenir ve sonunda ölçümle klasik bir çıktı elde edilir.*

Bu surecte ki tipik akis su sekildedir :

1.  **Klasik veri kodlama (encoding / feature map):**

    -   $x \in \mathbb{R}^d$ gibi bir girdi, parametreleri $x$'e bağlı
        bir kuantum devresiyle bir kuantum duruma gömülür:
        $$x \mapsto \lvert \phi(x) \rangle = U_{\phi}(x)\, \lvert 0 \rangle .$$

2.  **Kuantum işlem (ansatz / çekirdek / evrim):**

    -   Bu durum üzerinde bir devre daha uygulanır (örneğin parametrik
        bir ansatz).

3.  **Ölçüm ve klasik okuma (readout):**

    -   Gözlenenler (Pauli beklentileri, olasılıklar) klasik sayılara
        çevrilir:
        $$y = f\big( \langle O \rangle_{\lvert \psi(x) \rangle} \big).$$

4.  **Öğrenme:**

    -   Klasik kayıp fonksiyonu minimize edilir (cross-entropy, MSE
        vb.).

Bu sinif kapsaminda asagidaki problemler tanimlanabilir.

-   **Sınıflama:** Kuantum devre ölçümünden sınıf olasılıkları veya
    etiket çıkarımı.

-   **Regresyon:** Beklenti değerlerinden sürekli çıktı tahmini.

-   **Temsil öğrenme (representations):** Kuantum özellik haritasının
    ürettiği ölçümler bir "özellik vektörü" gibi kullanılır.

-   **Fizik/kimya hedefleri:** Klasik girdilerden (molekül
    tanımlayıcıları vb.) enerji/özellik tahmini; çıktı çoğunlukla klasik
    sayıdır.

Burada bilinmesi gereken bilimsel olarak kritik bir nokta var. O da bu
modelin basarisinin degerlendirilmesi icin bazi yeni kriterlerin
oldugudur. Bu kriterler asagidaki gibi ifade edilir:

1.  Seçilen encoding'in ifade gücü,

2.  Ölçüm istatistiğinin örnekleme maliyeti (shot noise),

3.  Optimizasyon zorluğu (barren plateaus, gürültü).

#### CC $\rightarrow$ QQ: Klasik Veriden Kuantum Durum Uretmek  Kuantum Cikti Uretmek

Bu sınıfta veri klasik gelir; ama amaç bir kuantum durumu üretmektir.
Yani modelin çıktısı bir etiket ya da sayı değil, doğrudan bir kuantum
objesidir:

$$x \mapsto \rho(x) \quad \text{veya} \quad x \mapsto \lvert \psi(x) \rangle .$$

Bu durum iki ana motivasyonla ortaya çıkar:

1.  **Kuantum veri üretimi / kuantum generatif modelleme**

    -   Amaç, bir dağılımı "kuantum durum" olarak temsil etmek veya
        belirli bir kuantum durum ailesini öğrenmektir.Örnek:
        Parametreleri klasik veriden türetilen bir devre, o veriye
        karşılık gelen kuantum durumunu hazırlar.

2.  **Kuantum algoritmalarına girdi hazırlama (state preparation)**

    -   Bazı kuantum algoritmaları (simülasyon, HHL benzeri lineer cebir
        rutinleri, amplitude encoding) doğrudan bir kuantum durum
        ister.Bu nedenle öğrenme problemi, klasik veriyi belirli bir
        doğrulukla kuantum duruma kodlayacak devreyi bulmaya
        dönüşebilir.

Bu sinif kapsaminda asagidaki problemler tanimlanabilir.

-   Generatif modelleme (kuantum durum üretimi).

-   Temsil öğrenme: Klasik veriyi kuantum uzayda daha uygun bir temsile
    dönüştürmek; çıktı kuantum kaldığı için başka kuantum modüllerle
    zincirlenebilir.

Burada bilinmesi gereken bilimsel olarak kritik bir nokta var. O da bu
modelin basarisinin degerlendirilmesi icin bazi yeni kriterlerin
oldugudur. Dogrudan **Dogruluk** yerine asagidaki kriterler kullanilir :

-   Fidelity,

-   Trace distance,

-   Observable matching,

-   Kernel alignment.

#### QQ $\rightarrow$ QC: Kuantum Veriden Klasik Karar/Sayı Cıkar (ölç, sınıflandır, tahmin et)

Bu sınıfta girdi kuantumdur: Elinizde bir kuantum durum ailesi (veya
kuantum kanal) vardır. Burada ki amaç, bundan klasik bir bilgi
çıkarmaktır. En doğal örnek: kuantum durum ayrımıdir. Burada ki genel
form matematiksel olarak soyle ifade edilir :

$$\rho \;\mapsto\; y \in \mathbb{R}
\quad \text{veya} \quad
\rho \;\mapsto\; y \in \{1,\dots,K\}.$$

Burada su soru sorulabilir : **Bu neden ayrı bir sınıf?** Çünkü burada
"veri yükleme" problemi yoktur; veri zaten kuantum cihazda veya kuantum
bellekte bulunur. Modelin görevi, bu durumdan uygun ölçüm
stratejileriyle bilgi çıkarmaktır. Bu anlamda tipik uygulamalar soyledir
:

-   **Sınıflama:** Hangi sınıfa ait kuantum durum? (state
    discrimination)

-   **Regresyon / parametre kestirimi:** Kuantum sensör verisinden bir
    fiziksel parametre tahmini.

-   **Faz tanıma (quantum phase recognition):** Kuantum çok-cisim
    sistemlerinden klasik faz etiketi çıkarımı.

-   **Deneysel gürültü tanılama:** Kuantum cihaz çıktılarından
    hata/gürültü parametrelerinin öğrenilmesi.

Bu model kapsaminda ki bilimsel kritik nokta biraz daha detaylidir.
Burada sınırlayıcı unsur, yalnızca "model kapasitesi" değil, aynı
zamanda ölçüm tasarımıdır. Kuantum veri ölçümle klasikleştirilirken
bilgi kaybı oluşabilir. Bu nedenle şu kavramlar önem kazanır:

-   POVM tasarımı,

-   Adaptif ölçümler,

-   Örnekleme maliyeti,

-   İstatistiksel sınırlar (örneğin Helstrom bound).

#### QQ $\rightarrow$ QQ: QQ→QQ: Kuantum Veriyi Kuantum Biçimde Dönüştür

Bu sınıfta hem girdi hem çıktı kuantumdur:

$$\rho_{\text{in}} \;\mapsto\; \rho_{\text{out}}.$$

Bu, "öğrenen bir kuantum kanal" veya "öğrenen bir kuantum devre
dönüşümü" olarak düşünülebilir.

Burada su soru sorulabilir :**Neden önemli?** Çünkü burada QML, klasik
etiket tahmini yerine doğrudan kuantum bilgi işleme görevlerinin içine
yerleşir: sıkıştırma, hata düzeltme, entanglement yapılandırma, durum
dönüştürme, kanal öğrenme gibi işlemler bu çerçevede ele alınır.

Bu kapsamda uygulanan tipik uygulamalar soyledir :

-   **Temsil öğrenme / sıkıştırma:** Kuantum autoencoder'lar; gereksiz
    altuzayı atıp bilgi taşıyan altuzayı korumayı hedefler.

-   **Hata azaltma / hata düzeltmeye yardımcı öğrenme:** Gürültü
    etkilerini telafi eden öğrenilmiş kuantum dönüşümleri.

-   **Kuantum devre derleme (compilation) / optimizasyon:** Hedef
    birimere yakın bir devreyi öğrenmek.

-   **Fizik/kimya simülasyonu:** Kuantum sistemin evrimini yaklaşık
    olarak gerçekleştiren öğrenilmiş kanallar.

Burada bilinmesi gereken bilimsel kritik nokta bu QQ $\rightarrow$ QQ
modellerinde amaç fonksiyonları klasik kayıplardan farklıdır; fidelity,
kanal mesafeleri, gözlenebilir uyumu gibi kuantum-özgü hedefler gerekir.
Ayrıca doğrulama (verification) maliyeti yüksek olabilir; çünkü kuantum
çıktıyı karakterize etmek çoğu zaman tam tomografi gerektirir ve bu da
ölçeklenme sorunlarına yol açar.

#### Uygulama Siniflari Bu Tipolojiye Nasil Oturur?

Şimdi verecegimiz uygulama sınıflarını (sınıflama, regresyon, generatif
modelleme, temsil öğrenme, fizik/kimya hedefleri) bu 4 tipolojiyle
ilişkilendirelim. Buradaki ana fikir şudur: uygulama etiketi, "ne yapmak
istiyoruz?" sorusudur; CC/QC/QQ ayrımı ise "neyle başlıyor ve ne
üretiyoruz?" sorusudur. Aynı uygulama, farklı veri/çıktı tiplerinde
görülebilir.

1.  **Sınıflama**

    -   CC$\rightarrow$QC: En yaygın; klasik veri, kuantum devre,
        ölçümden sınıf etiketi.

    -   QQ$\rightarrow$QC: Kuantum durum sınıflama (state
        discrimination, faz tanıma).

2.  **Regresyon**

    -   CC$\rightarrow$QC: Beklenti değerlerinden sürekli tahmin.

    -   QQ$\rightarrow$QC: Kuantum sensör okumasından parametre
        kestirimi.

3.  **Generatif modelleme**

    -   CC$\rightarrow$QQ: Klasik koşullama ile kuantum durum üretimi
        (quantum conditional generation).

    -   QQ$\rightarrow$QQ: Kuantum dağılımları dönüştüren/üreten kuantum
        kanallar; ör. bir kuantum kaynaktan gelen durumları hedef
        dağılıma eşleyen dönüşümler.

4.  **Temsil öğrenme**

    -   CC$\rightarrow$QC: Kuantum ölçümlerini özellik olarak kullanıp
        klasik uzayda temsil öğrenme.

    -   CC$\rightarrow$QQ: Temsil kuantum uzayında kalır; sonraki
        kuantum modüllere aktarılır.

    -   QQ$\rightarrow$QQ: Kuantum autoencoder'lar gibi doğrudan kuantum
        temsillerin öğrenilmesi.

5.  **Fizik/kimya hedefleri**

    Bu alan, dört sınıfın hepsine dağılabilir:

    -   CC$\rightarrow$QC: Molekül tanımlayıcılarından enerji/özellik
        tahmini.

    -   CC$\rightarrow$QQ: Klasik parametrelerden hedef kuantum durumu
        hazırlama.

    -   QQ$\rightarrow$QC: Deneysel kuantum sistemlerden faz/parametre
        çıkarımı.

    -   QQ$\rightarrow$QQ: Simülasyon/evrim operatörünün öğrenilmesi,
        hata azaltma ile fiziksel doğruluğu artırma.

Bunlari bilmek onemlidir cunku bu siniflandirmalar sadece terminoloji
degildir, hangi tur maliyetle karsilasacagimizi da onceden soyler.
Ornegin :

-   CC$\rightarrow$QC: Darboğaz genellikle encoding seçimi, shot
    maliyeti ve optimizasyondur.

-   CC$\rightarrow$QQ: Darboğaz, çıktı değerlendirmesi (fidelity vb.) ve
    state preparation karmaşıklığıdır.

-   QQ$\rightarrow$QC: Darboğaz, ölçüm tasarımı ve bilgi çıkarımı
    sınırlarıdır.

-   QQ$\rightarrow$QQ: Darboğaz, doğrulama (verification) maliyeti,
    kanal/durum metrikleri ve ölçeklenebilir eğitimdir.

Bu nedenle bir QML projesi tasarlarken "hangi sınıftayım?" sorusu; deney
tasarımı, kaynak bütçesi (shots, qubit sayısı), doğrulama protokolü ve
yayınlanabilir metodoloji açısından belirleyicidir.