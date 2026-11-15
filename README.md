<h1 align=center><code>BlockerPasses</code></h1>

<div align=center>
  <img src=https://img.shields.io/badge/Counter--Strike%202-Metamod%202.0%20(KHook)-orange?style=flat-square alt=metamod>
  <a href=https://github.com/Cookies2122/cs2-blockerpasses/commits><img src=https://img.shields.io/github/last-commit/Cookies2122/cs2-blockerpasses?style=flat-square alt="last commit"></a>
  <a href=LICENSE><img src=https://img.shields.io/github/license/Cookies2122/cs2-blockerpasses?style=flat-square alt=license></a>
</div>
<br>

Админ через меню ставит на карте пропы и beam-стены. Пока игроков меньше заданного числа, они появляются каждый раунд и закрывают проходы.

> Автор плагина: [ABKAM](https://github.com/ABKAM2023). Здесь версия 2.0.1 под новый SDK и Metamod 2.0, оригинал: [ABKAM2023/cs2-blockerpasses](https://github.com/ABKAM2023/cs2-blockerpasses).

## Что нужно

- [Metamod:Source](https://github.com/alliedmodders/metamod-source) 2.0 (KHook)
- [Utils](https://github.com/Pisex/cs2-menus)
- [Admin System](https://github.com/Pisex/cs2-admin_system) (права на меню, без него доступ даётся командой `mm_bp_access`)
- [ResourcePrecacher](https://github.com/Pisex/ResourcePrecacher) (модели пропов)

Пути моделей нужно добавить в ResourcePrecacher, например:

```
"dust_rollupdoor_96x128_surface_lod"    "models/props/de_dust/hr_dust/dust_windows/dust_rollupdoor_96x128_surface_lod.vmdl"
"chainlink_fence_001_256_capped"    "models/props/de_nuke/hr_nuke/chainlink_fence_001/chainlink_fence_001_256_capped.vmdl"
"dust_soccer_ball001"   "models/props/de_dust/hr_dust/dust_soccerball/dust_soccer_ball001.vmdl"
```

## Установка

Соберите плагин (раздел [Сборка](#сборка)) и скопируйте содержимое `build/package` в папку `csgo` на сервере. В пакете лежит:

| Файл | Куда |
| --- | --- |
| `BlockerPasses.so` | `addons/BlockerPasses/` |
| `BlockerPasses.vdf` | `addons/metamod/` |
| `settings.ini` | `addons/configs/BlockerPasses/` |
| `bp_data.ini` | `addons/data/` |
| `blockerpasses.phrases.txt` | `addons/translations/` |

После этого перезапустите сервер или смените карту.

## Команды

| Команда | Что делает |
| --- | --- |
| `!bp` | открыть меню (в консоли `mm_bp`) |
| `mm_bp_access <steamid64>` | выдать временный доступ к меню, если нет Admin System |

## Настройки

### settings.ini

`addons/configs/BlockerPasses/settings.ini`

| Ключ | По умолчанию | Что делает |
| --- | --- | --- |
| `min_players_to_open` | `10` | с какого числа игроков проходы открываются |
| `access_permission` | `@admin/bp` | право Admin System для меню |
| `chat_command` | `!bp` | чат-команда меню |
| `console_cmd_bp` | `mm_bp` | консольная команда меню |
| `console_cmd_access` | `mm_bp_access` | консольная команда выдачи доступа |
| `debug_log` | `0` | отладка в консоль, 1 включить |
| `ignore_spectators` | `1` | 1 не считать наблюдателей, 0 считать |

В секции `models` список моделей для меню: `label` название, `path` путь к модели.

<details>
<summary>Весь файл settings.ini</summary>

```
"BlockerPasses"
{
	// Минимальное количество игроков для открытия проходов
	"min_players_to_open"	"10"

	// Права доступа к команде !bp
	"access_permission"		"@admin/bp"

	// Команда в чате для открытия меню (например !bp, !blocker, !pass)
	"chat_command"			"!bp"

	// Консольная команда для открытия меню
	"console_cmd_bp"		"mm_bp"

	// Консольная команда для выдачи временного доступа
	"console_cmd_access"	"mm_bp_access"

	// Включить отладочные сообщения в консоль (0 - выкл, 1 - вкл)
	"debug_log"				"0"

	// Не считать наблюдателей при подсчёте игроков (0 - считать, 1 - не считать)
	"ignore_spectators"		"1"

	// Список моделей для размещения через меню
	"models"
	{
		"model1"
		{
			"label" "Желзеные двери"
			"path"  "models/props/de_dust/hr_dust/dust_windows/dust_rollupdoor_96x128_surface_lod.vmdl"
		}
		"model2"
		{
			"label" "Желзеный забор"
			"path"  "models/props/de_nuke/hr_nuke/chainlink_fence_001/chainlink_fence_001_256_capped.vmdl"
		}
	}
}
```

</details>

### bp_data.ini

`addons/data/bp_data.ini`

Здесь хранятся поставленные предметы по картам, файл заполняется из меню. Сейчас в нём пример: четыре стены на de_mirage.

## Переводы

Файл `addons/translations/blockerpasses.phrases.txt`, языки: ru, en. Его можно править под себя.

<details>
<summary>Все фразы</summary>

```
"Phrases"
{
	"Chat_Prefix"
	{
		"ru" "{GREEN}[BlockerPasses]{DEFAULT}"
		"en" "{GREEN}[BlockerPasses]{DEFAULT}"
	}

	"Chat_NoAccess"
	{
		"ru" "{DEFAULT}Нет доступа к {RED}!bp{DEFAULT}."
		"en" "{DEFAULT}No access to {RED}!bp{DEFAULT}."
	}

	"Chat_ClosedMsg"
	{
		"ru" "Проход закрыт. Откроется при {RED}%d{DEFAULT} игроках."
		"en" "Passage is closed. It will open at {RED}%d{DEFAULT} players."
	}

	"Chat_WallPos1"
	{
		"ru" "Поставьте первую точку пингом (колёсико мышки)"
		"en" "Place the first point with a ping (mouse wheel)"
	}

	"Chat_WallPos2"
	{
		"ru" "Теперь поставьте вторую точку пингом (колёсико мышки)"
		"en" "Now place the second point with a ping (mouse wheel)"
	}

	"Chat_WallCreated"
	{
		"ru" "Стена создана!"
		"en" "Wall created!"
	}

	"Chat_MustBeAlive"
	{
		"ru" "Для этого вы должны быть живы"
		"en" "You must be alive for this"
	}

	"Chat_UsePing"
	{
		"ru" "Выберите место с помощью пинга (колёсико мышки)"
		"en" "Choose a location with a ping (mouse wheel)"
	}

	"Menu_Title"
	{
		"ru" "BlockerPasses"
		"en" "BlockerPasses"
	}

	"Menu_Place"
	{
		"ru" "Поставить предмет"
		"en" "Place an item"
	}

	"Menu_Wall"
	{
		"ru" "Создать стену (beam)"
		"en" "Create wall (beam)"
	}

	"Menu_Edit"
	{
		"ru" "Редактировать предметы"
		"en" "Edit items"
	}

	"Menu_ModelTitle"
	{
		"ru" "Выбор модели"
		"en" "Select model"
	}

	"Menu_NoModels"
	{
		"ru" "Нет моделей"
		"en" "No models"
	}

	"Menu_EditPick"
	{
		"ru" "Выбери предмет"
		"en" "Choose an item"
	}

	"Menu_NoItems"
	{
		"ru" "Нет предметов"
		"en" "No items"
	}

	"Menu_Move"
	{
		"ru" "Двигать"
		"en" "Move"
	}

	"Menu_Rotate"
	{
		"ru" "Поворачивать"
		"en" "Rotate"
	}

	"Menu_Scale"
	{
		"ru" "Масштаб"
		"en" "Scale"
	}

	"Menu_Teleport"
	{
		"ru" "Телепортироваться"
		"en" "Teleport"
	}

	"Menu_BeamColor"
	{
		"ru" "Цвет лазера"
		"en" "Beam color"
	}

	"Menu_BeamColorTitle"
	{
		"ru" "Цвет лазера"
		"en" "Beam color"
	}

	"Menu_ItemColor"
	{
		"ru" "Цвет предмета"
		"en" "Item color"
	}

	"Menu_ItemColorTitle"
	{
		"ru" "Цвет предмета"
		"en" "Item color"
	}

	"Menu_PingMove"
	{
		"ru" "Телепортировать пингом"
		"en" "Move with ping"
	}

	"Menu_MoveTrace"
	{
		"ru" "Перенести в точку прицела"
		"en" "Move to crosshair"
	}

	"Menu_InvisOn"
	{
		"ru" "Скрыть"
		"en" "Hide"
	}

	"Menu_InvisOff"
	{
		"ru" "Показать"
		"en" "Show"
	}

	"Menu_Delete"
	{
		"ru" "Удалить"
		"en" "Delete"
	}

	"Menu_MoveTitle"
	{
		"ru" "Движение"
		"en" "Movement"
	}

	"Menu_RotateTitle"
	{
		"ru" "Поворот"
		"en" "Rotation"
	}

	"Menu_ScaleTitle"
	{
		"ru" "Масштаб"
		"en" "Scale"
	}

	"Menu_WallRotate"
	{
		"ru" "Поворот стены"
		"en" "Wall rotation"
	}

	"Menu_WallRotateTitle"
	{
		"ru" "Поворот стены"
		"en" "Wall rotation"
	}

	"Menu_WallScale"
	{
		"ru" "Размер стены"
		"en" "Wall size"
	}

	"Menu_WallScaleTitle"
	{
		"ru" "Размер стены"
		"en" "Wall size"
	}
}
```

</details>

## Что изменено

По сравнению с оригиналом:

- Переведено на новый SDK ([Wend4r/sourcesdk](https://github.com/Wend4r/sourcesdk)), старый после обновления CS2 от 12.11.2026 уже не подходит.
- Работает только на Metamod 2.0 (KHook), старый Metamod на SourceHook больше не поддерживается.
- Заголовки Utils обновлены под текущую версию, имена интерфейсов теперь `UTILS_INTERFACE` и `MENUS_INTERFACE`.
- Своя функция `GameEntitySystem()` убрана, в новом SDK entity system берётся через `IGameResourceService`.
- SchemaEntity обновлена: актуальные оффсеты виртуальных функций.
- При выгрузке плагин проверяет, что Utils ещё загружен. Раньше `meta unload` после выгрузки Utils мог уронить сервер.

## Сборка

Собирается на Linux. Нужны clang, python3, cmake и [AMBuild](https://github.com/alliedmodders/ambuild). Все команды ниже выполняются из одной папки.

**1. SDK.** Нужен [sourcesdk](https://github.com/Wend4r/sourcesdk) не старее обновления CS2 от 12.11.2026. Собирается один раз:

```bash
git clone --recursive https://github.com/Wend4r/sourcesdk hl2sdk-cs2
cmake -S hl2sdk-cs2 -B hl2sdk-cs2/build -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DSOURCESDK_AM_DEFINES=ON -DSOURCESDK_USE_MINIMAL_PROTOS=OFF
cmake --build hl2sdk-cs2/build -j$(nproc)
export HL2SDKCS2=$PWD/hl2sdk-cs2
```

**2. Metamod.** Нужен Metamod 2.0 с KHook, ветка `master`. Со старым Metamod на SourceHook сборка остановится с ошибкой.

```bash
git clone --recursive https://github.com/alliedmodders/metamod-source
```

**3. Плагин.** Папка SchemaEntity должна лежать рядом с папкой плагина.

```bash
git clone https://github.com/Cookies2122/SchemaEntity
git clone https://github.com/Cookies2122/cs2-blockerpasses
cd cs2-blockerpasses
mkdir build && cd build
python3 ../configure.py --enable-optimize --sdks=cs2 --targets=x86_64 --mms_path=$PWD/../../metamod-source --hl2sdk-manifests=../hl2sdk-manifests
ambuild
```

Готовые файлы появятся в `build/package`.

## Автор

Плагин написал [ABKAM](https://github.com/ABKAM2023), оригинал: [ABKAM2023/cs2-blockerpasses](https://github.com/ABKAM2023/cs2-blockerpasses).
Перенос на новый SDK и Metamod 2.0, исправления: \_ded\_cookies.

## Лицензия

GPL-3.0, текст в файле [LICENSE](LICENSE). В коде плагина лицензия тоже указана как GPL. Авторские права на оригинальный код у ABKAM.
