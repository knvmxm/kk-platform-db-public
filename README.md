# kk-platform-db-public
KK Platform-DB (Public)
Публичные справочники и словари для моделирования, создания калькуляторов и логистических инструментов от Конов Консалтинг (Konov Consulting).

Этот репозиторий создан для централизованного хранения актуальных нормативных и справочных данных (ОКЕИ, Типы транспорта, типы складских процессов и операций, ставки НДС, коды, курсы и т.д.). Веб-приложения платформы KK Platform обращаются к этим файлам напрямую, что позволяет обновлять справочники без необходимости переписывать или переопубликовывать сам код программного обеспечения.

-- Структура данных
Все файлы хранятся в формате .json. Каждый файл имеет строгую структуру, включающую служебный блок _meta (метаданные) и массив data (сами данные).

-- Пример формата файла:

[
    {  
    "_meta": {    
        "platform": "© KK Platform",
        "part": "DB", 
        "partition": "Dictionaries",    
        "copyright": "© 2025 Конов Консалтинг (Konov Consulting). Все права защищены.",    
        "type": "Справочник",
        "name": "Справочник Единиц по ОКЕИ",
        "file_name": "units-okei.json",
        "code": "units-okei",
        "version": "1.0.0",
        "github": "https://github.com/knvmxm/kk-platform-db-public",
        "github_direcroty": "dict",
        "create_date": "2026-06-15",
        "last_updated": "2026-06-15"  
    },  
    
        "data": [    
            { "code": "166", "name": "Килограмм", "symbol": "кг" }  
        ]
    }
]

-- Текущий список справочников:
--- kk-platform-dict-units-okei.json - Общероссийский классификатор единиц измерения (ОКЕИ)
--- kk-platform-dict-units-logitics.json - Единицы измерения применяемые в логистике (в том числе единицы входящие в ОКЕИ)
--- kk-platform-dict-units-wms.json - Единицы измерения необходимые для работы WMS (Warehouse Management System) (в том числе единицы входящие в ОКЕИ)
--- kk-platform-dict-units-tms.json - Единицы измерения необходимые для работы TMS (Transport Management System) (в том числе единицы входящие в ОКЕИ)
--- kk-platform-dict-units-yms.json - Единицы измерения необходимые для работы YMS (Yard Management System) (в том числе единицы входящие в ОКЕИ)

-- Как использовать (Для разработчиков)
Поскольку репозиторий публичный, вы можете получать данные напрямую через fetch или XMLHttpRequest по прямой ссылке raw.githubusercontent.com/knvmxm/kk-platform-db-public/main/[file_name].json

-- Пример на JavaScript:

async function getOKEI() {
    const url = 'https://raw.githubusercontent.com/knvmxm/kk-platform-db-public/main/kk-platform-dict-units-okei.json';
    
    try {
        const response = await fetch(url + '?t=' + Date.now()); // ?t= для защиты от кэширования
        if (!response.ok) throw new Error('Network response was not ok');
        
        const json = await response.json();
        
        // Проверяем метаданные
        console.log(`Загружен: ${json._meta.name} (версия ${json._meta.version})`);
        
        // Работаем с данными
        json.data.forEach(item => {
            console.log(`${item.code} - ${item.name}`);
        });
        
    } catch (error) {
        console.error('Ошибка загрузки справочника:', error);
    }
}

-- Лицензия и права
© 2025 Конов Консалтинг (Konov Consulting). Все права защищены.

Данные в данном репозитории предоставляются на основе официальных открытых источников. Скрипты-обертки и структура метаданных (_meta) являются интеллектуальной собственностью Конов Консалтинг (Konov Consulting).

Разрешено: Использование данных для личных проектов и интеграции с открытыми системами со ссылкой на источник.
Запрещено: Коммерческая перепродажа баз данных как самостоятельного продукта без согласования с правообладателем.

-- Контакты
Сайт: https://konov.consulting
Email: post@mkonov.ru, konov.com@yandex.ru

-- Обратная связь
По вопросам сотрудничества, неточности и / или корректировки данных обязательно пишите.

### Get Enjoy. Конов Консалтинг (Konov Consulting)