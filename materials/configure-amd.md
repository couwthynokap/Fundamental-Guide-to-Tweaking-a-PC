# Настройка драйвера AMD

Оптимизация драйвера AMD может значительно улучшить производительность вашей видеокарты и обеспечить более стабильную работу в играх и приложениях. Следуйте этим шагам для настройки драйвера и панели управления AMD.

### 1. Установка драйвера

- Перейдите на [веб-сайт AMD](https://www.amd.com/en/support) и выберите свою видеокарту. Скачайте последнюю версию рекомендованного (WHQL) драйвера.
- Распакуйте загруженный драйвер в отдельную папку на вашем компьютере.
- Переместите папку `Packages\Drivers\Display\XXXX_INF` на рабочий стол (название папки может варьироваться в зависимости от версии драйвера). Удалите все файлы в этой папке, кроме следующих.

- В папке каталога драйверов (например, B381690) переместите файл `ccc2_install.exe` на рабочий стол. Этот файл будет использоваться на следующем этапе.

- Откройте файл `ccc2_install.exe` в текстовом редакторе, таком как Блокнот, и сохраните его с тем же именем в папке с драйвером.

- Откройте Диспетчер устройств, щелкните правой кнопкой мыши на дисплейном адаптере, выберите "Обновить драйвер", затем "Просмотреть мой компьютер для поиска драйверов" и укажите папку с драйверами.

- После установки драйвера разархивируйте `ccc2_install.exe` с помощью 7-Zip и запустите `CN\cnext\cnext64\ccc-next64.msi` для установки панели управления программного обеспечения Radeon.

- Убедитесь, что вы отключили службы AMD bloatware. Для этого нажмите `Win + R`, введите `services.msc` и отключите ненужные службы.

### 2. Настройка панели управления AMD

После установки драйвера откройте панель управления AMD и выполните следующие настройки:

- **Качество фильтрации текстур**: Установите на "Производительность".
- **Режим тесселяции**: Переопределите настройки приложения.
- **Максимальный уровень тесселяции**: Выключите.
  
- **FreeSync**: Эта функция может потенциально увеличить задержку ввода из-за дополнительной обработки. Однако со временем она была улучшена, поэтому не стесняйтесь проверить это самостоятельно — ваши результаты могут отличаться.
- **Масштабирование GPU**: Выключите.
- **Поддержка HDCP**: Отключите (требуется для DRM-контента).
  
- **Блокировка частоты/состояния**: Установите на 0.

### 3. Дополнительные инструменты

Для уменьшения времени рендеринга и джиттера, вызванного переходами частоты, используйте утилиты **OverdriveNTool** или **MorePowerTool**. Эти инструменты помогут вам более точно настроить параметры работы вашей видеокарты.

### 4. Настройка с помощью RadeonMod

Запустите утилиту **RadeonMod**, выберите свою видеокарту и перейдите на панель 0000. Найдите вкладку **Power Saving** и установите параметр **Enable Ulps** в 0. Это поможет улучшить управление энергопотреблением и производительность вашей видеокарты.

### 5. Настройка AMD Dwords

Оптимизация параметров Dwords в реестре Windows для видеокарт AMD может помочь улучшить производительность и стабильность системы. В этом руководстве мы рассмотрим, как внести изменения в реестр, чтобы настроить работу вашей видеокарты AMD. Данные Dwords предоставил энтузиаст [Imribiy](https://github.com/imribiy).

### 1. Подготовка к изменению реестра

Перед внесением изменений в реестр рекомендуется создать резервную копию текущих настроек. Это позволит вам восстановить систему в случае возникновения проблем. Для этого выполните следующие шаги:

1. Нажмите `Win + R`, введите `regedit` и нажмите `Enter`.
2. В редакторе реестра выберите `Файл` > `Экспорт`.
3. Выберите место для сохранения резервной копии и нажмите `Сохранить`.

### 2. Внесение изменений в реестр

Скопируйте следующий текст в текстовый редактор и сохраните его с расширением `.bat`, например, `amd_settings.bat`. Этот файл содержит необходимые изменения для оптимизации работы видеокарты AMD.

```bat
@echo Off
reg add "HKCU\Software\AMD\CN" /v "AutoUpdateTriggered" /t REG_DWORD /d "0" /f > nul 2>&1 > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "PowerSaverAutoEnable_CUR" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "BuildType" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "WizardProfile" /t REG_SZ /d "PROFILE_CUSTOM" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "UserTypeWizardShown" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "AutoUpdate" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "RSXBrowserUnavailable" /t REG_SZ /d "true" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "SystemTray" /t REG_SZ /d "false" /f > nul 2>&11
reg add "HKCU\Software\AMD\CN" /v "AllowWebContent" /t REG_SZ /d "false" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "CN_Hide_Toast_Notification" /t REG_SZ /d "true" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN" /v "AnimationEffect" /t REG_SZ /d "false" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN\OverlayNotification" /v "AlreadyNotified" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "HKCU\Software\AMD\CN\VirtualSuperResolution" /v "AlreadyNotified" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "PerformanceMonitorOpacityWA" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "DvrEnabled" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "ActiveSceneId" /t REG_SZ /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "PrevInstantReplayEnable" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "PrevInGameReplayEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "PrevInstantGifEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "RemoteServerStatus" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKCU\Software\AMD\DVR" /v "ShowRSOverlay" /t REG_SZ /d "false" /f > nul 2>&1
reg add "HKCU\Software\ATI\ACE\Settings\ADL\AppProfiles" /v "AplReloadCounter" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKLM\Software\AMD\Install" /v "AUEP" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "HKLM\Software\AUEP" /v "RSX_AUEPStatus" /t REG_DWORD /d "2" /f > nul 2>&1

for /f "tokens=*" %%k in ('reg query "%regPath%" ^| findstr /r /c:"\\000[0-9][0-9]*"') do (
reg add "%%k" /v "NotifySubscription" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k" /v "IsComponentControl" /t REG_BINARY /d "00000000" /f > nul 2>&1
reg add "%%k" /v "KMD_USUEnable" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "KMD_RadeonBoostEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "IsAutoDefault" /t REG_BINARY /d "01000000" /f > nul 2>&1
reg add "%%k" /v "KMD_ChillEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "KMD_DeLagEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "ACE" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AnisoDegree_SET" /t REG_BINARY /d "3020322034203820313600" /f > nul 2>&1
reg add "%%k\UMD" /v "Main3D_SET" /t REG_BINARY /d "302031203220332034203500" /f > nul 2>&1
reg add "%%k\UMD" /v "Tessellation_OPTION" /t REG_BINARY /d "3200" /f > nul 2>&1
reg add "%%k\UMD" /v "Tessellation" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "AAF" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "GI" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD" /v "CatalystAI" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD" /v "TemporalAAMultiplier_NA" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "ForceZBufferDepth" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "EnableTripleBuffering" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "ExportCompressedTex" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD" /v "PixelCenter" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "ZFormats_NA" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "DitherAlpha_NA" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "SwapEffect_D3D_SET" /t REG_BINARY /d "3020312032203320342038203900" /f > nul 2>&1
reg add "%%k\UMD" /v "TFQ" /t REG_BINARY /d "3200" /f > nul 2>&1
reg add "%%k\UMD" /v "VSyncControl" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "TextureOpt" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "TextureLod" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "ASE" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "ASD" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "ASTT" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AntiAliasSamples" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AntiAlias" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "AnisoDegree" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AnisoType" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "AntiAliasMapping_SET" /t REG_BINARY /d "3028303A302C313A3029203228303A322C313A3229203428303A342C313A3429203828303A382C313A382900" /f > nul 2>&1
reg add "%%k\UMD" /v "AntiAliasSamples_SET" /t REG_BINARY /d "3020322034203800" /f > nul 2>&1
reg add "%%k\UMD" /v "ForceZBufferDepth_SET" /t REG_BINARY /d "3020313620323400" /f > nul 2>&1
reg add "%%k\UMD" /v "SwapEffect_OGL_SET" /t REG_BINARY /d "3020312032203320342035203620372038203920313120313220313320313420313520313620313700" /f > nul 2>&1
reg add "%%k\UMD" /v "Tessellation_SET" /t REG_BINARY /d "31203220342036203820313620333220363400" /f > nul 2>&1
reg add "%%k\UMD" /v "HighQualityAF" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "DisplayCrossfireLogo" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AppGpuId" /t REG_BINARY /d "300078003000310030003000" /f > nul 2>&1
reg add "%%k\UMD" /v "SwapEffect" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "PowerState" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "AntiStuttering" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "TurboSync" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "SurfaceFormatReplacements" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "EQAA" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "ShaderCache" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD" /v "MLF" /t REG_BINARY /d "3000" /f > nul 2>&1
reg add "%%k\UMD" /v "TruformMode_NA" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "LRTCEnable" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "3to2Pulldown" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "MosquitoNoiseRemoval_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "MosquitoNoiseRemoval" /t REG_BINARY /d "350030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Deblocking_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Deblocking" /t REG_BINARY /d "350030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "DemoMode" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "OverridePA" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "DynamicRange" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "StaticGamma_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "BlueStretch_ENABLE" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "BlueStretch" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "LRTCCoef" /t REG_BINARY /d "3100300030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "DynamicContrast_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "WhiteBalanceCorrection" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Fleshtone_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Fleshtone" /t REG_BINARY /d "350030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "ColorVibrance_ENABLE" /t REG_BINARY /d "31000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "ColorVibrance" /t REG_BINARY /d "340030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Detail_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Detail" /t REG_BINARY /d "310030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Denoise_ENABLE" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "Denoise" /t REG_BINARY /d "360034000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "TrueWhite" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "OvlTheaterMode" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "StaticGamma" /t REG_BINARY /d "3100300030000000" /f > nul 2>&1
reg add "%%k\UMD\DXVA" /v "InternetVideo" /t REG_BINARY /d "30000000" /f > nul 2>&1
reg add "%%k\UMD" /v "Main3D_DEF" /t REG_SZ /d "1" /f > nul 2>&1
reg add "%%k\UMD" /v "Main3D" /t REG_BINARY /d "3100" /f > nul 2>&1
reg add "%%k" /v "DisableDMACopy" /t REG_DWORD /d "1" /f > nul 2>&1
reg add "%%k" /v "DisableBlockWrite" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "PP_ThermalAutoThrottlingEnable" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "%%k" /v "DisableDrmdmaPowerGating" /t REG_DWORD /d "1" /f > nul 2>&1
)
reg add "HKLM\System\CurrentControlSet\Services\amdwddmg" /v "ChillEnabled" /t REG_DWORD /d "0" /f > nul 2>&1
reg add "HKLM\System\CurrentControlSet\Services\AMD Crash Defender Service" /v "Start" /t REG_DWORD /d "4" /f > nul 2>&1
reg add "HKLM\System\CurrentControlSet\Services\AMD External Events Utility" /v "Start" /t REG_DWORD /d "4" /f > nul 2>&1
reg add "HKLM\System\CurrentControlSet\Services\amdfendr" /v "Start" /t REG_DWORD /d "4" /f > nul 2>&1
reg add "HKLM\System\CurrentControlSet\Services\amdfendrmgr" /v "Start" /t REG_DWORD /d "4" /f > nul 2>&1
reg add "HKLM\System\CurrentControlSet\Services\amdlog" /v "Start" /t REG_DWORD /d "4" /f > nul 2>&1
sc config amdlog start=disabled
sc config "AMD External Events Utility" start=disabled
pause
```

### 3. Применение изменений

После того как вы создали файл `.reg`, выполните следующие шаги для его применения:

1. Дважды щелкните на созданный файл и подтвердите, что хотите внести изменения в реестр.
2. После этого перезагрузите компьютер, чтобы изменения вступили в силу.

### 4. Важные замечания

- **Осторожность**: Изменение параметров реестра может привести к нестабильной работе системы. Убедитесь, что вы понимаете, что делаете, и всегда создавайте резервные копии.
- **Тестирование**: После внесения изменений рекомендуется протестировать производительность вашей видеокарты в играх или приложениях, чтобы убедиться, что изменения положительно сказались на работе системы.
- **Обновления драйверов**: Убедитесь, что у вас установлены последние версии драйверов AMD, так как они могут содержать оптимизации и исправления, которые улучшат производительность.

Следуя этим шагам, вы сможете оптимизировать драйвер AMD и улучшить производительность вашей системы в играх и приложениях.
