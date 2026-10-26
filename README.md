# dns-client-test OpenWrt package

OpenWrt packaging for [dns-client-test](https://github.com/karen07/dns-client-test), a
configurable UDP DNS load generator. It installs the testing utility on OpenWrt.

## Описание

Пакет OpenWrt для [dns-client-test](https://github.com/karen07/dns-client-test) -
настраиваемого генератора нагрузки UDP DNS. Устанавливает тестовую утилиту на OpenWrt.

Пакет устанавливает бинарный файл `dns-client-test` в `/usr/bin` и не объявляет дополнительных зависимостей времени выполнения OpenWrt.

При разработке Makefile может собирать исходники из соседнего каталога `../dns-client-test`. Если такого каталога нет, OpenWrt загружает версию исходников по тегу, заданному в `PKG_VERSION`.

## Структура проекта

- `dns-client-test/Makefile` - описание OpenWrt package;
- `openwrt-build.env` - параметры пакета для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов общего reusable workflow.

## Сборка

Сборка выполняется через GitHub Actions. Workflow этого репозитория вызывает общий reusable workflow из [openwrt-package-ci](https://github.com/karen07/openwrt-package-ci).

CI можно запустить:

- push тега вида `vX.Y.Z` - значение тега используется как версия OpenWrt;
- вручную через `workflow_dispatch`, указав версию OpenWrt и при необходимости фильтры target/subtarget.

Параметры этого пакета хранятся в `openwrt-build.env`. Общие `openwrt-build.sh`, `openwrt-matrix.py` и логика сборки через OpenWrt SDK находятся в `openwrt-package-ci`.

Для ручной сборки каталог `dns-client-test/` можно использовать как обычный package directory внутри OpenWrt buildroot/SDK.

## Связанные проекты

- [dns-client-test](https://github.com/karen07/dns-client-test) - основной проект и исходный код клиента.
