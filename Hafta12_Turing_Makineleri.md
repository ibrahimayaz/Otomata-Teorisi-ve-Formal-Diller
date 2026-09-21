# Hafta 12: Turing Makineleri (TM)

## 1. Giriş
Turing Makinesi (TM), en genel hesaplama modelidir. Sınırsız uzunlukta bir bant, bant üzerinde hareket eden bir kafa (head) ve okuma/yazma yeteneği içerir.

## 2. Formal Tanım
M = (Q, Σ, Γ, δ, q0, B, F)
- Q: durumlar
- Σ: girdi alfabesi
- Γ: bant alfabesi (Σ ⊆ Γ)
- δ: geçiş fonksiyonu (Q×Γ → Q×Γ×{L,R})
- q0: başlangıç durumu
- B: boşluk sembolü (blank)
- F: kabul durumları

```mermaid
graph LR
    B1[... B] --- B2[a] --- B3[b] --- B4[a] --- B5[B ...]
    B3 -.kafa.-> Kontrol[Kontrol Birimi - Durum q]
```

## 3. Örnekler

**Örnek 1 — aⁿbⁿ dilini tanıyan TM:**
Strateji: her adımda bir 'a' işaretlenir (X ile), karşılık gelen bir 'b' işaretlenir (Y ile); tüm semboller eşleşince kabul.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q1: a/X,R
    q1 --> q1: a/a,R
    q1 --> q1: Y/Y,R
    q1 --> q2: b/Y,L
    q2 --> q2: a/a,L
    q2 --> q2: Y/Y,L
    q2 --> q0: X/X,R
    q0 --> qf: Y/Y,R
    qf --> [*]
```

**Örnek 2 — İkili sayıyı 1 artıran TM:**
Bant üzerinde sağdan sola giderek, ilk 0'ı 1 yapan, geçtiği 1'leri 0'a çeviren basit bir toplama makinesi.

**Örnek 3 — Palindrom kontrolü yapan TM:**
İlk ve son sembol karşılaştırılır, eşleşirse işaretlenir, kafa içe doğru hareket eder; tüm semboller eşleşirse kabul.

```mermaid
graph TD
    S1[Ilk ve son sembolu karsilastir] --> S2{Esit mi?}
    S2 -->|Evet| S3[Isaretle, ice dogru hareket et]
    S2 -->|Hayir| S4[Reddet]
    S3 --> S5{Bant ortalandi mi?}
    S5 -->|Hayir| S1
    S5 -->|Evet| S6[Kabul]
```

**Örnek 4 — aⁿbⁿcⁿ dilini tanıyan TM:**
Her tur bir a, bir b, bir c işaretlenir; üç sembol de eşit sayıda işaretlenirse kabul edilir (PDA'nın yapamadığı bir işlem, TM'nin yapabildiğini gösterir).

**Örnek 5 — İkili sayının kopyasını (w#w) üreten/kontrol eden TM:**
'#' işaretini bulur, sol ve sağ kısmı sembol sembol karşılaştırır.

## 4. Turing Makinesinin Çalışma Şeması

```mermaid
graph TD
    A[Baslangic Durumu] --> B[Sembol Oku]
    B --> C{Gecis Fonksiyonu delta}
    C --> D[Yeni Sembol Yaz]
    D --> E[Kafayi L/R hareket ettir]
    E --> F[Yeni Duruma Gec]
    F --> B
    F --> G[Kabul/Red]
```

## 5. TM Türleri
- **Deterministik TM (DTM)**
- **Non-deterministik TM (NTM)** — DTM'ye eşdeğer güçtedir
- **Çok bantlı TM** — tek bantlı TM'ye eşdeğer güçtedir
- **Evrensel Turing Makinesi (UTM)** — her TM'yi simüle edebilen TM

## 6. Alıştırma Soruları
1. Örnek 1'deki TM'nin "aabb" girdisini adım adım işleyerek kabul ettiğini gösteriniz.
2. Bir sayıyı ikiye katlayan (örn: bant üzerindeki 1'lerin sayısını ikiye katlayan) bir TM tasarlayınız.
3. Çok bantlı TM'nin neden tek bantlı TM'ye eşdeğer olduğunu kısaca açıklayınız.
4. Evrensel Turing Makinesi kavramının modern bilgisayarlarla ilişkisini tartışınız.
