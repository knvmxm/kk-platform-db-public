# kk-platform-db-public
## KK Platform Databases (Public)

Публичные справочники и словари для моделирования, создания калькуляторов и логистических инструментов от Конов Консалтинг (Konov Consulting).

Этот репозиторий создан для централизованного хранения актуальных нормативных и справочных данных (ОКЕИ, Типы транспорта, типы складских процессов и операций, ставки НДС, коды, курсы и т.д.). Веб-приложения платформы KK Platform обращаются к этим файлам напрямую, что позволяет обновлять справочники без необходимости переписывать или переопубликовывать сам код программного обеспечения.

---

## Структура данных

Все файлы хранятся в формате `.json`. Каждый файл имеет строгую структуру, включающую служебный блок `_meta` (метаданные) и массив `data` (сами данные). 

Сами данные в массиве `data` сгруппированы по категориям для удобства фильтрации и вывода в интерфейсах.

**Пример формата файла:**

```json
{
  "_meta": {    
    "platform": "© KK Platform",    
    "partition": "Dictionaries",    
    "copyright": "© 2025 Конов Консалтинг (Konov Consulting). Все права защищены.",    
    "type": "Справочник",
    "name": "Справочник Единиц используемых в логистике",
    "file_name": "units-logistics.json",
    "code": "units-logistics",
    "version": "1.0.0",
    "github": "https://github.com/knvmxm/kk-platform-db-public",
    "github_category": "dict",
    "create_date": "2026-06-15",
    "last_updated": "2026-06-15"  
  },  
  "data": [
    {
      "category": "Масса и вес",
      "items": [
        { "code": "166", "name": "Килограмм", "symbol_national": "кг", "symbol_international": "kg", "code_national": "КГ", "code_international": "KGM" },
        { "code": "168", "name": "Тонна; метрическая тонна (1000 кг)", "symbol_national": "т", "symbol_international": "t", "code_national": "Т", "code_international": "TNE" }
      ]
    },
    {
      "category": "Линейные размеры и расстояния",
      "items": [
        { "code": "003", "name": "Миллиметр", "symbol_national": "мм", "symbol_international": "mm", "code_national": "ММ", "code_international": "MMT" },
        { "code": "006", "name": "Метр", "symbol_national": "м", "symbol_international": "m", "code_national": "М", "code_international": "MTR" }
      ]
    }
  ]
}
```

---

## Текущий список справочников

* `kk-platform-dict-units-okei.json` - Общероссийский классификатор единиц измерения (ОКЕИ)
* `kk-platform-dict-units-logitics.json` - Единицы измерения применяемые в логистике (в том числе единицы входящие в ОКЕИ)
* `kk-platform-dict-units-wms.json` - Единицы измерения необходимые для работы WMS (Warehouse Management System) (в том числе единицы входящие в ОКЕИ)
* `kk-platform-dict-units-tms.json` - Единицы измерения необходимые для работы TMS (Transport Management System) (в том числе единицы входящие в ОКЕИ)
* `kk-platform-dict-units-yms.json` - Единицы измерения необходимые для работы YMS (Yard Management System) (в том числе единицы входящие в ОКЕИ)

---

## Как использовать (Для разработчиков)

Поскольку репозиторий публичный, вы можете получать данные напрямую через `fetch` или `XMLHttpRequest` по прямой ссылке `raw.githubusercontent.com/knvmxm/kk-platform-db-public/main/[file_name].json`

**Пример на JavaScript:**

```javascript
async function getLogisticsUnits() {
    const url = 'https://raw.githubusercontent.com/knvmxm/kk-platform-db-public/main/kk-platform-dict-units-logitics.json';
    
    try {
        const response = await fetch(url + '?t=' + Date.now()); // ?t= для защиты от кэширования
        if (!response.ok) throw new Error('Network response was not ok');
        
        const json = await response.json();
        
        // 1. Проверяем метаданные
        console.log(`Загружен: ${json._meta.name} (версия ${json._meta.version})`);
        console.log(`Файл: ${json._meta.file_name}, дата обновления: ${json._meta.last_updated}`);
        
        // 2. Работаем с категориями и данными
        json.data.forEach(categoryBlock => {
            console.log(`\n--- Категория: ${categoryBlock.category} ---`);
            
            categoryBlock.items.forEach(item => {
                console.log(`[${item.code}] ${item.name} (${item.symbol_national})`);
            });
        });
        
    } catch (error) {
        console.error('Ошибка загрузки справочника:', error);
    }
}
```

---

## Лицензия и права

© 2025 Конов Консалтинг (Konov Consulting). Все права защищены.

Данные в данном репозитории предоставляются на основе официальных открытых источников. Скрипты-обертки и структура метаданных (`_meta`) являются интеллектуальной собственностью Конов Консалтинг (Konov Consulting).

* **Разрешено:** Использование данных для личных проектов и интеграции с открытыми системами со ссылкой на источник.
* **Запрещено:** Коммерческая перепродажа баз данных как самостоятельного продукта без согласования с правообладателем.

---

## Контакты и обратная связь

* **Сайт:** [https://konov.consulting](https://konov.consulting)
* **Email:** [post@mkonov.ru](mailto:post@mkonov.ru), [konov.com@yandex.ru](mailto:konov.com@yandex.ru)

По вопросам сотрудничества, неточности и / или корректировки данных обязательно пишите.

---

### Get Enjoy. Конов Консалтинг (Konov Consulting)
```