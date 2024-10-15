# Фундаментальное руководство по настройке ПК

> [!CAUTION]
> Это руководство может быть полезно как начинающим твикерам, так и более опытным пользователям, которые хотят углубить свои знания и навыки в области настройки и оптимизации ПК.

## Обязательно к прочтению
> [!CAUTION]
> Вы не имеете права продавать или копировать бесплатный продукт. Такое поведение не будет терпеться. Пожалуйста, уважайте труд, работу и усилия, которые я вложил в это руководство. Если вы решите поделиться чужим контентом, пожалуйста, укажите мое авторство. Сообщайте нам о пользователях, которые пытаются нажиться на чужом труде. Также запрещено использовать скрипты, файлы и настройки реестра, взятые непосредственно из этой операционной системы, с целью получения прибыли.

## Предисловие

Это руководство предназначено для оптимизации новейших систем Windows 10/11. Я собирал информацию о настройке системы в течение нескольких месяцев, потому что для многих людей даже самая очевидная информация скрыта, и не забывайте, что многие люди все еще верят в советы плацебо. Прочитав это руководство, вы сможете настроить систему под свои нужды.

## Требования
Установлена последняя сборка Windows 10 или 11. Внимательное чтение означает, что в операционной системе установлена ее самая обновленная версия, способная обеспечить более стабильную и безопасную работу компьютера, а также поддержку новых функций и улучшений. Это также означает, что система работает на сборке 2004, которая является промежуточной версией обновления, содержащей исправления ошибок, улучшения производительности и новые функции, изначально выпущенные для Windows 10. Чтение и понимание информации об установленной версии операционной системы важно для обеспечения правильной работы компьютера и учета необходимости дополнительных обновлений или обслуживания.

## О пунктах и о том, почему нужно делать все по порядку
- Соблюдение правильного порядка выполнения советов из руководства по настройке ПК поможет вам избежать проблем и настроить компьютер максимально эффективно.

## Пункты по порядку

Строго следуйте шагам в этой последовательности, чтобы избежать проблем с настройками:

- **[Установка системы Windows](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/materials/install%20windows.md)** - Первоначальная установка операционной системы, которая является основой для всех последующих настроек.

- **[Настройка системы (OS)](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/materials/system%20tweaking.md)** - Оптимизация параметров операционной системы для повышения производительности и стабильности.

- **[Конфигурация сети](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/materials/network.md)** - Настройка сетевых параметров для обеспечения надежного и быстрого интернет-соединения.

- **[Настройка видеокарты NVIDIA](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/materials/configure-nvidia.md)** - Конфигурация параметров видеокарты NVIDIA для достижения максимальной производительности в играх и приложениях.

- **[Настройка видеокарты AMD](https://github.com/couwthynokap/Fundamental-Guide-to-Tweaking-a-PC/blob/main/materials/configure-amd.md)** - Оптимизация настроек видеокарты AMD для улучшения графической производительности и качества изображения.

## Бенчмаркинг
После завершения настройки системы по данному гайду, рекомендуется провести бенчмаркинг для оценки производительности. Вот несколько программ, которые могут помочь вам в этом:

- **[FrameView](https://www.nvidia.com/en-gb/geforce/technologies/frameview)** - Слишком нагруженное приложение. Если хотите - используйте. Я не советую использовать её.

- **[PresentMon](https://github.com/GameTechDev/PresentMon)** - Большое количество метрики и хорошие показатели. Для визуализации используйте **[Frame Time Analysis](https://boringboredom.github.io/Frame-Time-Analysis/)**. Полный список параметров запуска для PresentMon **[здесь](https://github.com/GameTechDev/PresentMon/blob/main/README-CaptureApplication.md#metric-definitions)**.

- **[Windows Performance Toolkit](https://learn.microsoft.com/en-us/windows-hardware/test/wpt)** - Расширенный анализ прерываний для Windows. Измерьте время выполнения ISR/DPC с помощью **[xperf](/files/xperf-test-script.bat)**.

- **[Mouse Tester](https://github.com/valleyofdoom/MouseTester)** - Проверьте интервал опроса, частоту работы мыши, узнайте о стабильности чувствительности.

- **[NVIDIA Reflex Analyzer](https://www.nvidia.com/en-gb/geforce/news/reflex-latency-analyzer-360hz-g-sync-monitors)** - Полезная утилита для игр с Reflex, позволяющая измерять задержку и оптимизировать игровой процесс.

- **[RTSS](https://www.guru3d.com/download/rtss-rivatuner-statistics-server-download/)** - В новой версии добавлены полезные метрики. Ищите на guru3d или других проверенных источниках бета-версию [здесь](https://www.youtube.com/watch?v=7DtEJlx-UQI).

## Гайд основан на исследованиях данных энтузиастов

Отдельное спасибо энтузиастам, которые свободно делятся своими исследованиями, навыками программирования, настройками и туториалами, предоставляют тесты и техническую информацию: [Amit](https://twitter.com/amitxv), [Bored](https://twitter.com/Bra1nlet), [Calypto](https://twitter.com/CaIypto), [CatGamerOP](https://twitter.com/CatGamerOP), [Chris Titus Tech](https://twitter.com/christitustech), [Melody](https://sites.google.com/view/melodystweaks/), [Imribiy](https://twitter.com/imribiy), [Phlegm](https://twitter.com/getggos), [TenForums](https://www.tenforums.com/), [Timecard](https://github.com/djdallmann/GamingPCSetup), [IIIЕX0III](https://discord.gg/qEWGUAGXCq), [Seniroad](https://github.com/Seniroad/Computer-RU-Setup-guide/tree/main), [div5064](https://shorturl.at/VXwBJ), [EXO](https://shorturl.at/VXwBJ), [BEYOND PERFORMANCE](https://discord.gg/xk3HKVPyef) и другие.
