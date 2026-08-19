# Cloudflare Gateway DNS Filter — Modified Ready

نسخة جاهزة ومبسطة من مشروع Cloudflare Gateway DNS Filter، مع قوائم AdGuard + HaGeZi Pro + OISD، Allow precedence، تحديث يومي، وقائمة SNI اختيارية.

## 1) GitHub
أضف إلى **Settings → Secrets and variables → Actions**:

Secrets:
- `CF_IDENTIFIER` = Cloudflare Account ID
- `CF_API_TOKEN` = Cloudflare API Token بصلاحيات إدارة Zero Trust/Gateway المطلوبة

Variables اختيارية:
- `ENABLE_SNI_FILTER=true`
- `ADLIST_URLS` روابط إضافية مفصولة بمسافات
- `WHITELIST_URLS` روابط السماح
- `DYNAMIC_BLACKLIST` نطاقات إضافية، سطر لكل نطاق
- `DYNAMIC_WHITELIST` نطاقات السماح

ثم شغّل **Actions → CGDNS Gateway Sync → Run workflow**.

## 2) Termux
```bash
pkg update -y
pkg install python git -y
git clone YOUR_REPOSITORY_URL
cd Cloudflare-Gateway-DNS-Filter-Modified
cp .env.example .env
nano .env
python cg_dns_filter.py run
```

لحذف كل القوائم والقواعد التي تحمل بادئات المشروع:
```bash
python cg_dns_filter.py leave
```

## 3) الراوتر
لا تستخدم 1.1.1.1 وتفترض أنه سيطبق Gateway policies. أنشئ Gateway Location في Cloudflare Zero Trust، ثم استخدم عنوان DNS الخاص بالموقع في إعداد DNS على الراوتر.

SNI يحتاج WARP/Gateway proxy كما في توثيق Cloudflare.

## 4) القوائم الافتراضية
- AdGuard SDNS Filter
- HaGeZi Pro
- OISD domainswild

القوائم تُدمج وتُنظف وتُقسم إلى 1000 نطاق لكل Cloudflare list، مع حد 300 قائمة.

## ملاحظة
هذه النسخة لا تضع أي Token داخل المستودع. لا ترفع `.env` إلى GitHub.
