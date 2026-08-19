# История версий / Changelog

Все заметные изменения публичных сборок Aetheria перечисляются здесь.

All notable changes to public Aetheria builds are documented here.

## [0.1.0-test] — обновлено 2026-08-18

Первая публичная тестовая версия; pre-release регулярно пересобирается из актуального `main`.

### Обновление сборки 0a59aca

- Сетевой обрыв во время создания мира теперь **приостанавливает точный workflow-step**, а не запускает аварийный сценарий Главного ГМа.
- Checkpoint хранит исходный замысел, персонажа, индекс шага, завершённые результаты, стенограмму совета и полную историю прерванного agent-run с успешными tool results.
- «Повторить» возобновляет того же агента после последнего успешного tool result; завершённые шаги, участники совета и мутации не проигрываются заново.
- Пока генерация приостановлена, fallback-локации, открывающая сцена и обычные игровые ходы механически заблокированы.
- Создаётся локальное recovery-сохранение. Workflow checkpoint входит в save payload и восстанавливается после перезапуска/загрузки.
- Добавлен десятый базовый агент — **Архитектор Дерева мира**. В рабочей части стартового совета он создаёт большой иерархический каркас из 13–20 связанных локаций и 5–8 фракций; Worldsmith затем наполняет готовое дерево, а не строит вторую карту.
- Введён системный контракт **«один ответ — один игровой момент»**. Это не лимит символов: Narrative GM получает правила ритма, выбирает одно текущее изменение, показывает действие/немедленное последствие/одну точную деталь и сразу возвращает управление.
- Несколько `narrate` в одном ответе не обрезаются: весь литературный batch отклоняется, и агент обязан переформулировать его как один связный момент. Один корректный narrative-тег также принимается как момент.
- Кампанийный Prompt Hubber больше не может задавать размер ответа или «медленную длинную прозу» поверх игрового контракта.
- Варианты действий появляются только в настоящих точках решения, а не после каждого простого шага.
- Стили `dread` и `tense` теперь являются валидными стилями Narrator и не вызывают бессмысленные циклы исправления.
- После Prompt Hubber полный совет всех базовых агентов формирует единый план мира; после строительства второй полный совет проверяет результат, а Главный ГМ автоматически исправляет подтверждённые проблемы до открытия сцены.
- Каждый игровой ход, включая реплику в диалоге, механически начинается отдельным `council.call` с 1–3 нужными специалистами. Остальные tools не выполняются до получения стенограммы совета.
- Любой физический предмет теперь можно взять в руку: объект без специального слота попадает в `main_hand`, а `off_hand` доступен явно. Исправлен показанный в логе `Nokia 3310 → not_equippable`.
- В канале Главного ГМа F6 работает Markdown: заголовки, жирный/курсивный текст, списки, цитаты, inline/fenced code и ссылки.
- В OOC художественные tools скрыты и запрещены механически; `{narrative: ...}` преобразуется в прямой текст F6.
- `entity.create` больше не может перезаписать существующий `player` или другой занятый ID.
- Реальный LLMost image-запрос подтверждён: движок последовательно убрал неподдерживаемые `aspect_ratio` и `resolution`, после чего изображение было успешно создано.
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

- 1136 автоматических тестов;
- 13 279 проверок;
- 0 падений перед экспортом;
- smoke-запуск экспортированного EXE в чистом профиле.

---

First public test version; the pre-release is rebuilt regularly from the current `main`.

### Build 0a59aca update

- A network interruption during world creation now **pauses the exact workflow step** instead of starting an emergency Head GM scenario.
- The checkpoint preserves premise, character, step index, completed results, council transcript, and the interrupted agent message/tool history.
- Retry resumes the same agent after the last successful tool result; completed steps, council members, and mutations are not replayed.
- Fallback locations, opening narration, and normal gameplay are mechanically blocked while generation is paused.
- A local recovery save includes the workflow checkpoint and can restore it after restart/load.
- Added the tenth built-in agent, **World Tree Architect**. During the working phase of the startup council it creates a large hierarchy of 13–20 connected locations and 5–8 factions; Worldsmith fills the existing tree instead of creating a second map.
- Added the **one response = one playable moment** system contract. This is not a character cap: Narrative GM selects one current change, shows the action/immediate consequence/one precise detail, and returns control.
- Multiple `narrate` calls are not truncated. The entire chapter-like batch is rejected and the agent must reformulate it as one coherent moment. One correct narrative tag is also accepted.
- Campaign overlays can no longer request long/slow prose or override narrative density.
- Choices appear only at genuine decision points, not after every trivial step.
- `dread` and `tense` are valid narrative styles and no longer trigger correction loops.
- After Prompt Hubber, a full built-in-agent council agrees on the world plan. A second full council reviews the built world, and Head GM repairs verified findings before the opening scene.
- Every gameplay turn, including dialogue replies, must begin with a separate `council.call` using 1–3 relevant specialists. Other tools cannot run until Head GM receives the transcript.
- Every physical item can now be held: slotless objects default to `main_hand`, with explicit `off_hand` support. This fixes the logged `Nokia 3310 → not_equippable` failure.
- The Head GM F6 channel now renders Markdown: headings, bold/italic, lists, quotes, inline/fenced code, and links.
- Narrative presentation tools are hidden and mechanically denied in OOC; `{narrative: ...}` is reduced to direct F6 text.
- `entity.create` can no longer overwrite an existing player or any occupied entity ID.
- A real LLMost image request verified adaptive capabilities: the engine removed unsupported `aspect_ratio`, then `resolution`, and generated the image successfully.
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
