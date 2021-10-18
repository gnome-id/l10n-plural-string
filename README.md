# Bentuk Jamak Untuk Terjemahan Format gettext: Saatnya Kembali ke Jalan yang Benar

[ANDIKA TRIWIDADA·SATURDAY, 27 OCTOBER 2018](https://www.facebook.com/notes/andika-triwidada/bentuk-jamak-untuk-terjemahan-format-gettext-saatnya-kembali-ke-jalan-yang-benar/2104238809628586/)

Ketika sedang menerjemahkan LibreOffice, saya menemui beberapa string yang tidak mungkin diterjemahkan secara memadai. String tersebut memiliki bentuk jamak, sehingga string asli dalam bahasa Inggris disajikan dalam dua bagian: bentuk tunggal dan bentuk jamak. Masalah muncul ketika saya coba terjemahkan ke bahasa Indonesia. Saya coba hanya menerjemahkan bentuk jamak, ternyata ditolak oleh aplikasi penerjemahan daring berbasis web milik LibreOffice (yang memakai Pootle). Akibatnya? Semua bentuk jamak string tersebut tidak akan pernah muncul ketika kita memakai bahasa Indonesia untuk antarmuka pengguna!

Saya coba laporkan masalah ini ke LibreOffice. Mereka cukup responsif, dan meminta konfirmasi, apakah benar aturan bentuk jamak yang dipakai oleh bahasa Indonesia adalah seperti yang dicantumkan di halaman ini:
[http://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html](http://docs.translatehouse.org/projects/localization-guide/en/latest/l10n/pluralforms.html)

nplurals=1; plural=0;

Tentu saja saya katakan itu benar, karena memang yang dipakai di GNOME dan banyak aplikasi lain yang saya terjemahkan ke bahasa Indonesia, itu yang dipakai.

Tapi ternyata ini bentuk yang salah. Bahkan manual gettext sudah menyatakan bentuk yang benar untuk bahasa Indonesia adalah:
[https://www.gnu.org/software/gettext/manual/html_node/Plural-forms.html#Plural-forms](https://www.gnu.org/software/gettext/manual/html_node/Plural-forms.html#Plural-forms)

__Two forms, singular used for one only - Austronesian family__ Bahasa Indonesian

Jadi, kenapa kok di berbagai tempat kita memakai bentuk yang salah?

Saya pikir, sudah saatnya ini diluruskan. Saatnya pindah ke bentuk yang dinyatakan oleh gettext.

# Pemutakhiran 2021

Hasil diskusi singkat pada Jumat, 15 Oktober 2021 19.31 s.d. 19.45 UTC+7 di kanal Telegram GNOME l10n ID

---
Tautan https://i14i.andika.info/index.php?title=Halaman_Utama#Bentuk_Jamak

## Bentuk Jamak
Identifikasi bentuk jamak untuk bahasa Indonesia berbeda antara gettext dengan unicode. Mana yang benar? Mana yang lebih sesuai untuk penerjemahan perangkat lunak? Apa implikasi penggunaan bentuk jamak unicode?

### GNU gettext
Lihat https://www.gnu.org/software/gettext/manual/html_node/Plural-forms.html.

Two forms, singular used for one onl This is the form used in most existing programs since it is what English is using. A header entry would look like this:
```
Plural-Forms: nplurals=2; plural=n != 1;
```
(Note: this uses the feature of C expressions that boolean expressions have to value zero or one.) Languages with this property include: Austronesian family: Bahasa Indonesian

### Unicode
https://unicode-org.github.io/cldr-staging/charts/37/supplemental/language_plural_rules.html
```
Plural-Forms: nplurals=1; plural=0;
```

## Kasus yang Pernah Ditemui

- Tunggal: There is one item bla bla bla
- Jamak: There are %d items bla bla bla

## Kesimpulan
1. Kembali ke `nplurals=1`
2. Jika menemui kasus seperti di atas, laporkan sebagai kutu

