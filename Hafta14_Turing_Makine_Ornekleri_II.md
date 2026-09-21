# Hafta 14: Turing Makine Örnekleri II

## 1. Giriş
Bu son haftada, daha ileri düzey Turing makinesi örneklerini, karar verilebilirlik (decidability) kavramını ve Turing makinelerinin sınırlarını inceliyoruz.

## 2. Örnekler

**Örnek 1 — aⁿbⁿcⁿ dilini tanıyan TM (detaylı):**
Her turda bir 'a', bir 'b', bir 'c' işaretlenir (X, Y, Z sembolleriyle). Eşit sayıda değilse reddedilir.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q1: a/X,R
    q1 --> q1: a/a,R
    q1 --> q1: Y/Y,R
    q1 --> q2: b/Y,R
    q2 --> q2: b/b,R
    q2 --> q2: Z/Z,R
    q2 --> q3: c/Z,L
    q3 --> q3: a,b,c,Y,Z/aynı,L
    q3 --> q0: X/X,R
    q0 --> qf: Y/Y,R
    qf --> [*]
```

**Örnek 2 — Çarpma yapan TM (unary çarpım, m×n):**
1ᵐ#1ⁿ girdisi verilir; TM, n'i m kez kopyalayarak 1^(m×n) sonucunu üretir.

```mermaid
graph TD
    A[m tane 1 var] --> B[Her biri icin n tane 1 kopyala]
    B --> C[Sonuc: m x n tane 1]
```

**Örnek 3 — Asal sayı testi yapan TM (unary sayı üzerinde):**
1ⁿ girdisi verilir. TM, n'nin 2'den n-1'e kadar herhangi bir sayıya bölünüp bölünmediğini (tekrarlı çıkarma ile) kontrol eder.

```mermaid
graph TD
    A[n girildi] --> B[k=2 dene]
    B --> C{n, k'ye tam bolunuyor mu?}
    C -->|Evet ve k noteq n| D[ASAL DEGIL - Red]
    C -->|Hayir| E[k=k+1]
    E --> F{k < n?}
    F -->|Evet| B
    F -->|Hayir| G[ASAL - Kabul]
```

**Örnek 4 — Evrensel Turing Makinesi (UTM) simülasyonu:**
UTM, bir TM'nin kodlanmış tanımını ve girdisini alır, o TM'yi simüle eder. Bu, "her algoritma bir TM ile ifade edilebilir" fikrinin (Church-Turing Tezi) temelidir.

```mermaid
graph LR
    Kod["<M> - Kodlanmış TM Tanımı"] --> UTM[Evrensel TM]
    Girdi[w - Girdi] --> UTM
    UTM --> Sonuc["M'nin w üzerindeki çalışması simüle edilir"]
```

**Örnek 5 — Durma Problemi (Halting Problem) — Karar Verilemezlik:**
"Bir TM'nin belirli bir girdide durup durmayacağını genel olarak belirleyen bir algoritma yoktur." Bu, Turing tarafından çelişki (diagonalization) yöntemiyle ispatlanmıştır.

```mermaid
graph TD
    A["Varsayim: H TM'si var, M ve w icin durur mu karar verir"] --> B["D adında yeni bir TM tanımla: D, H'yi kendi kodu üzerinde çalıştırır"]
    B --> C["D kendisi için çelişki üretir"]
    C --> D["Cakisma: Boyle bir H var olamaz"]
```

## 3. Karar Verilebilir vs Tanınabilir Diller

| Sınıf | Tanım |
|---|---|
| **Karar verilebilir (Decidable)** | Her girdide TM durur ve doğru cevap verir |
| **Tanınabilir (Recognizable/RE)** | Kabul edilen girdilerde durur, reddedilenlerde durmayabilir |
| **Karar verilemez (Undecidable)** | Durma Problemi gibi, hiçbir TM her zaman doğru cevap veremez |

```mermaid
graph TD
    A[Tum Diller] --> B[Turing Tanınabilir - RE]
    B --> C[Karar Verilebilir - Decidable]
    A --> D[Karar Verilemez - Undecidable]
```

## 4. Alıştırma Soruları
1. Örnek 1'deki TM'nin "aabbcc" girdisini kabul ettiğini adım adım gösteriniz.
2. Örnek 3'teki asal sayı testi TM'sinin n=6 için neden reddettiğini açıklayınız.
3. Durma Probleminin neden karar verilemez olduğunu kendi cümlelerinizle özetleyiniz.
4. Karar verilebilir ve tanınabilir dil sınıfları arasındaki farkı bir örnekle açıklayınız.
