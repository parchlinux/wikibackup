---
title: راه‌اندازی محیط توسعه آردویینو در پارچ
description: راهنمای نصب و استفاده از پلتفرم آردوینو در پارچ لینوکس
published: true
date: 2026-04-20T11:52:56.863Z
tags: پارچ لینوکس, ide, ادیتور, آردویینو, توسعه
editor: markdown
dateCreated: 2026-04-20T11:31:44.420Z
---


# آردوینو

آردوینو یک پلتفرم پروتوتایپینگ الکترونیک منبع‌باز است که بر پایه سخت‌افزار و نرم‌افزار انعطاف‌پذیر و آسان برای استفاده ساخته شده است. این پلتفرم برای هنرمندان، طراحان، علاقه‌مندان و هر کسی که به ایجاد اشیاء یا محیط‌های تعاملی علاقه‌مند است، طراحی شده است.

پس از اتصال و پیکربندی، کاربر می‌تواند عملیات خواندن/نوشتن را از طریق اتصال سریال برقرارشده انجام دهد. مثال‌ها شامل رابط از طریق UART با استفاده از یک برنامه نظارت سریال یا برنامه‌ریزی میکروکنترلر است. نوشتن، کامپایل و آپلود کد شما با استفاده از Arduino IDE رسمی تسهیل می‌شود که در مخزن رسمی پارج موجود است. به همین ترتیب کاربر می‌تواند از کامپایلر و برنامه‌نویس دلخواه خود برای برنامه‌ریزی میکروکنترلر استفاده کند.

## نصب

* بسته `arduino-cli` را برای CLI رسمی نصب کنید.
* بسته `arduino-ide-bin` را از مخزن پارچ برای رابط گرافیکی رسمی نصب کنید.
* دسترسی کاربر به دستگاه را فعال کنید (بخش [دسترسی به سریال](#دسترسی-به-سریال)).
* ممکن است نیاز به بارگذاری ماژول `cdc-acm` داشته باشید.

### Arduino IDE 1.x

بخش زیر فقط برای نسخه ۱.x محیط توسعه اعمال می‌شود. با این حال ممکن است بتوان برخی از این موارد را برای محیط جدید تطبیق داد.

#### بردهای AVR

برای استفاده از بردهای AVR مانند Arduino Uno می‌توانید بسته `arduino-avr-core` را به‌صورت اختیاری نصب کنید تا از avr-gcc upstream آرچ لینوکس به جای avr-core قدیمی bundled استفاده کنید. اگر هنوز می‌خواهید از arduino-core قدیمی استفاده کنید، باید آن را در Board Manager نصب کنید. همیشه می‌توانید بین هسته‌های مختلف از منوی Tools > Board تغییر دهید.

#### Pinoccio Scout

Pinoccio Scouts نیز می‌تواند با Arduino IDE برنامه‌ریزی شود. دستورالعمل‌ها را [اینجا](https://web.archive.org/web/20160611045134/https://pinocc.io/solo) پیدا کنید.

جایگزین، می‌توانید بسته `arduino-pinoccio` را از AUR نصب کنید.

#### Intel Galileo

برای استفاده از بردهای Intel Galileo با آرچ لینوکس، Arduino IDE را نصب کنید و بسته ابزار Galileo را از طریق Tools > Board > Boards Manager دانلود کنید.

برای رفع مشکل نصب، می‌توانید این پست گیت‌هاب را دنبال کنید.

### Arduino IDE 1.x یا 2.x

این مراحل باید برای هر دو نسخه محیط توسعه معتبر باشد.

#### بردهای AVR

بردهای AVR به‌طور خودکار توسط نسخه ۲.x محیط توسعه نصب می‌شوند، با این حال در هر دو نسخه ۱.x و ۲.x بردهای AVR را می‌توان از بخش Board Manager مدیریت کرد.

#### SparkFun

برای استفاده از بردهای SparkFun مانند Pro Micro نیاز به دانلود تعریف‌های برد آن‌ها دارید. اطلاعات بیشتر [اینجا](https://learn.sparkfun.com/tutorials/pro-micro--fio-v3-hookup-guide/installing-mac--linux) و [اینجا](https://github.com/sparkfun/Arduino_Boards).

#### RedBear Duo

ممکن است نیاز به نصب بسته `perl-archive-zip` داشته باشید وگرنه خطای missing crc32 دریافت خواهید کرد.

## پیکربندی

بیشتر بردهای آردوینو دارای پورت USB هستند که برای برقراری اتصال سریال استفاده می‌شود. این اتصال سریال به کاربر اجازه برنامه‌ریزی برد را می‌دهد. میکروکنترلر اصلی اکثر آردوینوها رابط USB ندارد. بنابراین برد معمولاً با یک چیپ USB-to-serial بین میکروکنترلر اصلی و پورت USB مجهز است.

برای برقراری اتصال سریال از طریق USB، بیشتر بردهای آردوینو اصلی با میکروکنترلر ATmega دیگر (مثلاً ATmega16U2) یا مبدل FTDI USB UART (مثلاً FT232RL) مجهز هستند. هر دو این چیپ‌ها خود را به‌عنوان دستگاه ACM از طریق USB ثبت می‌کنند و بنابراین لینوکس از ماژول `cdc_acm` استفاده خواهد کرد. آردوینو سپس به صورت `/dev/ttyACMx` ظاهر می‌شود.

بردهای آردوینو غیراصلی روی چیپ رابط صرفه‌جویی می‌کنند. آن‌ها معمولاً با چیپ WCH CH340x چینی یا تقلبی از مدل‌های ذکرشده مجهز هستند. CH340x خود را به‌عنوان دستگاه UART اختصاصی از طریق USB نشان می‌دهد. در اینجا ماژول `ch341` استفاده می‌شود که چنین آردوینوهایی را به صورت `/dev/ttyUSBx` نشان می‌دهد. این الگوی نام‌گذاری را می‌توان با تغییر قوانین udev سفارشی کرد.

برخی برد‌ها ممکن است با میکروکنترلر اصلی که خود رابط USB native را expose می‌کند مجهز باشند. چه برد چیپ رابط اختصاصی داشته باشد یا نه، بردهای اصلی از کارخانه با boot loader مناسب پیش‌نصب‌شده عرضه می‌شوند. چنین boot loaderهایی به‌طور خودکار اتصال سریال از طریق USB را پس از اتصال برقرار می‌کنند.

> **نکته:** برخی برد‌ها، به‌ویژه Pro Mini، اصلاً USB را expose نمی‌کنند و باید با سخت‌افزار اضافی برنامه‌ریزی شوند.

> **نکته:** ممکن است مفید باشد که پیام‌های کرنل را با دستور `dmesg` هنگام وصل کردن برد نظارت کنید. اگر اتصال موفق برقرار شده باشد، پورت اختصاص‌یافته را می‌توانید آنجا بخوانید.

### دسترسی به سریال

برای بردهایی که UART را از طریق USB expose می‌کنند، لازم است دسترسی خواندن/نوشتن به پورت سریال برای کاربران عادی مجاز شود. همان‌طور که در بخش Udev#Allowing regular users to use devices توضیح داده شده، فایلی با محتوای زیر ایجاد کنید:

```udev
ACTION!="remove", SUBSYSTEMS=="usb-serial", TAG+="uaccess"
ACTION!="remove", SUBSYSTEMS=="tty", TAG+="uaccess"
```

سپس قوانین udev را دوباره بارگذاری کنید و دستگاه آردوینو را دوباره وصل کنید. قبل از آپلود به آردوینو، مطمئن شوید پورت سریال، نوع برد و پردازنده درست از منوی Tools در نسخه ۱.x و گزینه Select board (در بالای IDE) در نسخه ۲.x تنظیم شده است.

> **نکته:** به یاد داشته باشید که هر برنامه نظارت سریال را هنگام آپلود کد بسته نگه دارید تا پورت برای برنامه‌نویس آزاد شود.

## ارتباط با دستگاه

### استفاده از CLI

مستندات بیشتر درباره `arduino-cli` را می‌توانید در [وب‌سایت رسمی arduino-cli](https://arduino.github.io/arduino-cli/1.4/getting-started/) پیدا کنید.

ابتدا بردهای متصل به کامپیوتر را لیست کنید:

```bash
arduino-cli board list
```

# مثال خروجی
```
Port         Protocol Type                   Board Name                  FQBN                          Core
/dev/ttyUSB0 serial   Serial Port (USB)       Arduino/Genuino MKR1000     arduino:samd:mkr1000          arduino:samd
/dev/ttyUSB1 serial   Serial Port (USB)       Unknown
```

سپس، پس از ایجاد sketch، آن را کامپایل کنید:

```bash
arduino-cli compile --fqbn <fully_qualified_board_name> MySketch
```

در نهایت sketch کامپایل‌شده را آپلود کنید:

```bash
arduino-cli upload -p <port> --fqbn <fully_qualified_board_name> MySketch
```

اگر دستور upload با خطای عدم مجوز کافی شکست خورد، مطمئن شوید کاربران عادی دسترسی خواندن/نوشتن به پورت‌های USB دارند. اگر با DEVICE_BUSY شکست خورد، مطمئن شوید هیچ برنامه دیگری مانند `arduino-ide-bin` در حال استفاده از دستگاه نیست.

### stty

آماده‌سازی:

```bash
stty -F /dev/ttyACM0 cs8 9600 ignbrk -brkint -imaxbel -opost -onlcr -isig -icanon -iexten -echo -echoe -echok -echoctl -echoke noflsh -ixon -crtscts
```

ارسال دستورات از طریق ترمینال بدون خط جدید بعد از دستور:

```bash
echo -n "Hello World" > /dev/ttyACM0
```

> **نکته:** چون ویژگی autoreset روی اتصال سریال به‌طور پیش‌فرض در اکثر برد‌ها فعال است، اگر می‌خواهید مستقیماً با برد خود با دستور آخر ارتباط برقرار کنید (به‌جای emulator ترمینال مانند Arduino IDE، screen یا picocom) باید این ویژگی را غیرفعال کنید. اگر برد Leonardo دارید، این مورد شامل شما نمی‌شود چون autoreset ندارد. اگر برد Uno دارید، یک خازن ۱۰ µF بین پین‌های RESET و GND وصل کنید. اگر برد دیگری دارید، یک مقاومت ۱۲۰ اهم بین RESET و ۵V وصل کنید. برای جزئیات بیشتر به [این صفحه](https://playground.arduino.cc/Main/DisablingAutoResetOnSerialConnection) مراجعه کنید.

خواندن خروجی آردوینو:

```bash
cat /dev/ttyACM0
```

### Arduino-Builder

> **توجه:** این بخش قبل از انتشار نسخه ۲.x محیط توسعه نوشته شده و توصیف توابع ممکن است نادرست باشد. در صفحه GitHub برای Arduino-Builder اعلام شده که این ابزار در حال phasing out به نفع Arduino CLI است.

شما همچنین می‌توانید sketchهای آردوینو را با ابزار خط فرمان `arduino-builder` بسازید. برای استفاده از `arduino-avr-core` ارائه‌شده همراه با avr-gcc و avrdude upstream، باید یک فایل تنظیمات کوچک ایجاد کنید:

```json
{
    "fqbn": "archlinux-arduino:avr:uno",
    "hardwareFolders": "/usr/share/arduino/hardware",
    "toolsFolders": "/usr/bin"
}
```

کامپایل یک sketch:

```bash
arduino-builder -build-options-file build.options.json blink.ino
```

یا همه گزینه‌ها را مستقیم از خط فرمان پاس دهید:

```bash
arduino-builder -fqbn archlinux-arduino:avr:uno -hardware /usr/share/arduino/hardware -tools /usr/bin blink.ino
```

## جایگزین‌های IDE

### Arduino-CMake

با استفاده از [Arduino-CMake-Toolchain](https://github.com/a9183756-gh/Arduino-CMake-Toolchain) و [CMake](https://www.cmake.org/cmake/resources/software.html) می‌توانید firmware آردوینو را از خط فرمان با چندین سیستم ساخت بسازید. CMake به شما اجازه می‌دهد سیستم ساخت مورد نیاز خود را تولید کنید و از ابزارهایی که دوست دارید استفاده کنید. می‌تواند هر نوع سیستم ساخت را تولید کند؛ از Makefile ساده تا پروژه‌های کامل برای Eclipse، Visual Studio، Xcode و غیره.

الزامات: `cmake`، گروه `arduino`، `avr-gcc`، `avr-binutils`، `avr-libc`، `avrdude`.

### Makefile

به جای استفاده از Arduino IDE می‌توانید از ویرایشگر دیگری و یک Makefile استفاده کنید.

یک دایرکتوری برای برنامه‌ریزی آردوینو تنظیم کنید و Makefile را داخل آن کپی کنید. نسخه‌ای از Makefile را می‌توانید از [این قالب گیت‌هاب](https://github.com/tomswartz07/arduino-makefile) بگیرید.

باید آن را کمی برای تنظیمات خود تغییر دهید. makefile تقریباً خودتوضیحی است. خطوطی که ممکن است نیاز به ویرایش داشته باشید:

```
PORT = معمولاً /dev/ttyUSBx (پورت سریال USB که آردوینو به آن وصل است)
TARGET = نام sketch شما
ARDUINO = /usr/share/arduino/lib/targets/arduino
```

بسته به توابع کتابخانه‌ای که در sketch فراخوانی می‌کنید، ممکن است نیاز به کامپایل بخش‌هایی از کتابخانه داشته باشید. برای این کار SRC و CXXSRC را ویرایش کنید تا کتابخانه‌های مورد نیاز را شامل شود.

حالا باید بتوانید با دستور `make && make upload` sketch را روی برد اجرا کنید.

### Arduino-mk

[arduino-mk](https://github.com/sudar/Arduino-Makefile) رویکرد Makefile جایگزین دیگری است. به کاربران اجازه می‌دهد Makefile محلی داشته باشند که Arduino.mk را شامل شود.

برای Arduino ۱.۵، Makefile محلی زیر را امتحان کنید (چون ساختار دایرکتوری کتابخانه Arduino ۱.۵ کمی متفاوت است):

```
ARDUINO_DIR = /usr/share/arduino
ARDMK_DIR = /usr/share/arduino
AVR_TOOLS_DIR = /usr
AVRDUDE_CONF = /etc/avrdude.conf
ARDUINO_CORE_PATH = /usr/share/arduino/hardware/archlinux-arduino/avr/cores/arduino
ARDUINO_PLATFORM_LIB_PATH = /usr/share/arduino/hardware/archlinux-arduino/avr/libraries
BOARDS_TXT = /usr/share/arduino/hardware/archlinux-arduino/avr/boards.txt
ARDUINO_VAR_PATH = /usr/share/arduino/hardware/archlinux-arduino/avr/variants
BOOTLOADER_PARENT = /usr/share/arduino/hardware/archlinux-arduino/avr/bootloaders
BOARD_TAG = uno
ARDUINO_LIBS =
include /usr/share/arduino/Arduino.mk
```

در برخی موارد ممکن است نیاز به نصب `avr-libc` و `avrdude` داشته باشید.

### Scons

با استفاده از [scons](https://www.scons.org/) همراه با [arscons](https://github.com/suapapa/arscons) بسیار آسان است که پروژه‌های آردوینو را از خط فرمان کامپایل و آپلود کنید. Scons بر پایه پایتون است و برای استفاده از رابط سریال به python-pyserial نیاز دارید. بسته‌های `python-pyserial`، `scons` و گروه `arduino` را نصب کنید.

دایرکتوری پروژه بسازید (مثلاً test)، سپس فایل پروژه آردوینو با همان نام دایرکتوری و پسوند `.ino` ایجاد کنید. اسکریپت [SConstruct](https://github.com/suapapa/arscons/blob/master/SConstruct) را از arscons بگیرید و داخل دایرکتوری بگذارید. آن را بررسی و در صورت نیاز ویرایش کنید. سپس اجرا کنید:

```bash
scons          # ساخت پروژه
scons upload   # آپلود پروژه به آردوینو
```

### PlatformIO

[PlatformIO](https://docs.platformio.org/en/latest/core/quickstart.html) ابزاری پایتون برای ساخت و آپلود sketchها برای چندین پلتفرم سخت‌افزاری است. در زمان نوشتن این متن، بردهای مبتنی بر Arduino/AVR، TI MSP430 و TI TM4C12x پشتیبانی می‌شوند. در آینده نزدیک نویسنده قصد دارد تابعی برای جستجو و شامل کردن مستقیم کتابخانه‌ها از GitHub اضافه کند.

#### نصب

بسته `platformio-core` را نصب کنید.

#### استفاده

موارد زیر بر اساس [راهنمای سریع رسمی PlatformIO](https://docs.platformio.org/en/latest/core/quickstart.html) است که نحوه ایجاد و آپلود یک پروژه نمونه را نشان می‌دهد.

یک دایرکتوری جدید برای پروژه platformio بسازید و داخل آن بروید.

سپس دستور زیر را برای مقداردهی اولیه پروژه برای یک برد خاص (مثلاً megaatmega2560) اجرا کنید:

```bash
pio project init --board megaatmega2560
```

این دستور toolchain و وابستگی‌ها را دانلود می‌کند و فایل `platformio.ini` را ایجاد می‌کند:

```ini
; PlatformIO Project Configuration File
[env:megaatmega2560]
platform = atmelavr
board = megaatmega2560
framework = arduino
```

کد را در فایل `main.cpp` داخل پوشه `src/` اضافه کنید (مانند مثال راهنمای سریع).

سپس کد را کامپایل و آپلود کنید:

```bash
pio run
pio run --target upload
```

### Emacs

امکان پیکربندی Emacs به‌عنوان محیط توسعه وجود دارد.

بسته `emacs-arduino-mode-git` را از AUR نصب کنید تا حالت `arduino-mode` فعال شود.

به فایل init اضافه کنید:

```emacs
;; arduino-mode
(require 'cl)
(autoload 'arduino-mode "arduino-mode" "Arduino editing mode." t)
(add-to-list 'auto-mode-alist '("\.ino$" . arduino-mode))
```

می‌توانید sketchها را با Arduino-mk (بالا ببینید) و دستور `M-x compile` و `make upload` کامپایل و آپلود کنید.

منبع اصلی: [اینجا](https://www.emacswiki.org/emacs/ArduinoSupport).

## عیب‌یابی

### نام‌گذاری ثابت دستگاه‌های آردوینو

اگر بیش از یک آردوینو دارید ممکن است متوجه شده باشید که نام‌های `/dev/ttyUSB[0-9]` به ترتیب اتصال اختصاص داده می‌شوند. در IDE این مسئله زیاد مشکل‌ساز نیست، اما وقتی نرم‌افزار خود را برای ارتباط با پروژه آردوینو در پس‌زمینه نوشته‌اید، آزاردهنده است. از قوانین udev زیر برای ایجاد symlink ثابت استفاده کنید:

```udev
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", SYMLINK+="sensors/ftdi_%s{serial}"
```

آردوینوهای شما تحت نام‌هایی مانند `/dev/sensors/ftdi_A700dzaF` در دسترس خواهند بود. اگر بخواهید نام‌های معنادارتر هم می‌توانید بدهید:

```udev
SUBSYSTEMS=="usb", KERNEL=="ttyUSB[0-9]*", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A700dzaF", SYMLINK+="arduino/nano"
```

برای اعمال تغییرات، آردوینو را unplug/replug کنید یا دستور `udevadm trigger` را اجرا کنید.

جفت‌های idVendor/idProduct رایج را می‌توانید در فایل `/usr/share/arduino/hardware/archlinux-arduino/avr/boards.txt` پیدا کنید. توجه کنید که برخی از آن‌ها (به‌ویژه FTDI) منحصر به پلتفرم آردوینو نیستند. استفاده از ویژگی `serial` راه خوبی برای تمایز دستگاه‌هاست.

### خطای Error opening serial port

ممکن است پورت سریال را هنگام شروع IDE ببینید ولی LEDهای TX/RX هنگام آپلود کاری نکنند. ممکن است قبلاً baudrate را در serial monitor به مقداری تغییر داده باشید که IDE دوست ندارد. فایل `~/.arduino/preferences.txt` را ویرایش کنید و `serial.debug_rate` را به سرعت دیگری مثل ۱۱۵۲۰۰ تغییر دهید.

### کار با Uno/Mega2560

آردوینو Uno و Mega2560 دارای رابط USB onboard (Atmel 8U2) هستند که داده سریال را قبول می‌کند، بنابراین از طریق `/dev/ttyACM0` که توسط ماژول cdc-acm ایجاد می‌شود، دسترسی دارند.

firmware 8U2 ممکن است نیاز به به‌روزرسانی داشته باشد. برای جزئیات بیشتر و راه‌حل به [این بحث](https://forum.arduino.cc/t/easy-to-brick-arduino-uno-on-linux/47039) مراجعه کنید (پاسخ شماره ۱۱). تصویر توضیح DFU mode در BBS قدیمی آردوینو حالا read-only است؛ اگر حساب ندارید به [این لینک scribd](https://www.scribd.com/doc/45913857/Arduino-UNO) مراجعه کنید.

برای تست عملکرد Uno، آن را در حالت loopback قرار دهید و کاراکترها را با baudrate ۱۱۵۲۰۰ در serial monitor تایپ کنید. باید echo شود. برای loopback، پین‌های ۰ و ۱ را short کنید و reset را نگه دارید یا GND را به RESET short کنید.

### شناسایی نشدن پورت USB با کلون‌های ارزان چینی Mega2560

درایور آن را نصب کنید: `i2c-ch341-dkms` از AUR.

### شکست آپلود: programmer is not responding

تغییر تنظیم پردازنده از `ATmega328P` به `ATmega328P (Old Bootloader)` (در Tools→Processor محیط IDE) ممکن است مشکل را حل کند.

### تداخل پورت سریال با brltty

اگر پورت `/dev/ttyUSB*` دیده نشود و journal حاوی موارد زیر باشد:

```
usb 3-1: usbfs: interface 0 claimed by ch341 while 'brltty' sets config #1
ch341-uart ttyUSB0: ch341-uart converter now disconnected from ttyUSB0
```

بسته `brltty` را حذف کنید. برای جزئیات بیشتر به [این بحث manjaro](https://forum.manjaro.org/t/cant-connect-serial-port-error-ch341-uart-disconnected-from-ttyusb0/87208) مراجعه کنید.

### شکست آپلود با Nano RP2040 Connect

اگر خطای زیر را دیدید:

```
Failed uploading: uploading error: exit status 1
```

بخش [دسترسی به سریال](#دسترسی-به-سریال) را انجام نداده‌اید؛ دستورالعمل‌های آن را اجرا کنید تا دسترسی خواندن/نوشتن برای کاربران مجاز شود.

## همچنین ببینید

* [وب‌سایت رسمی آردوینو](https://www.arduino.cc/)
* [راهنمای شروع کار با IDE نسخه ۲](https://docs.arduino.cc/software/ide-v2/tutorials/getting-started-ide-v2)
* [چگونه مسیر دستگاه منحصربه‌فرد برای آردوینو/FTDI بگیریم](https://answers.ros.org/question/9097/how-can-i-get-a-unique-device-path-for-my-arduinoftdi-device/)
```