# WebappSecret Tanıtım Sitesi Paket içeriği

Bu klasör, Next.js projesinin GitHub Pages üzerinde yayınlanmaya hazır statik çıktısını içerir. Aşağıdaki adımları izleyerek `bugraozel/WebappSecret` deposuna yükleyebilirsin.

## Yükleme Adımları
1. Bu klasörün (``deploy/WebappSecret``) içeriğini ayrı bir yerde kopyala ya da zip olarak al.
2. `WebappSecret` deposunu klonla veya aç.
3. Depoda sadece bu klasörün içindekileri (``index.html``, ``_next`` klasörü, ``.nojekyll`` vb.) root'a koy.
4. Gerekirse ``.nojekyll`` dosyasının repo root'unda olduğundan emin ol (GitHub Pages için gerekli).
5. Değişiklikleri commit et ve ``main`` veya GitHub Pages için ayarladığın branch'e push et.
6. GitHub repo ayarlarında **Pages** sekmesine git, kaynak olarak ilgili branch'i (ve root klasörü) seç.
7. Sayfa hazır olduğunda GitHub sana `https://bugraozel.github.io/WebappSecret/` adresini verecek.

## Tekrar Derleme
- Statik sayfayı güncellemek için proje kökünde aşağıdaki komutu çalıştırman yeterli:
  ```powershell
  $env:NEXT_PUBLIC_BASE_PATH="WebappSecret"; npm run build --workspace apps/frontend
  ```
- Ardından ``apps/frontend/out`` klasörünü tekrar ``deploy/WebappSecret`` içine kopyalayabilirsin.

Keyifli sunumlar! 🎮
