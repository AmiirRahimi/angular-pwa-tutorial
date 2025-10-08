# آموزش PWA با Angular

یک اپلیکیشن وب پیشرفته (Progressive Web App) ساده با استفاده از Angular که قابلیت‌های زیر را پیاده‌سازی می‌کند:

## ویژگی‌ها

### ✅ حالت آفلاین
- نمایش اعلان بصری هنگام قطع اتصال اینترنت
- امکان رفرش و کارکرد اپلیکیشن حتی در حالت آفلاین با استفاده از Service Worker

### ✅ نصب اپلیکیشن
- دکمه نصب اپلیکیشن (Add to Home Screen)
- تجربه کاربری شبیه به اپلیکیشن‌های native

### ✅ رابط کاربری ساده
- نمایش وضعیت آنلاین/آفلاین به صورت بصری
- طراحی responsive و کاربرپسند
- پشتیبانی از زبان فارسی (RTL)

### ✅ Service Worker
- کش کردن فایل‌های استاتیک
- پشتیبانی از کارکرد آفلاین
- بروزرسانی خودکار

## پیش‌نیازها

- Node.js (نسخه 18 یا بالاتر)
- npm یا yarn

## نحوه اجرای پروژه

### نصب وابستگی‌ها
```bash
npm install
```

### اجرای سرور توسعه
```bash
npm start
```

اپلیکیشن در آدرس `http://localhost:4200` اجرا خواهد شد.

### ساخت برای production
```bash
npm run build -- --configuration production
```

فایل‌های ساخته شده در پوشه `dist/angular-pwa-tutorial` قرار خواهند گرفت.

### تست PWA

برای تست قابلیت‌های PWA:

1. اپلیکیشن را در مرورگر باز کنید
2. Developer Tools را باز کنید (F12)
3. به تب Application > Service Workers بروید
4. مطمئن شوید Service Worker فعال است
5. اتصال اینترنت را قطع کنید و صفحه را رفرش کنید

## ساختار پروژه

```
src/
├── app/
│   ├── app.html          # قالب اصلی اپلیکیشن
│   ├── app.css           # استایل‌های اپلیکیشن
│   ├── app.ts            # کامپوننت اصلی
│   └── app.config.ts     # تنظیمات Angular
├── index.html            # فایل HTML اصلی
└── styles.css            # استایل‌های عمومی

public/
├── manifest.webmanifest  # تنظیمات PWA
└── icons/                # آیکون‌های PWA
```

## تکنولوژی‌های استفاده شده

- **Angular 20** - فریمورک اصلی
- **@angular/pwa** - بسته PWA
- **Angular Service Worker** - برای قابلیت آفلاین
- **TypeScript** - زبان برنامه‌نویسی
- **CSS** - استایل‌دهی

## نحوه کارکرد

### تشخیص آنلاین/آفلاین
اپلیکیشن از event listenerهای `online` و `offline` برای تشخیص وضعیت اتصال استفاده می‌کند.

### نصب PWA
با استفاده از `beforeinstallprompt` event، امکان نصب اپلیکیشن روی دستگاه فراهم می‌شود.

### Service Worker
Angular Service Worker فایل‌های ضروری را کش کرده و امکان کارکرد آفلاین را فراهم می‌کند.

## آموزش گام به گام

1. **ایجاد پروژه Angular با PWA**
   ```bash
   ng new my-pwa-app --routing --style=css
   cd my-pwa-app
   ng add @angular/pwa
   ```

2. **پیاده‌سازی تشخیص آنلاین/آفلاین**
   ```typescript
   // در کامپوننت اصلی
   ngOnInit() {
     window.addEventListener('online', () => this.isOnline.set(true));
     window.addEventListener('offline', () => this.isOnline.set(false));
   }
   ```

3. **اضافه کردن دکمه نصب**
   ```typescript
   // مدیریت beforeinstallprompt event
   window.addEventListener('beforeinstallprompt', (e) => {
     e.preventDefault();
     this.deferredPrompt = e;
     this.canInstall.set(true);
   });
   ```

4. **تنظیمات Service Worker**
   فایل `ngsw-config.json` را برای تعیین استراتژی کش ویرایش کنید.

## دمو

برای مشاهده اپلیکیشن، فایل‌های `dist` را روی یک سرور HTTP اجرا کنید:

```bash
cd dist/angular-pwa-tutorial/browser
python3 -m http.server 8080
```

سپس به آدرس `http://localhost:8080` بروید.
