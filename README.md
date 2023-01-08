# SIG_TEORI_TGS_23
 Handling Invalid Geometries
Langkah Kerja Peta 9: Handling Invalid Geometries (QGIS3)

1. Telusuri file India-States.zip yang diunduh di Peramban QGIS. Perluas dan seret file India-States.shp ke kanvas peta.

2. Anda akan melihat layer India-States baru dimuat di panel Layers. Pergi ke Memproses ‣ Toolbox.

3. Kami akan mencoba menjalankan algoritme pemrosesan pada lapisan input untuk mendemonstrasikan bagaimana geometri yang tidak valid dapat menyebabkan masalah selama operasi geoproses. Cari dan temukan Kartografi ‣ Algoritma pewarnaan topologi. Klik dua kali untuk meluncurkannya.

4. Dalam dialog pewarnaan Topologi, pilih India-States sebagai lapisan Input. Simpan semua parameter lain ke default dan klik Jalankan.

Catatan : Algoritma pewarnaan topologi mengimplementasikan algoritma untuk mewarnai peta sehingga tidak ada poligon yang berdekatan memiliki warna yang sama. Ini adalah teknik kartografi yang berguna dan Teorema Empat Warna menyatakan bahwa 4 warna cukup untuk mencapai hasil ini. Ada versi teori graf dari torem ini yang disebut teorema Lima warna. Implementasi algoritma QGIS didasarkan pada grafik sehingga dalam praktiknya Anda akan melihat bahwa lapisan poligon kompleks seperti ini akan membutuhkan hingga 5 warna.

5. Saat algoritme berjalan, Anda akan melihat peringatan ditampilkan di tab Log. 1 fitur di lapisan input memiliki geometri yang tidak valid dan dilewati selama pemrosesan. Pengaturan default untuk menangani geometri yang tidak valid di Kotak Alat Pemrosesan terletak di Pengaturan ‣ Opsi ‣ Pemrosesan ‣ Umum ‣ Pemfilteran fitur yang tidak valid dan diatur ke Lewati (abaikan) fitur dengan geometri yang tidak valid. Ini adalah pengaturan default yang bagus, tetapi jika masukan Anda besar, Anda mungkin melewatkan peringatan ini dan mungkin tidak mengetahui bahwa fitur masukan telah dilewati. Anda mungkin ingin mengubah nilainya menjadi Hentikan eksekusi algoritme saat geometri tidak valid.

6. Kembali ke jendela utama QGIS, Anda akan melihat layer baru Berwarna ditambahkan ke panel Layers. Perhatikan bahwa layer baru tidak memiliki status yang geometrinya tidak valid. Kami sekarang tahu bahwa poligon keadaan tertentu ini memiliki geometri yang tidak valid tetapi kami tidak tahu apa penyebabnya. Kita dapat dengan mudah mengetahuinya. Cari dan temukan geometri Vektor ‣ Periksa algoritme validitas.

7. Dalam dialog Check Validity, pilih India-States sebagai Input layer. Pilih GEOS sebagai Metode. Klik Jalankan.

8. Saat algoritme selesai diproses, Anda akan melihat 3 lapisan baru di panel Lapisan - Keluaran valid, Keluaran tidak valid, dan Keluaran kesalahan. Keluaran Error lapisan berisi lokasi dan deskripsi kesalahan geometri. Klik kanan dan pilih Buka Tabel Atribut.

Catatan : Dokumentasi QGIS memiliki artikel terperinci tentang Jenis pesan kesalahan dan artinya yang menjelaskan penyebab semua kesalahan.

9. Anda akan melihat bahwa pesan kesalahannya adalah Ring self-intersection. Pilih baris dan klik tombol Zoom map to selected features. Saat memperbesar, Anda akan melihat akar penyebab galat geometri.

10. QGIS hadir dengan algoritme bawaan untuk memperbaiki kesalahan geometri secara otomatis. Cari dan temukan geometri Vektor ‣ Perbaiki algoritma geometri. Klik dua kali untuk menjalankannya.

11. Dalam dialog Fix Geometries, pilih India-States sebagai Input layer dan klik Run.

12. Sebuah layer baru Fixed Geometries akan ditambahkan ke panel Layers. Pada titik ini, kesalahan geometri telah diperbaiki dan Anda dapat menjalankan algoritme pemrosesan apa pun pada lapisan ini tanpa masalah. Tetapi kita dapat melihat bahwa masih ada celah antara poligon yang berdekatan yang tidak terduga dan dapat menyebabkan kesalahan topologi di kemudian hari. Kami juga dapat memperbaikinya dengan mengedit poligon. Klik tombol Toggle Editing di Digitizing Toolbar. Pilih Vertex Tool dan dari drop-down pilih Vertex Tool (Current Layer).

13. Saat alat vertex aktif, klik pada vertex untuk memilihnya. Anda dapat menekan tombol Delete untuk menghapus simpul atau menyeretnya untuk memindahkannya. Anda dapat memindahkan simpul sehingga tepi poligon sekarang menyentuh poligon yang berdekatan.

14. Setelah selesai, klik tombol Toggle Editing lagi dan klik Save.

15. Mari kita jalankan lagi algoritma Kartografi ‣ Pewarnaan topologi.

16. Dalam dialog Topological Coloring, pastikan Anda memilih Fixed Geometries sebagai Input layer. Klik Jalankan.

17. Anda akan melihat algoritme berjalan tanpa kesalahan dan lapisan baru Berwarna akan ditambahkan ke panel Lapisan. Perhatikan bahwa algoritme tidak mewarnai layer dengan sendirinya, tetapi bekerja dengan menambahkan kolom baru bernama color_id ke setiap poligon yang dapat digunakan untuk menetapkan warna unik yang berbeda dari poligon yang berdekatan. Pilih layer Colored dan klik tombol Open the Layer Styling Panel.

18. Pilih Penyaji yang dikategorikan dan kolom color_id sebagai Nilai. Klik Klasifikasikan. Anda sekarang akan melihat peta berwarna sehingga poligon yang berdekatan memiliki warna yang berbeda.
