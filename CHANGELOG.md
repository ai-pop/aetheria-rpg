# История версий / Changelog

Все заметные изменения публичных сборок Aetheria перечисляются здесь.

All notable changes to public Aetheria builds are documented here.

## [0.1.0-test] — обновлено 2026-08-18

Первая публичная тестовая версия; pre-release регулярно пересобирается из актуального `main`.

### Обновление сборки 871a33f

- Строгие контракты между Главным ГМом, ГМом-рассказчиком и NPC: агент больше не получает заведомо запрещённые команды.
- NPC-команды автоматически привязываются к своему персонажу; исправлены `say`, `turn.end`, память, отношение и варианты имён tools с подчёркиваниями.
- Ошибка сети или API теперь показывается понятной карточкой с причиной, кнопками **«Повторить»** и **«Настройки»**; повтор продолжает прерванный ход без повторного применения успешных действий.
- Сетевой сбой при создании мира больше не запускает каскад одинаковых таймаутов.
- Prompt Hubber пишет только кампанийный стиль и не может переписать базовую роль агента.
- Автоматическая генерация мира применяет свои bootstrap-правила без четырёх последовательных 35-секундных подтверждений.
- Исправлена двойная прибавка номера хода и передача изображений/PF через workflow Главного ГМа.
- Ответы провайдера и аргументы tools разбираются без C++-ошибок на пустом, HTML или повреждённом JSON.

### Основное

- Текстовая RPG на Godot 4.5 с агентным LLM-циклом.
- 127 игровых инструментов и 9 базовых агентных ролей.
- Состояние мира: сущности, предметы, экипировка, эффекты, локации, квесты, фракции и время.
- Боевая система с действиями, зонами тела, бронёй, столкновениями и последствиями.
- Автономное рождение NPC: отдельные голос, память и снаряжение.
- Провайдеры LLMost, OpenAI-compatible, Anthropic, Ollama и LM Studio.
- SSE-стриминг, reasoning, usage-телеметрия, повторы запросов и диагностика.
- Русский и английский интерфейс.
- Сохранения, моды, data-driven workflows и инструменты.
- Прокручиваемый список сохранений.
- Отложенные подсказки с двухсекундным индикатором наведения.

### Проверка сборки

- 1114 автоматических тестов;
- 13 001 проверка;
- 0 падений перед экспортом;
- smoke-запуск экспортированного EXE в чистом профиле.

---

First public test version; the pre-release is rebuilt regularly from the current `main`.

### Build 871a33f update

- Strict Head GM, Narrative GM, and NPC contracts: agents are no longer offered commands the engine will inevitably reject.
- NPC calls are bound to their own character; fixed `say`, `turn.end`, memory, disposition, and underscore-form tool names.
- Network/API failures now appear as a clear card with the reason plus **Retry** and **Settings** actions. Retry resumes the interrupted turn without reapplying successful actions.
- A provider outage during world creation no longer starts a cascade of identical timeouts.
- Prompt Hubber writes campaign flavour only and cannot replace an agent's built-in role.
- Trusted world bootstrap rules no longer trigger four consecutive 35-second confirmation waits.
- Fixed double turn increments and image/PF forwarding through the Head GM workflow.
- Provider responses and tool arguments safely handle empty, HTML, and malformed JSON without C++ parser errors.

### Highlights

- Godot 4.5 text RPG with an agentic LLM loop.
- 127 game tools and 9 built-in agent roles.
- Persistent entities, items, equipment, effects, locations, quests, factions, and story time.
- Combat actions with body zones, armor, collisions, and consequences.
- Autonomous NPC birth with individual voice, memory, and equipment.
- LLMost, OpenAI-compatible, Anthropic, Ollama, and LM Studio providers.
- SSE streaming, reasoning handling, usage telemetry, retries, and diagnostics.
- Russian and English UI.
- Saves, mods, data-driven workflows, and tools.
- Scrollable save browser.
- Delayed two-second hover tooltips.
