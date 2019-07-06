# Rangkuman-Modul7

Hashing
untuk mempercepat pencarian dalam tabel data atau pembandingan data seperti di dalam basis data,
mencari duplikasi atau kesamaan disebuah arsip komputer yang besar, menemukan goresan-goresan yang sama di sebuah DNA, dan sebagainya.

Didalam Hashing ada beberrapa istilah, di antaranya:
1. Hash Table, yaitu sebuah tempat penyimpanan data, yang dibuat sedemikian rupa, sehingga dapat memudahkan pencarian.
   Tipe data list di python dapat digunakan untuk merepresentasikan hash table.
2. slot, yaitu posisi (indeks) yang terdapat pada hash table sebagai tempat penyimpanan setiap data.
   Karena slot berfungsi seperti halnya indeks, maka nilai slot adalah nilai integer mulai dari nol sampai dengan ukurang dari hash table,
   misalkan slot 0, slot 1, slot 2, .... , slot nn.
3. Hash function, yaitu suatu fungsi yang memetakan antara data dengan slot di dalam hash table.

Fungsi Hash
fungsi hash ini berperan sangat penting dalam algoritma hashing, pencarian data dilakukan berdasarkan nilai hash dari hash function ini.

Berikut adalah fungsi-fungsi yang diperlukan untuk algoritma hashing ini, antara lain :
  1. hash function (gunakan remainder function, yaitu data dimodulus dengan 11), nilai balik merupakan nilai hash
  2. createHashTable, untuk membuat hash table, dengan inisialisasi semua slot berisi 'none'
  3. putData, yaitu menyusun data ke dalam hash table, berdasarkan nilai hash yang dihasilkan
  4. searchHash, argumen merupakan data yang dicari, dan nilai balik berupa True or False, yaitu apakah data ditemukan di dalam hash table

      def remainderFunction (data,num):
          return (data%num)
      def createHashTable(num):
          temp=[]
          for i in range(num):
              temp.append('none')
          return(temp)
      def putData(data,table):
          for i in range(len(data)):
              ind=remainderFunction(data[i],len(table))  
              table[ind]=data[i]
          return(table)
      def searchHash(data,table):
          hashVal=remainderFunction(data,len(table))
          if data==table[hashVal]:
              return True
          else:
              return False
              
Berikut adalah contoh data dan pencarian dengan menggunakan konsep hashing

      a=[54, 26, 93, 17, 77, 31]
      hashTable=createHashTable(11)
      print(hashTable)
      
    hashTable=putData(a,hashTable)
    print(hashTable)

    searchHash(93,hashTable)
True


Berikut code untuk mendapatkan nilai ascii dari suatu karakter

    def strVal(strData):
        temp=0
        for i in range (len(strData)):
            temp=temp+ord(strData[i])
        return(temp)
    
    strVal('indonesia')
Hanya saja, fungsi tersebut akan menghasilkan nilai yang sama terhadap anagram. Misalkan nilai dari kata 'dia' sama dengan 'adi'

    print(strVal('dia'))
    print(strVal('adi'))

Berikut code untuk pembuatan fungsi Linear Probing.
Misalkan terdapat data a=[54, 26, 93, 17, 77, 31], dan hash function yang digunakan adalah remainder function,
maka tambahkan fungsi linear probing, agar dapat memasukkan data baru yaitu 44, 55, dan 20,
sehingga a= [54, 26, 93, 17, 77, 31, 44, 55, 20]

      def linearProbing(ind,hashTable,data):
          count=ind
          found=False
          while (count!=ind-1) and not(found):
              if hashTable[count]=='none':
                  found=True
                  hashTable[count]=data
              else:
                  count=count+1
                  if count==len(hashTable)-1:
                      count=0
          return(hashTable)

      def putData3(a,hashTable,functionName):
          for i in range(len(a)):
              if functionName=='reminder':
                  ind=remainderFunction(a[i],len(hashTable))      
              elif functionName=='midSq':
                  ind=midSqFunction(a[i],len(hashTable))  
              if hashTable[ind]=='none':
                  hashTable[ind]=a[i]
              else:
                  hashTable=linearProbing(ind,hashTable,a[i])    
          return(hashTable)

      a=[54, 26, 93, 17, 77, 31]
      hashTable=createHashTable(11)
      print(hashTable)
      hashTable=putData3(a,hashTable,'reminder')
      print(hashTable)
      
      a=[54, 26, 93, 17, 77, 31,44,55,20]
      hashTable=createHashTable(11)
      print(hashTable)
      hashTable=putData3(a,hashTable,'reminder')
      print(hashTable)



Soal Praktikum

Buatlah fungsi-fungsi yang diperlukan dalam pencarian berdasarkan menggunakan konsep hashing, dan penanganan collusion dengan chaining.
Fungsi-fungsi tersebut antara lain :
1. Hash Function yaitu fungsi hash yang menggunakan remainder function, dengan dua argument atau parameter, yaitu :
    a. data yang akan dimasukkan ke dalam table hash
    b. bilangan modulo
   Sedangkan return value nya berupa adalah slot atau posisi data pada hash table
   Contoh berikut adalah eksekusi reminderfunction dengan argument data berupa 55, dan bilangan modulo adalah 10,
   sehingga output yang dihasilkan adalah 55 % 10 = 5
   
    slot=remainderFuncition(55,10)
    print(slot)
5

2. create Hash Table, yaitu fungsi pembuatan hash table. Gunakan list 2D pada pembuatan hash table ini, karena dibutuhkan untuk
   penanganan collusion dengan chaining. Argumen yang terdapat pada fungsi ini adalah ukuran dari hash table, sedangkan return value
   berupa Hash table yang telah terbentuk (berupa list 2D, dengan nilai default adalah [None]
   Berikut adalah inisialisasi hash table dengan ukuran 11 


