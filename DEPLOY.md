# UBCAB Express — Supabase + Vercel Deployment Guide

## 1. Supabase тохиргоо

### 1.1 Шинэ проект үүсгэх
1. https://supabase.com → **New project** дарна
2. Нэр: `ubcab-express` (өөрийн хүссэн нэр)
3. Database password хадгалаарай
4. Region: Singapore (Asia Pacific, хамгийн ойр)

### 1.2 Хүснэгтүүд үүсгэх
1. Supabase → **SQL Editor** → **New query**
2. `supabase-schema.sql` файлын бүх агуулгыг хуулж буулгана
3. **Run** дарна → "Success" гарах ёстой

### 1.3 API keys авах
1. Supabase → **Settings** → **API**
2. Дараах 2 утгыг хуулна:
   - **Project URL**: `https://XXXXX.supabase.co`
   - **anon / public key**: `eyXXXXXX...`

### 1.4 supabase-sync.js тохируулах
`supabase-sync.js` файлын эхэнд:
```js
const SUPABASE_URL = 'https://ТАНЫ-URL.supabase.co';
const SUPABASE_KEY = 'eyТАНЫ-KEY...';
```

---

## 2. UBCAB Express App.html-д sync нэмэх

`UBCAB Express App.html` файлд `</body>` таагаас өмнө нэмнэ:
```html
<script src="supabase-sync.js"></script>
```

---

## 3. GitHub-д байршуулах

```bash
# Шинэ repo үүсгэх
git init
git add .
git commit -m "UBCAB Express initial commit"

# GitHub-д push
git remote add origin https://github.com/ТАНЫ-USERNAME/ubcab-express.git
git branch -M main
git push -u origin main
```

---

## 4. Vercel-д deploy хийх

### Арга 1: Vercel CLI
```bash
npm i -g vercel
vercel
```

### Арга 2: Vercel UI
1. https://vercel.com → **New Project**
2. GitHub repo-г импортлох
3. Framework: **Other** (plain static)
4. **Deploy** дарна

### Vercel Environment Variables (optional)
Supabase key-г environment variable болгохыг хүсвэл:
- `VITE_SUPABASE_URL` = your URL
- `VITE_SUPABASE_KEY` = your key

---

## 5. Хадгалагдах өгөгдлүүд

| localStorage key | Supabase table | Тайлбар |
|---|---|---|
| `ub_registrations` | `registrations` | Жолоочийн бүртгэл |
| `ub_return_results` | `return_results` | Авсан/Цуцалсан |
| `ub_driver_requests` | `driver_requests` | Бараа/Цалин хүсэлт |
| `ub_driver_notifs` | `driver_notifs` | Notification |
| `ub_shipment_tasks` | `shipment_tasks` | Excel даалгавар |
| `ub_cs_inbox_overrides` | `cs_inbox_overrides` | CS шийдвэр |

---

## 6. Ажиллагааны дараалал

```
Жолооч/CS → усePersist (localStorage, шуурхай)
                    ↓ (beforeunload)
             Supabase (cloud backup)
                    ↓ (realtime subscription)
             Бусад хэрэглэгчид шинэчлэгдэнэ
```

---

## 7. Туршилтын данс

| Режим | Нэвтрэх |
|---|---|
| Жолооч | Бүртгүүлэх → Admin зөвшөөрнө → Нэвтрэх |
| CS ажилтан | sara@ubcab.mn / нууц үг (demo) |
| Admin | admin@ubcab.mn / нууц үг (demo) |
