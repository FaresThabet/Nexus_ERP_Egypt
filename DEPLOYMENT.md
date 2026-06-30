# 🚀 Nexus ERP — دليل النشر على الإنتاج (Vercel / Netlify + Postgres)

دليل شامل لنشر النظام على Vercel أو Netlify مع قاعدة بيانات Postgres مدارة.

---

## 📋 المتطلبات قبل النشر

| المتطلب | الوصف |
|---------|-------|
| حساب GitHub | لرفع الكود (Vercel/Netlify يقرآن من Git) |
| حساب Supabase / Neon / Railway | لإنشاء قاعدة بيانات Postgres مجانية |
| حساب Vercel أو Netlify | لاستضافة التطبيق |

---

## 1️⃣ إعداد قاعدة بيانات Postgres

### الخيار A: Supabase (موصى به — مجاني حتى 500MB)

1. اذهب إلى https://supabase.com وأنشئ حساب
2. **New Project** → اختر اسماً ومنطقة (region) قريبة من مصر
3. انتظر دقيقة حتى يُنشأ المشروع
4. اذهب إلى **Project Settings → Database → Connection string**
5. انسخ **URI** بصيغة:
   ```
   postgresql://postgres.[ref]:[password]@aws-0-[region].pooler.supabase.com:6543/postgres?pgbouncer=true
   ```

### الخيار B: Neon (مجاني حتى 3GB)

1. https://neon.tech → **New Project**
2. انسخ **Connection string**:
   ```
   postgresql://[user]:[pass]@ep-[id]-pooler.[region].aws.neon.tech/[db]?sslmode=require
   ```

### الخيار C: Railway (مجاني لـ 30 يوم)

1. https://railway.app → **New Project → Provision PostgreSQL**
2. من تبويب **Variables** انسخ `DATABASE_URL`

---

## 2️⃣ النشر على Vercel (الأسهل)

### الخطوة 1: ارفع الكود إلى GitHub

```bash
cd nexus-erp-egypt
git init
git add .
git commit -m "Initial commit: Nexus ERP"
git branch -M main
git remote add origin https://github.com/USERNAME/nexus-erp-egypt.git
git push -u origin main
```

### الخطوة 2: اربط Vercel بـ GitHub

1. https://vercel.com → **Login with GitHub**
2. **Add New → Project** → اختر مستودع `nexus-erp-egypt`
3. سيكتشف Vercel أنه مشروع Next.js تلقائياً

### الخطوة 3: أضف متغيرات البيئة

في صفحة إعداد المشروع → **Environment Variables**:

| Key | Value |
|-----|-------|
| `DATABASE_URL` | postgresql://... (من Supabase/Neon) |
| `DIRECT_URL` | postgresql://... (نفس السابق بدون `?pgbouncer=true`) |
| `AUTH_SECRET` | شغّل: `openssl rand -base64 32` |
| `NEXT_PUBLIC_APP_URL` | https://your-app.vercel.app |
| `AUTH_URL` | https://your-app.vercel.app |
| `PRISMA_SCHEMA_PATH` | prisma/schema.postgres.prisma |

### الخطوة 4: انقر Deploy

- `npm install` → `npm run build`
- مدة البناء الأولى: ~3-5 دقائق
- ستحصل على رابط: `https://nexus-erp-egypt-xxx.vercel.app`

### الخطوة 5: شغّل migrations على Postgres

```bash
npm i -g vercel
vercel login
vercel link
vercel env pull .env.production
npx prisma migrate deploy --schema=prisma/schema.postgres.prisma
# أو مباشرة:
npm run db:migrate:prod
```

✅ **تم!** تطبيقك متاح على: `https://nexus-erp-egypt.vercel.app`

---

## 3️⃣ النشر على Netlify

### الخطوة 1: ثبّت @netlify/next adapter

```bash
cd nexus-erp-egypt
npm install -D @netlify/next
```

### الخطوة 2: ارفع إلى GitHub (نفس خطوات Vercel)

### الخطوة 3: اربط Netlify بـ GitHub

1. https://app.netlify.com → **Login with GitHub**
2. **Add new site → Import an existing project**
3. اختر مستودع `nexus-erp-egypt`
4. الإعدادات (تُملأ تلقائياً من `netlify.toml`):
   - **Build command**: `npm run build`
   - **Publish directory**: `.next`

### الخطوة 4: أضف Environment Variables

في **Site settings → Environment variables** أضف نفس المتغيرات.

### الخطوة 5: انقر Deploy

- مدة البناء: ~3-5 دقائق
- الرابط: `https://[random-name].netlify.app`

### الخطوة 6: شغّل migrations (نفس خطوات Vercel)

---

## 4️⃣ اختيار المنطقة (Region)

| المنصة | المنطقة الموصى بها |
|--------|---------------------|
| Vercel | `sin1` (Singapore) أو `fra1` (Frankfurt) |
| Netlify | `eu-west-1` (Dublin) |
| Supabase | `eu-central-1` (Frankfurt) أو `me-central-1` (UAE) |
| Neon | `aws-eu-central-1` |

---

## 5️⃣ نسخ احتياطي قاعدة البيانات

```bash
# تصدير
pg_dump $DATABASE_URL > backup-$(date +%Y%m%d).sql

# استعادة
psql $DATABASE_URL < backup-20260629.sql
```

---

## 6️⃣ استكشاف الأخطاء

### `PrismaClientInitializationError`
- تأكد أن URL يبدأ بـ `postgresql://`
- أضف `?sslmode=require` في نهاية URL
- للـ Supabase pooler: استخدم port `6543`

### `relation "User" does not exist`
- migrations لم تُشغّل: `npm run db:migrate:prod`

### `Function timeout exceeded` (Netlify)
- اضف indexes على الأعمدة المستخدمة في `where`/`orderBy`
- استخدم pagination
- ارقِ إلى Netlify Pro (60s)

### `Module not found: @netlify/next`
- `npm install -D @netlify/next`

---

## 7️⃣ Production Hardening Checklist

- [ ] تغيير كلمات السر الافتراضية
- [ ] تفعيل 2FA على حساب Vercel/Netlify
- [ ] ضبط `AUTH_SECRET` بقيمة 32+ حرف
- [ ] HTTPS فقط (تلقائي في Vercel/Netlify)
- [ ] Rate limiting على `/api/auth/login`
- [ ] CSRF protection على forms
- [ ] نسخ احتياطي تلقائي
- [ ] مراقبة uptime (UptimeRobot — مجاني)
