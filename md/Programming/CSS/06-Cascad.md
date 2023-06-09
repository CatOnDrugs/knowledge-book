# Наследование CSS стилей

## Наследование свойств(стилей)

Наследование становится важно, когда несколько селекторов указывают на один элемент:

1. Cascad(каскад) - берется последний определенный в CSS документе
1. Specific(специфичность) - чем более узкий селектор тем свойства(стиль) приоритетнее. [Более подробно](#расчет-специфичности)
1. Inherit(наследование) - некоторые свойства передются от родителя к потомку. В основном это касается текстовых свойства. Так же можно задать [наследование значений]()

## Расчет специфичности

(упрощенная версия) Расчитывается четырехзначное число по праилам ниже. Чем больше число тем выше приоритет стиля:

 - Тысячи : поставьте единицу в эту колонку, если объявление стиля находится внутри атрибута style(встроенные стили). Такие способ не имеют селекторов, поэтому их специфичность всегда просто 1000
 - Сотни  : поставьте единицу в эту колонку за каждый селектор ID, содержащийся в общем селекторе
 - Десятки: поставьте единицу в эту колонку за каждый селектор класса, селектор атрибута или псевдокласс, содержащийся в общем селекторе
 - Единицы: поставьте общее число единиц в эту колонку за каждый селектор элемента или псевдоэлемент, содержащийся в общем селекторе

 !important. Прописав это в свойстве, сделает его самым специфичным. Не рекомендуется использовать

 ````css
 p {
     border: none !important;
 }
````

## Наследование

Для начала нужно понять, что стили делятся на следущие группы:

- Initial value - базовый стиль. Один для всего веба. На MDN у HTML тегов описан в свойствах initial value
- Browser styles - браузерные стили. Индивидуальны для каждого браузера. Но по большей части схожи
- CSS - стили в CSS документе
- Style - аттрибут в html тегах

Эти значения можно прописывать любому свойсту стиля:

````css
/* взять значение свойства у ближайшего родительского элемента */
inherit
/* устанавливает значение из базового стиля */
initial
/* для наследуемых свойств применяется inherit, для не наследуемых initial */
/* возвращает свойству его естественное значение */
unset
/* работает как unset, но берет значения из стилей браузера */
/* не все браузеры поддерживают. Возвращает свойству его естественное значение */
revert
````

Так-то unset и revert бесполезны. Но с аттрибутом all все приобретает смысл:
{ all: unset } - сбрасывает все свойства до естественных
{ all: initial value } - сбрасывает все свойства до стандартных

