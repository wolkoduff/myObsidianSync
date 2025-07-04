# Обращение и работа с RestCall
## Для чего он нужен и как с ним работать
Нужен этот компонент, когда хотите не загружать весь справочник на форму, а вызвать справочник с ЕСНСИ и проверить полученные с него результаты с каким-либо значением. Например, не пускать получать услугу, если стоит ограничение на получателей, конкретный список ОГРН-ок, на стартовом экране же никак не проверить, да и загружать справочник в выпадающий список до экрана решения без уточняющих вопросов нельзя. Да и не нужно в целом, поскольку данный компонент поможет справиться с такой задачей
Далее будет расписан подобно пример по справочнику Participant_Legal_Entity
![[Pasted image 20250610225000.png]]
Записей в этом справочнике 7, мы рассмотрим одну из них
![[Pasted image 20250610224844.png]]
Как мы видим, у справочника есть запись с ОГРН ***1065009017534***
Как мы можем проверить, есть ли заявитель в справочнике ЕСНСИ для дальнейшего получения услуги?
> [!NOTE] Примечание автора
Есть два путя, как я говорил ранее:
>- Получить список через restCall-запрос и по полученному ответу проверить наличие там записи через ОГРН организации
>- Получить список через restCall-запрос и применить уже к полученным значениям фильтрацию по ОГРН организации

----
Если получаем список сразу же так, как есть, т.е. прописываем справочник, который будет вызываться и получаться по нему ответ
![[Pasted image 20250610225414.png]]
Если мы вызываем справочник через фильтрацию уже в запросе
![[Pasted image 20250610225247.png]]
Дальше заполняем только linkedValues значение
![[Pasted image 20250610225334.png]]

----
### Чем отличаются два подхода?
Да по большей части незначительно в рамках конфигурации самого компонента, а вот в правилах переходов будут иметь значительную разницу, о чём опишу далее
Что вернёт вызов без фильтрации? А вернёт весь список как есть (на момент поиска ответа в справочнике было 5 записей, скриншоты делались когда в справочнике уже 7 записей)
```json
{
    "error": {
        "code": 0,
        "message": "operation completed"
    },
    "fieldErrors": [],
    "total": 5,
    "items": [
        {
            "value": "5",
            "title": "АО \"Евросиб СПБ-ТС\"",
            "isLeaf": true,
            "children": [],
            "attributes": [
                {
                    "name": "code",
                    "type": "LONG",
                    "value": {
                        "asLong": 5,
                        "typeOfValue": "LONG",
                        "value": 5
                    },
                    "valueAsOfType": 5
                },
                {
                    "name": "Organization_name",
                    "type": "STRING",
                    "value": {
                        "asString": "АО \"Евросиб СПБ-ТС\"",
                        "typeOfValue": "STRING",
                        "value": "АО \"Евросиб СПБ-ТС\""
                    },
                    "valueAsOfType": "АО \"Евросиб СПБ-ТС\""
                },
                {
                    "name": "OGRN",
                    "type": "STRING",
                    "value": {
                        "asString": "1027806887206",
                        "typeOfValue": "STRING",
                        "value": "1027806887206"
                    },
                    "valueAsOfType": "1027806887206"
                },
                {
                    "name": "INN",
                    "type": "STRING",
                    "value": {
                        "asString": "7813151859",
                        "typeOfValue": "STRING",
                        "value": "7813151859"
                    },
                    "valueAsOfType": "7813151859"
                },
                {
                    "name": "OKPO",
                    "type": "STRING",
                    "value": {
                        "asString": "56306709",
                        "typeOfValue": "STRING",
                        "value": "56306709"
                    },
                    "valueAsOfType": "56306709"
                },
                {
                    "name": "KPP",
                    "type": "STRING",
                    "value": {
                        "asString": "781301001",
                        "typeOfValue": "STRING",
                        "value": "781301001"
                    },
                    "valueAsOfType": "781301001"
                },
                {
                    "name": "Legal_address",
                    "type": "STRING",
                    "value": {
                        "asString": "197046, город Санкт-Петербург, Мичуринская ул, д. 4 литера А, помещ. 14-н кабинет 65",
                        "typeOfValue": "STRING",
                        "value": "197046, город Санкт-Петербург, Мичуринская ул, д. 4 литера А, помещ. 14-н кабинет 65"
                    },
                    "valueAsOfType": "197046, город Санкт-Петербург, Мичуринская ул, д. 4 литера А, помещ. 14-н кабинет 65"
                },
                {
                    "name": "Participant_EPGU_experiment",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                },
                {
                    "name": "Transporter",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                }
            ],
            "attributeValues": {
                "OGRN": "1027806887206",
                "code": 5,
                "Legal_address": "197046, город Санкт-Петербург, Мичуринская ул, д. 4 литера А, помещ. 14-н кабинет 65",
                "Participant_EPGU_experiment": true,
                "Organization_name": "АО \"Евросиб СПБ-ТС\"",
                "INN": "7813151859",
                "KPP": "781301001",
                "Transporter": true,
                "OKPO": "56306709"
            }
        },
        {
            "value": "2",
            "title": "ЗАО \"Рустранс-спедишн\"",
            "isLeaf": true,
            "children": [],
            "attributes": [
                {
                    "name": "code",
                    "type": "LONG",
                    "value": {
                        "asLong": 2,
                        "typeOfValue": "LONG",
                        "value": 2
                    },
                    "valueAsOfType": 2
                },
                {
                    "name": "Organization_name",
                    "type": "STRING",
                    "value": {
                        "asString": "ЗАО \"Рустранс-спедишн\"",
                        "typeOfValue": "STRING",
                        "value": "ЗАО \"Рустранс-спедишн\""
                    },
                    "valueAsOfType": "ЗАО \"Рустранс-спедишн\""
                },
                {
                    "name": "OGRN",
                    "type": "STRING",
                    "value": {
                        "asString": "1037739971543",
                        "typeOfValue": "STRING",
                        "value": "1037739971543"
                    },
                    "valueAsOfType": "1037739971543"
                },
                {
                    "name": "INN",
                    "type": "STRING",
                    "value": {
                        "asString": "7729500163",
                        "typeOfValue": "STRING",
                        "value": "7729500163"
                    },
                    "valueAsOfType": "7729500163"
                },
                {
                    "name": "OKPO",
                    "type": "STRING",
                    "value": {
                        "asString": "71619022",
                        "typeOfValue": "STRING",
                        "value": "71619022"
                    },
                    "valueAsOfType": "71619022"
                },
                {
                    "name": "KPP",
                    "type": "STRING",
                    "value": {
                        "asString": "772901001",
                        "typeOfValue": "STRING",
                        "value": "772901001"
                    },
                    "valueAsOfType": "772901001"
                },
                {
                    "name": "Legal_address",
                    "type": "STRING",
                    "value": {
                        "asString": "119361, Россия, г. Москва, ул. Марии Поливановой, д. 9, каб. 24",
                        "typeOfValue": "STRING",
                        "value": "119361, Россия, г. Москва, ул. Марии Поливановой, д. 9, каб. 24"
                    },
                    "valueAsOfType": "119361, Россия, г. Москва, ул. Марии Поливановой, д. 9, каб. 24"
                },
                {
                    "name": "Participant_EPGU_experiment",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                },
                {
                    "name": "Transporter",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                }
            ],
            "attributeValues": {
                "OGRN": "1037739971543",
                "code": 2,
                "Legal_address": "119361, Россия, г. Москва, ул. Марии Поливановой, д. 9, каб. 24",
                "Participant_EPGU_experiment": true,
                "Organization_name": "ЗАО \"Рустранс-спедишн\"",
                "INN": "7729500163",
                "KPP": "772901001",
                "Transporter": true,
                "OKPO": "71619022"
            }
        },
        {
            "value": "6",
            "title": "ООО \"Делотех\"",
            "isLeaf": true,
            "children": [],
            "attributes": [
                {
                    "name": "code",
                    "type": "LONG",
                    "value": {
                        "asLong": 6,
                        "typeOfValue": "LONG",
                        "value": 6
                    },
                    "valueAsOfType": 6
                },
                {
                    "name": "Organization_name",
                    "type": "STRING",
                    "value": {
                        "asString": "ООО \"Делотех\"",
                        "typeOfValue": "STRING",
                        "value": "ООО \"Делотех\""
                    },
                    "valueAsOfType": "ООО \"Делотех\""
                },
                {
                    "name": "OGRN",
                    "type": "STRING",
                    "value": {
                        "asString": "1227700010680",
                        "typeOfValue": "STRING",
                        "value": "1227700010680"
                    },
                    "valueAsOfType": "1227700010680"
                },
                {
                    "name": "INN",
                    "type": "STRING",
                    "value": {
                        "asString": "9725071534",
                        "typeOfValue": "STRING",
                        "value": "9725071534"
                    },
                    "valueAsOfType": "9725071534"
                },
                {
                    "name": "OKPO",
                    "type": "STRING",
                    "value": {
                        "asString": "48142867",
                        "typeOfValue": "STRING",
                        "value": "48142867"
                    },
                    "valueAsOfType": "48142867"
                },
                {
                    "name": "KPP",
                    "type": "STRING",
                    "value": {
                        "asString": "770601001",
                        "typeOfValue": "STRING",
                        "value": "770601001"
                    },
                    "valueAsOfType": "770601001"
                },
                {
                    "name": "Legal_address",
                    "type": "STRING",
                    "value": {
                        "asString": "119049, город Москва, вн.тер.г. муниципальный округ Якиманка, ул. Донская, д. 15, помещение 1, ком. 7 (офис 605)",
                        "typeOfValue": "STRING",
                        "value": "119049, город Москва, вн.тер.г. муниципальный округ Якиманка, ул. Донская, д. 15, помещение 1, ком. 7 (офис 605)"
                    },
                    "valueAsOfType": "119049, город Москва, вн.тер.г. муниципальный округ Якиманка, ул. Донская, д. 15, помещение 1, ком. 7 (офис 605)"
                },
                {
                    "name": "Participant_EPGU_experiment",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                },
                {
                    "name": "Transporter",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                }
            ],
            "attributeValues": {
                "OGRN": "1227700010680",
                "code": 6,
                "Legal_address": "119049, город Москва, вн.тер.г. муниципальный округ Якиманка, ул. Донская, д. 15, помещение 1, ком. 7 (офис 605)",
                "Participant_EPGU_experiment": true,
                "Organization_name": "ООО \"Делотех\"",
                "INN": "9725071534",
                "KPP": "770601001",
                "Transporter": true,
                "OKPO": "48142867"
            }
        },
        {
            "value": "3",
            "title": "ООО \"Рускон\"",
            "isLeaf": true,
            "children": [],
            "attributes": [
                {
                    "name": "code",
                    "type": "LONG",
                    "value": {
                        "asLong": 3,
                        "typeOfValue": "LONG",
                        "value": 3
                    },
                    "valueAsOfType": 3
                },
                {
                    "name": "Organization_name",
                    "type": "STRING",
                    "value": {
                        "asString": "ООО \"Рускон\"",
                        "typeOfValue": "STRING",
                        "value": "ООО \"Рускон\""
                    },
                    "valueAsOfType": "ООО \"Рускон\""
                },
                {
                    "name": "OGRN",
                    "type": "STRING",
                    "value": {
                        "asString": "1022302380044",
                        "typeOfValue": "STRING",
                        "value": "1022302380044"
                    },
                    "valueAsOfType": "1022302380044"
                },
                {
                    "name": "INN",
                    "type": "STRING",
                    "value": {
                        "asString": "2315094729",
                        "typeOfValue": "STRING",
                        "value": "2315094729"
                    },
                    "valueAsOfType": "2315094729"
                },
                {
                    "name": "OKPO",
                    "type": "STRING",
                    "value": {
                        "asString": "26394769",
                        "typeOfValue": "STRING",
                        "value": "26394769"
                    },
                    "valueAsOfType": "26394769"
                },
                {
                    "name": "KPP",
                    "type": "STRING",
                    "value": {
                        "asString": "231501001",
                        "typeOfValue": "STRING",
                        "value": "231501001"
                    },
                    "valueAsOfType": "231501001"
                },
                {
                    "name": "Legal_address",
                    "type": "STRING",
                    "value": {
                        "asString": "353960, Краснодарский край, город Новороссийск, село Кирилловка, Ж/д петля 2-я ул.",
                        "typeOfValue": "STRING",
                        "value": "353960, Краснодарский край, город Новороссийск, село Кирилловка, Ж/д петля 2-я ул."
                    },
                    "valueAsOfType": "353960, Краснодарский край, город Новороссийск, село Кирилловка, Ж/д петля 2-я ул."
                },
                {
                    "name": "Participant_EPGU_experiment",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                },
                {
                    "name": "Transporter",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                }
            ],
            "attributeValues": {
                "OGRN": "1022302380044",
                "code": 3,
                "Legal_address": "353960, Краснодарский край, город Новороссийск, село Кирилловка, Ж/д петля 2-я ул.",
                "Participant_EPGU_experiment": true,
                "Organization_name": "ООО \"Рускон\"",
                "INN": "2315094729",
                "KPP": "231501001",
                "Transporter": true,
                "OKPO": "26394769"
            }
        },
        {
            "value": "4",
            "title": "ООО \"С 7 Карго\"",
            "isLeaf": true,
            "children": [],
            "attributes": [
                {
                    "name": "code",
                    "type": "LONG",
                    "value": {
                        "asLong": 4,
                        "typeOfValue": "LONG",
                        "value": 4
                    },
                    "valueAsOfType": 4
                },
                {
                    "name": "Organization_name",
                    "type": "STRING",
                    "value": {
                        "asString": "ООО \"С 7 Карго\"",
                        "typeOfValue": "STRING",
                        "value": "ООО \"С 7 Карго\""
                    },
                    "valueAsOfType": "ООО \"С 7 Карго\""
                },
                {
                    "name": "OGRN",
                    "type": "STRING",
                    "value": {
                        "asString": "1065009017534",
                        "typeOfValue": "STRING",
                        "value": "1065009017534"
                    },
                    "valueAsOfType": "1065009017534"
                },
                {
                    "name": "INN",
                    "type": "STRING",
                    "value": {
                        "asString": "5009053292",
                        "typeOfValue": "STRING",
                        "value": "5009053292"
                    },
                    "valueAsOfType": "5009053292"
                },
                {
                    "name": "OKPO",
                    "type": "STRING",
                    "value": {
                        "asString": "93733209",
                        "typeOfValue": "STRING",
                        "value": "93733209"
                    },
                    "valueAsOfType": "93733209"
                },
                {
                    "name": "KPP",
                    "type": "STRING",
                    "value": {
                        "asString": "500901001",
                        "typeOfValue": "STRING",
                        "value": "500901001"
                    },
                    "valueAsOfType": "500901001"
                },
                {
                    "name": "Legal_address",
                    "type": "STRING",
                    "value": {
                        "asString": "142007, Московская область, тер Аэропорт Домодедово, стр. 8, этаж 4/кабинет 4.17",
                        "typeOfValue": "STRING",
                        "value": "142007, Московская область, тер Аэропорт Домодедово, стр. 8, этаж 4/кабинет 4.17"
                    },
                    "valueAsOfType": "142007, Московская область, тер Аэропорт Домодедово, стр. 8, этаж 4/кабинет 4.17"
                },
                {
                    "name": "Participant_EPGU_experiment",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                },
                {
                    "name": "Transporter",
                    "type": "BOOLEAN",
                    "value": {
                        "asString": "true",
                        "asBoolean": true,
                        "typeOfValue": "BOOLEAN",
                        "value": true
                    },
                    "valueAsOfType": true
                }
            ],
            "attributeValues": {
                "OGRN": "1065009017534",
                "code": 4,
                "Legal_address": "142007, Московская область, тер Аэропорт Домодедово, стр. 8, этаж 4/кабинет 4.17",
                "Participant_EPGU_experiment": true,
                "Organization_name": "ООО \"С 7 Карго\"",
                "INN": "5009053292",
                "KPP": "500901001",
                "Transporter": true,
                "OKPO": "93733209"
            }
        }
    ],
    "status": 200
}
```
----
И вот как мы видим, есть **много атрибутов** у ответа с компонента:
* *error* (сложный атрибут, у которого 2 свойства - code и message)
* *fieldsErrors* (массив)
* *total* (простой атрибут)
* *items* (массив)
* *status* (простой атрибут)

Некоторые атрибуты `сложные`, какие-то являются `массивами (items, fieldErrors)`, которые желательно перебирать через циклы, ну или через *anyMatch*, *noneMatch* или *allMatch* (это методы коллекций, которыми и являются массивы).
> [!IMPORTANT]
> ### В чём разница между простыми и сложными? 
В простых answer.componentId.value - для простых, а вот для сложных надо уточнять, какое значение брать, т.е. answer.componentId.value.id (text,code,title и т.д.).

Итак, немного отвлеклись, продолжим:
> [!NOTE]
Надо проверять полученные значения, можно пойти двумя путями:
* добавить экран типа redirect (для логики, когда заявитель ничего не видит, но происходит магия-магия-магия)
* прописать всё в правиле перехода, заморочиться с условиями
На первый взгляд может показаться, что прописать всё в правиле перехода будет очень просто, и это будет так, отчасти, если уверены в том, что правильно пропишете правило перехода. Помним, что нас интересует атрибут items с нашего ответа restCall-компонента, а это массив, что несколько осложнит нашу задачу, в моём случае, у меня такой компонент c50
![[Pasted image 20250610232804.png]]
Если же пойти через компонент redirect и там добавить компонент `universalLogic`, у которого прописать тип компонента `ValueCalculator`, то можно добиться похожего результата, но в более понятной для программистов форме
```json
{
    "linkedValues": [
        {
            "version": 2,
            "argument": "ogrnValidate",
            "definition": {
                "expression1": "arg2.contains(arg1) ? 'yahoo' : 'fuck'",
                "arg1": "'${protected.orgOgrn}'",
                "arg2": "asList('${c50.items.[*].attributeValues.LegalEntityOGRN}')"
            }
        }
    ]
}
```
Разберём чуть подробнее, что же там такое происходит:
`expression1` - непосредственно выражение для вычисления и всей работы, оно выводится в результат и записывается в переменную `ogrnValidate`
`arg1`, `arg2` - непосредственные аргументы для работы с нашим выражением. 
Что такое `arg1` - запись в переменную arg1 ОГРН организации из личного кабинета
Что такое `arg2` - мы берём содержимое ответа нашего с компонента c50, уточняем, что нас интересует атрибут items, `.[*].` - берём все значения из этого массива, уточняем атрибуты для каждого значения, что нас интересует конкретно `attributeValues`, в котором уже берём атрибут `LegalEntityOGRN`, и оборачиваем эту всю коллекцию в список через метод `asList()`
Как мы вычисляем значение - мы проверяем, есть ли в списке `arg2` значение `arg1`, и если оно есть, тогда возвращаем `yahoo`, во всех остальных случаях `fuck` (можно упростить, оставив только `arg2.contains(arg1)`, тогда ответы будут `'true'` и `'false'`)

> [!IMPORTANT]
Всё это строки, с ними меньше мороки и нервотрёпки

А как же тогда обращаться к вычисленному значению калькулятора? 
Да очень просто:
![[Pasted image 20250610233457.png]]
В скриншоте, как мы видим, проверяется строка и константное значение `'true'`, поскольку правило там такое `arg2.contains(arg1)` - если нашли, значит истина, иначе ложно
А как же быть, если мы сразу применяем фильтр?
В таких случаях всё гораздо проще, мы можем так сильно не заморачиваться и не строить таких воздушных замков, поскольку за нас уже всё сделано, внизу представлен ответ, когда с применением фильтра значение не нашлось
```json
{
    "error": {
        "code": 0,
        "message": "operation completed"
    },
    "fieldErrors": [],
    "total": 0,
    "items": [],
    "status": 200
}
```

> [!IMPORTANT]
> ### На что обращаем внимание:
`items` - пуст, `total` - 0
А значит, наше правило перехода становится гораздо проще:

![[Pasted image 20250610234804.png]]
Это мы рассмотрели случаи, когда запрос restCall значения возвращает, а как быть, если не возвращает?
вот тут уже нам на помощь приходит атрибут `error`
Ниже представлено 2 ответа с разными error.code в response от BackRestCall-запросов (отличие в наличии атрибута `response`)
```json
{
    "statusCode": 200,
    "response": {
        "error": {
            "code": 3,
            "message": "Internal Error"
        },
        "fieldErrors": [],
        "total": 0,
        "items": []
    }
}

{
    "statusCode": 200,
    "response": {
        "error": {
            "code": 7,
            "message": "Entity not found"
        },
        "fieldErrors": [],
        "total": 0,
        "items": []
    }
}
```

> [!IMPORTANT]
Если код 3 - внутренняя ошибка, что-то с витриной не так или что-то на стороне ЕПГУ не работает (абидна, да?)
Если код 7 - записи не найдены (или ~~сучность~~ сущность не нашлась)
Но там и там total также присутствует, а значит правило обращения к total независимо от `error` и его значения `code` нас не волнует
