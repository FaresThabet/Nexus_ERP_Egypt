# Nexus ERP — Access Credentials Matrix

This document lists every login account provisioned in the system.
Run `bun run scripts/seed-roles-users.ts` then `bun run scripts/seed-per-module-users.ts` to seed all of them.

**Password for ALL accounts:** `password123`

---

## 👑 1. Super Admin — Full access to every section

| Field    | Value                    |
| -------- | ------------------------ |
| Email    | `admin@nexuserp.com`     |
| PIN      | `0000`                   |
| Password | `password123`            |
| Role     | Super Admin (`*`)        |
| Access   | All 32 modules           |

A second super-admin account is also available:
- `ahmed@nexuserp.com` / `password123` / PIN `1234` — seeded by `seed-roles-users.ts`

---

## 🎯 2. Per-Section Accounts — One account per single module

Each account below has access to **only its own section** (plus the always-granted modules: `dashboard`, `settings`, `ai-copilot`).

| #   | Section (Module)     | Email                       | PIN   | Officer (EN)              | Officer (AR)              |
| --- | -------------------- | --------------------------- | ----- | ------------------------- | ------------------------- |
| 1   | `financial`          | `finance@nexuserp.com`      | `1001` | Khaled Finance            | خالد المالية              |
| 2   | `crm`                | `crm@nexuserp.com`          | `1002` | Layla CRM                 | ليلى العملاء              |
| 3   | `sales`              | `sales@nexuserp.com`        | `1003` | Yousef Sales              | يوسف مبيعات               |
| 4   | `purchasing`         | `purchasing@nexuserp.com`   | `1004` | Hossam Purchasing         | حسام مشتريات              |
| 5   | `inventory`          | `inventory@nexuserp.com`    | `1005` | Tarek Inventory           | طارق مخازن                |
| 6   | `fleet`              | `fleet@nexuserp.com`        | `1006` | Adel Fleet                | عادل أسطول                |
| 7   | `hr`                 | `hr@nexuserp.com`           | `1007` | Nour HR                   | نور موارد بشرية           |
| 8   | `attendance`         | `attendance@nexuserp.com`   | `1008` | Sami Attendance           | سامي حضور                 |
| 9   | `payroll`            | `payroll@nexuserp.com`      | `1009` | Reem Payroll              | ريم رواتب                 |
| 10  | `projects`           | `projects@nexuserp.com`     | `1010` | Hana Projects             | هناء مشاريع               |
| 11  | `assets`             | `assets@nexuserp.com`       | `1011` | Karim Assets              | كريم أصول                 |
| 12  | `eta`                | `eta@nexuserp.com`          | `1012` | Sherif ETA                | شريف ضرائب                |
| 13  | `dms`                | `dms@nexuserp.com`          | `1013` | Mona DMS                  | منى توزيع                 |
| 14  | `helpdesk`           | `helpdesk@nexuserp.com`     | `1014` | Ali Helpdesk              | علي دعم                   |
| 15  | `customer-portal`    | `cportal@nexuserp.com`      | `1015` | Salma Customer Portal     | سلمى بوابة عملاء          |
| 16  | `vendor-portal`      | `vportal@nexuserp.com`      | `1016` | Hatem Vendor Portal       | حاتم بوابة موردين         |
| 17  | `admin`              | `sysadmin@nexuserp.com`     | `1017` | Ibrahim SysAdmin          | إبراهيم إدارة نظام        |
| 18  | `reports`            | `reports@nexuserp.com`      | `1018` | Dina Reports              | دينا تقارير               |
| 19  | `credit-mgmt`        | `credit@nexuserp.com`       | `1019` | Wael Credit               | وائل ائتمان               |
| 20  | `whatsapp`           | `whatsapp@nexuserp.com`     | `1020` | Esraa WhatsApp            | إسراء واتساب              |
| 21  | `currency`           | `currency@nexuserp.com`     | `1021` | Farah Currency            | فرح عملات                 |
| 22  | `drilldown`          | `drilldown@nexuserp.com`    | `1022` | Galal Drilldown           | جلال تحليل                |
| 23  | `paylinks`           | `paylinks@nexuserp.com`     | `1023` | Hala Paylinks             | هالة روابط دفع            |
| 24  | `pos`                | `pos@nexuserp.com`          | `1024` | Taha POS                  | طه نقطة بيع               |
| 25  | `zreport`            | `zreport@nexuserp.com`      | `1025` | Iman ZReport              | إيمان تقرير يومي          |
| 26  | `reorder`            | `reorder@nexuserp.com`      | `1026` | Jamal Reorder             | جمال إعادة طلب            |
| 27  | `statement`          | `statement@nexuserp.com`    | `1027` | Kamal Statement           | كمال كشوف                 |
| 28  | `po-approvals`       | `poapprovals@nexuserp.com`  | `1028` | Laila PO Approvals        | ليلى اعتماد طلبات         |
| 29  | `roles`              | `roles@nexuserp.com`        | `1029` | Maged Roles               | ماجد أدوار                |

---

## 👥 3. Grouped Role Accounts — Multi-section access (from `seed-roles-users.ts`)

These cover the most common staff roles — each has access to several related modules at once.

| Role (EN)        | Role (AR)         | Email                     | PIN   | Modules Granted                                                                       |
| ---------------- | ----------------- | ------------------------- | ----- | ------------------------------------------------------------------------------------- |
| Sales Manager    | مدير مبيعات       | `sara@nexuserp.com`       | `2345` | sales, crm, inventory, credit-mgmt, paylinks, statement, whatsapp, currency, reports |
| Cashier          | كاشير             | `mahmoud@nexuserp.com`    | `3456` | pos, zreport, paylinks                                                                |
| Accountant       | محاسب             | `fatma@nexuserp.com`      | `4567` | financial, eta, reports, currency, statement, paylinks                                |
| Inventory Manager| مدير مخازن        | `omar@nexuserp.com`       | `5678` | inventory, purchasing, po-approvals, reorder, reports                                 |
| HR Manager       | مدير موارد بشرية  | (create via Roles UI)     | —     | hr, attendance, payroll, reports                                                      |
| Viewer           | مشاهد             | (create via Roles UI)     | —     | dashboard, reports, drilldown                                                         |

---

## 🔐 How permissions work

1. Every user is assigned a **Role** (or gets `permissionsOverride` set directly).
2. The role stores `permissions` as a JSON array of `ModuleId` strings.
3. The special value `["*"]` means "all modules" (super-admin).
4. Three modules are **always granted** to every user regardless of role: `dashboard`, `settings`, `ai-copilot` — see `ALWAYS_GRANTED` in `src/lib/erp-store.ts`.
5. The login endpoint (`POST /api/auth/login`) returns the expanded permission list. The Zustand store saves it as `currentUser.permissions`.
6. The main page (`src/app/page.tsx`) calls `hasAccess(currentUser.permissions, moduleId)` for:
   - Each sidebar entry → only renders modules the user can access.
   - The currently active module → renders a "🔒 Access Denied" screen if the user lacks permission.
7. The Role Management UI (under Admin → Roles) lets super-admins create new roles, assign modules, and override per-user permissions at runtime.

---

## 🛠️ Production hardening checklist

- [ ] Replace `dev-hash:password123` with real bcrypt/argon2 hashes via `POST /api/users/[id]/set-password`
- [ ] Replace `dev-token-<id>-<ts>` with a real JWT signed with `JWT_SECRET`
- [ ] Add rate-limiting on `/api/auth/login` (max 10 attempts / minute / IP)
- [ ] Add session expiry + refresh tokens
- [ ] Enable mandatory 2FA for super-admin role (`twoFactor=true` on the User model)
- [ ] Move always-granted modules into the role permissions so they can be revoked for ultra-restricted accounts
