# Beast Vault — Hex Tactics Royale (GitHub Pages)

Đây là bản **static Web** của Beast Vault (tên cũ: Cờ Thú 2D / Đại Chiến Thú Rừng), export từ Godot 4.6.2. URL Pages giữ nguyên `jungle-chess-2d`.
**Nơi up chính thức từ 23/11/2026: GitHub Pages** (thay cho Netlify Drop).

## Cấu trúc (bắt buộc đúng cấp gốc repo)

```
index.html          <- copy của CoThu.html (GitHub Pages cần index.html)
CoThu.html
CoThu.js
CoThu.wasm
CoThu.pck
CoThu.service.worker.js
CoThu.manifest.json
CoThu.audio*.js
CoThu.*.png
.nojekyll           <- bắt buộc: tắt Jekyll để Pages không bỏ qua file tĩnh
README.md
```

Không được bọc thêm thư mục con. Không đẩy `project\`, không đẩy bản Windows.

## Cách đẩy lên GitHub (lần đầu)

1. Tạo repo **public** trên https://github.com/new (vd `gamecothu2d`).
   - Free account: repo phải **Public** thì GitHub Pages mới chạy.
   - Không tick "Initialize with README" (repo đang có README sẵn).
2. Trong PowerShell, tại thư mục này:

```powershell
cd "E:\CodeGame\GameCoThu_GoDot\build\GameCoThu2D_GitHubPages"
git init -b main
git add .
git commit -m "Game Co Thu 2D Web - v13 github pages"
git remote add origin https://github.com/<TEN_TAI_KHOAN>/<TEN_REPO>.git
git push -u origin main
```

3. Vào repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch `main` / `/(root)` → **Save**.
4. Đợi 1–3 phút, link chạy ở:
   - `https://<TEN_TAI_KHOAN>.github.io/<TEN_REPO>/`
   - Nếu repo đặt tên `<TEN_TAI_KHOAN>.github.io` thì link là `https://<TEN_TAI_KHOAN>.github.io/`.

**Bản đang public:** https://troggzz.github.io/jungle-chess-2d/ (repo `https://github.com/Troggzz/jungle-chess-2d`).

**Lần 59:** Sửa tạo/tìm phòng trên Web và đồng bộ vào trận khi chủ phòng bấm Bắt đầu.

**Lần 58:** Báo rõ khi khách cần đăng nhập để tạo phòng Online, thêm lối về màn đăng nhập,
cải thiện form Web ở khổ dọc và không để hướng dẫn che Cẩm nang.

**Lần 57:** âm thanh toàn màn hình (autoload `AudioManager` + 14 SFX + nhạc nền),
hiệu ứng đòn mạnh hơn (hit-stop/rung/chớp/zoom), thay emoji bằng ký tự ASCII để hết ô vuông `□`,
và sửa text lỗi (`giảm N lượt CD`, `giảm N% ST nhận vào`).
Supabase: `https://hgrevylyxqfeobqrdcha.supabase.co`.

## Cập nhật lần sau

Export Web lại từ Godot, **copy `CoThu.html` → `index.html`**, rồi copy toàn bộ file vào folder này
(giữ `.nojekyll` và `README.md`), sau đó:

```powershell
cd "E:\CodeGame\GameCoThu_GoDot\build\GameCoThu2D_GitHubPages"
git add -A
git commit -m "update web"
git push
```

URL giữ nguyên.

## Lưu ý quan trọng cho AI/người bảo trì sau

- **Mic chỉ chạy khi `isSecureContext=true`.** GitHub Pages là HTTPS nên OK; `http://localhost` cũng OK.
  Không test mic trên `http://<ip>:8123`.
- Supabase URL + publishable key đã dán sẵn trong `supabase_client.gd` từ Lần 44 → người chơi mới không cần dán gì.
- `user://` trên Web nằm trong IndexedDB **theo origin**. Đổi từ Netlify sang GitHub Pages là đổi origin
  → tài khoản "Chơi ngay", `profile.cfg`, `settings.cfg`, `supabase_config.json` **không theo sang**.
  Đăng nhập lại bằng Email để kéo hồ sơ từ bảng `player_profiles` về; guest thì mất dữ liệu cũ.
- Logo Godot lúc tải đã bị thay bằng Custom HTML Shell (`project/web_shell/cothu_shell.html`).
  Sau khi export Web, `index.html` sẽ hiện chữ "BEAST VAULT · HEX TACTICS ROYALE" + thanh tải, không còn logo Godot.
  Nhãn "Powered by Netlify" cũng không có vì host là GitHub Pages.
- GitHub Pages **chỉ static hosting**: không chạy game server. Phòng online dùng Supabase
  (xem `update/HUONG_DAN_SUPABASE_ONLINE.md` trong thư mục gốc dự án).
- Nếu mở `/` báo 404: thiếu `index.html` hoặc thiếu `.nojekyll`. Copy lại rồi push lại.
