A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?
"Constraints go down" dilanggar oleh Row. Row memberi lebar tak terbatas ke Text, jadi Text melebar sebesar teksnya dan melewati batas layar.

Why is adding width: 150 to the text the wrong fix, even if the stripes disappear?
Angka tetap hanya cocok di satu ukuran. Di layar atau teks lain masalahnya muncul lagi, jadi bug-nya hanya pindah tempat.

You fixed the landscape overflow by wrapping everything in a SingleChildScrollView and setting shrinkWrap: true on the list. Which test fails, and why does it matter once the data comes from an API?
Test 7 (500 items) gagal, karena shrinkWrap: true membangun semua item sekaligus. Kalau datanya dari API dan jumlahnya besar, layar jadi lambat dan boros memori.

Why does the tablet layout use LayoutBuilder rather than MediaQuery.sizeOf(context)?
LayoutBuilder membaca ruang yang diberikan parent, sedangkan MediaQuery membaca ukuran seluruh layar. Jadi layout tetap benar walau widget ditaruh di panel atau area yang lebih sempit.

The empty-data crash was not a layout error. Why does it belong in a layout lab anyway?
Layout bergantung pada data, bukan hanya ukuran layar. Kode yang mengandaikan data selalu ada akan rusak saat datanya kosong, jadi perlu empty state.