# DNS Client Test OpenWrt Package

OpenWrt packaging for [dns-client-test](https://github.com/karen07/dns-client-test), a
configurable UDP DNS load generator. It installs the testing utility on OpenWrt.

Пакет OpenWrt для [dns-client-test](https://github.com/karen07/dns-client-test) -
настраиваемого генератора нагрузки UDP DNS. Устанавливает тестовую утилиту на OpenWrt.

## Описание

Пакет устанавливает бинарный файл `dns-client-test` в `/usr/bin` и не объявляет дополнительных зависимостей времени выполнения OpenWrt.

При разработке Makefile может собирать исходники из соседнего каталога `../dns-client-test`. Если такого каталога нет, OpenWrt загружает версию исходников по тегу, заданному в `PKG_VERSION`.

## Разработка и проверка изменений

**Основные точки изменения:**

- `dns-client-test/Makefile` - зависимости, версия и правила установки (клиентский DNS-генератор);
- `openwrt-build.env` - параметры сборки для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов переиспользуемого OpenWrt workflow.

**Проверка изменений:** Изменения функциональности: генерация DNS-запросов изменяется в отдельном `dns-client-test`. Для упаковки проверяйте `Makefile`, `openwrt-build.env` и CI вместе; тестируйте итоговый пакет на нужной версии OpenWrt, поскольку сборка приложения сама по себе не проверяет установку и зависимости.

## Сборка

Сборка выполняется через GitHub Actions. Workflow этого репозитория вызывает общий reusable workflow из [openwrt-package-ci](https://github.com/karen07/openwrt-package-ci).

CI можно запустить:

- push тега вида `vX.Y.Z` - значение тега используется как версия OpenWrt;
- вручную через `workflow_dispatch`, указав версию OpenWrt и при необходимости фильтры target/subtarget.

Параметры этого пакета хранятся в `openwrt-build.env`. Общие `openwrt-build.sh`, `openwrt-matrix.py` и логика сборки через OpenWrt SDK находятся в `openwrt-package-ci`.

Для ручной сборки каталог `dns-client-test/` можно использовать как обычный package directory внутри OpenWrt buildroot/SDK.

## Структура проекта

- `dns-client-test/Makefile` - описание OpenWrt package;
- `openwrt-build.env` - параметры пакета для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов общего reusable workflow.

## Связанные проекты

- [dns-client-test](https://github.com/karen07/dns-client-test) - основной проект и исходный код клиента.

## Лицензия

Проект распространяется под лицензией GNU Affero General Public License v3.0. Подробности см. в файле [LICENSE](LICENSE).
