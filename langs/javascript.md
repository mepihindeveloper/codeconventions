# Содержание

1. [Объявление переменных](#references)
2. [Объекты](#objects)
3. [Массивы](#arrays)
4. [Деструктуризация](#destructuring)
5. [Строки](#strings)
6. [Функции](#functions)
7. [Стрелочные функции](#farrow-functions)
8. [Итераторы и генераторы](#iterators-and-generators)
9. [Переменные](#variables)
10. [Операторы сравнения и равенства](#comparison-operators--equality)
11. [Блоки](#blocks)
12. [Точка с запятой](#semicolons)
13. [События](#events)
14. [jQuery](#jquery)

<a name="references"></a>
# Объявление переменных

Использование `var` запрещено. 

Если необходимо переопределять значения, то используйте `let`. Если переменная не переопределяется, то используйте `const`.

<a name="objects"></a>
# Объекты

Для создания объекта используйте литеральную нотацию `const item = {}`. 

Не мспользуйте сокращённую запись метода объекта:

```javascript
const atom = {
    value: 1,

    addValue: function (value) {
        return atom.value + value;
    },
};
```
Используйте сокращённую запись свойств объекта (в случае, когда наименование ключа совпадает с названием переменной):

```javascript
const lukeSkywalker = 'Luke Skywalker';

const obj = {
    lukeSkywalker,
};
```
Группируйте сокращённые записи свойств в начале объявления объекта. Так легче сказать, какие свойства используют сокращённую запись:

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker'

const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
};
```
Все идентификаторы помещаются в кавычки:

```javascript
const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
};
```
Не вызывайте напрямую методы `Object.prototype`, такие как `hasOwnProperty`, `propertyIsEnumerable`, и `isPrototypeOf`. Эти методы могут быть переопределены в свойствах объекта, который мы проверяем `{ hasOwnProperty: false }`, или этот объект может быть `null` (`Object.create(null)`:

```javascript
const has = Object.prototype.hasOwnProperty; // Кэшируем запрос в рамках модуля.
console.log(has.call(object, key))
```

Используйте оператор расширения вместо `Object.assign` для поверхностного копирования объектов. Используйте синтаксис оставшихся свойств, чтобы получить новый объект с некоторыми опущенными свойствами:

```javascript
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```
<a name="arrays"></a>
# Массивы

Для создания массива используйте литеральную нотацию `const items = []`.

Для добавления элемента в массив используйте `Array.push` вместо прямого присваивания `someStack.push('abracadabra')`.

Для копирования массивов используйте оператор расширения `...`: `const itemsCopy = [...items]`

Для преобразования итерируемого объекта в массив используйте оператор расширения `...` вместо `Array.from`: `const nodes = [...foo]`.

Используйте операторы `return` внутри функций обратного вызова в методах массива. Можно опустить `return`, когда тело функции состоит из одной инструкции, возвращающей выражение без побочных эффектов:

```javascript
[1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
});

[1, 2, 3].map((x) => x + 1);

[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
    const flatten = acc.concat(item);
    return flatten;
});

// хорошо
inbox.filter((msg) => {
    const { subject, author } = msg;
    if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
    }

    return false;
});
```
<a name="destructuring"></a>
# Деструктуризация

При обращении к нескольким свойствам объекта используйте деструктуризацию объекта. Деструктуризация избавляет вас от создания временных переменных для этих свойств.

```javascript
// В случае необходимости использовать другие ключи user
function getFullName(user) {
    const { firstName, lastName } = user;
    return `${firstName} ${lastName}`;
}

// При использовании конкретных ключей user
function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
}
```

Используйте деструктуризацию массивов:

```javascript
const arr = [1, 2, 3, 4];

// Неудачная реализация
const first = arr[0];
const second = arr[1];

// Удачная реализация
const [first, second] = arr;
```

Используйте деструктуризацию объекта для множества возвращаемых значений, но не делайте тоже самое с массивами. Вы сможете добавить новые свойства через некоторое время или изменить порядок без последствий:

```javascript
// Неудачная реализация
function processInput(input) {
    // затем происходит чудо
    return [left, right, top, bottom];
}

// при вызове нужно подумать о порядке возвращаемых данных
const [left, __, top] = processInput(input);

// Удачная реализация
function processInput(input) {
    // затем происходит чудо
    return { left, right, top, bottom };
}

// при вызове выбираем только необходимые данные
const { left, top } = processInput(input);
```
<a name="strings"></a>
# Строки

Используйте одинарные кавычки `''` для строк. 

Если есть необходимость встроить занчение переменной в строку, то используйте шаблонный вариант: ``` const question = `How are you, ${name}?` ```

<a name="functions"></a>
# Функции

Используйте функциональные выражения без наименования функции после `function` вместо объявлений функций:

```javascript
const foo = function () {
    // ...
};
```

Оборачивайте в скобки немедленно вызываемые функции. Немедленно вызываемая функция представляет собой единый блок. Чтобы чётко показать это — оберните функцию и вызывающие скобки в ещё одни скобки. Обратите внимание, что в мире с модулями вам больше не нужны немедленно вызываемые функции.

```javascript
(function () {
    console.log('Welcome to the Internet. Please follow me.');
}());
```

Используйте синтаксис записи аргументов по умолчанию, а не изменяйте аргументы функции.

<a name="arrow-functions"></a>
# Стрелочные функции

Когда вам необходимо использовать анонимную функцию (например, при передаче встроенной функции обратного вызова), используйте стрелочную функцию. Таким образом создаётся функция, которая выполняется в контексте `this`, который мы обычно хотим, а также это более короткий синтаксис. Если у вас есть довольно сложная функция, вы можете переместить эту логику внутрь её собственного именованного функционального выражения.

```javascript
// Неудачная реализация
[1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
});

// Удачная реализация
[1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
});

[1, 2, 3].map((x) => x * x);
```

Если тело функции состоит из одного оператора, возвращающего выражениетбез побочных эффектов, то опустите фигурные скобки и используйте неявное возвращение. В противном случае, сохраните фигурные скобки и используйте оператор `return`. Синтаксический сахар. Когда несколько функций соединены вместе, то это лучше читается.

```javascript
// Неудачная реализация
[1, 2, 3].map((number) => {
    const nextNumber = number + 1;
    `A string containing the ${nextNumber}.`;
});

// Удачная реализация
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

// Удачная реализация
[1, 2, 3].map((number) => {
    const nextNumber = number + 1;
    return `A string containing the ${nextNumber}.`;
});

// Удачная реализация
[1, 2, 3].map((number, index) => ({
    [index]: number,
}));

// Неявный возврат с побочными эффектами
function foo(callback) {
    const val = callback();
    if (val === true) {
    // Сделать что-то, если функция обратного вызова вернёт true
    }
}

let bool = false;

// Неудачная реализация
foo(() => bool = true);

// Удачная реализация
foo(() => {
    bool = true;
});
```
Всегда оборачивайте аргументы круглыми скобками для ясности и согласованности. Минимизирует различия при удалении или добавлении аргументов.

```javascript
// Удачная реализация
[1, 2, 3].map((x) => x * x);

// Удачная реализация
[1, 2, 3].map((number) => (
    `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
));

// Удачная реализация
[1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
});
```

<a name="iterators-and-generators"></a>
# Итераторы и генераторы

Не используйте итераторы. Применяйте функции высшего порядка вместо таких циклов как `for-in` или `for-of`.  Это обеспечивает соблюдение нашего правила о неизменности переменных. Работать с чистыми функциями, которые возвращают значение, проще, чем с функциями с побочными эффектами. Используйте `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... для итерации по массивам, а `Object.keys()` / `Object.values()` / `Object.entries()` для создания массивов, с помощью которых можно итерироваться по объектам.

```javascript
const numbers = [1, 2, 3, 4, 5];

// Неудачная реализация
const increasedByOne = [];
for (let i = 0; i < numbers.length; i++) {
  increasedByOne.push(numbers[i] + 1);
}

// Удачная реализация
const increasedByOne = [];
numbers.forEach((num) => {
  increasedByOne.push(num + 1);
});

// Удачная реализация
const increasedByOne = numbers.map((num) => num + 1);
```

<a name="variables"></a>
# Переменные

Используйте объявление `const` или `let` для каждой переменной или присвоения. Таким образом проще добавить новые переменные. Также вы никогда не будете беспокоиться о перемещении `;` и `,` и об отображении изменений в пунктуации. Вы также можете пройтись по каждому объявлению с помощью отладчика, вместо того, чтобы прыгать через все сразу.

```javascript
// Неудачная реализация
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// Удачная реализация
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

В первую очередь группируйте `const`, а затем `let`. Это полезно, когда в будущем вам понадобится создать переменную, зависимую от предыдущих.

<a name="comparison-operators--equality"></a>
# Операторы сравнения и равенства

Используйте `===` и `!==` вместо `==` и `!=`.

Используйте сокращения для булевских типов, а для строк и чисел применяйте явное сравнение.

```javascript
// Неудачная реализация
if (isValid === true) {
  // ...
}

// Удачная реализация
if (isValid) {
  // ...
}

// Неудачная реализация
if (name) {
  // ...
}

// Удачная реализация
if (name !== '') {
  // ...
}

// Неудачная реализация
if (collection.length) {
  // ...
}

// Удачная реализация
if (collection.length > 0) {
  // ...
}
```

Тернарные операторы не должны быть вложены и в большинстве случаев должны быть расположены на одной строке.

```javascript
// Неудачная реализация
const foo = maybe1 > maybe2
  ? "bar"
  : value1 > value2 ? "baz" : null;

// Удачная реализация
const maybeNull = value1 > value2 ? 'baz' : null;

const foo = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// Удачная реализация
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

<a name="blocks"></a>
# Блоки

Используйте фигурные скобки, когда блок кода занимает несколько строк. 

```javascript
// Неудачная реализация
if (test) return false;

// Удачная реализация
if (test)
  return false;


// Неудачная реализация
function foo() { return false; }

// Удачная реализация
function bar() {
  return false;
}
```

Если в блоке `if` всегда выполняется оператор `return`, последующий блок `else` не нужен. `return`  внутри блока `else if`, следующем за блоком `if`, который содержит `return`, может быть разделён на несколько блоков `if`. 

```javascript
// Неудачная реализация
function foo() {
  if (x) {
    return x;
  } else {
    return y;
  }
}

// Неудачная реализация
function cats() {
  if (x) {
    return x;
  } else if (y) {
    return y;
  }
}

// Неудачная реализация
function dogs() {
  if (x) {
    return x;
  } else {
    if (y) {
      return y;
    }
  }
}

// Удачная реализация
function foo() {
  if (x) {
    return x;
  }

  return y;
}

// Удачная реализация
function cats() {
  if (x) {
    return x;
  }

  if (y) {
    return y;
  }
}

// Удачная реализация
function dogs(x) {
  if (x) {
    if (z) {
      return y;
    }
  } else {
    return z;
  }
}
```

<a name="semicolons"></a>
# Точка с запятой

Точка с запятой `;` ставится обязательно везде.

<a name="events"></a>
# События

Когда привязываете данные к событию (например, события `DOM` или какие-то собственные события, как `Backbone` события), передавайте литерал объекта (также известный как «хэш») вместо простого значения. Это позволяет другим разработчикам добавлять больше данных без поиска и изменения каждого обработчика события. К примеру, вместо:

```javascript
// Неудачная реализация
$(this).trigger('listingUpdated', listing.id);

// ...

$(this).on('listingUpdated', (e, listingID) => {
  // делает что-то с listingID
});
```

предпочитайте:

```javascript
// Удачная реализация
$(this).trigger('listingUpdated', { listingID: listing.id });

// ...

$(this).on('listingUpdated', (e, data) => {
  // делает что-то с data.listingID
});
```

<a name="jquery"></a>
# jQuery

Начинайте названия переменных, хранящих объект jQuery, со знака `$`.

```javascript
// Неудачная реализация
const sidebar = $('.sidebar');

// Удачная реализация
const $sidebar = $('.sidebar');

// Удачная реализация
const $sidebarBtn = $('.sidebar-btn');
```

Кэшируйте jQuery-поиски.

```javascript
// Неудачная реализация
function setSidebar() {
  $('.sidebar').hide();

  // ...

  $('.sidebar').css({
    'background-color': 'pink',
  });
}

// Удачная реализация
function setSidebar() {
  const $sidebar = $('.sidebar');
  $sidebar.hide();

  // ...

  $sidebar.css({
    'background-color': 'pink',
  });
}
```

Для поиска в DOM используйте каскады `$('.sidebar ul')` или селектор родитель > ребёнок `$('.sidebar > ul')`.

Используйте функцию `find` для поиска в сохранённых jQuery-объектах.

```javascript
// Неудачная реализация
$('ul', '.sidebar').hide();

// плохо
$('.sidebar').find('ul').hide();

// Удачная реализация
$('.sidebar ul').hide();

// Удачная реализация
$('.sidebar > ul').hide();

// Удачная реализация
$sidebar.find('ul').hide();
```