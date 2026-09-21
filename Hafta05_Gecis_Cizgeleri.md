# Hafta 5: Geçiş Çizgeleri (Transition Graphs)

## 1. Giriş
Geçiş çizgesi (transition graph), bir otomatanın görsel gösterimidir. Durumlar düğüm (node), geçişler ise etiketli ok (edge) olarak gösterilir. NFA'larda kenar etiketleri kelime (string) de olabilir, sadece tek sembol olmak zorunda değildir.

## 2. Geçiş Çizgesi Bileşenleri
- **Düğümler (states):** daireler
- **Kenarlar (transitions):** etiketli oklar
- **Başlangıç durumu:** giriş oku ile gösterilir
- **Kabul durumları:** çift çember ile gösterilir

```mermaid
graph LR
    Start((Başlangıç)) -->|ok| Q0((q0))
    Q0 -->|a| Q1((q1))
    Q1 -->|b| Q2(((q2 - kabul)))
```

## 3. Örnekler

**Örnek 1 — Kelime etiketli geçiş çizgesi (Generalized Transition Graph):**
q0'dan q1'e "ab" etiketiyle doğrudan geçiş:

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q1: ab
    q1 --> [*]
```

**Örnek 2 — Çoklu yol (birden fazla kabul durumu):**
"a" ile başlayan veya "b" ile biten dizeleri kabul eden çizge:

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q1: a
    q0 --> q2: b
    q1 --> q1: a,b
    q2 --> q2: a,b
    q1 --> [*]
    q2 --> [*]
```

**Örnek 3 — Döngü (loop) içeren geçiş çizgesi:**
Aynı durumdan kendine dönen kenar (self-loop):

```mermaid
stateDiagram-v2
    [*] --> q0
    q0 --> q0: a
    q0 --> q1: b
    q1 --> [*]
```

**Örnek 4 — ε-geçişli genelleştirilmiş çizge:**
İki alt otomatanın ε ile birleştirilmesi:

```mermaid
stateDiagram-v2
    [*] --> p0
    p0 --> p1: a
    p1 --> q0: ε
    q0 --> q1: b
    q1 --> [*]
```

**Örnek 5 — Birden fazla başlangıçtan tek kabule giden çizge (NFA görünümü):**

```mermaid
stateDiagram-v2
    [*] --> s1
    [*] --> s2
    s1 --> f: a
    s2 --> f: b
    f --> [*]
```

## 4. Geçiş Çizgesinden Geçiş Tablosuna Dönüşüm
Örnek 3 için tablo:

| Durum | a | b |
|---|---|---|
| →q0 | q0 | q1 |
| *q1 | - | - |

## 5. Alıştırma Soruları
1. Örnek 2'deki geçiş çizgesinin kabul ettiği dili küme gösterimiyle yazınız.
2. "aab" veya "bba" kelimelerini kabul eden bir genelleştirilmiş geçiş çizgesi çiziniz.
3. Bir geçiş çizgesini geçiş tablosuna dönüştürme adımlarını açıklayınız.
4. ε-geçişlerin geçiş çizgelerinde neden kullanışlı olduğunu tartışınız.
