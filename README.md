# Делегаты

Обсудить [![Join the chat at https://gitter.im/EvilBeaver/oscript-library](https://badges.gitter.im/EvilBeaver/oscript-library.svg)](https://gitter.im/EvilBeaver/oscript-library?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![GitHub release](https://img.shields.io/github/release/artbear/delegate.svg)](https://github.com/artbear/delegate/releases) [![Build Status](http://build.oscript.io/buildStatus/icon?job=oscript-library/delegate/master)](http://build.oscript.io/job/oscript-library/job/delegate/job/master/) 

Библиотека предназначена для создания и выполнения делегатов/функторов.

Делегат представляет собой объект, который может ссылаться на метод другого объекта.

Например, можно выполнять `функции-коллбэки` или унифицированно выполнять методы у схожих объектов.

Также можно использовать для замены "некрасивых" и многословных объектов 1С - `ОписаниеОповещения`,
которые имеют мало смысла в мире OneScript.

## Использование

### Обработчик-процедура

```bsl
// Подключение библиотеки
#Использовать Делегат

// Метод, вызываемый из делегата
Процедура Поздороваться(Имя) Экспорт
    Сообщить("Привет, " + Имя + "!");
КонецПроцедуры

Делегат = Делегаты.Создать(ЭтотОбъект, "Поздороваться", "Мир");

Делегаты.Исполнить(Делегат); // или Делегат.Исполнить();

ДелегатНовыйМир = Делегаты.Создать(ЭтотОбъект, "Поздороваться");

ДелегатНовыйМир.Исполнить("Новый мир"); // или Делегаты.Исполнить(ДелегатНовыйМир, "Новый мир");
```

### Обработчик-функция

```bsl
// Подключение библиотеки
#Использовать Делегат

// Метод, вызываемый из делегата
Функция Поздороваться(Имя) Экспорт
    Сообщить("Привет, " + Имя + "!");
    Возврат Имя;
КонецФункции

Делегат = Делегаты.Создать(ЭтотОбъект, "Поздороваться", "Мир");

ИмяМир = Делегаты.Исполнить(Делегат); // или Делегат.Исполнить();

ДелегатНовыйМир = Делегаты.Создать(ЭтотОбъект, "Поздороваться");

ИмяНовыйМир = ДелегатНовыйМир.Исполнить("Новый мир"); // или Делегаты.Исполнить(ДелегатНовыйМир, "Новый мир");
```

### Передача нескольких параметров

```bsl
#Использовать Делегат

Процедура МетодСТремяПараметрами(Парам1, Парам2, Парам3) Экспорт
	Журнал  = СтрШаблон("%1%2, %3, %4!", Журнал, Парам1, Парам2, Парам3);
КонецПроцедуры

Делегат = Делегаты.Создать(ЭтотОбъект, "МетодСТремяПараметрами");

Массив = Делегаты.МассивПараметров(1, "Два", "Десять");

Делегат.Исполнить(Массив);
```

или можно указать параметры при создании Делегата

```bsl
#Использовать Делегат

Процедура МетодСТремяПараметрами(Парам1, Парам2, Парам3) Экспорт
	Сообщить(СтрШаблон("%1, %2, %3!", Парам1, Парам2, Парам3));
КонецПроцедуры

Массив = Делегаты.МассивПараметров(1, "Два", "Десять");

Делегат = Делегаты.Создать(ЭтотОбъект, "МетодСТремяПараметрами", Массив);

Делегат.Исполнить();
```
