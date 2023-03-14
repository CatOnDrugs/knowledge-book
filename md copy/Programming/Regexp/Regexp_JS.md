# Регулярные выражения

Нужны для поиска в тексте по шаблону

# Как создать

Прекомпелированное регулярное выражение

````js
const regexp = /<regexp>/;
````

Компилирует регулярное выражение в RunTime
````js
var regexp = new RegExp("ab+c");
````

# Шаблоны

## Поиск обычных последовательностей

````js
const regexp = /abc/; // Поиск обычной последовательности
const regexp = /^It/; // Поиск It в начале строки
const regexp = /end$/; // Поиск end в конце строки
const regexp = /\b/; // Граница(находит и начало и конец) слов
const regexp = /./; // Поиск любого символа кроме переноса строки
const regexp = /\B/; // Поиск несловобразующей границы
// Проще: между двумя словобразующими символами или двумя неслообразующими символами
````

## Наборы символов

````js
const regexp = /[xyz]/;     // Поиск любого символа из перечисленных
const regexp = /[^xyz]/;    // Поиск любого символа НЕ из перечисленных

const regexp = /[0-9]/;     // Все цифры
const regexp = /\d/;

const regexp = /[^0-9]/;    // Все НЕ цифры
const regexp = /\D/;

const regexp = /[0-9a-zA-Z_]/; // Все цифробуквенные символы и нижнее подчеркивание
const regexp = /\w/;

const regexp = /[^0-9a-zA-Z_]/; // Все НЕ цифробуквенные символы и нижнее подчеркивание
const regexp = /\W/;

const regexp = /\s/; // Соответствует одиночному символу пустого пространства, включая пробел, табуляция, прогон страницы, перевод строки.
const regexp = /\S/; // Соответствует одиночному символу непустого пространства

// Поиск специальных символов
const regexp = /\*/;
````

## Поиск повторяющихся последовательностей

````js
// {n} - соответствует предыдущему символу повторенному n раз
const regexp = /Vasia{4}/; // Соответствует: Vasiaaaa

// {n, m} - соответствует предыдущему символу повторенному минимум n и максимум m раз
const regexp = /Vasia{2,3}/; // Соответствует: Vasiaa, Vasiaaa

// * - соответствует предыдущему символу повторенному 0 или более раз
const regexp = /Yeah*/; // Соответствует: Yea, Yeah, Yeahhh

// + - соответствует предыдущему символу повторенному 1 или более раз
const regexp = /Yeah+/; // Соответствует: Yeah, Yeahhh

// ? - соответствует предыдущему символу повторенному 0 или 1 раз
const regexp = /Yeah?/; // Соответствует: Yea, Yeah
````

## Шаблон с запоминанием

````js
// ( ... ) - запоминает соответствие. Кладет в результрующий массив [1]
const regexp = /c(ont)ent/; // Соответствует: content

// ( ?<name>... ) - запоминает соответствие. Кладет в словарь group. Достается с указанием <name>. Данная возможность поддерживается не всеми браузерами
const regexp = /c(?<partWord>ont)ent/; // Соответствует: content

// ( ?:... ) - НЕ запоминает соответствие. Не кладет в результрующий массив [1]
const regexp = /c(?:.*)ent/; // Соответствует: content

// \n - получает значение из результирующего массива. Значение считается с конца
const regexp = /petia(,) vasia\n jenia/; // Соответствует: petia, vasia, jenia
````

## Шаблоны с условием

````js
const regexp = /abc|def/; // Находит либо abc, либо def
const regexp = /abc(?=def)/; // Находит abc, только если за ним следует def
const regexp = /abc(?!def)/; // Находит abc, только если за ним НЕ следует def
````

# Используются в функциях

## match VS exec - поиск совпадения в строке

Значения для примеров ниже

````js
var str = "[99].[76].[34]"
var regExp = /\d+/
var globalRegExp = /\d+/g
````

Без флага g
````js
str.match( regExp )
// => ["99", index: 1, input: "[99].[76].[34]", groups: [undefined]]
regExp.exec( str )
// => ["99", index: 1, input: "[99].[76].[34]", groups: [undefined]]
````

С флагом g

````js
str.match( globalRegExp )
// => ["99", "76", "34"]

// exec с флагом g, меняет globalRegExp.lastIndex. С каждый вызов использует lastIndex как точку начала для поиска
globalRegExp.exec( str )
// => ["99", index: 1, input: "[99].[76].[34]", groups: [undefined]]
globalRegExp.exec( str )
// => ["76", index: 6, input: "[99].[76].[34]", groups: [undefined]]
globalRegExp.lastIndex;
// => 11
````

## test VS search - поиск совпадения в строке


````js
regex.test(str)
// Проверяет есть ли вхождения в строке. Если есть - true, иначе false

str.search(regex)
// Проверяет есть ли вхождения в строке. Если есть - вернет его index, иначе -1
````

## replace и replaceAll - замена найденных подстрок

replace с флагом g и replaceAll работают одинаково

Значения для примеров ниже

````js
var str = "[99].[76].[34]"
````

Второй аргумент строка

````js
str.replace(/\d+/g, 'fox') // константа
// => [[fox].[fox].[fox]]
str.replace(/\d+/g, '$& $&') // то что нашли
// => [[99 99].[76 76].[34 34]]
str.replace(/76/g, "$` $'") // слева от найденного и справа от найденного
// => [99]. .[34]

str.replace(/(\d)(\d)/g, '$1 - $2') // 1 и 2 сохраненные значения
// => [[9 - 9].[7 - 6].[3 - 4]]
str.replace(/(?<num>\d\d)/g, '1$<num>') // значение сохраненное под именем <num>
// => [[199].[176].[134]]
````

Вторым аргументом может быть функция. Функция принимает:

````js
function replacer(
    match,                  // найденная подстрока
    p1, p2, /* …, */ pN,    // сохраненные значения
    offset,                 // index смещения найденной подстроки
    string,                 // вся исследуемая строка
    groups                  // (?<name>...)
) {
  return replacement;       // то на что заменяем
}
````

## split - разделение строки

Стандартный split, но разделяет по найденному регулярному выражению

````js
var str = "[99].[76].[34]"
str.split(/]?\.?\[/)
// => [ '', '99', '76', '34]' ]
````

# Флаги

Пишутся в конце:
````js
var regexp = /regexp/gimy;
````

|Флаг|Общее описание|Комментарий|
|:--:|:--|:--|
|g|глобальный поиск|в примерах выше применен везде, где на что-то влияет|
|i|регистронезависимый поиск|
|m|многострочный поиск| На странице regexp с MDN, есть две пометки когда флаг на что-то влияет, но я так и не понял зачем он нужен
|y|применяет регулярку прямо в позиции lastIndex