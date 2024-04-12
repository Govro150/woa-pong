<img align="right" src="https://github.com/n00b69/woa-polaris/blob/main/polaris.png" width="350" alt="Windows 11 running on polaris">

# Запуск Windows на Xiaomi Mix 2s

## Обновление драйверов 

### Требования
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Драйвера](https://github.com/n00b69/woa-polaris/releases/tag/Drivers)
  
- [Образ UEFI](https://github.com/n00b69/woa-polaris/releases/tag/UEFI)

### Запуск UEFI
> Замените **<путь\к\polaris-uefi.img>** путём к образу UEFI 
```cmd
fastboot boot <путь\к\polaris-uefi.img>
```

#### Включение режима mass storage 
> После загрузки в UEFI используйте кнопки регулировки громкости для навигации по меню и кнопку питания для подтверждения
- Выберите **UEFI Boot Menu**.
- Выберите **USB Attached SCSI (UAS) Storage**.
- Нажмите кнопку **питания** дважды чтобы подтвердить.

### Diskpart
```cmd
diskpart
```

#### Отобразить разделы устройства
> Чтобы отобразить список всех подключенных разделов, используйте
```cmd
list volume
```

#### Выберите раздел Windows 
> Замените `$` номером раздела **WINPOLARIS**
```cmd
select volume $
```

#### Привязать букву к WINPOLARIS
```cmd
assign letter X
```

### Выйти из diskpart
```cmd
exit
```

### Установка драйверов 
> Extract the drivers folder from the archive, then run the following command, replacing`<path\to\drivers>` with the actual path of the drivers folder
```cmd
dism /image:X:\ /add-driver /driver:<path\to\drivers> /recurse
```

#### Загрузка обратно в Windows
> Перезагрузите устройство, чтобы снова загрузиться в Windows. Если после этого планшет загрузится в Android, перепрошейте образ UEFI с помощью fastboot или с помощью приложения WOA Helper

## Готово!