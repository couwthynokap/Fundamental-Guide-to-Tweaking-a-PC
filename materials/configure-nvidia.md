# Настройте драйвер NVIDIA

Если вам не нужен GeForce Experience, выполните следующие шаги, запустите программу установки драйверов и перейдите к настройке видеодрайвера. Если драйвер вам не нужен, распакуйте его архиватором в папку. Удалите все файлы из папки, оставив только необходимые файлы.

```
Display.Driver
NVI2
EULA.txt
ListDevices.txt
setup.cfg
setup.exe
```

- Откройте файл setup.cfg с помощью блокнота и удалите следующие три строки:

```
<file name=«${{EulaHtmlFile}}» />
<file name=«${{FunctionalConsentFile}}» />
<file name=«${{PrivacyPolicyFile}}» />
```

- Откройте CMD и введите следующую команду для отключения телеметрии

```bat
reg add «HKLM\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\Startup\SendTelemetryData» /t REG_DWORD /d «0» /f
```

- Запустите файл setup.exe и установите драйвер.

### Настройка MSI Afterburner

В программе MSI Afterburner необходимо отключить ограничения или увеличить их до максимума, а также включить стабильные напряжения, мониторинг напряжений и запомнить модель видеокарты. После в браузере найдите паспортное повышение частоты и запомните его. 

В программе MSI Afterburner включите key boost, для чего необходимо поставить скин [EVGA SKIN](https://drive.google.com/file/d/1buaP5Gv7f3Jv3OPQzKWF6Q7fSvxft2a0/view?usp=sharing). Для этого скачайте архив с папкой skins и скопируйте файл default в папку skins. После перезагрузки компьютера выберите скин и включите keyboost.

### Настройка видеодрайвера

Если вам нужна панель управления NVIDIA для настройки параметров 3D, возможно, вам не хватает данных. Трогать ее имеет смысл только в том случае, если вы используете G-SYNC. Все настройки 3D бесполезны. При необходимости измените остальные настройки в других разделах.

### Блокировка частоты / P-State0

- Мы заставим P-State 0 с помощью специального параметра в реестре, чтобы уменьшить время рендеринга и джиттер, вызванный переходами частоты.

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000]
```

Этот путь не будет идентичным во всех случаях, так как номер 0000 относится к конкретной видеокарте и может быть переписан при установке драйверов или перемещении GPU в другой слот. Чтобы определить подходящий номер ссылки (например, 0000, 0001, 0002), откройте редактор реестра и перейдите по указанному ниже пути, затем посмотрите на значения «DriverDesc или HardwareInformation.AdapterString», которые должны содержать имя адаптера видеокарты, например NVIDIA GeForce GTX 1050. (timecard).

- Узнав путь, создайте файл типа REG.DWORD с именем DisableDynamicPstate и установите значение 1.

## Lock GPU Clocks/P-State 0

Принудительно включите P-State 0 с помощью [ключа реестра](https://github.com/djdallmann/GamingPCSetup/blob/master/CONTENT/RESEARCH/WINDRIVERS/README.md#q-is-there-a-registry-setting-that-can-force-your-display-adapter-to-remain-at-its-highest-performance-state-pstate-p0), приведенного ниже (требуется перезагрузка). Убедитесь, что ключ драйвера изменен на тот, который соответствует нужному графическому процессору NVIDIA ([пример](/assets/images/find-driver-key-example.png)). Это уменьшает нежелательную задержку выполнения новых инструкций, когда устройство переходит в состояние более глубокого энергосбережения за счет более высоких температур простоя и энергопотребления

``bat
reg add «HKLM\SYSTEM\CurrentControlSet\Control\Class\{4d36e968-e325-11ce-bfc1-08002be10318}\0000» /v «DisableDynamicPstate» /t REG_DWORD /d «1» /f
``

# Настройте панель управления NVIDIA

### Управление настройками 3D

> Если вы настраиваете систему для общего использования, например, для работы или учебы, пропустите этот шаг, так как он не требуется.

- Анизотропная фильтрация - Выкл.

- Сглаживание - Гамма-коррекция - Выкл.

- Режим низкой задержки - Вкл/Ультра

> Если игра поддерживает режим NVIDIA Reflex Low Latency, мы рекомендуем использовать этот режим вместо режима Ultra Low Latency в драйвере. Однако если вы оставите оба режима включенными, режим Reflex Low Latency будет иметь более высокий приоритет автоматически ([1](https://www.nvidia.com/en-gb/geforce/news/reflex-low-latency-platform)).

- Режим управления питанием - Предпочитает максимальную производительность

- Размер шейдерного кэша - Неограниченно

- Фильтрация текстур - Качество - Высокая производительность

- Потоковая оптимизация - разгружает задачи обработки, связанные с GPU, на CPU ([1](https://tweakguides.pcgamingwiki.com/NVFORCE_8.html)). Обычно это вредит частоте кадров, поскольку отнимает процессорное время у приложения, работающего в реальном времени. Если вы решите включить эту настройку, вам также следует определить, нет ли у вас уже узкого места для процессора.

- Убедитесь, что настройки не переопределяются для программ на вкладке ``Настройки программы``, например, параметр Image Sharpening для некоторых игр EAC.

### Изменить разрешение

- Выходной динамический диапазон - Полный

### Настройка параметров цвета видео

- Динамический диапазон - Полный

## Настройка Nvidia Dwords

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power]
"ExitLatency"=dword:00000001 
"ExitLatencyCheckEnabled"=dword:00000001
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

## Настройте NVIDIA Inspector
> 📊 **Не** слепо следуйте рекомендациям в этом разделе. **Проведите** бенчмарки указанных изменений, чтобы убедиться, что они приводят к положительному приросту производительности, поскольку каждая система ведет себя по-разному и изменения могут непреднамеренно ухудшить производительность.

Скачайте и извлеките [NVIDIA Profile Inspector](https://github.com/Orbmu2k/nvidiaProfileInspector) Пожалуйста, скачайте мой [личный профиль]([https://drive.google.com/file/d/18PiWZ9HR8BPmGbdr5MyJzn8fwDlbCoxW/view?usp=sharing](https://github.com/couwthynokap/Fundamental-guide-to-tweaking-a-pc/blob/main/bin/base-nvidia-settings.nip)) и примените его.
