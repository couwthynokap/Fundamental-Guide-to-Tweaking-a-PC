# Конфигурация сети

## 1. Предисловие

Перед выполнением любых действий убедитесь, что установлен драйвер сетевой карты.

## 2. Кабельные соединения

К наиболее распространенным типам кабелей относятся UTP, FTP, STP, S/FTP, S/STP, а также стандарты cat5, cat5e, cat6, cat6a, cat7 и cat8. Идеальным и самым дорогим вариантом является использование экранированного кабеля cat8 (STP) длиной не более 50 см. В случае ограниченного бюджета (и низкой скорости интернета) рекомендуется обратить внимание на экранированные кабели cat5e или cat6 (STP или S/STP). Это обеспечит более стабильное соединение с сетью.

## 3. Важные факты (о которых мало кто знает)

Производство всех сетевых адаптеров в Китае стоит около 5 долларов. Смена провайдера трафика с циклического на более чувствительный к задержкам может привести к увеличению скорости соединения до ±500 раз. Многие провайдеры используют агрегацию пакетов, что позволяет увеличить скорость загрузки за счет объединения нескольких пакетов в один. Некоторые сетевые карты, например Solarflare, имеют время задержки, которое может повлиять на производительность.

## 4. Выберите сетевой адаптер

Если у вас установлен адаптер Realtek, вы можете столкнуться с проблемами, в то время как адаптеры Intel обычно обеспечивают надежную работу. Предпочтительным вариантом является использование встроенных сетевых адаптеров Intel или внешних адаптеров той же марки. Не забывайте периодически обновлять драйверы для сетевого адаптера (LAN/WI-FI), загружая их с официального сайта производителя материнской платы.

## 5. Немного теории

- **Скорость Интернета** определяется как количество битов информации, передаваемых в секунду, и измеряется в килобитах в секунду (Кбит/с), мегабитах в секунду (Мбит/с) или гигабитах в секунду (Гбит/с). Можно выполнить [тест скорости Интернета](http://www.dslreports.com/speedtest).

- **Потеря пакетов** происходит, когда один или несколько пакетов не достигают адреса назначения во время передачи данных. Вы можете выполнить [тест потери пакетов](https://packetlosstest.com).

- **Чрезмерная буферизация сети** может привести к увеличению задержки и джиттера, а также к снижению пропускной способности. Можно выполнить тест на чрезмерную [сетевую буферизацию](https://www.waveform.com/tools/bufferbloat).

## 6. Настройки сетевого адаптера

>**⚠**
> Настройки разгрузки в сетевых картах позволяют делегировать определенные функции обработки пакетов, что снижает нагрузку на процессор. Это, в свою очередь, позволяет выделить больше процессорного времени для других задач и игр, улучшая общую производительность системы.

### Рекомендации для сетевых адаптеров Realtek и Intel

Для оптимизации работы сетевого адаптера Realtek выполните следующий скрипт в командной строке с правами администратора:

```bat
@echo off
:: Ensure admin privileges
fltmc >nul 2>&1 || (
    echo Administrator privileges are required.
    PowerShell Start -Verb RunAs '%0' 2> nul || (
        echo Right-click on the script and select "Run as administrator".
        pause & exit 1
    )
    exit 0
)
setlocal EnableExtensions DisableDelayedExpansion

for /f %%a in ('reg query "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e972-e325-11ce-bfc1-08002be10318}" /v "*SpeedDuplex" /s ^| findstr  "HKEY"') do (
    for /f %%i in ('reg query "%%a" /v "*DeviceSleepOnDisconnect" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*DeviceSleepOnDisconnect" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "*EEE" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*EEE" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "*ModernStandbyWoLMagicPacket" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*ModernStandbyWoLMagicPacket" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "*SelectiveSuspend" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*SelectiveSuspend" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "*WakeOnMagicPacket" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*WakeOnMagicPacket" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "*WakeOnPattern" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "*WakeOnPattern" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "AutoPowerSaveModeEnabled" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "AutoPowerSaveModeEnabled" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "EEELinkAdvertisement" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "EEELinkAdvertisement" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "EeePhyEnable" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "EeePhyEnable" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "EnableGreenEthernet" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "EnableGreenEthernet" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "EnableModernStandby" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "EnableModernStandby" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "GigaLite" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "GigaLite" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "PnPCapabilities" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "PnPCapabilities" /t REG_DWORD /d "24" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "PowerDownPll" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "PowerDownPll" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "PowerSavingMode" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "PowerSavingMode" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "ReduceSpeedOnPowerDown" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "ReduceSpeedOnPowerDown" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "S5WakeOnLan" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "S5WakeOnLan" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "SavePowerNowEnabled" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "SavePowerNowEnabled" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "ULPMode" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "ULPMode" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "WakeOnLink" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "WakeOnLink" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "WakeOnSlot" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "WakeOnSlot" /t REG_SZ /d "0" /f >nul 2>&1
    )
    for /f %%i in ('reg query "%%a" /v "WakeUpModeCap" ^| findstr "HKEY"') do (
        Reg.exe add "%%i" /v "WakeUpModeCap" /t REG_SZ /d "0" /f >nul 2>&1
    )
) >nul 2>&1
cls
powershell disable-netadapterbinding -name "*" -componentid vmware_bridge, ms_lldp, ms_lltdio, ms_implat, ms_tcpip6, ms_rspndr, ms_server, ms_msclient
cls
SETLOCAL EnableDelayedExpansion
for /f "tokens=1,2*" %%i in ('reg query "HKLM\SYSTEM\CurrentControlSet\Control\Class\{4D36E972-E325-11CE-BFC1-08002bE10318}" /s /v "*IfType"^| findstr /i "HKEY 0x6"') do if /i "%%i" neq "*IfType" (set REGPATH_ETHERNET=%%i) else (
    reg add "!REGPATH_ETHERNET!" /v "*DeviceSleepOnDisconnect" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*FlowControl" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*InterruptModeration" /t REG_SZ /d "1" /f 
    reg add "!REGPATH_ETHERNET!" /v "*IPChecksumOffloadIPv4" /t REG_SZ /d "3" /f 
    reg add "!REGPATH_ETHERNET!" /v "*JumboPacket" /t REG_SZ /d "1514" /f 
    reg add "!REGPATH_ETHERNET!" /v "*LsoV1IPv4" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*LsoV2IPv4" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*LsoV2IPv6" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*ModernStandbyWoLMagicPacket" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*PriorityVLANTag" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*RSS" /t REG_SZ /d "1" /f 
    reg add "!REGPATH_ETHERNET!" /v "*RssBaseProcNumber" /t REG_SZ /d "1" /f 
    reg add "!REGPATH_ETHERNET!" /v "*RssMaxProcNumber" /t REG_SZ /d "1" /f 
    reg add "!REGPATH_ETHERNET!" /v "*SpeedDuplex" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*TCPChecksumOffloadIPv4" /t REG_SZ /d "3" /f 
    reg add "!REGPATH_ETHERNET!" /v "*TCPChecksumOffloadIPv6" /t REG_SZ /d "3" /f 
    reg add "!REGPATH_ETHERNET!" /v "*UDPChecksumOffloadIPv4" /t REG_SZ /d "3" /f 
    reg add "!REGPATH_ETHERNET!" /v "*UDPChecksumOffloadIPv6" /t REG_SZ /d "3" /f 
    reg add "!REGPATH_ETHERNET!" /v "*WakeOnMagicPacket" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "*WakeOnPattern" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_ETHERNET!" /v "ITR" /t REG_SZ /d "65535" /f 
    reg add "!REGPATH_ETHERNET!" /v "TxIntDelay" /t REG_SZ /d "5" /f 

    reg query "!REGPATH_ETHERNET!" /v "ProviderName" | findstr "Intel" 
    if !ERRORLEVEL! equ 0 (
        reg add "!REGPATH_ETHERNET!" /v "AdaptiveIFS" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "AutoPowerSaveModeEnabled" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "EEELinkAdvertisement" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "EnablePME" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "EnableTss" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "LinkNegotiationProcess" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_ETHERNET!" /v "LogLinkStateEvent" /t REG_SZ /d "16" /f 
        reg add "!REGPATH_ETHERNET!" /v "MasterSlave" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "ULPMode" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "ReduceSpeedOnPowerDown" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "SavePowerNowEnabled" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "SipsEnabled" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "WaitAutoNegComplete" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "WakeOnLink" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "WakeOnSlot" /t REG_SZ /d "0" /f 
    )
    reg query "!REGPATH_ETHERNET!" /v "ProviderName" | findstr "Realtek" 
    if !ERRORLEVEL! equ 0 (
        reg add "!REGPATH_ETHERNET!" /v "*EEE" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "AdvancedEEE" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "AutoDisableGigabit" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "EnableGreenEthernet" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "GigaLite" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "PowerSavingMode" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "S5WakeOnLan" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_ETHERNET!" /v "WolShutdownLinkSpeed" /t REG_SZ /d "2" /f 
    )
)
call:POWERSHELL "$NetAdapters = Get-NetAdapterHardwareInfo | Get-NetAdapter | Where-Object {$_.Status -eq 'Up'};foreach ($NetAdapter in $NetAdapters) {$MaxNumRssQueues = [int](($NetAdapter | Get-NetAdapterAdvancedProperty -RegistryKeyword '*NumRssQueues').ValidRegistryValues | Measure-Object -Maximum).Maximum;$NetAdapter | Set-NetAdapterAdvancedProperty -RegistryKeyword '*NumRssQueues' -RegistryValue $MaxNumRssQueues}"
call:POWERSHELL "$NetAdapters = Get-NetAdapterHardwareInfo | Get-NetAdapter | Where-Object {$_.Status -eq 'Up'};foreach ($NetAdapter in $NetAdapters) {$iReceiveBuffers = [int]($NetAdapter | Get-NetAdapterAdvancedProperty -RegistryKeyword '*ReceiveBuffers').NumericParameterMaxValue;$iTransmitBuffers = [int]($NetAdapter | Get-NetAdapterAdvancedProperty -RegistryKeyword '*TransmitBuffers').NumericParameterMaxValue;$NetAdapter | Set-NetAdapterAdvancedProperty -RegistryKeyword '*ReceiveBuffers' -RegistryValue $iReceiveBuffers;$NetAdapter | Set-NetAdapterAdvancedProperty -RegistryKeyword '*TransmitBuffers' -RegistryValue $iTransmitBuffers}"
for /f "tokens=1,2*" %%i in ('reg query "HKLM\SYSTEM\CurrentControlSet\Control\Class\{4D36E972-E325-11CE-BFC1-08002bE10318}" /s /v "*IfType"^| findstr /i "HKEY 0x47"') do if /i "%%i" neq "*IfType" (set REGPATH_WIFI=%%i) else (
    reg add "!REGPATH_WIFI!" /v "*DeviceSleepOnDisconnect" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*PacketCoalescing" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*PMARPOffload" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*PMNSOffload" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*PMWiFiRekeyOffload" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*PriorityVLANTag" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*WakeOnMagicPacket" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "*WakeOnPattern" /t REG_SZ /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "WirelessMode" /t REG_SZ /d "34" /f
    reg add "!REGPATH_WIFI!" /v "ScanWhenAssociated" /t REG_DWORD /d "0" /f 
    reg add "!REGPATH_WIFI!" /v "ScanDisableOnLowTraffic" /t REG_DWORD /d "1" /f
    reg add "!REGPATH_WIFI!" /v "ScanDisableOnMediumTraffic" /t REG_DWORD /d "1" /f 
    reg add "!REGPATH_WIFI!" /v "ScanDisableOnHighOrMulticast" /t REG_DWORD /d "1" /f 
    reg add "!REGPATH_WIFI!" /v "ScanDisableOnLowLatencyOrQos" /t REG_DWORD /d "1" /f 

    reg query "!REGPATH_WIFI!" /v "ProviderName" | findstr "Intel" 
    if !ERRORLEVEL! equ 0 (
        reg add "!REGPATH_WIFI!" /v "BgScanGlobalBlocking" /t REG_SZ /d "2" /f 
        reg add "!REGPATH_WIFI!" /v "CtsToItself" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_WIFI!" /v "FatChannelIntolerant" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "IbssQosEnabled" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "IbssTxPower" /t REG_SZ /d "100" /f 
        reg add "!REGPATH_WIFI!" /v "MIMOPowerSaveMode" /t REG_SZ /d "3" /f 
        reg add "!REGPATH_WIFI!" /v "RoamAggressiveness" /t REG_SZ /d "0" /f
        reg add "!REGPATH_WIFI!" /v "ThroughputBoosterEnabled" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_WIFI!" /v "PropPacketBurstEnabled" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_WIFI!" /v "uAPSDSupport" /t REG_SZ /d "0" /f
    )
    reg query "!REGPATH_WIFI!" /v "ProviderName" | findstr "Realtek"
    if !ERRORLEVEL! equ 0 (
        reg add "!REGPATH_WIFI!" /v "ARPOffloadEnable" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "b40Intolerant" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "bLeisurePs" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "GTKOffloadEnable" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "InactivePs" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "NSOffloadEnable" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "ProtectionMode" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_WIFI!" /v "RegROAMSensitiveLevel" /t REG_SZ /d "127" /f 
        reg add "!REGPATH_WIFI!" /v "RTD3Enable" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "TxPwrLevel" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "WakeOnDisconnect" /t REG_SZ /d "1" /f 
        reg add "!REGPATH_WIFI!" /v "WoWLANLPSLevel" /t REG_SZ /d "0" /f 
        reg add "!REGPATH_WIFI!" /v "WoWLANS5Support" /t REG_SZ /d "0" /f 
    )
)
pause
```

- **Эти рекомендации направлены на оптимизацию производительности сети и снижение задержек. За более подробной информацией и пояснениями обращайтесь к руководствам Realtek, Intel и Microsoft по настройке производительности сетевой подсистемы, доступным в разделе «Технические ссылки».**

## 7. Дополнительные рекомендации по настройке

- Убедитесь, что все изменения в реестре и параметры сетевого адаптера применяются корректно. Это поможет избежать проблем с подключением и производительностью сети.

- Если у вас возникли трудности с выполнением скрипта, проверьте наличие прав администратора и правильность написания команд.

- Рекомендуется периодически проверять обновления драйверов и системных компонентов, чтобы поддерживать оптимальную производительность системы.

- Для получения дополнительной информации о настройках сетевой подсистемы и их влиянии на производительность, ознакомьтесь с официальной документацией от Intel и Microsoft.

### Конфигурация для конкретной операционной системы

## Настройка NetworkThrottlingIndex

Перед тем как вносить изменения, убедитесь, что функция индекса регулирования сети включена. Это критически важно для оптимизации производительности сети и обеспечения качественного воспроизведения мультимедийного контента.

- **Рекомендация по значению**: Установите значение от 10 до 20 после запятой, например, 15–30 Мбит/с. Это значение позволяет сбалансировать пропускную способность и задержку.

## 3. Изменение настроек в реестре

>**⚠**
>  Я не утверждаю, что это идеальная конфигурация реестра и что у неё нет недостатков. При желании вы можете самостоятельно внести изменения в файл конфигурации. **Скрипт не восстанавливает настройки при изменении значений с "включено" на "выключено".**

### Шаги для изменения параметра NetworkThrottlingIndex:

1. **Открытие редактора реестра**:
   - Нажмите `Win + R`, введите `regedit` и нажмите `Enter`.

2. **Навигация к нужному пути**:
   - Перейдите к следующему пути:
     ```
     HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile
     ```

3. **Изменение параметра**:
   - Найдите параметр `NetworkThrottlingIndex`.
   - Если параметр отсутствует, создайте новый:
     - Щелкните правой кнопкой мыши на правой панели, выберите `Создать` > `DWORD (32-бит)`.
     - Назовите его `NetworkThrottlingIndex`.

### Установка значений

- **Включено**: Установите значение `10` (десятичное).
- **Отключено**: Установите значение `0xFFFFFFFF` (шестнадцатеричное).

## 4. Проверка изменений

После внесения изменений рекомендуется проверить их влияние на производительность сети. Для этого можно использовать инструмент `xperf`, который позволяет захватывать данные DPC и анализировать их.

### Использование xperf для анализа DPC

1. **Установка Windows Performance Toolkit**:
   - Установите Windows Performance Toolkit, который входит в состав Windows SDK.

2. **Запуск захвата данных**:
   - Откройте командную строку с правами администратора.
   - Введите следующую команду для начала захвата:
     ```cmd
     xperf -start MySession -on DPC -stackwalk DPC -buffering 1024
     ```
   - Запустите приложение или игру, для которой вы хотите проверить производительность.

3. **Остановка захвата**:
   - После завершения теста введите:
     ```cmd
     xperf -stop MySession
     ```

4. **Анализ результатов**:
   - Сохраните результаты в файл:
     ```cmd
     xperf -save MySession.etl
     ```
   - Откройте файл в Windows Performance Analyzer (WPA) для анализа задержек DPC и других метрик.

Настройка NetworkThrottlingIndex может значительно повлиять на производительность сети и качество мультимедийного контента. Важно помнить, что отключение этой функции может привести к увеличению задержки DPC, что негативно скажется на производительности приложений, требующих низкой задержки, таких как видеоигры.

### Рекомендации

- **Тестируйте изменения**: После внесения изменений обязательно проводите тестирование, чтобы оценить влияние на производительность.
- **Следите за показателями**: Обратите внимание на задержку и пропускную способность, чтобы найти оптимальные настройки для вашей системы.
- **Документируйте изменения**: Ведите записи о внесенных изменениях, чтобы в будущем можно было легко откатить настройки при необходимости.

### Сетевые протоколы

### Настройки для оптимизации сетевых протоколов

Оптимизация сетевых протоколов является важной задачей для повышения производительности и надежности сетевых соединений. Одним из подходов к этой оптимизации является использование технологии NestH, которая может значительно снизить задержки в интернете и улучшить работу TCP-программ.

NestH (Network Enhanced Streaming and Transport for High-performance) представляет собой набор методов и инструментов, направленных на улучшение передачи данных по сети. Основная цель этой технологии — минимизация задержек, возникающих из-за различных факторов, таких как перегрузка сети, потеря пакетов и неэффективное использование пропускной способности.

Ключевым аспектом NestH является адаптивное управление потоком данных, позволяющее динамически регулировать скорость передачи в зависимости от текущих условий сети. Это особенно важно для TCP-программ, которые могут страдать от задержек и потерь пакетов. Используя алгоритмы предсказания и анализа, NestH может заранее определять оптимальные параметры передачи, что приводит к более стабильному и быстрому соединению.

Кроме того, NestH включает механизмы для улучшения обработки ошибок и восстановления после потерь пакетов, что позволяет TCP-программам более эффективно реагировать на проблемы в сети, минимизируя время простоя и улучшая общую производительность.

Внедрение технологий, подобных NestH, может существенно повысить качество интернет-соединений, что особенно актуально в условиях растущих требований к скорости и надежности передачи данных. Оптимизация сетевых протоколов через такие решения не только улучшает работу существующих приложений, но и открывает новые возможности для разработки более сложных и требовательных к ресурсам сервисов.

## Настройки Netsh

Для оптимизации сетевых протоколов в Windows используйте следующие команды:

```bat
netsh int tcp set global autotuninglevel=normal
netsh int tcp set heuristics disabled
netsh int tcp set global chimney=disabled
netsh int tcp set global netdma=disabled
netsh int tcp set global dca=enabled
netsh int tcp set global rss=enabled
netsh int tcp set global rsc=disabled
netsh int tcp set global ecncapability=default
netsh int tcp set global timestamps=disabled
netsh int tcp set global initialRto=2000
```

### 1. `netsh int tcp set global autotuninglevel=normal`
- **Описание**: Управляет автоматическим регулированием окна TCP. Установка значения `normal` позволяет системе автоматически настраивать размер окна в зависимости от условий сети.
- **Рекомендация**: Используйте это значение для большинства сценариев, так как оно обеспечивает баланс между производительностью и стабильностью.

### 2. `netsh int tcp set heuristics disabled`
- **Описание**: Отключает эвристические алгоритмы, которые могут влиять на поведение TCP.
- **Рекомендация**: Отключение эвристик может быть полезно в средах с предсказуемыми условиями сети.

### 3. `netsh int tcp set global chimney=disabled`
- **Описание**: Отключает поддержку TCP Chimney Offload, снижая нагрузку на процессор.
- **Рекомендация**: Отключение может быть полезно при проблемах с совместимостью или производительностью.

### 4. `netsh int tcp set global netdma=disabled`
- **Описание**: Отключает поддержку Network Direct Memory Access (NetDMA).
- **Рекомендация**: Отключение может помочь избежать проблем с совместимостью, но может снизить производительность в некоторых сценариях.

### 5. `netsh int tcp set global dca=enabled`
- **Описание**: Включает Data Center Bridging (DCA) для оптимизации обработки трафика в дата-центрах.
- **Рекомендация**: Рекомендуется включать в средах с поддержкой DCA.

### 6. `netsh int tcp set global rss=enabled`
- **Описание**: Включает Receive Side Scaling (RSS) для распределения входящего трафика между несколькими процессорами.
- **Рекомендация**: Включение RSS рекомендуется для многопроцессорных систем.

### 7. `netsh int tcp set global rsc=disabled`
- **Описание**: Отключает Receive Segment Coalescing (RSC).
- **Рекомендация**: Отключение может быть полезно при проблемах с производительностью или совместимостью.

### 8. `netsh int tcp set global ecncapability=default`
- **Описание**: Устанавливает возможность использования Explicit Congestion Notification (ECN).
- **Рекоменда### 8. `netsh int tcp set global ecncapability=default`
- **Описание**: Устанавливает возможность использования Explicit Congestion Notification (ECN), который позволяет сетям сигнализировать о перегрузках.
- **Рекомендация**: Оставьте значение по умолчанию, если не уверены в необходимости использования ECN.

### 9. `netsh int tcp set global timestamps=disabled`
- **Описание**: Отключает использование временных меток в TCP, которые могут использоваться для улучшения управления потоком и обнаружения потерь.
- **Рекомендация**: Отключение может помочь в некоторых случаях, но может снизить производительность в других.

### 10. `netsh int tcp set global initialRto=2000`
- **Описание**: Устанавливает начальное значение времени ожидания повторной передачи (RTO) в миллисекундах. Значение 2000 означает, что система будет ожидать 2 секунды перед повторной передачей потерянного пакета.
- **Рекомендация**: Настройка этого параметра может помочь в сетях с высокой задержкой, но может увеличить время восстановления в случае потерь.

## Настройка TCP CongestionProvider

Для настройки параметров CongestionProvider в зависимости от версии Windows используйте следующие команды:

### Windows 10

```bat
netsh int tcp set supplemental Template=Internet CongestionProvider=DCTCP
netsh int tcp set supplemental Template=Datacenter CongestionProvider=DCTCP
netsh int tcp set supplemental Template=Compat CongestionProvider=DCTCP
netsh int tcp set supplemental Template=DatacenterCustom CongestionProvider=DCTCP
netsh int tcp set supplemental Template=InternetCustom CongestionProvider=DCTCP
netsh int tcp set supplemental Template=Automatic CongestionProvider=DCTCP

Get-NetTCPSetting | Select SettingName, CongestionProvider
```

### Windows 11

```bat
netsh int tcp set supplemental Template=Internet CongestionProvider=bbr2
netsh int tcp set supplemental Template=Datacenter CongestionProvider=bbr2
netsh int tcp set supplemental Template=Compat CongestionProvider=bbr2
netsh int tcp set supplemental Template=DatacenterCustom CongestionProvider=bbr2
netsh int tcp set supplemental Template=InternetCustom CongestionProvider=bbr2
netsh int tcp set supplemental Template=Automatic CongestionProvider=bbr2

Get-NetTCPSetting | Select SettingName, CongestionProvider
```

Эти параметры могут быть полезны для настройки TCP в Windows в зависимости от специфики вашей сети и приложений. Рекомендуется тестировать изменения в контролируемой среде, чтобы определить, какие настройки обеспечивают наилучшие результаты для ваших нужд. 

Оптимизация сетевых протоколов и правильная настройка параметров TCP могут значительно улучшить производительность сетевых соединений. Используйте предложенные команды и рекомендации для достижения наилучших результатов в вашей среде.

### Библиотека групповых политик

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetCache]
"Enabled"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\LLTD]
"EnableRspndr"=dword:00000000
"AllowRspndrOnDomain"=dword:00000000
"AllowRspndrOnPublicNet"=dword:00000000
"ProhibitRspndrOnPrivateNet"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\LLTD]
"EnableRspndr"=dword:00000000
"AllowRspndrOnDomain"=dword:00000000
"AllowRspndrOnPublicNet"=dword:00000000
"ProhibitRspndrOnPrivateNet"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\LLTD]
"EnableLLTDIO"=dword:00000000
"AllowLLTDIOOnDomain"=dword:00000000
"AllowLLTDIOOnPublicNet"=dword:00000000
"ProhibitLLTDIOOnPrivateNet"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\HotspotAuthentication]
"Enabled"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\HotspotAuthentication]
"Enabled"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\System]
"EnableFontProviders"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\System]
"EnableFontProviders"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\PeerDist\Service]
"Enable"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Policies\Microsoft\PeerDist\Service]
"Enable"=dword:00000000

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\BITS]
"EnablePeercaching"=dword:00000000
```

Следуя приведенным рекомендациям и настройкам, вы сможете оптимизировать свою сетевую конфигурацию для достижения максимальной производительности и стабильности интернет-соединения. Регулярно проверяйте и обновляйте настройки, чтобы адаптироваться к изменениям в вашем оборудовании и программном обеспечении. Помните, что правильная настройка сетевых параметров может значительно улучшить ваш опыт в играх и других сетевых приложениях.

## 8. Выбор правильного маршрутизатора

Одним из ключевых элементов стабильного и быстрого интернет-соединения является правильный выбор маршрутизатора. Некачественный роутер может вызвать проблемы с сигналом Wi-Fi, низкую скорость интернета, перебои в соединении и другие неприятности.

### Лучшие роутеры

Ниже представлены модели маршрутизаторов от известных производителей, которые считаются одними из лучших на рынке.

### Keenetic

> **Keenetic Viva 1912**: Бюджетный маршрутизатор с хорошей скоростью и удобной прошивкой.  
> **Keenetic Sprinter**: Маршрутизатор среднего класса, подходящий для небольших квартир и домов.  
> **Keenetic Hopper**: Высокоскоростной маршрутизатор с поддержкой Wi-Fi 6.  
> **Keenetic Giga**: Маршрутизатор с гигабитными портами для высокоскоростного интернета.  
> **Keenetic Ultra KN-1811**: Высококлассный маршрутизатор с множеством возможностей и функций.  

### Asus

> **ASUS RT-AX1800U**: Маршрутизатор с поддержкой Wi-Fi 6.  
> **RT-AX86U**: Высокоскоростной маршрутизатор с широким набором функций.  
> **RT-AX86S**: Компактный маршрутизатор с Wi-Fi 6.  
> **RT-AC68U**: Популярный маршрутизатор с отличным соотношением цены и качества.  
> **RT-AC66U B1**: Маршрутизатор с поддержкой технологии MU-MIMO.  

### Ubiquiti

> **Edge Router X**: Высокопроизводительный маршрутизатор для бизнеса.  
> **ER4**: Маршрутизатор среднего класса с поддержкой VPN и других функций.  

### MikroTik

> **MikroTik hAP ac v3**: Маршрутизатор с поддержкой Wi-Fi ac.  
> **MikroTik hAP ax v2**: Маршрутизатор с поддержкой Wi-Fi 6.  

### TP Link

> **Archer C20**: Бюджетный маршрутизатор с хорошей скоростью и стабильностью.  
> **Archer C50**: Маршрутизатор с поддержкой двух диапазонов.  
> **Archer C5 AC1200**: Маршрутизатор с поддержкой Wi-Fi ac.  
> **Archer C6**: Маршрутизатор с широким набором функций.  
> **Archer A6**: Компактный маршрутизатор с поддержкой Wi-Fi ac.  

### Xiaomi

> **Xiaomi Mi Router 4A Gigabit Edition**: Бюджетный маршрутизатор с гигабитными портами.  
> **Xiaomi AX3200 / Redmi AX6S**: Маршрутизатор с поддержкой Wi-Fi 6.  
> **Xiaomi Redmi AX6000**: Высококлассный маршрутизатор с множеством функций и высокой скоростью.  

### Дополнительные ресурсы

# SpeedGuide.net

SpeedGuide.net — это ресурс, посвященный широкополосным интернет-соединениям, сетевой безопасности, беспроводным сетям и производительности систем. В этом гиде мы рассмотрим основные разделы сайта и полезные инструменты, которые помогут вам оптимизировать ваше интернет-соединение и улучшить сетевую безопасность.

## Основные разделы сайта

1. **Широкополосные соединения**
   - Информация о различных типах широкополосных соединений, таких как DSL и кабельные модемы.
   - Рекомендации по выбору провайдера и оборудованию.

2. **Сетевая безопасность**
   - Советы по защите вашей сети от угроз и уязвимостей.
   - Рекомендации по настройке маршрутизаторов и брандмауэров.

3. **Беспроводные сети**
   - Информация о настройке и оптимизации Wi-Fi сетей.
   - Советы по улучшению качества сигнала и скорости соединения.

4. **Производительность систем**
   - Рекомендации по улучшению производительности TCP/IP в сетях с высокой скоростью и задержками.

## Полезные инструменты

### 1. TCP Analyzer
- **Ссылка:** [TCP Analyzer](https://www.speedguide.net/analyzer.php)
- **Описание:** Этот инструмент позволяет анализировать параметры вашего TCP-соединения и выявлять возможные проблемы, которые могут влиять на скорость интернета.

### 2. TCP Optimizer
- **Ссылка:** [TCP Optimizer](https://www.speedguide.net/downloads.php)
- **Описание:** Программа для оптимизации настроек TCP/IP на вашем компьютере. Она помогает улучшить производительность интернет-соединения, изменяя параметры, такие как MTU, RWIN и другие.

### 3. Тест скорости
- **Ссылка:** [Тест скорости](https://www.speedguide.net/speedtest/)
- **Описание:** Инструмент для проверки скорости вашего интернет-соединения. Он измеряет скорость загрузки и выгрузки данных, а также задержку.

### 4. Сканирование безопасности
- **Ссылка:** [Сканирование безопасности](https://www.speedguide.net/scan.php)
- **Описание:** Этот инструмент позволяет проверить вашу сеть на наличие уязвимостей и потенциальных угроз.

### 5. IP Locator
- **Ссылка:** [IP Locator](https://www.speedguide.net/ip/)
- **Описание:** Инструмент для определения местоположения IP-адреса. Полезен для анализа сетевой активности и выявления подозрительных подключений.

### 6. Маршрутизаторы
- **Ссылка:** [Маршрутизаторы](https://www.speedguide.net/broadband-list.php)
- **Описание:** Список маршрутизаторов с информацией о их характеристиках и производительности. Помогает выбрать подходящее оборудование для вашей сети.

### 7. Порты TCP/IP
- **Ссылка:** [Порты TCP/IP](https://www.speedguide.net/ports.php)
- **Описание:** Справочник по портам TCP/IP, включая информацию о стандартных портах и их назначении.

## Заключение

SpeedGuide.net предлагает множество ресурсов и инструментов для оптимизации интернет-соединения и повышения сетевой безопасности. Используйте представленные инструменты для анализа и улучшения вашей сети, чтобы обеспечить стабильное и быстрое соединение.


## Заключение

Выбор правильного маршрутизатора — это важный шаг к обеспечению стабильного и быстрого интернет-соединения. Учитывая разнообразие моделей и технологий, представленных на рынке, важно тщательно оценить свои потребности и требования. Правильный маршрутизатор не только улучшит качество соединения, но и обеспечит надежность работы всех ваших устройств в сети.

Не забывайте о регулярном обновлении прошивки маршрутизатора и драйверов сетевых адаптеров, чтобы поддерживать оптимальную производительность и безопасность. Также учитывайте, что дополнительные функции, такие как поддержка Wi-Fi 6, MU-MIMO и VPN, могут значительно повысить эффективность работы вашей сети.

Следуя рекомендациям и советам, представленным в этом гайде, вы сможете выбрать идеальный маршрутизатор, который будет соответствовать вашим требованиям и обеспечит высокую производительность в любых сценариях использования, будь то работа, игры или потоковое видео. Помните, что инвестиции в качественное сетевое оборудование — это инвестиции в комфорт и продуктивность вашей работы и досуга.
