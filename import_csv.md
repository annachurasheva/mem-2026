Отличный выбор — **[Contact List (Personal CRM) — Notion Templates](https://www.notion.so/templates/search?q=contact+list&utm_source=chatgpt.com)** или **[Client List (CRM) — Notion Templates](https://www.notion.so/templates/search?q=client+list+crm&utm_source=chatgpt.com)** действительно удобно адаптировать под вашу задачу.

Я внесла ваши правки:

### Структура базы **Persons**

(имена полей — **латиницей**, для импорта в Notion)

| Поле                  | Тип поля в Notion | Комментарий                                      |
| --------------------- | ----------------- | ------------------------------------------------ |
| `last_name`           | Text              | Фамилия                                          |
| `first_name`          | Text              | Имя                                              |
| `patronymic`          | Text              | Отчество                                         |
| `birth_year`          | Number            | Год рождения                                     |
| `draft_place`         | Text              | Место призыва                                    |
| `military_unit`       | Text              | Воинская часть                                   |
| `date_of_loss`        | Date              | Дата гибели / пропажи                            |
| `source_camo`         | Text              | Фонд / опись / дело                              |
| `burial_relation`     | Relation/Text     | Вероятное братское захоронение                   |
| `reburied`            | Select            | `да / нет / неизвестно`                          |
| `verification_status` | Select            | `v_rabote`, `zapros_otpravlen`, `otvet_poluchen` |
| `confidence_percent`  | Number            | 0–100                                            |
| `scan_link`           | URL               | ссылка на скан                                   |
| `notes`               | Text              | заметки                                          |

---

### CSV-файл (с тестовой записью)

Готово. Скачайте и импортируйте в Notion:

[Скачать CSV шаблон](sandbox:/mnt/data/notion_persons_template.csv)

(кодировка **UTF-8 BOM**, русские буквы откроются корректно в Excel и Notion)

---

# Как активировать шаблон в Notion (ваш регламент)

### Вариант 1: через готовый шаблон

1. Откройте выбранный шаблон:

   * [Contact List template](https://www.notion.so/templates/search?q=contact+list&utm_source=chatgpt.com)
2. Нажмите **Duplicate** (вверху справа).
3. Выберите ваш workspace.
4. Шаблон появится в левой панели.

---

### Вариант 2: импорт моего CSV

После открытия шаблона:

1. Откройте страницу шаблона.
2. Внутри таблицы нажмите **…** → **Merge with CSV**
   *(или New database → Import → CSV)*.
3. Выберите файл `notion_persons_template.csv`.
4. Notion сам создаст поля.

---

### После импорта сразу поправьте типы:

* `birth_year` → **Number**
* `date_of_loss` → **Date**
* `reburied` → **Select**
* `verification_status` → **Select**
* `confidence_percent` → **Number**
* `scan_link` → **URL**

---

### Рекомендую сразу создать 3 View:

1. **В работе** → фильтр `verification_status = v_rabote`
2. **Запросы** → `verification_status = zapros_otpravlen`
3. **Ответы** → `verification_status = otvet_poluchen`

Так будет намного удобнее вести архивный поток.

========
Да — тогда проще дать вам как **CSV-текст**, который вы сохраните вручную.

**Как сохранить:**

1. Откройте **Блокнот** (Windows) или любой текстовый редактор.
2. Вставьте текст ниже целиком.
3. Сохраните как: `notion_persons_template.csv`
4. Кодировка: **UTF-8** (важно)
5. В Notion → **Import → CSV**

```csv
last_name,first_name,patronymic,birth_year,draft_place,military_unit,date_of_loss,source_camo,burial_relation,reburied,verification_status,confidence_percent,scan_link,notes
Иванов,Иван,Иванович,1915,"г. Смоленск","123 сп",1943-08-12,"Ф.58 Оп.18001 Д.123","Братское захоронение №7, Орловская обл.",нет,v_rabote,75,https://example.org/scan123,"Предположительно захоронен как неизвестный"
```

### Пояснение по форматам полей для вашей ручной работы:

* **Текст** → просто вписываете текст
  пример: `Иванов`
* **Дата** → строго `ГГГГ-ММ-ДД`
  пример: `1943-08-12`
* **Число** → без текста
  пример: `75`
* **URL** → полная ссылка
  пример: `https://pamyat-naroda.ru/...`
* **Select (выбор)** → используйте одинаковые значения:

  * `reburied`: `да`, `нет`, `неизвестно`
  * `verification_status`:

    * `v_rabote`
    * `zapros_otpravlen`
    * `otvet_poluchen`

---

Совет: когда импортируете в [Notion](https://www.notion.so/?utm_source=chatgpt.com), сразу переименуйте таблицу в **Persons_DB** — потом будет легче делать связи с таблицами **Burials_DB** и **Scans_DB**.
