Изменения обработки параметров в релизах > 2.3.0
------------------------------------------------

Система параметров отличается от того, что было ранее и достаточно сильно:

* изменения имён и стиля параметров

Все параметры теперь в виде --help (gnu-style), у некоторых есть шорткаты в виде -h (unix-style). 
Это касается всех систем, в том числе винды.

--daemon=1 и подобное -> просто --daemon, без параметра. Нет опции - false, есть - true
--notransit=1 -> --notransit, то же что и выше: есть опция - false, нет - true
--v6 -> --ipv6 (первое было похоже на версию какого-то своего протокола, типа socksproxy --v5)
--tunnelscfg -> --tunconf (имя параметра было слишком длинным, cfg переделан на conf - единообразно с --conf)
--sockskeys -> разделён на два, для socks и httpproxy по-отдельности

* поддержка секций в основном конфиге

Выглядит это так:

    # основные опции
    pidfile = /var/run/i2pd.pid
    #
    # настройки конкретного модуля
    [httproxy]
    address = 1.2.3.4
    port    = 4446
    keys    = httproxy-keys.dat
    # и так далее
    [sam]
    enabled = no
    addresss = 127.0.0.2
    # ^^ переопределяется только адрес, остальное берётся из дефолта

Точно так же сейчас работает конфиг туннелей: секция до точки - имя, после - параметр

* поддержка выключения отдельных сервисов "на корню" см sam.enabled и подобное

Это позволило задать дефолт для номера порта и не писать его руками для включения.

* добавлен --help (см #110)

* присутствует некая валидация параметров, --port=abcd - не прокатит, --port=100500 - тоже