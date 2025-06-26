---
title: Praktikum 1 - Pengenalan R dan Statistika Deskriptif
author: Gibekkk
date: 2025-03-02 22:41:00 +0800
categories: [Praktikum, R]
tags: [r programming, instalasi, statistika deskriptif]
image:
  path: /assets/img/R_logo.png
  alt: R Programming
---

# Praktikum 1: Pengenalan R dan Statistika Deskriptif

Pada praktikum ini, kita akan belajar dasar-dasar R untuk analisis statistika deskriptif.

## Bagian 1: Instalasi R

### 1.1 Mengunduh dan Menginstal R

1. Kunjungi situs [CRAN R](https://cran.r-project.org/).
2. Pilih sistem operasi Anda: Windows, macOS, atau Linux.
3. Unduh dan instal versi terbaru.

### 1.2 Mengunduh dan Menginstal RStudio

1. Kunjungi [Posit RStudio](https://posit.co/download/rstudio-desktop/).
2. Unduh versi RStudio Desktop (gratis).
3. Instal dan jalankan RStudio.

## Bagian 2: Dasar-Dasar R

### 2.1 Menjalankan R

- Jika menggunakan R GUI, buka aplikasi R.
- Jika menggunakan RStudio, buka aplikasi RStudio dan gunakan Console atau Script Editor.

### 2.2 Operasi Dasar di R

```r
# Aritmatika dasar
5 + 3
10 - 4
3 * 5
15 / 3
2^4  # pangkat

# Membuat variabel
x <- 10
y <- 5
x + y

# Membuat vektor
angka <- c(10, 15, 20, 25, 30)
names <- c("Andi", "Budi", "Cindy", "Doni")

# Operasi pada vektor
mean(angka)
sum(angka)
length(angka)
```

### 2.3 Import Data

R dapat membaca berbagai format data seperti CSV dan Excel.

```r
# Membaca file CSV
data <- read.csv("nutrient.csv")

# Melihat struktur data
str(data)

# Melihat beberapa baris pertama
head(data)

# Ringkasan data
summary(data)
```

## Bagian 3: Statistika Deskriptif dengan R

### 3.1 Ukuran Pemusatan

```r
# Mean
mean(data$kolom1)

# Median
median(data$kolom1)

# Modus (tidak ada fungsi bawaan)
find_mode <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}

find_mode(data$kolom1)
```

### 3.2 Ukuran Penyebaran

```r
# Range
range(data$kolom1)
diff(range(data$kolom1))

# Varians
var(data$kolom1)

# Standar deviasi
sd(data$kolom1)

# Kuartil
quantile(data$kolom1)

# Rentang interkuartil (IQR)
IQR(data$kolom1)
```

### 3.3 Visualisasi Data

```r
# Histogram
hist(data$kolom1, 
     main="Histogram",
     xlab="Nilai", 
     col="skyblue",
     border="white")

# Boxplot
boxplot(data$kolom1, 
        main="Boxplot",
        ylab="Nilai", 
        col="lightgreen")

# Scatter plot
plot(data$kolom1, data$kolom2,
     main="Scatter Plot",
     xlab="Kolom 1", 
     ylab="Kolom 2",
     pch=19, 
     col="darkblue")

# Bar plot untuk data kategorikal
barplot(table(data$kolom_kategori),
        main="Bar Plot",
        xlab="Kategori", 
        ylab="Frekuensi",
        col="coral")
```

## Latihan

1. Download file `nutrient.csv`
2. Buka vscode / Rstudio
3. Masukkan kode berikut

```r
# Operasi dasar R
2 + 3
5 * 4
sqrt(25)

# Membuat dan menggunakan variabel
x <- 10 
y <- x + 5
print(y)

# Bekerja dengan vektor
data_vektor <- c(5, 10, 15, 20)
mean(data_vektor)

# Import dataset
data <- read.csv("nutrient.csv") 
head(data)
summary(data)

# Analisis statistik deskriptif

# 1. Ukuran Pemusatan untuk setiap kolom numerik
# Pilih kolom yang ingin dianalisis (ganti "kolom1" sesuai nama kolom di dataset)
kolom_numerik <- "kolom1"

# Mean
mean_nilai <- mean(data[[kolom_numerik]])
cat("Mean:", mean_nilai, "\n")

# Median
median_nilai <- median(data[[kolom_numerik]])
cat("Median:", median_nilai, "\n")

# Modus (menggunakan fungsi yang telah didefinisikan di tutorial)
find_mode <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}
modus_nilai <- find_mode(data[[kolom_numerik]])
cat("Modus:", modus_nilai, "\n")

# 2. Ukuran Penyebaran
# Range
range_nilai <- diff(range(data[[kolom_numerik]]))
cat("Range:", range_nilai, "\n")

# Varians
var_nilai <- var(data[[kolom_numerik]])
cat("Varians:", var_nilai, "\n")

# Standar deviasi
sd_nilai <- sd(data[[kolom_numerik]])
cat("Standar Deviasi:", sd_nilai, "\n")

# Kuartil
kuartil <- quantile(data[[kolom_numerik]])
print(kuartil)

# Rentang interkuartil (IQR)
iqr_nilai <- IQR(data[[kolom_numerik]])
cat("IQR:", iqr_nilai, "\n")

# 3. Visualisasi Data
# Histogram
hist(data[[kolom_numerik]], 
     main="Histogram",
     xlab="Nilai", 
     col="skyblue",
     border="white")

# Boxplot
boxplot(data[[kolom_numerik]], 
        main="Boxplot",
        ylab="Nilai", 
        col="lightgreen")

# Scatter plot (jika ada dua variabel yang ingin dibandingkan)
# Ganti "kolom2" dengan nama kolom kedua
plot(data[[kolom_numerik]], data[["kolom2"]],
     main="Scatter Plot",
     xlab="Kolom 1", 
     ylab="Kolom 2",
     pch=19, 
     col="darkblue")

# Bar plot untuk data kategorikal (jika ada)
# Ganti "kolom_kategori" dengan nama kolom kategorikal
if("kolom_kategori" %in% names(data)) {
  barplot(table(data[["kolom_kategori"]]),
          main="Bar Plot",
          xlab="Kategori", 
          ylab="Frekuensi",
          col="coral")
}
```

4. Modifikasi kode di atas dengan mengganti nama kolom sesuai dengan kolom yang ada di dataset `nutrient.csv`
5. Bandingkan hasil perhitungan menggunakan fungsi bawaan R dengan perhitungan manual
6. Buatlah laporan singkat yang menjelaskan hasil analisis statistik deskriptif dari dataset `nutrient.csv`

## Referensi

- R Core Team (2023). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria.https://www.R-project.org/.
- Wickham, H. (2016). ggplot2: Elegant Graphics for Data Analysis. Springer-Verlag New York.
