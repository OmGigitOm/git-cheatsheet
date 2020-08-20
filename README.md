# git-cheatsheet

Workflow sederhana penggunaan `git`.

## install git

### github untuk windows
https://windows.github.com

### github untuk mac
https://mac.github.com

### untuk semua platform
https://git-scm.com

## konfigurasi informasi user untuk semua repository lokal

set nama user yang akan digunakan sebagai informasi identitas user saat anda melakukan transaksi commit

`git config --global user.name "your_user_name"`

set alamat email yang akan digunakan sebagai informasi identitas user saat anda melakukan transaksi commit

`git config --global user.email "your_valid_email_address"`

melihat list config yang ada

`git config --list`

## Meng-_clone_ repository ke lokal

Meng-_clone_ repository dari github/gitlab ke komputer lokal.

`git clone <url-repository>`

Contoh:

```sh
git clone https://github.com/OmGigitOm/git-cheatsheet.git
```

## Membuat _branch_ baru

_Repository_ `git` terdiri dari _branch_. Masing-masing _branch_ berisikan versi perubahan. _Branch_ utama biasanya diberi nama _branch_ `master`. Satu _repository_ bisa memiliki banyak _branch_.

## untuk melihat list branch yang ada

`git branch`

Untuk melakukan perubahan _checkout_ dari branch `master` dan kemudian lakukan perubahan di-repository yang baru di _checkout_.

`git checkout -b <nama-branch>`

Contoh:

buat _branch_ `versi-1` dan pindah ke _branch_ tersebut.
```sh
git checkout -b versi-1
```

atau

`git branch <new_branch_name>`

kemudian pindah ke branch tersebut

`git checkout <new_branch_name>`

## Berpindah antar _branch_

Untuk berpindah antar _branch_ lakukan _checkout_ terhadap nama _branch_.

`git checkout <nama-branch>`

Contoh:

* Pindah ke _branch_ `master`
  ```sh
  git checkout master
  ```
* Pindah ke _branch_ `versi-1`
  ```sh
  git checkout versi-1
  ```

## Melakukan perubahan

Jangan biasakan membuat perubahan pada _branch_ `master`, lakukan perubahan pada _branch_ baru dan kemudian baru di-_merge_.

Setelah melakukan perubahan, tandai _file_/_directory_ yang akan di-_commit_ (disimpan perubahannya ke repository).

`git add <nama-file/directory>`

Contoh:

* Menambahkan perubahan file `README.md`
  ```sh
  git add README.md
  ```
* Menambahkan seluruh perubahan di-directory sekarang
  ```sh
  git add .
  ```

Setelah menandai file/directory yang akan ditambahkan dengan `git add`, lakukan _commit_ supaya perubahan tersimpan ke repository.

`git commit [-m "pesan-commit"]`

Contoh:

* Commit dengan pesan commit di baris perintah
  ```sh
  git commit -m "menambahkan readme"
  ```
* Commit dengan pesan commit diketikkan di text editor (biasanya `vim`)
  ```sh
  git commit
  ```

## Mengirimkan perubahan ke repository utama

Untuk mengirimkan perubahan ke repository utama supaya bisa dilihat atau di-_pull_ anggota tim yang lainnya lakukan _push_.

`git push -u origin HEAD`

Contoh:

Apabila _branch_ yang sedang aktif adalah `versi-1`, perintah berikut akan mem-_push_ perubahan di lokal ke repository utama di branch `versi-1` juga.
```sh
git push -u origin HEAD
```

Setelah melakukan _push_ dan perubahan ini akan digabungkan ke _branch_ `master`, buat _Pull Request_, dilakukan di halaman web github.

Dengan membuat _Pull Request_ perubahan yang dibuat bisa di-review terlebih dahulu oleh anggota tim sebelum di-_merge_.

## Menarik perubahan dari repository utama

Supaya perubahan pada repository utama bisa digunakan di repository lokal perlu dilakukan `pull`.

`git pull [nama-repository] [nama-branch]`

Contoh:

Menarik seluruh perubahan pada repository utama branch `master`
```sh
git pull origin master
```

Apabila nama repository dan nama branch tidak dicantumkan biasanya akan default ke repository `origin` (utama) dan branch yang aktif.

## Meng-_sync_ branch perubahan dengan branch `master`

Apabila sebuah repository di-edit oleh banyak anggota tim, usahakan sering-sering mem-_pull_ `master` dan _sync_ branch perubahan kita dengan branch `master` supaya lebih gampang mem-_resolve_ konflik (kalau ada).

Langkah-langkah:
* checkout branch `master`
  ```sh
  git checkout master
  ```
* tarik perubahan dari repository `origin`
  ```sh
  git pull origin master
  ```
* pindah ke branch perubahan di lokal misalnya `versi-1`
  ```sh
  git checkout versi-1
  ```
* merge master ke branch perubahan
  ```sh
  git merge master
  ```

## Melihat hasil perubahan
```sh
git show
```
atau
```
git show <nama_file>
```

Contoh:
`git show README.md`

## Flow standar bekerja dalam tim

Untuk bekerja di dalam tim flow bisa mengikuti flow kerja berikut ini:
1. Clone repo ke lokal (`git clone`)
2. Setiap perubahan dibuat pada branch baru (`git checkout -b nama-branch`)
3. Setelah selesai perubahan jangan lupa di add dan di commit (`git add . && git commit -m "pesan"`)
4. Sync perubahan master ke branch perubahan kita:
   * `git checkout master`
   * `git pull`
   * `git checkout branch-lokal`
   * `git merge master` atau `git rebase master`
5. Push perubahan ke repository origin (`git push -u origin HEAD`)
6. Bikin Pull Request minta request ke tim
7. Tim silahkan review, kalau sudah oke di-approve kalau belum kasi komentar dan diperbaiki lagi.
