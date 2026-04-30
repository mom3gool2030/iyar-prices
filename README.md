# 🏛 عيار العقارية — نظام تحديث الأسعار التلقائي

نظام يسحب الأسعار من المصادر الرسمية ويحدّثها كل ١٥ يوم تلقائياً.

## 📡 المصادر

- **منصة سكني** → https://sakani.sa/reports-and-data
- **البورصة العقارية** → https://srem.moj.gov.sa

## ⚙️ كيف يعمل

```
GitHub Actions (كل ١٥ يوم)
    ↓
يشغّل scraper.py
    ↓
يولّد prices.json + prices.js
    ↓
يرفعهم على GitHub تلقائياً
    ↓
الموقع iyar.netlify.app يقرأ منهم
```

## 📂 الملفات

| الملف | الوصف |
|-------|--------|
| `scraper.py` | السكربت الرئيسي — يسحب البيانات |
| `prices.json` | الأسعار بصيغة JSON |
| `prices.js` | الأسعار بصيغة JavaScript للموقع |
| `.github/workflows/update-prices.yml` | الجدولة التلقائية |

## 🚀 التشغيل اليدوي

```bash
pip install requests beautifulsoup4
python3 scraper.py
```

## 🔄 التحديث التلقائي

السكربت يشتغل تلقائياً:
- **يوم 1 من كل شهر** الساعة 3 صباحاً (UTC)
- **يوم 15 من كل شهر** الساعة 3 صباحاً (UTC)

لتشغيله يدوياً من GitHub:
1. اذهب إلى تبويب **Actions**
2. اختر **تحديث أسعار عيار العقارية**
3. اضغط **Run workflow**

## 📊 هيكل البيانات

```json
{
  "metadata": { ... },
  "districts": {
    "الملقا": {
      "name": "الملقا",
      "region": "north",
      "tier": "luxury",
      "annual_rent": {
        "apartment": 65000,
        "villa": 180000,
        "floor": 110000
      },
      "monthly_rent": { ... },
      "fair_range": { "low": 55000, "high": 75000 },
      "price_per_sqm": 6800,
      "last_updated": "2026-04-29"
    }
  }
}
```
