Project
Diberikan suatu data penjualan perbulan dalam setahun yang masing-masing disimpan dalam file .CSV, sehingga terdapat 12 file .CSV (File sdh disediakan dan dpt di download dalam bentuk .ZIP).

Untuk memudahkan analisis, maka lakukan merge ke-12 file tersebut ke dalam 1 file bernama dataPenjualanSetahun.csv. 
Hapus data yang mengandung nilai Nan.
Konversikan data sesuai tipenya; misal: Quantity dan Harga adalah tipe numerik. Tentu saja sebelum mengonversi, harus dilihat dulu tipe data masing-masing kolom nya.
Tambahkan satu kolom bernama "Month" yg bertipe numerik dari kolom "Order Date", dengan perintah:
       data['Month'] = all_data['Order Date'].str[0:2]
       data['Month'] = all_data['Month'].astype('int32')

Berikan penjelasan mengenai kode tersebut, mengapa bisa menambahkan 1 kolom bernama "Month" dan sesuai dengan bulan pada "Order Date". Penjelasan diberikan sebagai komentar di dalam program.

Tambahkan satu kolom lagi "City" untuk pemrosesan lebih lanjut dengan perintah:      
       def get_city(address):
             return address.split(",")[1].strip(" ")
       def get_state(address):
            return address.split(",")[2].split(" ")[1]
       data['City'] = data['Purchase Address'].apply(lambda x: f"{get_city(x)}  ({get_state(x)})")

Berikan penjelasan mengenai kode tersebut, mengapa bisa menambahkan 1 kolom bernama "City" dan sesuai dengan bulan pada " Purchase Address". Penjelasan diberikan sebagai komentar di dalam program.

Visualisasikan data penjualan berdasarkan bulan dengan bar plot. Kira2 hasilnya seperti ini:
satu


Visualisasi data penjualan berdasarkan kota dengan bar plot. Kira2 hasilnya seperti ini:
penjualan kota

Visualisasi produk yang paling laris terjual dengan cara menjumlahkan data "Quantity Ordered" yang kemudian dikelompokkan berdasarkan nama produknya. Kira2 hasilnya seperti ini:
bar plot 2

Overlaying-chart bisa menjadi solusi untuk produk yang paling laris terjual. Overlaying-chart dapat diterapkan dengan memadukan barplot dengan lineplot. Barplot untuk melihat jumlah "Quantity Ordered" berdasarkan produk, sedangkan lineplot untuk melihat rata-rata harga setiap penjualan berdasarkan produk. Cobalah dengan kode berikut ini:

      prices = all_data.groupby('Product').mean()['Price Each']
      fig, ax1 = plt.subplots()
      ax2 = ax1.twinx()
      ax1.bar(keys, quantity_ordered, color='g')
      ax2.plot(keys, prices, color='b')
      ax1.set_xlabel('Product Name')
      ax1.set_ylabel('Quantity Ordered', color='g')
      ax2.set_ylabel('Price ($)', color='b')
      ax1.set_xticklabels(keys, rotation='vertical', size=8)
      fig.show()

Kira2 hasilnya seperti ini:
overlay plot
