Nama  : Hamas Izzuddin Fathi
NIM   : H1D022097

# Screensot Hasil dan Penejelasan 
## Halaman Home
![image](https://github.com/user-attachments/assets/1408da3c-c033-4e46-91cc-28c72c7122a3)

### Penjelasan
1. Dihalaman home kita dapat melihat ada data mahasiswa beserta jurusannya dan di samping itu terdapat tombol eidt dan hapus
2. dan jika kita lihat di bawah halaman ada tombol untuk tambahkan mahasiswa

## Tambah Mahasiswa
![image](https://github.com/user-attachments/assets/fcdaf9e5-461e-45b6-b376-98f617db5432)
tambahMahasiswa() {
    if (this.nama != '' && this.jurusan != '') {
      let data = {
        nama: this.nama,
        jurusan: this.jurusan,
      }
      this.api.tambah(data, 'tambah.php')
        .subscribe({
          next: (hasil: any) => {
            this.resetModal();
            console.log('berhasil tambah mahasiswa');
            this.getMahasiswa();
            this.modalTambah = false;
            this.modal.dismiss();
          },
          error: (err: any) => {
            console.log('gagal tambah mahasiswa');
          }
        })
    } else {
      console.log('gagal tambah mahasiswa karena masih ada data yg kosong');
    }
  }
  
### Penjelasan
- kode diatas adalah cara untuk menambahkan data dengan cara untuk menambahkan data mahasiswa dengan mengisi nama dan jurusan
- Fungsi ini pertama-tama memeriksa apakah nilai this.nama dan this.jurusan sudah terisi. Jika kedua variabel tersebut tidak kosong (this.nama != '' && this.jurusan != ''), proses penambahan data akan dilanjutkan.
- Jika ada data yang masih kosong, pesan kesalahan akan dicetak di konsol (console.log('gagal tambah mahasiswa karena masih ada data yg kosong')), dan proses penambahan data dihentikan.
- jika sudah mengisi data maka akan langsung muncul di halaman utama atau home

## Edit Data Mahasiswa
![image](https://github.com/user-attachments/assets/7ed7e406-c39b-40b1-93ae-e016f59cb2a3)
editMahasiswa() {
    let data = {
      id: this.id,
      nama: this.nama,
      jurusan: this.jurusan
    }
    this.api.edit(data, 'edit.php')
      .subscribe({
        next: (hasil: any) => {
          console.log(hasil);
          this.resetModal();
          this.getMahasiswa();
          console.log('berhasil edit Mahasiswa');
          this.modalEdit = false;
          this.modal.dismiss();
        },
        error: (err: any) => {
          console.log('gagal edit Mahasiswa');
        }
      })
  }

### Penjelasan 
- Fungsi ini mengedit data mahasiswa yang ada.
- Mengumpulkan id, nama, dan jurusan ke dalam objek data, lalu mengirimkannya ke endpoint edit.php melalui api.edit().
- Jika berhasil (next), modal edit ditutup (modalEdit = false dan this.modal.dismiss()), data di-refresh dengan getMahasiswa(), dan pesan berhasil dicetak di konsol.
- Jika gagal (error), pesan kesalahan dicetak di konsol.

## Hapus Data
![image](https://github.com/user-attachments/assets/c16f35dc-262d-44e0-b36f-c0baf48ba3c5)
hapusMahasiswa(id: any) {
    this.api.hapus(id,
      'hapus.php?id=').subscribe({
        next: (res: any) => {
          console.log('sukses', res);
          this.getMahasiswa();
          console.log('berhasil hapus data');
        },
        error: (error: any) => {
          console.log('gagal');
        }
      })
  }
  
### Penjelasan
- hapusMahasiswa(id: any) adalah fungsi yang mengirimkan permintaan untuk menghapus data mahasiswa.
- Memanggil api.hapus() dengan id dan endpoint hapus.php?id= sebagai parameter. Fungsi ini diasumsikan mengakses endpoint API yang bertanggung jawab untuk menghapus data.
- Jika berhasil (next), data mahasiswa di-refresh dengan getMahasiswa(), dan pesan berhasil dicetak di konsol.
- Jika gagal (error), pesan kesalahan dicetak di konsol.

