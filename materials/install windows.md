# Установите Windows

## 1. Разделы для хранения

Настройте систему [мультизагрузки](https://en.wikipedia.org/wiki/Multi-booting), чтобы создать отдельные окружения для работы и игр, при этом игровая среда должна оставаться свободной от лишнего программного обеспечения. Это поможет вам поддерживать чистоту игрового раздела, избавляя его от ненужных приложений, как упоминалось ранее. Таким образом, вы сможете избежать установки bloatware на том же разделе, где работают приложения в реальном времени, не теряя при этом удобства. Для этого уменьшите объем в Управлении дисками ([инструкции](https://docs.microsoft.com/en-us/windows-server/storage/disk-management/shrink-a-basic-volume)), чтобы освободить место для установки новой операционной системы.

## 2. Обсуждение версий и сборок Windows

- В старых версиях Windows отсутствует поддержка античитов, что связано с нехваткой обновлений безопасности для устаревших операционных систем. Также не поддерживаются драйверы, особенно для графических процессоров и сетевых карт, из-за чего некоторые пользователи вынуждены переходить на более новые версии. В таблице ниже указаны минимальные версии Windows, необходимые для установки драйверов для различных графических процессоров:

    |GPU|Минимальная версия Windows|
    |---|---|
    |NVIDIA 10 серия и ниже|Поддерживаются практически все версии Windows|
    |NVIDIA 16, 20 серия|Win7, Win8, Win10 1709 и выше|
    |NVIDIA 30 серия|Win7, Win10 1803 и выше|
    |NVIDIA 40 серия|Win10 1803 и выше|
    |AMD|Смотрите на странице поддержки драйверов|

- В Windows Server не поддерживаются многие сетевые карты, предназначенные для потребителей. Способы обхода, такие как [данный](https://github.com/loopback-kr/Intel-I219-V-for-Windows-Server), могут нарушать работу античитов из-за недействительных сертификатов.

- Драйверы NVIDIA DCH совместимы с Windows 10 версии 1803 и выше ([1](https://nvidia.custhelp.com/app/answers/detail/a_id/4777/~/nvidia-dch%2Fstandard-display-drivers-for-windows-10-faq)).

- При воспроизведении мультимедиа на Windows 10 версии 1709 служба [Multimedia Class Scheduler Service](https://learn.microsoft.com/en-us/windows/win32/procthread/multimedia-class-scheduler-service) увеличивает разрешение таймера до 0,5 мс, что ограничивает контроль над запрашиваемым разрешением.

- Для трассировки лучей на графических процессорах NVIDIA требуется Windows 10 версии 1809 и выше.

- Microsoft внедрила фиксированную частоту 10 МГц для QueryPerformanceFrequency в Windows 10 версии 1809 и выше.

- В Windows 10 версии 1903 и выше обновлен планировщик для процессоров Ryzen с несколькими CCX ([1](https://i.redd.it/y8nxtm08um331.png)).

- Для использования DirectStorage необходима Windows 10 версии 1909 и выше, однако игры на Windows 11 получают дополнительные преимущества благодаря новым оптимизациям стека хранения ([1](https://devblogs.microsoft.com/directx/directstorage-developer-preview-now-available)).

- Windows 10 версии 2004 и выше требуется для [Hardware Accelerated GPU Scheduling](https://devblogs.microsoft.com/directx/hardware-accelerated-gpu-scheduling), необходимого для генерации кадров DLSS ([1](https://developer.nvidia.com/rtx/streamline/get-started)).

- В Windows 10 версии 2004 и выше процессы, повышающие разрешение таймера, больше не влияют на глобальное разрешение таймера ([1](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timebeginperiod), [2](https://randomascii.wordpress.com/2020/10/04/windows-timer-resolution-the-great-rule-change)). Это означает, что разрешение устанавливается для каждого процесса отдельно, и процессы, которые не повышают разрешение, обслуживаются реже. В Windows 11 это поведение было улучшено: более высокое разрешение не гарантируется, если окно процесса свернуто или перекрыто ([1](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timebeginperiod)). Microsoft добавила возможность восстановления глобального поведения в Windows Server 2022 и Windows 11 с помощью изменения в реестре ([1](https://randomascii.wordpress.com/2020/10/04/windows-timer-resolution-the-great-rule-change)), что означает, что это не может быть восстановлено в Windows 10 версиях 2004 - 22H2.

- В Windows 11 и выше обновлен планировщик для процессоров Intel 12-го поколения и новее ([1](https://www.anandtech.com/show/16959/intel-innovation-alder-lake-november-4th/3)), однако такое поведение можно воспроизвести вручную с помощью политик сродства в любой версии Windows, как будет объяснено в следующих разделах.

- Windows 11 и выше ограничивает частоту опроса фоновых процессов ([1](https://blogs.windows.com/windowsdeveloper/2023/05/26/delivering-delightful-performance-for-more-than-one-billion-users-worldwide)).

- Windows 11 является минимальным требованием для [Cross Adapter Scan-Out](https://videocardz.com/newz/microsoft-cross-adapter-scan-out-caso-delivers-16-fps-increse-on-laptops-without-dgpu-igpu-mux-switch) ([1](https://devblogs.microsoft.com/directx/optimizing-hybrid-laptop-performance-with-cross-adapter-scan-out-caso)).

- Параметр AllowTelemetry можно установить на 0 в версиях Windows Server ([1](https://admx.help/?Category=Windows_10_2016&Policy=Microsoft.Policies.DataCollection::AllowTelemetry)).

- Начиная с версии Windows 10 2004, комплект драйверов Windows включает модуль расширения класса сетевого адаптера ([NetAdapterCx](https://learn.microsoft.com/ru-ru/windows-hardware/drivers/netcx)). С версии Windows 11 24h2 UMDF NetAdapterCx позволяет драйверам сетевых адаптеров работать в пользовательском режиме.

    - Это замена NDIS (драйвера интернет-адаптера) на драйвер с поддержкой NetAdapter Class Extension, который имеет преимущества по сравнению с предыдущими версиями ([1](https://learn.microsoft.com/ru-ru/windows-hardware/drivers/netcx/)).

- В версии 24h2 также были внесены следующие изменения:

    - Обновлен WDDM до версии 3.2 ([1](https://learn.microsoft.com/en-us/windows-hardware/drivers/what-s-new-in-driver-development#display-and-graphics-drivers)).
      
    - Связь потока ввода (функции GetRawInputData) с DPC от GPU-драйвера была устранена, что должно положительно сказаться на итоговых результатах.

    - В DWM теперь используется два потока ввода вместо трех, как это было в версии 23h2.

- Только для Windows Server:

  - Чтобы включить Wi-Fi, перейдите в ``Управление -> Добавить роли и компоненты`` на панели управления Server Manager и активируйте ``Службу беспроводной локальной сети``.
