# Tugas Klastering Twitter

|   |   |
|---|---|
|__NIM__| 20.01.53.0033 |
|__Nama__| Muhammad Falah Abdurrafi |
|__Progdi__| Teknik Informatika - S1 |
|__Mata Kuliah__| Text Mining |
|__Kelas__| A1 |
|__Dosen Pengampu__| Dr. Drs. ERI ZULIARSO, M.Kom. |
|   |   |

<br>

## :footprints: Tahapan Proses
1. Scrapping (SNScrape)
2. Preprocessing
3. Representasi Vektor
4. Klastering

<br>

## :pick: Scrapping
Pada tugas ini, proses scrapping data dari twitter akan menggunakan bantuan salah satu SNS (Social Networking Serivces) yaitu __SNScrape__. Detail pencarian yang ingin dilakukan diantaranya :
- Kata kunci pencarian = __pssi__
- Batas awal dan akhir dari tanggal tweet di-post = __1-16 Oktober 2022__
- Batas maksimum tweet yang dicari = __200 tweet__
- Nama file dari output pencarian yang berupa file JSON = __tweet.json__
- Bahasa yang digunakan oleh tweet = __Indonesia__

<br>

## :gear: Preprocessing
1. Case Folding
2. Stemming (PorterStemmer)
3. Filtering (Stopword Removal)

<br>

## :bar_chart: Representasi Vektor
Kata-kata yang sudah diperoleh perlu direpresentasikan dalam bentuk angka-angka vektor agar dapat dipahami oleh model NLP (Natural language Processing).
Terdapat dua metode yang sering digunakan, yaitu TF-IDF dan Bag of Words.

<dl>
  <dt>Bag of Words</dt>
  <dd>Metode ini merupakan metode yang sangat sederhana, hanya menghitung frekuensi kemunculan kata pada seluruh dokumen.</dd>
  
  <dt>TF-IDF (Term Frequency - Inverse Document Frequency)</dt>
  <dd>Dalam merepresentasikan kata sebagai vektor, metode ini akan mempertimbangkan apakah data tersebut relevan/informatif terhadap isi dokumen.</dd>
</dl>

<br>

## :traffic_light: Klastering (K-Means Clustering)
- K-Means Clustering termasuk algoritma __unsupervised learning__, yang mana label/kelompok data belum ditentukan di awal.
- Data dikelompokkan berdasarkan kedekatan jarak terhadap __Centroid__ (titik pusat) terdekatnya.
- Jarak data terhadap centroid dapat dihitung menggunakan __Euclidean Distance__.
- Setelah data dikelompokkan, centroid (titik pusat) akan diperbarui dan dikelompokkan kembali berdasarkan centroid yang baru. Iterasi ini terus dilakukan hingga pola yang didapat sama dengan pola sebelumnya.

<img src="./images/k-means-clustering.png" alt="K-Means Clustering" style="width:400px;"/><br>
(Gambar: <a href="https://medium.com/mlearning-ai/ml-k-means-clustering-5c11c1d2577b" target="_parent">https://medium.com/mlearning-ai/ml-k-means-clustering-5c11c1d2577b</a>)

<br>

## :traffic_light: Klastering (Hierarchical Clustering)
- Hierarchical Clustering termasuk algoritma __unsupervised learning__, yang mana label/kelompok data belum ditentukan di awal.
- Data yang dibagi menjadi cluster-cluster kecil akan digabungkan berulang kali ke dalam beberapa cluster, sampai terbentuk 1 kluster utuh. Proses penggabungan ini akan membentuk suatu __pohon hirarki__.
- Hirarki ini dapat di-visualisasikan menggunakan __Dendrogram__.

<br>

Secara umum, hierarchical clustering dibagi menjadi dua jenis yaitu agglomerative dan divisive.

<img src="./images/agglomerative-divisive.png" alt="Agglomerative & Divisive" style="width:400px;"/><br>
(Gambar: <a href="https://rpubs.com/inayatus/hierarchical-clustering" target="_parent">https://rpubs.com/inayatus/hierarchical-clustering</a>)

<ul>
    <li><b>Agglomerative</b> : memulai dari bawah ke atas (bottom up)</li>
    <li><b>Divisive</b> : memulai dari atas ke bawah (top down)</li>
</ul>

<br>

Proses penggabungan (linkage) cluster-cluster kecil menjadi satu dendrogram utuh dilakukan melalui beberapa pendekatan <b>Linkage Method</b>. Berikut ini linkage method yang sering digunakan :

<img src="./images/linkage-methods.png" alt="Linkage Methods" style="width:600px;"/><br>
(Gambar: <a href="https://rpubs.com/inayatus/hierarchical-clustering" target="_parent">https://rpubs.com/inayatus/hierarchical-clustering</a>)

<ul>
    <li><b>Centroid Linkage</b> : Mengukur jarak antar centroid pada dua cluster. Perhitungan centroid disini menggunakan rata-rata pada suatu variabel x. Dendrogram yang terbentuk akan berdasarkan cluster dengan jarak antar centroid paling kecil.</li>
    <br>
    <li><b>Single/Minimum Linkage</b> : Mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda (pairwise distances). Jarak paling kecil (minimum distance) akan menjadi ukuran (dis)similarity antar cluster. Dendrogram akan terbentuk dari cluster-cluster yang memiliki (dis)similarity paling kecil. Hal ini membuat dendrogram yang terbentuk menjadi lebih “loose” atau berdekatan antar clusternya.</li>
    <br>
    <li><b>Complete/Maximum Linkage</b> : Mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda (pairwise distances). Jarak paling tinggi (maximum distance) akan menjadi ukuran (dis)similarity antar cluster. Kemudian, dendrogram akan terbentuk dari cluster-cluster yang memiliki (dis)similarity paling kecil. Hal ini membuat dendrogram yang terbentuk menjadi lebih terpisah antar clusternya (terbentuk cluster yang “compact”).</li>
    <br>
    <li><b>Average Linkage</b> : Mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda (pairwise distances). Kemudian, dihitung rata-rata jarak dari pairwise distance tersebut dan nilai tersebut akan menjadi ukuran (dis)similarity antar cluster. Dendrogram akan terbentuk dari cluster-cluster yang memiliki (dis)similarity paling kecil. Umumnya metode ini akan menghasilkan cluster yang tidak terlalu “loose” maupun “compact”</li>
    <br>
    <li><b>Ward’s minimum Variance</b> : Pada metode ini, di tiap iterasinya akan dibentuk cluster-cluster yang kemudian dihitung nilai within sum of square tiap cluster (WSS). WSS dapat diartikan sebagai jumlah dari jarak tiap observasi ke nilai tengah cluster. Cluster-cluster yang menghasilkan within sum of square terkecil akan diambil kemudian digabungkan hingga membentuk satu dendrogram utuh.</li>
</ul>