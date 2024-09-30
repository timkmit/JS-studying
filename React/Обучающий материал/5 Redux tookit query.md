
**Redux Toolkit Query (RTK Query)** — это мощная библиотека для работы с API, встроенная в Redux Toolkit. Она значительно упрощает процесс выполнения запросов к серверу, автоматизирует управление состоянием, кеширование, рефетчинг данных и другие аспекты работы с асинхронными операциями.

RTK Query устраняет необходимость вручную писать экшены, редьюсеры и дополнительные мидлвары для обработки запросов. Благодаря RTK Query можно легко интегрировать работу с REST API, GraphQL или любыми другими источниками данных в Redux-приложение.

### Основные функции RTK Query
1. **Запросы к API**: выполняются с помощью хуков (например, `useQuery`, `useMutation`), которые генерируются автоматически.
2. **Кеширование данных**: RTK Query автоматически кеширует данные и использует их для оптимизации запросов.
3. **Рефетчинг данных**: позволяет легко обновлять данные при изменении условий.
4. **Оптимизация производительности**: минимизирует количество запросов, повторно используя закешированные данные.
5. **Поддержка мутаций**: включает создание, обновление и удаление данных с минимальными усилиями.

### Основные компоненты RTK Query
1. **`createApi`**: главный инструмент для создания запросов и мутаций.
2. **`fetchBaseQuery`**: вспомогательная функция для выполнения запросов к REST API.
3. **`endpoints`**: набор запросов (queries) и мутаций (mutations), которые можно определить для взаимодействия с сервером.
4. **Хуки**: автоматически сгенерированные хуки (`useQuery`, `useMutation`) для использования в компонентах React.

---
### Термины этой главы:
- **Эндпоинты (endpoints)**: Описывают запросы и мутации, которые можно выполнять через API. В RTK Query эндпоинты включают запросы (queries) для получения данных и мутации (mutations) для создания, обновления или удаления данных.

- **Мидлвары (middleware)**: Функции, которые перехватывают действия (actions) между их отправкой и обработкой редьюсерами. В RTK Query мидлвар управляет запросами, кешированием, и состоянием загрузки.

- **Кеширование**: Механизм сохранения результатов запросов для повторного использования. RTK Query автоматически кеширует данные, чтобы минимизировать количество запросов к серверу и ускорить доступ к уже полученным данным.

- **Мутации (mutations)**: Операции, изменяющие данные на сервере, такие как создание, обновление или удаление. В RTK Query мутации также управляют состоянием загрузки и ошибок для асинхронных операций.

- **Base Query**: Функция, которая определяет, как будут выполняться запросы к API. В RTK Query часто используется встроенная функция `fetchBaseQuery`, которая работает на основе стандартного `fetch`.

- **Reducer Path**: Уникальный ключ в Redux-хранилище, под которым будет сохраняться состояние, связанное с определённым API (например, `userApi.reducerPath`).

- **Selector**: Функция, которая извлекает данные из состояния Redux. В RTK Query селекторы используются для доступа к кешированным данным и состояниям запросов (например, `selectUserById`).

- **Refetching**: Повторный запрос данных, даже если они закешированы. Используется для обновления устаревших данных или после изменений на сервере.

- **Polling**: Механизм регулярного повторного запроса данных с интервалом времени. RTK Query поддерживает авто-рефетчинг через polling.

- **Invalidation**: Механизм, который позволяет "протухать" (invalidating) кешированные данные. После мутации (например, добавления/обновления) можно пометить определённые данные как устаревшие, чтобы они автоматически обновлялись при следующем запросе.

- **Error Handling**: Обработка ошибок, возникающих во время выполнения запросов или мутаций. RTK Query предоставляет удобные состояния для управления ошибками (`isError`, `error`).

- **`unwrap()`**: Метод, используемый с мутациями для получения сырых данных из промиса. Позволяет обработать результат мутации, а не оборачивать его в экшены или стейты.

- **Force Refetching**: Принудительный запрос данных, даже если они недавно кешировались. Используется для ситуаций, когда необходимо обновить данные независимо от состояния кеша.
---

### Пример настройки RTK Query
*(Повторять код не нужно, он для примера, просмотрите его, а приложение напишите по ролику)*

Для начала работы с RTK Query нужно создать API с использованием `createApi` и интегрировать его с Redux-хранилищем.
```
import {
  createApi,
  fetchBaseQuery,
} from '@reduxjs/toolkit/query/react';

export const userApi = createApi({
  reducerPath: 'userApi', // уникальный ключ для хранилища
  baseQuery: fetchBaseQuery({ baseUrl: '/api' }), // базовый URL для всех запросов
  endpoints: (builder) => ({
    getUserById: builder.query({
      query: (id) => `users/${id}`, // путь для получения пользователя по ID
    }),
    createUser: builder.mutation({
      query: (newUser) => ({
        url: 'users',
        method: 'POST',
        body: newUser,
      }),
    }),
  }),
});

export const { useGetUserByIdQuery, useCreateUserMutation } = userApi;
```
- **`createApi`**: создаёт объект API с базовым запросом и набором эндпоинтов.
- **`reducerPath`**: уникальный идентификатор для интеграции в хранилище.
- **`baseQuery`**: определяет общие параметры запроса, такие как базовый URL и обработка запросов.
- **`endpoints`**: здесь определены два эндпоинта — `getUserById` (для получения данных о пользователе) и `createUser` (для создания нового пользователя).
- **`useGetUserByIdQuery`, `useCreateUserMutation`**: автоматически сгенерированные хуки для выполнения запросов и мутаций.

#### Интеграция в Redux Store
Чтобы RTK Query работал с Redux, нужно добавить его редьюсер и мидлвар в хранилище.

```
import { configureStore } from '@reduxjs/toolkit';
import { userApi } from './userApi';

const store = configureStore({
  reducer: {
    [userApi.reducerPath]: userApi.reducer, // добавляем редьюсер API
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(userApi.middleware), // добавляем мидлвар API
});

export default store;
```

### Использование в компонентах React
RTK Query генерирует хуки для запросов и мутаций, которые можно использовать прямо в компонентах.

#### 1. Запрос данных (Query)
```
import React from 'react';
import { useGetUserByIdQuery } from './userApi';

function UserProfile({ userId }) {
  const { data, error, isLoading } = useGetUserByIdQuery(userId); // выполняем запрос

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error loading user</div>;
  
  return (
    <div>
      <h1>{data.name}</h1>
      <p>Email: {data.email}</p>
    </div>
  );
}

export default UserProfile;
```
- **`useGetUserByIdQuery(userId)`**: хук, который автоматически выполняет запрос на сервер для получения данных пользователя.
- **`isLoading`**: состояние, указывающее на то, что данные загружаются.
- **`error`**: содержит ошибку, если запрос не удался.
- **`data`**: содержит результат успешного выполнения запроса (данные пользователя).

#### 2. Создание или изменение данных (Mutation)
```
import React, { useState } from 'react';
import { useCreateUserMutation } from './userApi';

function CreateUserForm() {
  const [createUser, { isLoading, error }] = useCreateUserMutation();
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  
  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      await createUser({ name, email }).unwrap(); // выполняем мутацию
      alert('User created successfully!');
    } catch (err) {
      console.error('Failed to create user:', err);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Name"
      />
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <button type="submit" disabled={isLoading}>
        {isLoading ? 'Creating...' : 'Create User'}
      </button>
      {error && <p>Error: {error.message}</p>}
    </form>
  );
}

export default CreateUserForm;
```
- **`useCreateUserMutation`**: хук для создания нового пользователя.
- **`createUser`**: функция для выполнения мутации.
- **`isLoading`**: состояние загрузки.
- **`error`**: ошибка, если создание пользователя не удалось.

### Кеширование и рефетчинг данных

RTK Query автоматически кеширует данные и может использовать их повторно без новых запросов. Но иногда требуется обновить данные. Это можно сделать вручную с помощью функции `refetch`.

```
const { data, refetch } = useGetUserByIdQuery(userId);

// Пример ручного рефетчинга
<button onClick={() => refetch()}>Refresh User Data</button>;
```
**`refetch()`**: позволяет выполнить запрос заново и обновить данные.

### Политики кеширования

RTK Query предоставляет гибкие политики управления кешем. Вы можете настраивать параметры кеша для каждого эндпоинта, такие как время жизни кеша (TTL) и необходимость принудительного рефетчинга.
```
const userApi = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: '/api' }),
  endpoints: (builder) => ({
    getUserById: builder.query({
      query: (id) => `users/${id}`,
      keepUnusedDataFor: 60, // данные будут храниться в кеше 60 секунд
    }),
  }),
});
```
**`keepUnusedDataFor`**: определяет, как долго данные будут храниться в кеше, если они не используются (в секундах).

