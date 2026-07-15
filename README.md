# Custom ROMs — Galaxy Tab A7 (SM-T505 / gta4l · SM-T500 / gta4lwifi)

**[Русский](#русский) · [English](#english)**

---

## Русский

Кастомные прошивки на Android 11 (**PixelExperience Plus** и **LineageOS 18.1**) для Galaxy Tab A7 10.4: **SM-T505 (LTE, gta4l)** и **SM-T500 (Wi-Fi, gta4lwifi)**.

Особенности сборок: **Dolby Atmos** (рабочие профили), приложение **[System Tweaks](https://github.com/dolbaras/SystemTweaks)** (смена разрешения рендера/записи на лету), **4-канальный звук** ([гайд](docs/Quad-Speaker-Audio.md)), Google Camera (в PE).

### Скачать
Вкладка **[Releases](../../releases)** — архивы прошивок и md5.

### Перед установкой
- Сначала установи **последнюю официальную прошивку** для своей модели. На более ранних версиях полная работа не гарантируется.
- Нужен разблокированный загрузчик и рекавери (OrangeFox/TWRP).

### Установка
1. В OrangeFox → **Mount** снять галки с **System / Vendor / Product** (иначе установка на dynamic-partitions падает).
2. Install → выбрать zip → свайп.
3. Первая установка: **Wipe → Format Data** (`yes`).
4. Reboot → System. Первый запуск 5–15 минут.

LineageOS идёт без GApps — при желании флешить отдельно (MindTheGapps arm64).

### Отзывы
[Issues](../../issues): модель, версия стоковой прошивки, что не работает, `logcat`.

### Дисклеймер
Неофициально, ставите на свой риск. Разблокировка загрузчика триггерит Knox.

---

## English

Android 11 custom ROMs (**PixelExperience Plus** and **LineageOS 18.1**) for the Galaxy Tab A7 10.4: **SM-T505 (LTE, gta4l)** and **SM-T500 (Wi-Fi, gta4lwifi)**.

Build highlights: **Dolby Atmos** (working profiles), the **[System Tweaks](https://github.com/dolbaras/SystemTweaks)** app (change render/recording resolution on the fly), **4-channel audio** ([guide](docs/Quad-Speaker-Audio.md)), Google Camera (on PE).

### Download
The **[Releases](../../releases)** tab — ROM archives and md5.

### Before flashing
- First install the **latest official firmware** for your model. On older firmware full functionality isn't guaranteed.
- Unlocked bootloader and a recovery (OrangeFox/TWRP) required.

### Install
1. In OrangeFox → **Mount**, uncheck **System / Vendor / Product** (otherwise flashing to dynamic partitions fails).
2. Install → pick the zip → swipe.
3. First install: **Wipe → Format Data** (`yes`).
4. Reboot → System. First boot takes 5–15 minutes.

LineageOS ships without GApps — flash them separately if needed (MindTheGapps arm64).

### Feedback
[Issues](../../issues): model, stock firmware version, what fails, `logcat`.

### Disclaimer
Unofficial, use at your own risk. Unlocking the bootloader trips Knox.
