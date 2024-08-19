~~~dart
import 'dart:io';

  

// Fungsi untuk menghitung sisa kredit setelah uang muka

double hitungSisaKredit(double hargaMobil, double uangMuka) {

  return hargaMobil - uangMuka;

}

  

// Fungsi closure untuk menghitung bunga

Function hitungBunga(double sukuBunga) {

  return (double sisaKredit) {

    return sisaKredit * sukuBunga / 100;

  };

}

  

// Fungsi utama untuk menghitung total pembayaran kredit

double hitungTotalPembayaran(double hargaMobil, double uangMuka, double sukuBunga, int lamaCicilan) {

  double sisaKredit = hitungSisaKredit(hargaMobil, uangMuka);

  var bunga = hitungBunga(sukuBunga); // Closure untuk menghitung bunga

  double totalPembayaran = 0;

  for (int i = 0; i < lamaCicilan; i++) {

    double bungaPerBulan = bunga(sisaKredit);

    double cicilanPerBulan = sisaKredit / lamaCicilan + bungaPerBulan;

    totalPembayaran += cicilanPerBulan;

  }

  return totalPembayaran;

}

  

void main() {

  // Input dari pengguna

  stdout.write('Masukkan harga mobil: ');

  double hargaMobil = double.parse(stdin.readLineSync()!);

  

  stdout.write('Masukkan uang muka: ');

  double uangMuka = double.parse(stdin.readLineSync()!);

  

  stdout.write('Masukkan suku bunga (%): ');

  double sukuBunga = double.parse(stdin.readLineSync()!);

  

  stdout.write('Masukkan lama cicilan (bulan): ');

  int lamaCicilan = int.parse(stdin.readLineSync()!);

  

  // Memastikan input valid menggunakan percabangan

  if (uangMuka >= hargaMobil) {

    print('Uang muka tidak bisa lebih besar atau sama dengan harga mobil.');

    return;

  }

  

  if (lamaCicilan <= 0) {

    print('Lama cicilan harus lebih dari 0.');

    return;

  }

  

  // Hitung total pembayaran kredit

  double totalPembayaran = hitungTotalPembayaran(hargaMobil, uangMuka, sukuBunga, lamaCicilan);

  print('Total pembayaran kredit adalah: Rp ${totalPembayaran.toStringAsFixed(2)}');

}
~~~