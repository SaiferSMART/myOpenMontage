# Передача из ветки «Живой текст»: форк myOpenMontage — разобрать под видеопроекты

Дата: 25.07.2026. Отправитель: ветка «Живой текст» (D:\Antiplastik).
Решение Евгении: разбор форка отдать ветке ScreenVideo.

---

## Что это

Евгения форкнула 24.07: **`SaiferSMART/myOpenMontage`** (форк `calesthio/OpenMontage`), публичный, 2461 файл, 75 МБ.
Заявка автора: «World's first open-source, agentic video production system. 12 production pipelines,
100+ tools, 700+ agent skills».

Структура корня: `.agents/`, `.claude/`, `.codex/`, `.cursor/` (скиллы под разные IDE), `backlot/`,
`ink-theater/`, `lib/`, `pipeline_defs/`, `remotion-composer/`, `schemas/`, `scripts/`, `skills/`
(INDEX.md + core/creative/meta/pipelines), `styles/`, `tools/`, `tests/`. Плюс AGENTS.md, AGENT_GUIDE.md,
CLAUDE.md, PROJECT_CONTEXT.md, PROMPT_GALLERY.md, Makefile, requirements*.txt (есть GPU-вариант).

## ⚠️ ГЛАВНОЕ, до того как что-то оттуда брать: лицензия AGPL-3.0

Самый заразный копилефт из распространённых. Практический смысл:

- **Личное использование как инструмента** (монтировать свои ролики у себя на машине) — можно, AGPL
  срабатывает на распространении.
- **Идеи, форматы, методички** (как строится сценарий, как верстается нарратив, как оформляются титры) —
  можно: идеи лицензией не покрываются, покрывается код и текст.
- **Тащить их код в продукт, который отдаётся людям через сеть** (сайт, бот, мини-апп, витрина) —
  НЕЛЬЗЯ без открытия исходников всего продукта на AGPL. Для коммерческих продуктов Евгении это
  прямой конфликт.

**Первым пунктом разбора — проверить лицензию по САМОМУ файлу LICENSE в репозитории**, а не по README
и не по моему пересказу; заодно посмотреть, не менялась ли лицензия в истории. Это приём из канона
(`D:\Downloads\Рабочая-схема-веток.html`, секция «3а. Приёмы»): статьи и пересказы врут, а снимок
лицензии на момент скачивания — единственное доказательство. Снимок сохранить рядом.

## Где это реально полезно

Форк — про видео, не про текст. Ложится на:
- **ScreenVideo** («Запись эфира») — твой проект;
- **Промо-обзор Studio** (D:\Promo-Obzor-Studio) — монтаж роликов с диктором;
- **Muzograf** — там как раз титры и субтитры;
- **youtube-autopost / insta-autopost** — сборка контента.

Конкретно по текстовой части я нашёл 166 файлов, релевантных сценариям и титрам. Самые интересные пути:
```
.agents/skills/hyperframes-core/references/script-format.md
.agents/skills/hyperframes-creative/references/narration.md
.agents/skills/hyperframes-creative/references/house-style.md
.agents/skills/hyperframes-media/references/captions/authoring.md
.agents/skills/hyperframes-animation/adapters/animate-text.md
.agents/skills/hyperframes-animation/blueprints/typewriter-reveal.md
.agents/skills/create-video/references/visual-styles.md
.agents/skills/azure-speech-to-text/SKILL.md
.agents/skills/heygen/references/{scripts,captions,voices,text-overlays}.md
.agents/skills/avatar-video/references/{scripts,captions,text-overlays,voices}.md
.agents/skills/hyperframes-creative/scripts/extract-audio-data.py
```
⚠️ Не путать: папка `styles/` в корне — это ВИЗУАЛЬНЫЕ стили (`anime-ghibli.yaml`,
`flat-motion-graphics.yaml`, `premium-minimalist.yaml`, `clean-professional.yaml`,
`minimalist-diagram.yaml`), к «авторскому стилю текста» отношения не имеет.

## Что просила Евгения

«Посмотри там всё, что нужно» — то есть пройти форк и вытащить, что годится в её видеоконтур,
с оглядкой на лицензию. Разбор раздавать подрядчикам по схеме: чтение и выжимки → ChatGPT,
код по репозиторию → Cursor/Grok (у него запасы огромные: Ultra израсходован на 5%, сброс 9 августа,
пропорция по канону — больше половины объёма на Grok).

## Предложение по объёму разбора (решает ветка ScreenVideo)

1. **Лицензия** — вердикт по файлу LICENSE: что можно личным инструментом, что можно как идеи,
   что нельзя в продукт. Одна страница, без юридической воды.
2. **Инвентарь** — какие из 12 пайплайнов и 100+ инструментов реально применимы к её задачам
   (запись экрана → монтаж → титры → выкладка), а какие требуют платных внешних сервисов
   (HeyGen, Azure) или GPU.
3. **Что забрать как идеи** — форматы сценария, нарратива, титров; сравнить с тем, что уже написано
   в «Промо-обзоре» и ScreenVideo, отметить, где у них лучше.
4. **Что можно запустить локально** — есть `render_demo.py`, `render-demo.sh`, Makefile,
   `requirements-gpu.txt`; проверить, поедет ли на её машине и что для этого нужно.

## Контекст, который пригодится

- Канон рабочей схемы: `D:\Downloads\Рабочая-схема-веток.html` (v3.4, 18 правил, 28 граблей, 6 приёмов).
- Грабли по проектам: `D:\Saifer-AI-Workflow\грабли\`.
- Транскрибация видео без локального whisper (может пригодиться ScreenVideo): ffmpeg-нарезка по 30 минут
  + LiteLLM-хаб, модель `buddy-sluh`, ключи-донор `D:\buddy_bot\.env`. 30 минут аудио — 10 секунд работы.
  Проверено сегодня на эфире 2 ч 36 мин.
