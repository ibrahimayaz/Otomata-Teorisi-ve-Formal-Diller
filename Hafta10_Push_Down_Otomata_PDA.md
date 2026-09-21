# Hafta 10: Push Down Otomata (PDA)

## 1. Giriş
Push Down Otomata (PDA), sonlu otomataya ek olarak bir **yığın (stack)** belleği içeren hesaplama modelidir. Bağlamdan bağımsız dilleri (CFL) tanıyabilir.

## 2. Formal Tanım
M = (Q, Σ, Γ, δ, q0, Z0, F)
- Q: durumlar
- Σ: girdi alfabesi
- Γ: yığın alfabesi
- δ: geçiş fonksiyonu (Q×Σ∪{ε}×Γ → Q×Γ*)
- q0: başlangıç durumu
- Z0: yığının başlangıç sembolü
- F: kabul durumları

```mermaid
graph TD
    A[Girdi Seridi] --> B[PDA Kontrol Birimi]
    C[Yigin - Stack] <--> B
    B --> D{Kabul mu?}
```

## 3. Örnekler

**Örnek 1 — aⁿbⁿ dilini kabul eden PDA:**
Her 'a' için yığına push, her 'b' için pop yapılır; yığın boşalınca kabul.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q0: a, Z0/AZ0
    q0 --> q0: a, A/AA
    q0 --> q1: b, A/ε
    q1 --> q1: b, A/ε
    q1 --> q2: ε, Z0/Z0
    q2 --> [*]
```

**Örnek 2 — Dengeli parantez PDA:**
'(' için push, ')' için pop işlemi yapılır.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q0: "(" , Z0/XZ0
    q0 --> q0: "(" , X/XX
    q0 --> q0: ")" , X/ε
    q0 --> q0: ε, Z0/Z0
```

**Örnek 3 — Palindrom (ortası bilinen, wcwᴿ) kabul eden PDA:**
İlk yarıda push, 'c' ortasında geçiş, ikinci yarıda pop yapılarak eşleşme kontrol edilir.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q0: a, Z0/AZ0
    q0 --> q0: b, Z0/BZ0
    q0 --> q1: c, Z0/Z0
    q1 --> q1: a, A/ε
    q1 --> q1: b, B/ε
    q1 --> q2: ε, Z0/Z0
    q2 --> [*]
```

**Örnek 4 — Eşit sayıda a ve b içeren dizeleri kabul eden PDA:**
Yığında sayaç mantığıyla fazlalık a veya b tutulur; sonunda yığın Z0'a dönmelidir.

**Örnek 5 — {aⁿb²ⁿ | n≥0} dilini kabul eden PDA:**
Her 'a' için 2 sembol push edilir, her 'b' için 1 sembol pop edilir.

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q0: a, Z0/AAZ0
    q0 --> q0: a, A/AAA
    q0 --> q1: b, A/ε
    q1 --> q1: b, A/ε
    q1 --> q2: ε, Z0/Z0
    q2 --> [*]
```

## 4. Kabul Türleri
- **Boş yığınla kabul (acceptance by empty stack)**
- **Son durumla kabul (acceptance by final state)**

Bu iki yöntem birbirine dönüştürülebilir ve eşdeğerdir.

## 5. PDA ile CFG Arasındaki İlişki
Her CFG için eşdeğer bir PDA, her PDA için eşdeğer bir CFG oluşturulabilir (yapısal eşdeğerlik).

## 6. Alıştırma Soruları
1. {wwᴿ | w ∈ {a,b}*} dilini kabul eden bir PDA tasarlayınız.
2. Örnek 1'deki PDA'nın "aaabbb" girdisini adım adım işleyerek kabul ettiğini gösteriniz.
3. Boş yığınla kabul ile son durumla kabul arasındaki farkı açıklayınız.
4. {aⁿbᵐ | n≠m} dilini kabul eden bir PDA fikri tasarlayınız.
