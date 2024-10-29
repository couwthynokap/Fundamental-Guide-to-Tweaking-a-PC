# Настройте драйвер NVIDIA

> Перед выполнением всех действий рекомендуется создать точку восстановления системы, чтобы в случае необходимости можно было вернуть изменения обратно, поэтому действуйте с осторожностью.

## 1. Установка DDU и удаление старых драйверов

Перед установкой нового драйвера Nvidia необходимо удалить текущую версию, чтобы избежать конфликтов и обеспечить корректную работу новой версии. Для этого рекомендуется использовать утилиту под названием Display Driver Uninstaller (DDU). Этот инструмент значительно упрощает процесс удаления драйверов и гарантирует, что все остаточные файлы будут удалены.

#### Шаги по удалению старых драйверов с помощью DDU:

1. **Загрузка в безопасный режим**: 
   Для начала перезагрузите компьютер и войдите в безопасный режим. Это можно сделать, удерживая клавишу Shift во время перезагрузки и выбирая соответствующий пункт в меню.

2. **Запуск DDU**: 
   После загрузки в безопасном режиме скачайте и запустите DDU. Вы можете скачать утилиту по следующей ссылке: [Скачать DDU](https://www.guru3d.com/files-get/display-driver-uninstaller-download,19.html).

3. **Настройка DDU**: 
   В интерфейсе DDU выберите настройки, как показано на изображении ниже (вставьте изображение с настройками). Эти параметры помогут вам полностью удалить текущие драйверы Nvidia.

4. **Удаление драйверов**: 
   После настройки выберите опцию «Clean & Restart» (Очистить и перезагрузить). Утилита удалит старые драйверы, а ваш компьютер автоматически перезагрузится.

5. **Проверка разрешения экрана**: 
   После перезагрузки ваш монитор может быть установлен на частоту 60 Гц. Не беспокойтесь, это нормально. Вам нужно будет установить новые драйверы Nvidia, чтобы вернуть экран к его рекламируемой частоте обновления.

Следуя этим шагам, вы сможете эффективно удалить старые драйверы Nvidia и подготовить систему к установке новой версии, что обеспечит оптимальную производительность вашей видеокарты.

## 2. Установка драйвера через NVCleanstall

Для установки драйвера Nvidia с помощью утилиты NVCleanstall выполните следующие шаги. Этот инструмент позволяет настроить установку драйвера, исключая ненужные компоненты и оптимизируя производительность.

1. **Скачивание и запуск NVCleanstall**: 
   Сначала скачайте NVCleanstall по следующей ссылке: [Скачать NVCleanstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/). Запустите программу после завершения загрузки. Если у вас ноутбук, то обязательно включите [Optimus](https://www.nvidia.com/en-us/geforce/technologies/optimus/technology/)      

3. **Выбор версии драйвера**: 
   В интерфейсе NVCleanstall выберите нужную версию драйвера Nvidia. После этого нажмите кнопку "Далее" в правом нижнем углу программы.

4. **Обратите внимание на новые драйверы**: 
   В новых версиях драйверов отсутствует возможность отключения комбинирования записи, что может привести к увеличению задержки и количеству вводимых данных. Убедитесь, что вы учитываете это при выборе версии драйвера для установки.

5. **Настройка компонентов**: 
   Для достижения максимальной производительности скопируйте следующие настройки:
   - В разделе **Installation Tweaks** отметьте следующие опции:
     - **Disable Installer Telemetry & Advertising** (Отключить телеметрию и рекламу установщика)
     - **Unattended Express Installation** (Автоматическая установка)
     - **Perform a Clean Installation** (Выполнить чистую установку)
     - **Disable Multiplane Overlay (MPO)** (Отключить многоплановый оверлей)
     - **Disable Ansel** (Отключить Ansel)
     - **Show Expert Tweaks** (Показать экспертные настройки)
     - **Disable Driver Telemetry (Experimental)** (Отключить телеметрию драйвера - экспериментально)
     - **Enable Message Signaled Interrupts** (Включить прерывания с сообщениями)
     - **Disable HDCP** (Отключить HDCP)
     - **Rebuild digital signature (required for one or more selected tweaks)** (Восстановить цифровую подпись - требуется для одной или нескольких выбранных настроек)
     - **Use method compatible with Easy-Anti-Cheat (triggers a "driver unsigned" warning during installation)** (Использовать метод, совместимый с Easy-Anti-Cheat - вызывает предупреждение "драйвер не подписан" во время установки)
     - **Automatically accept the "driver unsigned" warning** (Автоматически принимать предупреждение "драйвер не подписан").

6. **Завершение установки**: 
   После настройки всех параметров нажмите кнопку "Далее" для завершения установки драйвера. Следуйте инструкциям на экране, чтобы завершить процесс.

Используя NVCleanstall, вы сможете установить драйвер Nvidia с оптимальными настройками, что обеспечит лучшую производительность вашей видеокарты и минимизирует ненужные компоненты.

## 3. Настройка MSI Afterburner

MSI Afterburner — это мощный инструмент для разгона видеокарт, который позволяет пользователям настраивать производительность своих графических адаптеров. Чтобы оптимизировать работу видеокарты, выполните следующие шаги:

1. **Отключение ограничений**: 
   В интерфейсе MSI Afterburner отключите ограничения или увеличьте их до максимума. Это позволит вашей видеокарте работать на полную мощность, что может повысить производительность в играх и других графически интенсивных приложениях.

2. **Настройка напряжений**: 
   Включите стабильные напряжения и мониторинг напряжений. Это важно для обеспечения надежной работы видеокарты и предотвращения перегрева или нестабильной работы.

3. **Запомните модель видеокарты**: 
   Убедитесь, что вы знаете модель своей видеокарты. Это поможет вам в дальнейшем искать информацию о паспортном повышении частоты и других характеристиках.

4. **Поиск паспортного повышения частоты**: 
   В браузере найдите паспортное повышение частоты для вашей модели видеокарты. Это даст вам представление о том, на сколько можно увеличить частоты без риска повреждения устройства.

5. **Включение Key Boost**: 
   Для активации функции Key Boost в MSI Afterburner вам потребуется установить специальный скин. Скачайте скин [EVGA SKIN](https://drive.google.com/file/d/1buaP5Gv7f3Jv3OPQzKWF6Q7fSvxft2a0/view?usp=sharing).

   - После загрузки архива скиньте папку `skins` в директорию установки MSI Afterburner.
   - Скопируйте файл `default` в папку `skins`.

6. **Перезагрузка компьютера**: 
   После установки скина перезагрузите компьютер. 

7. **Выбор скина и активация Key Boost**: 
   Запустите MSI Afterburner, выберите установленный скин и активируйте функцию Key Boost. Это позволит вам использовать дополнительные возможности разгона и улучшить производительность вашей видеокарты.

Следуя этим шагам, вы сможете настроить MSI Afterburner для достижения максимальной производительности вашей видеокарты, что позволит вам наслаждаться играми и графически интенсивными приложениями без задержек и проблем.

## 4. Настройка видеодрайвера

### Полное удаление телеметрии Nvidia

Если вы хотите полностью отключить телеметрию Nvidia и избавиться от ненужных данных, собираемых компанией, вы можете использовать следующий скрипт. Этот скрипт выполняет несколько действий, включая изменение реестра, удаление файлов и отключение задач, связанных с телеметрией.

#### Шаги по удалению телеметрии Nvidia:

1. **Создание скрипта**: 
   Откройте текстовый редактор, например, Блокнот, и скопируйте в него следующий код:

   ```batch
   @echo off

   Reg.exe add "HKLM\SOFTWARE\NVIDIA Corporation\NvControlPanel2\Client" /v "OptInOrOutPreference" /t REG_DWORD /d 0 /f
   Reg.exe add "HKCU\SOFTWARE\NVIDIA Corporation\NVControlPanel2\Client" /v "OptInOrOutPreference" /t REG_DWORD /d "0" /f
   Reg.exe add "HKCU\Software\Classes\Software\NVIDIA Corporation\NVControlPanel2\Client" /v "OptInOrOutPreference" /t REG_DWORD /d "0" /f
   cls
   rmdir /s /q "C:\Windows\System32\drivers\NVIDIA Corporation"
   cd /d "C:\Windows\System32\DriverStore\FileRepository\"
   dir NvTelemetry64.dll /a /b /s
   del NvTelemetry64.dll /a /s
   cls
   cd /d "%PROGRAMFILES%\NVIDIA Corporation\"
   dir NvTelemetry64.dll /a /b /s
   del NvTelemetry64.dll /a /s
   cls
   cd /d "SYSTEM32\DriverStore\FileRepository\"
   dir NvTelemetry64.dll /a /b /s
   del NvTelemetry64.dll /a /s
   cls
   DevManView.exe /disable "NvModuleTracker Device" >nul 2>&1
   DevManView.exe /disable "NVIDIA Virtual Audio Device (Wave Extensible) (WDM)" >nul 2>&1
   cls
   for %%i in (NvTmMon NvTmRep NvProfile NvNodeLauncher NvDriverUpdateCheckDaily "NVIDIA GeForce Experience SelfUpdate*") do for /f "tokens=1 delims=," %%a in ('schtasks /query /fo csv ^| findstr /v "TaskName" ^| findstr "%%~i"') do schtasks /change /tn "%%a" /disable >nul 2>&1
   Reg.exe add "HKCU\SOFTWARE\NVIDIA Corporation\Global\GFExperience" /v "NotifyNewDisplayUpdates" /t REG_DWORD /d "0" /f >nul 2>&1
   Reg.exe add "HKCU\SOFTWARE\NVIDIA Corporation\NvTray" /v "StartOnLogin" /t REG_DWORD /d "0" /f >nul 2>&1
   exit
   ```

2. **Сохранение файла**: 
   Сохраните файл с расширением `.bat`, например, `RemoveNvidiaTelemetry.bat`.

3. **Запуск скрипта**: 
   Запустите созданный файл от имени администратора. Это необходимо для выполнения всех команд, требующих повышенных привилегий.

#### Что делает этот скрипт:

- **Изменение реестра**: Скрипт изменяет параметры реестра, отключая сбор телеметрии.
- **Удаление файлов**: Удаляются файлы, связанные с телеметрией, такие как `NvTelemetry64.dll`.
- **Отключение устройств**: Отключаются устройства, связанные с телеметрией, такие как `NvModuleTracker Device` и `NVIDIA Virtual Audio Device`.
- **Отключение задач**: Отключаются запланированные задачи, связанные с телеметрией и обновлениями GeForce Experience.
- **Настройка параметров запуска**: Отключается автоматический запуск GeForce Experience при входе в систему.

### Полное удаление компонентов Nvidia с помощью Driver Strip

Если вы хотите полностью удалить ненужные компоненты и телеметрию Nvidia, вы можете использовать следующий скрипт. Этот скрипт выполняет множество действий, включая отключение служб, удаление файлов и изменение настроек реестра, чтобы очистить систему от всех следов драйверов и утилит Nvidia.

#### Шаги по использованию скрипта:

1. **Создание скрипта**: 
   Откройте текстовый редактор, например, Блокнот, и скопируйте в него следующий код:

   ```batch
   @echo off

   :start

   sc config NVDisplay.ContainerLocalSystem start= disabled >NUL 2>&1
   sc stop NVDisplay.ContainerLocalSystem >NUL 2>&1
   echo                           Do you have Geforce Experience installed? (y/n)

   :choice

   set /p userChoice=
   if /i "%userChoice%"=="n" (
       rmdir /s /q "C:\Program Files\NVIDIA Corporation">nul 2>&1
       cd /d "C:\Windows\System32\DriverStore\FileRepository\nv_*" >nul 2>&1
       del /f nvFBC*.dll, nvIFR*.dll >nul 2>&1

       cd /d ".\Display.NvContainer\plugins\LocalSystem" >nul 2>&1
       takeown /r /d Y /f * >nul 2>&1
       icacls * /grant "%USERNAME%":F >nul 2>&1
       @REM del /f NvcDispWatchdog.dll >nul 2>&1 maybe breaks control panel

       cd /d "../Session" >nul 2>&1
       takeown /f * /r /d Y >nul 2>&1
       icacls * /grant "%USERNAME%":F >nul 2>&1
       del /f _NvGSTPlugin.dll >nul 2>&1

       cd /d "C:\Windows\System32" >nul 2>&1
       takeown /r /d Y /f "nv*.*" >nul 2>&1
       icacls "nv*.*" /grant "%USERNAME%":F /t >nul 2>&1
       del /f NvFBC64.dll, NvIFR64.dll >nul 2>&1

       cd /d "C:\Windows\SysWOW64" >nul 2>&1
       takeown /r /d Y /f "nv*.*" >nul 2>&1
       del /f NvFBC.dll, NvIFR.dll >nul 2>&1
       echo                                    Removing GeForce components.
       goto start
   ) else if /i "%userChoice%"=="y" (
       echo                                    Skipping GeForce components.
       goto start
   ) else (
       echo Invalid choice. Please type 'y' or 'n'.
       goto choice
   )

   :start
   rmdir /s /q "C:\Windows\System32\drivers\NVIDIA Corporation" >nul 2>&1
   cd /d "C:\Windows\System32\DriverStore\FileRepository\" >nul 2>&1
   dir NvTelemetry64.dll /a /b /s >nul 2>&1
   del NvTelemetry64.dll /a /s >nul 2>&1
   reg add "HKCU\SOFTWARE\NVIDIA Corporation\NVControlPanel2\Client" /v "OptInOrOutPreference" /t REG_DWORD /d "0" /f >nul 2>&1
   reg add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\Startup\SendTelemetryData" /ve /t REG_DWORD /d "0" /f >nul 2>&1

   cd /d "C:\Windows\System32\DriverStore\FileRepository\nv_*" >nul 2>&1
   takeown /r /d Y /f * >nul 2>&1
   takeown /f NVWMI /R /D Y >nul 2>&1
   icacls "NVWMI" /grant "%USERDOMAIN%\%USERNAME%":F /t >nul 2>&1
   rmdir /s /q NVWMI >nul 2>&1

   takeown /f NvCamera /R /D Y >nul 2>&1
   icacls "NvCamera" /grant "%USERDOMAIN%\%USERNAME%":F /t >nul 2>&1
   rmdir /s /q NvCamera >nul 2>&1
   reg delete "HKLM\System\ControlSet001\Services```batch
   \nvlddmkm\NvCamera" /f >nul 2>&1

   icacls * /grant "%USERDOMAIN%\%USERNAME%":(F) /t >nul 2>&1
   del /f "NvTelemetry64.dll" >nul 2>&1

   del /f nvptxJitCompiler32.dll, nvptxJitCompiler64.dll >nul 2>&1
   del /f nvsmartmax*.*, nvinfo.pb >nul 2>&1
   del /f nvIccAdvancedColorIdentity.icm, nvEncMFT*.dll, nvDevMFT*.dll >nul 2>&1

   cd /d "./Display.NvContainer" >nul 2>&1
   takeown /f * /R /D Y >nul 2>&1
   icacls * /grant "%USERNAME%":F >nul 2>&1
   del /f "nvtopps.db3" >nul 2>&1

   cd /d "./plugins/LocalSystem/" >nul 2>&1
   takeown /f _DisplayDriverR*.dll /R /D Y >nul 2>&1
   icacls "_DisplayDriverRAS.dll" /grant "%USERNAME%":F >nul 2>&1
   del /f _DisplayDriverRAS.dll >nul 2>&1
   del /f _nvtopps.dll >nul 2>&1

   cd /d "../Session" >nul 2>&1
   takeown /f * /R /D Y >nul 2>&1
   icacls * /grant "%USERNAME%":F >nul 2>&1
   del /f nvprofileupdaterplugin.dll >nul 2>&1

   cd /d "C:\Windows\System32" >nul 2>&1
   del /f nvinfo.pb >nul 2>&1
   rmdir /s /q lxss >nul 2>&1
   del /f MCU.exe, nvcudadebugger.dll, nvdebugdump.exe /f >nul 2>&1

   sc config NVDisplay.ContainerLocalSystem start= auto >NUL 2>&1
   sc start NVDisplay.ContainerLocalSystem >NUL 2>&1

   echo.
   echo                                The driver was stripped successfully.
   ```

### Описание работы скрипта

Этот скрипт выполняет следующие действия:

1. **Отключение и остановка службы**: 
   Сначала скрипт отключает и останавливает службу `NVDisplay.ContainerLocalSystem`, чтобы предотвратить любые конфликты во время удаления компонентов.

2. **Удаление компонентов GeForce Experience**: 
   Если у вас не установлен GeForce Experience, скрипт удаляет все связанные с ним файлы и папки, включая драйвера и плагины.

3. **Удаление файлов телеметрии**: 
   Скрипт ищет и удаляет файлы, связанные с телеметрией Nvidia, такие как `NvTelemetry64.dll`, а также другие ненужные файлы и библиотеки.

4. **Изменение прав доступа**: 
   Скрипт использует команды `takeown` и `icacls` для получения прав на удаление файлов, которые могут быть защищены.

5. **Удаление дополнительных компонентов**: 
   Удаляются дополнительные компоненты, такие как `NvCamera`, `NVWMI`, и другие, которые могут не понадобиться.

6. **Восстановление службы**: 
   После завершения всех операций скрипт восстанавливает службу `NVDisplay.ContainerLocalSystem` и устанавливает ее на автоматический запуск.

7. **Уведомление об успешном завершении**: 
   В конце скрипт выводит сообщение о том, что процесс удаления завершен успешно.

### Настройка резкости изображения и плавности с помощью реестра

Для улучшения качества изображения на видеокартах Nvidia вы можете настроить параметры резкости и плавности с помощью редактора реестра Windows. В зависимости от версии драйвера, вам могут понадобиться разные настройки.

#### Включение резкости изображения (для драйверов 496.76 и выше)

Если вы используете драйверы версии 496.76 и выше, вы можете включить функцию резкости изображения, добавив соответствующий параметр в реестр. Для этого выполните следующие шаги:

1. **Создание файла .reg**: 
   Откройте текстовый редактор, например, Блокнот, и скопируйте в него следующий код:

   ```reg
   Windows Registry Editor Version 5.00

   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\FTS]
   "EnableGR535"=dword:00000000
   ```

2. **Сохранение файла**: 
   Сохраните файл с расширением `.reg`, например, `EnableImageSharpness.reg`.

3. **Импорт в реестр**: 
   Дважды щелкните на созданный файл и подтвердите внесение изменений в реестр. Это активирует резкость изображения.

#### Включение плавности SILK (для драйверов 457.30 и ниже)

Если у вас установлены драйверы версии 457.30 и ниже, вы можете включить функцию плавности SILK, используя следующий код:

1. **Создание файла .reg**: 
   Откройте текстовый редактор и вставьте следующий код:

   ```reg
   Windows Registry Editor Version 5.00

   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\FTS]
   "EnableRID61684"=dword:00000001
   ```

2. **Сохранение файла**: 
   Сохраните файл с расширением `.reg`, например, `EnableSILKSmoothness.reg`.

3. **Импорт в реестр**: 
   Дважды щелкните на созданный файл и подтвердите внесение изменений в реестр. Это активирует плавность SILK.

### Важно:
- Перед внесением изменений в реестр рекомендуется создать резервную копию текущих настроек реестра, чтобы в случае необходимости можно было восстановить систему.
- Изменения в реестре могут повлиять на работу системы, поэтому действуйте осторожно и следуйте инструкциям внимательно.

### Оптимизация настроек NVIDIA с помощью скрипта

Скрипт, представленный ниже, предназначен для оптимизации работы видеокарт NVIDIA путем изменения некоторых параметров в реестре Windows. Он отключает динамическое состояние P-стейтов, настраивает параметры управления производительностью и отключает ведение журналов, что может помочь в повышении стабильности и производительности системы.

#### Шаги по использованию скрипта:

1. **Создание скрипта**: 
   Откройте текстовый редактор, например, Блокнот, и вставьте следующий код:

   ```batch
   @echo off
   for /f %%i in ('wmic path Win32_VideoController get PNPDeviceID^| findstr /L "PCI\VEN_"') do (
       for /f "tokens=3" %%a in ('reg query "HKLM\SYSTEM\ControlSet001\Enum\%%i" /v "Driver"') do (
           for /f %%i in ('echo %%a ^| findstr "{"') do (
               Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Control\Class\%%i" /v "DisableDynamicPstate" /t REG_DWORD /d "1" /f > nul 2>&1
           )
       )
   )
   cls
   C:
   cd C:\Program Files\NVIDIA Corporation\NVSMI
   nvidia-smi.exe -acp 0
   cls
   for /f %%i in ('wmic path Win32_VideoController get PNPDeviceID^| findstr /L "PCI\VEN_"') do (
       for /f "tokens=3" %%a in ('reg query "HKLM\SYSTEM\ControlSet001\Enum\%%i" /v "Driver"') do (
           for /f %%i in ('echo %%a ^| findstr "{"') do (
               Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Control\Class\%%i" /v "RMHdcpKeyglobZero" /t REG_DWORD /d "1" /f > nul 2>&1
           )
       )
   )
   cls
   Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters" /v "LogWarningEntries" /t REG_DWORD /d "0" /f
   Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters" /v "LogPagingEntries" /t REG_DWORD /d "0" /f
   Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters" /v "LogEventEntries" /t REG_DWORD /d "0" /f
   Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters" /v "LogErrorEntries" /t REG_DWORD /d "0" /f
   Reg.exe add "HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters" /v "DmaRemappingCompatible" /t REG_DWORD /d "0" /f
   Exit
   ```

2. **Сохранение файла**: 
   Сохраните файл с расширением `.bat`, например, `NVIDIA_Tweaks.bat`.

3. **Запуск скрипта**: 
   Запустите созданный файл от имени администратора. Это необходимо для выполнения всех команд, требующих повышенных привилегий.

#### Описание работы скрипта:

- **Отключение динамического состояния P-стейтов**: 
  Скрипт ищет идентификаторы устройств видеокарт и добавляет параметр `DisableDynamicPstate`, который отключает динамическое управление состоянием питания, что может улучшить производительность в играх и приложениях.

- **Настройка параметров управления производительностью**: 
  Скрипт использует утилиту `nvidia-smi` для настройки управления производительностью видеокарты.

- **Отключение ведения журналов**: 
  Устанавливаются параметры, отключающие ведение журналов предупреждений, ошибок и событий, что может снизить нагрузку на систему.

- **Настройка совместимости DMA**: 
  Параметр `DmaRemappingCompatible` устанавливается в значение `0`, что может помочь в улучшении совместимости с некоторыми приложениями и играми.

## Настройка Nvidia Dwords

Настройка параметров реестра Windows для графических карт Nvidia может значительно улучшить производительность и стабильность системы. В данном руководстве мы рассмотрим, как изменить значения Dwords в реестре, чтобы оптимизировать работу графического адаптера.

### 1. Подготовка к изменению реестра

Перед внесением изменений в реестр рекомендуется создать резервную копию текущих настроек. Это позволит вам восстановить систему в случае возникновения проблем. Для этого выполните следующие шаги:

1. Нажмите `Win + R`, введите `regedit` и нажмите `Enter`.
2. В редакторе реестра выберите `Файл` > `Экспорт`.
3. Выберите место для сохранения резервной копии и нажмите `Сохранить`.

### 2. Внесение изменений в реестр

Скопируйте следующий текст в текстовый редактор и сохраните его с расширением `.reg`, например, `nvidia_settings.reg`. Этот файл содержит необходимые изменения для оптимизации работы графической карты Nvidia.

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power]
"ExitLatency"=dword:00000001 
"ExitLatencyCheckEnabled"=dword:00000001
"Latency"=dword:00000001 
"LatencyToleranceDefault"=dword:00000001 
"LatencyToleranceFSVP"=dword:00000001 
"LatencyTolerancePerfOverride"=dword:00000001 
"LatencyToleranceScreenOffIR"=dword:00000001
"RtlCapabilityCheckLatency"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Power]
"DefaultD3TransitionLatencyActivelyUsed"=dword:00000001 
"DefaultD3TransitionLatencyIdleLongTime"=dword:00000001 
"DefaultD3TransitionLatencyIdleMonitorOff"=dword:00000001 
"DefaultD3TransitionLatencyIdleNoContext"=dword:00000001 
"DefaultD3TransitionLatencyIdleShortTime"=dword:00000001 
"DefaultD3TransitionLatencyIdleVeryLongTime"=dword:00000001 
"DefaultLatencyToleranceIdle0"=dword:00000001 
"DefaultLatencyToleranceIdle0MonitorOff"=dword:00000001 
"DefaultLatencyToleranceIdle1"=dword:00000001
"DefaultLatencyToleranceIdle1MonitorOff"=dword:00000001 
"DefaultLatencyToleranceMemory"=dword:00000001 
"DefaultLatencyToleranceNoContext"=dword:00000001 
"DefaultLatencyToleranceNoContextMonitorOff"=dword:00000001 
"DefaultLatencyToleranceOther"=dword:00000001 
"DefaultLatencyToleranceTimerPeriod"=dword:00000001 
"DefaultMemoryRefreshLatencyToleranceActivelyUsed"=dword:00000001 
"DefaultMemoryRefreshLatencyToleranceMonitorOff"=dword:00000001 
"DefaultMemoryRefreshLatencyToleranceNoContext"=dword:00000001 
"Latency"=dword:00000001 
"MaxIAverageGraphicsLatencyInOneBucket"=dword:00000001
"MiracastPerfTrackGraphicsLatency"=dword:00000001 
"MonitorLatencyTolerance"=dword:00000001 
"MonitorRefreshLatencyTolerance"=dword:00000001 
"TransitionLatency"=dword:00000001 

[HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\GraphicsDrivers]
"SchedulingDelay"=dword:00000000
"DisableOverlays"=dword:00000001
"SupportRuntimePowerManagement"=dword:00000000
"RuntimePowerManagement"=dword:00000000
"Protection"=dword:00000000
"ProtectionLevel"=dword:00000000
"OPMSetProtectionLevel"=dword:00000000
"NumberOfIdleStates"=dword:00000000
"EnableRuntimePowerManagement"=dword:00000000
"DriverProtection"=dword:00000000
"PoFxStartDevicePowerManagement"=dword:00000000
"PoFxPowerControl"=dword:00000000
"DxgkWaitForIdle"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\NVIDIA Corporation\Global\Startup\SendTelemetryData]
@=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\Startup]
"SendTelemetryData"=dword:000```reg
00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\FTS]
"EnableGR535"=dword:00000000
"EnableRID44231"=dword:00000000
"EnableRID64640"=dword:00000000
"EnableRID66610"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler]
"DisableWriteCombining"=dword:00000001
"DisablePreemption"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Parameters]
"DisablePreemption"=dword:00000001
"DisableWriteCombining"=dword:00000001
"EnablePerformanceMode"=dword:00000001

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"EnablePreemption"=dword:00000000
"DisableWriteCombining"=dword:00000001
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableOverclockingAllPstates"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0001]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"EnablePreemption"=dword:00000000
"DisableWriteCombining"=dword:00000001
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableOverclockingAllPstates"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0002]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"EnablePreemption"=dword:00000000
"DisableWriteCombining"=dword:00000001
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableOverclockingAllPstates"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0003]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"EnablePreemption"=dword:00000000
"DisableWriteCombining"=dword:00000001
```reg
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableOverclockingAllPstates"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0004]
"RMAERRForceDisable"=dword:00000001
"RMNoECCFuseCheck"=dword:00000001
"RMDisableRCOnDBE"=dword:00000001
"RM1441072"=dword:00000001
"RMAERRHandling"=dword:00000000
"EnablePreemption"=dword:00000000
"DisableWriteCombining"=dword:00000001
"DisableAsyncPstates"=dword:00000001
"DisableDynamicPstate"=dword:00000001
"DisableOverclockedPstates"=dword:00000000
"EnablePerformanceMode"=dword:00000001
"RMEnableOverclockingAllPstates"=dword:00000001
"RmProfilingAdminOnly"=dword:00000000
```

### 3. Применение изменений

После того как вы создали файл `.reg`, выполните следующие шаги для его применения:

1. Дважды щелкните на созданный файл и подтвердите, что хотите внести изменения в реестр.
2. После этого перезагрузите компьютер, чтобы изменения вступили в силу.

### 4. Важные замечания

- **Осторожность**: Изменение параметров реестра может привести к нестабильной работе системы. Убедитесь, что вы понимаете, что делаете, и всегда создавайте резервные копии.
- **Тестирование**: После внесения изменений рекомендуется протестировать производительность вашей графической карты в играх или приложениях, чтобы убедиться, что изменения положительно сказались на работе системы.
- **Обновления драйверов**: Убедитесь, что у вас установлены последние версии драйверов Nvidia, так как они могут содержать оптимизации и исправления, которые улучшат производительность.

Следуя этим шагам, вы сможете настроить параметры Dwords для вашей графической карты Nvidia, что может привести к улучшению производительности и стабильности работы системы.

## Настройте NVIDIA Inspector

## Важность тестирования изменений в настройках

> **Не** слепо следуйте рекомендациям в этом разделе. **Проведите** бенчмарки указанных изменений, чтобы убедиться, что они приводят к положительному приросту производительности. Каждая система уникальна, и изменения, которые могут улучшить работу одной конфигурации, могут непреднамеренно ухудшить производительность другой. Поэтому важно подходить к настройкам с осторожностью и вниманием.

### 1. Зачем проводить бенчмарки?

Бенчмарки позволяют вам объективно оценить влияние изменений на производительность вашей системы. Это может включать в себя:

- **Измерение FPS (кадров в секунду)** в играх до и после внесения изменений.
- **Тестирование времени загрузки** приложений и игр.
- **Мониторинг температуры** и использования ресурсов, чтобы убедиться, что изменения не приводят к перегреву или чрезмерной нагрузке на систему.

### 2. Использование NVIDIA Profile Inspector

Для более тонкой настройки графических параметров вашей видеокарты Nvidia вы можете использовать [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector). Этот инструмент позволяет вам изменять различные настройки профилей для игр и приложений, что может помочь оптимизировать производительность.

1. **Скачайте и извлеките NVIDIA Profile Inspector**. Убедитесь, что вы используете последнюю версию для получения всех доступных функций.
   
2. **Примените личный профиль**. Я подготовил [личный профиль](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/files/base-nvidia-settings.nip), который можно использовать в качестве отправной точки для настройки. Этот профиль содержит оптимизированные параметры, которые могут помочь улучшить производительность в различных играх и приложениях.

### 3. Как применить профиль

- Откройте NVIDIA Profile Inspector.
- Импортируйте скачанный профиль, выбрав соответствующий файл.
- Примените изменения и протестируйте производительность вашей системы.

### 4. Заключение

Помните, что каждая система ведет себя по-разному, и то, что работает для одного пользователя, может не подойти другому. Поэтому всегда проводите тестирование и бенчмарки после внесения изменений, чтобы убедиться, что они действительно приносят пользу. Настройка системы — это процесс проб и ошибок, и важно находить оптимальные параметры именно для вашей конфигурации.
