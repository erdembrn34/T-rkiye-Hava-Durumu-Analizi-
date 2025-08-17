# Proje: Türkiye Hava Durumu Analizi

## 1️⃣ README.md

````markdown
# Türkiye Hava Durumu Analizi

Bu proje, Türkiye'deki hava durumu verilerini kullanarak günlük sıcaklık değişimleri ve hava durumu açıklamalarının analizini yapmaktadır.

## İçerik
- Şehirlere göre günlük sıcaklık değişimi
- Hava durumu sıklıkları
- Zaman serisi analizi (Tarihe göre sıcaklık trendi)
- Kelime bulutu (hava durumu açıklamalarının sık kullanılan kelimeleri)

## Kullanım
1. Kaggle'dan veri setini indirin: [Türkiye Hava Durumu Verisi](https://www.kaggle.com/datasets/aslemimolu/trkiye-hava-durumu-verisi-kasm-2024)
2. `weather_analysis.ipynb` dosyasını açın ve çalıştırın.
3. Grafikleri ve analizleri görüntüleyin.

## Gereksinimler
```bash
pip install pandas matplotlib seaborn wordcloud
```
````

---

## 2️⃣ Jupyter Notebook (`weather_analysis.ipynb`)

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from wordcloud import WordCloud

# Veri Yükleme
df = pd.read_csv("hava_durumu_tahmini.csv")

# 1️⃣ Genel Bilgi
print(df.info())
print(df.head())

# 2️⃣ Sıcaklık İstatistikleri
print(df['Sıcaklık (°C)'].describe())

# 3️⃣ Şehirlere Göre Günlük Sıcaklık Değişimi
plt.figure(figsize=(12,6))
sns.lineplot(data=df, x='Tarih', y='Sıcaklık (°C)', hue='Şehir', marker='o')
plt.title("Şehirlere Göre Günlük Sıcaklık Değişimi")
plt.xlabel("Tarih")
plt.ylabel("Sıcaklık (°C)")
plt.xticks(rotation=45)
plt.show()

# 4️⃣ Hava Durumu Açıklamaları Sıklığı
plt.figure(figsize=(12,6))
sns.countplot(y='Durum', data=df, order=df['Durum'].value_counts().index)
plt.title("Hava Durumu Sıklıkları")
plt.xlabel("Adet")
plt.ylabel("Hava Durumu")
plt.show()

# 5️⃣ Zaman Serisi Analizi (Tarihe Göre Ortalama Sıcaklık)
df['Tarih'] = pd.to_datetime(df['Tarih'])
daily_avg = df.groupby('Tarih')['Sıcaklık (°C)'].mean()
plt.figure(figsize=(12,6))
daily_avg.plot(marker='o')
plt.title("Tarihe Göre Günlük Ortalama Sıcaklık")
plt.xlabel("Tarih")
plt.ylabel("Ortalama Sıcaklık (°C)")
plt.xticks(rotation=45)
plt.show()

# 6️⃣ Kelime Bulutu (Hava Durumu Açıklamaları)
text = " ".join(desc for desc in df['Durum'].dropna())
wordcloud = WordCloud(width=800, height=400, background_color='white').generate(text)
plt.figure(figsize=(12,6))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.show()
```

---

## 3️⃣ requirements

```
pandas
matplotlib
seaborn
wordcloud
```

