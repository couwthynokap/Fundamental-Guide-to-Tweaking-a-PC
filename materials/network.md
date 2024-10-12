# Конфигурация сети

## Предисловие

Перед выполнением любых действий убедитесь, что установлен драйвер сетевой карты.

## Кабельные соединения:

К наиболее распространенным типам кабелей относятся UTP, FTP, STP, S/FTP, S/STP, а также стандарты cat5, cat5e, cat6, cat6a, cat7 и cat8. Идеальным и самым дорогим вариантом является использование экранированного кабеля cat8 (STP) длиной не более 50 см. В случае ограниченного бюджета (и низкой скорости интернета) рекомендуется обратить внимание на экранированные кабели cat5e или cat6 (STP или S/STP). Это обеспечит более стабильное соединение с сетью и изображение № 1

## Важные факты (о которых мало кто знает):

Производство всех сетевых адаптеров в Китае стоит около 5 долларов. Смена провайдера трафика с циклического на более чувствительный к задержкам может привести к увеличению скорости соединения до ±500 раз. Многие провайдеры используют агрегацию пакетов, что позволяет увеличить скорость загрузки за счет объединения нескольких пакетов в один. Некоторые сетевые карты, например Solarflare, имеют время задержки.

## Выберите сетевой адаптер:

Если у вас установлен адаптер Realtek, вы можете столкнуться с проблемами, в то время как адаптеры Intel обычно обеспечивают надежную работу. Предпочтительным вариантом является использование встроенных сетевых адаптеров Intel или внешних адаптеров той же марки. Не забывайте периодически обновлять драйверы для сетевого адаптера (LAN/WI-FI), загружая их с официального сайта производителя материнской платы.

## Немного теории:

- Скорость Интернета определяется как количество битов информации, передаваемых в секунду, измеряется в килобитах в секунду (Кбит/с), мегабитах в секунду (Мбит/с) или гигабитах в секунду (Гбит/с). Можно выполнить [Тест скорости Интернета] (http://www.dslreports.com/speedtest).

- Потеря пакетов происходит, когда один или несколько пакетов не достигают адреса назначения во время передачи данных. Вы можете выполнить [тест потери пакетов](https://packetlosstest.com).

- Чрезмерная буферизация сети может привести к увеличению задержки и джиттера, а также к снижению пропускной способности. Можно выполнить тест на чрезмерную [сетевую буферизацию](https://www.waveform.com/tools/bufferbloat).

## Настройки сетевого адаптера

Функции разгрузки в сетевых картах делегируют определенные функции обработки пакетов, снижая потребление процессора. В идеале это позволяет выделить больше процессорного времени для других задач и игр.

## Настройки для рекомендаций Realtek:

```
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

## Настройки для рекомендаций Intel:

```
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

- **Эти рекомендации направлены на оптимизацию производительности сети и снижение задержек. За более подробной информацией и пояснениями обращайтесь к руководствам Intel и Microsoft по настройке производительности сетевой подсистемы, доступным в разделе «Технические ссылки »**.

## Конфигурация для конкретной операционной системы

- Убедитесь, что функция Network Throttling Index включена. Рекомендации: Установите значение между 10 и 20 знаками после запятой, например, от 15 Мбит/с до 30 Мбит/с.
``HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\NetworkThrottlingIndex``.

## Сетевые протоколы

Netsh (Network Shell) - это мощная утилита командной строки в Windows, которая позволяет вам управлять сетевыми настройками. 
Она может быть вашим верным союзником в борьбе за стабильный интернет и плавный геймплей, особенно в играх, использующих TCP-протокол.

## Как Netsh может улучшить геймплей в TCP играх:

- Снижение лагов: Правильно настроенные параметры TCP могут значительно снизить лаги в играх, которые используют этот протокол для передачи данных. 
- Улучшение стабильности: Оптимизация сетевых настроек может повысить стабильность интернет-соединения и снизить риск разрывов соединения во время игры.

 ```
:: View the globally available netsh protocols.
:: netsh interface tcp show global - Displays global TCP parameters.
:: netsh interface tcp show heuristics - Displays the parameters of TCP heuristics.
:: netsh interface tcp show rscstats - Output TCP statistics for interfaces with support for merging received segments.
:: netsh interface tcp show security - Displays the TCP security settings.
:: netsh interface tcp show supplemental - Output TCP parameters based on the optional template.

:: @echo off & chcp 65001
:: for %%i in (global heuristics rscstats security supplemental) do (
::     echo. >> "%userprofile%\Desktop\NETSH Backup.txt"
::     echo === netsh interface tcp show %%i === >> "%userprofile%\Desktop\NETSH Backup.txt"
::     netsh interface tcp show %%i >> "%userprofile%\Desktop\NETSH Backup.txt"
:: )

:: Sets the number of attempts to re-establish the connection using SYN packets.
:: Windows 8.1 and Windows Server 2012 R2 only.
:: netsh int tcp set global maxsynretransmissions=2

:: Enable dynamic send buffering for TCP protocols.
netsh winsock set autotuning on

:: Disable the TCP behavior adjustment feature for data flow control.
netsh interface tcp set global hystart=disabled

:: Allows data to be sent and received in initial SYN packets during TCP communication establishment.
netsh interface tcp set global fastopen=enabled

:: Disable (Proportional Rate Reduction) TCP flow control algorithm, which is used to control the rate of data transmission on the network.
netsh int tcp set global prr=disabled

:: Disable data transfer pausing in TCP connections
netsh int tcp set global pacingprofile=off

:: Disables RTT persistence for clients not using SACK
:: It is recommended to enable for connections with unstable ping and in the presence of packet loss.
:: netsh int tcp set global nonsackrttresiliency=disabled

:: Set the max. number of entries in the neighbor cache for all interfaces.
netsh int ip set global neighborcachelimit=4096

:: Set the max. IPv4 routing cache size
netsh int ip set global routecachelimit=4096

:: Disable initial IP routing. Discards packets routed by the source.
netsh int ip set global sourceroutingbehavior=drop

:: Checksum Download. Allows you to reduce the load on the CPU by shifting some of the tasks required to maintain the TCP/IP stack to the network card.
:: Enabled for RSS to work properly.
netsh int ip set global taskoffload=enabled

:: Disable the media sensor to determine the state of the DHCP environment.
netsh int ip set global dhcpmediasense=disabled

:: Disable logging of cable (non)connection event logging.
netsh int ip set global mediasenseeventlog=disabled

:: Disable (IGMP) multicore mailing (violates OBS NDI)
netsh int ip set global mldlevel=none

:: Increases the receiving window and the amount of data sent. This increases throughput on higher latency / broadband internet connections.
netsh int tcp set supplemental Internet congestionprovider=ctcp

:: Default setting in Windows 10 Creators update, default in Linux kernels 2.6 through 3.2. Uses the cubic growth function of the TCP congestion window. The algorithm uses the time elapsed since the last congestion event (instead of the acknowledgment time) to grow the TCP congestion window. It is designed for high-speed TCP transmission.
:: Can lead to bufferbloat in large BDP networks (e.g., Internet) with unmanaged queues such as ADSL and LTE.
:: netsh int tcp set supplemental Internet congestionprovider=CUBIC

:: Direct Cache Access (DCA) allows a capable I/O device, such as a network controller, to deliver data directly to the CPU cache. The goal of DCA is to reduce memory latency and memory bandwidth requirements in high bandwidth (gigabit) environments. DCA requires support from the I/O device, the system chipset, and the CPU.
netsh int tcp set global dca=enabled

:: Provides support for advanced direct memory access. In essence, it provides the ability to move network data more efficiently by minimizing CPU usage. NetDMA relieves the CPU from handling memory transfers between NIC data buffers and application buffers using the DMA mechanism.
:: According to Microsoft, NetDMA is not supported in Windows 8/8.1 and changing this setting will have no effect.
:: NetDMA (TCPA) does not work with Chimney Offload either, you have to choose one or the other. For NetDMA to work, it must be enabled/supported by your BIOS and your processor must support Intel I/O Acceleration Technology (I/OAT)
netsh int tcp set global netdma=disabled

:: Teredo is an IPv6 transition technology that provides address assignment and automatic tunneling between nodes for IPv6 unicast traffic when IPv6/IPv4 nodes are located behind one or more IPv4 Network Address Translators (NATs). IPv6 packets are sent as UDP messages to bypass IPv4 networks.
:: ISATAP (In-Site Automatic Tunnel Addressing Protocol) is an IPv6 transition mechanism designed to transmit IPv6 packets between dual-stack nodes over an IPv4 network.
netsh int isatap set state disable
netsh int teredo set state disable

netsh interface teredo set state disabled
netsh interface isatap set state disabled

netsh int ipv6 isatap set state disabled
netsh int ipv6 6to4 set state disabled

netsh interface IPV6 set global randomizeidentifier=disabled
netsh interface IPV6 set privacy state=disabled

:: Set the max "lifetime" of the base entry. Determines how long the interface will consider other nodes available after the last successful packet exchange with them.
:: Specifies the value of the number of consecutive messages sent while the network driver performs repeat address detection.
:: Disable the use of third-party protocols or interface state-dependent features.
:: Disable router discovery for a network interface.
:: Set the persistent storage type of settings for the network interface.
for /f "tokens=1" %%i in ('netsh int ip show interfaces ^| findstr [0-9]') do set INTERFACE=%%i
netsh int ip set interface %INTERFACE% basereachable=3600000 dadtransmits=0 otherstateful=disabled routerdiscovery=disabled store=persistent

:: The scaling setting on the receive side provides parallel processing of received packets on multiple processors while avoiding packet reordering . It avoids packet reordering by dividing packets into "streams" and using a single processor to process all packets for a given stream. Packets are divided into streams by computing a hash value based on specific fields in each packet , and the resulting hash values are used to select a processor to process the stream. This approach ensures that all packets belonging to a given TCP connection are queued to the same processor in the same order in which they are received by the network adapter.
:: For RSS to work properly, taskoffload must be enabled.
netsh int tcp set global rss=enabled

:: Receive Segment Combining (RSC) allows the NIC to combine multiple TCP/IP packets received during the same interrupt cycle into a single larger packet (up to 64KB) so that the network stack has fewer headers to process, resulting in an increase of 10% to 30% reduction in I/O overhead depending on the workload, thereby improving performance. Receive segment aggregation (RCS) allows packets received during the same interrupt cycle to be collected and aggregated so that they can be delivered to the network stack more efficiently. This can significantly increase the amount of traffic that can be processed without severely impacting the CPU.
:: Only supported by some network adapters. For games where latency is more important than net throughput, any type of memory packet aggregation should be disabled. Memory packet merging reduces CPU utilization and increases throughput, but causes the network adapter to merge packets before communicating with other hardware, which negatively affects input latency.
netsh int tcp set global rsc=disabled

:: The retransmission timeout (RTO) determines how many milliseconds of unconfirmed data are required before the connection is terminated. The default timeout for the initial RTO of 3 seconds can usually be reduced for today's low latency broadband connections unless you are in a remote location, connected to satellite internet or experiencing high latency. In high latency situations, this may increase the number of retransmissions if the RTO is reached on a regular basis.
netsh int tcp set global initialRto=2000

:: Windows 8 (like Windows 7) has the ability to automatically change its own TCP window autotuning behavior to a more conservative state regardless of any user settings. If heuristics limit the autotuning level, you may see this message when viewing netsh settings:
:: "** The above auto-tuning level setting is the result of Windows scaling heuristics overriding any local or policy configuration in at least one profile."
:: When the heuristic limits the autotuning level, the command "netsh int tcp show global" will still (incorrectly) show the user-defined autotuning level. You will have to use "netsh int tcp show heuristics" to see the actual current heuristics limit. To ensure the user-defined autotuning level of the TCP receive window and prevent heuristics from limiting the growth of the TCP receive window, disable heuristics. It is best to disable this feature before applying the autotuning level to ensure that the autotuning level set by the user is maintained.
netsh int tcp set heuristics disabled
netsh interface tcp set heuristics disabled

:: Disable TCP window scaling after the second retransmission of a SYN packet
netsh interface tcp set heuristics forcews=disabled
netsh int tcp set heuristics wsh=disabled

:: The Memory Overload Protection feature consists of three security settings. These include memory overload protection (MPP), profiles, and port exclusion.
netsh int tcp set security mpp=disabled
netsh int tcp set security profiles=disabled

:: This is a mechanism that provides routers with an alternative method of reporting network congestion. The goal is to reduce the number of retransmissions. Essentially, ECN assumes that the cause of any packet loss is router congestion . This allows routers experiencing congestion to mark packets and allows clients to automatically reduce the transmission rate to prevent further packet loss . Traditionally, TCP/IP networks signal congestion by dropping packets. 
:: When ECN is successfully negotiated, an ECN-enabled router can set a bit in the IP header (in the DiffServ field) instead of dropping the packet to signal congestion. The receiver sends a congestion message to the sender, which should react as if a packet drop has been detected. ECN is disabled by default in modern Windows implementations of TCP/IP, as it is possible that this may cause problems with some legacy routers that drop packets with the ECN bit set rather than ignoring this bit.
:: Enable only for short-term interactive connections and HTTP requests to routers that support it if there is congestion/packet loss, "off" otherwise (for pure bulk bandwidth with a large TCP window, no regular congestion/packet loss or legacy routers without ECN support). loss or legacy routers without ECN support). Might be worth trying "on" for games with unstable connections.
:: netsh int tcp set global ecncapability=enabled
netsh int tcp set global ecncapability=disabled

:: This is a TCP window scaling designed to improve transmission reliability by retransmitting segments that are not acknowledged within a certain retransmission timeout (RTO) interval. The problem with timestamps is that they add 12 bytes to the 20-byte TCP header of each packet, so their inclusion results in significant overhead.
netsh int tcp set global timestamps=disabled

:: Determines whether the path cache is updated in response to ICMP redirect packets.
netsh int ip set global icmpredirects=disabled

:: Set the max. dynamic port range for basic network protocols
netsh int ipv4 set dynamicport tcp start=1025 num=64511
netsh int ipv4 set dynamicport udp start=1025 num=64511

:: Indicates whether the window should be forcibly scaled for retransmission.
powershell Set-NetTCPSetting -SettingName "*" -ForceWS Disabled
 ```

## Библиотека групповых политик

 ```
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

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\LLTD]
"EnableLLTDIO"=dword:00000000
"AllowLLTDIOOnDomain"=dword:00000000
"AllowLLTDIOOnPublicNet"=dword:00000000
"ProhibitLLTDIOOnPrivateNet"=dword:00000000

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

# Выбор правильного маршрутизатора

Одним из ключевых элементов стабильного и быстрого интернет-соединения является правильный выбор маршрутизатора. Некачественный роутер может вызвать проблемы с сигналом Wi-Fi, низкую скорость интернета, перебои в соединении и другие неприятности.

## Лучшие роутеры:

Ниже представлены модели маршрутизаторов от известных производителей, которые считаются одними из лучших на рынке. 

## Keenetic:

> Keenetic Viva 1912: Бюджетный маршрутизатор с хорошей скоростью и удобной прошивкой.
> Keenetic Sprinter: Маршрутизатор среднего класса, подходящий для небольших квартир и домов.
> Keenetic Hopper: высокоскоростной маршрутизатор с поддержкой Wi-Fi 6.
> Keenetic Giga: маршрутизатор с гигабитными портами для высокоскоростного интернета.
> Keenetic Ultra KN-1811: Высококлассный маршрутизатор с множеством возможностей и функций.

## Asus:

> ASUS RT-AX1800U: Маршрутизатор с поддержкой Wi-Fi 6.
> RT-AX86U: высокоскоростной маршрутизатор с широким набором функций.
> RT-AX86S: Компактный маршрутизатор с Wi-Fi 6.
> RT-AC68U: Популярный маршрутизатор с отличным соотношением цены и качества.
> RT-AC66U B1: Маршрутизатор с поддержкой технологии MU-MIMO.

## Ubiquiti:

> Edge Router X: высокопроизводительный маршрутизатор для бизнеса.
> ER4: маршрутизатор среднего класса с поддержкой VPN и других функций.

## MikroTik:

> MikroTik hAP ac v3: Маршрутизатор с поддержкой Wi-Fi ac.
> MikroTik hAP ax v2: Маршрутизатор с поддержкой Wi-Fi 6.

## TP Link:

> Archer C20: Бюджетный маршрутизатор с хорошей скоростью и стабильностью.
> Archer C50: Маршрутизатор с поддержкой двух диапазонов.
> Archer C5 AC1200: Маршрутизатор с поддержкой Wi-Fi ac.
> Archer C6: Маршрутизатор с широким набором функций.
> Archer A6: компактный маршрутизатор с поддержкой Wi-Fi ac.

## Xiaomi:

> Xiaomi Mi Router 4A Gigabit Edition: Бюджетный маршрутизатор с гигабитными портами.
> Xiaomi AX3200 / Redmi AX6S: Маршрутизатор с поддержкой Wi-Fi 6.
> Xiaomi Redmi AX6000: Высококлассный маршрутизатор с множеством функций и высокой скоростью.

## Дополнительные ресурсы:

- [Speedguide](https://www.speedguide.net/broadband-list.php) - сайт рейтинга маршрутизаторов. 

Рекомендации:

- Правильный выбор маршрутизатора может значительно улучшить качество вашего интернет-соединения. Помните, что лучший маршрутизатор - это тот, который отвечает вашим конкретным потребностям.

> Определите свои потребности: Какой тип подключения вам нужен (Wi-Fi, Ethernet), какой объем трафика вы планируете использовать, какие функции вам нужны (VPN, MU-MIMO, Wi-Fi 6)?
> Почитайте отзывы: Прочитайте отзывы о выбранных моделях маршрутизаторов на различных ресурсах.
> Сравните цены: Сравните цены на разных сайтах и в магазинах.

### Советы

Оптимизируйте производительность системы, используя лучшие из доступных компонентов CPU, RAM и GPU. Выполните качественный разгон этих компонентов, учитывая скорость работы CPU и RAM, а также тайминги оперативной памяти и размер кэша CPU. Эти параметры напрямую влияют на задержку системы, что может сказаться на производительности hit-reg в игровых сценариях.

If possible, consider removing the router from the network chain. Connect the network cable directly, bypassing the router. This may result in a slight decrease in ping by 1-3 milliseconds.
