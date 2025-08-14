# My Font CDN

CDN tĩnh để lưu trữ `font-family` (woff2) và file CSS khai báo `@font-face`.

## Cấu trúc

```
my-font-cdn/
├─ css/
│  └─ fonts.css      # Khai báo @font-face
└─ fonts/            # Đặt file .woff2 tại đây
```

## Thêm font

1. Copy file `.woff2` vào thư mục `fonts/`. Ví dụ: `YourFontName-Regular.woff2`, `YourFontName-Italic.woff2`, `YourFontName-Bold.woff2`.
2. Mở `css/fonts.css` và cập nhật tên font + đường dẫn tương ứng.

## Sử dụng

Thêm vào HTML của bạn:

```html
<link rel="stylesheet" href="https://<domain-or-cdn>/css/fonts.css" />
<!-- Hoặc dùng endpoint động kiểu Google Fonts -->
<link rel="stylesheet" href="https://<domain-or-cdn>/api/fonts.css?family=I+Love+You&family=College+Black&display=swap" />
```

Sau đó dùng trong CSS:

```css
body { font-family: "YourFontName", system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, "Noto Sans"; }
```

## Cache & CORS

- Các file trong `fonts/` được cấu hình cache dài hạn: `Cache-Control: public, max-age=31536000, immutable`.
- Bật CORS cho font: `Access-Control-Allow-Origin: *`.
- Khi thay đổi nội dung, hãy version hóa đường dẫn (ví dụ: `/css/fonts.css?v=2024-08-12`) để tránh cache cũ.

## Triển khai nhanh

### Vercel

- Đã kèm `vercel.json` để set header. Chạy:

```bash
npx vercel --yes
```

### Netlify

- Đã kèm `netlify.toml` để set header. Kéo thả repo này lên Netlify hoặc dùng CLI.

### GitHub Pages (tùy chọn)

- Có thể build tĩnh và publish, nhưng GitHub Pages không chỉnh header tùy biến. Ưu tiên Vercel/Netlify để có CORS + Cache.

## Gợi ý tốt nhất

- Ưu tiên `.woff2` để tối ưu dung lượng, nhưng có thể dùng `.otf` (đã ví dụ sẵn trong `css/fonts.css`).
- Dùng `font-display: swap` để tránh chặn render.
- Nếu font có nhiều subset (latin, vietnamese…), cân nhắc tách file để tiết kiệm băng thông.

## Thử nhanh tại local

Chạy server tĩnh và mở demo:

```bash
cd demo
python3 -m http.server 8080
# Mở http://localhost:8080
```


