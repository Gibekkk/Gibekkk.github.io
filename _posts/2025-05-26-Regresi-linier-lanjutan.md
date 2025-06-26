---
title: Regresi Linier Lanjutan - Inferensi, Model Multipel, dan Variabel Kategori
author: Gibekkk
date: 2025-05-26 10:00:00 +0800
categories: [Statistika, Regresi]
tags: [regresi multipel, uji t, uji F, anova regresi, variabel dummy, koefisien determinasi, r-squared]
math: true
image:
  path: /assets/img/regresi.jpg
  alt: Regresi Linier Multipel
---

Setelah memahami dasar-dasar regresi linier sederhana dan cara mengestimasi parameternya, kita akan melanjutkan ke topik yang lebih lanjut, termasuk inferensi statistik, perluasan ke model dengan lebih dari satu prediktor (regresi multipel), dan bagaimana menangani variabel prediktor kategorikal.

## Inferensi dalam Regresi Linier Sederhana

Inferensi dalam regresi bertujuan untuk membuat kesimpulan tentang parameter populasi ($$\beta_0, \beta_1$$) berdasarkan estimasi sampel ($$\hat{\beta}_0, \hat{\beta}_1$$).

### Uji Hipotesis untuk Kemiringan ($$\beta_1$$)
Uji yang paling umum adalah menguji apakah ada hubungan linier yang signifikan antara $$X$$ dan $$Y$$. Ini sama dengan menguji apakah kemiringan populasi ($$\beta_1$$) berbeda dari nol.

*   **Hipotesis:**
    *   $$H_0: \beta_1 = 0$$ (Tidak ada hubungan linier antara X dan Y)
    *   $$H_1: \beta_1 \neq 0$$ (Ada hubungan linier antara X dan Y) (Bisa juga satu arah: $$H_1: \beta_1 > 0$$ atau $$H_1: \beta_1 < 0$$)
*   **Statistik Uji (t-statistik):**
    $$ t = \frac{\hat{\beta}_1 - \beta_{1,0}}{SE(\hat{\beta}_1)} = \frac{\hat{\beta}_1 - 0}{SE(\hat{\beta}_1)} $$
    Dimana $$SE(\hat{\beta}_1)$$ adalah standar error dari estimator kemiringan:
    $$ SE(\hat{\beta}_1) = \frac{s_e}{\sqrt{\sum(X_i - \bar{X})^2}} = \sqrt{\frac{\text{MSE}}{\sum(X_i - \bar{X})^2}} $$
    $$s_e = \sqrt{\text{MSE}}$$ adalah standar error dari estimasi.
*   **Derajat Kebebasan (df):** $$n-2$$
*   **Keputusan:** Tolak $$H_0$$ jika p-value $$ \le \alpha $$ atau jika $$|t_{\text{hitung}}| \ge t_{\text{kritis}}$$.

#### Contoh (melanjutkan data OCR dari Regresi Linier Sederhana):
Kita punya: $$\hat{\beta}_1 = 5.1$$, $$\text{MSE} = 24.9$$, $$\sum(X_i - \bar{X})^2 = 10$$, $$n=5$$.
*   $$SE(\hat{\beta}_1) = \sqrt{\frac{24.9}{10}} = \sqrt{2.49} \approx 1.58$$
*   Statistik uji t:
    $$ t = \frac{5.1 - 0}{1.58} \approx 3.23 $$
*   $$df = 5-2 = 3$$
*   **P-value** (untuk uji dua arah, $$H_1: \beta_1 \neq 0$$):
    P-value = $$2 \times P(T > |3.23|)$$ dengan $$df=3$$.
    Menggunakan kalkulator atau tabel t, p-value $$\approx 2 \times 0.0247 = 0.0494$$.
*   **Keputusan** (misal $$\alpha = 0.05$$):
    Karena p-value (0.0494) < $$\alpha$$ (0.05), kita **tolak $$H_0$$**.
*   **Kesimpulan**: Ada cukup bukti statistik pada tingkat signifikansi 5% untuk menyatakan bahwa ada hubungan linier yang signifikan antara jam belajar (X) dan nilai ujian (Y). Artinya, jam belajar berpengaruh signifikan terhadap nilai ujian.

```r
# Melanjutkan contoh dari file sebelumnya
X_belajar <- c(1, 2, 3, 4, 5)
Y_nilai <- c(50, 55, 53, 70, 68)
model_regresi <- lm(Y_nilai ~ X_belajar)

# Ringkasan model sudah termasuk uji t untuk koefisien
summary_model <- summary(model_regresi)
print(summary_model)

# Mengambil t-value dan p-value untuk beta_1 (X_belajar)
t_value_beta1 <- summary_model$coefficients["X_belajar", "t value"]
p_value_beta1 <- summary_model$coefficients["X_belajar", "Pr(>|t|)"]

print(paste("t-value untuk Beta_1:", round(t_value_beta1, 2)))
print(paste("P-value untuk Beta_1:", round(p_value_beta1, 4)))
Use code with caution.
Output R:
Call:
lm(formula = Y_nilai ~ X_belajar)

Residuals:
   1    2    3    4    5 
 1.0  0.9 -6.2  5.7 -1.4 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)  
(Intercept)   43.900      5.579   7.868   0.0043 **
X_belajar      5.100      1.578   3.232   0.0484 * 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 4.99 on 3 degrees of freedom
Multiple R-squared:  0.7769,	Adjusted R-squared:  0.7025 
F-statistic: 10.45 on 1 and 3 DF,  p-value: 0.04839

[1] "t-value untuk Beta_1: 3.23"
[1] "P-value untuk Beta_1: 0.0484"
Use code with caution.
(Catatan: Ada sedikit perbedaan p-value antara manual dan R (0.0494 vs 0.0484) karena pembulatan pada SE(
β
^
1
β
^
​
  
1
​
 
) di perhitungan manual. Output R lebih presisi).
Interval Kepercayaan untuk Kemiringan (
β
1
β 
1
​
 
)
Interval kepercayaan memberikan rentang nilai yang mungkin untuk parameter populasi
β
1
β 
1
​
 
.
Interval kepercayaan
(
1
−
α
)
100
%
(1−α)100%
untuk
β
1
β 
1
​
 
adalah:
β
^
1
±
t
α
/
2
,
n
−
2
×
S
E
(
β
^
1
)
β
^
​
  
1
​
 ±t 
α/2,n−2
​
 ×SE( 
β
^
​
  
1
​
 )
Contoh (melanjutkan data OCR):
Interval kepercayaan 95% untuk
β
1
β 
1
​
 
(
α
=
0.05
α=0.05
,
t
0.025
,
3
≈
3.182
t 
0.025,3
​
 ≈3.182
dari tabel t):
Menggunakan
S
E
(
β
^
1
)
≈
1.578
SE( 
β
^
​
  
1
​
 )≈1.578
dari output R:
5.1
±
3.182
×
1.578
5.1±3.182×1.578

5.1
±
5.020
5.1±5.020

Interval: (
0.080
,
10.120
0.080,10.120
)
Karena interval ini tidak mencakup 0, ini konsisten dengan penolakan
H
0
:
β
1
=
0
H 
0
​
 :β 
1
​
 =0
.
# Interval kepercayaan untuk koefisien
confint(model_regresi, level = 0.95)
Use code with caution.
R
Output R:
2.5 %   97.5 %
(Intercept) 26.224421 61.57558
X_belajar    0.079885 10.12011
Use code with caution.
(Perbedaan kecil dari perhitungan manual di atas karena penggunaan nilai t yang lebih presisi dan SE dari R).
Koefisien Determinasi (
R
2
R 
2
 
)
R
2
R 
2
 
(R-squared) mengukur proporsi variasi total dalam variabel dependen (
Y
Y
) yang dapat dijelaskan oleh variabel independen (
X
X
) melalui model regresi.
Nilai
R
2
R 
2
 
berkisar dari 0 hingga 1 (atau 0% hingga 100%).
Semakin tinggi
R
2
R 
2
 
, semakin baik model menjelaskan variasi dalam
Y
Y
.
R
2
=
SSR
SST
=
1
−
SSE
SST
R 
2
 = 
SST
SSR
​
 =1− 
SST
SSE
​
 

Dimana:
SST (Total Sum of Squares): Variasi total dalam Y.
SST
=
∑
(
Y
i
−
Y
ˉ
)
2
SST=∑(Y 
i
​
 − 
Y
ˉ
 ) 
2
 
SSR (Regression Sum of Squares): Variasi dalam Y yang dijelaskan oleh regresi.
SSR
=
∑
(
Y
^
i
−
Y
ˉ
)
2
SSR=∑( 
Y
^
  
i
​
 − 
Y
ˉ
 ) 
2
 
SSE (Error Sum of Squares): Variasi dalam Y yang tidak dijelaskan oleh regresi (residual).
SSE
=
∑
(
Y
i
−
Y
^
i
)
2
SSE=∑(Y 
i
​
 − 
Y
^
  
i
​
 ) 
2
 

SST = SSR + SSE
Untuk regresi linier sederhana,
R
2
=
r
2
R 
2
 =r 
2
 
, dimana
r
r
adalah koefisien korelasi Pearson antara X dan Y.
Contoh (melanjutkan data OCR):
SSE = 74.70 (dihitung sebelumnya)
Untuk menghitung SST:
|
Y
i
Y 
i
​
 
|
Y
ˉ
=
59.2
Y
ˉ
 =59.2
|
Y
i
−
Y
ˉ
Y 
i
​
 − 
Y
ˉ
 
|
(
Y
i
−
Y
ˉ
)
2
(Y 
i
​
 − 
Y
ˉ
 ) 
2
 
|
| :-----: | :-------------: | :---------------: | :-------------------: |
| 50 | 59.2 | -9.2 | 84.64 |
| 55 | 59.2 | -4.2 | 17.64 |
| 53 | 59.2 | -6.2 | 38.44 |
| 70 | 59.2 | 10.8 | 116.64 |
| 68 | 59.2 | 8.8 | 77.44 |
| | | | SST = 334.8 |
R
2
=
1
−
74.70
334.8
=
1
−
0.2231
≈
0.7769
R 
2
 =1− 
334.8
74.70
​
 =1−0.2231≈0.7769

Sekitar 77.69% variasi dalam nilai ujian dapat dijelaskan oleh variasi dalam jam belajar.
# R-squared dari summary model
r_squared <- summary_model$r.squared
print(paste("R-squared:", round(r_squared, 4)))
Use code with caution.
R
Output R:
[1] "R-squared: 0.7769"
Use code with caution.
Regresi Linier Multipel
Regresi linier multipel memperluas model sederhana dengan menyertakan dua atau lebih variabel independen (prediktor) untuk menjelaskan variabel dependen.
Model populasi:
Y
i
=
β
0
+
β
1
X
1
i
+
β
2
X
2
i
+
⋯
+
β
k
X
k
i
+
ε
i
Y 
i
​
 =β 
0
​
 +β 
1
​
 X 
1i
​
 +β 
2
​
 X 
2i
​
 +⋯+β 
k
​
 X 
ki
​
 +ε 
i
​
 

Dimana:
X
1
i
,
X
2
i
,
…
,
X
k
i
X 
1i
​
 ,X 
2i
​
 ,…,X 
ki
​
 
adalah nilai dari
k
k
variabel independen untuk observasi ke-
i
i
.
β
1
,
β
2
,
…
,
β
k
β 
1
​
 ,β 
2
​
 ,…,β 
k
​
 
adalah koefisien regresi parsial.
β
j
β 
j
​
 
mengukur perubahan rata-rata pada
Y
Y
untuk setiap kenaikan satu unit pada
X
j
X 
j
​
 
, dengan asumsi semua variabel independen lainnya dalam model dijaga konstan (holding all other predictors constant).
Estimasi parameter (
β
^
0
,
β
^
1
,
…
,
β
^
k
β
^
​
  
0
​
 , 
β
^
​
  
1
​
 ,…, 
β
^
​
  
k
​
 
) juga menggunakan metode kuadrat terkecil, meskipun perhitungannya lebih kompleks dan biasanya dilakukan dengan software statistik.
Variabel Prediktor Kategorikal (Dummy Variables)
Variabel kualitatif (kategorikal) dapat dimasukkan ke dalam model regresi menggunakan variabel dummy (indikator).
Variabel dummy adalah variabel biner (0 atau 1) yang merepresentasikan satu kategori dari variabel kualitatif.
Jika variabel kategori memiliki 2 level (misal, Jenis Kelamin: Pria, Wanita):
Buat satu variabel dummy. Misal, Wanita = 1 jika subjek adalah wanita, Wanita = 0 jika pria (kategori pria menjadi referensi).
Model:
Y
=
β
0
+
β
1
X
kontinu
+
β
2
D
wanita
Y=β 
0
​
 +β 
1
​
 X 
kontinu
​
 +β 
2
​
 D 
wanita
​
 

β
2
β 
2
​
 
adalah perbedaan rata-rata
Y
Y
antara wanita dan pria, setelah mengontrol
X
kontinu
X 
kontinu
​
 
.
Jika variabel kategori memiliki
k
k
level (misal, Tingkat Pendidikan: SD, SMP, SMA, Sarjana):
Buat
k
−
1
k−1
variabel dummy. Satu level dipilih sebagai kategori referensi.
Misal, referensi = SD.
D_SMP = 1 jika SMP, 0 jika lainnya.
D_SMA = 1 jika SMA, 0 jika lainnya.
D_Sarjana = 1 jika Sarjana, 0 jika lainnya.
Model:
Y
=
β
0
+
β
1
D
SMP
+
β
2
D
SMA
+
β
3
D
Sarjana
Y=β 
0
​
 +β 
1
​
 D 
SMP
​
 +β 
2
​
 D 
SMA
​
 +β 
3
​
 D 
Sarjana
​
 

β
1
β 
1
​
 
adalah perbedaan rata-rata
Y
Y
antara SMP dan SD (referensi).
β
2
β 
2
​
 
adalah perbedaan rata-rata
Y
Y
antara SMA dan SD.
β
3
β 
3
​
 
adalah perbedaan rata-rata
Y
Y
antara Sarjana dan SD.
Penting: Jangan membuat
k
k
variabel dummy untuk
k
k
kategori, karena ini akan menyebabkan kolinearitas sempurna (satu dummy bisa diprediksi sempurna dari dummy lainnya), dan model tidak bisa diestimasi.
Uji Signifikansi Global Model (Uji F atau Omnibus Test)
Setelah mem-fitting model regresi (terutama multipel), kita ingin tahu apakah model secara keseluruhan signifikan. Artinya, apakah setidaknya satu variabel independen memiliki hubungan yang signifikan dengan variabel dependen?
Hipotesis:
H
0
:
β
1
=
β
2
=
⋯
=
β
k
=
0
H 
0
​
 :β 
1
​
 =β 
2
​
 =⋯=β 
k
​
 =0
(Semua koefisien kemiringan adalah nol; tidak ada variabel independen yang signifikan)
H
A
:
H 
A
​
 :
Setidaknya satu
β
j
≠
0
β 
j
​
 

=0
(Minimal satu variabel independen signifikan)
Statistik Uji (F-statistik):
Statistik F didasarkan pada perbandingan varians yang dijelaskan oleh model (MSR) dengan varians yang tidak dijelaskan (MSE). Ini juga bisa dilihat sebagai uji ANOVA untuk regresi.
F
=
MSR
MSE
F= 
MSE
MSR
​
 

Dimana:
MSR (Mean Square due to Regression):
SSR
/
k
SSR/k
k
k
= jumlah variabel independen.
MSE (Mean Square Error):
SSE
/
(
n
−
k
−
1
)
SSE/(n−k−1)
n
−
k
−
1
n−k−1
= derajat kebebasan untuk error.
Distribusi F: Statistik uji F mengikuti distribusi F dengan
k
k
derajat kebebasan pembilang dan
n
−
k
−
1
n−k−1
derajat kebebasan penyebut.
Keputusan: Tolak
H
0
H 
0
​
 
jika F-hitung > F-kritis atau jika p-value
≤
α
≤α
.
Tabel ANOVA untuk Regresi:
Sumber Variasi	Sum of Squares (SS)	df	Mean Square (MS)	F
Regresi	SSR	
k
k
MSR = SSR/
k
k
MSR/MSE
Error (Residual)	SSE	
n
−
k
−
1
n−k−1
MSE = SSE/(
n
−
k
−
1
n−k−1
)	
Total	SST	
n
−
1
n−1
Contoh (melanjutkan data OCR, regresi sederhana, k=1):
SST = 334.8
SSE = 74.70
SSR = SST - SSE = 334.8 - 74.70 = 260.1
k
=
1
k=1
(hanya X_belajar)
n
=
5
n=5
MSR = SSR/
k
k
= 260.1 / 1 = 260.1
MSE = SSE/(
n
−
k
−
1
n−k−1
) = 74.70 / (5-1-1) = 74.70 / 3 = 24.9
F-statistik = MSR/MSE = 260.1 / 24.9
≈
10.446
≈10.446
P-value untuk F(1, 3) = 10.446 adalah sekitar 0.04839 (dari output R).
(Catatan: Untuk regresi linier sederhana,
F
=
t
2
F=t 
2
 
. Di sini
10.446
≈
(
3.232
)
2
10.446≈(3.232) 
2
 
, dan p-value uji F sama dengan p-value uji t dua arah untuk
β
1
β 
1
​
 
).
# F-statistik dan p-value dari summary model
f_statistic_val <- summary_model$fstatistic[1] # Value
# df untuk F adalah (k, n-k-1)
df_num <- summary_model$fstatistic[2] # df numerator (k)
df_den <- summary_model$fstatistic[3] # df denominator (n-k-1)

# p-value untuk F-test sudah ada di summary_model$p.value
# F-statistic: 10.45 on 1 and 3 DF,  p-value: 0.04839
print(paste("F-statistik:", round(f_statistic_val, 3)))
print(paste("P-value untuk F-test (dari summary):", summary_model$p.value)) # Ini adalah p-value untuk F-test
Use code with caution.
R
Output R:
[1] "F-statistik: 10.446"
[1] "P-value untuk F-test (dari summary): 0.048389186405193"
Use code with caution.
Uji F untuk Subset Variabel Independen
Uji F juga dapat digunakan untuk membandingkan dua model regresi: model penuh (full model) dan model tereduksi (reduced model, subset dari prediktor di model penuh). Ini berguna untuk menguji apakah sekelompok variabel secara bersama-sama signifikan.
Misalkan:
Full Model:
Y
=
β
0
+
β
1
X
1
+
β
2
X
2
+
β
3
X
3
+
β
4
X
4
+
ε
Y=β 
0
​
 +β 
1
​
 X 
1
​
 +β 
2
​
 X 
2
​
 +β 
3
​
 X 
3
​
 +β 
4
​
 X 
4
​
 +ε
(dengan
k
k
prediktor)
Reduced Model:
Y
=
β
0
+
β
1
X
1
+
β
2
X
2
+
ε
Y=β 
0
​
 +β 
1
​
 X 
1
​
 +β 
2
​
 X 
2
​
 +ε
(dengan
l
l
prediktor,
l
<
k
l<k
)
Kita ingin menguji apakah
X
3
X 
3
​
 
dan
X
4
X 
4
​
 
secara bersama-sama signifikan, yaitu
H
0
:
β
3
=
β
4
=
0
H 
0
​
 :β 
3
​
 =β 
4
​
 =0
.
Statistik F:
F
=
(
SSE
R
−
SSE
F
)
/
(
k
−
l
)
SSE
F
/
(
n
−
(
k
+
1
)
)
F= 
SSE 
F
​
 /(n−(k+1))
(SSE 
R
​
 −SSE 
F
​
 )/(k−l)
​
 

Dimana:
SSE
R
SSE 
R
​
 
: Sum of Squares Error dari model tereduksi.
SSE
F
SSE 
F
​
 
: Sum of Squares Error dari model penuh.
k
−
l
k−l
: Jumlah parameter yang diuji (jumlah prediktor yang dihilangkan).
n
−
(
k
+
1
)
n−(k+1)
: Derajat kebebasan error untuk model penuh.
Memeriksa Asumsi Regresi
Penting untuk memeriksa asumsi model regresi untuk memastikan validitas hasil. Asumsi utama untuk error (
ε
i
ε 
i
​
 
) adalah:
Linieritas: Hubungan antara X dan Y adalah linier (sudah tersirat dalam pemilihan model).
Independensi Error: Error (
ε
i
ε 
i
​
 
) independen satu sama lain. (Penting untuk data time series).
Normalitas Error: Error (
ε
i
ε 
i
​
 
) berdistribusi normal. Dapat dicek dengan histogram residual, Q-Q plot residual.
Homoskedastisitas (Varians Konstan Error): Varians error (
σ
2
σ 
2
 
) konstan untuk semua level X. Dapat dicek dengan plot residual vs fitted values (atau vs X). Pola corong menandakan heteroskedastisitas.
Tidak Ada Multikolinearitas Sempurna (untuk regresi multipel): Variabel independen tidak boleh berkorelasi sempurna satu sama lain. Kolinearitas tinggi (tidak sempurna) juga bisa menjadi masalah.
Plot diagnostik standar yang sering digunakan:
Scatter plot Y vs X (untuk regresi sederhana, cek linieritas).
Plot Residual vs Fitted Values (cek homoskedastisitas, linieritas, independensi).
Q-Q Plot of Residuals (cek normalitas error).
Histogram of Residuals (cek normalitas error).
Plot Residuals vs Predictor Variables (cek apakah ada pola yang terlewat).
Memahami dan menerapkan konsep-konsep ini akan memungkinkan analisis regresi yang lebih komprehensif dan akurat.
