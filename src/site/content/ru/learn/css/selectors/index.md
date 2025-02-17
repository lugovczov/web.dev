---
title: Селекторы
description: |-
  Чтобы применить CSS к элементу, нужно выбрать его.
  CSS позволяет сделать это несколькими способами, описанными в этом модуле.
audio:
  title: 'Подкаст CSS — 002: Селекторы'
  src: "https://traffic.libsyn.com/secure/thecsspodcast/TCP_CSS_Podcast__Episode_002_v2.0_FINAL.mp3?dest-id=1891556"
  thumbnail: image/foR0vJZKULb5AGJExlazy1xYDgI2/ECDb0qa4TB7yUsHwBic8.png
authors:
  - andybell
date: 2021-03-29
---

Каким способом можно увеличить шрифт текста первого абзаца статьи и сделать его красным?

```html
<article>
  <p>Шрифт этого абзаца должен быть красным и более крупным, чем в остальном тексте.</p>
  <p>Шрифт этого абзаца должен иметь нормальный размер и цвет, используемый по умолчанию.</p>
</article>
```

С помощью селектора CSS найдите нужный элемент и примените к нему правило CSS, как показано ниже.

```css
article p:first-of-type {
  color: red;
  font-size: 1.5em;
}
```

Для подобных ситуаций в CSS имеется множество способов выбора элементов и применения правил к ним — от очень простых до очень сложных.

{% Codepen { user: 'web-dot-dev', id: 'XWprGYz', height: 250 } %}

## Части правила CSS

Чтобы понять, как работают селекторы и какова их роль в CSS, важно знать части правила CSS. Правило CSS — это блок кода, в котором содержится один или несколько селекторов и одно или несколько объявлений.

<figure class="w-figure">{% Img src="image/VbAJIREinuYvovrBzzvEyZOpw5w1/hFR4OOwyH5zWc5XUIcyu.svg", alt="Изображение правила CSS с селектором .my-css-rule", width="800", height="427" %}</figure>

В этом правиле CSS **селектором** является элемент `.my-css-rule`, который находит все элементы с классом `my-css-rule` на странице. В фигурных скобках содержатся три объявления. Объявление — это пара, состоящая из свойства и значения, благодаря которой можно применять стили к элементам, соответствующим селекторам. Правило CSS может иметь неограниченное количество объявлений и селекторов.

## Простые селекторы

Группа самых простых селекторов предназначена для элементов HTML, а также классов, идентификаторов и других атрибутов, которые можно добавить в тег HTML.

### Универсальный селектор

[Универсальный селектор,](https://developer.mozilla.org/docs/Web/CSS/Universal_selectors) также называемый подстановочным знаком, соответствует любому элементу.

```css
* {
  color: hotpink;
}
```

Благодаря этому правилу текст каждого элемента HTML на странице будет иметь ярко-розовый (hotpink) цвет.

### Селектор типа

[Селектор типа](https://developer.mozilla.org/docs/Web/CSS/Type_selectors) напрямую соответствует элементу HTML.

```css
section {
  padding: 2em;
}
```

Благодаря этому правилу для всех сторон каждого элемента `<section>` атрибут отступа `padding` будет иметь значение `2em`.

### Селектор класса

Элемент HTML может содержать один или несколько элементов, определенных в его атрибуте `class`. [Селектор класса](https://developer.mozilla.org/docs/Web/CSS/Class_selectors) соответствует любому элементу, к которому применен этот класс.

```html
<div class="my-class"></div>
<button class="my-class"></button>
<p class="my-class"></p>
```

Любой элемент, к которому применен этот класс, будет окрашен в красный цвет:

```css
.my-class {
  color: red;
}
```

Обратите внимание на то, что символ `.` имеется только в CSS, но **не** в HTML. Это связано с тем, что символ `.` указывает языку CSS, что необходимо сопоставить члены атрибутов класса. Это распространенный шаблон в CSS, когда специальный символ или набор символов используется для определения типов селекторов.

Элемент HTML, имеющий класс `.my-class`, по-прежнему будет соответствовать указанному выше правилу CSS, даже если у него есть несколько других классов. Пример:

```html
<div class="my-class another-class some-other-class"></div>
```

Это связано с тем, что CSS ищет атрибут `class`, который *содержит* определенный класс, а не точно соответствует этому классу.

{% Aside %} Значение атрибута класса может быть практически любым. Единственное, что может ввести в заблуждение, — то, что класс (или идентификатор) не должен начинаться с числа, например так: `.1element`. Дополнительные сведения см. [в спецификации](https://www.w3.org/TR/CSS21/syndata.html#characters). {% endAside %}

### Селектор идентификатора

Элемент HTML с атрибутом `id` должен быть единственным элементом на странице с нужным значением идентификатора. Выбирайте элементы с помощью [селектора идентификатора](https://developer.mozilla.org/docs/Web/CSS/ID_selectors) следующим образом:

```css
#rad {
  border: 1px solid blue;
}
```

Этот код CSS задает синюю границу для элемента HTML, у которого атрибут `id` имеет значение `rad`. Пример:

```html
<div id="rad"></div>
```

Как и в случае с селектором класса `.` используйте символ `#`, чтобы указать CSS, что нужно искать элемент, соответствующий следующему за ним атрибуту `id`.

{% Aside %} Если браузер найдет несколько экземпляров атрибута `id`, он все равно будет применять все правила CSS, соответствующие селектору этого атрибута. Тем не менее у любого элемента с атрибутом `id` должно быть уникальное значение этого атрибута, поэтому если вы не пишете очень специфический код CSS для одного элемента, старайтесь не применять стили с использованием селектора `id`, так как вы не сможете повторно использовать эти стили в другом месте. {% endAside %}

### Селектор атрибута

С помощью [селектора атрибута](https://developer.mozilla.org/docs/Web/CSS/Attribute_selectors) можно выполнять поиск элементов, которые имеют определенный атрибут HTML или определенное значение атрибута HTML. Чтобы указать CSS, что нужно найти атрибуты, заключите селектор в квадратные скобки (`[ ]`).

```css
[data-type='primary'] {
  color: red;
}
```

Этот код CSS ищет все элементы, у которых есть атрибут `data-type` со значением `primary`. Пример:

```html
<div data-type="primary"></div>
```

Вместо того, чтобы искать конкретное значение атрибута `data-type`, можно также искать элементы, у которых имеется этот атрибут независимо от его значения.

```css
[data-type] {
  color: red;
}
```

```html
<div data-type="primary"></div>
<div data-type="secondary"></div>
```

Текст в обоих этих элементах `<div>` будет красным.

Вы можете использовать селекторы атрибутов с учетом регистра, добавляя в них оператор `s`.

```css
[data-type='primary' s] {
  color: red;
}
```

Это означает, что если бы у элемента HTML атрибут `data-type` имел значение `Primary`, а не `primary`, текст в нем не был бы красным. Можно сделать наоборот — отключить функцию учета регистра — с помощью оператора `i`.

Наряду с операторами case можно использовать операторы, которые сопоставляют части строк внутри значений атрибутов.

```css
/* Элемент href, содержащий адрес "example.com" */
[href*='example.com'] {
  color: red;
}

/* Элемент href, начинающийся с https */
[href^='https'] {
  color: green;
}

/* Элемент href, оканчивающийся на .com */
[href$='.com'] {
  color: blue;
}
```

<figure class="w-figure">{% Codepen { user: 'web-dot-dev', id: 'BapBbOy' } %} <figcaption class="w-figcaption">В этой демонстрации оператор $ в селекторе атрибута получает значение типа файла из атрибута href. Это позволяет добавить префикс к подписи на основе этого типа файла с помощью псевдоэлемента.</figcaption></figure>

### Группирование селекторов

Селектор необязательно должен соответствовать только одному элементу. Можно сгруппировать несколько селекторов, разделив их запятыми:

```css
strong,
em,
.my-class,
[lang] {
  color: red;
}
```

В этом примере изменяется цвет как элементов `<strong>`, так и элементов `<em>`. Он также расширен и включает класс `.my-class` и элемент с атрибутом `lang`.

{% Assessment 'simple-selectors' %}

## Псевдоклассы и псевдоэлементы

В CSS имеются полезные типы селекторов, которые ориентированы на определенное состояние платформы, например на структуры *внутри* элемента или на части элемента, когда на элемент наведен указатель мыши.

### Псевдоклассы

Элементы HTML могут находиться в разных состояниях потому что с ними взаимодействует пользователь либо потому что один из их дочерних элементов находится в том или ином состоянии.

Например, пользователь может навести указатель мыши как на сам элемент HTML, *так и* на его дочерний элемент. В таких ситуациях используйте псевдокласс `:hover`.

```css
/* На нашу ссылку навели указатель мыши */
a:hover {
  outline: 1px dotted green;
}

/* Настройка другого цвета фона для всех четных абзацев */
p:nth-child(even) {
  background: floralwhite;
}
```

Дополнительные сведения см. в [модуле, посвященном псевдоклассам](/learn/css/pseudo-classes).

### Псевдоэлемент

Псевдоэлементы отличаются от псевдоклассов тем, что они не реагируют на состояние платформы, а действуют так, как если бы они вставляли новый элемент с помощью CSS. Кроме того, синтаксис псевдоэлементов отличается от синтаксиса псевдоклассов, потому что вместо одинарного двоеточия (`:`) в них используется двойное двоеточие (`::`).

{% Aside %} Двойное двоеточие (`::`) отличает псевдоэлемент от псевдокласса, но так как этого различия не было в старых версиях спецификаций CSS, браузеры поддерживают одинарное двоеточие для исходных псевдоэлементов, например `:before` и `:after`. Это обеспечивает обратную совместимость со старыми браузерами, например IE8. {% endAside %}

```css
.my-element::before {
  content: 'Prefix - ';
}
```

Как и в приведенной выше демонстрации, в которой вы указали тип файла в качестве префикса подписи ссылки, с помощью псевдоэлемента `::before` можно вставить содержимое **в начало элемента**, а с помощью псевдоэлемента `::after` — в **конец элемента**.

Перечень функций псевдоэлементов не ограничен вставкой содержимого. Их также можно использовать для нацеливания на определенные части элемента. Предположим, у вас есть список. С помощью псевдоэлемента `::marker` можно применить стиль к каждому маркеру (или номеру) в списке.

```css
/* Теперь в списке будут либо красные точки, либо красные номера */
li::marker {
  color: red;
}
```

Кроме того, с помощью псевдоэлемента `::selection` можно применять стили к содержимому, выделенному пользователем.

```css
::selection {
  background: black;
  color: white;
}
```

Подробные сведения см. в [модуле о псевдоэлементах](/learn/css/pseudo-elements).

{% Assessment 'pseudo-selectors' %}

## Сложные селекторы

Вы уже познакомились с большим количеством селекторов, но иногда требуется более *детальный контроль* с помощью CSS. В этом случае на помощь приходят сложные селекторы.

Следует помнить, что хотя указанные ниже селекторы предоставляют больше возможностей, мы можем только **выполнять каскадирование вниз**, выбирая дочерние элементы. Мы не можем нацеливаться вверх и выбирать родительские элементы. Мы расскажем, что такое каскад и как он работает, [в следующем занятии](/learn/css/the-cascade).

### Комбинаторы

Комбинатор — это то, что находится между двумя селекторами. Например, если используется селектор `p > strong`, комбинатором будет символ `>`. Селекторы, в которых используются такие комбинаторы, позволяют выбирать элементы в зависимости от их расположения в документе.

#### Комбинатор потомков

Чтобы понять, что такое комбинаторы потомков, нужно сначала разобраться, что представляют собой родительские и дочерние элементы.

```html
<p>Абзац текста, часть которого <strong>выделена полужирным шрифтом</strong>.</p>
```

Родительский элемент — это элемент `<p>`, который содержит текст. Внутри этого элемента `<p>` находится элемент `<strong>`, благодаря которому шрифт заключенного в нем текста будет полужирным. Так как он находится внутри элемента `<p>`, он представляет собой дочерний элемент этого элемента.

Комбинатор потомков позволяет нам нацеливаться на дочерний элемент. В нем используется пробел (` `), указывающий браузеру искать дочерние элементы:

```css
p strong {
  color: blue;
}
```

Этот фрагмент кода выбирает все элементы `<strong>`, которые являются дочерними элементами только для элементов `<p>` и рекурсивно делает их синими.

<figure class="w-figure">{% Codepen { user: 'web-dot-dev', id: 'BapBbGN' } %} <figcaption class="w-figcaption">Так как комбинатор потомков является рекурсивным, то к каждому дочернему элементу будет добавлен отступ, что приведет к эффекту «ступенек».</figcaption></figure>

Этот эффект лучше визуализирован в примере выше, в котором используется селектор комбинаторов `.top div`. Это правило CSS добавляет левый отступ к этим элементам `<div>`. Так как комбинатор является рекурсивным, то ко всем элементам `<div>`, находящимся в элементе `.top`, будет применен одинаковый отступ.

Посмотрите на панель HTML в этой демонстрации, и вы увидите, что элемент `.top` имеет несколько дочерних элементов `<div>`, у которых, в свою очередь, есть дочерние элементы `<div>`.

#### Комбинатор следующего элемента одного уровня

С помощью символа `+` в селекторе можно выполнить поиск элемента, который следует непосредственно за другим элементом.

{% Codepen { user: 'web-dot-dev', id: 'JjEPzwB' } %}

Чтобы добавить пробел между элементами в стопке, используйте комбинатор следующего элемента одного уровня, *только* если элемент является **следующим элементом одного уровня** для дочернего элемента `.top`.

С помощью следующего селектора можно добавить поле ко всем дочерним элементам `.top`:

```css
.top * {
  margin-top: 1em;
}
```

Проблема заключается в том, что, поскольку вы выбираете каждый дочерний элемент `.top`, это правило может создать дополнительное ненужное пространство. **Комбинатор следующего элемента одного уровня** в сочетании с **универсальным селектором** позволяет не только управлять тем, для каких элементов будет добавлено пространство, но и добавлять пространство к **любому элементу**. Это дает некоторую гибкость в долгосрочной перспективе независимо от того, какие элементы HTML будут встречаться в элементе `.top`.

#### Комбинатор последующего элемента одного уровня

Комбинатор последующего элемента очень похож на селектор следующего элемента одного уровня. Однако вместо символа `+` здесь используется символ `~`. Отличие заключается в том, что элемент просто должен следовать за другим элементом с одинаковым родительским элементом, а не быть следующим элементом с тем же родителем.

<figure class="w-figure">{% Codepen { user: 'web-dot-dev', id: 'ZELzPPX', height: 400 } %} <figcaption class="w-figcaption">С помощью селектора последующего элемента и псевдокласса :checked можно создать «чистый» элемент переключателя CSS.</figcaption></figure>

Этот комбинатор последующего элемента обеспечивает немного меньшую жесткость, что полезно в контекстах, аналогичных тому, который приведен в примере выше. В этом контексте мы меняем цвет настраиваемого переключателя, если связанный с ним флажок находится в состоянии `:checked`.

#### Комбинатор дочернего элемента

Комбинатор дочернего элемента (также называемый прямым потомком) предоставляет дополнительные возможности управления рекурсией, которая применяется в селекторах комбинаторов. С помощью символа `>` можно использовать селектор комбинатора **только** для непосредственных дочерних элементов.

Рассмотрим предыдущий пример с комбинатором следующего элемента одного уровня. Код добавляет пространство к каждому **следующему элементу одного уровня**, но если у одного из этих элементов также есть **следующие элементы одного уровня** в качестве дочерних элементов, это может привести к добавлению нежелательного дополнительного пространства.

{% Codepen { user: 'web-dot-dev', id: 'ExZYMJL' } %}

Чтобы смягчить последствия этой проблемы, измените **селектор следующего элемента одного уровня**, включив в него комбинатор дочернего элемента `> * + *`. Теперь это правило будет применяться **только** к непосредственным дочерним элементам элемента `.top`.

{% Codepen { user: 'web-dot-dev', id: 'dyNbrEr' } %}

### Составные селекторы

Вы можете сочетать селекторы, чтобы повысить уровень конкретности и удобочитаемость. Например, чтобы выполнить нацеливание на элементы `<a>`, которые также имеют класс `.my-class`, используйте следующий код:

```css
a.my-class {
  color: red;
}
```

Этот код не будет применять красный цвет ко всем ссылкам; он будет применять красный цвет только к элементу `.my-class`, **если** он находится в элементе `<a>`. Дополнительные сведения об этом см. в [модуле, посвященном специфичности](/learn/css/specificity).

{% Assessment 'complex-selectors' %}

## Ресурсы

- [Справочное руководство по селекторам CSS](https://developer.mozilla.org/docs/Web/CSS/CSS_Selectors)
- [Интерактивная игра по селекторам](https://flukeout.github.io/)
- [Справочное руководство по псевдоклассам и псевдоэлементам](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- [Средство, которое переводит селекторы CSS в эксплейнеры на понятном английском языке](https://kittygiraudel.github.io/selectors-explained/)
