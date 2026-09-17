# 🏆 AWARD-GRADE MOBILE UI — Visual Patterns Lab
### Интерактивный каталог award-winning UI/interaction паттернов для Phaser 4 · v3.0

**Автор:** Senior UI/Interaction Designer, AAA+ mobile studio
**Фокус курса:** только визуальная и интерактивная часть — то, что превращает обычную игру в игру уровня Apple Design Awards / Google Play Best of.
**Технология:** Phaser 4 (release «Caladan», 10.04.2026)
**Метод:** 80/20 — выделяем ⭐ «Золотую дорожку» (~60 паттернов), дающую 80% award-ощущения. Остальное — полная библиотека для глубокого погружения.

---

## 📊 МАСШТАБ КАТАЛОГА

| Раздел | Паттернов | ⭐ Золото (20%) |
|---|---|---|
| 1. Motion Foundations | 8 | 3 |
| 2. Buttons & Touch Responses | 12 | 4 |
| 3. Menus & Navigation | 38 | 6 |
| 4. Scroll-driven UI | 32 | 5 |
| 5. Parallax & Depth Systems | 22 | 4 |
| 6. Sliders, Knobs & Selectors | 44 | 5 |
| 7. Carousels & Cards | 70 | 6 |
| 8. Inventory & Drag-and-Drop | 28 | 4 |
| 9. HUD & Progress | 63 | 6 |
| 10. Lists, Grids & Collections | 23 | 4 |
| 11. Popups, Modals & Overlays | 33 | 5 |
| 12. Maps, Level Selection & Skill Trees | 34 | 5 |
| 13. Mobile Game Controls | 27 | 5 |
| 14. Special Interactive Elements | 30 | 5 |
| 15. UI Effects Lab (модификаторы) | 51 | 5 |
| 16. Performance & Accessibility | 12 | 4 |
| **Итого** | **≈530** | **≈76** |

---

## ⚙️ PHASER 4: ПОЧЕМУ ОН МЕНЯЕТ ПРАВИЛА ИГРЫ

Каталог использует фичи, недоступные в v3 — на них построены все рецепты:

| Фича v4 | Что даёт для award-UI |
|---|---|
| **Новый WebGL-рендерер (RenderNodes)** | Стабильный кадр, до 100x быстрее — фундамент «дорогого» ощущения |
| **Filters: единая система** (`filters.internal` / `filters.external`) | Blur, Glow, Bloom, Shadow, Vignette, Wipe, ColorMatrix, Pixelate, Bokeh, Displacement, GradientMap, Blend, Quantize — **на любом объекте и камере**, стеком |
| `AddEffectBloom() / AddEffectShine() / AddMaskShape()` | Блики и «голограммы» в одну строку |
| **Gradient** (linear/radial/conic/bilinear) | Живые заливки, liquid-эффекты без текстур |
| **Noise** (Simplex/Cellular/Worley на GPU) | Диззолвы, шиммер, процедурные фоны, дым/огонь для UI |
| **SpriteGPULayer / TilemapGPULayer** | Кипящие фоны меню и параллакс без просадки FPS |
| **Новая модель освещения** (self-shadows, normal maps) | Объём кнопок, карт, HUD-элементов без ручных шейдеров |
| **FilterMask** (маски = фильтры) | Reveal-эффекты, scratch, fog of war, шторки |
| **Camera rewrite** (scroll, zoom, shake, rotation) | Параллакс, pinch-zoom карт, cinematic reveal боссов |
| DynamicTexture (`render()`), Stamp, CaptureFrame | Snapshot-морфы, FLIP-переходы, scratch-механики |
| Tweens + Tween Chains + Timelines | Хореография состояний кнопок и карточек |

---

## 🧩 АНАТОМИЯ КАЖДОГО ДЕМО

Каждый паттерн в каталоге = **живое Phaser 4 демо** с единой структурой:

1. **Демо** — интерактивное, с пальцем/мышью
2. **Панель параметров** — speed, stiffness/damping, слои/глубина, perspective, blur, источник управления (touch / scroll / gyro)
3. **Разбор «как устроено»** — код-рецепт на Phaser 4 (какие фильтры, твины, маски)
4. **«Где в игре»** — типовые игровые сценарии применения
5. **Чек-лист качества** — тайминги, тап-таргеты, states

**Глобальные переключатели в каждом демо:** Reduce Motion · режим левши · размер touch-таргета · mute-safe (вся обратная связь — визуальная, не звуковая) · safe areas.

---

## 📚 16 РАЗДЕЛОВ КАТАЛОГА

---

### 1 · MOTION FOUNDATIONS ⚙️ фундамент всего

Прежде чем трогать кнопки — язык движения. Без этого раздела остальные 15 — набор трюков.

| Группа | Паттерны | Phaser 4 |
|---|---|---|
| Тайминги UI | ⭐ калибровка длительностей (100 мс клик / 200 мс микротранзишн / 350 мс экран), stagger-хореография, overlap вместо последовательности | Tweens, Timelines, Tween Chains |
| Кривые | ⭐ галерея easing на реальных объектах (back, elastic, cubic, expo), custom bezier, spring-интегратор (stiffness/damping) | Tween eases + свой Spring-класс на scene.update |
| Принципы | anticipation → action → follow-through на UI-элементе, squash & stretch, вторичное движение | scaleX/scaleY counter-tweens |
| Дисциплина | анимируем только transform (x/y/scale/angle/alpha), Reduce Motion — одна переключалка на всё | RenderNode-статистика |

---

### 2 · BUTTONS & TOUCH RESPONSES — 12 паттернов

Не коллекция кнопок, а **характеры и сценарии**.

| Паттерн | Суть | Phaser 4 |
|---|---|---|
| ⭐ **Spring press** | Вдавливание, squash, блик, пружинный возврат | tween yoyo + `filters.internal.addGlow` |
| ⭐ **Liquid fill** | Заполнение из точки касания | FilterMask + Gradient + круг-маска из точки |
| ⭐ **Hold-to-confirm** | Удержание с круговым прогрессом и финальным snap | Graphics arc + камер-shake при commit |
| ⭐ **Morphing state** | Buy → Loading → Success → Equipped | Timeline + CrossFade через DynamicTexture |
| Drag-to-confirm | Ползунок подтверждения (покупка/удаление/старт) | drag + resistance + snap-зоны |
| Charge button | Накопление энергии, дрожь, импульс на релизе | noise-тряска + частицы |
| Magnetic touch | Кнопка следует за пальцем в малой зоне | lerp к pointer в радиусе |
| Split action | Основное действие + раскрывающаяся вторичная | container + дуговой stagger |
| Destructive | Антиципация → предупреждение → контролируемое разрушение | частицы + Wipe + shake |
| Multi-stage | normal / pressed / charged / cooldown / disabled | state machine + 5 визуальных слоёв |
| Contextual FAB | Меняет форму и функцию от контекста | morph по DynamicTexture |
| Button swarm | Действия вылетают из кнопки по дуге | частицы-иконки + stagger |

---

### 3 · MENUS & NAVIGATION — 38 паттернов

**Нижняя навигация (10):** ⭐ gooey tab bar (метаболы) · ⭐ floating island tab bar · ⭐ expanding active tab · sliding capsule · elastic indicator · liquid blob · icon-to-label morph · curved notch · contextual tab bar · hide-on-scroll tab bar.
**Главные меню (8):** ⭐ layered cinematic menu (многослойный параллакс-фон) · card-based с depth/parallax · horizontal world menu · character-centered · expandable tile · constellation · portal menu · ⭐ diegetic menu (интерфейс в объектах мира).
**Боковые и доп. (12):** ⭐ weapon wheel / radial · slide drawer · push-content drawer · liquid edge drawer · fan menu · arc menu (одна рука) · long-press contextual · pie menu · command palette · fold-out toolbar · edge-swipe quick menu.
**Пауза и настройки (8):** ⭐ blur pause menu (фон уходит в боке) · ⭐ morphing pause ‖→× · freeze-frame · layered pause cards · accordion settings · settings с живым preview · animated segmented nav · пауза с параллаксом.

**Phaser 4:** gooey = связка `FilterBlur + FilterThreshold` (эффект метабола) · cinematic-меню = несколько слоёв с разным `scrollFactor` + SpriteGPULayer для фонов · пауза = `filters.external.addBlur` на сцену игры · weapon wheel = container + drag-угол + snap.

---

### 4 · SCROLL-DRIVEN UI — 32 паттерна

**Базовые (7):** ⭐ collapsing header · ⭐ section snap · ⭐ elastic overscroll · sticky tabs · scroll progress line · scroll-aware nav (прячется вниз, возвращается вверх) · velocity-aware UI (при быстром свайпе детали упрощаются).
**Композиции (15):** ⭐ coverflow scroll · ⭐ card stack · depth tunnel (полёт по Z) · horizontal chapters · parallax shelf · layered world map · scroll timeline · character showcase (скролл вращает персонажа) · pinned scene · before/after reveal · scroll-driven portal · zoom-through interface (камера входит в карточку) · infinite looping scroll · skill tree по скроллу · scroll-linked background (цвет/материал/свет между разделами).
**Игровые применения (10):** ⭐ Battle Pass road · quest timeline · season history · achievement gallery · character progression · weapon collection · store categories · daily rewards calendar · narrative codex · level selection map.

**Phaser 4:** свой ScrollController (drag + инерция + lerp-snap) — DOM-скролла нет · velocity из `pointer.velocity` для LOD-упрощения · прогресс = входной сигнал, который мапится в scale/pos/alpha/mask элементов · TileSprite для бесконечных лент.

---

### 5 · PARALLAX & DEPTH SYSTEMS — 22 паттерна

**Виды (12):** ⭐ multi-plane scene parallax · ⭐ pointer/touch parallax · ⭐ gyroscope parallax · scroll parallax · gesture velocity parallax · spring-delayed parallax · inverted parallax · depth-of-field parallax (blur по глубине) · perspective card parallax · reflection/highlight parallax · layered text · floating particle parallax.
**Элементы (10):** ⭐ 3D reward card (наклон + блик + частицы + слои) · character selection card (слои движутся независимо) · game mode tile (фон отстаёт, иконка опережает, текст стабилен) · parallax main menu · inventory inspection (реакция на наклон) · parallax world map · depth carousel · holographic card (спектральный блик от угла) · window into another world · parallax dialog.

**Панель настроек каждого демо:** слои · глубина · коэффициент · stiffness/damping · perspective · blur по глубине · источник (touch/scroll/gyro) · Reduce Motion.
**Phaser 4:** камеры с разным `scrollFactor` · DeviceOrientationEvent для гиро · `FilterBlur` на дальних слоях = DOF · `AddEffectShine` + GradientMap для голограмм · Noise для партикл-глубины.

---

### 6 · SLIDERS, KNOBS & SELECTORS — 44 паттерна

**Линейные (15):** ⭐ rubber slider (выход за границы с пружиной) · ⭐ discrete snap slider (магнитные деления) · spring slider · liquid track · растущий thumb · tooltip из бегунка · range (два бегунка) · color gradient slider · slider с preview · curved path slider · vertical · с инерцией · с resistance-зонами.
**Игровые применения (9):** сложность · громкость · яркость · чувствительность · сила способности · распределение характеристик · сравнение оружия · ставка/количество · progress scrubber для replay.
**Knobs (8):** ⭐ rotary knob · infinite dial · safe lock dial · radial progress selector · circular difficulty selector · clock-style · rotating rune selector · multi-ring selector.
**Picker'ы (12):** ⭐ wheel picker · ⭐ slot-machine picker · snap carousel selector · segmented control · animated chips · toggle group · morphing dropdown · filter pills · rarity selector · difficulty cards · class selector.

**Phaser 4:** drag + свой spring-интегратор для rubber/инерции · rotation-маппинг для knobs · wheel picker = вращающийся контейнер + `Math.sin` для «3D» барабана · slot machine = Tween Chain со ступенчатой остановкой и overshoot.

---

### 7 · CAROUSELS & CARDS — 70 паттернов

**Карусели (20):** ⭐ center-snapping · ⭐ coverflow 3D · ⭐ infinite · card stack · tinder-swipe deck · circular · arc · wheel · vertical · multi-row · peek (край следующей виден) · expandable · variable-width · momentum + rubber edges · с прогресс-индикатором · с animated background · masked transitions · parallax внутри карточек.
**Эффекты переключения (12):** scale · rotation · depth · blur · desaturation · glow · liquid stretch · shared background color · particles · mask reveal · card unfold · glass refraction.
**Карточки-трансформеры (26):** ⭐ card → detail page (FLIP) · ⭐ stack → grid · card → bottom sheet · card → fullscreen · card → equipment slot · card → comparison panel · card → 3D inspection · ⭐ card → reward reveal (pack opening) · compact → expanded stats · collectible flip · foldable · peel-to-reveal · scratch card · burning/dissolving · frozen unlock · breaking seal · upgrade evolution · card fusion · duplicate merge · drag to target · reorderable · swipe actions · multi-select.
**Применения (12):** character/skin/weapon/level/mode selection, reward preview, card collection, store offers, news/events, achievements, pet selection, world selection.

**Phaser 4:** FLIP вручную: First (capture) → Last (layout) → Invert (tween from) → Play · morph-надёжность через DynamicTexture snapshot исходной карточки · coverflow = per-frame раскладка scale/angle/alpha по дистанции от центра · ColorMatrix для desaturation дальних карточек.

---

### 8 · INVENTORY & DRAG-AND-DROP — 28 паттернов

**Механики (20):** ⭐ drag + magnetic slot snapping · ⭐ item fly-to-inventory · ⭐ loot vacuum · ⭐ item merge · invalid drop return · slot highlight по совместимости · swap · stack splitting · long-press pickup · drag ghost · auto-scroll при переносе · drag to character (equip) · drag to trash · drag to craft · multi-select · reorder grid · expandable slot · compare items · quick equip.
**Эффекты (8):** предмет уменьшается в слот · trail за движением · подходящие слоты пульсируют · несовместимый слот отталкивает · редкий предмет оставляет glow trail · merge = два в один с вспышкой · equip переносит рамку на персонажа · заполненный слот пружинит + ripple.

**Phaser 4:** нативные drag-события · ghost = CaptureFrame/DynamicTexture snapshot · магнит = поиск ближайшего слота + spring-tween · glow trail = `AddEffectBloom` + частицы · equip-линия = Graphics stroke с прогрессом.

---

### 9 · HUD & PROGRESS — 63 паттерна

**Полосы (16):** ⭐ health bar с delayed/chip damage · ⭐ radial cooldown · segmented armor · shield · stamina · mana · XP · boss health · overheat · combo meter · danger meter · oxygen · stealth visibility · rhythm accuracy · ability charge · ult meter (перестраивает рамку экрана).
**Поведение (12):** ⭐ damage chunk отлетает с задержкой · критическое здоровье деформирует бар · переполнение = overshield · регенерация отдельным слоем · статус-иконка становится таймером · несколько ресурсов в один компактный контрол · HUD сворачивается вне боя · HUD реагирует на направление угрозы · cooldown заполняется жидкостью · ability icon замерзает/трескается · ⭐ boss bar с cinematic reveal (letterbox).
**Счётчики (8):** ⭐ одометр/rolling digits · pop count · fly-to-counter · delayed banking · milestone burst · coins · gems · combo.
**Progress/Loading (27):** ⭐ skeleton shimmer · ⭐ portal loading (лоадер становится контентом) · ⭐ pull-to-refresh · liquid fill · wave fill · path/map route progress · battle pass track · multi-stage loading · placeholder morph · hold-to-load · logo loader · puzzle loader · character animation loader · download/install progress · unlock seal · breaking lock · fog clearing · chest opening progress · research/construction timers.

**Phaser 4:** delayed damage = два бара, второй lerp-догоняет в `update()` · одометр = колонки цифр BitmapText + tween y · radial = Graphics arc · shimmer = Gradient + маска-sweep · letterbox = камеры + tween viewport · coin fly = bezier-путь через кастомный onUpdate.

---

### 10 · LISTS, GRIDS & COLLECTIONS — 23 паттерна

⭐ staggered entry (каскадное появление) · ⭐ FLIP sort-переход · ⭐ swipe actions · ⭐ virtualized list · animated insert/remove · reorderable · expandable row · accordion · sectioned · sticky group headers · search filtering transition · grid↔list · grid reflow · masonry · infinite list · select mode · batch actions · locked/unlocked transitions · empty-state transformation · new-item highlight · recently acquired sorting · collection completion effect · rarity-based layout.

**Phaser 4:** пул объектов + layout-функция (никаких тысяч отображённых объектов) · FLIP через snapshot · completion effect = частицы + Bloom + camera flash.

---

### 11 · POPUPS, MODALS & OVERLAYS — 33 паттерна

**Типы (22):** ⭐ draggable bottom sheet · ⭐ reward popup · ⭐ coach mark (спотлайт на элементе) · center modal · multi-level bottom sheet · side sheet · fullscreen dialog · popover from source · tooltip · context bubble · confirmation · level-up popup · achievement banner · quest-complete overlay · pause overlay · error sheet · connection-loss overlay · update-required · daily reward · offer reveal · item comparison overlay.
**Анимации входа/выхода (11):** ⭐ spring from source (попап растёт из кнопки) · scale+fade · curtain reveal (Wipe) · mask expansion · blur depth · glass morph · fold · elastic sheet · liquid edge · particle dissolve · stacked modal depth.

**Phaser 4:** фон-«вьюпорт» = масштаб контейнера игры + Blur + dim (классический stacked depth) · spring from source = FLIP от rect кнопки · coach mark = FilterMask с «дыркой» · reward = Choreography-таймлайн (вспышка → лут → одометр → burst).

---

### 12 · MAPS, LEVEL SELECTION & SKILL TREES — 34 паттерна

**Карты (12):** ⭐ scrollable world map с pinch-to-zoom · ⭐ fog of war reveal · parallax map layers · route drawing · animated/pulsing markers · location cluster expansion · map-to-level transition · mini-map expansion · compass · floor selector.
**Level selection (10):** ⭐ node path (тропа из узлов) · planet system · island map · tower floors · chapter book · door/portal selection · arena carousel · unlock chain · completed level transformation · secret level reveal.
**Skill trees (12):** ⭐ branching tree с animated connection lines · radial skill tree · constellation · hex grid · orbit system · zoomable infinite canvas · ⭐ node hold-to-unlock · dependency highlighting · upgrade preview · skill reset animation · multiple build comparison.

**Phaser 4:** camera bounds + two-pointer pinch (дистанция между pointers → zoom) · fog = FilterMask с динамическим стиранием через DynamicTexture · линии-связи = DrawLine/StrokePath render nodes + прогресс-анимация · hold-to-unlock = arc-fill + shake на провале.

---

### 13 · MOBILE GAME CONTROLS — 27 паттернов

⭐ floating joystick (появляется под пальцем) · ⭐ dynamic joystick · ⭐ swipe-to-aim с индикатором · ⭐ radial ability menu · ⭐ pinch zoom + two-finger camera rotate · fixed joystick · elastic joystick · dual-stick · drag-to-aim · aim cone · hold-and-release ability · charge direction indicator · gesture spell drawing · path drawing · tap target selection · drag unit placement · context action button · adaptive action cluster · combo input display · rhythm tap zone · steering wheel · throttle slider · flight joystick · one-handed arc controls · quick item wheel · touch region visualization · rebindable layout.

**Панель каждого демо:** dead zone · threshold · hysteresis · visual feedback · возврат · отмена · режим левши · увеличенный touch target · Reduce Motion.
**Phaser 4:** multi-pointer (`pointer1/pointer2`), clamp-радиус + dead zone математика, debug-оверлей зон на Graphics, mirror-функция раскладки для левши.

---

### 14 · SPECIAL INTERACTIVE ELEMENTS — 30 паттернов

⭐ scratch-to-reveal (стирание монеткой) · ⭐ spin wheel (инерция + тики + приз) · ⭐ card pack opening (rarity-ригуал) · ⭐ chest opening (антиципация → взрыв) · ⭐ safe dial / combination lock · peel sticker · tear-open package · slot machine · dice throw · rune tracing · shape matching · drag cable to socket · liquid transfer · pouring control · balance scale · physics toggle · elastic rope selector · fold/unfold map · book page turning · holographic scanner · radar sweep · fingerprint hold · energy reactor · orbital selector · mechanical lever · pull cord · spring latch · crank control · puzzle-like menu unlock.

**Phaser 4:** scratch = DynamicTexture + стирание маски «кистью» по движению пальца · wheel = угловая инерция + тик-фидбек (scale-pulse) · pack opening = Choreography: glow (Bloom нарастает) → тряска → burst частиц → rarity-цвет → reveal · crank = непрерывный rotation-drag с hysteresis.

---

### 15 · UI EFFECTS LAB — 51 модификатор

Это **не галерея трюков, а библиотека модификаторов**, применяемых к элементам разделов 2–14.

**Материалы (16):** ⭐ liquid glass (blur+blend+подсветка кромки) · ⭐ holographic foil (Shine + GradientMap) · ⭐ neon (Glow + Blend) · frosted glass · plasma · gel · metal (ColorMatrix-град) · paper · fabric · crystal · ice · fire · smoke (Noise) · ink · pixel (Pixelate/Quantize) · glitch.
**Reveal (14):** ⭐ Wipe-семейство (radial/directional/curtain/blinds) · liquid wipe · dissolve (Noise-маска) · particles assembling · blur-to-focus · pixelation · scan line · shard assembly · ink spread · glow trace · outline-to-fill.
**Деформации (12):** ⭐ squash & stretch · ⭐ wobble/jelly (spring-цепочка вершин) · ripple · wave · bend · fold · twist · elastic edge · blob morph · soft-body response.
**Глубина (9):** perspective · tilt · layered blur · dynamic shadow · reflection · specular highlight · foreground occlusion · atmospheric particles · ImageLight-освещение.

**Правило лаборатории:** каждый модификатор = пресет (вход: любой объект, параметры: intensity/speed/scale), с таблицей стоимости по FPS.

---

### 16 · PERFORMANCE & ACCESSIBILITY — 12 инструментов

Финальный босс: award не дают тормозящему визуалу.

| Инструмент | Содержание |
|---|---|
| ⭐ **FX-бюджет** | Таблица «фильтр → цена в кадрах» на low/mid/high девайсах; правила стекирования фильтров |
| ⭐ **60 FPS протокол** | Профилирование RenderNodes, батч-дисциплина (атласы), лимиты частиц, SpriteGPULayer для массовых сцен |
| ⭐ **Reduce Motion** | Полная параллельная ветка анимаций: что упрощаем, что оставляем |
| ⭐ **A11y-аудит UI** | Тап-таргеты ≥60dp, контраст в солнечный день, safe areas, режим левши, mute-safe фидбек |
| Батарея/термика | Тест 30 минут: троттлинг-детектор, график FPS/температуры |
| Текстурная память | Атлас-планировщик, DynamicTexture переиспользование, CaptureFrame-лимиты |
| Пулинг | Переиспользование объектов списков/частиц — ноль аллокаций в кадре |
| Чек-лист лоу-энда | Протокол теста на Android Go-классе |

---

## 🥇 ЗОЛОТАЯ ДОРОЖКА (метод 80/20)

Маршрут из ⭐76 паттернов, выстроенный по зависимости навыков:

```
Motion Foundations (3)
  → Buttons (4) → HUD core (6) → Modals (5)
  → Menus (6) → Lists (4) → Carousels & Cards (6)
  → Scroll (5) → Parallax (4) → Sliders (5)
  → Inventory (4) → Maps & Trees (5) → Controls (5)
  → Special (5) → Effects Lab (5) → Perf & A11y (4)
```

Прошедший Золотую дорожку получает «скилл-три» из трёх веток: **Feel** (кнопки, HUD, моушн), **Flow** (навигация, скролл, карусели), **Wow** (параллакс, эффекты, спецэлементы) — и умеет собрать интерфейс, который жюри крутит второй раз.

---

## ⚙️ ТЕХПЛАН СБОРКИ

1. **Ядро:** единый HTML-шелл каталога + Phaser 4 (bundled inline — превью работает офлайн), тёмная тема, поиск, прогресс
2. **Фреймворк демо:** общие классы `SpringIntegrator`, `ScrollController`, `Choreography`, `FXPreset`, панель параметров, Reduce Motion / левша-тумблеры
3. **Наполнение:** Золотая дорожка ⭐ первыми (76 демо), затем полная библиотека по разделам
4. **Полировка:** FPS-счётчик в каждом демо (демонстрация раздела 16), чек-листы качества

---

## 🚀 СЛЕДУЮЩИЙ ШАГ

Собираю каркас каталога и начинаю с **Раздела 1 (Motion Foundations)** + первых ⭐-демо кнопок — это фундамент, на который лягут остальные 15 разделов. Дальше итерациями по разделам.
