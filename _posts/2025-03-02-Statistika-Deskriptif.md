---
title: Statistika Deskriptif - Ukuran Pemusatan
author: KingPublic
date: 2025-03-02 22:42:00 +0800
categories: [Statistika, Dasar]
tags: [statistika deskriptif, mean, median, modus]
math: true
image:
  path: /assets/img/statistika.jpg
  alt: Statistika Deskriptif
---

# Ukuran Pemusatan Data

Dalam statistika deskriptif, ukuran pemusatan data merupakan nilai yang mewakili kecenderungan pusat dari sekumpulan data. Tiga ukuran pemusatan yang umum digunakan adalah mean (rata-rata), median, dan modus.

## Mean (Rata-rata)

Mean adalah nilai rata-rata aritmatika dari sekumpulan data yang dihitung dengan menjumlahkan semua nilai data kemudian membaginya dengan banyaknya data.

### Rumus Mean

$$ \mu = \frac{1}{N}\sum_{i=1}^{N}x_i $$

atau untuk data sampel:

$$ \bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i $$

### Contoh

Untuk data berikut:
```
18, 23, 20, 21, 24, 23, 20, 20, 15, 19, 24
```

Mean = $\frac{18 + 23 + 20 + 21 + 24 + 23 + 20 + 20 + 15 + 19 + 24}{11} = 20.64$

### Implementasi di R

```r
# Input data
data <- c(18, 23, 20, 21, 24, 23, 20, 20, 15, 19, 24)

# Hitung mean
mean_value <- mean(data)
print(paste("Mean:", mean_value))
```

## Median

Median adalah nilai tengah dari sekumpulan data yang telah diurutkan. Jika banyaknya data ganjil, median adalah nilai yang terletak di tengah. Jika banyaknya data genap, median adalah rata-rata dari dua nilai tengah.

### Contoh

Untuk data yang sama setelah diurutkan:
```
15, 18, 19, 20, 20, 20, 21, 23, 23, 24, 24
```

Median = 20 (nilai tengah)

### Implementasi di R

```r
# Hitung median
median_value <- median(data)
print(paste("Median:", median_value))
```

## Modus

Modus adalah nilai yang paling sering muncul dalam sekumpulan data.

### Contoh

Untuk data yang sama:
```
15, 18, 19, 20, 20, 20, 21, 23, 23, 24, 24
```

Modus = 20 (muncul 3 kali)

### Implementasi di R

R tidak memiliki fungsi bawaan untuk modus, namun kita dapat membuatnya:

```r
# Fungsi untuk menghitung modus
find_mode <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}

# Hitung modus
mode_value <- find_mode(data)
print(paste("Modus:", mode_value))
```

## Kapan Menggunakan Masing-masing Ukuran?

- **Mean**: Cocok untuk data numerik dengan distribusi yang simetris tanpa outlier.
- **Median**: Lebih tepat untuk data yang memiliki outlier atau distribusi miring.
- **Modus**: Berguna untuk data kategorikal atau untuk mengetahui nilai yang paling umum.

## Latihan (Mengingat)

1. Hitung mean, median, dan modus untuk data berikut:
   ```
   5, 17, 8, 2, 55, 9, 22, 11, 16, 5
   ```

2. Tentukan ukuran pemusatan yang paling tepat untuk kasus berikut:
   - Harga rumah di Jakarta
   - Metode transportasi yang digunakan mahasiswa
   - Nilai ujian matematika siswa