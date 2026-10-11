# Ditto — Bản build cá nhân hoá (Việt hoá +slash-filter + Minimalist)

Fork từ [sabrogden/Ditto](https://github.com/sabrogden/Ditto) — clipboard manager cho Windows, build từ source với bộ tuỳ biến cá nhân:

## Tuỳ biến so với bản gốc

- **Tiếng Việt đầy đủ** — dịch 100% 581 chuỗi giao diện (18 section), đặt làm ngôn ngữ mặc định khi cài.
- **Theme Minimalist** — nền trắng sạch, chữ đen, gạch phân cách hàng mảnh xám, hàng chọn xám nhạt. Theme mặc định khi cài.
- **Slash-filter trong ô tìm kiếm** — gõ nhanh để lọc theo loại clip:
  - `/image` — chỉ clip ảnh
  - `/file` — chỉ clip file (CF_HDROP)
  - `/text` — chỉ clip text
  - `/link` — chỉ link (bắt đầu bằng `http`)
  - `/star` — chỉ clip giữ (never auto delete)
  - `/today` — chỉ clip hôm nay
  - Kết hợp được: `/image /today`, `/link từ khoá`. Gõ sai prefix (`/images`) → tìm text như thường. `/q` giữ nguyên hành vi cũ.
- **Ctrl+S thông minh** — lưu clip đang chọn ra file, tự chọn định dạng theo clip: ảnh → `.png`, text → `.txt`.
- **Ctrl+E / Ctrl+Q** — Ctrl+E sửa clip (cửa sổ lớn, căn giữa màn hình lần đầu, nhớ vị trí sau đó, mở ở đầu nội dung + caret cuối). Ctrl+Q lưu + đóng + quay lại danh sách, focus đúng clip vừa sửa.
- **Icon mới** — nền trắng bo tròn, 2 nét chéo đen (Tabler slashes).
- **Danh sách dễ đọc** — hàng cao hơn ~40%, gạch phân cách mảnh, ảnh thumbnail lớn theo.
- **Popup nhớ vị trí** — mở tại vị trí lần cuối sử dụng, không nhảy theo con trỏ.

## Tải về

Tải bản build mới nhất trong tab [Releases](https://github.com/nguyendinhquocx/Ditto/releases) — giải nén và chạy `Ditto.exe` trực tiếp (không cần cài đặt).

Yêu cầu: Windows 10/11 x64, [Visual C++ Redistributable 2015-2022](https://aka.ms/vs/17/release/vc_redist.x64.exe).

## Cài đặt thay bản cũ

1. Thoát Ditto bản cũ (system tray → Exit). Settings + database nằm ở `%APPDATA%\Ditto` và registry `HKCU\Software\Ditto` — gỡ bản cũ KHÔNG ảnh hưởng nếu giữ chúng.
2. Giải nén bản build vào thư mục bất kỳ (giữ nguyên cấu trúc `Language\`, `Themes\`, `Addins\`).
3. Chạy `Ditto.exe` — tự đọc lịch sử clip + settings cũ.
4. Bật khởi động cùng Windows: phím tắt shortcut vào `shell:startup` hoặc registry `HKCU\...\Run`.

Ngôn ngữ tiếng Việt + theme Minimalist được bật sẵn sau lần chạy đầu.

## Build từ source

Yêu cầu: Visual Studio 2022 (17.14+) với workload Desktop C++, component **MFC + ATL for v143 build tools**.

```
nuget restore CP_Main_10.sln -PackagesDirectory packages
msbuild CP_Main_10.sln /p:Configuration=Release /p:Platform=x64 /m
```

Output: `Release64\Ditto.exe`. Copy `Debug\Language\` + `Debug\Themes\` cạnh exe nếu chưa có.

Toolset: **v143** (fallback từ v145 của upstream — sửa trong 6 file `.vcxproj`).

## Scripts hỗ trợ

- `docs/specs/.working/SPEC-2026-10-10-ditto-customize/tools/diff_language.py` — đối chiếu file ngôn ngữ với English.xml (gate bắt buộc khi sửa bản dịch).
- `docs/specs/.working/SPEC-2026-10-10-ditto-customize/tools/render_icon.py` — tái tạo bộ icon từ SVG.

## Upstream

- Base: [sabrogden/Ditto](https://github.com/sabrogden/Ditto) master (`a80fd35`)
- Toàn bộ thay đổi nằm trong branch `ai/slash-filter` — lịch sử commit rõ ràng từng tính năng, thuận tiện cho việc tách PR upstream sau này (bản dịch + slash-filter).
- Cảm ơn [Scott Brogden](https://github.com/sabrogden) và cộng đồng Ditto.
