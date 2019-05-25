# SASS Flexbox grid

1.   [](#&#167;)

## Содержание
1.   [Описание](#&#167;1)   
1.   [Быстрый старт](#&#167;2)   
1.   [Описание миксинов для построения сетки](#&#167;3)      
    1.   [grid-container-fluid](#&#167;3-1)     
    1.   [grid-container](#&#167;3-2)       
    1.   [grid-row](#&#167;3-3)     
    1.   [grid-col](#&#167;3-4)         
1.   [Обзор](#&#167;4)      
    1.   [*Контейнеры](#&#167;4-)   
    1.   [Параметры сеток](#&#167;4-2)  
    1.   [*Контейнер с адаптивной шириной](#&#167;4-)   
    1.   [*Мультиряд одинаковой ширины](#&#167;4-)  
    1.   [*Выравнивание](#&#167;4-)     
        1.   [*Вертикальное выравнивание](#&#167;4-5-)  
        1.   [*Горизонтальное выравнивание](#&#167;4-5-)    
        1.   [*](#&#167;4-5-)   
        1.   [*](#&#167;4-5-)   
    1.   [*Изменение порядка элементов](#&#167;4-)  
    1.   [*Смещающиеся колонки](#&#167;4-)  
    1.   [*Вложенность](#&#167;4-)      
> \* Пункты еще не готовы       

## &#167;1
## Описание    

Система сеток SASS Flexbox Grid использует контейнеры, ряды и колонки, чтобы удобно располагать содержимое. Библиотека реализован с помощью флексбокса и полностью адаптивен. 

Содержит в себе набор миксинов, благодаря которым генерируется код необходимый для создания сетки. 

Используя миксины отпадает необходимость использовать множество классов для построения сетки. Вы исипользуете только симантические классы не засоряя свой html и css  лишними классами. Все необходимые свойства добавляются в ваши классы. 



## &#167;2
##  Быстрый старт

Добавить файл  `_flexboxgrid.scss` в ваш файл стилей.
```
@import '../../flexbox-grid/flexboxgrid';
```
Применять миксины для построения сетки.


## &#167;3
##  Описание миксинов для построения сетки.

Список используемых миксинов:
*   grid-container-fluid
*   grid-container
*   grid-row
*   grid-col

### &#167;3-1
### grid-container-fluid

Для создания растягивающегося контейнера. Будет занимать всю область родительского контейнера на всех брекпоинтах сетки.

Применить в блоке который должен стать контейнером:
```
.container-fluid {
    @include grid-container-fluid;
}

```

Полчим CSS код: 
```
.container {
  /* grid container-fluid */
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
```


### &#167;3-2
### grid-container

Для создания отзывчивого контейнера, с фиксированной шириной (что значит, что его max-width изменяется на каждом брейкпойнте) 

Применить в блоке который должен стать контейнером:
```
.container {
    @include grid-container;
}

```

Полчим CSS код: 
```
.container {
  /*  grid container  */
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

@media (min-width: 576px) {
  .container {
    /*  grid container  */
    max-width: 540px;
  }
}

@media (min-width: 768px) {
  .container {
    /*  grid container  */
    max-width: 720px;
  }
}

@media (min-width: 992px) {
  .container {
    /*  grid container  */
    max-width: 960px;
  }
}

@media (min-width: 1200px) {
  .container {
    /*  grid container  */
    max-width: 1140px;
  }
}
```

### &#167;3-3
### grid-row

Для инициализации ряда (строки или row). Применить в классе являющийся родителем для блоков сетки.
Синтаксис:
```
//  Для установки настроик одного брекпоинта (точки изменения расположения блоков)
@include grid-row([extend] [, justify-content] [, align-items] [, text-align] [, direction]);

//  Для установки только некоторых свойств брекпоинта
@include grid-row($extend: xl, $text-align: center);

//  Мульти устанвок свойств сразу всех брекпоинтов сетки
@include grid-row((
    extend: justify-content align-items text-align direction,
    extend: '' align-items text-align direction,
    extend: justify-content '' text-align direction,
    extend: '',

    ...
))

```

> __extend__ (значение по умолчанию: xs)    
>   Брек поинт сетки [таблица брек поинтов](#breakpoint)    
> Все варианты выбора:
> * ___xs___
> * ___sm___
> * ___md___
> * ___lg___
> * ___xl___

> __justify-content__ (значение по умолчанию: start)     
> Определяет выравнивание вдоль основной оси.      
> * ___start___ - элементы прижимаются к началу строки;
> * ___end___ - элементы прижимаются к концу строки;
> * ___center___ - элементы прижимаются к концу строки;
> * ___space-between___ - элементы размещаются равномерно на линии; первый элемент находится в начале строки, последний элемент находится в конце строки
> * ___space-around___ - элементы размещаются равномерно на линии с одинаковым пространством возле них. Обратите внимание, что визуально пространство не одинаковое, так как у всех элементов одинаковое пространство с обеих сторон.


> __align-items__ (значение по умолчанию: stretch)     
> Это свойство определяет поведение ¡ex-элементов вдоль поперечной оси на текущей строке. Думайте о нём как о justify-content, только для поперечной оси (перпендикулярной основной оси).     
> * ___start___ - элементы размещаются в начале поперечной оси;
> * ___end___ - элементы размещаются в конце поперечной оси;
> * ___center___  - элементы располагаются по центру поперечной оси;
> * ___baseline___ center - элементы располагаются по центру поперечной оси;
> * ___stretch___ -  растягиваются чтобы заполнить весь контейнер (попрежнему соблюдают min-width / max-width

> __text-align__ (значение по умолчанию: left) 
> Выравнивание текста в контейнера, опирирует свойством text-align
> * left
> * right
> * center
> * justify

> __direction__ (значение по умолчанию: row) 
> Устанавливает основную ось, таким образом определяет направление элементов расположенных в контейнере.
> * ___row (по умолчанию)___ - слева направо в ltr; справа налево в rtl;
> * ___row-reverse___ - справа налево в ltr; слева направо в rtl;
> * ___column___ - тоже самое что row , только сверху вниз;
> * ___column-reverse___ - тоже самое что row-reverse , только снизу вверх;

    Внимание!
    Для корректной работы необходимо в контейнере обязательно применить свойство для брекпоинта xs. Т.е

```
@include grid-row();

```

### &#167;3-4
### grid-col

Колокнки эелементы которые непосредственно распределяются по сетке. 
Синтаксис:
```
//  Для установки настроик одного брекпоинта (точки изменения расположения блоков)
@include grid-col([$extend] [, $col] [, $offset] [, $order] );

//  Для установки только некоторых свойств брекпоинта
@include grid-col($extend: lg, $offset: 5);
//  или так
@include grid-col((
  lg: '' 5,
))

//  Мульти устанвок свойств сразу всех брекпоинтов сетки
//  для пропуска свойства использовать пустую строку ''
@include grid-col((
  extend: [col] [offset] [oreder],
  extend: [col] [offset] [oreder],
  ...
))
```
> __extend__ (значение по умолчанию: xs)    
>   Брек поинт сетки [таблица брек поинтов](#breakpoint)    
> Все варианты выбора:
> * ___xs___
> * ___sm___
> * ___md___
> * ___lg___
> * ___xl___

> ___col___ (значение по умолчанию: auto)
> 1-12 указать количество колонок, которые будет занимать контейнер
> * 1-12 (number)
> * auto  Добавляйте любое количество простых классов для каждого брейкпойнта, и каждая колонка будет одинаковой ширины.

> ___offset___  (значение по умолчанию: 0)
> Позволяет смещять контейнер. Указать величину сетки. 
> * 1-12 

> ___oreder___  (значение по умолчанию: 0)
> изменяет порядок элементов. Он поддерживает 1 для 12 
> * 1-12

## &#167;4
##  Обзор

Ряды – это обертка для колонок. Каждая колонка имеет горизонтальный padding (настраивается в $gap) для контроля пространства между колонками. Этот padding (паддинг) влияет на ряды с отрицательным марджином. В этом случае все содержимое ваших колонок будет визуально центрировано внизу с левой стороны.

Содержимое должно быть расположено в колонках, и только колонки могут быть расположены в рядах.

### &#167;4-1
### Контейнеры
---

Это базовый элемент, они необходимы при использовании стандартной сеточной системы. Выбирайте отзывчивый, с фиксированной шириной (что значит, что его max-width изменяется на каждом брейкпойнте) или контейнер с плавающей шириной (width ==100% всегда).

Контейнеры могут иметь вложенные элементы, но в большинстве случаев можно обойтись без них.

Используйте `@include grid-container` для создания отзывчивого контейнера с фиксированной широиной.

```html
<!-- Имя контейнера может быть любым -->
<div class="container">
  <!-- Content here -->
</div>
```
SASS файл:
```
.container {
    @include grid-container;
}
```

Используйте `@include grid-container-fluid` для создания контейнера полной ширины, занимающий 100% зоны просмотра.
```html
<!-- Имя контейнера может быть любым -->
<div class="container-fluid">
  ...
</div>
```
SASS файл:
```
.container {
    @include grid-container-fluid;
}
```
## &#167;4-2
##  Параметры сеток
Библиотека использует em и rem для задания большинства размеров, а пиксели px – для «брейкпойнтов» сетки и ширин контейнеров. Это происходит потому, что ширина зоны видимости на каждом устройстве измеряется в пикселях и не изменяется с размером шрифта.

Посмотрим, как действуют некоторые аспекты системы сеток Bootstrap на разных «ручных» устройствах.


##### Breakpoint
**  | Extra Small |   Small   |   Medium  |   Large   |   Extra Large
--- | --- |   --- |   --- |   --- |   --- 
**  | <576px  |   &#8805;576px    |   &#8805;768px    |   &#8805;992px    |   &#8805;1200px   
Максимальная ширина контейнера  | None (auto) | 	540px |	720px |	960px |	1140px
Имя опции   | 	xs 	|   sm  |   md  |   lg  |   xl  |
Число колонок 	|   Настраивается переменной `$columns` (дефолтно 12 )
Ширина отступа  | 	настраивается переменной `$gap` (дефолтно 15px с каждой стороны столбца)
Может быть вложенным    | 	Да  
Упорядочивание колонок  | 	Да

##  Равная ширина

Например, здесь мы видим две сетки, которые подойдут к любому устройству и зоне видимости, от xs до xl. Добавляйте любое количество простых классов для каждого брейкпойнта, и каждая колонка будет одинаковой ширины.
1 из 2
2 из 2
1 из 3
2 из 3
3 из 3

<div class="container">
  <div class="row">
    <div class="col">
      1 из 2
    </div>
    <div class="col">
      2 из 2
    </div>
  </div>
  <div class="row">
    <div class="col">
      1 из 3
    </div>
    <div class="col">
      2 из 3
    </div>
    <div class="col">
      3 из 3
    </div>
  </div>
</div>
