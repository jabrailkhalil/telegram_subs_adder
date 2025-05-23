# Telegram Member Scraper & Adder 🛠️

**Python CLI**, позволяющий  
1. **собрать (scrape)** участников любого чата/группы, где вы состоите;  
2. **пригласить (add)** этих участников в ваш чат / канал, избегая дубликатов.

---

## 1. Быстрый старт

    # 1 – установите зависимости
    python -m pip install -r requirements.txt      # telethon

    # 2 – задайте секреты (лучше через переменные окружения)
    export TG_API_ID=12345678
    export TG_API_HASH=0123456789abcdef0123456789abcdef
    export TG_PHONE="+15551234567"

    # 3 – первый, одноразовый запуск для получения кода
    python authorization.py        # введите код из Telegram

    # 4 – работаем!
    python auto-add.py

> ⚠️ **Никогда не хардкодьте** `api_id`, `api_hash`, `phone`.  
> Храните их в переменных окружения, `.env`, секретах CI и т.п.

---

## 2. Как это работает

| Опция в `auto-add.py` | Действие |
|-----------------------|----------|
| `1` | **Scrape** – собирает всех участников выбранного чата/мегагруппы и сохраняет в `members-<title>.csv`. |
| `2` | **Add** – берёт последний (или выбранный) `members-*.csv` и приглашает пользователей в ваш чат/канал. Идентификаторы добавленных записываются в `added-<chat_id>.txt`, поэтому при повторных запусках дубликаты пропускаются. |
| `3` | Показать содержимое любого `members-*.csv`. |
| `0` | Шаг назад в любой момент. |
| `q` | Выход из программы. |

`authorization.py` нужен только один раз – создать session-файл (после ввода кода из Telegram). Затем `auto-add.py` использует его автоматически.

---

## 3. Лимиты и советы

* Telegram вводит *Flood-Wait* → скрипт делает паузу **60 сек** между инвайтами (`PAUSE_SEC` в коде).  
* **Каналы** (`broadcast`) не отдают список подписчиков. Скрапить можно **только** чаты/мегагруппы.  
* Чтобы приглашать в канал/группу, вы должны быть **админом** там.  
* Соблюдайте правила Telegram и законы своей страны (только добрые группы можно!).

---

## 4. Кастомизация

* Измените `PAUSE_SEC` в `auto-add.py`, если уверены, что не словите бан.  
* Хотите хранить секреты в `.env`? Добавьте (с помощью `python-dotenv` или аналога):

        TG_API_ID=...
        TG_API_HASH=...
        TG_PHONE=...

* В CI/CD положите эти переменные в секреты пайплайна.

---

## 5. Лицензия

`MIT` — используйте свободно, но автор не несёт ответственности за любые последствия.

---

🤖 *Happy scraping!*
