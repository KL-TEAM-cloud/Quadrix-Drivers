# Quadrix-Drivers

Каталог драйверов Linux для [Quadrix OS](https://github.com/KL-TEAM-cloud/Quadrix_OS).

Драйверы из ядра Linux (исходники без изменений) собраны как загружаемые
модули для слоя драйверов Linux в Quadrix (процесс `lxdrv`) и упакованы в
подписанные пакеты `.qdrv`. Quadrix OS скачивает их сама:
**Параметры → Устройства → «Найти драйвер»** у устройства без драйвера.

## Как устроен каталог

Каждый релиз содержит:

| Файл | Что это |
|------|---------|
| `drivers.index` | список пакетов: id, версия, название, файл, PCI ID устройств, описание |
| `org.quadrix.driver.<модуль>-<версия>.qdrv` | пакет драйвера: модуль `.ko` и его PCI ID, подпись Ed25519 |
| `quadrix-linux-drivers-src.tar` | исходники слоя драйверов и драйверов Linux (GPLv2) |

Система читает последний релиз:
`https://github.com/KL-TEAM-cloud/Quadrix-Drivers/releases/latest/download/drivers.index`.
Пакеты подписаны ключом каталога; его открытая часть входит в доверенные
ключи Quadrix OS (`/system/etc/trusted-keys`).

Релизы публикует GitHub Actions из репозитория Quadrix OS (workflow
«Каталог драйверов», метка `drivers-<версия>`).

## Лицензия

Драйверы и слой совместимости — GNU GPL v2 (`COPYING`). Исходники каждого
релиза приложены к нему (`quadrix-linux-drivers-src.tar`).
