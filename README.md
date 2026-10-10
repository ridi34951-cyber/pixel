# GyroLock V24 — Fix Orientasi + Mirror Blur + Exposure

Proyek Android untuk diunggah ke root repository GitHub lalu dibangun menjadi APK melalui **Actions → Build GyroLock APK**.

## Perubahan V24
- **Normalisasi orientasi di piksel video:** rotasi sumber diterapkan oleh shader OpenGL; ukuran output ditukar untuk rotasi 90°/270°; video final tidak diberi metadata rotasi kedua. V23 sebelumnya menghitung rotasi tetapi membuat renderer dengan nilai `0`.
- **Mirror blur fill:** area tepi yang muncul akibat koreksi stabilisasi diisi pantulan/cerminan dari frame yang sama dan diburamkan secara lembut; area utama tetap tajam.
- **Tap-to-focus ring:** saat preview diketuk, lingkaran kecil muncul sebentar pada lokasi sentuhan dan kamera meminta AF/AE metering.
- **Exposure control:** slider EV untuk terang/gelap serta tombol AE LOCK melalui Camera2 interop bila kamera mendukungnya. ISO manual tidak dipaksakan karena dukungan berbeda antarperangkat.
- Tetap memakai jalur OpenGL ES + MediaCodec, kurva koreksi gyro 240 titik, target output 30 FPS, zoom 1×/2×/4×, dan torch bila tersedia.

## Penting
Ini adalah **source ZIP kandidat V24**, belum diklaim sudah lulus build atau uji perangkat di sini. Setelah GitHub Actions menghasilkan APK, uji dengan klip portrait pendek di OPPO A54 terlebih dahulu. Periksa apakah video hasil tetap portrait, tidak gepeng, dan area tepi terisi sesuai harapan sebelum memakai untuk rekaman penting. File video asli tetap dipertahankan jika proses stabilisasi gagal.

## Build APK
Workflow `.github/workflows/build.yml` menggunakan JDK 17 dan Gradle 8.9, lalu mengunggah `app/build/outputs/apk/debug/app-debug.apk` sebagai artifact bernama `GyroLock-debug-apk`.
