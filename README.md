# Sistem Rekomendasi Makanan - Jihan Kusumawardhani
 
## Domain Proyek
 
### **Latar Belakang**
 
Sektor kuliner di Indonesia saat ini mengalami ekspansi yang sangat dinamis, dicirikan oleh kemunculan restoran, rumah makan, dan kafe dalam jumlah yang terus meningkat. Diversitas pilihan hidangan yang melimpah ini, meskipun memberikan kekayaan variasi, justru kerap memicu overwhelm pada benak konsumen, menyulitkan mereka dalam menyeleksi opsi yang benar-benar selaras dengan preferensi pribadi, kebutuhan diet spesifik, atau bahkan suasana hati pada momen tertentu. Di sisi lain, para pelaku usaha di industri gastronomis ini juga dihadapkan pada imperatif untuk mengadopsi pendekatan inovatif guna menggenjot profitabilitas operasional dan memperluas basis pelanggan di tengah kompetisi pasar yang kian intensif.
 
Merespons kompleksitas ini, sebuah solusi berbasis teknologi menjadi krusial: pengembangan sistem rekomendasi makanan yang adaptif dan cerdas. Sistem semacam ini dirancang untuk mampu menyajikan saran yang sangat personalized, didasarkan pada analisis mendalam terhadap pola preferensi historis pengguna dan karakteristik intrinsik dari setiap item makanan. Implementasi teknologi ini tidak hanya bertujuan untuk menyederhanakan proses pengambilan keputusan bagi konsumen, tetapi juga memberikan keunggulan kompetitif bagi penyedia layanan kuliner melalui penargetan promosi menu yang lebih akurat dan peningkatan kepuasan pelanggan secara signifikan.
 
 
Dalam kerangka kerja proyek ini, pengembangan sistem rekomendasi difasilitasi melalui adopsi dua metodologi fundamental yang saling melengkapi:
* **Pendekatan Berbasis Konten (*Content-Based Filtering*)**: Strategi ini menitikberatkan pada pemanfaatan atribut deskriptif intrinsik dari setiap item (misalnya, karakteristik atau kategori makanan) untuk mengidentifikasi dan memetakan tingkat kemiripan antar item, sehingga rekomendasi didasarkan pada kesesuaian profil item dengan preferensi yang dinyatakan atau inferensi dari pengguna.
* **Pendekatan Kolaboratif (*Collaborative Filtering*)**: Metodologi ini beroperasi dengan menganalisis dan memanfaatkan pola data umpan balik eksplisit maupun implisit dari interaksi pengguna terhadap item, guna memprediksi selera dan kecenderungan preferensi pengguna aktif, serta menyajikan rekomendasi yang lebih terpersonalisasi dan relevan.
 
Referensi: [Food Recommendation System](https://www.kaggle.com/datasets/schemersays/food-recommendation-system)
 
## Business Understanding
 
Proyek ini digagas dengan tujuan fundamental untuk memberdayakan konsumen dalam proses pengambilan keputusan pemilihan makanan, dengan secara presisi memandu mereka menuju opsi kuliner yang selaras dengan preferensi personal mereka yang unik. Selain itu, inisiatif riset ini juga berorientasi untuk memberikan wawasan strategis yang mendalam bagi para pelaku usaha di sektor kuliner, guna mengidentifikasi peluang peningkatan profitabilitas dan memperluas jangkauan pasar secara efektif.
 
 
### Pernyataan Masalah (*Problem Statement*)
 
* Bagaimana merancang dan mengimplementasikan mekanisme rekomendasi makanan yang mampu menyajikan saran yang sangat *personalized*, sehingga secara akurat merefleksikan dan memenuhi preferensi individual masing-masing pengguna?
* Bagaimana memanfaatkan secara optimal data *rating* historis pengguna dan informasi deskriptif yang kaya dari setiap item makanan untuk mengkonstruksi sistem rekomendasi yang tidak hanya akurat dalam prediksinya tetapi juga efisien dalam operasional komputasinya?
 
### Tujuan Proyek (*Project Goals*)
 
* Mengembangkan sebuah arsitektur sistem rekomendasi makanan yang memiliki kapabilitas esensial dalam menghasilkan sugesti kuliner yang terpersonalisasi, disesuaikan dengan profil dan riwayat interaksi pengguna.
* Mengimplementasikan secara paralel dua pendekatan algoritmik utama, yaitu *Content-Based Filtering* dan *Collaborative Filtering*, dengan tujuan mengoptimalkan performa rekomendasi melalui kombinasi kekuatan masing-masing metode.
 
### Pernyataan Solusi (*Solution Statement*)
 
* **Untuk *Content-Based Filtering*:** Mengaplikasikan teknik *TF-IDF Vectorizer* guna mengekstraksi representasi fitur tekstual yang signifikan dari deskripsi atau kategori makanan, yang kemudian diikuti dengan perhitungan *cosine similarity* untuk mengukur dan mengidentifikasi tingkat kemiripan antar makanan.
* **Untuk *Collaborative Filtering*:** Membangun sebuah arsitektur jaringan saraf tiruan (*neural network*), khususnya model *RecommenderNet* yang dilengkapi dengan *embedding layer*, untuk secara cerdas mempelajari pola interaksi kompleks antara identitas pengguna dan item makanan, serta memprediksi *rating* implisit atau eksplisit yang mungkin diberikan pengguna.
* Proses evaluasi kinerja model akan dilakukan secara komprehensif dengan menggunakan metrik *Precision* untuk menilai efektivitas *Content-Based Filtering*, dan *Root Mean Squared Error* (RMSE) untuk mengukur akurasi prediksi *rating* pada model *Collaborative Filtering*.
 
 
## Data Understanding
 
Proyek ini menggunakan dua *dataset* utama, yaitu **dataset makanan** dan **dataset rating**, yang keduanya bersumber dari [Food Recommendation System](https://www.kaggle.com/datasets/schemersays/food-recommendation-system).
 
### 1. Dataset Makanan
 
1. **Jumlah Data**  
   - Berdasarkan pemanggilan `df_makanan.shape`, didapatkan hasil **(400, 5)**.  
     Ini berarti **dataset makanan** memiliki **400 baris** dan **5 kolom**.
 
2. **Struktur Data**  
   - Hasil `df_makanan.info()` memberikan gambaran berikut:
     ```
     <class 'pandas.core.frame.DataFrame'>
     RangeIndex: 400 entries, 0 to 399
     Data columns (total 5 columns):
      #   Column    Non-Null Count  Dtype 
      ---  ------    --------------  ----- 
      0   Food_ID   400 non-null    int64 
      1   Name      400 non-null    object
      2   C_Type    400 non-null    object
      3   Veg_Non   400 non-null    object
      4   Describe  400 non-null    object
     dtypes: int64(1), object(4)
     memory usage: 15.8+ KB
     ```
     Terlihat bahwa tidak ada *missing value* pada setiap kolom di dataset makanan (masing-masing kolom memiliki 400 *non-null* entries).
 
 
3. **Uraian Fitur**  
   Berikut adalah deskripsi singkat mengenai setiap fitur pada dataset makanan:  
   * **Food_ID**: Kolom ini berfungsi sebagai pengidentifikasi primer yang unik dan tidak berulang untuk setiap item makanan yang tercatat dalam dataset.
   * **Name**: Atribut ini menyimpan penamaan spesifik dari masing-masing hidangan atau produk makanan, memberikan informasi deskriptif langsung kepada pengguna.
   * **C_Type**: Kategorisasi makanan ini mengacu pada jenis masakan atau klasifikasi umum dari hidangan (misalnya, masakan India, makanan ringan, hidangan penutup), yang penting untuk memfilter dan mengelompokkan preferensi.
   * **Veg_Non**: Kolom ini menyediakan klasifikasi biner mengenai status diet makanan, secara jelas menandakan apakah hidangan tersebut berbasis vegetarian atau non-vegetarian.
   * **Describe**: Atribut deskriptif ini memberikan rincian kontekstual yang lebih kaya mengenai makanan, seperti daftar bahan-bahan yang digunakan, metode persiapan, atau karakteristik unik lainnya.
 
4. **Distribusi Kategori Makanan**  
   Melalui perintah `df_makanan['C_Type'].value_counts().sort_values().plot(kind='barh')`, dihasilkan visualisasi gambar di bawah ini yang menunjukkan jumlah makanan pada setiap kategori. Dapat diamati bahwa **Indian**, **Healthy Food**, dan **Dessert** menjadi kategori terbanyak pada dataset ini.

![download](https://github.com/user-attachments/assets/7e68930a-6388-400f-8111-e833fa9725a8)

### 2. Dataset Rating
 
1. **Jumlah Data**  
   - Berdasarkan pemanggilan `df_rating.shape`, didapatkan hasil **(512, 3)**.  
     Ini berarti **dataset rating** memiliki **512 baris** dan **3 kolom**.
 
2. **Struktur Data**  
   - Hasil `df_rating.info()` memberikan gambaran berikut:
     ```
     <class 'pandas.core.frame.DataFrame'>
     RangeIndex: 512 entries, 0 to 511
     Data columns (total 3 columns):
      #   Column   Non-Null Count  Dtype  
      ---  ------   --------------  -----  
      0   User_ID  511 non-null    float64
      1   Food_ID  511 non-null    float64
      2   Rating   511 non-null    float64
     dtypes: float64(3)
     memory usage: 12.1 KB
     ```
     Terlihat bahwa terdapat 1 baris data *missing* untuk masing-masing kolom (511 *non-null* dari total 512 baris).
 
3. **Uraian Fitur**  
   Berikut adalah deskripsi singkat mengenai setiap fitur pada dataset rating:  
   
   * **User_ID:** Kolom ini berfungsi sebagai penanda unik untuk setiap individu pengguna yang telah berkontribusi dengan memberikan penilaian atau umpan balik. Identifikasi unik ini fundamental untuk melacak preferensi individual dan perilaku konsumsi dalam sistem.
   * **Food_ID:** Atribut ini merupakan identifikasi unik bagi setiap item makanan yang menjadi objek penilaian atau rekomendasi. Penting untuk dicatat bahwa `Food_ID` pada *dataset* rating ini secara langsung merujuk dan berkorespondensi dengan `Food_ID` yang terdapat pada *dataset* makanan utama, memastikan konsistensi dan kemampuan untuk menggabungkan informasi dari kedua sumber data.
   * **Rating:** Kolom `Rating` menyimpan nilai penilaian numerik yang diberikan oleh pengguna untuk sebuah makanan tertentu. Nilai ini merefleksikan tingkat kepuasan atau preferensi pengguna terhadap makanan tersebut. Secara umum, nilai *rating* ini berada dalam rentang skala 1 hingga 10, di mana nilai yang lebih tinggi mengindikasikan preferensi atau kepuasan yang lebih besar, dan sebaliknya. Informasi *rating* ini adalah inti dari data umpan balik eksplisit yang akan digunakan oleh algoritma rekomendasi.
 
 
4. **Distribusi Rating**  
   Melalui perintah `sns.displot(df_rating['Rating'], kde=True, bins=10)`, dihasilkan visualisasi gambar di bawah ini yang menunjukkan sebaran rating yang diberikan oleh pengguna. Rating tampak tersebar pada rentang 1–10, dengan beberapa puncak di nilai 3, 5, dan 10.

![download (1)](https://github.com/user-attachments/assets/3db9f8a0-5d99-48bc-ad5a-c5d56df01e5b)


## Data Preparation
 
Pada tahap Data Preparation, dilakukan serangkaian langkah untuk memastikan data yang akan digunakan dalam model bersih dan siap untuk diproses. Tahapan yang dilakukan meliputi:
 
### 1. Handling Missing Values & Penggabungan Data
 
Untuk menggabungkan informasi rating dengan data makanan, kedua dataset di-*merge* berdasarkan kolom `Food_ID`. Setelah itu, dilakukan pengecekan missing values dan penghapusan baris yang tidak lengkap.
 
```python
df_gabungan = pd.merge(df_rating, df_makanan[['Food_ID', 'Name', 'C_Type']], on='Food_ID', how='left')
print(df_gabungan.head())
print(df_gabungan.isnull().sum())
df_gabungan = df_gabungan.dropna()
```
 
**Output:**
 
```
   User_ID  Food_ID  Rating                        Name    C_Type
0      1.0     88.0     4.0     peri peri chicken satay     Snack
1      1.0     46.0     3.0     steam bunny chicken bao  Japanese
2      1.0     24.0     5.0  green lentil dessert fudge   Dessert
3      1.0     25.0     4.0          cashew nut cookies   Dessert
4      2.0     49.0     1.0        christmas tree pizza   Italian
```
 
```
User_ID    1
Food_ID    1
Rating     1
Name       1
C_Type     1
dtype: int64
```
 
### 2. Handling Duplicate & Sorting Data
 
Data hasil penggabungan kemudian diurutkan berdasarkan `Food_ID`. Setelah itu, duplikat dihapus agar setiap makanan hanya muncul sekali. Selain itu, terdapat penyesuaian nilai pada kolom `C_Type` (misalnya, mengubah `'Healthy Food'` menjadi `'Healthy_Food'`).
 
```python
df_urut = df_gabungan.sort_values('Food_ID', ascending=True)
print(df_urut.head())
print(len(df_urut['Food_ID'].unique()))
print(df_urut['C_Type'].unique())
```
 
**Output:**
 
```
     User_ID  Food_ID  Rating                  Name        C_Type
376     71.0      1.0    10.0   summer squash salad  Healthy Food
253     49.0      1.0     5.0   summer squash salad  Healthy Food
116     22.0      2.0     5.0  chicken minced salad  Healthy Food
200     39.0      2.0    10.0  chicken minced salad  Healthy Food
50       9.0      2.0     3.0  chicken minced salad  Healthy Food
```
 
```
309
```
 
```
['Healthy Food' 'Snack' 'Dessert' 'Japanese' 'Indian' 'French' 'Mexican'
 'Italian' 'Chinese' 'Beverage' 'Thai']
```
 
### 3. Pembuatan DataFrame Baru untuk Content-Based Filtering
 
Setelah pembersihan, dibuatlah dataframe baru untuk content-based filtering dengan mengekstrak kolom `Food_ID`, `Name`, dan `C_Type`. Data ini kemudian dikonversi ke format yang lebih sederhana dengan mengganti nama kolom (misalnya, `C_Type` menjadi `category`).
 
```python
list_id = df_prep['Food_ID'].tolist()
list_nama = df_prep['Name'].tolist()
list_kategori = df_prep['C_Type'].tolist()
 
print(len(list_id), len(list_nama), len(list_kategori))
 
df_makanan_baru = pd.DataFrame({
    'id': list_id,
    'food_name': list_nama,
    'category': list_kategori
})
 
print(df_makanan_baru.head())
print(df_makanan_baru.sample(5))
```
 
**Output:**
 
```
309 309 309
```
 
Contoh tampilan awal dataframe:
```
    id             food_name      category
0  1.0   summer squash salad  Healthy_Food
1  2.0  chicken minced salad  Healthy_Food
2  3.0  sweet chilli almonds         Snack
3  4.0       tricolour salad  Healthy_Food
4  5.0        christmas cake       Dessert
```
 
Contoh tampilan sample:
```
        id                    food_name category
169  170.0  fried rice with soya chunks  Chinese
196  197.0  cheese and avocado parantha  Mexican
295  296.0          tandoori fish tikka   Indian
124  125.0        cheese chicken kebabs   Indian
282  283.0            veg hakka noodles  Chinese
```
 
### 4. Ekstraksi Fitur dengan TF-IDF
 
Untuk mengukur pentingnya kata pada kolom `category`, digunakan metode TF-IDF. Tahap ini menghasilkan matriks fitur yang nantinya digunakan untuk menghitung derajat kemiripan antar makanan (cosine similarity).
 
```python
tfidf_vect = TfidfVectorizer()
tfidf_vect.fit(df_makanan_baru['category'])
print(tfidf_vect.get_feature_names_out())
 
tfidf_matrix = tfidf_vect.fit_transform(df_makanan_baru['category'])
print(tfidf_matrix.shape)
print(tfidf_matrix.todense())
```
 
**Output:**
 
```
['beverage' 'chinese' 'dessert' 'french' 'healthy_food' 'indian' 'italian'
 'japanese' 'mexican' 'snack' 'thai']
```
 
```
(309, 11)
```
 
Contoh tampilan matriks TF-IDF (dense):
```
[[0. 0. 0. ... 0. 0. 0.]
 [0. 0. 0. ... 0. 0. 0.]
 [0. 0. 0. ... 0. 1. 0.]
 ...
 [0. 0. 0. ... 0. 0. 0.]
 [0. 0. 0. ... 0. 0. 0.]
 [0. 0. 0. ... 0. 1. 0.]]
```
 
Untuk memberikan gambaran yang lebih terperinci, ditampilkan pula sample subset dari dataframe TF-IDF:
 
```python
df_tfidf = pd.DataFrame(tfidf_matrix.todense(), 
                        columns=tfidf_vect.get_feature_names_out(),
                        index=df_makanan_baru['food_name'])
print(df_tfidf.sample(11, axis=1).sample(10, axis=0))
```
 
**Output (Contoh Tampilan):**
 
```
                                                italian  indian  chinese  \
food_name                                                                  
thai pineapple rice                                 0.0     0.0      0.0   
shrimp & cilantro ceviche                           0.0     0.0      0.0   
chicken minced salad                                0.0     0.0      0.0   
sugar free modak                                    0.0     0.0      0.0   
black rice                                          0.0     0.0      0.0   
red rice poha                                       0.0     1.0      0.0   
curd rice                                           0.0     1.0      0.0   
chicken and mushroom lasagna                        1.0     0.0      0.0   
methi chicken masala                                0.0     1.0      0.0   
banana phirni tartlets with fresh strawberries      0.0     0.0      0.0   
 
                                                french  japanese  snack  \
food_name                                                                 
thai pineapple rice                                0.0       0.0    0.0   
shrimp & cilantro ceviche                          1.0       0.0    0.0   
chicken minced salad                               0.0       0.0    0.0   
sugar free modak                                   0.0       1.0    0.0   
black rice                                         0.0       0.0    0.0   
red rice poha                                      0.0       0.0    0.0   
curd rice                                          0.0       0.0    0.0   
chicken and mushroom lasagna                       0.0       0.0    0.0   
methi chicken masala                               0.0       0.0    0.0   
banana phirni tartlets with fresh strawberries     0.0       0.0    1.0   
 
                                                healthy_food  thai  dessert  \
food_name                                                                     
thai pineapple rice                                      0.0   1.0      0.0   
shrimp & cilantro ceviche                                0.0   0.0      0.0   
chicken minced salad                                     1.0   0.0      0.0   
sugar free modak                                         0.0   0.0      0.0   
black rice                                               1.0   0.0      0.0   
red rice poha                                            0.0   0.0      0.0   
curd rice                                                0.0   0.0      0.0   
chicken and mushroom lasagna                             0.0   0.0      0.0   
methi chicken masala                                     0.0   0.0      0.0   
banana phirni tartlets with fresh strawberries           0.0   0.0      0.0   
 
                                                beverage  mexican  
food_name                                                          
thai pineapple rice                                  0.0      0.0  
shrimp & cilantro ceviche                            0.0      0.0  
chicken minced salad                                 0.0      0.0  
sugar free modak                                     0.0      0.0  
black rice                                           0.0      0.0  
red rice poha                                        0.0      0.0  
curd rice                                            0.0      0.0  
chicken and mushroom lasagna                         0.0      0.0  
methi chicken masala                                 0.0      0.0  
banana phirni tartlets with fresh strawberries       0.0      0.0  
```
 
### 5. Pembuatan Dictionary untuk Collaborative Filtering
 
Untuk melakukan encoding pada data rating, dibuatlah dictionary yang memetakan `User_ID` dan `Food_ID` ke indeks numerik. Hal ini akan digunakan dalam model collaborative filtering.
 
```python
user_list = df_rating['User_ID'].unique().tolist()
print('User_ID list:', user_list)
 
user2idx = {user: idx for idx, user in enumerate(user_list)}
idx2user = {idx: user for idx, user in enumerate(user_list)}
print('Mapping User_ID:', user2idx)
print('Mapping indeks ke User_ID:', idx2user)
 
food_list = df_rating['Food_ID'].unique().tolist()
food2idx = {food: idx for idx, food in enumerate(food_list)}
idx2food = {idx: food for idx, food in enumerate(food_list)}
```
 
**Output:**
 
```
User_ID list: [1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 10,0, ... , 100.0]
```
 
```
Mapping User_ID: {1.0: 0, 2.0: 1, 3.0: 2, 4.0: 3, 5.0: 4, 6.0: 5, ... , 100.0: 99}
Mapping indeks ke User_ID: {0: 1.0, 1: 2.0, 2: 3.0, 3: 4.0, 4: 5.0, 5: 6.0, ... , 99: 100.0}
```
 
### 6. Persiapan Data untuk Training pada Collaborative Filtering
 
Setelah encoding, data rating dipersiapkan untuk training dengan melakukan mapping ulang ke variabel baru dan normalisasi rating. Data kemudian diacak dan dibagi menjadi training set dan validation set.
 
```python
df_rating['user'] = df_rating['User_ID'].map(user2idx)
df_rating['food'] = df_rating['Food_ID'].map(food2idx)
 
n_users = len(user2idx)
n_foods = len(idx2food)
print(n_users, n_foods)
 
df_rating['rating'] = df_rating['Rating'].astype(np.float32)
min_rat = df_rating['rating'].min()
max_rat = df_rating['rating'].max()
print('Jumlah User: {}, Jumlah Food: {}, Rating Min: {}, Rating Max: {}'.format(n_users, n_foods, min_rat, max_rat))
 
df_rating = df_rating.sample(frac=1, random_state=42)
 
X_data = df_rating[['user', 'food']].values
y_data = df_rating['rating'].apply(lambda x: (x - min_rat) / (max_rat - min_rat)).values
 
split_index = int(0.8 * df_rating.shape[0])
X_train, X_val = X_data[:split_index], X_data[split_index:]
y_train, y_val = y_data[:split_index], y_data[split_index:]
print(X_data, y_data)
```
 
**Output yang Diharapkan:**
 
- Tampilan jumlah pengguna dan jumlah makanan:
  ```
  100 309
  ```
- Informasi rating:
  ```
  Jumlah User: 100, Jumlah Food: 309, Rating Min: 1.0, Rating Max: 10.0
  ```
- Tampilan array `X_data` dan `y_data` sebagai hasil mapping dan normalisasi rating.
 
 
 
## Modeling and Results
 
### Content-Based Filtering
 
Pada pendekatan content-based filtering, sistem rekomendasi menghitung derajat kemiripan antar makanan menggunakan *cosine similarity* dari matriks yang dihasilkan di tahap Data Preparation. Fungsi rekomendasi menerima input berupa nama makanan dan mengembalikan daftar makanan dengan kemiripan tertinggi berdasarkan kategori.
 
Contoh fungsi rekomendasi:
 
```python
def rekomendasi_makanan(nama_makanan, sim_data=df_cosine, items=df_makanan_baru[['food_name', 'category']], top=5):
    # Mengambil indeks kemiripan
    idx_array = sim_data.loc[:, nama_makanan].to_numpy().argpartition(range(-1, -top, -1))
    rekomendasi = sim_data.columns[idx_array[-1:-(top+2):-1]]
    rekomendasi = rekomendasi.drop(nama_makanan, errors='ignore')
    return pd.DataFrame(rekomendasi).merge(items).head(top)
```
 
Contoh pemanggilan:
```python
print(df_makanan_baru[df_makanan_baru['food_name'] == 'banana chips'])
print(rekomendasi_makanan('banana chips'))
```
 
**Output:**
 
Data makanan dengan nama *banana chips*:
| id    | food_name    | category |
|-------|--------------|----------|
| 306.0 | banana chips | Snack    |
 
Rekomendasi untuk "banana chips":
| Food Name                                     | Category |
|-----------------------------------------------|----------|
| puffed rice                                   | Snack    |
| californian breakfast benedict                | Snack    |
| banana phirni tartlets with fresh strawberries | Snack    |
| baked raw banana samosa                       | Snack    |
| baked multigrain murukku                        | Snack    |
 
### Collaborative Filtering
 
Pada pendekatan collaborative filtering, model neural network dibangun dengan embedding layer untuk pengguna dan makanan. Model ini menghitung prediksi rating dengan mengoperasikan dot product antara embedding pengguna dan makanan, ditambah bias, dan diaktivasi dengan fungsi sigmoid sehingga output berada pada rentang [0,1].
 
Contoh struktur model:
```python
class RecommenderModel(tf.keras.Model):
    def __init__(self, total_users, total_foods, embed_size, **kwargs):
        super(RecommenderModel, self).__init__(**kwargs)
        self.user_embed = layers.Embedding(total_users, embed_size, 
                                           embeddings_initializer='he_normal',
                                           embeddings_regularizer=keras.regularizers.l2(1e-6))
        self.user_bias = layers.Embedding(total_users, 1)
        self.food_embed = layers.Embedding(total_foods, embed_size, 
                                           embeddings_initializer='he_normal',
                                           embeddings_regularizer=keras.regularizers.l2(1e-6))
        self.food_bias = layers.Embedding(total_foods, 1)
    
    def call(self, inputs):
        u_vec = self.user_embed(inputs[:, 0])
        u_bias = self.user_bias(inputs[:, 0])
        f_vec = self.food_embed(inputs[:, 1])
        f_bias = self.food_bias(inputs[:, 1])
        
        dot = tf.reduce_sum(u_vec * f_vec, axis=1, keepdims=True)
        x_out = dot + u_bias + f_bias
        return tf.nn.sigmoid(x_out)
```
 
Model dilatih selama 50 epoch dengan loss Binary Crossentropy dan optimizer Adam (learning rate 0.0001). Evaluasi dilakukan menggunakan metrik RMSE.
 
Setelah pelatihan, model digunakan untuk memprediksi rating dan menghasilkan rekomendasi bagi seorang sample user. Berikut adalah contoh output rekomendasi untuk *User_ID* 6:
 
**Makanan yang Pernah Dinilai Tinggi oleh User (User: 41)**
| Food Name                                | Category         |
|------------------------------------------|------------------|
| tricolour salad                          | Healthy_Food     |
| christmas chocolate fudge cookies        | Dessert          |
| spicy chicken curry                      | Indian          |
| ragi coconut ladoo (laddu)               | Dessert          |
 
**Top 10 Rekomendasi Makanan untuk User 41**
| Food Name                     | Category      |
|-------------------------------|---------------|
| sweet chilli almonds       | Snack       |
| lax seed and beetroot modak       | French        |
| sugar free modak              | Japanese      |
| crispy herb chicken           | Italian       |
| cajun spiced turkey wrapped with bacon          | Mexican      |
| japanese fish stew              | Japanese       |
| damdama fish curry                 | Indian       |
| whole wheat cake       | Healthy_Food       |
| lamb korma | Indian     |
| white chocolate and lemon pastry  | dessert |
 
---
 
## Evaluation
 
### Evaluasi Kinerja Sistem Rekomendasi Berbasis Konten (Content-Based Filtering)
 
Kinerja sistem rekomendasi yang mengadopsi pendekatan *Content-Based Filtering* dinilai menggunakan metrik **Precision**, yang esensial untuk mengukur proporsi akurasi rekomendasi yang disajikan kepada pengguna. Metrik Precision didefinisikan sebagai rasio antara jumlah rekomendasi yang benar-benar relevan (*True Positives*, TP) dengan total jumlah rekomendasi yang diberikan (*True Positives* + *False Positives*, FP). Berdasarkan hasil evaluasi yang dilakukan pada sampel data, diperoleh nilai Precision yang sempurna:
 
$$Precision = \frac{TP}{TP + FP} = \frac{5}{5+0} = 1$$
 
Pencapaian nilai Precision sebesar **1** (atau 100%) ini secara tegas mengindikasikan bahwa setiap rekomendasi yang dihasilkan oleh sistem berbasis konten adalah relevan dan sesuai dengan preferensi pengguna yang diharapkan. Hal ini menegaskan kemampuan sistem dalam memfilter dan menyajikan item yang benar-benar cocok berdasarkan karakteristik konten yang disukai pengguna.
 
### Evaluasi Kinerja Sistem Rekomendasi Berbasis Kolaboratif (Collaborative Filtering)
 
Model *Collaborative Filtering* dievaluasi secara kuantitatif dengan menggunakan metrik **Root Mean Squared Error (RMSE)**. RMSE merupakan indikator statistik yang mengukur besaran rata-rata perbedaan antara nilai prediksi *rating* yang dihasilkan oleh model dengan nilai *rating* aktual yang diberikan oleh pengguna. Metrik ini sangat relevan untuk sistem rekomendasi yang memprediksi nilai numerik seperti *rating*. Formula untuk menghitung RMSE adalah sebagai berikut:
 
$$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N}(y_i - \hat{y}_i)^2}$$
 
Di sini, $N$ merepresentasikan jumlah total pasangan *rating* yang dievaluasi, $y_i$ adalah nilai *rating* sesungguhnya yang diberikan oleh pengguna, dan $\hat{y}_i$ adalah nilai *rating* yang diprediksi oleh model. Nilai RMSE yang lebih rendah secara konsisten mengindikasikan bahwa model memiliki tingkat akurasi prediksi yang lebih tinggi dan kesalahan rata-rata yang lebih kecil, yang berarti prediksi *rating* model lebih mendekati *rating* aktual pengguna.
 
 
Berdasarkan hasil pelatihan selama 50 epoch, diperoleh nilai sebagai berikut:
 
- **RMSE pada data training (epoch terakhir):** 0.2595 
- **RMSE pada data validasi (epoch terakhir):** 0.3137  
 
 
Visualisasi grafik pelatihan secara komprehensif mengilustrasikan evolusi performa model sepanjang setiap *epoch* pelatihan, di mana sebuah **penurunan yang konsisten pada nilai *Root Mean Squared Error* (RMSE) teramati secara berkelanjutan**. Tren penurunan RMSE ini, baik pada data pelatihan (*training data*) maupun data validasi (*validation data*), secara definitif mengindikasikan bahwa **model berhasil melakukan proses pembelajaran yang efektif dari data yang diberikan**.
 
Pada titik akhir pelatihan, nilai RMSE yang teregistrasi pada *data training* menunjukkan tingkat kesalahan prediksi yang rendah, yang merefleksikan kemampuan model dalam memprediksi *rating* atau nilai numerik target dengan akurasi yang substansial. Meskipun demikian, adanya **disparitas kecil antara nilai RMSE pada *data training* dan *data validation***, di mana RMSE validasi sedikit lebih tinggi, merupakan **indikasi adanya potensi *overfitting* ringan**. Fenomena *overfitting* ini menunjukkan bahwa model mungkin telah terlalu menyesuaikan diri dengan pola spesifik pada *data training*, sehingga generalisasinya pada data yang belum pernah dilihat sebelumnya sedikit menurun, namun masih dalam batas yang dapat diterima dan tidak mengurangi efektivitas keseluruhan model secara signifikan.
 
 
## Kesimpulan dan Saran
 
* Sistem rekomendasi yang telah dikembangkan ini, dengan mengadopsi integrasi dua paradigma utama — yaitu *content-based filtering* dan *collaborative filtering* — secara efektif mendemonstrasikan kapabilitasnya dalam menyajikan rekomendasi makanan yang tidak hanya *personalized* tetapi juga sangat relevan dengan preferensi spesifik pengguna.
* Hasil evaluasi kinerja model menunjukkan bahwa pendekatan rekomendasi berbasis konten mencapai tingkat akurasi yang memuaskan berdasarkan metrik Precision, sementara itu, model *collaborative filtering* menghasilkan nilai *Root Mean Squared Error* (RMSE) yang rendah, secara definitif mengindikasikan kemampuan model untuk melakukan prediksi *rating* dengan tingkat presisi yang tinggi.
* Sebagai langkah strategis untuk pengembangan di masa mendatang, disarankan untuk menginvestigasi dan mengimplementasikan pendekatan *hybrid* yang secara sinergis menggabungkan kekuatan dari kedua metode tersebut. Tujuan dari eksplorasi ini adalah untuk lebih mengoptimalkan performa keseluruhan sistem rekomendasi, sekaligus secara signifikan meningkatkan pengalaman pengguna melalui saran yang lebih komprehensif dan akurat.
 
---
 
## Daftar Pustaka
 
[1] Muliadi, K. H., & Lestari, C. C. (2019). Rancang Bangun Sistem Rekomendasi Tempat Makan Menggunakan Algoritma Typicality Based Collaborative Filtering. Techno. Com, 18(4). https://doi.org/10.33633/tc.v18i4.2515
 
[2] Bahri, M. N. S., Jaya, I. P. Y. D., Dirgantoro, B., Ahmad, U. A., & Septiawan, R. R. (2021). Implementasi Sistem Rekomendasi Makanan pada Aplikasi EatAja Menggunakan Algoritma Collaborative Filtering. MULTINETICS, 7(2), 177-185. https://doi.org/10.32722/multinetics.v7i2.4062
 
[3] schemersays, "Food Recommendation System," Kaggle.com, 2022. https://www.kaggle.com/datasets/schemersays/food-recommendation-system
 
---
