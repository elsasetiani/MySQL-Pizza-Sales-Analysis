# 🍕 MySQL's Project: Pizza Sales Analysis

Proyek ini menampilkan analisis data penjualan menggunakan SQL untuk mengidentifikasi tren penjualan, kinerja produk, dan metrik bisnis utama pada sebuah toko pizza.
---

## Tujuan
- Menganalisis tren pendapatan dan penjualan.
- Mengidentifikasi pizza dengan kinerja terbaik dan yang berkinerja buruk.
- Mengekstrak indikator kinerja utama (KPI).
- Mendukung rekomendasi bisnis berdasarkan data.

---

## Deskripsi Dataset
- Baris: 48,620
- Periode: Sepanjang tahun 2015
- Bidang: `pizza_id`, `order_id`, `pizza_name_id`, `quantity`, `order_date`, `order_time`, `unit_price`, `total_price`, `pizza_category`, `pizza_size`, `pizza_ingredients`, `pizza_name`

---

## Alat

- MySQL Workbench 8.0 CE
- Excel (opsional untuk data cleaning)

---

## A. Indikator Kinerja Utama (KPI)

### 1. Total Revenue

### Input
```sql
SELECT SUM(total_price) AS Total_Revenue
FROM project_pizzasales;
```
### Output 
| Total_Revenue | 
|---------------|        
| 817860.05    |
### Insight
Total pendapatan dari seluruh penjualan pizza mencapai $8.17 juta, mencerminkan performa penjualan yang sangat baik secara keseluruhan.

---

### 2. Average Order Value

### Input
```sql 
SELECT (SUM(total_price) / COUNT(DISTINC order_id)) AS Avg_Order_Value
FROM project_pizzasales;
```
### Output 
| Avg_Order_Value | 
|-----------------|        
| 38.307262       |
### Insight
Rata-rata pelanggan membelanjakan sekitar $38.31 per pesanan, menunjukkan nilai transaksi yang cukup tinggi per pembelian.

---

### 3. Total Pizza Solds

### Input
```sql 
SELECT SUM(quantity) AS Total_Solds
FROM project_pizzasales;
```
### Output 
| Total_Solds | 
|-------------|        
| 49574       |
### Insight
Sebanyak 49,574 pizza telah terjual, membuktikan adanya permintaan konsisten terhadap produk.

---

### 4. Total Orders

### Input
```sql 
SELECT COUNT(DISTINCT order_id) AS Total_Orders 
FROM project_pizzasales;
```
### Output 
| Total_Orders | 
|--------------|        
| 21350        |
###  Insight
Dengan 21,350 pesanan unik, restoran menunjukkan volume transaksi yang stabil dalam periode waktu tertentu.

---

### 5. Average Pizzas per Order

### Input
```sql 
SELECT SUM(quantity) / COUNT(DISTINCT order_id) AS Avg_Pizza_per_Order
FROM project_pizzasales;
```
### Output 
| Avg_Pizza_per_Order | 
|---------------------|        
| 2.3220              |
### Insight
Rata-rata pembeli memesan sekitar 2.32 pizza per pesanan, menandakan bahwa banyak pelanggan membeli lebih dari satu pizza dalam sekali order—indikasi kemungkinan pembelian untuk keluarga atau kelompok.

---

## B. Daily Trend for Total Orders

### Input
```sql 
SELECT DAYNAME(order_date) AS order_day, COUNT(DISTINCT order_id) AS Total_Orders
FROM project_pizzasales
GROUP BY DAYNAME(order_date);
```
### Output 
| Order_day        | Total_Orders | 
|------------------|--------------|
| Friday           | 3538         | 
| Monday           | 2794         | 
| Saturday         | 3158         | 
| Sunday           | 2624         | 
| Thursday         | 3239         |
| Tuesday          | 2973         | 
| Wednesday        | 3024         |
### Insight
- Puncak tertinggi pesanan terjadi pada hari Jumat (3,538 orders), diikuti oleh Kamis dan Sabtu.
- Hari dengan pesanan terendah adalah Minggu (2,624 orders), sedikit lebih rendah dari hari Senin.
- Tren menunjukkan bahwa pesanan cenderung meningkat menjelang akhir minggu, kemungkinan karena orang-orang mulai bersantai dan memesan makanan dari luar.
- Hari kerja (Senin–Kamis) tetap menunjukkan volume pesanan yang stabil, terutama Rabu dan Kamis.
### Rekomendasi
#### 1. Promosi Khusus Jumat & Sabtu:
Manfaatkan volume tinggi di hari tersebut dengan bundle deals atau limited time offers untuk meningkatkan pendapatan.
#### 2. Tingkatkan Penjualan di Hari Minggu:
Buat "Sunday Family Pizza Pack" atau promo "Buy 1 Get 1" khusus hari Minggu untuk menarik pelanggan di hari dengan trafik terendah.
#### 3. Optimalisasi Operasional:
Alokasikan lebih banyak staf dan bahan baku pada hari-hari sibuk seperti Jumat dan Sabtu agar pelayanan tetap optimal dan cepat.
#### 4. Analisis Segmentasi Pelanggan:
Pelajari perilaku pelanggan berdasarkan hari untuk personalisasi marketing, misalnya kirimkan voucher lewat email/SMS pada Kamis malam menjelang hari dengan order tinggi.

---

## C. Monthly Trend for Total Orders
### Input
```sql 
SELECT MONTHNAME(order_date) AS Month_Name, COUNT(DISTINCT order_id) AS Total_Orders
FROM project_pizzasales
GROUP BY MONTHNAME(order_date) DESC;
```
### Output 
| Month_Name | Total_Orders |
|------------|--------------|
| July       | 1935         |
| May        | 1853         |
| January    | 1845         |
| August     | 1841         |
| March      | 1840         |
| April      | 1799         |
| November   | 1792         |
| June       | 1773         |
| February   | 1685         |
| December   | 1680         |
| September  | 1661         |
| October    | 1646         |
### Insight
- Puncak pemesanan terjadi di bulan Juli dengan 1.935 pesanan, diikuti oleh Mei, Januari, dan Agustus, yang semuanya mencatatkan lebih dari 1.840 pesanan.
- Musim awal tahun (Q1)—Januari hingga Maret—menunjukkan performa cukup kuat, menandakan permintaan yang tetap stabil setelah libur panjang akhir tahun.
- Bulan dengan pesanan paling rendah adalah Oktober (1.646), sedikit di bawah September dan Desember.
- Performa kuartal 3 (Juli–September) relatif fluktuatif: Juli sangat tinggi, namun turun cukup tajam di September.
### Rekomendasi
#### 1. Perkuat strategi promosi di kuartal rendah (September & Oktober):
Tawarkan diskon spesial, paket bundling, atau kampanye musiman untuk meningkatkan penjualan.
#### 2. Manfaatkan momentum tinggi pada bulan Juli dan Mei:
Jalankan promosi besar seperti “Mid-Year Sale” atau “Summer Pizza Fest” untuk mendongkrak repeat order.
#### 3. Analisis lebih dalam penyebab penurunan di bulan-bulan tertentu, seperti Oktober:
Apakah ada faktor eksternal seperti cuaca, libur nasional, kompetitor.
#### 4. Rancang kampanye tahunan berbasis tren bulanan:
Dengan memanfaatkan bulan-bulan dengan performa tinggi sebagai "anchor point", kampanye tahunan bisa disusun lebih strategis dan efektif.

---

##  D. % of Sales by Pizza Category
### Input
```sql 
SELECT pizza_category, 
CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue, 
CAST((SUM(total_price) * 100) / (SELECT SUM(total_price) FROM project_pizzasales) AS DECIMAL(10,2)) AS PCT
FROM project_pizzasales
GROUP BY pizza_category;
```
### Output 
| pizza_category | Total_Revenue | PCT   |
|----------------|---------------|-------|
| Classic        | 220053.10     | 26.91 |
| Veggie         | 193690.45     | 23.68 |
| Supreme        | 208197.00     | 25.46 |
| Chicken        | 195919.50     | 23.96 |
### Insight
- Kategori "Classic" menghasilkan pendapatan tertinggi dengan kontribusi 26.91% dari total penjualan, menunjukkan popularitasnya yang dominan di antara pelanggan.
- Kategori "Supreme" menyusul di posisi kedua (25.46%), menunjukkan permintaan yang cukup tinggi terhadap varian pizza dengan topping komplit.
- Performa "Veggie" dan "Chicken" seimbang, masing-masing berkontribusi sekitar 23–24%, menandakan variasi preferensi pelanggan yang cukup merata terhadap opsi non-daging dan berbasis ayam.
- Perbedaan antar kategori relatif kecil (kurang dari 4%), yang berarti semua kategori memiliki permintaan yang cukup stabil dan tidak terlalu timpang.
### Rekomendasi
#### 1. Pertahankan stok dan promosi kategori "Classic" dan "Supreme", karena dua kategori ini menyumbang lebih dari 50% total pendapatan.
#### 2. Optimalkan penjualan “Veggie” dan “Chicken” dengan strategi upselling seperti:
Menawarkan add-on atau topping spesial.
#### 3. Membuat paket hemat dengan minuman/dessert.
Lakukan analisis lebih lanjut pada varian pizza dalam setiap kategori untuk mengidentifikasi produk dengan performa terbaik dan terburuk sebagai dasar pengambilan keputusan bisnis (misalnya: discontinue varian tidak laku atau promosi varian favorit).
#### 4. Gunakan data ini untuk menyusun strategi bundling:
Kombinasi satu pizza classic + satu veggie bisa jadi pilihan bundling menarik untuk menjangkau preferensi pelanggan yang berbeda.

---

## E. % of Sales by Pizza Size
### Input
```sql 
SELECT pizza_size, 
CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue, 
CAST((SUM(total_price) * 100) / (SELECT SUM(total_price) FROM project_pizzasales) AS DECIMAL(10,2)) AS PCT
FROM project_pizzasales
GROUP BY pizza_size 
ORDER BY PCT DESC;
```
### Output
| pizza_size | Total_revenue | PCT   |
|------------|---------------|-------|
| L          | 375318.70     | 45.89 |
| M          | 249382.25     | 30.49 |
| S          | 178076.50     | 21.77 |
| XL         | 14076.00      | .1.72 |
| XLL        | 1006.60       | 0.12  |
### Insight
- Ukuran L (Large) mendominasi penjualan dengan kontribusi hampir 46% dari total pendapatan, menjadikannya ukuran pizza paling populer di kalangan pelanggan.
- Ukuran M (Medium) juga sangat populer, menyumbang sekitar 30.5% dari total penjualan.
- Ukuran S (Small) masih cukup diminati, menyumbang sekitar 21.77%, tetapi jauh tertinggal dibanding ukuran L dan M.
- Ukuran XL dan XLL hampir tidak berkontribusi, masing-masing hanya 1.72% dan 0.12%, menunjukkan permintaan yang sangat rendah untuk ukuran-ukuran besar ini.
### Rekomendasi
#### 1. Fokus pada stok dan promosi untuk ukuran L dan M, karena keduanya menyumbang lebih dari 75% total pendapatan—pastikan bahan baku, harga, dan ketersediaannya stabil.
#### 2. Tinjau kembali efektivitas produk ukuran XL dan XLL:
- Evaluasi apakah masih layak dipertahankan di menu atau perlu dikemas ulang secara promosi
- Jika tetap ingin ditawarkan, promosikan dalam bentuk paket untuk berbagi atau event khusus.
#### 3. Kembangkan strategi upselling dari S ke M atau M ke L:
- Tawarkan upgrade ukuran dengan harga diskon.
- Gunakan kalimat seperti "Hanya tambah Rp10.000 untuk ukuran lebih besar!"
#### 4. Gunakan preferensi ukuran untuk personalisasi marketing:
Kirim promo ukuran L ke pelanggan yang sering beli ukuran L sebelumnya.

---

## F. Total Pizzas by Pizza Category
### Input
```sql 
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM project_pizzasales
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
### Output
| pizza_category | Total_Quantity_Sold | 
|----------------|---------------------|
| Classic        | 14888               | 
| Veggie         | 11987               | 
| Supreme        | 11649               |
| Chicken        | 11050               |
### Insight
- Kategori "Classic" menjadi yang paling laris secara kuantitas, dengan total lebih dari 14.800 pizza terjual, menandakan preferensi kuat pelanggan terhadap varian klasik.
- Kategori "Veggie", "Supreme", dan "Chicken" memiliki selisih kuantitas yang cukup kecil satu sama lain, menandakan permintaan yang relatif seimbang di luar kategori utama.
- Pola ini selaras dengan data revenue sebelumnya, menunjukkan bahwa volume penjualan dan nilai penjualan berjalan seiring.
### Rekomendasi
#### 1. Pertahankan ketersediaan dan variasi pada kategori Classic, karena ini adalah tulang punggung penjualan dalam hal kuantitas maupun pendapatan.
#### 2. Promosikan kategori dengan performa kuantitas menengah seperti Chicken dan Supreme, misalnya:
- Paket bundling “2 Supreme + 1 Veggie”
- Diskon pembelian lebih dari 2 pizza dalam kategori tersebut.
#### 3. Luncurkan kampanye tematik berdasarkan kategori populer:
Misal, "Classic Week" dengan diskon atau topping ekstra gratis bisa mendorong pembelian lebih tinggi.

---

## G. Top 5 Pizzas by Total Revenue
### Input
```sql 
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
LIMIT 5;
```
### Output
| pizza_name                    | Total_Revenue | 
|-------------------------------|---------------|
| The Thai Chicken Pizza        | 43434.25      | 
| The Berbecue Chicken Pizza    | 42785.50      | 
| The California Chicken Pizza  | 41409.50      |
| The Classic Deluxe Pizza      | 38180.50      |
| The Spicy Italian Pizza       | 34831.25      |
### Insight
- Tiga dari lima pizza dengan revenue tertinggi adalah varian berbasis chicken, menunjukkan preferensi pelanggan yang kuat terhadap menu berbahan dasar ayam.
- "The Thai Chicken Pizza" menduduki peringkat pertama dengan total pendapatan lebih dari $43.434.25 menjadikannya menu premium dengan performa tinggi.
- "The Classic Deluxe" dan "Spicy Italian" juga masuk 5 besar, menandakan kombinasi topping klasik dan cita rasa kuat masih sangat digemari.
### Rekomendasi
#### 1. Fokuskan promosi pada lima pizza teratas ini dengan strategi seperti:
- Paket combo
- Program loyalitas untuk pembelian ulang
- “Best Seller” badge di menu
#### 2. Perkuat branding untuk varian chicken, karena performanya konsisten tinggi secara revenue dan quantity.
#### 3. Lakukan analisis harga vs volume penjualan, terutama pada Thai Chicken Pizza—jika harganya premium tapi tetap laku keras, strategi harga premium bisa diterapkan ke varian lain dengan konsep serupa.
#### 4. Gunakan top 5 ini sebagai dasar pengembangan varian baru:
Contoh: pengembangan “Spicy Chicken Thai Pizza” yang menggabungkan elemen populer dari varian top.
#### 5. Tingkatkan eksposur di media sosial dan promosi aplikasi, terutama pada jam sibuk dan akhir pekan, menggunakan visual dari pizza-pizza ini sebagai ikon utama.

---

## H. Bottom 5 Pizzas by Total Revenue
### Input
```sql 
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
LIMIT 5;
```
### Output
| pizza_name                    | Total_Revenue | 
|-------------------------------|---------------|
| Double Mushroom Truffle Pizza | 265.00        | 
| Classic Pepperoni Pizza       | 7486.50       | 
| Spicy Veggie Lovers Pizza     | 11048.00      |
| The Brie Carre Pizza          | 11588.50      |
| The Green Garden  Pizza       | 13955.75      |
### Insight
- "Double Mushroom Truffle Pizza" memiliki performa yang sangat rendah dengan total pendapatan hanya $265.00, terpaut sangat jauh dari pizza lain — ini bisa jadi karena harga tinggi, keterbatasan promosi, atau kurangnya minat pasar.
- Varian seperti Spicy Veggie Lovers dan The Green Garden Pizza menunjukkan bahwa beberapa menu veggie atau eksperimental tidak sepopuler varian chicken dan classic.
- "Classic Pepperoni Pizza" tampil mengejutkan di peringkat bawah, padahal secara umum pepperoni biasanya populer—mungkin terjadi karena:
- Nama yang terlalu umum (kurang menarik),
- Terlalu banyak pesaing internal (dengan nama lebih "menjual").
### Rekomendasi
#### 1. Evaluasi kembali keberadaan menu "Double Mushroom Truffle Pizza":
- Jika bahan bakunya mahal, pertimbangkan untuk menghapus dari menu atau menawarkan sebagai seasonal item.
- Jika tetap ingin dipertahankan, perlu rebranding atau promosi agresif untuk meningkatkan awareness.
#### 2. Tingkatkan visibilitas pizza-pizza dengan performa rendah:
- Letakkan di bagian depan katalog/menu
- Buat promosi bundle (contoh: “Beli Classic, Gratis Green Garden”)
#### 3. Lakukan survei pelanggan untuk memahami alasan rendahnya minat:
- Apakah karena rasa, harga, nama, atau faktor lain?
- Feedback ini bisa digunakan untuk modifikasi resep atau nama produk.
#### 4. Kaji ulang strategi penamaan produk:
Nama seperti "The Brie Carre Pizza" dan "Green Garden Pizza" mungkin kurang menggugah minat atau tidak cukup menjelaskan rasa/komposisinya.
#### 5. Pertimbangkan positioning ulang:
- Jadikan sebagai opsi eksklusif atau “chef recommendation” agar terkesan lebih spesial.
- Sertakan deskripsi menarik pada menu agar pelanggan tertarik mencoba.

---

## I. Top 5 Pizzas by Quantity Sold
```sql 
SELECT pizza_name, SUM(quantity) AS Total_Quantit
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC
LIMIT 5;
```
### Output
| pizza_name                 | Total_Quantity | 
|----------------------------|----------------|
| The Classic Deluxe Pizza   | 2453           | 
| The Berbecue Chicken Pizza | 2433           | 
| The Hawaiian Pizza         | 2422           |
| The Pepperoni Pizza        | 2419           |
| The Thai Chicken Pizza     | 2371           |
### Insight                                                 
- The Classic Deluxe Pizza menjadi menu dengan penjualan tertinggi secara kuantitas, menunjukkan daya tarik luas dan mungkin menjadi pilihan default pelanggan.
- Varian chicken seperti Barbecue Chicken dan Thai Chicken Pizza juga tampil dominan, menandakan preferensi tinggi terhadap topping ayam.
- The Hawaiian Pizza dan Pepperoni Pizza masih kuat dalam penjualan, membuktikan bahwa topping klasik tetap memiliki tempat di hati konsumen.
- Perbedaan kuantitas antar posisi sangat tipis, menunjukkan bahwa lima menu teratas ini bersaing ketat dan semuanya berkontribusi besar terhadap total volume penjualan.
### Rekomendasi 
#### 1. Pastikan pasokan bahan baku untuk lima varian ini selalu tersedia, karena mereka menjadi penopang utama dari sisi volume.
#### 2. Gunakan menu-menu ini sebagai andalan dalam promosi pemasaran, seperti:
- Paket keluarga
- Diskon bundle
- Loyalty reward
#### 3. Tingkatkan visualisasi menu di platform digital (GoFood, GrabFood, dll) dengan menampilkan 5 besar ini sebagai "Most Ordered Pizzas" atau "Customer Favorites".
#### 4. Lakukan eksperimen upsell dan cross-sell:
Contoh: pelanggan yang membeli Classic Deluxe ditawarkan upgrade ukuran atau tambahan minuman.
#### 5. Perluas varian turunan dari menu terlaris:
Misalnya: The Spicy Classic Deluxe atau The Creamy Hawaiian untuk memperkaya penawaran tanpa kehilangan basis pelanggan.

---

## J. Bottom 5 Pizzas by Quantity Sold
```sql 
SELECT pizza_name, SUM(quantity) AS Total_Quantity
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Quantity ASC
LIMIT 5;
```
### Output
| pizza_name                    | Total_Quantity | 
|-------------------------------|----------------|
| Double Mushroom Truffle Pizza | 19             | 
| The Brie Carre Pizza          | 490            | 
| Classic Pepperoni Pizza       | 541            |
| Spicy Veggie Lovers Pizza     | 797            |
| The Mediterranean Pizza       | 934            |
### Insight
- Double Mushroom Truffle Pizza sangat jauh tertinggal dibandingkan lainnya, hanya terjual 19 unit, menunjukkan adanya masalah serius dalam penerimaan pasar.
- Menu seperti The Brie Carre dan Spicy Veggie Lovers juga masuk ke dalam kategori rendah penjualan, yang bisa jadi karena tidak familier bagi pelanggan dan terlalu eksperimental atau segmentasi pasar terlalu sempit.
- Classic Pepperoni Pizza, meskipun populer secara global, menunjukkan performa rendah secara kuantitas di toko ini — ini mungkin disebabkan oleh persaingan internal, penamaan produk yang kurang menarik, atau kurang promosi.
- The Mediterranean Pizza berada di posisi kelima terbawah, menunjukkan bahwa varian non-mainstream mungkin kurang diminati oleh target pasar saat ini.
### Rekomendasi
#### 1. Evaluasi menu yang sangat rendah penjualannya (misalnya Double Mushroom Truffle Pizza) untuk:
- Dihapus dari menu reguler, dijadikan seasonal item, atau ditawarkan sebagai limited edition dengan nilai eksklusif.
#### 2. Lakukan rebranding atau penyesuaian nama menu agar lebih mudah dikenali dan menarik secara emosional. Contoh: “The Brie Carre Pizza” → “Creamy Brie Delight”.
#### 3. Promosikan menu-menu ini secara khusus:
- Campaign “Discover Hidden Gems” untuk menarik perhatian pada menu kurang populer.
- Diskon spesial atau bundling dengan menu populer.
#### 4. Tingkatkan edukasi pelanggan melalui deskripsi menu yang menarik, misalnya menyertakan info asal usul atau bahan-bahan spesial yang digunakan.
#### 5. Lakukan A/B testing dengan desain ulang foto produk, penempatan dalam menu, dan copywriting promosi untuk mengetahui apakah perubahan visual dan kata-kata bisa meningkatkan penjualan.

---

## K. Top 5 Pizzas by Total Orders
```sql 
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```
### Output
| pizza_name                 | Total_Orders | 
|----------------------------|--------------|
| The Classic Deluxe Pizza   | 2329         | 
| The Hawaiian Pizza         | 2280         | 
| The Pepperoni Pizza        | 2278         |
| The Berbecue Chicken Pizza | 2273         |
| The Thai Chicken Pizza     | 2225         |
### Insight
- The Classic Deluxe Pizza adalah menu dengan jumlah pesanan terbanyak, menegaskan statusnya sebagai pilihan utama pelanggan.
- Posisi lima besar didominasi oleh varian pizza dengan cita rasa klasik dan familiar, seperti Hawaiian, Pepperoni, dan BBQ Chicken.
- Selisih pesanan antar peringkat sangat kecil (hanya 50 order), menunjukkan bahwa kelima menu ini sangat kompetitif dan sama-sama disukai pelanggan.
- Konsistensi menu yang sering muncul di berbagai metrik (Total Orders, Quantity, Revenue) memperlihatkan bahwa kelima pizza ini adalah menu andalan toko.
### Rekomendasi
#### 1. Fokus pada promosi menu-menu ini sebagai Signature Dishes, karena terbukti paling sering dipesan dan mudah dikenali oleh pelanggan baru maupun lama.
#### 2. Optimalkan stok dan bahan baku untuk kelima varian ini agar tidak terjadi kekurangan saat jam ramai.
#### 3. Gunakan data ini untuk merancang paket kombo atau bundle:
Contoh: “Top 5 Favorite Box” atau “Most Loved Combo”.
#### 4. Highlight kelima menu ini di media sosial atau aplikasi pemesanan makanan, dengan label seperti:
⭐ Best Seller
🔥 Customer Favorite
💡 Reorder Favorite
#### 5. Pertahankan kualitas dan konsistensi rasa dari kelima menu ini, karena mereka merupakan pendorong utama retensi dan loyalitas pelanggan.

---

## K. Bottom 5 Pizzas by Total Orders
```sql 
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM project_pizzasales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
```
### Output
| pizza_name                    | Total_Orders | 
|-------------------------------|--------------|
| Double Mushroom Truffle Pizza | 19           | 
| The Brie Carre Pizza          | 480          | 
| Classic Pepperoni Pizza       | 522          |
| Spicy Veggie Lovers Pizza     | 773          |
| The Mediterranean Pizza       | 912          |
### Insight
- Double Mushroom Truffle Pizza sangat jarang dipesan dengan hanya 19 order, menunjukkan ketertarikan pelanggan yang sangat rendah.
- Menu-menu lainnya juga menunjukkan performa pesanan yang jauh di bawah rata-rata, sebagian besar tidak mencapai 1.000 order.
- Classic Pepperoni Pizza, meskipun secara global populer, justru memiliki performa rendah dalam jumlah pesanan, yang bisa menunjukkan kurangnya visibilitas atau daya tarik dalam konteks menu lokal.
- Terdapat korelasi kuat antara pizza-pizza ini dengan hasil sebelumnya (rendah pada total quantity dan revenue), memperkuat bukti bahwa mereka tidak menjadi pilihan utama pelanggan.
### Rekomendasi
#### 1. Lakukan audit terhadap setiap menu yang berada di posisi terbawah, khususnya:
Rasa, Harga, Visual di katalog/menu, dan penempatan dalam daftar menu digital/cetak.
#### 2. Pertimbangkan untuk menghapus atau mengganti Double Mushroom Truffle Pizza, kecuali memiliki nilai branding khusus (misalnya premium/seasonal).
#### 3. Lakukan A/B testing terhadap deskripsi dan harga menu, untuk melihat apakah penyesuaian bisa meningkatkan daya tarik.
#### 4. Tingkatkan promosi atau edukasi pelanggan terkait menu-menu ini, misalnya dengan mencoba:
Label “Hidden Gem”,
Diskon terbatas,
Paket uji coba (“Try Something New” combo).
#### 5. Jika performa tetap rendah setelah optimasi, gunakan data ini sebagai dasar untuk menyederhanakan menu dan memfokuskan produksi hanya pada varian dengan performa terbaik.


















