**Redux** — это библиотека для управления состоянием в JavaScript приложениях. Она помогает управлять данными в приложении, организовывая их в единое глобальное хранилище (store). Redux часто используется с React, хотя его можно применять и с другими фреймворками.

#### Зачем нужен Redux?

В больших приложениях, когда компонентов много и они обмениваются данными, передача данных напрямую через `props` становится сложной и запутанной. Redux решает эту проблему, предоставляя единое централизованное хранилище, к которому могут обращаться любые компоненты приложения.

##### Проблемы, которые решает Redux:

1. **Управление глобальным состоянием**: Вместо того, чтобы передавать данные через несколько уровней компонентов, вы можете хранить их в одном месте (глобальном store), откуда их могут взять любые компоненты.
2. **Предсказуемость**: Redux использует строгие правила для изменения состояния, что делает поведение приложения более предсказуемым и простым для отладки.
3. **Управление сложными данными**: Когда данные приложения становятся сложными, с вложенными структурами и множеством изменений, Redux помогает организовать логику управления этими данными.

#### Основные концепции Redux:

1. **Store (хранилище)** — это объект, который содержит всё состояние вашего приложения. Он создается один раз и хранит в себе глобальное состояние.
2. **Actions (действия)** — это простые объекты, которые описывают, что произошло в приложении. У действия всегда есть тип (например, `ADD_ITEM`, `REMOVE_ITEM`) и, возможно, данные, передаваемые с ним.
3. **Reducers (редьюсеры)** — это функции, которые принимают текущее состояние и действие и возвращают новое состояние. Reducer не может изменять текущее состояние напрямую, а должен возвращать его копию с изменениями.
4. **Dispatch (отправка)** — это функция, с помощью которой вы отправляете actions для изменения состояния.
5. **Selectors (селекторы)** — функции, которые извлекают данные из store, чтобы компонент мог их использовать.

#### Как работает Redux?

1. Компонент вызывает действие через **dispatch**.
2. Redux передаёт это действие редьюсеру.
3. Редьюсер обновляет состояние в зависимости от типа действия.
4. Компоненты приложения получают обновленное состояние через **selectors**.

### Что такое Redux Toolkit?

**Redux Toolkit** — это официальный инструмент, созданный для упрощения работы с Redux. Он помогает избежать большого количества шаблонного кода и делает процесс создания и управления состоянием удобнее и быстрее.

Основные функции Redux Toolkit:

1. **configureStore** — создаёт store с уже встроенной поддержкой middleware (например, для асинхронных действий) и инструментами для отладки.
2. **createSlice** — объединяет редьюсеры и actions в одном месте, упрощая их создание.
3. **createAsyncThunk** — помогает работать с асинхронными операциями, например, запросами к API.
4. **redux-persist** — сохраняет состояние приложения в `localStorage` или других хранилищах, чтобы после перезагрузки страницы данные не терялись.

### Дополнительные библиотеки для работы с Redux

1. **react-redux** — позволяет легко интегрировать Redux с React, предоставляя хуки для работы с состоянием и действиями:
    - **useSelector** — для получения данных из store.
    - **useDispatch** — для отправки действий.
2. **redux-thunk** — middleware для работы с асинхронными действиями, например, для выполнения запросов к API.
3. **redux-persist** — позволяет сохранять состояние в `localStorage` или `sessionStorage`, чтобы оно сохранялось между перезагрузками страницы.
4. **reselect** — библиотека для создания мемоизированных селекторов, которые предотвращают ненужные перерисовки компонентов, если данные не изменились.

---

 Пока не приступили к разработке, упомяну, что архитектура приложения с redux toolkit выглядит так:
```
project
->/node_modules
->/public
->/src
->App.jsx
->App.css
->index.css
->main.jsx

/src содержит
->/assets
->/components
->/features
->/store

/components содержит компоненты (в данных проектах не в отдельных папках так как нет стилей. Но если используются стили, рекомендуется в этой папке создавать под каждый компонент отдельную папку с компонентом и его стилями)
```
 Подробнее:
```
project
->/node_modules
->/public
->/src
-->/assets
-->/components
--->/SomeComponent.jsx
--->/SomeComponent2.jsx
-->/features
--->/counter
---->/ounterSlice.js
--->/movie
---->/favoriteMovieSlice.js
-->/store
--->/store.js
->App.jsx
->App.css
->index.css
->main.jsx 
```
---
#### Простой пример: счётчик

*Исходный код находится в репозитории https://github.com/timkmit/rtk-examples.git*

Создадим простое приложение с использованием Redux Toolkit, где будет реализован счётчик, который можно увеличивать и уменьшать.

Создадим приложение:
`npm create vite@latest`

После, нужно установить Redux Toolkit:
`npm install @reduxjs/toolkit react-redux`

1. **Создание store**

Store — это место, где будет храниться состояние нашего приложения.

```
// store.js
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice'; // <-его пока нет, после создания обновите пути если файл не найден
const store = configureStore({
  reducer: { counter: counterReducer },
});
export default store;
```

2. **Создание slice (часть стейта)**

Slice объединяет в себе логику работы с определённой частью состояния, включая действия (actions) и редьюсеры (reducers).

```
// counterSlice.js 
import { createSlice } from '@reduxjs/toolkit';
const initialState = { value: 0 };
const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

- **createSlice** — создаёт slice, автоматически генерируя actions и reducers.
- **increment** и **decrement** — это действия для увеличения и уменьшения счётчика.

3. **Подключение store к приложению**

Теперь нужно подключить наше хранилище к React-приложению.

```
// main.jsx 
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import './index.css'

import { Provider } from 'react-redux';
import store from './store/store.js';

createRoot(document.getElementById('root')).render(
  <Provider store={store}>
     <App />
  </Provider>
)
```

- **Provider** — компонент, который передаёт store всему приложению.

4. **Использование стейта и dispatch в компонентах**

Теперь можно создать компоненты, которые будут взаимодействовать с нашим Redux store.

```
// Counter.jsx 
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from '../features/counter/CounterSlice';

const Counter = () => {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      {' '}
      <h1>{count}</h1>{' '}
      <button onClick={() => dispatch(increment())}>Увеличить</button>{' '}
      <button onClick={() => dispatch(decrement())}>Уменьшить</button>{' '}
    </div>
  );
};

export default Counter;
```


- **useSelector** — вытаскивает нужное значение из стейта (в данном случае — значение счётчика).
- **useDispatch** — позволяет отправлять actions для изменения стейта (в данном случае — увеличивать или уменьшать счётчик).

5. **Запуск приложения**

Для запуска осталось только передать готовый компонент в App.jsx
```
import './App.css'
import Counter from './components/Counter'
  
function App() {

  return (
    <>
      <Counter/>
    </>
  )
}  

export default App
```

Теперь всё готово. В итоге мы имеем простое приложение, где можно увеличивать и уменьшать значение счётчика, а все данные управляются через Redux Toolkit.
Чтобы проверить работоспособность, запустим приложение с помощью `npm run dev`.

Чтобы проследить за работой redux toolkit, можно воспользоваться Redux DevTools.

---
#### Сделаем еще одно приложение "Мои избранные фильмы". 

*Исходный код находится в репозитории https://github.com/timkmit/rtk-examples.git*

Суть приложения в том, что мы сможем добавлять фильмы в список, а так же при перезагрузке они сохранятся, потому что будем записывать данные в localStorage с помощью библиотеки redux-persist.

Начнём с установки приложения и необходимых зависимостей:
`npm create vite@latest`
`npm install @reduxjs/toolkit react-redux redux-persist`

#### 1. Настройка хранилища с `redux-persist`

Сначала создадим Redux store и настроим его с поддержкой `redux-persist` для сохранения данных в `localStorage`.

```
store.js
import { configureStore } from '@reduxjs/toolkit';
import { persistStore, persistReducer } from 'redux-persist';
import storage from 'redux-persist/lib/storage'; // используем localStorage по умолчанию, но можем и другие хранилища

import favoriteMoviesReducer from '../features/movies/favoriteMoviesSlice';

// Конфигурация persist
const persistConfig = {
  key: 'root',
  storage,
};

// Обёртываем редьюсер с persist
const persistedReducer = persistReducer(
  persistConfig,
  favoriteMoviesReducer
);

// Создание store
const store = configureStore({
  reducer: {
    favoriteMovies: persistedReducer,
  },
});

// Создание persistor для контроля состояния persist
export const persistor = persistStore(store);
export default store;
```
- **redux-persist** позволяет автоматически сохранять и загружать состояние из `localStorage`.
- **persistReducer** — это обёртка, которая позволяет редьюсеру сохранять состояние в `localStorage`.

#### 2. Создание slice для избранных фильмов

Slice будет содержать действия для добавления и удаления фильмов из списка избранных.

```
// favoriteMoviesSlice.js
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  movies: [],
};

const favoriteMoviesSlice = createSlice({
  name: 'favoriteMovies',
  initialState,
  reducers: {
    addMovie: (state, action) => {
      const isAlreadyAdded = state.movies.find(
        (movie) => movie.id === action.payload.id
      );

      if (!isAlreadyAdded) {
        state.movies.push(action.payload);
      }
    },

    removeMovie: (state, action) => {
      state.movies = state.movies.filter(
        (movie) => movie.id !== action.payload
      );
    },
  },
});

export const { addMovie, removeMovie } = favoriteMoviesSlice.actions;
export default favoriteMoviesSlice.reducer;
```
- **addMovie** — добавляет фильм в список, проверяя, что такого фильма ещё нет в списке.
- **removeMovie** — удаляет фильм по его `id`.

#### 3. Подключение `store` и `persistor` к приложению

Чтобы наше приложение сохраняло данные в `localStorage`, нужно подключить `PersistGate` и передать `store` и `persistor` через `Provider`.

```
// main.jsx
import { createRoot } from 'react-dom/client'
import App from './App.jsx'
import './index.css'

import { Provider } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react';
import store, { persistor } from './store/store.js';
  
createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <PersistGate loading={null} persistor={persistor}>
      <App />
    </PersistGate>
  </Provider>
)
```
- **PersistGate** позволяет приложениям ожидать восстановления состояния из `localStorage` перед рендером.

#### 4. Компоненты приложения

Теперь создадим компоненты для отображения списка фильмов и добавления в избранное.

##### 4.1. Компонент для добавления фильма

```
// MovieMount.jsx
import { useState } from 'react';
import { useDispatch } from 'react-redux';
import { addMovie } from '../features/movies/favoriteMoviesSlice';

const MovieInput = () => {
  const [movieTitle, setMovieTitle] = useState('');
  const dispatch = useDispatch();

  const handleAddMovie = () => {
    if (movieTitle.trim()) {
      const newMovie = {
        id: Date.now(),
        title: movieTitle,
      };
      dispatch(addMovie(newMovie));
      setMovieTitle('');
    }
  };

  return (
    <div>
      <input
        type="text"
        placeholder="Введите название фильма"
        value={movieTitle}
        onChange={(e) => setMovieTitle(e.target.value)}
      />
      <button onClick={handleAddMovie}>Добавить в избранное</button>
    </div>
  );
};

export default MovieInput;
```
Здесь мы можем добавлять фильм, вводя его название, а затем нажимая на кнопку.

4.2. Компонент для отображения списка фильмов

```
// MovieList.jsx
import { useSelector, useDispatch } from 'react-redux';
import { removeMovie } from '../features/movies/favoriteMoviesSlice;

const FavoriteMoviesList = () => {
  const movies = useSelector((state) => state.favoriteMovies.movies);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Избранные фильмы</h2>
      <ul>
        {movies.map((movie) => (
          <li key={movie.id}>
            {movie.title}
            <button onClick={() => dispatch(removeMovie(movie.id))}>Удалить</button>
          </li>
        ))}
      </ul>
    </div>
  );
};

export default FavoriteMoviesList;
```
- **FavoriteMoviesList** отображает список избранных фильмов и позволяет удалять их.
- 
#### 5. Основное приложение

Наконец, объединим всё в главном компоненте:
```
import './App.css'
import FavoriteMoviesList from './components/MovieList'
import MovieInput from './components/MovieMount'

function App() {

  return (
    <>
      <div>
        <h1>Мои избранные фильмы</h1>
        <MovieInput />
        <FavoriteMoviesList />
      </div>
    </>
  )
}

export default App
```
Теперь, если вы запустите приложение, можно добавлять фильмы в список избранных, удалять их, и всё это будет сохраняться в `localStorage`.

---
Да данном этапе на 2 примерах разобрали основы redux toolkit и persist. Далее для более глубокого изучения требуется выбрать любой функциональный проект и разработать самостоятельно с использованием вышеупомянутых технологий.
