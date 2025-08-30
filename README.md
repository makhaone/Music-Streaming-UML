
# 🎵 مدل‌سازی UML برای پلتفرم پخش آنلاین موسیقی

<div align="center" dir="rtl" lang="fa">

تحلیل و طراحی سیستم جامع پلتفرم پخش آنلاین موسیقی با استفاده از نمودارهای استاندارد UML

*نقشه راه کاملی برای توسعه نرم‌افزار از طریق نمایش بازیگران، قابلیت‌ها، ساختار داخلی و جریان‌های کاری سیستم*

</div>

---

## 📋 فهرست مطالب

- [🎯 قابلیت‌های کلیدی سیستم](#-قابلیتهای-کلیدی-سیستم)
- [🏗️ معماری و ساختار سیستم](#️-معماری-و-ساختار-سیستم)
- [🔄 نمونه جریان تعامل](#-نمونه-جریان-تعامل)
- [📁 فایل‌های پروژه](#-فایلهای-پروژه)

---

## 🎯 قابلیت‌های کلیدی سیستم

> Use Case Diagram - نشان‌دهنده این که چه کسانی از سیستم استفاده می‌کنند و هر کدام چه کارهایی می‌توانند انجام دهند.

![نمودار Use Case](Diagrams/Use%20Case%20Diagram.jpg)

### 👤 کاربران سیستم

<details open>
<summary><strong>🔓 کاربر مهمان (Guest User)</strong></summary>

کاربری که وارد حساب خود نشده است:

- 🔍 جستجوی موسیقی (Search Music)
- 👀 مشاهده جزئیات (View Details)
- 📝 ثبت‌نام در سیستم (Sign Up)
- 🔐 ورود به سیستم (Log In)

</details>

<details open>
<summary><strong>👤 کاربر عضو (Registered User)</strong></summary>

کاربری که پس از ورود به سیستم، می‌تواند:

- ✅ تمام قابلیت‌های کاربر مهمان
- ❤️ لایک کردن آهنگ (Like Song)
- 👥 دنبال کردن هنرمند (Follow Artist)
- 📝 ایجاد لیست پخش (Create Playlist)
- ⚙️ مدیریت لیست پخش (Manage Playlist)
- 🚪 خروج از سیستم (Log Out)

</details>

<details open>
<summary><strong>⭐ کاربر ویژه (Premium User)</strong></summary>

کاربری با اشتراک پولی که علاوه بر قابلیت‌های کاربر عضو:

- 💾 دانلود آهنگ (Download Song)
- 📱 پخش آفلاین (Offline Playback)

</details>

<details open>
<summary><strong>🎤 هنرمند (Artist)</strong></summary>

هنرمندان پس از ورود به سیستم:

- ⬆️ آپلود آهنگ یا آلبوم (Upload Song/Album)
- 🎵 مدیریت آثار موسیقی (Manage Music)
- 📊 مشاهده آمار و تحلیل‌ها (View Analytics)

</details>

<details open>
<summary><strong>⚙️ مدیر سیستم (Administrator)</strong></summary>

مدیر کل سیستم با دسترسی کامل:

- 🔐 ورود به سیستم (Log In)
- 👥 مدیریت کاربران (Manage Users)
- 🗃️ مدیریت محتوای سایت (Manage Content)
- 📈 تهیه گزارش‌های کلی (Generate Reports)
- 🚪 خروج از سیستم (Log Out)

> نکته: بر اساس نمودار Use Case، تمام روابط بین کاربران و قابلیت‌ها از نوع «include» هستند که نشان‌دهنده الزامی بودن این قابلیت‌ها برای هر نقش کاربری است.

</details>

---

## 🏗️ معماری و ساختار سیستم

> Class Diagram - ساختار داخلی و استاتیک سیستم، شامل کلاس‌های اصلی، ویژگی‌ها و روابط بین آن‌ها

![نمودار Class](Diagrams/Class%20Diagram.jpg)

### 🏛️ ساختار کلی سیستم

#### 👥 کلاس‌های کاربری
```
User (کلاس پایه)
├── userID: int
├── username: string
├── email: string
├── passwordHash: string
└── methods: login(), logout(), updateProfile()
    │
    ├── RegisteredUser
    │   └── methods: createPlaylist(), likeSong(), followArtist()
    │
    ├── PremiumUser
    │   ├── subscriptionEndDate: Date
    │   └── methods: downloadSong(), renewSubscription()
    │
    └── Artist_Class
        ├── artistName: string
        ├── biography: string
        └── methods: uploadSong(), manageAlbum(), viewAnalytics()
```
#### 🎵 کلاس‌های موسیقی

<table dir="ltr">
<tr>
<td>

🎼 Song
- songID: int
- title: string
- duration: float
- filePath: string
- releaseDate: Date

*Methods:* play(), pause(), getDetails()

</td>
<td>

💿 Album
- albumID: int
- title: string
- coverArtURL: string
- releaseYear: int

*Methods:* getSongs(), addSong(), removeSong()

</td>
</tr>
<tr>
<td>

📋 Playlist
- playlistID: int
- name: string
- creationDate: Date

*Methods:* addSong(), removeSong(), share()

</td>
<td>

🎭 Genre
- genreID: int
- name: string

*برای دسته‌بندی آهنگ‌ها*

</td>
</tr>
</table>

#### 🔗 روابط کلاس‌ها

<table dir="rtl">
<tr>
<th>رابطه</th>
<th>منبع</th>
<th>مقصد</th>
<th>نوع</th>
<th>توضیح</th>
</tr>
<tr>
<td><code>1:*</code></td>
<td><code>User</code></td>
<td><code>Playlist</code></td>
<td>Association</td>
<td>هر کاربر می‌تواند چند playlist داشته باشد</td>
</tr>
<tr>
<td><code>1:*</code></td>
<td><code>Album</code></td>
<td><code>Song</code></td>
<td>Composition</td>
<td>هر آلبوم شامل یک یا چند آهنگ</td>
</tr>
<tr>
<td><code>*:*</code></td>
<td><code>Song</code></td>
<td><code>Genre</code></td>
<td>Association</td>
<td>هر آهنگ می‌تواند چند ژانر داشته باشد</td>
</tr>
<tr>
<td><code>*:*</code></td>
<td><code>Playlist</code></td>
<td><code>Song</code></td>
<td>Aggregation</td>
<td>playlist ها شامل مجموعه‌ای از آهنگ‌ها</td>
</tr>
<tr>
<td><code>*:*</code></td>
<td><code>Song</code></td>
<td><code>Artist</code></td>
<td>Association</td>
<td>هر هنرمند ممکنه چند آهنگ داشته باشه و هر آهنگ ممکنه چند هنرمند داشته باشه</td>
</tr>
</table>

---

## 🔄 نمونه جریان تعامل

> Sequence Diagram - نمایش تعامل اشیاء و کامپوننت‌های مختلف سیستم در طول زمان

### 🎵 سناریو: پخش آهنگ توسط کاربر عضو

![نمودار Sequence](Diagrams/Sequence%20Diagram.jpg)

### 📊 مراحل تعامل:

<table dir="rtl">
<tr>
<th>مرحله</th>
<th>عمل</th>
<th>پارامتر</th>
<th>توضیح</th>
</tr>
<tr>
<td><strong>1</strong></td>
<td><code>playSongClick()</code></td>
<td>-</td>
<td>کاربر روی دکمه پخش کلیک می‌کند</td>
</tr>
<tr>
<td><strong>2</strong></td>
<td><code>handlePlayRequest()</code></td>
<td><code>songID</code></td>
<td>رابط کاربری شناسه آهنگ را به کنترلر ارسال می‌کند</td>
</tr>
<tr>
<td><strong>3</strong></td>
<td><code>checkAccess()</code></td>
<td><code>userID</code></td>
<td>کنترلر دسترسی کاربر را از طریق AuthService بررسی می‌کند</td>
</tr>
<tr>
<td><strong>4</strong></td>
<td><code>[access Granted]</code></td>
<td>-</td>
<td>تأیید دسترسی کاربر</td>
</tr>
<tr>
<td><strong>5</strong></td>
<td><code>getSongFile()</code></td>
<td><code>songID</code></td>
<td>دریافت فایل آهنگ از دیتابیس</td>
</tr>
<tr>
<td><strong>6</strong></td>
<td><code>[songFile]</code></td>
<td>-</td>
<td>بازگرداندن فایل آهنگ</td>
</tr>
<tr>
<td><strong>7</strong></td>
<td><code>play()</code></td>
<td><code>songFile</code></td>
<td>دستور پخش فایل به رابط کاربری ارسال می‌شود</td>
</tr>
</table>

---

## 📁 فایل‌های پروژه

<div align="center">

### 📂 ساختار پروژه
```
music-platform-uml/
├── 📁 diagrams/                         # نمودارهای UML
│   ├── 🖼️ use case diagram.jpg          # Use Case Diagram
│   ├── 🖼️ class diagram.jpg             # Class Diagram  
│   ├── 🖼️ sequence diagram.jpg          # Sequence Diagram
│   └── 📄 Music_Platform_Diagrams.pdf   # تمام نمودارها در یک فایل
└── 📄 README.md                        # این فایل
```
### 📋 نمودارهای موجود:

<table dir="rtl">
<tr>
<th>نمودار</th>
<th>فایل</th>
<th>توضیحات</th>
</tr>
<tr>
<td><strong>Use Case</strong></td>
<td><code>use case diagram.jpg</code></td>
<td>نمایش بازیگران و قابلیت‌های سیستم</td>
</tr>
<tr>
<td><strong>Class</strong></td>
<td><code>class diagram.jpg</code></td>
<td>ساختار کلاس‌ها و روابط آن‌ها</td>
</tr>
<tr>
<td><strong>Sequence</strong></td>
<td><code>sequence diagram.jpg</code></td>
<td>جریان تعامل در سناریو پخش آهنگ</td>
</tr>
<tr>
<td><strong>کامل</strong></td>
<td><code>Music_Platform_Diagrams.pdf</code></td>
<td>تمام نمودارها در یک فایل PDF</td>
</tr>
</table>

</div>

---
