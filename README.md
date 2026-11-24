# Çalışan Maaş, Performans Analizi ve Veri Ön İşleme

Sentetik insan kaynakları (İK) verisi üzerinde Python, Pandas ve NumPy kullanarak çalışan maaş-performans analizi, özellik mühendisliği (feature engineering), kategorik veri kodlama (encoding) ve dengesiz veri seti dengeleme (resampling) süreçlerini uçtan uca uygulayan veri analizi çalışması.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Veri%20Analizi-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Sayısal%20İşlemler-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Resampling-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

---

## Projenin Amacı ve Çözdüğü Problem

İnsan kaynakları ve organizasyon verileri çoğu zaman ham hâlde bulunur; departmanlar arası maaş/performans dağılımını görmek, deneyim düzeyine göre yeni metrikler türetmek ve veriyi makine öğrenmesi modellerine hazırlamak sistemli bir ön işleme süreci gerektirir.

Bu proje aşağıdaki temel veri bilimi problemlerini pratik ve tekrarlanabilir (`seed=42`) bir akışla ele alır:
* Ham çalışan kayıtlarından genel ve departman bazlı özet iş metrikleri üretmek.
* Mevcut sütunlardan anlamlı kategorik ve sayısal yeni özellikler türetmek.
* Metinsel/kategorik sütunları sayısal formata (Ordinal ve One-Hot Encoding) dönüştürmek.
* Azınlık sınıfların baskılandığı dengesiz (imbalanced) veri dağılımlarını çoğaltma (oversampling) yöntemiyle dengelemek.

---

## Öne Çıkan Özellikler ve Analiz Adımları

1. **Tekrarlanabilir Sentetik Veri Seti Oluşturma**
   * `np.random.seed(42)` ile sabitlenmiş, **200 çalışan** ve **5 departman** (`Software`, `HR`, `Finance`, `Sales`, `Marketing`) içeren 9 sütunlu veri seti (`EmployeeId`, `Department`, `Age`, `ExperienceYears`, `EducationLevel`, `Salary`, `PerformanceScore`, `OvertimeHours`, `ProjectsCompleted`).
2. **Genel Özet ve Departman Bazlı Analiz**
   * Toplam çalışan ve departman sayısı ile ortalama maaş (TL), ortalama deneyim (yıl) ve ortalama performans puanının hesaplanması.
   * `groupby` ve `agg` kullanarak her departman için çalışan sayısı, ortalama maaş, ortalama performans ve ortalama deneyim tablosunun oluşturulması.
3. **Özellik Mühendisliği (Feature Engineering) ve Kırılım Analizleri**
   * **Deneyim Seviyesi (`ExperienceLevel`):** `ExperienceYears` değerine göre `Junior` (0–2 yıl), `Mid` (3–5 yıl), `Senior` (6–10 yıl) ve `Expert` (11+ yıl) segmentasyonu.
   * **Deneyim Başına Maaş (`SalaryPerExperience`):** Sıfır yıl deneyimli çalışanlarda sıfıra bölünme hatasını önleyerek (`replace(0, 1)`) deneyim yılı başına düşen maaşın hesaplanması.
   * **Mesai ve Proje Kırılımları:** 20 saat üzeri mesai yapanların (`Fazla Mesai` / `Az/Yok`) ortalama performans karşılaştırması ve 15'ten fazla proje tamamlayanların (`Çok Proje` / `Az Proje`) ortalama maaş karşılaştırması.
4. **Kategorik Veri Kodlama (Encoding)**
   * `ExperienceLevel` sütunu için sıralı kodlama (**Ordinal Encoding**: `Junior: 0`, `Mid: 1`, `Senior: 2`, `Expert: 3`).
   * `Department` sütunu için `pd.get_dummies(..., dtype=int)` ile **One-Hot Encoding**.
5. **Dengesiz Veri Seti Dengeleme (Oversampling / Resampling)**
   * `Software` (70), `HR` (5) ve `Finance` (5) olmak üzere 80 satırlık dengesiz veri dağılımının, `resample` (`replace=True`, `random_state=42`) yöntemiyle tüm sınıflar **70'er örnek** (toplam 210 satır) olacak şekilde dengelenmesi.

### Gerçek Proje Çıktıları ve Bulgular

* **Toplam Çalışan / Departman:** 200 çalışan, 5 departman
* **Ortalama Maaş:** `[9654.43 TL]`
* **Ortalama Deneyim:** `[9.5 Yıl]`
* **Ortalama Performans Puanı:** `[48.6]`
* **Resampling Dağılımı:** Öncesi → `Software: 70, HR: 5, Finance: 5` | Sonrası → `Software: 70, HR: 70, Finance: 70`

---

## Kullanılan Teknolojiler ve Kütüphaneler

| Teknoloji / Kütüphane | Kullanım Amacı |
| :--- | :--- |
| **Python 3** | Ana programlama dili |
| **Pandas** | DataFrame oluşturma, `groupby` analizleri, özellik mühendisliği ve encoding (`map`, `get_dummies`) |
| **NumPy** | Tekrarlanabilir (`seed=42`) sentetik veri üretimi |
| **Scikit-learn** | Dengesiz veri setinde azınlık sınıfları çoğaltma (`sklearn.utils.resample`) |
| **Jupyter Notebook** | Etkileşimli kod geliştirme ve analiz dokümantasyonu |

---

## Kurulum ve Çalıştırma

Projeyi kendi bilgisayarınızda çalıştırmak için aşağıdaki adımları izleyin:

1. **Depoyu klonlayın:**
   ```bash
   git clone [https://github.com/](https://github.com/)[esmanuryavuz908]/[calisan-maas-performans-analizi].git
   cd [calisan-maas-performans-analizi]
   ```

2. **(Önerilen) Sanal ortam oluşturun ve aktif edin:**
   ```bash
   python -m venv venv
   # Windows için:
   venv\Scripts\activate
   # macOS / Linux için:
   source venv/bin/activate
   ```

3. **Gerekli kütüphaneleri yükleyin:**
   ```bash
   pip install pandas numpy scikit-learn jupyter
   ```

4. **Jupyter Notebook'u başlatın ve dosyayı çalıştırın:**
   ```bash
   jupyter notebook
   ```
   Açılan arayüzden `calisan_maas_performans_analizi.ipynb` dosyasını açın ve tüm hücreleri sırayla (**Restart & Run All**) çalıştırın.

---
