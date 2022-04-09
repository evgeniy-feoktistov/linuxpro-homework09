# linuxpro-homework09

## Домашнее задание
### Работа с загрузчиком

Описание/Пошаговая инструкция выполнения домашнего задания:
1. [Попасть в систему без пароля несколькими способами.](#1)
2. [Установить систему с LVM, после чего переименовать VG.](#2)
3. [Добавить модуль в initrd.](#3)

***

<a name="1"/>
</a>

### 1. Попасть в систему без пароля несколькими способами.
- 1й способ: добавим в загрузчик опцию
```
linux init=/bin/bash
```
Имеем Hyper-v: При запуске виртуальной машины, выбираем нужные пункт с загрузкой (например, по умолчанию) и нажимаем "**e**", чтобы попасть в меню редактирования параметров данного пункта загрузки.
![8f99ea6d96b8a6100f35705b2fd02740.png](:/0b1e190e5147431bb3fbb189973c8d28)
В конце строки, начинающейся с linuxefi добавляем init=/bin/bash
![https://github.com/evgeniy-feoktistov/linuxpro-homework09/blob/main/8f99ea6d96b8a6100f35705b2fd02740.png](:/00f735fe00fa4a2292494ac81d90f861)
и нажимае **ctrl+x** для загрузки системы
Таким образом мы попали сразу в оболочку bash с правами root
![4577c0f53065c2909d452564a145197f.png](:/72641eb70b12466d96191f0c52020802)
После загрузки оболочки необходимо перемонтировать корневой раздел в режим RW, если нам требуется внести какие либо изменения, например, сменить пароль **root**:
```
mount -o remount,rw /
```
- 2й способ: добавим в загрузчик опцию
```
linux rd.break
```
Так же в конце строки добавляем опцию и загружаемся через **ctrl+x**
![80a5d73cba4beae66d62fbed25f32171.png](:/11578f40bcba42648312359b86d3479b)
Таким образом мы попадаем в режим **emergecy mode**. Наша корневая файловая система так же смонтирована в режиме **Read-only**. Далее в нее необходимо попасть следующим образом, и после можно будет сменить пароль от **root**:
![12be770a92a8622620e0ff0fad59f042.png](:/ded405bdfaac4566803274ff346281a1)
- 3й способ: замена параметра
```
rw init=/sysroot/bin/bash
```
Так же заходим в режим редактирования пункта загрузки и заменяем параметр **ro** на **rw init=/sysroot/bin/bash**
![a53dd1604c998bec9d966b6ddc3c664b.png](:/f0e1485f90fe4eaeb8412e0a8940ab51)
![c0d1ac3d2a8251560a735cb333d22e17.png](:/6a313b24dbbc401fbf439309fe083f95)
нажимаем **ctrl+x** для загрузки в систему.
В таком варианте файловая система уже смонтирована в режиме **Read-write**
![091818787478caf782b6dd405e32b98e.png](:/b2d172c8df2046889bd07d5d548c0521)
***
<a name="2"/>
</a>

### 2. Установить систему с LVM, после чего переименовать VG.

***
<a name="3"/>
</a>

### 3. Добавить модуль в initrd.
