
`React Router` — это библиотека для создания маршрутизации в приложениях на React. Она позволяет навигацию между различными страницами или компонентами без перезагрузки страницы, что делает приложения более отзывчивыми.

### **Docs:**
https://reactrouter.com/en/main

### **1. Установка React Router**

Перед началом работы установим `react-router-dom`, который включает компоненты для работы с маршрутизацией в веб-приложениях:

`npm install react-router-dom`

### **2. Основные компоненты React Router**

1. **`BrowserRouter`** — компонент, который оборачивает все приложение и включает поддержку маршрутизации.
2. **`Routes`** и **`Route`** — компоненты для определения маршрутов.
3. **`Link`** — компонент для навигации между страницами без перезагрузки.
4. **`useNavigate`** — хук для программной навигации между страницами.

### **3. Пример простого приложения с маршрутизацией**

Создадим простое приложение с тремя страницами: Главная страница, О нас и Контакты.
```
//App.jsx
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';

  

function App() {
  return (
    <Router>
      <nav>
        <ul>
          <li><Link to="/">Главная</Link></li>
          <li><Link to="/about">О нас</Link></li>
          <li><Link to="/contact">Контакты</Link></li>
        </ul>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </Router>
  );
}

export default App;
```
Создайте папку pages в src и добавьте другие страницы для сайта. Этому примеру требуются About.jsx , Contact.jsx , Home.jsx .
```
//About.jsx
function About() {
  return <h1>О нас</h1>;
}

export default About;
```
Аналогично создайте и добавьте остальные страницы.

После запуска проекта будет рабочая навигация по нашему сайту. Каждый созданный компонент в данном случае является целой страницей, можете добавить информацию или стили, а так же добавить еще пару роутов.

### **4. Программная навигация с useNavigate**

Хук `useNavigate` используется для программной навигации. Например, если нужно перенаправить пользователя на другую страницу после отправки формы.
#### Пример использования:
```
//App.jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import Login from './pages/Login';
import Home from './pages/Home';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login />} />
      </Routes>
    </Router>
  );
}

export default App;
```

```
//Home.jsx
import { useNavigate } from 'react-router-dom';

function Home() {
  const navigate = useNavigate() 

  const goToLogin = () => {
    navigate('/login');
  };

  return (
    <div>
      <h1>Главная страница</h1>
      <button onClick={goToLogin}>Перейти на страницу входа</button>
    </div>
  );
}
  
export default Home;
```

```
//Login.jsx
import { useNavigate } from 'react-router-dom';

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // Обычно здесь выполняется логика входа
    // Перенаправление на главную страницу после успешного входа
    navigate('/');
  };

  const goToHome = () => {
    navigate('/');
  };

  return (
    <div>
      <h2>Страница входа</h2>
      <button onClick={handleLogin}>Войти</button>
      <button onClick={goToHome}>На главную страницу</button>
    </div>
  );
} 

export default Login;
```
### **Пояснение**
1. **`App.jsx`**: Конфигурирует маршруты для вашего приложения. Главная страница (`Home`) доступна по пути `/`, а страница логина (`Login`) — по пути `/login`.
2. **`Home.jsx`**: Главная страница с кнопкой "Перейти на страницу входа". При нажатии на эту кнопку вызывается функция `goToLogin`, которая использует хук `useNavigate` для перенаправления на страницу логина.
3. **`Login.jsx`**: Страница входа с кнопкой "Войти". При нажатии на кнопку вызывается функция `handleLogin`, которая выполняет перенаправление на главную страницу с помощью хука `useNavigate`.

---
## **Управляемые и неуправляемые формы, валидация**

Формы в React могут быть управляемыми (controlled) и неуправляемыми (uncontrolled). Управляемые формы — это формы, где значения элементов управления (input, select и т.д.) хранятся в состоянии компонента. Неуправляемые формы — это формы, где значения управляются напрямую через DOM-элементы с помощью рефов.

### **1. Управляемые Формы**

Управляемые формы используют состояние компонента для управления значениями полей ввода. Это позволяет легко отслеживать и изменять значения полей формы и обрабатывать их в зависимости от состояния компонента.

#### Пример Управляемой Формы

Создадим форму для ввода имени и email с валидацией.
##### **`ControlledForm.jsx`**
```
import { useState } from 'react';

function ControlledForm() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [errors, setErrors] = useState({});

  // Валидация формы
  const validate = () => {
    const newErrors = {};
    if (!name) newErrors.name = 'Имя обязательно';
    if (!email) newErrors.email = 'Email обязателен';
    else if (!/\S+@\S+\.\S+/.test(email)) newErrors.email = 'Некорректный email';
    setErrors(newErrors);
    return Object.keys(newErrors).length === 0;
  };

  
  // Обработка отправки формы
  const handleSubmit = (event) => {
    event.preventDefault();
    if (validate()) {
      alert(`Имя: ${name}, Email: ${email}`);
      // Можно добавить здесь логику отправки данных на сервер
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Имя:
          <input
            type="text"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />

          {errors.name && <span style={{ color: 'red' }}>{errors.name}</span>}
        </label>
      </div>
      <div>
        <label>
          Email:
          <input
            type="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
          {errors.email && <span style={{ color: 'red' }}>{errors.email}</span>}
        </label>
      </div>
      <button type="submit">Отправить</button>
    </form>
  );
}

export default ControlledForm;
```
- `useState` используется для хранения значений полей формы (`name` и `email`), а также для хранения ошибок (`errors`).
- `validate` функция проверяет значения полей и устанавливает ошибки, если данные некорректны - такая ручная валидация не обязательна, потому что существуют библиотеки для валидации в React.
- `handleSubmit` обрабатывает отправку формы, выполняет валидацию и показывает данные при успешной валидации.

### **2. Неуправляемые Формы**

Неуправляемые формы используют рефы для доступа к значению полей ввода напрямую через DOM, а не через состояние компонента.

#### Пример Неуправляемой Формы

Создадим форму с теми же полями, но будем использовать рефы для получения значений.
##### **`UncontrolledForm.jsx`**
```
import { useRef } from 'react';

function UncontrolledForm() {
  const nameRef = useRef(null);
  const emailRef = useRef(null);

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Имя: ${nameRef.current.value}, Email: ${emailRef.current.value}`);
    // Можно добавить здесь логику отправки данных на сервер
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Имя:
          <input type="text" ref={nameRef} />
        </label>
      </div>
      <div>
        <label>
          Email:
          <input type="email" ref={emailRef} />
        </label>
      </div>
      <button type="submit">Отправить</button>
    </form>
  );
}

export default UncontrolledForm;
```
- `useRef` используется для создания рефов, которые привязываются к полям ввода.
- `handleSubmit` извлекает значения полей через `ref` и показывает их в alert.

### **3. Валидация Форм**

Валидация может быть как простой (например, проверка обязательности полей), так и сложной (например, проверка соответствия определенному шаблону).

В React для валидации форм часто используют популярные библиотеки, такие как **Formik**, **Yup**, и **React Hook Form**. Эти инструменты значительно упрощают процесс управления формами и валидации, делают код более компактным и легко читаемым. Давайте разберем, как использовать каждую из них.

### **Docs:**
https://formik.org/
https://yup-docs.vercel.app/docs/intro
#### **Установите обе библиотеки:**
`npm install formik yup`
##### **`Form.jsx`**
```
import { Formik, Form, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup';

// Схема валидации с помощью Yup
const validationSchema = Yup.object({
  name: Yup.string()
    .required('Имя обязательно')
    .min(2, 'Имя должно содержать минимум 2 символа'),
  email: Yup.string()
    .email('Некорректный email')
    .required('Email обязателен'),
  password: Yup.string()
    .required('Пароль обязателен')
    .min(8, 'Пароль должен быть минимум 8 символов')
    .matches(/\d/, 'Пароль должен содержать хотя бы одну цифру'),
});

  

const FormikForm = () => {
  return (
    <Formik
      initialValues={{ name: '', email: '', password: '' }}
      validationSchema={validationSchema}
      onSubmit={(values) => {
        alert(JSON.stringify(values, null, 2));
      }}
    >
      {() => (
        <Form>
          <div>
            <label>Имя</label>
            <Field name="name" type="text" />
            <ErrorMessage name="name" component="div" style={{ color: 'red' }} />
          </div>

          <div>
            <label>Email</label>
            <Field name="email" type="email" />
            <ErrorMessage name="email" component="div" style={{ color: 'red' }} />
          </div>
          <div>
            <label>Пароль</label>
            <Field name="password" type="password" />
            <ErrorMessage name="password" component="div" style={{ color: 'red' }} />
          </div>
          <button type="submit">Отправить</button>
        </Form>
      )}
    </Formik>
  );
};

export default FormikForm;
```

##### **`App.jsx`**
```
import FormikForm from "./components/Form";

function App() {
  return (
    <FormikForm/>
  );
}

export default App;
```
### **Объяснение:**
1. **Formik** используется для управления состоянием формы и обработки отправки.
2. **Yup** предоставляет декларативную валидацию полей:
    - Поле имени должно быть не пустым и содержать минимум 2 символа.
    - Поле email должно быть правильного формата.
    - Поле пароля должно быть не пустым, содержать минимум 8 символов и хотя бы одну цифру.
3. **Field** — это компонент Formik, который связывается с полем формы.
4. **ErrorMessage** выводит сообщения об ошибках.

Эти библиотеки предоставляют простую и надежную валидацию. Но необязательно использовать Formik и Yup сразу, все зависит от запросов бизнеса. Далее рассмотрим вполне самостоятельную библиотеку для валидации форм, которая используется в каждом втором проекте.

### **2. Валидация с использованием React Hook Form**

#### **React Hook Form** — это легковесная библиотека для работы с формами в React, которая использует хуки для управления состоянием формы. Она также поддерживает валидацию, что делает её отличным выбором для проектов.

### **Docs:**
https://react-hook-form.com/
#### **Установка:**
`npm install react-hook-form`

Создадим ту же форму для регистрации с полями "Имя", "Email" и "Пароль", но используя `react-hook-form`.

##### **`ReactHookForm.jsx`**
```
import { useForm } from 'react-hook-form';

const ReactHookForm = () => {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    alert(JSON.stringify(data));
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <label>Имя</label>
        <input
          {...register('name', { required: 'Имя обязательно', minLength: { value: 2, message: 'Имя должно содержать минимум 2 символа' } })}
        />
        {errors.name && <p style={{ color: 'red' }}>{errors.name.message}</p>}
      </div>
      <div>
        <label>Email</label>
        <input
          {...register('email', {
            required: 'Email обязателен',
            pattern: { value: /\S+@\S+\.\S+/, message: 'Некорректный email' },
          })}
        />
        {errors.email && <p style={{ color: 'red' }}>{errors.email.message}</p>}
      </div>
      <div>
        <label>Пароль</label>
        <input
          type="password"
          {...register('password', {
            required: 'Пароль обязателен',
            minLength: { value: 8, message: 'Пароль должен быть минимум 8 символов' },
            pattern: { value: /\d/, message: 'Пароль должен содержать хотя бы одну цифру' },
          })}
        />
        {errors.password && <p style={{ color: 'red' }}>{errors.password.message}</p>}
      </div>
      <button type="submit">Отправить</button>
    </form>
  );
};

export default ReactHookForm;
```
##### **`App.jsx`**
```
import ReactHookForm from "./components/FormHook";

function App() {
  return (
    <ReactHookForm/>
  );
}

export default App;
```
### **Объяснение:**
1. **useForm** предоставляет несколько методов для управления формой:
    - **register** регистрирует поля ввода для их контроля и валидации.
    - **handleSubmit** управляет процессом отправки формы.
    - **formState.errors** содержит информацию об ошибках валидации.
2. Мы указываем правила валидации прямо в методе **register**, включая обязательность поля, минимальную длину и шаблон (паттерн) для проверки email и пароля.

#### **Коротко:**
- **Formik и Yup** предоставляют декларативный и удобный подход к работе с формами и валидацией. Formik особенно удобен для сложных форм с большим количеством полей.
- **React Hook Form** — это легковесная библиотека, которая обеспечивает высокую производительность за счет минимального количества рендеров. Она хорошо подходит для форм с динамическими полями или большим объемом данных.

Библиотек для валидации на самом деле очень много, но все они выполняют одну роль. Важно помнить, что валидация полей очень важная часть разработки, так как она не только заставляет пользователей использовать корректные данные, но и защищает от уязвимостей.

---
## **3. HTTP-запросы и работа с API через fetch/axios**

Для взаимодействия с внешними API в React можно использовать два основных метода: **fetch API** (встроенный в браузеры) и библиотеку **axios** (популярная библиотека для работы с HTTP-запросами).
### **Использование fetch**

**fetch** — это встроенный API в браузере, который используется для отправки HTTP-запросов. Он возвращает промис и может использоваться для получения данных от сервера.
### **Пример использования fetch**
Создадим компонент, который будет загружать список пользователей с помощью `fetch` и отображать их на экране.
##### **`FetchUsers.jsx`**
```
import { useEffect, useState } from 'react';

function FetchUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then((response) => {
        if (!response.ok) {
          throw new Error('Ошибка сети');
        }
        return response.json();
      })
      .then((data) => {
        setUsers(data);
        setLoading(false);
      })
      .catch((error) => {
        setError(error.message);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return <div>Загрузка...</div>;
  }

  if (error) {
    return <div>Ошибка: {error}</div>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default FetchUsers;
```

##### **`App.jsx`**
```
import FetchUsers from "./components/FetchUsers";

function App() {
  return (
    <FetchUsers />
  );
}

export default App;
```
### **Объяснение:**
1. Используем `useState` для хранения данных (`users`), статуса загрузки (`loading`) и ошибок (`error`).
2. В `useEffect` выполняем HTTP-запрос через `fetch`.
3. Проверяем, был ли ответ успешным, и преобразуем его в JSON с помощью `.json()`.
4. В случае ошибки выводим сообщение об ошибке, а если данные успешно получены — отображаем их.

Это самый популярный способ работы с запросами. Не нужно ничего устанавливать, браузер итак его поддерживает. 

### **Использование axios**

**axios** — это самая популярная библиотека для работы с HTTP-запросами. Она предоставляет чуть более удобный интерфейс для работы с запросами, чем fetch, и позволяет легко обрабатывать запросы с более сложной логикой (например, с обработкой токенов аутентификации).

#### **Установка axios**
`npm install axios`

### **Пример использования axios**
Давайте перепишем предыдущий пример, но с использованием axios.
##### **`AxiosUsers.jsx`**
```
import { useEffect, useState } from 'react';
import axios from 'axios';

function AxiosUsers() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios
      .get('https://jsonplaceholder.typicode.com/users')
      .then((response) => {
        setUsers(response.data);
        setLoading(false);
      })
      .catch((error) => {
        setError(error.message);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return <div>Загрузка...</div>;
  }

  if (error) {
    return <div>Ошибка: {error}</div>;
  }

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default AxiosUsers;
```

##### **`App.jsx`**
```
import AxiosUsers from "./components/AxiosUsers";

function App() {
  return (
    <AxiosUsers/>
  );
}

export default App;
```
### **Объяснение:**
1. Вместо `fetch` мы используем метод `axios.get()` для получения данных.
2. Axios автоматически преобразует ответ в JSON, поэтому не нужно явно использовать `.json()`, как это делается с fetch.
3. Обработка ошибок и загрузка данных работает аналогично.

### **Axios и асинхронные функции**
Также можно использовать асинхронные функции (async/await) для работы с axios:

```
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/users');
        setUsers(response.data);
        setLoading(false);
      } catch (error) {
        setError(error.message);
        setLoading(false);
      }
    };
    fetchData();
  }, []);
```

---
## **4. Lazy Loading, React.lazy и Suspense**

Lazy loading (ленивая загрузка) — это техника, которая позволяет загружать компоненты только тогда, когда они действительно необходимы. Это особенно полезно для оптимизации производительности в больших приложениях.

### **React.lazy**
`React.lazy()` — это встроенная функция React, которая позволяет динамически загружать компоненты. Она используется вместе с компонентом `Suspense`, который показывает запасной контент (например, индикатор загрузки), пока компонент загружается.

### **Пример ленивой загрузки компонента**
Допустим, у нас есть два компонента: `HomePage` и `AboutPage`. Мы хотим загружать `AboutPage` только тогда, когда пользователь действительно перейдет на эту страницу.

##### **`AboutPage.jsx`**
```
function AboutPage() {
  return <h2>О нас</h2>;
}

export default AboutPage;
```

##### **`App.jsx`**
```
import { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
  
const AboutPage = lazy(() => import('./pages/About'));

function HomePage() {
  return <h2>Главная страница</h2>;
}

function App() {
  return (
    <Router>
      <nav>
        <Link to="/">Главная</Link> | <Link to="/about">О нас</Link>
      </nav>
      <Suspense fallback={<div>Загрузка...</div>}>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/about" element={<AboutPage />} />
        </Routes>
      </Suspense>
    </Router>
  );
}

export default App;
```
### **Объяснение:**
1. **React.lazy** используется для динамической загрузки компонента `AboutPage`. Компонент не будет загружен до тех пор, пока пользователь не перейдет на страницу "О нас".
2. **Suspense** используется для отображения запасающего контента (например, сообщения "Загрузка...") пока компонент загружается.
3. Мы настроили маршруты с помощью `react-router-dom`, чтобы переключаться между страницами "Главная" и "О нас".
