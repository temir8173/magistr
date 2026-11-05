# Магистерская диссертация: ИИ и БПЛА в животноводстве

**Тема:** Мал шаруашылығында жасанды интеллект және ұшқышсыз ұшу аппараттарын қолдану

Этот репозиторий — рабочее место для практической части диссертации.
Руководитель готовит учебные модули, автор их выполняет и отправляет на проверку.

- План практической части: [practice/PLAN.md](practice/PLAN.md)
- Журнал исследования: [practice/journal.md](practice/journal.md)
- Материалы по диссертации (статья, теория, требования кафедры): [materials/](materials/)

## Модули

| Модуль | Тема | Ноутбук | Ветка |
|---|---|---|---|
| 0–1 | Colab, видеокарта, изображение как числа, первый запуск YOLO, почему готовая модель не видит скот с дрона | [module-01-colab-yolo.ipynb](practice/notebooks/module-01-colab-yolo.ipynb) · [открыть в Colab](https://colab.research.google.com/github/temir8173/magistr/blob/main/practice/notebooks/module-01-colab-yolo.ipynb) | `module-1` |

Для модуля 0–1 понадобятся учебные снимки из [practice/data/samples/](practice/data/samples/).

---

## 1. Установка (Windows, один раз)

WSL и Docker **не нужны**. Нейросети обучаются в Google Colab (в браузере),
на компьютере нужен только лёгкий набор программ.

### 1.1 Git
1. Скачать и установить: https://git-scm.com/download/win
   (все настройки по умолчанию подходят).
2. Открыть **PowerShell** и представиться Git'у:
   ```powershell
   git config --global user.name "Имя Фамилия"
   git config --global user.email "ваша@почта"
   ```

### 1.2 GitHub
1. Завести аккаунт на https://github.com (если нет).
2. Принять приглашение в репозиторий `temir8173/magistr` (придёт на почту).

### 1.3 Python 3.12
1. Скачать с https://www.python.org/downloads/windows/
2. **При установке обязательно поставить галочку «Add python.exe to PATH».**
3. Проверить в новом окне PowerShell:
   ```powershell
   python --version
   ```

### 1.4 VS Code
1. Установить: https://code.visualstudio.com
2. Во вкладке Extensions поставить расширения **Python** и **Jupyter** (от Microsoft).

### 1.5 Скачать проект и установить библиотеки
```powershell
cd ~\Documents
git clone https://github.com/temir8173/magistr.git
cd magistr
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```
Если PowerShell пишет, что выполнение скриптов запрещено, один раз выполнить:
```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```
и повторить активацию.

### 1.6 Google-аккаунт
Нужен для **Google Colab** (бесплатная видеокарта для обучения) и
**Google Drive** (там будут храниться датасеты и обученные модели — они
слишком большие для GitHub).

### 1.7 Claude Code (по желанию)
Помощник-наставник прямо в VS Code или терминале. Нужна подписка Claude.
Установка: https://docs.claude.com/en/docs/claude-code/setup

В проекте есть файл [CLAUDE.md](CLAUDE.md) — в нём правила, по которым Claude
**объясняет и помогает разобраться, но не делает работу за вас**.
Цель — чтобы вы сами понимали каждый шаг и уверенно отвечали на защите.

---

## 2. Как работаем: цикл одного модуля

```
Руководитель выкладывает модуль в main
        ↓
Автор: git pull → новая ветка module-N
        ↓
Автор: ноутбук в Colab → журнал → ответы на вопросы → результаты
        ↓
Автор: commit → push → Pull Request
        ↓
Руководитель: комментарии в PR  →  (если нужно — исправления)
        ↓
Короткий созвон: автор своими словами объясняет, что сделал
        ↓
PR принят → следующий модуль
```

### 2.1 Начать модуль
```powershell
cd ~\Documents\magistr
git checkout main
git pull
git checkout -b module-1
```

### 2.2 Работа с ноутбуком в Colab
- **Открыть:** https://colab.research.google.com → *File → Open notebook* →
  вкладка **GitHub** → поставить галочку *Include private repos* →
  выбрать `temir8173/magistr`, ветку `module-N`, нужный ноутбук.
- **Включить видеокарту:** *Runtime → Change runtime type → T4 GPU*.
- **Сохранить обратно:** *File → Save a copy in GitHub* → тот же репозиторий,
  ветка `module-N`, тот же путь к файлу. После этого на компьютере сделать
  `git pull`.
- Другой вариант: *File → Download → .ipynb* и положить файл в
  `practice/notebooks/` вручную.

### 2.3 Что сдаётся по каждому модулю
| Что | Куда |
|---|---|
| Выполненный ноутбук (с результатами запуска) | `practice/notebooks/` |
| Запись в журнале исследования | `practice/journal.md` |
| Ответы на контрольные вопросы | `practice/answers/module-N.md` (шаблон: `_template.md`) |
| Таблицы, графики, примеры (если есть) | `practice/results/module-N/` |

### 2.4 Отправить на проверку
```powershell
git add .
git commit -m "Модуль N: краткое описание"
git push -u origin module-N
```
Затем на GitHub нажать **Compare & pull request** → создать Pull Request в `main`.

Комментарии руководителя появятся прямо в Pull Request. Исправления —
в той же ветке: `commit` → `push`, PR обновится сам.

---

## 3. Что НЕ кладём в Git

- датасеты и обученные модели (`*.pt`, `*.onnx`) — на Google Drive;
- презентации `*.pptx` — передаём отдельно;
- папку `.venv` и служебные файлы.

Всё это уже прописано в `.gitignore`.

---

## 4. Структура

```
magistr/
  README.md            ← этот файл
  CLAUDE.md            ← правила для Claude-наставника
  requirements.txt     ← Python-библиотеки
  materials/           ← статья, теория, требования кафедры
    requirements/      ← методички и требования кафедры
  practice/
    PLAN.md            ← план практической части
    journal.md         ← журнал исследования (ведёт автор)
    answers/           ← ответы на контрольные вопросы по модулям
    notebooks/         ← ноутбуки Colab
    data/              ← описание данных (сами данные — на Drive)
    results/           ← таблицы, графики, примеры детекций
    app/               ← прототип Streamlit
    economics/         ← экономический расчёт
    chapter/           ← текст главы (рус → каз)
```
