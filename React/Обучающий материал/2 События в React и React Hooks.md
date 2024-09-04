## **1. События в React**

В React обработка событий похожа на обработку событий в обычном JavaScript, но с некоторыми отличиями. События в React используются для взаимодействия с пользователем и обновления состояния компонентов.

### **Обработка событий**

#### 1.1. **onClick**

`onClick` — это событие, которое срабатывает при клике мыши на элемент. Оно используется для обработки пользовательских взаимодействий.

##### Пример использования `onClick`:
```
import React from 'react';

function ClickableButton() {
  function handleClick() {
    alert('Кнопка нажата!');
  }
  return <button onClick={handleClick}>Нажми меня</button>;
}

export default ClickableButton;
```
**Объяснение**:
- `handleClick` — функция, которая вызывается при клике на кнопку.
- `onClick={handleClick}` — атрибут, который привязывает функцию обработки события к кнопке.

#### 1.2. **onChange**

`onChange` — это событие, которое срабатывает при изменении значения в элементе формы, таком как `<input>`, `<textarea>`, или `<select>`.

##### Пример использования `onChange`:
```
import React, { useState } from 'react';

function TextInput() {
  const [value, setValue] = useState('');
  
  function handleChange(event) {
    setValue(event.target.value);
  }

  return (
    <div>
      <input type="text" value={value} onChange={handleChange} />
      <p>Текущее значение: {value}</p>
    </div>
  );
} 

export default TextInput;
```
**Объяснение**:
- `handleChange` — функция, которая обновляет состояние при изменении значения в поле ввода.
- `onChange={handleChange}` — атрибут, который привязывает функцию обработки изменения значения к `<input>`.

#### 1.3. **onSubmit**

`onSubmit` — это событие, которое срабатывает при отправке формы. Используется для обработки данных формы.

##### Пример использования `onSubmit`:
```
import React, { useState } from 'react';

function Form() {
  const [name, setName] = useState('');

  function handleSubmit(event) {
    event.preventDefault(); // Предотвращает перезагрузку страницы
    alert(`Форма отправлена! Имя: ${name}`);

  }

  function handleChange(event) {
    setName(event.target.value);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={name}
        onChange={handleChange}
        placeholder="Введите ваше имя"
      />
      <button type="submit">Отправить</button>
    </form>
  );
}

export default Form;
```
**Объяснение**:
- `handleSubmit` — функция, которая вызывается при отправке формы. `event.preventDefault()` предотвращает перезагрузку страницы.
- `onSubmit={handleSubmit}` — атрибут, который привязывает функцию обработки отправки формы к `<form>`.

---
## **2. Логические операторы и условия**

В React можно использовать логические операторы и условия для управления отображением компонентов и их состоянием.

### **Логические операторы**

#### 2.1. **&& (И)**

Оператор `&&` используется для условного отображения элементов. Если условие слева от `&&` истинно, то отобразится элемент справа от `&&`.

##### Пример использования `&&`:
```
import React, { useState } from 'react';

function ConditionalRendering() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  
  return (
    <div>
      {isLoggedIn && <p>Вы вошли в систему!</p>}
      <button onClick={() => setIsLoggedIn(!isLoggedIn)}>
        {isLoggedIn ? 'Выйти' : 'Войти'}
      </button>
    </div>
  );
}

export default ConditionalRendering;
```
**Объяснение**:
- Если `isLoggedIn` истинно, то отображается текст "Вы вошли в систему!".
- Кнопка переключает состояние `isLoggedIn`, что изменяет отображаемый текст.

#### 2.2. **|| (ИЛИ)**

Оператор `||` используется для задания значений по умолчанию. Если значение слева от `||` ложно, будет возвращено значение справа от `||`.

##### Пример использования `||`:
```
import React from 'react';

function DefaultText({ text }) {
  return (
    <div>
      <p>{text || 'Нет текста для отображения.'}</p>
    </div>
  );
}

export default DefaultText;
```
**Объяснение**:
- Если `text` не передан или является ложным значением, отображается текст "Нет текста для отображения."

---

## **3. React Hooks**

React Hooks — это функции, которые позволяют использовать состояние и другие возможности React без написания классовых компонентов.

### **3.1. useState**

`useState` — это хук, который позволяет функциональным компонентам иметь состояние.

##### Пример использования `useState`:
```
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Инициализация состояния

  return (
    <div>
      <p>Счётчик: {count}</p>
      <button onClick={() => setCount(count + 1)}>Увеличить</button>
      <button onClick={() => setCount(count - 1)}>Уменьшить</button>
    </div>
  );
}

export default Counter;
```
**Объяснение**:
- `useState(0)` инициализирует состояние с начальным значением 0.
- `setCount` используется для обновления значения состояния.

### **3.2. useEffect**

`useEffect` — это хук, который позволяет выполнять побочные эффекты в функциональных компонентах. Эти эффекты могут быть асинхронными операциями, такими как запросы к API, подписка на события и т.д.

##### Пример использования `useEffect`:
```
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds((prevSeconds) => prevSeconds + 1);
    }, 1000);
    // Очистка интервала при размонтировании компонента
    return () => clearInterval(interval);
  }, []);

  return (
    <div>
      <p>Прошло секунд: {seconds}</p>
    </div>
  );
}

export default Timer;
```
**Объяснение**:
- `useEffect` устанавливает интервал, который увеличивает счётчик каждую секунду.
- Возвращаемая функция очистки вызывается при размонтировании компонента, чтобы предотвратить утечки памяти.

`useEffect` часто используется для выполнения побочных эффектов, таких как запросы к API, когда компонент монтируется или обновляется.
```
import React, { useState, useEffect } from 'react';

function UserProfile() {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Функция для получения данных
    async function fetchUserData() {
      try {
        const response = await fetch(
          'https://jsonplaceholder.typicode.com/users/1'
        );
        if (!response.ok) {
          throw new Error('Ошибка сети');
        }
        const data = await response.json();
        setUser(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    fetchUserData();
  }, []); // Пустой массив зависимостей, поэтому эффект выполняется только при монтировании
  if (loading) return <p>Загрузка...</p>;
  if (error) return <p>Ошибка: {error}</p>;

  return (
    <div>
      <h1>Профиль пользователя</h1>
      <p>Имя: {user.name}</p>
      <p>Email: {user.email}</p>
      <p>Город: {user.address.city}</p>
    </div>
  );
}

export default UserProfile;
```

### **3.3. useRef**

`useRef` — это хук, который позволяет создавать и сохранять ссылки на DOM-элементы или любые другие значения, которые не требуют повторного рендеринга при изменении.

##### Пример использования `useRef`:
```
import React, { useRef } from 'react';

function FocusInput() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus(); // Устанавливает фокус на input
  }

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleClick}>Установить фокус</button>
    </div>
  );
}

export default FocusInput;
```
**Объяснение**:
- `useRef` создаёт ссылку на элемент `input`.
- Функция `handleClick` устанавливает фокус на `input` при нажатии на кнопку.

### **3.4. useContext**

`useContext` — это хук, который позволяет использовать контекст в функциональных компонентах. Контекст используется для передачи данных через дерево компонентов без необходимости передавать props вручную на каждом уровне.

##### Пример использования `useContext`:
```
import React, { createContext, useState, useContext } from 'react';

// Создание контекста
const ThemeContext = createContext();

export function useTheme() {
  return useContext(ThemeContext);
}

// Провайдер контекста
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  function toggleTheme() {
    setTheme((prevTheme) =>
      prevTheme === 'light' ? 'dark' : 'light'
    );
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```
**Объяснение**:
- `createContext` создаёт контекст для управления темой.
- `ThemeProvider` предоставляет контекст для дочерних компонентов.
- `useTheme` — кастомный хук для упрощения использования контекста.

2. **Использование контекста в компонентах**

Создайте компонент `ThemeSwitcher`, который использует контекст для переключения темы.
```
import React from 'react';
import { useTheme } from './ThemeContext';

function ThemeSwitcher() {
  const { theme, toggleTheme } = useTheme();
  
  return (
    <div
      style={{
        background: theme === 'light' ? '#fff' : '#333',
        color: theme === 'light' ? '#000' : '#fff',
        padding: '16px',
      }}
    >
      <p>Текущая тема: {theme}</p>
      <button onClick={toggleTheme}>Сменить тему</button>
    </div>
  );
}

export default ThemeSwitcher;
```
**Объяснение**:
- `useTheme` используется для получения текущей темы и функции для её изменения.
- В зависимости от темы изменяются стили компонента.

3. **Оборачивание приложения в ThemeProvider**

В основном файле приложения (`App.js` или `index.js`), оберните ваше приложение в `ThemeProvider`.
```
import { createRoot } from 'react-dom/client'
import { ThemeProvider } from './ThemeContext';
import App from './App.jsx'
import './index.css'

createRoot(document.getElementById('root')).render(
  <ThemeProvider>
    <App />
  </ThemeProvider>,
)
```
**Объяснение**:
- `ThemeSwitcher` позволяет пользователю переключать тему приложения.

---
