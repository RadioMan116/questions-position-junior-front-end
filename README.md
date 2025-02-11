# questions position junior front-end

# Frontend Interview Materials for Junior React Developer

Этот репозиторий содержит материалы для проверки знаний кандидата на позицию Junior Frontend Developer с использованием React, TypeScript, Redux и других современных технологий.

---

## Содержание

- [Теоретические вопросы и ответы](#теоретические-вопросы-и-ответы)
    - [1. Типы данных и особенности undefined/ null](#1-типы-данных-и-особенности-undefined-null)
    - [2. Области видимости и разница между var/let/const](#2-области-видимости-и-разница-между-varletconst)
    - [3. Цикл событий (event loop)](#3-цикл-событий-event-loop)
    - [4. JSX и его роль в React](#4-jsx-и-его-роль-в-react)
    - [5. Хуки: useEffect vs useLayoutEffect](#5-хуки-useeffect-vs-uselayouteffect)
    - [6. Virtual DOM и процесс reconciliation](#6-virtual-dom-и-процесс-reconciliation)
    - [7. TypeScript](#7-typescript)
    - [8. Redux/RTK](#8-reduxrtk)
- [Live Coding Задания](#live-coding-задания)
    - [Задание 1. Реализация простого счетчика](#задание-1-реализация-простого-счетчика)
    - [Задание 2. Что выведет в консоль](#задание-2-что-выведет-в-консоль)
    - [Задание 3. Найти и исправить ошибки](#задание-3-найти-и-исправить-ошибки)
        - [Вариант с ошибками](#вариант-с-ошибками)
        - [Исправленный вариант с комментариями и альтернативными решениями](#исправленный-вариант-с-комментариями-и-альтернативными-решениями)

---

## Теоретические вопросы и ответы

Ниже приведён итоговый пакет материалов для проверки джуна по фронтенду. В нём собраны ответы на теоретические вопросы, решения для live coding заданий и пример задания «Найти и исправить ошибки» с двумя вариантами (исходный с ошибками и исправленный с комментариями и альтернативами). Эти ответы можно предоставить как вам, так и вашему техдиру, чтобы он понимал суть вопросов и решений.

---

## Теоретические вопросы и ответы

### 1. JavaScript – Типы данных и особенности undefined/ null
**Вопрос:**  
Какие типы данных существуют в JavaScript и чем отличаются `undefined` от `null`?

**Ответ:**  
**Примитивные типы:**
- **Number:** для чисел (целые, дробные, специальные значения `NaN`, `Infinity` и т.д.).
- **String:** для строк.
- **Boolean:** для логических значений (`true` и `false`).
- **Undefined:** значение переменной, которой не было присвоено значение; также результат отсутствия возвращаемого значения в функции.
- **Null:** преднамеренно заданное «отсутствие значения»; используется для явного указания, что переменная не содержит значимого значения.
- **Symbol (ES6):** для создания уникальных идентификаторов.
- **BigInt (ES2020):** для представления чисел произвольной длины.

**Ссылочные типы:**
- **Object:** включает объекты, массивы, функции, даты и т.д.

**Отличия:**
- `undefined` означает отсутствие значения вследствие неинициализации переменной или отсутствия свойства.
- `null` — это намеренное указание на отсутствие объекта.
- При этом тип `undefined` имеет тип `"undefined"`, а `null` — исторически имеет тип `"object"`.

---

### 2. JavaScript – Области видимости и разница между var/let/const
**Вопрос:**  
Расскажи про области видимости в JavaScript и в чем разница между `var`, `let` и `const`?

**Ответ:**  
**Области видимости (scoping):**
- **Функциональная область видимости:**  
  Переменные, объявленные с `var`, видны внутри функции, в которой они объявлены. Они также поднимаются (hoisting) в начало функции.
- **Блочная область видимости:**  
  Переменные, объявленные с `let` и `const`, ограничены блоком (например, фигурными скобками в условных конструкциях или циклах).

**Различия:**
- **var:**
    - Область видимости — функция.
    - Повторное объявление в одной области допустимо.
    - Подвержен подъёму (hoisting).
```javascript
if (true) {
var varVariable = 'Меня видно за пределами блока!';
}
console.log(varVariable); // "Меня видно за пределами блока!"
```
<p>Но такой хойстинг может привести к странным ситуациям:</p>
```javascript
console.log(testVar); // undefined
var testVar = 'Это тест!';
```
<p>Переменная поднята, но она не инициализирована на момент вызова.</p>
- **let:**
    - Область видимости — блок.
    - Нельзя повторно объявлять в одном блоке.
    - Имеет «временную мёртвую зону» (TDZ) до инициализации.

```javascript
if (true) {
let letVariable = 'Меня видно только в блоке!';
}
console.log(letVariable); // Ошибка: letVariable не определена
```

- **const:**
    - Тоже блочная область видимости.
    - Обязательно инициализируется при объявлении.
    - Нельзя переназначать значение (хотя для объектов/массивов можно менять содержимое).

```javascript
const myConstant = 10;
myConstant = 20; // Ошибка: нельзя изменить значение const
```


```javascript
const obj = { name: 'John' };
obj.name = 'Renat'; // Это работает
obj = {}; // Ошибка: нельзя изменить саму ссылку на объект
```
---

### 3. JavaScript – Что такое цикл событий (event loop) и как он работает?
**Вопрос:**  
Что такое цикл событий (event loop) и как он работает?

**Ответ:**  
Event loop — это бесконечный процесс, который управляет выполнением задач в JavaScript. Он распределяет задачи между синхронным кодом (который выполняется в стеке вызовов) и асинхронными операциями, используя очереди:
- **Микротаски (microtasks):** включают обработчики промисов, `queueMicrotask`, `MutationObserver` и выполняются после завершения синхронного кода (с более высоким приоритетом).
- **Макротаски (macrotasks):** включают `setTimeout`, `setInterval`, DOM-события и другие. Они выполняются после микротасок.

Порядок выполнения:
1. Выполняется весь синхронный код (стек вызовов).
2. Затем – все микротаски.
3. После – одна макротаска из очереди, затем снова микротаски и так далее.

_Пример результата кода:_
```js
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');
```
**Вывод:**
```
Start
End
Promise
Timeout
```
Микротаски (Promise) выполняются раньше макротасок (setTimeout), несмотря на нулевую задержку.

---

### 4. React – Что такое JSX и зачем он нужен в React? Можно ли использовать React без JSX?
**Вопрос:**  
Что такое JSX и зачем он нужен в React? Можно ли использовать React без JSX?

**Ответ:**  
**JSX** — это синтаксическое расширение для JavaScript, которое позволяет писать HTML-подобный код внутри JavaScript. Он делает код компонентов более читаемым и удобным для написания, поскольку упрощает создание иерархии компонентов.  
Можно использовать React без JSX, напрямую вызывая `React.createElement()`, но это менее удобно.

_Пример с JSX:_
```jsx
function Greeting() {
  return <h1>Привет, мир!</h1>;
}
```
_Пример без JSX:_
```jsx
function Greeting() {
  return React.createElement('h1', null, 'Привет, мир!');
}
```

---

### 5. React – Какие хуки ты использовал? В чем разница между useEffect и useLayoutEffect?
**Вопрос:**  
Какие хуки ты использовал? В чем разница между `useEffect` и `useLayoutEffect`?

**Ответ:**  
<h3>Основные хуки:</h3>
  <ul>
    <li><code>useState</code>: Позволяет работать с локальным состоянием. Он принимает начальное значение и возвращает текущее значение и функцию для его обновления. Компонент перерисовывается после каждого вызова этой функции.</li>
    <li><code>useEffect</code>: Используется для выполнения побочных эффектов в функциональных компонентах, таких как запросы, изменения DOM и подписки. Вызывается асинхронно после отрисовки компонентов. Принимает массив зависимостей, определяющий, когда эффект должен вызываться. Если массив пустой, эффект вызывается только при монтировании компонента. Если массив не передан, эффект будет вызываться при каждом рендере. Можно вернуть функцию очистки, которая вызывается при изменении зависимостей или размонтировании компонента.</li>
    <li><code>useLayoutEffect</code>: Работает аналогично <code>useEffect</code>, но выполняется синхронно после всех изменений DOM и перед обновлением браузера. Это полезно для измерений и изменений, которые должны быть видны пользователю сразу.</li>
    <li><code>useRef</code>: Возвращает объект с свойством <code>current</code>, позволяя получать доступ к элементам или сохранять значения, которые не вызывают повторный рендер при изменении. Мутирование <code>current</code> не приводит к повторному рендеру, так как это один и тот же объект при каждом рендере.</li>
    <li><code>useContext</code>: Используется для получения текущего значения контекста, позволяя избежать передачи пропсов через несколько уровней.</li>
    <li><code>useReducer</code>: Альтернатива <code>useState</code> для управления более сложным состоянием. Позволяет использовать редьюсеры, что особенно полезно для управления состоянием в больших компонентах.</li>
    <li><code>useCallback</code>: Мемоизирует функции, принимая массив зависимостей. Если зависимости изменяются, ссылка на функцию также изменяется, что помогает избежать лишних рендеров дочерних компонентов.</li>
    <li><code>useMemo</code>: Мемоизирует возвращаемые значения, принимая функцию обратного вызова и массив зависимостей. Возвращает мемоизированное значение, что помогает оптимизировать производительность, избегая лишних вычислений.</li>
  </ul>

<h3>Разница между <code>useEffect</code> и <code>useLayoutEffect</code>:</h3>
  <p>
    <code>useLayoutEffect</code> работает так же, как и <code>useEffect</code>, с тем отличием, что выполняется синхронно и может блокировать отрисовку браузера. Это означает, что <code>useLayoutEffect</code> срабатывает после всех изменений DOM, но до того, как браузер обновит отображение. Это полезно для случаев, когда необходимо производить измерения или изменения, которые должны быть видны пользователю сразу.
  </p>
  <p>
    В отличие от этого, <code>useEffect</code> работает асинхронно и не блокирует рендер. Он срабатывает после отрисовки, что делает его более подходящим для работы с данными, запросами и подписками, которые не требуют немедленного отображения результатов.
  </p>
</div>

---

### 6. React – Что такое Virtual DOM и React Reconciliation, и как они работают вместе в React?
**Вопрос:**  
Что такое Virtual DOM и как работает процесс reconciliation в React?

**Ответ:**
- **Virtual DOM:** Легковесное представление реального DOM в памяти, которое React использует для отслеживания изменений в состоянии компонентов.
- **Reconciliation (согласование):** При изменении состояния React создаёт новое представление Virtual DOM, сравнивает его с предыдущим (алгоритм diffing) и вычисляет минимальный набор изменений, которые необходимо внести в реальный DOM. Это позволяет обновлять только изменённые части, повышая производительность приложения.

---

### 7. TypeScript – Что такое TypeScript и для чего он нужен в React?
**Вопрос:**  
Что такое TypeScript, для чего он используется и какие преимущества даёт при разработке на React?

**Ответ:**  
**TypeScript** — это надстройка над JavaScript, добавляющая статическую типизацию.  
_Преимущества:_
- Обнаружение ошибок на этапе компиляции.
- Улучшенное автодополнение, рефакторинг и поддержка кода.
- Улучшение читаемости и документированности благодаря явному описанию типов.
- В React помогает создавать компоненты с чёткими контрактами (например, через типизацию пропсов и состояния).

---

### 8. Redux/RTK – Что такое Redux, зачем он нужен, и преимущества Redux Toolkit (RTK)
**Вопрос:**  
Что такое Redux, зачем он нужен, и пробовал ли ты использовать Redux Toolkit (RTK)? Какие преимущества RTK даёт по сравнению с классическим Redux?

**Ответ:**
- **Redux:** Библиотека для управления состоянием приложения с централизованным хранилищем (store). Состояние обновляется предсказуемо через экшены и редьюсеры.
- **Redux Toolkit (RTK):** Официальная обёртка над Redux, снижающая количество шаблонного кода.  
  _Преимущества RTK:_
    - Меньше кода и более понятный API.
    - Встроенные средства для иммутабельного обновления (например, через Immer).
    - Лучшая организация кода и преднастройки для типизации в TypeScript.

---

## Live Coding Задания

### Задание 1. Реализация простого счетчика
**Условие:**  
Напиши React-компонент, который отображает число и имеет две кнопки для увеличения и уменьшения значения. Используй хук `useState`.

**Пример решения:**

```jsx
import React, { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  const handleIncrement = () => setCount(prev => prev + 1);
  const handleDecrement = () => setCount(prev => prev - 1);

  return (
    <div>
      <h2>Счётчик: {count}</h2>
      <button onClick={handleIncrement}>Увеличить</button>
      <button onClick={handleDecrement}>Уменьшить</button>
    </div>
  );
};

export default Counter;
```

---

### Задание 2. Что выведет в консоль
**Пример кода:**

```js
console.log('Start');

setTimeout(() => {
  console.log('Timeout');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise');
});

console.log('End');
```

**Ответ и объяснение:**  
Вывод в консоль будет таким:
```
Start
End
Promise
Timeout
```  
Объяснение:
- Сначала выполняется весь синхронный код: выводятся "Start" и "End".
- Затем выполняются все микротаски (обработчики промисов) – выводится "Promise".
- После этого выполняется макротаска из `setTimeout` – выводится "Timeout".

---

### Задание 3. «Найти и исправить ошибки»

#### Вариант с ошибками

```jsx
import React, { useEffect, useState } from 'react';

interface ItemListProps {
  items?: string[];
}

const ItemList = ({ items }) => {
  useEffect(() => {
    console.log('Component mounted or updated, items count:', items.length);
  });
  
  const [count, setCount] = useState(0);

  return (
    <div>
      <ul>
        {items.map(item => (
          <li>{item}</li>
        ))}
      </ul>
      <div style={{ marginTop: '1rem' }}>
        <p>Счётчик: {count}</p>
        <input
          type="number"
          value={count}
          onChange={(e) => setCount(Number(e.target.value))}
          style={{ marginRight: '0.5rem' }}
        />
        <button onClick={setCount(count + 1)}>
          Увеличить
        </button>
        <button onClick={setCount(count - 1)} style={{ marginLeft: '0.5rem' }}>
          Уменьшить
        </button>
      </div>
    </div>
  );
};

export default ItemList;
```

#### Исправленный вариант с комментариями и альтернативными решениями

```tsx
import React, { useEffect, useState } from 'react';

// 5) Определяем интерфейс для пропсов и используем React.FC для типизации компонента
interface ItemListProps {
  items?: string[];
}

// 4) Задаем дефолтное значение для items и применяем типизацию через React.FC
const ItemList: React.FC<ItemListProps> = ({ items = [] }) => {
  // 6) Состояние счётчика
  const [count, setCount] = useState(0);

  // 1) useEffect с массивом зависимостей, чтобы эффект выполнялся только при изменении items
  useEffect(() => {
    console.log('Component mounted or updated, items count:', items.length);
  }, [items]);

  // 2) Проверяем, что items действительно является массивом.
  // Вариант A: проверка в начале компонента и возврат сообщения об ошибке
  if (!Array.isArray(items)) {
    return <div>Ошибка: неверный тип данных для items</div>;
  }

  // 6) Альтернативный вариант обработчиков для обновления счётчика через callback-версию setCount
  const plusHandler = (e: React.MouseEvent<HTMLButtonElement>) => {
    setCount(prevCount => prevCount + 1);
  };

  const minusHandler = (e: React.MouseEvent<HTMLButtonElement>) => {
    setCount(prevCount => prevCount - 1);
  };

  return (
    <div>
      <ul>
        { 
          // 3) Добавляем уникальный атрибут key для каждого элемента списка
          // Вариант 1: стандартная проверка
          items.map((item, index) => (
            <li key={index}>{item}</li>
          ))
          
          /*  
          Альтернативные варианты для проверки, что items является массивом:
          
          Вариант 2 (тернарный оператор):
          {Array.isArray(items)
            ? items.map((item, index) => (
                <li key={index}>{item}</li>
              ))
            : <p>Ошибка: items не является массивом</p>}
          
          Вариант 3 (логический оператор &&):
          {Array.isArray(items) && items.map((item, index) => (
              <li key={index}>{item}</li>
            ))}
          {!Array.isArray(items) && <p>Ошибка: items не является массивом</p>}
          */
        }
      </ul>

      {/* Секция со счётчиком */}
      <div style={{ marginTop: '1rem' }}>
        <p>Счётчик: {count}</p>
        <input
          type="number"
          value={count}
          onChange={(e) => setCount(Number(e.target.value))}
          style={{ marginRight: '0.5rem' }}
        />
        {/* 6) Обновляем счётчик через callback-версию setCount */}
        <button onClick={() => setCount(prevCount => prevCount + 1)}>
          Увеличить
        </button>
        <button onClick={() => setCount(prevCount => prevCount - 1)} style={{ marginLeft: '0.5rem' }}>
          Уменьшить
        </button>
        {/* Альтернативный вариант с использованием отдельных обработчиков */}
        <button onClick={plusHandler} style={{ marginLeft: '1rem' }}>
          Увеличить (alt)
        </button>
        <button onClick={minusHandler} style={{ marginLeft: '0.5rem' }}>
          Уменьшить (alt)
        </button>
      </div>
    </div>
  );
};

export default ItemList;
```

---

## Итог

**Теоретические вопросы:**
1. Типы данных, особенности `undefined` и `null`.
2. Области видимости, разница между `var`, `let` и `const`.
3. Цикл событий (event loop): микротаски и макротаски, порядок выполнения.
4. JSX и его роль в React, возможность использования без JSX.
5. Хуки в React, различия между `useEffect` и `useLayoutEffect`.
6. Virtual DOM и процесс reconciliation.
7. TypeScript: что это, для чего используется, преимущества.
8. Redux и преимущества Redux Toolkit (RTK).

**Live Coding Задания:**
1. Простой счетчик с использованием `useState`.
2. Анализ порядка вывода в консоли (результат: Start, End, Promise, Timeout).
3. Задание «Найти и исправить ошибки»: представлен исходный вариант с ошибками и исправленный вариант с комментариями и альтернативными решениями (включая проверку типа пропса и обновление счётчика).

Эти материалы позволят проверить базовые знания кандидата, а также его умение находить и исправлять типичные ошибки в React-коде.
