```text
 ██╗   ██╗███████╗███╗   ███╗ ██████╗ 
 ██║   ██║██╔════╝████╗ ████║██╔═══██╗
 ██║   ██║█████╗  ██╔████╔██║██║   ██║
 ╚██╗ ██╔╝██╔══╝  ██║╚██╔╝██║██║   ██║
  ╚████╔╝ ███████╗██║ ╚═╝ ██║╚██████╔╝
   ╚═══╝  ╚══════╝╚═╝     ╚═╝ ╚═════╝ 
   V E R A   E M U L A T O R   ( V E M O )
  [ Powered by VE-NE 3D/2D Hardware Engine ]
```

# 🎮 VEMO — Cyber-Arcade Retro Console for Android
**Version: v2.0.0-beta • License: MIT**  
*Vera Creation • Dibuat dengan cinta*

> **VEMO** adalah aplikasi konsol game retro mandiri (*standalone*) untuk Android yang menggabungkan estetika antarmuka modern **Flutter Hardware-Accelerated** dengan keperkasaan mesin *bare-metal* **VE-NE (C++17 / OpenGL ES 3.0 / AAudio / ARM NEON SIMD)** untuk menghadirkan pengalaman bermain 60 FPS murni, audio tanpa jeda, dan kenyamanan bermain layaknya konsol fisik.

---

## 📥 Unduh & Pasang Cepat (Ready to Play)

Berkas instalasi APK siap pakai tersedia langsung di dalam repositori ini:
- 📱 **[`Vemo.beta.apk`](./Vemo.beta.apk)** (~70 MB)
- Kompatibilitas: Android 8.0 (API 26) ke atas • Arsitektur: **ARM64-v8a**
- Langsung pasang ke perangkat Android kamu tanpa perlu proses *compile* manual.

---

## Status Versi & Kejujuran Teknis (Beta Transparency)

VEMO saat ini dirilis dalam status **Public Beta (v2.0-beta)** dengan peta kematangan sistem sebagai berikut:

| Kategori Sistem | Status Kematangan | Ketersediaan Core |
| :--- | :---: | :--- |
| **Nintendo GBA (Game Boy Advance)** | 🟢 **Stable (60 FPS)** | Bawaan (`libmgba.so`) |
| **Game Boy & Game Boy Color (GB / GBC)** | 🟢 **Stable (60 FPS)** | Bawaan (`libmgba.so`) |
| **Super Nintendo (SNES / Super Famicom)** | 🟢 **Stable (60 FPS)** | Bawaan (`libsnes9x.so`) |
| **Nintendo Entertainment System (NES / FDS)** | 🟢 **Stable (60 FPS)** | Bawaan (`libfceumm.so`) |
| **Sega Genesis / Mega Drive (MD / SMS / GG)** | 🟢 **Stable (60 FPS)** | Bawaan (`libgenesis_plus_gx.so`) |
| **Sony PlayStation 1 (PS1 / PSX)** | 🟡 **Architecture Ready** | Roadmap *(Core `libpcsx_rearmed.so` siap diintegrasikan)* |
| **Nintendo 64 / Arcade** | 🟡 **Planned** | Roadmap Tahap Berikutnya |

---

## Keunggulan Arsitektur VE-NE di VEMO

- **128-Bit ARM NEON SIMD Vectorization**: Konversi warna frame game 8 piksel per siklus CPU ($7\times$ speedup) membuat rendering super ringan dan suhu baterai tetap dingin.
- **Ultra-Low-Latency AAudio Dynamic Pipeline**: Penyetelan buffer hardware $2\times\text{burst}$ memotong latensi suara hingga $< 10\text{ ms}$ tanpa distorsi atau *crackling*.
- **Hybrid Deadline Frame Pacer**: Sinkronisasi ganda (Kernel coarse sleep + microspin assembly ARM64 `yield`) mengunci *frame rate* dengan jitter sangat rendah ($< 0.05\text{ ms}$).
- **Zero-Copy SurfaceTexture**: Menghubungkan frame buffer core C++ langsung ke `SurfaceTexture` hardware Android tanpa overhead browser atau WebView.
- **Auto-Extract Multi-ROM ZIP**: Pengguna dapat memasukkan puluhan ROM sekaligus ke dalam 1 berkas `.zip`. VEMO otomatis memindai, membersihkan judul dump yang kotor, dan memasangkannya ke pustaka.
- **CUE + BIN Pairing**: Mendukung disc image multi-file game retro secara rapi tanpa duplikasi berkas.
- **Custom Controller Editor (PUBG Style)**: Bebas mengatur posisi, ukuran, transparansi slider, dan kemiringan tombol virtual.
- **Instant Save & Load States**: 3 Slot penyimpanan cepat binary RAM snapshot langsung ke memori lokal.
- **100% Bebas Iklan & Offline**: Pengalaman konsol sejati tanpa interupsi jaringan.

---

## Struktur Repositori

```text
repack/github/
├── README.md             # Dokumentasi utama proyek
├── LICENSE               # Lisensi resmi MIT (Vera Creation)
├── .gitignore            # Konfigurasi filter berkas Git
├── Vemo (beta).apk       # Berkas APK rilis resmi siap pasang
└── vemo/                 # Kode sumber bersih aplikasi VEMO
    ├── android/          # Native C++ JNI bridge, jniLibs ARM64, & Gradle
    ├── assets/           # Ikon aplikasi 2D line art, font, & boxart
    ├── lib/              # Kode sumber Flutter (Clean architecture)
    ├── test/             # Unit & widget test suite
    └── pubspec.yaml      # Konfigurasi dependensi proyek
```

---

## Kompilasi dari Sumber (Build from Source)

Jika ingin melakukan kompilasi mandiri dari kode sumber:

### Prasyarat
1. Flutter SDK `>= 3.3.0`
2. Android NDK & CMake (untuk modul C++ native di `android/app/src/main/cpp/`)
3. Repositori pendamping **`ve-ne`** (diletakkan sejajar dengan folder `vemo`):
   ```bash
   # Struktur direktori:
   # workspace/
   # ├── ve-ne/
   # └── vemo/
   ```

### Langkah Kompilasi
```bash
cd vemo
flutter pub get
flutter build apk --release
```
Berkas APK hasil build akan berada di `vemo/build/app/outputs/flutter-apk/app-release.apk`.

---

## Lisensi

Proyek ini dilisensikan di bawah [Lisensi MIT](LICENSE) — dikembangkan dengan dedikasi penuh oleh **Vera Creation**.
