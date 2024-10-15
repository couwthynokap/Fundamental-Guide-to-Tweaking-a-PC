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

### Рекомендации для сетевых адаптеров Realtek

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
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*EEE" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*FlowControl" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*IPChecksumOffloadIPv4" -RegistryValue "3" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*InterruptModeration" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*LsoV2IPv4" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*LsoV2IPv6" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*NumRssQueues" -RegistryValue "2" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PMARPOffload" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PMNSOffload" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PriorityVLANTag" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*RSS" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*WakeOnMagicPacket" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*WakeOnPattern" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*ReceiveBuffers" -RegistryValue "2048" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TransmitBuffers" -RegistryValue "2048" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TCPChecksumOffloadIPv4" -RegistryValue "3" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TCPChecksumOffloadIPv6" -RegistryValue "3" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*UDPChecksumOffloadIPv4" -RegistryValue "3" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*UDPChecksumOffloadIPv6" -RegistryValue "3" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "DMACoalescing" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "EEELinkAdvertisement" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "ITR" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "ReduceSpeedOnPowerDown" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WaitAutoNegComplete" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WakeOnLink" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "AdvancedEEE" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "EnableGreenEthernet" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "GigaLite" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "PowerSavingMode" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "S5WakeOnLan" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WolShutdownLinkSpeed" -RegistryValue "2" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "LogLinkStateEvent" -RegistryValue "16" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WakeOnMagicPacketFromS5" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Ultra Low Power Mode" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "System Idle Power Saver" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Selective Suspend" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Selective Suspend Idle Timeout" -DisplayValue "60" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Link Speed Battery Saver" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*SelectiveSuspend" -RegistryValue "0" >nul 2>&1 
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnablePME" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "TxIntDelay" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "TxDelay" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnableModernStandby" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*ModernStandbyWoLMagicPacket" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnableLLI" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*SSIdleTimeout" -RegistryValue "60" >nul 2>&1
cls
pause
endlocal
exit /b 0
```

### Настройки для рекомендаций Intel

Для оптимизации работы сетевого адаптера Intel выполните следующий скрипт в командной строке с правами администратора:

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
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*EEE" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*FlowControl" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*IPChecksumOffloadIPv4" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*InterruptModeration" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*LsoV2IPv4" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*LsoV2IPv6" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*NumRssQueues" -RegistryValue "2" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PMARPOffload" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PMNSOffload" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*PriorityVLANTag" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*RSS" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*WakeOnMagicPacket" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*WakeOnPattern" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*ReceiveBuffers" -RegistryValue "2048" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TransmitBuffers" -RegistryValue "2048" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TCPChecksumOffloadIPv4" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*TCPChecksumOffloadIPv6" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*UDPChecksumOffloadIPv4" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "*UDPChecksumOffloadIPv6" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "DMACoalescing" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "EEELinkAdvertisement" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "ITR" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "ReduceSpeedOnPowerDown" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WaitAutoNegComplete" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WakeOnLink" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "AdvancedEEE" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "EnableGreenEthernet" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "GigaLite" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "PowerSavingMode" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "S5WakeOnLan" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WolShutdownLinkSpeed" -RegistryValue "2" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "LogLinkStateEvent" -RegistryValue "16" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -RegistryKeyword "WakeOnMagicPacketFromS5" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Ultra Low Power Mode" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "System Idle Power Saver" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Selective Suspend" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Selective Suspend Idle Timeout" -DisplayValue "60" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -Name "*" -DisplayName "Link Speed Battery Saver" -DisplayValue "Disabled" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*SelectiveSuspend" -RegistryValue "0" >nul 2>&1 
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnablePME" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "TxIntDelay" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "TxDelay" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnableModernStandby" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*ModernStandbyWoLMagicPacket" -RegistryValue "0" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "EnableLLI" -RegistryValue "1" >nul 2>&1
powershell Set-NetAdapterAdvancedProperty -AllProperties -Name "*" -RegistryKeyword "*SSIdleTimeout" -RegistryValue "60" >nul 2>&1
cls
pause
endlocal
exit /b 0
```

- **Эти рекомендации направлены на оптимизацию производительности сети и снижение задержек. За более подробной информацией и пояснениями обращайтесь к руководствам Intel и Microsoft по настройке производительности сетевой подсистемы, доступным в разделе «Технические ссылки».**

## 7. Дополнительные рекомендации по настройке

- Убедитесь, что все изменения в реестре и параметры сетевого адаптера применяются корректно. Это поможет избежать проблем с подключением и производительностью сети.

- Если у вас возникли трудности с выполнением скрипта, проверьте наличие прав администратора и правильность написания команд.

- Рекомендуется периодически проверять обновления драйверов и системных компонентов, чтобы поддерживать оптимальную производительность системы.

- Для получения дополнительной информации о настройках сетевой подсистемы и их влиянии на производительность, ознакомьтесь с официальной документацией от Intel и Microsoft.

### Конфигурация для конкретной операционной системы

- Убедитесь, что функция Network Throttling Index включена. Рекомендации: установите значение между 10 и 20 знаками после запятой, например, от 15 Мбит/с до 30 Мбит/с.
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\NetworkThrottlingIndex
```

### Сетевые протоколы

Netsh (Network Shell) — это мощная утилита командной строки в Windows, которая позволяет вам управлять сетевыми настройками. Она может быть вашим верным союзником в борьбе за стабильный интернет и плавный геймплей, особенно в играх, использующих TCP-протокол.

### Как Netsh может улучшить геймплей в TCP играх

- **Снижение лагов**: Правильно настроенные параметры TCP могут значительно снизить лаги в играх, которые используют этот протокол для передачи данных.

- **Улучшение стабильности**: Оптимизация сетевых настроек может повысить стабильность интернет-соединения и снизить риск разрывов соединения во время игры.

```bash
:: Просмотр доступных глобальных протоколов netsh.
netsh interface tcp show global

:: Просмотр параметров TCP эвристики.
netsh interface tcp show heuristics

:: Вывод статистики TCP для интерфейсов с поддержкой объединения полученных сегментов.
netsh interface tcp show rscstats

:: Просмотр настроек безопасности TCP.
netsh interface tcp show security

:: Вывод параметров TCP на основе дополнительного шаблона.
netsh interface tcp show supplemental
```

### Настройки для оптимизации

```bash
:: Установите максимальное количество попыток восстановления соединения с использованием SYN-пакетов.
netsh int tcp set global maxsynretransmissions=2

:: Включите динамическое буферизование отправки для TCP-протоколов.
netsh winsock set autotuning on

:: Отключите функцию регулировки поведения TCP для управления потоком данных.
netsh interface tcp set global hystart=disabled

:: Разрешите отправку и получение данных в начальных SYN-пакетах во время установления TCP-соединения.
netsh interface tcp set global fastopen=enabled

:: Отключите алгоритм управления потоком TCP (Proportional Rate Reduction).
netsh int tcp set global prr=disabled

:: Отключите приостановку передачи данных в TCP-соединениях.
netsh int tcp set global pacingprofile=off

:: Отключите постоянство RTT для клиентов, не использующих SACK.
netsh int tcp set global nonsackrttresiliency=disabled

:: Установите максимальное количество записей в кэше соседей для всех интерфейсов.
netsh int ip set global neighborcachelimit=4096

:: Установите максимальный размер кэша маршрутизации IPv4.
netsh int ip set global routecachelimit=4096

:: Отключите начальную маршрутизацию IP.
netsh int ip set global sourceroutingbehavior=drop

:: Включите загрузку контрольной суммы для снижения нагрузки на ЦП.
netsh int ip set global taskoffload=enabled

:: Отключите сенсор медиа для определения состояния DHCP.
netsh int ip set global dhcpmediasense=disabled

:: Отключите ведение журнала событий подключения/отключения кабеля.
netsh int ip set global mediasenseeventlog=disabled

:: Отключите многопоточную рассылку IGMP.
netsh int ip set global mldlevel=none

:: Увеличьте окно приема и объем передаваемых данных.
netsh int tcp set supplemental Internet congestionprovider=ctcp

:: Установите поддержку Advanced Direct Memory Access (NetDMA).
netsh int tcp set global netdma=disabled

:: Отключите Teredo и ISATAP для IPv6.
netsh int teredo set state disabled
netsh int isatap set state disabled
```

### Библиотека групповых политик

```plaintext
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

- [Speedguide](https://www.speedguide.net/broadband-list.php) - сайт рейтинга маршрутизаторов.

### Рекомендации

Правильный выбор маршрутизатора может значительно улучшить качество вашего интернет-соединения. Помните, что лучший маршрутизатор - это тот, который отвечает вашим конкретным потребностям.

> **Определите свои потребности**: Какой тип подключения вам нужен (Wi-Fi, Ethernet), какой объем трафика вы планируете использовать, какие функции вам нужны (VPN, MU-MIMO, Wi-Fi 6)?  
> **Почитайте отзывы**: Прочитайте отзывы о выбранных моделях маршрутизаторов на различных ресурсах.  
> **Сравните цены**: Сравните цены на разных сайтах и в магазинах.  

## Заключение

Выбор правильного маршрутизатора — это важный шаг к обеспечению стабильного и быстрого интернет-соединения. Учитывая разнообразие моделей и технологий, представленных на рынке, важно тщательно оценить свои потребности и требования. Правильный маршрутизатор не только улучшит качество соединения, но и обеспечит надежность работы всех ваших устройств в сети.

Не забывайте о регулярном обновлении прошивки маршрутизатора и драйверов сетевых адаптеров, чтобы поддерживать оптимальную производительность и безопасность. Также учитывайте, что дополнительные функции, такие как поддержка Wi-Fi 6, MU-MIMO и VPN, могут значительно повысить эффективность работы вашей сети.

Следуя рекомендациям и советам, представленным в этом гайде, вы сможете выбрать идеальный маршрутизатор, который будет соответствовать вашим требованиям и обеспечит высокую производительность в любых сценариях использования, будь то работа, игры или потоковое видео. Помните, что инвестиции в качественное сетевое оборудование — это инвестиции в комфорт и продуктивность вашей работы и досуга.
