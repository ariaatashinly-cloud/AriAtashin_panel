# atiaatashin

پنل فارسی با تم آتشی و ساخت خودکار اینباند، کاربر، لینک و QR؛ روی هستهٔ رسمی **3x-ui 3.8.5 / Xray**، سازگار با launcher فعلی Go.

**[راهنمای نصب فارسی](INSTALL-FA.md)** را قبل از اولین Deploy بخوان. این پروژه هنوز روی حساب GitHub یا Velixir تو نصب نشده است.

## امکانات نسخهٔ اول

- VLESS/WS، VLESS/XHTTP، VMess/WS و Trojan/WS با پورت داخلی loopback و مسیر تصادفی.
- هماهنگی خودکار Address، پورت عمومی، Host، SNI، TLS و ALPN از یک آدرس واقعی.
- سهمیه و انقضای کاربر؛ ساخت گروهی ۱ تا ۵۰ کاربر؛ لینک، QR محلی و Subscription.
- ویرایش، فعال/غیرفعال، ریست مصرف، تعویض کلید و حذف.
- داشبورد مصرف واقعی، عیب‌یابی داخلی، بکاپ و بازیابی ادغامی با حفظ کلید و Path.
- Cookie امن، CSRF، محدودیت تلاش ورود، assets محلی و SHA-256 هستهٔ pinned.

نسخهٔ اول، برای **یک مدیر / یک Replica / Linux amd64** است. تمام امکانات پیشرفتهٔ سنایی، نمایندگی یا پرداخت را ندارد. اطلاعات کاربران قبلی خودکار migrate نمی‌شوند. بکاپ native سنایی با بکاپ این پنل متفاوت است.

## تنظیم حداقلی

در Environment میزبان این مقادیر را تعیین کن، نه داخل GitHub:

```text
ATIA_PUBLIC_URL=https://your-real-app.velixir.run
ATIA_ADMIN_USER=admin
ATIA_ADMIN_PASSWORD=<a-private-password-of-at-least-12-characters>
```

HTTP برنامه معمولاً روی `PORT=8080` است؛ گوشی روی HTTPS عمومی `443` وصل می‌شود. Min/Max replicas را **۱** نگه‌دار. برای Health probe از `/health` استفاده کن. روی Velixir دیسک موقتی است؛ پیش از Restart/Redeploy بکاپ لازم است. پلن پولی Volume واقعی ایجاد نمی‌کند.

## توسعه و اجرای دارای Volume

```sh
go test -race ./...
go vet ./...
go build .
```

Go 1.22 یا جدیدتر، بدون dependency خارجی Go. تمام فایل‌های Go و پوشهٔ `web` باید کنار `go.mod` باشند. اولین اجرای source-build، هستهٔ رسمی amd64 را دانلود و digest آن را بررسی می‌کند. Dockerfile هسته را هنگام Build می‌گیرد.

`compose.yaml` برای سرور دارای Docker و Volume ارائه شده؛ HTTPS reverse proxy را جدا تنظیم کن. فایل `.env`، دیتابیس و بکاپ را commit نکن. محدودیت شبکه و مجوز VPN/proxy میزبان همچنان برقرار است.

گزارش آزمون: [TEST-REPORT.md](TEST-REPORT.md). انتساب و مجوز اجزای ثالث: [THIRD-PARTY.md](THIRD-PARTY.md). راهنمای launcher قدیمی صرفاً در [LEGACY-LAUNCHER-README.md](LEGACY-LAUNCHER-README.md) برای سابقه نگه داشته شده است.
