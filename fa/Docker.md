---
title: داکر
description: داکر یک ابزار برای ایزوله سازی (Containerization) برای توسعه تمیز تر و راحت برای توسعه دهندگان است
published: true
date: 2024-08-12T07:20:23.121Z
tags: داکر, container
editor: markdown
dateCreated: 2024-07-23T16:21:30.996Z
---




# توضیحات

docker ابزاری برای ایزوله سازی (Containerization) است که امکان اشتراک گذاری محیط توسعه را به صورت container در هر سیستم عاملی می دهد, این کار موجب تسریع زمان توسعه و اشتراک گذاری محیط بین اعضای تیم می شود, همچنین از تداخل وابستگی ها جلوگیری می کند، چرا که تمام وابستگی ها در container و به صورت ایزوله نگه داری میشود.

# تاریخچه
قبل از ایجاد مفهموم container و ایزوله سازی محیط, مجازی سازی (Virtualization) یکی از اصلی ترین راهکار ها برای جدا کردن محیط توسعه از سیستم میزبان بود, کاربر با اختصاص دادن cpu ,memory و hard space تایین می کرد چه مقدار منابع از سیستم میزبان به سیستم مجازی تعلق دارد, اما این راهکار چندان مناسب نبود چرا که مقدار قابل توجهی از منابع به سیستم عامل مجازی تعلق میگرفت و سرعت پردازش نسبت به سیستم میزبان کند تر بود.

اما با ورود مفهوم container, موجب شد که ایزوله سازی و جدا کردن محیط های مختلف به صورت کم هزینه تر و با منابع کمتری صورت بپذیرد. 

docker یکی از ابزار هایی است که میتوان برای ساخت و مدیریت container و ... از آن استفاده کرد, ممکن است نیاز داشته باشد که محیط توسعه/محصول خودتان را با دیگر اعضا به اشتراک بگذارید, docker این امکان را فراهم می کند تا با اشتراک گذاری فایل اسکلت container خود (image) این کار را تسریع کنید, همچنین افراد دیگر نگرانی جهت بر طرف کردن وابستگی ها ندارند چرا که تمام انها از قبل حل شده است.

# [نصب و راه اندازی](https://itsfoss.com/install-docker-arch-linux/) 

سایت مرجع [docker](https://docs.docker.com/engine/install/) اموزش کاملی را جهت نصب در سیستم های لینوکسی پوشش داده است اما توزیع های مبتبی بر ارچ به صورت رسمی پوشش داده نشده است و نصب آن به صورت unstable است.

1- ترمینال را باز کنید و با استفاده از مدیر بسته docker را نصب کنید

```
sudo pacman -S docker
```
> اگر با خطای ```docker not found``` مواجه شدید مطمئن شوید مخازن خود را بروزرسانی کرده اید با دستور ```sudo pacman -Syu``` می توانید از بروز بودن مخازن خود اطمینان حاصل کنید

2- اگر از systemd به عنوان init استفاده می کنید با دستور زیر سرویس docker را فعال کنید:

```
sudo systemctl enable --now docker.service
```

3- در این مرحله باید نام کاربری خودتان را به گروه docker اضافه کنید:

> برای اعمال تغییرات یکبار از سیستم logout کنید یا از دستور ```newgrp docker``` استفاده کنید.

```
sudo usermod -aG docker $USER
```

4- حالا می توانید با run کردن hello-world که یک image است از درست کار کردن docker اطمینان حاصل کنید.

```
docker run hello-world
```

دستور run همانطور که از اسم آن پیداست برای اجرا کردن image ها می باشد,  image ها اسلکت هایی هستند که container ها از آنها ساخته میشوند, مجموعه از فایل ها و پیکربندی هایی از پیش تعریف شده که container بر اساس آنها ساخته میشود.

برای لیست کردن image های موجود در سیستم خودتان میتوانید از ```docker images``` استفاده کنید

برای لیست کردن container های فعال میتوانید از ```docker ps``` استفاده کنید.

# [Docker hub](https://hub.docker.com/)

[Docker hub](https://hub.docker.com/) به عنوان مخزن پیشفرض docker برای دانلود و اپلود image ها مورد استفاده قرار می گیرد.

به عنوان مثال ممکن است بخواهید از nginx به عنوان webserver خود استفاده کنید, میتوانید image nginx را از docker hub دریافت کنید و از روی آن یک container ایجاد کنید.

1- با استفاده از ```docker login``` به حساب کاربری خود وارد شوید.
> اگر حساب کاربری ندارید, یکی [ایجاد](https://app.docker.com/signup?) کنید

2- میتوانید با استفاده از ```docker pull nginx```  اخرین ورژن nginx را از docker hub دریافت کنید. 

> متاسفانه docker hub در ایران تحریم است, در صورتی که با خطای 403 یا connection time out مواجه شدید, به احتمال زیاد مشکل از تحریم ها می باشد, میتوانید با خواندن [رفع تحریم](#رفع-تحریم) این مشکل را حل کنید.

> وب سرور nginx در docker hub [مستندات کاملی](https://wiki.parchlinux.com/fa/Docker) را درباره نحوه کار با image و container جمع اوری کرده است. 

بعد از اتمام دانلود image میتوانید با استفاده از دستور ```run``` یک container برای nginx ایجاد کنید

```
docker run --name some-nginx -p 8080:80 -v /some/content:/usr/share/nginx/html:ro -d nginx
```

> اگر از mirror  های دیگری مانند focker.ir برای دانلود image استفاده کرده اید باید از نام focker.ir/nginx به جای nginx استفاده کنید 

```
docker run --name some-nginx -p 8080:80 -v /some/content:/usr/share/nginx/html:ro -d focker.ir/nginx
```

1- پرچم ```name--``` برای اختصاص یک نام به container استفاده میشود که در این مثال some-nginx می باشد
2- پرچم ```v-``` یا ```volume--``` برای اشتراک گذاری یک (مسیر از سیستم میزبان) با (یک مسیر در کانتینر) استفاده میشود 

> در این مثال مسیر ```/some/content``` از سیستم میزبان (اصلی) با ```/usr/share/nginx/html``` در container مشترک شده است, به عنوان مثال اگر فایلی به نام name.txt را در سیستم میزبان (اصلی) در مسیر ```/some/content``` ایجاد کنید, بعد از ورود به container می توانید همان فایل را در ادرس ```/usr/share/nginx/html``` مشاهده کنید. 

> در اخرین بخش مقدار volume که با ```:``` جدا شده اند, ```ro``` به معنا تنها خواندی (readonly) می باشد, اگر مقدار آن را rw قرار دهید خواندنی و نوشتنی (read and write) خواهد بود.

4- پرچم ```p-``` یا ```port--``` یک پورت از سیستم میزبان را به یک پورت از container متصل می کند

> در این مثال پورت ```8080``` از سیستم میزبان (اصلی) به پورت ```80``` container متصل شده است.

3- پرچم ```d-```  به معنای اجرای پروسه در background می باشد.

# رفع تحریم

برای رفع تحریم می توان از راهکار های زیر استفاده کرد:

1- استفاده از dns 
2- استفاده از mirror های دیگر
3- استفاده از ابزار های proxy client همانند [hiddify](https://hiddify.com/) و [nekoray](https://github.com/MatsuriDayo/nekoray) ...


## استفاده از mirror های دیگر

ساده ترین روش برای دور زدن تحریم‌ها، استفاده از مخازن دیگر برای دانلود image ها است (همانند ایران‌سرور، focker.ir و ابراروان).

### 1. ایران‌سرور
می توانید از طریق مستند ایران سرور اقدام به تغییر به صورت کامل برای دریافت راحت این کار انجام بدهید و یا به‌طور خلاصه می‌توانید با افزودن آدرس دامنه https://mirror.iranserver.com/docker/ به ابتدای نام image، از مخازن ایران‌سرور برای دانلود image استفاده کنید:
```bash
docker pull mirror.iranserver.com/docker/<ImageName>
```

این آدرس به شما این امکان را می‌دهد که از طریق سرورهای ایران‌سرور، image مورد نظر خود را با سرعت و بدون تحریم دریافت کنید.

### 2. ابراروان
ابراروان یک [مستند](https://www.arvancloud.ir/fa/dev/docker) جامع در این باز منتشر کرده است. اما به طور خلاصه می‌توانید تنها با اضافه کردن آدرس دامنه `/docker.arvancloud.ir` به اول اسم image از مخازن ابراروان برای دانلود image استفاده کنید:

```bash
docker pull docker.arvancloud.ir/<ImageName>
```

### 3. focker.ir
برای استفاده از focker.ir نیز به همین صورت است:

```bash
docker pull focker.ir/<ImageName>
```




## استفاده از dns 

تعدادی dns داخلی به جهت رفع تحریم ها در دسترس است که معروف ترین انها  [shecan](https://shecan.ir/), [403](https://403.online/) و [begzar](https://begzar.ir/) است. 

### begzar

```
etc/resolv.conf/#
 nameserver 185.55.226.26
nameserver 185.55.225.25
```

### 403

```
etc/resolv.conf/#
 nameserver 10.202.10.202
nameserver 10.202.10.102
```

### shecan

```
etc/resolv.conf/#
 nameserver 178.22.122.100
nameserver 185.51.200.2
``` 

#   [docker compose](https://docs.docker.com/compose/)

docker compose یکی از قدرتمند ترین دستور های docker است که امکان می دهد در صورت استفاده از چند container برای یک هدف مشترک, config های انها را در یک فایل yaml تعریف کنید و هر بار مجبور به تایپ کردن آنها در ترمینال یا نوشتن دستی آنها در script نباشید و در نهایت با اجرا تنها یک دستور تمامی container ها را اجرا کنید.



# ابزار ها

## پرچم ها

داکر مجوعه از پرچم ها را ارائه می دهد:

### --help

نحوه استفاده از docker و دستورات را نمایش می دهد.

### -D, --debug=true|false

حالت دیباگ را فعال با غیر فعال می کند

### -H, --host=[unix:///var/run/docker.sock]

ادرس socket را برای سرویس docker مشخص می کند

### -l, --log-level=debug|info|warn|error|fatal

سطح لاگ را مشخص می کند (به صورت پیشفرض info است)
### --tls=true|false

استفاده از پکت ها tls را مشخص میکند (پیشفرض false)

### --tlscacert=~/.docker/ca.pem

بررسی می کند certs ها حتما توسط CA مشخص شده امضا شده باشد

### --tlscert=~/.docker/cert.pem

نحوه استفاده از داکر و مجوعه ای از دستورات را نمایش می دهد.

### --tlskey=~/.docker/key.pem

ادرس کلید tls را برای CA مشخض می کند

### --tlsverify=true|false

از tls استفاده می کند و کنترول از راه دور را تایید می کند

### -v, --version=true|false

نسخه فعلی docker را نمایش می دهد

## دستورات

با استفاده از ```docker --help``` می توانید لیست دستورات را بررسی کنید

### run
اجرای یک container جدید از یک تصویر
```
docker run hello-world
```
### exec
اجرای دستورات در یک container در حال اجرا
```
docker exec -it my_container bash
```
### ps
نمایش container های در حال اجرا
```
docker ps
```
### build
ساخت تصویر Docker از فایل Dockerfile
```
docker build -t my_image .
```
### pull
دانلود image از Docker Hub
```
docker pull nginx
```
### push
آپلود image به Docker Hub
```
docker push focker.ir/my_image
```
### images
نمایش لیست image های موجود
```
docker images
```
### login
ورود به Docker Hub
```
docker login
```
### logout
خروج از Docker Hub
```
docker logout
```
### search
جستجوی image در Docker Hub
```
docker search redis
```
### version
نمایش نسخه Docker
```
docker version
```
### info
نمایش اطلاعات سیستم Docker
```
docker info
```
### attach
اتصال به یک container در حال اجرا
```
docker attach my_container
```
### commit
ساخت یک image از یک container در حال اجرا
```
docker commit my_container my_image
```
### cp
کپی فایل ها بین هاست ( سیستم میزبان) و container
```
docker cp my_container:/path/in/container /path/on/host
```
### create
ساخت یک container جدید
```
docker create --name my_container ubuntu
```
### diff
نمایش تغییرات فایل های container
```
docker diff my_container
```
### events
نمایش رویدادهای Docker
```
docker events
```
### export
خروجی گرفتن از filesystem یک container به صورت فایل tar
```
docker export my_container -o my_container.tar
```
### history
نمایش تاریخچه یک image
```
docker history ubuntu
```
### import
وارد کردن filesystem به عنوان image
```
docker import my_container.tar my_image
```
### inspect
نمایش جزئیات یک container یا image
```
docker inspect my_container
```
### kill
متوقف کردن یک container
```
docker kill my_container
```
### load
بارگذاری image از فایل tar
```
docker load -i my_image.tar
```
### logs
نمایش لاگ های یک container
```
docker logs my_container
```
### pause
متوقف کردن موقت اجرای یک container
```
docker pause my_container
```
### port
نمایش نقشه برداری پورت container
```
docker port my_container
```
### rename
تغییر نام یک container
```
docker rename my_container new_container_name
```
### restart
ریستارت کردن یک container
```
docker restart my_container
```
### rm
حذف یک container
```
docker rm my_container
```
### rmi
حذف یک image
```
docker rmi my_image
```
### save
ذخیره یک image به صورت فایل tar
```
docker save -o my_image.tar my_image
```
### start
شروع به کار یک container متوقف شده
```
docker start my_container
```
### stats
نمایش اطلاعات آماری container ها
```
docker stats my_container
```
### stop
متوقف کردن اجرای یک container
```
docker stop my_container
```
### tag
ایجاد یک tag برای یک image
```
docker tag my_image my_repo/my_image:tag
```
### top
نمایش فرآیندهای در حال اجرای یک container
```
docker top my_container
```
### unpause
ادامه اجرای یک container متوقف شده
```
docker unpause my_container
```
### update
به‌روزرسانی تنظیمات یک container
```
docker update --cpus=2 my_container
```
### wait
منتظر ماندن تا پایان اجرای یک container
```
docker wait my_container
```
 



