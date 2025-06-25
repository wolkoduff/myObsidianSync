
Синхронизация заметок в обсидиане с компом и телефоном

https://habr.com/ru/articles/843288/ - добить на планшет синхронизацию
[Ноутбук HP TPN-C126 / Попросили добавить оперативную память! - смотреть видео онлайн от «Чистка с безупречным блеском» в хорошем качестве, опубликованное 18 ноября 2023 года в 11:55:09.](https://rutube.ru/video/a8b0446b35652519ab062ace7f49666c/?&utm_source=embed&utm_medium=referral&utm_campaign=logo&utm_content=a8b0446b35652519ab062ace7f49666c&utm_term=yastatic.net%2F&referrer=appmetrica_tracking_id%3D1037600761300671389%26ym_tracking_id%3D14652293992110778507)

```mermaid
flowchart TB
    start_sequence((s57c1 = 1)) --> ustupka[Уступка]
    ustupka --> address[Изменение адреса]
    address --> date[Дата НОУ]
    date --> changeArea{Среда меняется?}
    changeArea -->|Нет| changeTerr{Изменение связано с территорией}
    changeArea -->|Да| newArea[Новая среда вещания]
    newArea -->|Спутник| changeTerr{Изменение связано с территорией}
    newArea -->|Эфирка| nev{Какой вид эфирного вещания}
    newArea -->|Кабель/Универсалка чистая| changeTerr{Изменение связано с территорией}
    nev --> |Аналоговая| analog{Есть конкурсные города?}
    nev --> |Цифровая| changeTerr{Изменение связано с территорией}
    analog --> changeTerr{Изменение связано с территорией и частотами?}
    changeTerr --> get_bread
    get_bread -->   do_i_peanut_butter
    do_i_peanut_butter -->|No| get_peanut_butter{Get Peanut Butter}
    do_i_peanut_butter -->|Yes| assemble{Assemble Sandwich}
    get_peanut_butter --> assemble{Assemble Sandwich}
    assemble --> end_sequence((END))
```

Протестировать разные ветки, сверить посещение экранов


```mermaid
flowchart TB
    start_sequence((s57c1 = 1)) --> concept[Изменение связано с ПН/КВ и наименованием канала]
    concept --> |ПН/КВ и наименование канала|changeSmiVolume{Изменение ПН/КВ подразумевает изменение объёмов СМИ?}
    concept --> |Только наименование канала|next[Следующий экран]
    concept --> |Только ПН/КВ|changeSmiVolume{Изменение ПН/КВ подразумевает изменение объёмов СМИ?}
    concept --> |Нет|next[Следующий экран]
    changeSmiVolume --> |Да|changeSmi{Изменение связано с добавлением или исключением СМИ?}
    changeSmiVolume --> |Нет|next[Следующий экран]
```