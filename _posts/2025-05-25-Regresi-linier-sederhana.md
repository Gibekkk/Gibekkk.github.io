---
title: Regresi Linier Sederhana - Konsep Dasar dan Estimasi
author: KingPublic
date: 2025-05-25 14:00:00 +0800
categories: [Statistika, Regresi]
tags: [regresi linier, regresi sederhana, model probabilistik, estimasi parameter, least squares, koefisien regresi]
math: true
image:
  path: /assets/img/simplelinier.png
  alt: Regresi Linier Sederhana
---

Regresi adalah teknik statistik yang digunakan untuk memodelkan dan menganalisis hubungan antara variabel. Secara spesifik, regresi mengeksploitasi hubungan antara satu atau lebih variabel independen (prediktor) untuk memprediksi atau menjelaskan variabel dependen (respons).

## Apa itu Regresi Linier Sederhana?

**Regresi Linier Sederhana** adalah model yang mencoba menjelaskan hubungan antara satu variabel dependen ($$Y$$) dan satu variabel independen ($$X$$) menggunakan garis lurus (linier).

**Tujuan Regresi:**
*   **Prediksi**: Memperkirakan nilai variabel dependen berdasarkan nilai variabel independen.
*   **Estimasi**: Mengestimasi parameter hubungan (kemiringan dan intersep).
*   **Pengujian Hipotesis**: Menguji apakah ada hubungan yang signifikan antara variabel.
*   **Pemodelan Hubungan Kausal**: Dalam beberapa kasus (dengan desain penelitian yang tepat), regresi dapat membantu memahami hubungan sebab-akibat.

## Istilah dalam Regresi

| Variabel Dependen ($$Y$$) | Variabel Independen ($$X$$) |
| :----------------------- | :-------------------------- |
| Outcome Variable         | Predictor Variable          |
| Response Variable        | Explanatory Variable        |
| Variabel Terikat         | Variabel Bebas              |
| Variabel yang dijelaskan | Variabel yang menjelaskan   |

## Model Regresi Linier Sederhana Probabilistik

Hubungan antara variabel di dunia nyata jarang sekali deterministik sempurna. Oleh karena itu, kita menggunakan model probabilistik yang menyertakan komponen acak (error).

Model regresi linier sederhana probabilistik untuk populasi adalah:
$$ Y_i = \beta_0 + \beta_1 X_i + \varepsilon_i $$

Dimana:
*   $$Y_i$$: Nilai variabel dependen untuk observasi ke-$$i$$.
*   $$X_i$$: Nilai variabel independen untuk observasi ke-$$i$$.
*   $$\beta_0$$ (beta-nol): **Intersep populasi**, yaitu nilai rata-rata $$Y$$ ketika $$X=0$$.
*   $$\beta_1$$ (beta-satu): **Kemiringan (slope) populasi**, yaitu perubahan rata-rata pada $$Y$$ untuk setiap kenaikan satu unit pada $$X$$.
*   $$\varepsilon_i$$ (epsilon): **Error acak (residual)** untuk observasi ke-$$i$$. Ini mewakili faktor-faktor lain yang memengaruhi $$Y$$ selain $$X$$, serta variabilitas acak. Diasumsikan $$\varepsilon_i$$ berdistribusi normal dengan rata-rata 0 dan varians konstan $$\sigma^2$$ ($$\varepsilon_i \sim N(0, \sigma^2)$$), dan independen satu sama lain.

### Implikasi Model Probabilistik
*   **Nilai Harapan (Expected Value) Y**: Untuk nilai $$X$$ tertentu (misal $$X^*$$), nilai harapan $$Y$$ adalah fungsi linier dari $$X$$:
    $$ E(Y | X=X^*) = \mu_{Y|X^*} = \beta_0 + \beta_1 X^* $$
    Ini adalah **garis regresi populasi sejati**.
*   **Varians Y**: Untuk nilai $$X$$ tertentu, varians $$Y$$ adalah konstan:
    $$ V(Y | X=X^*) = \sigma^2_{Y|X^*} = \sigma^2 $$

### Contoh Interpretasi Parameter
Misalkan model regresi untuk hubungan antara tinggi badan ($$X$$, dalam cm) dan berat badan ($$Y$$, dalam kg) adalah:
$$ Y = -50 + 0.8 X $$
*   $$\beta_0 = -50$$: Secara teoritis, jika tinggi seseorang 0 cm (tidak realistis), beratnya -50 kg. Intersep seringkali tidak memiliki interpretasi praktis jika $$X=0$$ berada di luar rentang data observasi.
*   $$\beta_1 = 0.8$$: Untuk setiap kenaikan 1 cm tinggi badan, berat badan rata-rata diperkirakan meningkat sebesar 0.8 kg.

## Estimasi Parameter Model Regresi

Karena parameter populasi ($$\beta_0, \beta_1, \sigma^2$$) biasanya tidak diketahui, kita perlu mengestimasinya menggunakan data sampel. Estimasi ini dilambangkan dengan $$\hat{\beta}_0$$ (baca: beta-nol-topi) dan $$\hat{\beta}_1$$ (beta-satu-topi).

Model regresi linier sampel (garis regresi yang diestimasi):
$$ \hat{Y}_i = \hat{\beta}_0 + \hat{\beta}_1 X_i $$
Dimana $$\hat{Y}_i$$ adalah nilai prediksi $$Y$$ untuk observasi ke-$$i$$.

### Metode Kuadrat Terkecil (Least Squares Method)
Metode yang paling umum digunakan untuk mengestimasi $$\hat{\beta}_0$$ dan $$\hat{\beta}_1$$ adalah metode kuadrat terkecil. Metode ini mencari nilai $$\hat{\beta}_0$$ dan $$\hat{\beta}_1$$ yang meminimalkan jumlah kuadrat dari selisih antara nilai observasi $$Y_i$$ dan nilai prediksi $$\hat{Y}_i$$ (yaitu, meminimalkan jumlah kuadrat error/residual).
$$ \text{Minimalkan SSE} = \sum_{i=1}^{n} (Y_i - \hat{Y}_i)^2 = \sum_{i=1}^{n} (Y_i - (\hat{\beta}_0 + \hat{\beta}_1 X_i))^2 $$

**Rumus Estimator Least Squares:**
1.  **Estimator Kemiringan ($$\hat{\beta}_1$$):**
    $$ \hat{\beta}_1 = \frac{\sum_{i=1}^{n}(X_i - \bar{X})(Y_i - \bar{Y})}{\sum_{i=1}^{n}(X_i - \bar{X})^2} = \frac{\text{Cov}(X,Y)}{\text{Var}(X)} $$
    Atau, bisa juga ditulis sebagai:
    $$ \hat{\beta}_1 = r \frac{s_Y}{s_X} $$
    Dimana $$r$$ adalah koefisien korelasi Pearson antara X dan Y, $$s_Y$$ adalah simpangan baku Y, dan $$s_X$$ adalah simpangan baku X.

2.  **Estimator Intersep ($$\hat{\beta}_0$$):**
    $$ \hat{\beta}_0 = \bar{Y} - \hat{\beta}_1 \bar{X} $$

Dimana $$\bar{X}$$ dan $$\bar{Y}$$ adalah rata-rata sampel dari X dan Y.

### Nilai Prediksi dan Residual
*   **Nilai Prediksi (Fitted Values, $$\hat{Y}_i$$)**: Nilai $$Y$$ yang diprediksi oleh model regresi sampel untuk setiap $$X_i$$.
    $$ \hat{Y}_i = \hat{\beta}_0 + \hat{\beta}_1 X_i $$
*   **Residual ($$e_i$$)**: Selisih antara nilai observasi aktual $$Y_i$$ dan nilai prediksi $$\hat{Y}_i$$. Ini adalah estimasi dari error populasi $$\varepsilon_i$$.
    $$ e_i = Y_i - \hat{Y}_i $$

Residual sangat penting untuk mengevaluasi kecocokan model dan memeriksa asumsi.

### Estimasi Varians Error ($$\hat{\sigma}^2$$)
Varians error ($$\sigma^2$$) diestimasi oleh **Mean Squared Error (MSE)** atau varians residual ($$s_e^2$$):
$$ \hat{\sigma}^2 = s_e^2 = \text{MSE} = \frac{\text{SSE}}{n-2} $$
Dimana **Sum of Squared Errors (SSE)** adalah:
$$ \text{SSE} = \sum_{i=1}^{n} e_i^2 = \sum_{i=1}^{n} (Y_i - \hat{Y}_i)^2 $$
Pembaginya adalah $$n-2$$ karena kita mengestimasi dua parameter ($$\beta_0$$ dan $$\beta_1$$) dari data. Akar kuadrat dari MSE, yaitu $$s_e = \sqrt{\text{MSE}}$$, disebut **Standard Error of the Estimate** atau simpangan baku residual.

## Contoh Perhitungan Estimasi Model Regresi (dari Materi OCR)

Data Observasi:
| No | X (Jam Belajar) | Y (Nilai Ujian) |
| :--: | :-------------: | :-------------: |
| 1  | 1               | 50              |
| 2  | 2               | 55              |
| 3  | 3               | 53              |
| 4  | 4               | 70              |
| 5  | 5               | 68              |

**a. Hitung nilai rata-rata:**
*   $$\bar{X} = (1+2+3+4+5)/5 = 15/5 = 3$$
*   $$\bar{Y} = (50+55+53+70+68)/5 = 296/5 = 59.2$$

**b. Hitung komponen untuk $$\hat{\beta}_1$$:**
| $$X_i$$ | $$Y_i$$ | $$X_i - \bar{X}$$ | $$Y_i - \bar{Y}$$ | $$(X_i - \bar{X})(Y_i - \bar{Y})$$ | $$(X_i - \bar{X})^2$$ |
| :-----: | :-----: | :---------------: | :---------------: | :---------------------------------: | :-------------------: |
| 1       | 50      | -2                | -9.2              | 18.4                                | 4                     |
| 2       | 55      | -1                | -4.2              | 4.2                                 | 1                     |
| 3       | 53      | 0                 | -6.2              | 0.0                                 | 0                     |
| 4       | 70      | 1                 | 10.8              | 10.8                                | 1                     |
| 5       | 68      | 2                 | 8.8               | 17.6                                | 4                     |
| **Sum** |         |                   |                   | **51.0**                            | **10**                |

*   $$\sum(X_i - \bar{X})(Y_i - \bar{Y}) = 51$$
*   $$\sum(X_i - \bar{X})^2 = 10$$

**c. Estimasi $$\hat{\beta}_1$$:**
$$ \hat{\beta}_1 = \frac{51}{10} = 5.1 $$
Interpretasi: Untuk setiap tambahan 1 jam belajar, nilai ujian rata-rata diperkirakan meningkat sebesar 5.1 poin.

**d. Estimasi $$\hat{\beta}_0$$:**
$$ \hat{\beta}_0 = \bar{Y} - \hat{\beta}_1 \bar{X} = 59.2 - (5.1)(3) = 59.2 - 15.3 = 43.9 $$
Interpretasi: Jika jam belajar adalah 0 (secara teoritis), nilai ujian rata-rata diperkirakan 43.9.

**e. Model Regresi Sampel:**
$$ \hat{Y} = 43.9 + 5.1 X $$

**f. Hitung Nilai Prediksi ($$\hat{Y}_i$$) dan Residual ($$e_i$$):**

| No | $$X_i$$ | $$Y_i$$ | $$\hat{Y}_i = 43.9 + 5.1 X_i$$ | $$e_i = Y_i - \hat{Y}_i$$ | $$e_i^2$$ |
| :--: | :-----: | :-----: | :---------------------------: | :-----------------------: | :-------: |
| 1  | 1       | 50      | $$43.9 + 5.1(1) = 49.0$$      | $$50 - 49.0 = 1.0$$       | 1.00      |
| 2  | 2       | 55      | $$43.9 + 5.1(2) = 54.1$$      | $$55 - 54.1 = 0.9$$       | 0.81      |
| 3  | 3       | 53      | $$43.9 + 5.1(3) = 59.2$$      | $$53 - 59.2 = -6.2$$      | 38.44     |
| 4  | 4       | 70      | $$43.9 + 5.1(4) = 64.3$$      | $$70 - 64.3 = 5.7$$       | 32.49     |
| 5  | 5       | 68      | $$43.9 + 5.1(5) = 69.4$$      | $$68 - 69.4 = -1.4$$      | 1.96      |
|    |         |         |                               | **Sum $$e_i^2$$ (SSE)**   | **74.70** |

**g. Hitung Varians Error ($$\hat{\sigma}^2$$ atau MSE):**
$$ \text{SSE} = 74.70 $$
$$ n = 5 $$
$$ \hat{\sigma}^2 = \text{MSE} = \frac{\text{SSE}}{n-2} = \frac{74.70}{5-2} = \frac{74.70}{3} = 24.9 $$

**h. Standard Error of the Estimate ($$s_e$$):**
$$ s_e = \sqrt{\text{MSE}} = \sqrt{24.9} \approx 4.99 $$
Ini adalah ukuran tipikal seberapa jauh nilai observasi $$Y$$ menyimpang dari garis regresi.

```r
# Data dari contoh OCR
X_belajar <- c(1, 2, 3, 4, 5)
Y_nilai <- c(50, 55, 53, 70, 68)

# Membuat model regresi linier di R
model_regresi <- lm(Y_nilai ~ X_belajar)

# Menampilkan ringkasan model (termasuk koefisien)
summary(model_regresi)

# Koefisien
beta_0_hat <- coef(model_regresi)[1] # Intercept
beta_1_hat <- coef(model_regresi)[2] # Slope untuk X_belajar
print(paste("Estimasi Beta_0 (Intercept):", round(beta_0_hat, 1)))
print(paste("Estimasi Beta_1 (Slope):", round(beta_1_hat, 1)))

# Nilai prediksi
Y_hat <- predict(model_regresi)
print("Nilai Prediksi (Y_hat):")
print(round(Y_hat, 1))

# Residual
residuals_e <- residuals(model_regresi)
print("Residual (e):")
print(round(residuals_e, 1))

# SSE
sse <- sum(residuals_e^2)
print(paste("SSE:", round(sse, 2)))

# MSE dan Standard Error of the Estimate
n_obs <- length(Y_nilai)
df_error <- n_obs - 2 # n-k-1, k=1 (jumlah prediktor)
mse_calc <- sse / df_error # Di R, summary(model_regresi)$sigma^2 adalah MSE
s_e_calc <- sqrt(mse_calc) # Di R, summary(model_regresi)$sigma adalah s_e
print(paste("MSE (Manual Calc):", round(mse_calc, 2)))
print(paste("Standard Error of the Estimate (s_e, Manual Calc):", round(s_e_calc, 2)))
Use code with caution.
Output R akan mengkonfirmasi perhitungan manual:
[1] "Estimasi Beta_0 (Intercept): 43.9"
[1] "Estimasi Beta_1 (Slope): 5.1"
[1] "Nilai Prediksi (Y_hat):"
[1] 49.0 54.1 59.2 64.3 69.4
[1] "Residual (e):"
[1]  1.0  0.9 -6.2  5.7 -1.4
[1] "SSE: 74.7"
[1] "MSE (Manual Calc): 24.9"
[1] "Standard Error of the Estimate (s_e, Manual Calc): 4.99"
Use code with caution.
Langkah selanjutnya adalah melakukan inferensi statistik terhadap parameter model, seperti menguji signifikansi
β
1
β 
1
​
 
, yang akan dibahas lebih lanjut.