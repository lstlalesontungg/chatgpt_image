# OpenAI Image Generator

Static web tạo ảnh OpenAI. 1 file `index.html`, không backend.

## Chạy local

```bash
open index.html
```

Hoặc serve:
```bash
python3 -m http.server 8000
```

## Deploy Cloudflare Pages qua GitHub Actions

### 1. Push repo lên GitHub

```bash
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```

### 2. Tạo Cloudflare Pages project (1 lần)

- Vào https://dash.cloudflare.com/?to=/:account/pages
- Create > Pages > **Direct Upload** (không cần kết nối GitHub, vì dùng Actions)
- Đặt tên project: `openai-image-gen` (phải khớp `--project-name` trong workflow)

### 3. Lấy Cloudflare API token + Account ID

- **Account ID**: Cloudflare dashboard > sidebar phải
- **API Token**:
  - https://dash.cloudflare.com/profile/api-tokens
  - Create Token > template **"Edit Cloudflare Workers"** (hoặc custom với quyền `Account.Cloudflare Pages: Edit`)

### 4. Add GitHub Secrets

Repo > Settings > Secrets and variables > Actions > New repository secret:

| Name | Value |
|---|---|
| `CLOUDFLARE_API_TOKEN` | token bước 3 |
| `CLOUDFLARE_ACCOUNT_ID` | account ID bước 3 |

### 5. Push → tự deploy

URL sẽ là: `https://openai-image-gen.pages.dev`

## Bảo mật

API key lưu **localStorage** browser, gửi trực tiếp `api.openai.com`. Không qua server bạn. Đừng dùng key chung trên thiết bị công cộng.
