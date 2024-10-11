# myObsidianSync
Синхронизация заметок в обсидиане с компом и телефоном

https://habr.com/ru/articles/843288/ - добить на планшет синхронизацию


```mermaid
flowchart TB
    start_sequence((s57c1 = 1)) --> ustupka[Уступка]
    ustupka --> address[Изменение адреса]
    address --> date[Дата НОУ]
    date --> changeArea{Среда меняется?}
    changeArea -->|Нет| changeTerr{Изменение связано с территорией}
    changeArea -->|Да| newArea[Новая среда вещания]
    newArea -->|Спутник| 
    newArea -->|Эфирка|
    newArea -->|Кабель/Универсалка (чистая)|
    get_bread -->   do_i_peanut_butter
    do_i_peanut_butter -->|No| get_peanut_butter{Get Peanut Butter}
    do_i_peanut_butter -->|Yes| assemble{Assemble Sandwich}
    get_peanut_butter --> assemble{Assemble Sandwich}
    assemble --> end_sequence((END))
```
