# Настройка драйвера NVIDIA

## 1. Установка DDU и удаление старых драйверов

- После загрузки в безопасном режиме скачайте и запустите утилиту DDU (Display Driver Uninstaller). Вы можете скачать её по следующей ссылке: [Скачать DDU](https://www.guru3d.com/files-get/display-driver-uninstaller-download,19.html). 

- Настройки данной программы можно увидеть на изображении: ![Настройки DDU](https://i.imgur.com/E7ZH1ww.png). После этого выберите драйвер и удалите его.

---

## 2. Установка драйвера через NVCleanstall

- Многие пользователи не знают, какую версию драйвера устанавливать. Мой совет: ставьте только последние версии или ту, которую выбрал вам NVCleanstall. В данном окне ничего не нужно ставить, как показано на изображении: ![Настройки NVCleanstall](https://i.imgur.com/ATvSjgc.png).

- Если вам нужен GeForce Experience, скачайте его после установки видеодрайвера. В другом окне ставьте строго эти галки, никаких других, так как в разделе `Show Expert Tweaks` пункт `Disable Driver Telemetry` может вызвать недействительность сертификата, в результате чего драйвер не установится на 24h2. Смотрите изображение: ![Галочки NVCleanstall](https://i.imgur.com/3yXMkB4.png).

- После установки нажмите сюда: ![Удаление папки GFExperience](https://i.imgur.com/G9vjQjU.png) и удалите папку с названием GFExperience. В файле `setup.cfg` удалите следующие строки:
  ```
  <<filename="S{{Eula Html File}}" />
  <<file name="${{Functional Consent File}}" />
  <<file name="${{Privacy Policy File}}" />
  ```

---

## 3. Полное удаление телеметрии NVIDIA

- Если вам не нужен GeForce Experience, откройте данный BAT файл:

```bat
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
    ...
    echo                                    Removing GeForce components.
    goto start
) else if /i "%userChoice%"=="y" (
    echo                                    Skipping GeForce components.
    goto start
) else (
    echo Invalid choice. Please type 'y' or 'n'.
    goto choice
)
```

---

## 4. Блокировка частот GPU/состояния 0 (P-State 0)

- Принудительно включите P-State 0 с помощью следующего ключа реестра (требуется перезагрузка). Убедитесь, что ключ драйвера изменен на тот, который соответствует вашему графическому процессору NVIDIA. Это уменьшает нежелательную задержку выполнения новых инструкций, когда устройство переходит в состояние более глубокого энергосбережения.

```bat
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000" /v "DisableDynamicPstate" /t REG_DWORD /d "1" /f
```

---

## 5. Настройка NVIDIA Inspector

- Скачайте и распакуйте [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector). Эта утилита позволяет детально настраивать параметры графических драйверов NVIDIA, что может значительно улучшить производительность в играх и приложениях.

- **Отключите `Enable Ansel`**: Ansel — это функция, которая позволяет делать высококачественные скриншоты в играх. Однако она может внедряться во все игры драйверами дисплея, что иногда вызывает конфликты со сторонними инструментами или инжекторами. Отключение этой функции может помочь избежать проблем с совместимостью и повысить стабильность работы.

- **Эксперименты с Resizable BAR**: Если вы хотите попробовать принудительную настройку Resizable BAR в неподдерживаемых играх, это может привести к потенциальному повышению производительности. Resizable BAR позволяет процессору обращаться к видеопамяти более эффективно, что может улучшить производительность в некоторых сценариях. Для этого вам нужно будет переключить следующие опции в NVIDIA Profile Inspector:
  - **rBAR - Feature**: Включите эту опцию, чтобы активировать поддержку Resizable BAR.
  - **rBAR - Options**: Убедитесь, что эта опция настроена на использование Resizable BAR.
  - **rBAR - Size Limit**: Установите размер, который будет использоваться для Resizable BAR. Обычно рекомендуется использовать максимальный размер, поддерживаемый вашей системой.

- **Использование пресета настроек**: У меня есть свой пресет настройки NVIDIA Inspector, который вы можете использовать для оптимизации производительности. Вы можете скачать его по следующей ссылке: [base-nvidia-settings.nip](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/files/base-nvidia-settings.nip). Этот пресет включает в себя оптимальные настройки для различных игр и приложений, что позволяет улучшить качество графики и производительность.

  - Чтобы применить пресет, откройте NVIDIA Profile Inspector и выберите опцию импорта. Найдите загруженный файл и импортируйте его в программу. После этого настройки будут автоматически применены к вашей видеокарте.

- **Настройка параметров производительности**: В NVIDIA Profile Inspector вы можете настроить множество параметров, таких как:
  - **Сглаживание**: Настройте уровень сглаживания для уменьшения зазубрин на краях объектов.
  - **Тени**: Измените параметры теней для улучшения их качества или производительности.
  - **Текстуры**: Настройте качество текстур для повышения детализации в играх.
  - **Фильтрация**: Измените параметры фильтрации текстур для улучшения качества изображения.

- **Сохранение и тестирование**: После внесения всех изменений не забудьте сохранить настройки. Рекомендуется протестировать производительность в играх после применения новых параметров, чтобы убедиться, что они действительно улучшают игровой процесс. Если вы заметите проблемы или снижение производительности, вы всегда можете вернуться к предыдущим настройкам.

---

## 6. Настройка MSI Afterburner

MSI Afterburner — это мощный инструмент для разгона видеокарт. Чтобы оптимизировать работу видеокарты, выполните следующие шаги:

1. **Отключение ограничений**: В интерфейсе MSI Afterburner отключите ограничения или увеличьте их до максимума.
2. **Настройка напряжений**: Включ2. **Настройка напряжений**: Включите стабильные напряжения и мониторинг напряжений. Это важно для обеспечения надежной работы видеокарты и предотвращения перегрева или нестабильной работы.

3. **Запомните модель видеокарты**: Убедитесь, что вы знаете модель своей видеокарты. Это поможет вам в дальнейшем искать информацию о паспортном повышении частоты и других характеристиках.

4. **Поиск паспортного повышения частоты**: В браузере найдите паспортное повышение частоты для вашей модели видеокарты. Это даст вам представление о том, на сколько можно увеличить частоты без риска повреждения устройства.

5. **Включение Key Boost**: Для активации функции Key Boost в MSI Afterburner вам потребуется установить специальный скин. Скачайте скин [EVGA SKIN](https://drive.google.com/file/d/1buaP5Gv7f3Jv3OPQzKWF6Q7fSvxft2a0/view?usp=sharing).

   - После загрузки архива скопируйте папку `skins` в директорию установки MSI Afterburner.
   - Скопируйте файл `default` в папку `skins`.

6. **Перезагрузка компьютера**: После установки скина перезагрузите компьютер.

7. **Выбор скина и активация Key Boost**: Запустите MSI Afterburner, выберите установленный скин и активируйте функцию Key Boost. Это позволит вам использовать дополнительные возможности разгона и улучшить производительность вашей видеокарты.

---

## 7. Дополнительные советы

- **Мониторинг температуры**: Используйте MSI Afterburner или другие утилиты для мониторинга температуры видеокарты во время игр и стресс-тестов. Это поможет избежать перегрева и обеспечить стабильную работу.

- **Тестирование стабильности**: После разгона проведите стресс-тесты с помощью программ, таких как FurMark или Unigine Heaven, чтобы убедиться в стабильности системы. Если возникают сбои или артефакты, уменьшите частоты или напряжения.

- **Регулярные обновления**: Следите за обновлениями драйверов NVIDIA и программного обеспечения для разгона. Новые версии могут содержать улучшения производительности и исправления ошибок.

- **Создание резервной копии**: Перед внесением изменений в настройки драйвера или разгона создайте резервную копию текущих настроек. Это позволит вам быстро восстановить систему в случае проблем.

## 8. Внесение изменений в реестр

Для оптимизации работы графической карты NVIDIA вы можете внести изменения в реестр Windows. Следуйте приведенным ниже инструкциям, чтобы создать файл реестра с необходимыми настройками.

1. **Создание файла реестра**: Скопируйте следующий текст в текстовый редактор, например, Блокнот. После этого сохраните файл с расширением `.reg`, например, `nvidia_settings.reg`.

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
"SendTelemetryData"=dword:00000000

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

### Важные замечания

- **Риски**: Внесение изменений в реестр может повлиять на работу вашей системы. Некоторые из этих настроек могут привести к нестабильности или даже поломке драйвера на определенных видеокартах. Поэтому используйте этот файл на свой страх и риск. Рекомендуется создать резервную копию реестра перед внесением изменений.

- **Создание резервной копии реестра**: Чтобы создать резервную копию реестра, выполните следующие шаги:
  1. Нажмите `Win + R`, введите `regedit` и нажмите `Enter`.
  2. В редакторе реестра выберите `Файл` > `Экспорт`.
  3. Выберите место для сохранения резервной копии и дайте ей имя.
  4. Убедитесь, что выбран параметр "Все" в разделе "Диапазон экспорта", и нажмите `Сохранить`.

- **Применение изменений**: После создания файла `.reg` дважды щелкните по нему и подтвердите внесение изменений в реестр. Вы также можете импортировать файл через редактор реестра, выбрав `Файл` > `Импорт` и указав путь к вашему файлу.

- **Перезагрузка**: После внесения изменений в реестр рекомендуется перезагрузить компьютер, чтобы они вступили в силу.

Следуя этим шагам, вы сможете оптимизировать работу вашей графической карты NVIDIA, однако всегда помните о рисках, связанных с изменениями в реестре.
