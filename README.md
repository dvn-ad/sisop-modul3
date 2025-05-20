[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Eu-CByJh)
|    NRP     |      Name      |
| :--------: | :------------: |
| 5025241179 | Erlangga Rizqi Dwi Raswanto |
| 5025241193  | Farrel Jatmiko Aji |
| 5025241220 | Davin Adiputra Suryolaksana |

# Praktikum Modul 3 _(Module 3 Lab Work)_

### Laporan Resmi Praktikum Modul 3 _(Module 3 Lab Work Report)_

Di suatu pagi hari yang cerah, Budiman salah satu mahasiswa Informatika ditugaskan oleh dosennya untuk membuat suatu sistem operasi sederhana. Akan tetapi karena Budiman memiliki keterbatasan, Ia meminta tolong kepadamu untuk membantunya dalam mengerjakan tugasnya. Bantulah Budiman untuk membuat sistem operasi sederhana!

_One sunny morning, Budiman, an Informatics student, was assigned by his lecturer to create a simple operating system. However, due to Budiman's limitations, he asks for your help to assist him in completing his assignment. Help Budiman create a simple operating system!_

### Soal 1

> Sebelum membuat sistem operasi, Budiman diberitahu dosennya bahwa Ia harus melakukan beberapa tahap terlebih dahulu. Tahap-tahapan yang dimaksud adalah untuk **mempersiapkan seluruh prasyarat** dan **melakukan instalasi-instalasi** sebelum membuat sistem operasi. Lakukan seluruh tahapan prasyarat hingga [perintah ini](https://github.com/arsitektur-jaringan-komputer/Modul-Sisop/blob/master/Modul3/README-ID.md#:~:text=sudo%20apt%20install%20%2Dy%20busybox%2Dstatic) pada modul!

> _Before creating the OS, Budiman was informed by his lecturer that he must complete several steps first. The steps include **preparing all prerequisites** and **installing** before creating the OS. Complete all the prerequisite steps up to [this command](https://github.com/arsitektur-jaringan-komputer/Modul-Sisop/blob/master/Modul3/README-ID.md#:~:text=sudo%20apt%20install%20%2Dy%20busybox%2Dstatic) in the module!_

**Answer:**

- **Code:**
  
  `1. Update & Install software:`
    ```bash
    sudo apt -y update
    sudo apt -y install qemu-system build-essential bison flex libelf-dev libssl-dev bc grub-common grub-pc libncurses-dev libssl-dev mtools grub-pc-bin xorriso tmux
    ```
  `2. Buat direktori osboot`
    ```bash
    mkdir -p osboot
    cd osboot
    ```
  `3. Download dan ekstrak kernel linux`
    ```bash
    wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.1.1.tar.xz
    tar -xvf linux-6.1.1.tar.xz
    cd linux-6.1.1
    ```
  `4. Kommpilasi Kernel`
    ```bash
    make -j$(nproc)
    ```
  `5. Copy file bzImage ke /osboot`
    ```bash
     cp arch/x86/boot/bzImage ..
    ```
  `6. Install BusyBox`
    ```bash
    sudo apt install -y busybox-static
    ```
- **Explanation:**

  - Persiapkan kernel Linux  
    1. Update dan install software yang dibutuhkan seperti qemu, build-essential, bison, flex, dan lainnya menggunakan kode `1`.
    2. Membuat direktori untuk pembuatan dan konfigurasi kernel menggunakan kode `2`. Disini nama direktorinya adalah `osboot`. Hasilnya ada di screenshot `i`.
    3. Download dan ekstrak kernel linux menggunakan kode `3` (`wget` untuk donwload lalu ekstrak dengan `tar -xvf (-x untuk extract)` kemudian pindah dir ke folder hasil ekstrak dengan `cd`).
    4. Lalu configurasi kernel dengan `make tinyconfig` dan `make menuconfig`. Hasil config akan tersimpah di file `.config`. Screenshot `iii` dan `iv`.
    5. Kompilasi kernel (kode `4`) agar menghasilkan file `bzImage` (file kernel yang digunakan untuk booting). Hasilnya dapat dilihat di screenshot `v`
    6. File `bzImage` akan terbuat di folder  `arch/x86/boot/`, kita copy file tersebut ke folder `osboot` dengan kode `5`. screenshot `vi`
    7. Terakhir, install `BusyBox` dengan kode `6`. screenshot `vii`
  

- **Screenshot:**

  1. Hasil `mkdir osboot`
     
     ![image](https://github.com/user-attachments/assets/8d9fb6ee-7ba2-4697-91de-e8cd14206078)
  2. Hasil `Download dan ekstrak kernel linux`
     
     ![image](https://github.com/user-attachments/assets/6f138adb-88e4-4ef0-8cea-e73a7252f86d)
  3. Hasil `make tinyconfig`
     
     ![image](https://github.com/user-attachments/assets/b36a6ba0-7368-4f6a-9859-f2a070ed3dd2)
  4. Tampilan dari `make menuconfig`
     
     ![image](https://github.com/user-attachments/assets/52115f49-2a20-4f09-bfe4-fc180198f39b)
  5. file `bzImage`
     
     ![image](https://github.com/user-attachments/assets/ed2b7b22-8d68-4a21-8b30-2e85e2465e25)
  6. Copy `bzImage`
     
     ![image](https://github.com/user-attachments/assets/a23d4edf-09fd-48e3-b8c3-89fde0398d75)
  7. Install `BusyBox`
      
     ![image](https://github.com/user-attachments/assets/780021d8-50af-4bce-add6-7b189bee52da)



   

     


### Soal 2

> Setelah seluruh prasyarat siap, Budiman siap untuk membuat sistem operasinya. Dosen meminta untuk sistem operasi Budiman harus memiliki directory **bin, dev, proc, sys, tmp,** dan **sisop**. Lagi-lagi Budiman meminta bantuanmu. Bantulah Ia dalam membuat directory tersebut!

> _Once all prerequisites are ready, Budiman is ready to create his OS. The lecturer asks that the OS should contain the directories **bin, dev, proc, sys, tmp,** and **sisop**. Help Budiman create these directories!_

**Answer:**

- **Code:**

  1. Superuser
     ```bash
     sudo bash
     ```
  2. Buat directory `bin`, `dev`, `proc`, `sys`, `tmp` dan `sisop`.
     ```bash
     mkdir -p myramdisk/{bin,dev,proc,sys,tmp,sisop}
     ```
  3. Copy file device ke dir `dev`
     ```bash
     cp -a /dev/null myramdisk/dev
     cp -a /dev/tty* myramdisk/dev
     cp -a /dev/zero myramdisk/dev
     cp -a /dev/console myramdisk/dev
     ```
  4. Copy BusyBox ke dir `bin`
     ```bash
     cp /usr/bin/busybox myramdisk/bin
     cd myramdisk/bin
     ./busybox --install .
     ```

- **Explanation:**
  
  Sebelum membuat direktori, Budiman harus menjadikan dirinya sebagai superuser dengan kode `i`. Setelah itu, Budiman membuat directory yang diminta dosen menggunakan kode `ii` dengan hasil pada screenshot `a`. Kemudian Budiman copy file dari host yang diperlukan ke `/myramdisk/dev/` (kode `iii`, hasil `b`). Lalu Budiman copy file lain dari host yang diperlukan ke `/myramdisk/bin/` (kode `iv`, hasil `c`).

- **Screenshot:**

  a. Isi dari dir `/myramdisk`

     ![image](https://github.com/user-attachments/assets/c2203627-56fe-4029-af03-b23b97d093f9)

  b. Isi dari dir `myramdisk/dev`

     ![image](https://github.com/user-attachments/assets/e9daf89f-339e-4ea1-a083-f0df71dc372e)
  c. Isi dari dir `myramdisk/bin`

     ![image](https://github.com/user-attachments/assets/e044aefb-cc8c-4f3c-af5e-93cf17a3a4ce)


 

### Soal 3

> Budiman lupa, Ia harus membuat sistem operasi ini dengan sistem **Multi User** sesuai permintaan Dosennya. Ia meminta kembali kepadamu untuk membantunya membuat beberapa user beserta directory tiap usernya dibawah directory `home`. Buat pula password tiap user-usernya dan aplikasikan dalam sistem operasi tersebut!

> _Budiman forgot that he needs to create a **Multi User** system as requested by the lecturer. He asks your help again to create several users and their corresponding home directories under the `home` directory. Also set each user's password and apply them in the OS!_

**Format:** `user:pass`

```
root:Iniroot
Budiman:PassBudi
guest:guest
praktikan1:praktikan1
praktikan2:praktikan2
```

**Answer:**

- **Code:**
  1. buat dir keperluan
     ```bash
     mkdir -p myramdisk/{etc,root,home/Budiman,home/guest,home/praktikan1,home/praktikan2}
     ```
  2. Generate hash password dengan `openssl`
     ```bash
     openssl passwd -1 Iniroot
     openssl passwd -1 PassBudi
     openssl passwd -1 guest
     openssl passwd -1 praktikan1
     openssl passwd -1 praktikan2
     ```
  3. Buat file `passwd` di `etc` lalu isi:
     ```bash
     cd myramdisk/etc
     echo "root:\$1\$BhcvypYC\$OSRhex7O3EqiMeilCS3RN.:0:0:root:/root:/bin/sh" > passwd
     echo "Budiman:\$1\$APmP/CPo\$9tJ1gc7LERFoNiokqTmXI1:1001:100:Budiman:/home/Budiman:/bin/sh" >> passwd
     echo "guest:\$1\$7UdOu54I\$/RlSgSEgMrV1AJ8CNirUv.:1002:100:guest:/home/guest:/bin/sh" >> passwd
     echo "praktikan1:\$1\$vXI1Xt1N\$RbmUtj2DjFiSF3fv2R5Te.:1003:100:praktikan1:/home/praktikan1:/bin/sh" >> passwd
     echo "praktikan2:\$1\$yrCE8TmC\$rdwOr9Lvj9YnZzKLodWly.:1004:100:praktikan2:/home/praktikan2:/bin/sh" >> passwd
     ```
     

- **Explanation:**

  `put your answer here`
  pwd:
  $1$BhcvypYC$OSRhex7O3EqiMeilCS3RN.
$1$APmP/CPo$9tJ1gc7LERFoNiokqTmXI1
$1$7UdOu54I$/RlSgSEgMrV1AJ8CNirUv.
$1$vXI1Xt1N$RbmUtj2DjFiSF3fv2R5Te.
$1$yrCE8TmC$rdwOr9Lvj9YnZzKLodWly.


- **Screenshot:**

  a. isi dari dir `myramdisk` dan `home`

  ![image](https://github.com/user-attachments/assets/f71a65ba-e9c3-4d27-aa70-7bc2b48c5077)
  b. Hasil generate password

  ![image](https://github.com/user-attachments/assets/c2ff82d4-6260-46f7-a3c5-5c12a5006673)
  c. Kode dan Hasil buat file `passwd`

  ![image](https://github.com/user-attachments/assets/89d1c5f8-db12-46cc-917d-6204c819f460)




### Soal 4

> Dosen meminta Budiman membuat sistem operasi ini memilki **superuser** layaknya sistem operasi pada umumnya. User root yang sudah kamu buat sebelumnya akan digunakan sebagai superuser dalam sistem operasi milik Budiman. Superuser yang dimaksud adalah user dengan otoritas penuh yang dapat mengakses seluruhnya. Akan tetapi user lain tidak boleh memiliki otoritas yang sama. Dengan begitu user-user selain root tidak boleh mengakses `./root`. Buatlah sehingga tiap user selain superuser tidak dapat mengakses `./root`!

> _The lecturer requests that the OS must have a **superuser** just like other operating systems. The root user created earlier will serve as the superuser in Budiman's OS. The superuser should have full authority to access everything. However, other users should not have the same authority. Therefore, users other than root should not be able to access `./root`. Implement this so that non-superuser accounts cannot access `./root`!_

**Answer:**

- **Code:**
  ```bash
  cd myramdisk/etc
  echo "root:x:0:" > group
  echo "bin:x:1:root" >> group
  echo "sys:x:2:root" >> group
  echo "tty:x:5:root,Budiman,guest,praktikan1,praktikan2" >> group
  echo "disk:x:6:root" >> group
  echo "wheel:x:10:root" >> group
  echo "users:x:100:Budiman,guest,praktikan1,praktikan2" >> group
  ```

- **Explanation:**

  `put your answer here`

- **Screenshot:**
  ![image](https://github.com/user-attachments/assets/30fdef1d-e119-4373-ab43-e281e7802ad9)

  `put your answer here`

### Soal 5

> Setiap user rencananya akan digunakan oleh satu orang tertentu. **Privasi dan otoritas tiap user** merupakan hal penting. Oleh karena itu, Budiman ingin membuat setiap user hanya bisa mengakses dirinya sendiri dan tidak bisa mengakses user lain. Buatlah sehingga sistem operasi Budiman dalam melakukan hal tersebut!

> _Each user is intended for an individual. **Privacy and authority** for each user are important. Therefore, Budiman wants to ensure that each user can only access their own files and not those of others. Implement this in Budiman's OS!_

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

### Soal 6

> Dosen Budiman menginginkan sistem operasi yang **stylish**. Budiman memiliki ide untuk membuat sistem operasinya menjadi stylish. Ia meminta kamu untuk menambahkan tampilan sebuah banner yang ditampilkan setelah suatu user login ke dalam sistem operasi Budiman. Banner yang diinginkan Budiman adalah tulisan `"Welcome to OS'25"` dalam bentuk **ASCII Art**. Buatkanlah banner tersebut supaya Budiman senang! (Hint: gunakan text to ASCII Art Generator)

> _Budiman wants a **stylish** operating system. Budiman has an idea to make his OS stylish. He asks you to add a banner that appears after a user logs in. The banner should say `"Welcome to OS'25"` in **ASCII Art**. Use a text to ASCII Art generator to make Budiman happy!_ (Hint: use a text to ASCII Art generator)

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

### Soal 7

> Melihat perkembangan sistem operasi milik Budiman, Dosen kagum dengan adanya banner yang telah kamu buat sebelumnya. Kemudian Dosen juga menginginkan sistem operasi Budiman untuk dapat menampilkan **kata sambutan** dengan menyebut nama user yang login. Sambutan yang dimaksud berupa kalimat `"Helloo %USER"` dengan `%USER` merupakan nama user yang sedang menggunakan sistem operasi. Kalimat sambutan ini ditampilkan setelah user login dan setelah banner. Budiman kembali lagi meminta bantuanmu dalam menambahkan fitur ini.

> _Seeing the progress of Budiman's OS, the lecturer is impressed with the banner you created. The lecturer also wants the OS to display a **greeting message** that includes the name of the user who logs in. The greeting should say `"Helloo %USER"` where `%USER` is the name of the user currently using the OS. This greeting should be displayed after user login and after the banner. Budiman asks for your help again to add this feature._

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

### Soal 8

> Dosen Budiman sudah tua sekali, sehingga beliau memiliki kesulitan untuk melihat tampilan terminal default. Budiman menginisiatif untuk membuat tampilan sistem operasi menjadi seperti terminal milikmu. Modifikasilah sistem operasi Budiman menjadi menggunakan tampilan terminal kalian.

> _Budiman's lecturer is quite old and has difficulty seeing the default terminal display. Budiman takes the initiative to make the OS look like your terminal. Modify Budiman's OS to use your terminal appearance!_

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

### Soal 9

> Ketika mencoba sistem operasi buatanmu, Budiman tidak bisa mengubah text file menggunakan text editor. Budiman pun menyadari bahwa dalam sistem operasi yang kamu buat tidak memiliki text editor. Budimanpun menyuruhmu untuk menambahkan **binary** yang telah disiapkan sebelumnya ke dalam sistem operasinya. Buatlah sehingga sistem operasi Budiman memiliki **binary text editor** yang telah disiapkan!

> _When trying your OS, Budiman cannot edit text files using a text editor. He realizes that the OS you created does not have a text editor. Budiman asks you to add the prepared **binary** into his OS. Make sure Budiman's OS has the prepared **text editor binary**!_

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

### Soal 10

> Setelah seluruh fitur yang diminta Dosen dipenuhi dalam sistem operasi Budiman, sudah waktunya Budiman mengumpulkan tugasnya ini ke Dosen. Akan tetapi, Dosen Budiman tidak mau menerima pengumpulan selain dalam bentuk **.iso**. Untuk terakhir kalinya, Budiman meminta tolong kepadamu untuk mengubah seluruh konfigurasi sistem operasi yang telah kamu buat menjadi sebuah **file .iso**.

> After all the features requested by the lecturer have been implemented in Budiman's OS, it's time for Budiman to submit his assignment. However, Budiman's lecturer only accepts submissions in the form of **.iso** files. For the last time, Budiman asks for your help to convert the entire configuration of the OS you created into a **.iso file**.

**Answer:**

- **Code:**

  `put your answer here`

- **Explanation:**

  `put your answer here`

- **Screenshot:**

  `put your answer here`

---

Pada akhirnya sistem operasi Budiman yang telah kamu buat dengan susah payah dikumpulkan ke Dosen mengatasnamakan Budiman. Kamu tidak diberikan credit apapun. Budiman pun tidak memberikan kata terimakasih kepadamu. Kamupun kecewa tetapi setidaknya kamu telah belajar untuk menjadi pembuat sistem operasi sederhana yang andal. Selamat!

_At last, the OS you painstakingly created was submitted to the lecturer under Budiman's name. You received no credit. Budiman didn't even thank you. You feel disappointed, but at least you've learned to become a reliable creator of simple operating systems. Congratulations!_
