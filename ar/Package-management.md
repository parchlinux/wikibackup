---
title: مدير الحزم
description: 
published: true
date: 2025-02-25T18:26:43.584Z
tags: 
editor: markdown
dateCreated: 2025-02-25T18:26:43.584Z
---

# إدارة الحزم في بارش لينكس

## مدير الحزم

مدير الحزم في بارش لينكس يُعرف باسم pacman.

وفقًا لوِيكِي ArchLinux:

> يُعتبر مدير الحزم pacman من أبرز ميزات أرش لينكس. يجمع هذا المدير بين صيغة بسيطة لحزم البرامج مع نظام بناء سهل. الهدف من pacman هو إدارة الحزم بسهولة بحيث يمكن إدارة الحزم بسهولة، سواء كانت من مستودعات رسمية أو غير رسمية.
> يقوم pacman بتحديث النظام عن طريق مزامنة قائمة الحزم مع الخوادم الرئيسية. يسمح هذا النموذج بين الخادم والمستخدم للمستخدم بتثبيت الحزم باستخدام أمر بسيط، مع جميع التبعيات المطلوبة.
> تم كتابة pacman بلغة البرمجة C ويستخدم صيغة tar مع bsdtar(1) لتعبئة الحزم.

## كيفية عمل pacman

إليك دليل صغير يساعدك في استخدام pacman:

### العمليات الأساسية

| العمل | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| البحث عن حزمة(ات) | `pacman -Ss` | `dnf search` | `apt search` | `zypper search` أو `zypper se [-s]` | `emerge --search` (`-s`) أو `emerge --searchdesc` (`-S`) |
| تثبيت حزمة(ات) بالاسم | `pacman -S` | `dnf install` | `apt install` | `zypper install` أو `zypper in` | `emerge` |
| تنزيل الحزم المصدرية والتبعيات | `makepkg -s PKGBUILD` | `dnf builddep` | `apt build-dep` | `zypper source-install` (`zypper si`) أو `zypper install -d` | `emerge`، أو باستخدام `emerge --with-bdeps` |
| عرض الأهداف دون تنفيذ العمليات | `pacman --print` (أو `-p`) | `dnf --setopt=tsflags=test` | `apt --simulate` (أو `-s`، `--dry-run`، `--just-print`) | `zypper --dry-run` | `emerge --pretend` (`-p`) |
| تغيير التأكيدات | `pacman --confirm` أو `pacman --noconfirm` | `dnf --assumeyes` (`-y`) أو `dnf --assumeno` | `apt --yes` (`-y`) | `zypper --non-interactive` (`-n`) أو `zypper --no-confirm` (`-y`) | `emerge --ask` (`-a`) |
| تحديث مستودع الحزم المحلي | `pacman -Sy` | `dnf check-update` أو `dnf makecache` أو `dnf upgrade` | `apt update` | `zypper refresh` أو `zypper ref` `[-s]` | `emerge --sync` |
| ترقية الحزم | `pacman -Syu` | `dnf upgrade` | `apt upgrade` | `zypper update` أو `zypper up` | `emerge -[a]uDN @world` |
| ترقية الحزم (ترقيات معقدة) | `pacman -Syu` | `dnf distro-sync` | `apt dist-upgrade` | `zypper dup` | `emerge -[a]uDN @world` |
| إزالة الحزم والتبعيات | `pacman -Rs` | `dnf remove` | `apt autoremove` | `zypper remove` أو `zypper rm` | `emerge --depclean` (`-c`) |
| إزالة الحزم وملفات التكوين | `pacman -Rn` | ؟ | `apt purge` | ؟ | غير متاح |
| إزالة الحزم، التبعيات وملفات التكوين | `pacman -Rns` | ؟ | `apt autoremove --purge` | ؟ | غير متاح |
| إزالة التبعيات غير اللازمة | `pacman -Qdtq | pacman -Rs -` `` (`-Qdttq` للتبعيات الاختيارية) | `dnf autoremove` | `apt autoremove` | `zypper rm -u` أو `zypper packages --unneeded` | `emerge --depclean` (`-c`) |
| إزالة الحزم غير الموجودة في المستودعات | `pacman -Rs $(pacman -Qmq)` | `dnf repoquery --extras` | `aptitude purge '~o'` || ؟ |
| عرض الحزم المثبتة بشكل صريح | `pacman -D --asexplicit` | `dnf mark install` | `apt-mark manual` | `zypper install --force` | `emerge --select` (`-w`) |
| تثبيت الحزم كاعتماديات | `pacman -S --asdeps` | `dnf install` ثم `dnf mark remove` | `apt-mark auto` | غير متاح ([الحل](https://bugzilla.opensuse.org/show_bug.cgi?id=1175678)) | `emerge --oneshot` (`-1`) |
| تنزيل الحزم فقط | `pacman -Sw` | `dnf download` | `apt install --download-only` أو `apt download` | `zypper --download-only` | `emerge --fetchonly` (`-f`) |
| تنظيف الذاكرة المحلية | `pacman -Sc` أو `pacman -Scc` | `dnf clean all` | `apt autoclean` أو `apt clean` | `zypper clean` | `eclean distfiles` |
| بدء جلسة قشرة | | `dnf shell` | | `zypper shell` ||

### استعلام الحزم الخاصة

| العمل | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| عرض معلومات الحزمة | `pacman -Si` أو `pacman -Qi` | `dnf list` أو `dnf info` | `apt show` أو `apt-cache policy` | `zypper info` أو `zypper if` | `emerge -S`، `emerge -pv` أو `eix` |
| عرض معلومات الحزمة المحلية | `pacman -Qi` | `rpm -qi` / `dnf info installed` | `dpkg -s` أو `aptitude show` | `zypper --no-remote info` أو `rpm -qi` | `emerge -pv` أو `emerge -S` |
| عرض معلومات الحزمة من بعيد | `pacman -Si` | `dnf info` | `apt-cache show` أو `aptitude show` | `zypper info` | `emerge -pv` و `emerge -S` أو `equery meta` |
| عرض ملفات الحزمة المحلية | `pacman -Ql` | `rpm -ql` | `dpkg -L` | `rpm -ql` | `equery files` أو `qlist` |
| عرض ملفات الحزمة من بعيد | `pacman -Fl` | `dnf repoquery -l` أو `repoquery -l` | `apt-file list` || `pfl` |
| استعلام الحزمة التي توفر الملف | `pacman -Qo` | `rpm -qf` (مثبتة) أو `dnf provides` (جميعها) أو `repoquery -f` | `dpkg -S` أو `dlocate` | `rpm -qf` (مثبتة) أو `zypper search -f` (جميعها) | `equery belongs` أو `qfile` |
| قائمة الملفات في الحزمة | `pacman -Ql` أو `pacman -Fl` | `dnf repoquery -l` | `dpkg-query -L` | `rpm -ql` | `equery files` أو `qlist` |
| عرض مقدمي الحزم العكسي | `pacman -F` | `dnf provides` | `apt-file search` | `zypper what-provides` أو `zypper wp` (دقيق) | `equery belongs` (مثبتة) أو `pfl` |
| البحث عن حزمة بواسطة الملف | `pacman -F` | `dnf provides` | `apt-file search` أو `auto-apt` | `zypper search -f` | `equery belongs` أو `qfile` |
| عرض تغييرات الحزمة | `pacman -Qc` | `dnf changelog` | `apt-get changelog` | `rpm -q --changelog` | `equery changes -f` |

### AUR

> مستودع المستخدمين في Arch (AUR) هو مستودع مخصص لمستخدمي Arch تدعمه المجتمع. يحتوي هذا المستودع على وصف الحزم (PKGBUILDs) التي تتيح لك تجميع حزمة من المصدر باستخدام makepkg ومن ثم تثبيتها عبر pacman. تم إنشاء AUR لتنظيم ومشاركة الحزم الجديدة من المجتمع، وللمساعدة في إضافة الحزم الشهيرة إلى المستودعات الإضافية وتسريع تحديث الحزم المعروفة.
> العديد من الحزم الجديدة التي تدخل المستودعات الرسمية تبدأ

 أولاً في AUR.

## الحزم المثبتة

| العمل | Arch | Red Hat/Fedora | Debian/Ubuntu | SLES/openSUSE | Gentoo |
|--------|------|-----------------|----------------|-----------------|--------|
| قائمة الحزم المثبتة | `pacman -Q` | `dnf list installed` | `dpkg -l` أو `apt list --installed` | `zypper se --installed-only` | `equery list` |
| عرض حزم من مستودع محدد | `pacman -Qd` | ؟ | `apt list --installed` | ؟ | `equery list` |
| عرض حزم من نوع معين | `pacman -Qdt` | ؟ | `apt list --installed` | ؟ | `equery list` |
| قائمة الحزم مع إصدارها | `pacman -Q` | `dnf list installed` | `dpkg -l` أو `apt list --installed` | `zypper se --installed-only` | `equery list` |
| إزالة الحزم | `pacman -R` | `dnf remove` | `apt remove` | `zypper remove` أو `zypper rm` | `emerge --unmerge` |

### مدير AUR

يستخدم توزيعة **بارش لینکس** **Paru** كمدير AUR.
استخدام **Paru** مشابه لاستخدام **pacman**، حيث يمكنك بسهولة تثبيت الحزم من AUR بنفس طريقة الكتابة.

#### استخدام Paru
إليك بعض الأوامر المفيدة لاستخدام Paru:

| الأمر | الشرح |
| --- | --- |
| `paru` | تحديث النظام بالكامل |
| `paru -Syu` | تحديث النظام بالكامل |
| `paru -S <اسم_البرنامج>` | تثبيت البرنامج من AUR |
| `paru <اسم_البرنامج>` | تثبيت البرنامج من AUR، مع اختيار من القائمة |
| `paru -Sc` | مسح ذاكرات التخزين المؤقت لـ Pacman و Paru |
| `paru -Ss <اسم_البرنامج>` | البحث عن حزمة |

تساعدك هذه الأوامر في تثبيت الحزم من AUR بسهولة وإدارة النظام بشكل أفضل.

