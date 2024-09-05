
`React Router` — это библиотека для создания маршрутизации в приложениях на React. Она позволяет навигацию между различными страницами или компонентами без перезагрузки страницы, что делает приложения более отзывчивыми.
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

### **1. Управляемые формы**

Управляемые формы используют состояние компонента для управления значениями полей ввода.
