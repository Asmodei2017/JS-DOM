#### Работа с  DOM узлами и Асинхронность JS
## DOM
- [выбор узла елемента](#ПОИСК)
- [работа с атрибутами](#АТРИБУТЫ)
- [dom-свойства](#DOM-СВОЙСТВА)
- [работа с классами](#КЛАССЫ)
- [Объект CSSStyleDeclaration](#Объект_CSSStyleDeclaration)
  - [CSS переменные](#CSS_variables)
- [создание и вставка DOM узлов](#DOM-УЗЛЫ)
- [удаление узлов](#Удаление)


------------
Дополнительные источники

[Что такое DOM и чем не является](https://getpocket.com/a/read/2435409919)

### ПОИСК 

#### Новые методы
`elem.querySelector(selector)`  Используется когда мы заведомо знаем, что подходящий элемент только `один`.
  - Возвращает не все, а только первый элемент, соответствующий CSS-селектору selector. Иначе говоря – ищется только первое совпадение, после чего поиск прекращается.
  - Если ничего не найдено, вернет null.

`elem.querySelectorAll(selector)`  Используется когда мы заведомо знаем, что подходящих элементов `более одного`.
  - Возвращает псевдомассив всех элементов внутри elem, удовлетворяющих CSS-селектору selector.
  - Псевдо-классы в selector, такие как :hover и :active, также поддерживаются.
  - Если ничего не найдено вернет пустой массив.

#### Устаревшие методы
`document.getElementById(id)`	Выбирает дом узел по идентификатору id. Возвращает ссылку на найденый DOM-узел или null если ничего не найдено.

`elem.getElementsByTagName(tag)`	Ищет все элементы с заданным тегом tag внутри элемента elem и возвращает их в виде списка

`elem.getElementsByClassName(cls)`	Возвращает коллекцию элементов с классом cls. Находит элемент и в том случае, если у него несколько классов, а искомый – один из них.

------------


### АТРИБУТЫ

#### Работа с атрибутами тегов HTML

`elem.hasAttribute(name)`	Проверяет наличие аттрибута, `ВОЗВРАЩАЕТ TRUE/FALSE`

`elem.getAttribute(name)`	ПОЛУЧАЕТ значение атрибута и возвращает его

`elem.setAttribute(name, value)`	УСТАНАВЛИВАЕТ атрибут

`elem.removeAttribute(name)`	УДАЛЯЕТ атрибут

`elem.attributes`	свойство, возвращает КОЛЛЕКЦИЮ всех атрибутов элемента

------------


### DOM-СВОЙСТВА

`.hidden` Работает так же, как style = "display: none". Возможные значния true или false.

`.value` Содержит контент input, select, textarea.

`.href`	 Содержимое атрибута href ссылки.

`.alt`	 Альтернативный текст изображения.  

------------


### КЛАССЫ

#### Методы для работы с классами элемента. Оперирует значениями атрибута class="..." тегов HTML

`elem.classList.contains(cls)`	проверяет есть ли такой класс в значение атрибута class="" элемента `ВОЗВРАЩАЕТ TRUE/FALSE` 

`elem.classList.add(cls)`	добавляет класс cls в значение атрибута class="" элемента 

`elem.classList.remove(cls)`	удаляет класс cls в значение атрибута class="" элемента 

`elem.classList.toggle(cls)`	если класса cls нет, добавляет его, если есть - удаляет.

------------

### Объект_CSSStyleDeclaration

[почитать](#https://medium.com/@lucyhackwrench/%D1%87%D1%82%D0%BE-%D0%B7%D0%B0-%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82-cssstyledeclaration-%D0%B8-%D0%BE%D1%82%D0%BA%D1%83%D0%B4%D0%B0-%D0%BE%D0%BD-%D0%B1%D0%B5%D1%80%D0%B5%D1%82%D1%81%D1%8F-9fbee0c634ca)
Объект CSSStyleDeclaration — это объект, который возвращается, когда мы хотим получить значение стиля из JS

Объект CSSStyleDeclaration 
свойства:

CSSStyleDeclaration.cssText - возвращает/устанавливает текстовое представление CSS стиля.
CSSStyleDeclaration.length - возвращает КОЛИЧЕСВО стилей CSS.
CSSStyleDeclaration.parentRule - возвращает CssRule медиа-запроса CSS.

методы:

**CSSStyleDeclaration.getPropertyPriority()** - возвращает значение флага important
**CSSStyleDeclaration.getPropertyValue()** - возвращает значение свойства
**CSSStyleDeclaration.item()** - возвращает имя свойства
**CSSStyleDeclaration.removeProperty()** - удаляет свойство из CSS Declaration Block
**CSSStyleDeclaration.setProperty()** - меняет существующее или создает новое свойство

### CSS_variables
Стандартными методами получения/установки переменных CSS3 являются .setProperty() и .getPropertyValue().
Если переменные являются глобальными (объявлено в :root), то можно использовать следующее для получения и установки своих значений.

```javascript
// setter
document.documentElement.style.setProperty('--myVariable', 'blue'); 
// параметры метода setProperty (СSS-переменная , новое значение)

// getter
document.documentElement.style.getPropertyValue('--myVariable');
```

------------
### DOM-УЗЛЫ

#### Создание.

`.createElement("тег")` создаст HTML тег указанный аргументом

`innerHTML += <тег> контент </тег>` пишем строку браузер преобразует в валидный код 
 

#### Вставка. 
Сперва указываем **РОДИТЕЛЯ** вставки затем **КУДА** вставляем затем **КАКОЙ** елемент 

##### 1-родитель 2-место вставки  3-созданный елемент

`node.append(nodes)`	добавляет nodes в КОНЕЦ node

`node.prepend(nodes)`	добавляет nodes в НАЧАЛО node

`node.after(nodes)`	добавляет nodes ПОСЛЕ узла node

`node.before(nodes)`	добавляет nodes ПЕРЕД узлом node

`node.replaceWith(nodes)`	добавляет nodes ВМЕСТО node 


#### insertAdjacentHTML/Element/Text

Метод insertAdjacentHTML **парсит указанную строку как HTML и добавляет результирующие узлы в указанное место DOM-дерева**. 

Он **не делает повторный рендеринг** как  innerHTML для существующих элементов внутри элемента-родителя на котором используется. Это делает его намного **быстрее, чем innerHTML**.

```javascript
element.insertAdjacentHTML(position, newElem);
elem.insertAdjacentElement(position, newElem);
elem.insertAdjacentText(position, text);

```

**elem.insertAdjacentElement(position, newElem)** - вставляет в произвольное место не HTML-строку, а элемент newElem.

**elem.insertAdjacentText(position, text)** - создаёт текстовый узел из строки text и вставляет его в указанное место относительно elem.

#### Позиции
**position** - позиция относительно **element** и должна быть одной из следующих значений: 

**beforebegin**	перед element
**afterbegin**	внутрь element, в самое начало контента
**beforeend**	внутрь element, в самый конец контента
**afterend**	после element


------------


#### Удаление.

`elem.remove()` - удаляет elem из DOM

`elem.remove("elem")` - удаляет elem который указан аргументом из elem-который указан вначале. Например если нужно удалить дочерний елемент , который входит в состав родительского елемента  

------------


### ПОЛУЧАЕМ и ВСТАВЛЯЕМ КОНТЕНТ

#### innerHTML   

`elem.innerHTML`  позволяет **получить содержимое элемента в виде строки**. 
Оно доступно как для **чтения** так и для **записи**.

**Используя innerHTML можем добавить что-то внутрь элемента**. `для создания новых DOM-узлов.`

Лучше использовать **insertAdjacentHTML** так как он бысрее. 

#### textContent / innerText

`elem.textContent`    содержит **только текст внутри элемента, за вычетом всех тегов**. textContent доступен для записи, при чем вне зависимости что будет передано в textContent, **данные всегда будут записаны как текст**.

 `elem.innerText`  устаревшая версия. делает тоже что и `elem.textContent`


### HTM5 DATA-АТРИБУТЫ

##### В HTML5 можно создавать произвольный атрибут и получать значения этого атрибута в JavaScript. 
###### Прием использования произвольного атрибута заключается в следующем:

- Создается атрибут общий для группы input: к корню слова date через дефис дописывают произвольный суффикс (например - "data-color").

- Вновь созданному атрибуту присваивается значение, связанное с данным input (например - "red", "blue" и т.д.)

- В JavaScript обращаемся к псевдомассиву элементов input для получения значения input - elem.value

- В JavaScript обращаемся к псевдомассиву элементов input для получения значения атрибута input - elem.dataset.color 

### НАВИГАЦИЯ ПО УЗЛАМ.

 - `elem.parentNode`	Выберет `РОДИТЕЛЯ` elem

##### Псевдомассиы
 - `elem.children`	Псевдо-массив хранит только `ДОЧЕРНИЕ УЗЛЫ-ЭЛЕМЕНТЫ`, то есть `ТЕГИ`

 - `elem.childNodes`	Псевдо-массив хранит `ВСЕ ДОЧЕРНИЕ` элементы, то есть `ТЕГИ` и `ТЕКСТОВЫЕ`

##### Первый внутри родителя
 - `elem.firstElementChild`	Выберет `ПЕРВЫЙ ДОЧЕРНИЙ УЗЕЛ-ЭЛЕМЕНТ` внутри elem, то есть `ТЕГ`

 - `elem.firstChild`	Выберет `ПЕРВЫЙ ДОЧЕРНИЙ элемент`  внутри elem, включая `ТЕКСТОВЫЕ` узлы.


##### Последний внутри родителя
 - `elem.lastElementChild`	Выберет `ПОСЛЕДНИЙ ДОЧЕРНИЙ УЗЕЛ-ЭЛЕМЕНТ` внутри elem. то есть `ТЕГ`

 - `elem.lastChild	` Выберет `ПОСЛЕДНИЙ ДОЧЕРНИЙ элемент`  внутри elem, включая `ТЕКСТОВЫЕ` узлы.

##### Слева от соседа
 - `elem.previousElementSibling`	Выберет `УЗЕЛ-ЭЛЕМЕНТ` "слева" от elem (его предыдущего соседа) 

 - `elem.previousSibling`	Выберет `элемент` "слева" от elem (его предыдущего соседа)


##### Справа от соседа
 - `elem.nextElementSibling`	Выберет `УЗЕЛ-ЭЛЕМЕНТ` "справа" от elem (его предыдущего соседа)

 - `elem.nextSibling`	Выберет `элемент` "справа" от elem (его следующего соседа)

//////////////////////////////////////////////////////

## СОБЫТИЯ

#### addEventListener
`addEventListener()`  добавить слушателя события. 

##### Принимает три параметра

- `event`	  имя/тип события, например click, передается как строка
- `handler`	ссылка на функцию, которую надо поставить обработчиком 
- `phase`	  Необязательный аргумент, «фаза», на которой обработчик должен сработать. Этот аргумент редко нужен.

###### Хорошей практикой считается когда функцию обработчик выносим за пределы. А в качестве аргумента при вызове слушателя события передаем ссылку на нее. 
###### Также не стоит использовать аргументом слушателя АНОНИМНУЮ функцию `() => { }` так как на нее не получится получить ссылку. 

#### removeEventListener
`removeEventListener`  Удаление слушателя события осуществляется вызовом removeEventListener. Аргументы те же что у addEventListener

###### При удалении слушателя , вторым аргументом, должна быть ТАЖЕ функция как и при добавлении слушателя. 


##### Детали произошедшего браузер записывает в «объект события» event, который передаётся первым аргументом в обработчик. 
##### У этого объекта много методов, таких как .target, .currentTarget , .nodeName, .clientX и  .clientY и др. 


#### Всплытие

##### При клике или ином другом событии, происходит следующее: 

- capturing phase - событие начинается на window и тонет до самого глубокого целевого элемента

- target phase - событие дошло до самого глубокого целевого элемента

- bubbling phase - событие всплывает от самого глубокого целевого элемента до window

##### После того  как событие дошло до цели , в объект `event` запишется все информация о целевом елементе, которую в дальнейшем мы можем использовать. После чего наступает фаза всплытия и "пакет с информацией" летит наверх , где мы можем его перехватить. Для этого используется делегирование. 

##### Фазу всплытия можно контролировать

`event.stopPropagation()` останавливает дальнейшее всплытие. тоесть событие отработает на текущей цели и дальше не всплывет

#### Делегирование

##### Назначаем слушателя событий родителю, который будет отлавливать события которые будут происходить с дочерними елементами. Это позволяет не писать событие для каждого елемента а ограничится одним. Далее через event.target можно узнать на каком елементе произошло событие. С помощтю event.nodeName , который возвращает имя тега с которым произошло событие, узнаем тег и можем проводить разные проверки и условия.  

`event.target`  получаем ССЫЛКУ на елемент на котором произошло событие

`event.nodeName` возвращает ИМЯ ТЕГА в виде строки в верхнем регистре - 'IMG', 'DIV' и т.п. С помощью этого метода отсеиваем ненужные события. Например нам нужно получить значение атрибута тега <img>, на родителя повесили слушателя событий. При таком раскладе мы будем получать события для всех елементов внутри. С помощью метода можем сделать проверку `if (event.target.nodeName !== 'IMG') return` если целевой елемент НЕ <img> , то выходим из функции. 

#### Действия браузера по умолчанию

##### Браузер имеет встроенные действия при ряде событий – переход по ссылке, отправка формы и т.п. Как правило, их можно отменить.

##### Например:

- Клик по ссылке инициирует переход на новый URL.
- Нажатие на кнопку «отправить» в форме – отсылку ее на сервер.
- Двойной клик на тексте – инициирует его выделение.
- Основной способ это воспользоваться объектом события. 

##### Для отмены действия браузера существует стандартный метод 

`event.preventDefault()` отменяет действия браузера по умолчанию

#### Загрузка документа

##### процесс загрузки HTML-документа, состоит из трёх стадий

- DOMContentLoaded – браузер полностью загрузил HTML и построил DOM-дерево.
- load – браузер загрузил все ресурсы.
- beforeunload/unload – уход со страницы.

##### Мы будем вешать слушателей когда браузер построил DOM дерево

`document.addEventListener("DOMContentLoaded", ()=> { тут вешаем все свои слушатели})` 
- слушатели помещаем внутрь 
- все функции которые будут описывать нужные нам дейсвтвия помещаем вне

/////////////////////////////////////////////////

## АСИНХРОННОСТЬ

Асинхронный код **ВСЕГДА будет выполняться только после того , как закончит свое выполнение синхронный**. После чего, если в очереди есть другие асинхронные операции, javascript выполнит те, которые быстрее выполнятся. 

#### setTimeout и clearTimeout

`setTimeout( () => {CODE}, 2000);` принимает 2 аргумента
- callback-функцию которая будет вызвана по истечении времени
- время через которое сработает функция
Возвращает цифровой идентификатор созданного таймера, это необходимо для возможность его удаления.
 
`const timerId = setTimeout(callback, delay);` в переменную будет записан ID

##### Если нужно отменить вызов функции внутри таймаута, используется функция `clearTimeout(id)` , которая получает идентификатор (id) таймера и очищает (удаляет) его.
 
`clearTimeout(timerId);` удалит таймер timerId

#### setInterval и clearInterval

###### Интервалы - это более простой способ повторения кода снова и снова, с установленным промежутком времени повторений.
###### Функция `setInterval` имеет синтаксис, аналогичный `setTimeout`.

###### B отличие от `setTimeout`, она запускает выполнение функции не один раз, а регулярно повторяет её через указанный интервал времени (delay).
###### Остановить исполнение можно вызовом `clearInterval(id)`.


####  Promise

Promise (обещание, промис) - **объект, представляющий текущее состояние асинхронной операции**. 
Удобный способ организации асинхронного кода.

У промиса есть 2 состояния:

1. **Pending** - ожидание, исходное состояние при создании промиса
2. **Settled** - выполнен, которое в свою очередь имеет 2 варианта результата.
   2.1 ***fullfilled*** - выполнено успешно
   2.2 ***rejected*** - выполнено с ошибкой

Способ использования, в общих чертах, такой:

1. Код, которому надо сделать что-то асинхронно, создаёт объект promise и возвращает его.
2. Внешний код, получив promise, навешивает на него обработчики.
3. По завершении процесса асинхронный код переводит promise в состояние fulfilled (с результатом) или rejected (с ошибкой). При этом автоматически вызываются соответствующие обработчики во внешнем коде.

**СОЗДАНИЕ**
Cоздается как экземпляр класса Promise(fn) с одной функцией в качестве аргумента. Вызов new Promise немедленно исполнит функцию, переданную в качестве аргумента. Цель этой функции состоит в информировании экземпляра (промиса), когда событие, с которым он связан, будет завершено.
```javascript
const promise = new Promise((resolve, reject) => {
// Эта функция будет вызвана автоматически

// В ней можно делать любые асинхронные операции.
// Когда они завершатся — нужно вызвать одно из:
// resolve(результат) при успешном выполнении
// reject(ошибка) при ошибке
});

Параметры передаваемой функции:

**resolve(arg)** - функция которую необходимо вызвать при успешной операции. Переданный в нее аргумент будет значением выполненного промиса.
**reject(arg)** - функция которую необходимо вызвать при ошибке. Переданный в нее аргумент будет значением ошибки которое можно будет обработать.
```
В переменную promise будет записан объект обещания в состоянии pending, а через 2 секунды, после того как будет вызван resolve("success!"), промис перейдет в состояние resolved.
```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("success!");
  }, 2000);
});
```

**ИСПОЛЬЗОВАНИЕ**

Метод .then  - передаются две функции которые будут вызваны когда промис перейдет в состояние выполнен (settled). 
**Выполниться Promise может удачно(resolve) и неудачно(reject)**.

```javascript 
.then(resolve, reject)   
```

- resolve(arg) - будет вызвана при **успешном** выполнении промиса, и **получит результат промиса как аргумент (то, что передаем в вызов resolve())**.
- reject(arg) - будет вызвана при выполнении промиса **с ошибкой**, и получит **ошибку как аргумент (то, что передаем в вызов reject())**.

Метод .catch используется для обработки ошибки, в конце цепочки.
```javascript
.catch(error => console.log(error));
``` 

Цепочки 
Удобно после того как вернулся Promise, работать с данными используя цепочки. 
В методе .then будем использовать успешные результаты а в методе .catch будем отлавливать неудачные. 

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(5);
  }, 2000);
});

promise
  .then(value => {
    console.log(value); // 5
    return value * 2;
  })
  .then(value => {
    console.log(value); // 10
    return value * 3;
  })
  .then(value => {
    console.log(value); // 30
  })
  .catch(err => console.log(err));
```
**При возникновении ошибки в любом месте цепочки, выполнение всех последующих then отменяется, а управление передается методу catch.**


### Promise.all и Promise.race

Иногда бывают ситуации когда нам необходимо дождаться выполнения не одного, а сразу набора промисов, и только тогда что-то сделать. 
Бывают и такие ситуации когда из набора промисов необходимо дождаться выполнения любого одного,проигнорировав остальные.

#### Promise.all
**Promise.all([promise1, promise2, ...])** - статический метод, получает массив промисов и ждет их исполнения, возвращает промис.

При успешном выполнении **всех промисов** из массива, промис возвращаемый из Promise.all перейдет в состояние settled -> fullfilled, а его значением будет массив результатов исполнения каждого промиса.

**Если в массиве промисов хотябы один исполнился с ошибкой, то перейдет в состояние settiled -> rejected, а значением промиса будет ошибка.**

```javascript
const makePromise = (text, delay) =>{
  return new Promise(resolve => setTimeout(() => resolve(text), delay));
}
const promiseA = makePromise("promiseA", 1000);
const promiseB = makePromise("promiseB", 3000);

// выполнится спустя 3 секунды,
// когда выполнится второй промис с задержкой в 3c.
// Первый выполнится через секунду и просто будет готов
Promise.all( [promiseA, promiseB] )
  .then(result => console.log(result)) //["promiseA", "promiseB"]
  .catch(err => console.log(err));
  ```

#### Promise.race

**Promise.race([promise1, promise2, ...])** - статический метод, получает массив промисов и возвращает обещание. 
Когда **хотябы одно** обещание в массиве исполнилось, исполнится возвращаемый промис.

```javascript
const makePromise = (text, delay) =>
  new Promise(resolve => setTimeout(() => resolve(text), delay));

const promiseA = makePromise("promiseA", 1000);
const promiseB = makePromise("promiseB", 3000);

// выполнится спустя 1 секунду, когда выполнится
// самый быстрый promiseA с задержкой в 1c.
// Второй промис promiseB будет проигнорирован
Promise.race( [promiseA, promiseB] )
  .then(result => console.log(result)) // "promiseA"
  .catch(err => console.log(err));
```

////////////////////////////////////////////////

## Объект Date

`let date = new Date();` создается путем объявления `new Date()`

###### Если не были переданы аргументы, то JavaScript просто вернет текущую дату и время в ВИДЕ СТРОКИ

#### Аргументы new Date 
- new Date(year, month, date, hours, minutes, seconds, ms)

#### Методы 

##### Геттеры 

`getDate()` - возвращает день месяца от 1 до 31
`getDay()` - возвращает день недели от 0 до 6
`getMonth()` - возвращает месяц от 0 до 11
`getFullYear()` - возвращает год из 4 цифр
`getHours()` - возвращает час
`getMinutes()` - возвращает минуты
`getSeconds()` - возвращает секунды
`getMilliseconds()` - возвращает миллисекунды
`getTime()` - возвращает кол-во миллисекунд прошедших со старта эпохи Unix
`getTimezoneOffset()` - возвращает разницу между местным и UTC-временем, в минутах

##### Сеттеры 

`setDate()` - устанавливает день месяца
`setDay()` - устанавливает день недели
`setMonth()` - устанавливает месяц
`setFullYear()` - устанавливает год
`setHours()` - устанавливает час
`setMinutes()` - устанавливает минуты
`setSeconds()` - устанавливает секунды
`setMilliseconds()` - устанавливает миллисекунды
`setTime()` - устанавливает кол-во миллисекунд c начала эпохи Unix
