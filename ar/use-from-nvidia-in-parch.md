---
title: استخدام بطاقة الرسومات من إنفيديا في بارش
description: 
published: true
date: 2025-02-25T18:35:52.813Z
tags: 
editor: markdown
dateCreated: 2025-02-25T18:35:52.813Z
---

### استخدام بطاقة الرسومات من إنفيديا في بارش

وفقًا لما يقوله الخبراء والمستخدمون في نظام لینکس، فإن بطاقة الرسومات من إنفيديا تسبب الكثير من المشاكل في لينكس، ويمكن أن تظهر وكأنها وحش مخيف، ولكننا هنا اليوم للقضاء على هذا الوحش الكبير!

## تثبيت التعريفات

### التعريف الحصري من إنفيديا

قبل كل شيء، يجب علينا تحديد أي نسخة من التعريف متوافقة مع بطاقة الرسومات لدينا، لذلك يجب تثبيت البرنامج `nvidia-helper` من مستودعات بارش وتشغيله:

```bash
sudo pacman -S nvidia-helper && nvidia-helper
```

إذا حصلنا على هذا المخرج، فهذا يعني أننا يمكننا تثبيت أحدث نسخة من التعريف:

```
Your card is supported by the latest drivers.
It is recommended to install the nvidia package or install the nvidia-dkms package for custom kernels
```

### خطوات التثبيت:

1. أولاً، استخدم محرر النانو لفتح الملف `/etc/mkinitcpio.conf`:

```bash
sudo nano /etc/mkinitcpio.conf
```

2. ثم قم بتعبئة قسم `MODULES` كما يلي:

```
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
```

3. بعد ذلك، من قسم `HOOKS` في نفس الملف، قم بحذف الكلمة `kms`. ثم باستخدام الاختصار <kbd>Ctrl + o</kbd> لحفظ الملف، واضغط <kbd>Enter</kbd>، ثم باستخدام الاختصار <kbd>Ctrl + x</kbd> للخروج من المحرر.

4. في النهاية، قم بتثبيت التعريف والأجزاء المتعلقة به باستخدام الأمر التالي:

```bash
sudo pacman -S nvidia nvidia-utils nvidia-settings nvidia-pacman-hook
```

> **ملاحظة**  
إذا كنت قد قمت بتثبيت نواة مخصصة، يجب عليك تثبيت التعريف `nvidia-dkms`:
```bash
sudo pacman -S nvidia-dkms nvidia-utils nvidia-settings
```
إذا كنت تستخدم نواة `lts`:
```bash
sudo pacman -S nvidia-lts nvidia-utils nvidia-settings
```

ولكن إذا حصلت على أحد المخرجات التالية، بناءً على اسم التعريف الذي تم توفيره، يجب تثبيت أحد التعريفات المناسبة:

```
Your card is supported by the Tesla(470xx) dkms drivers.
Your card is supported by the legacy 390xx drivers.
Your card is supported by the legacy 340xx drivers.
```

باستخدام الأوامر:

```bash
paru -S nvidia-470xx-dkms nvidia-470xx-settings or paru -S nvidia-390xx-dkms nvidia-390xx-settings or paru -S nvidia-340xx-dkms nvidia-340xx-settings
```

### تثبيت التعريف المفتوح

في لینکس، هناك تعريفان مفتوحان لبطاقات الرسومات من إنفيديا:

1. **nouveau**

يتم تضمين هذا التعريف بشكل افتراضي في النواة ولا يتطلب تثبيت أي شيء إضافي. ولكن له العديد من المشاكل، مثل عدم القدرة على التحكم في سرعة المروحة والأداء الضعيف، لذلك يُوصى بعدم استخدامه.

2. **nvidia-open**

من الإصدار 510 وما بعده، تم إصدار التعريف `nvidia-open` الذي يحتوي على الشيفرة المصدرية المفتوحة ويدعم بطاقات الرسومات من سلسلة تورينغ وما بعدها. يمكن العثور على قائمة البطاقات المدعومة من هذا التعريف هنا.

طريقة تثبيته هي كالتالي، أولاً، افتح الملف `/etc/mkinitcpio.conf` باستخدام محرر النانو:

```bash
sudo nano /etc/mkinitcpio.conf
```

ثم قم بتعبئة قسم `MODULES` بهذا الشكل:

```
MODULES=(nvidia-open)
```

بعد ذلك، قم بحذف الكلمة `kms` من قسم `HOOKS` في نفس الملف. باستخدام الاختصار <kbd>Ctrl + o</kbd> لحفظ الملف، ثم <kbd>Enter</kbd>، ثم <kbd>Ctrl + x</kbd> للخروج من المحرر.

في النهاية، قم بتثبيت التعريف والملحقات ذات الصلة باستخدام الأمر التالي:

```bash
sudo pacman -S nvidia-open nvidia-utils nvidia-settings
```

> **ملاحظة**  
إذا كنت قد قمت بتثبيت نواة مخصصة أو نواة `lts`، يجب عليك تثبيت التعريف `nvidia-open-dkms`:
```bash
sudo pacman -S nvidia-open-dkms nvidia-utils nvidia-settings
```

## ملاحظات مهمة

1. لتشغيل الألعاب باستخدام بطاقة الرسومات إنفيديا، يجب تثبيت تعريف إنفيديا 32 بت ونسخ 64 و 32 بت من Mesa و Vulkan:

إذا كنت تستخدم التعريف الحصري من إنفيديا أو `nvidia-open`:

```bash
sudo pacman -S vulkan-icd-loader lib32-vulkan-icd-loader lib32-nvidia-utils mesa lib32-mesa
```

إذا كنت تستخدم `nouveau`:

```bash
sudo pacman -S vulkan-icd-loader lib32-vulkan-icd-loader vulkan-nouveau lib32-vulkan-nouveau 
```

2. لتحسين عمل Wayland ومديراته

من الإصدار 364 وما بعده، تم إضافة علم `nvidia_drm.modeset=1` لتحسين أداء Wayland و X11 في وضع الجذر. نظرًا لأن تعريف إنفيديا لا يمكنه التوافق مع إعدادات وضع النواة (KMS) في لينكس، إذا تأخر تحميل الإعداد أو ظهر بعد بدء البروتوكول، فلا يمكنه ضبط دقة الشاشة تلقائيًا، وقد لا يكون من الممكن تغيير وحدة التحكم (tty). لذلك تم إضافة هذا العلم إلى التعريف ليحل محل إعدادات KMS مع إعدادات مدير النواة DRM الخاص بإنفيديا. لإضافة هذا العلم إلى معلمات النواة، استخدم الأمر التالي:

```bash
sudo tee /etc/modprobe.d/nvidia-modeset.conf <<< 'options nvidia_drm modeset=1'
```

أيضًا، بدءًا من الإصدار 545 من التعريف، تمت إضافة العلم `nvidia_drm.fbdev=1` الذي يجعل `simpledrm` هو مدير النواة DRM، مما يجعله مناسبًا للشاشات ذات الدقة العالية. لتفعيل هذا وتحديث متغيرات النواة، استخدم الأمر التالي:

```bash
sudo tee /etc/modprobe.d/nvidia-modeset.conf <<< 'options nvidia_drm modeset=1 fbdev=1'
```

## التبديل بين بطاقتي رسومات في الكمبيوتر المحمول

هناك طريقتان بسيطتان وسهلتان لذلك:

### Bumblebee (غير موصى به)

يستخدم هذا البرنامج تقنية NVIDIA Optimus لتبديل بين بطاقتي الرسومات بناءً على الحمل الحالي. 

يعمل Bumblebee عن طريق حظر نواة `nvidia-drm` عند التمهيد، مما يمنع تحميل التعريف وبدء إعداد الشاشة على بطاقة الرسومات إنفيديا، بل يحصل العرض على الطاقة من بطاقة الرسومات المدمجة عندما تكون تقوم بمهام خفيفة مثل تصفح الإنترنت أو في وضع الاستعداد.

> **ملاحظة**  
قد يسبب استخدام Bumblebee مشاكل مثل نقص الإطارات في الألعاب أو انخفاض الأداء في البرامج الأخرى. راجع [هنا](https://bbs.archlinux.org/viewtopic.php?pid=1822926) أو [هنا](https://github.com/Witko/nvidia-xrun/issues/4#issuecomment-153386837) للمزيد من التفاصيل.

إذا كنت تقوم بمهام ثقيلة مثل تحرير الفيديو أو الألعاب، يقوم Bumblebee بتوجيه التطبيق لاستخدام بطاقة إنفيديا ولكن العرض يبقى على البطاقة المدمجة.

> **تحذير**  
يجب إزالة Bumblebee إذا كنت تختار طريقًا آخر، حتى يتمكن التعريف من إنفيديا من العمل بشكل صحيح.

لتثبيته، استخدم الأمر التالي (افترضنا أنك تستخدم التعريف `nvidia`):

```bash
sudo pacman -S bumblebee mesa lib32-nvidia-utils lib32-virtualgl
```

ثم قم بإضافة المستخدم إلى مجموعة Bumblebee وابدأ خدمة Bumblebee:

```bash
sudo gpasswd -a $user bumblebee && sudo systemctl enable --now bumblebeed.service
```

أخيرًا، أعد تشغيل النظام.

#### إدارة الطاقة في Bumblebee

Bumblebee لا يقوم بإيقاف بطاقة الرسومات المخصصة تلقائيًا عندما لا تكون قيد الاستخدام، لذا نحتاج إلى برنامج آخر للقيام بذلك. يقوم برنامج `bbswatch` بذلك:

```bash
sudo pacman -S bbswitch
```

لأنوية `lts` أو الأنوية المخصصة:

```bash
sudo pacman -S bbswitch-dkms
```

> **ملاحظة**  
لا يتطلب هذا البرنامج وجود Bumblebee ويمكنك تثبيته في أي وقت، ولكن هذه الطريقة لا تعمل على أجهزة الكمبيوتر غير المحمولة.

### Envycontrol

هذا البرنامج يعمل بنفس طريقة Bumblebee باستخدام تقنية NVIDIA Optimus، ولكن يوفر ثلاثة أوضاع مختلفة يمكن للمستخدم ضبطها يدويًا. مقارنةً بـ Bumblebee، لا يسبب Envycontrol مشاكل مثل انخفاض الإطارات أو تمزق الشاشة أثناء التبديل.

لتثبيته، استخدم الأمر التالي:

```bash
sudo pacman -S envycontrol
```


#### ضبط وضع التبديل باستخدام Envycontrol

لتفعيل التبديل التلقائي بين الب

طاقات، قم بتعديل الملف `envycontrol.conf` باستخدام محرر النصوص:

```bash
sudo nano /etc/envycontrol.conf
```

تأكد من أن القيمة `Optimus_mode=1` موجودة.

إذا كنت ترغب في التبديل يدويًا بين البطاقتين، استخدم الخيارات التالية:

```bash
# لتشغيل بطاقة إنفيديا
envycontrol nvidia

# لتشغيل البطاقة المدمجة
envycontrol intel
```

### النهاية

بمجرد أن تتابع هذه الخطوات، يجب أن تتمكن من تشغيل بطاقة إنفيديا على بارش بشكل مثالي.