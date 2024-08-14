**Flexbox** (так они называются) — это модель компоновки в CSS, которая позволяет легко управлять расположением элементов внутри контейнера (того же div, или любого блочного). С помощью Flexbox можно выравнивать элементы горизонтально и вертикально, управлять их размером и пространством между ними, а также обеспечивать гибкость компоновки.

## 1. Flex-контейнер
Чтобы сделать элемент Flex-контейнером, нужно применить к нему свойство `display: flex;`. Внутри такого контейнера все дочерние элементы автоматически становятся Flex-элементами.
```
<!DOCTYPE html> 
<html lang="ru"> 
<head> 
	<meta charset="UTF-8"> 
	<meta name="viewport" content="width=device-width, initial-scale=1.0"> 
	<title>Пример Flex-контейнера</title> 
	<style> 
		.flex-container { 
			display: flex; 
			background-color: lightgray; 
			padding: 10px; 
		} 
		.flex-item { 
			background-color: coral; 
			padding: 20px; 
			margin: 10px; 
		} 
	</style> 
</head> 
	<body> 
		<div class="flex-container"> 
			<div class="flex-item">Элемент 1</div> 
			<div class="flex-item">Элемент 2</div> 
			<div class="flex-item">Элемент 3</div> 
		</div> 
	</body> 
</html>
```
Сверху пример целой страницы с таким контейнером. Скопируйте в пустой файл html и проверьте работоспособность. 
## Важно:
все стили в примерах указаны в теге `<style>` чтобы проще было понимать. Можете как копировать целиком, так и создать отдельный файл .css и переносить стили в него.

## 2. Направление Flex-контейнеров
Одним из ключевых свойств Flex-контейнера является `flex-direction`. Оно определяет, как будут располагаться элементы внутри контейнера: по горизонтали (рядом друг с другом) или по вертикали (один под другим).

- **`row`** (по умолчанию) — элементы располагаются в строку (по горизонтали).
- **`column`** — элементы располагаются в колонку (по вертикали).
- **`row-reverse`** — элементы располагаются в обратном порядке по горизонтали.
- **`column-reverse`** — элементы располагаются в обратном порядке по вертикали.

```
<!DOCTYPE html> 
<html lang="ru"> 
<head>     
<meta charset="UTF-8">     
<meta name="viewport" content="width=device-width, initial-scale=1.0">     
<title>Flex-направление</title>     
<style>         
	.flex-container {             
		display: flex;             
		flex-direction: column;             
		background-color: lightgray;             
		padding: 10px;         
	}         
	.flex-item {             
		background-color: coral;             
		padding: 20px;             
		margin: 10px;         
	}     
</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
Здесь элементы будут располагаться один под другим, так как задано направление `column`.
Самостоятельно измените значения `flex-direction` и посмотрите на поведение контейнеров.

## 3. Перенос элементов внутри контейнера
Если у вас много элементов внутри Flex-контейнера и они не помещаются в одну строку, можно использовать свойство `flex-wrap`. Оно позволяет элементам переноситься на следующую строку, если не хватает места.

- **`nowrap`** (по умолчанию) — элементы не переносятся и остаются в одной строке.
- **`wrap`** — элементы переносятся на следующую строку, если не хватает места.
- **`wrap-reverse`** — элементы переносятся на следующую строку в обратном порядке.

```
<!DOCTYPE html>
<html lang="ru">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Перенос Flex-элементов</title>
	<style>
		.flex-container {
			display: flex;
			flex-wrap: wrap;
			background-color: lightgray;
			padding: 10px;
		}
		.flex-item {
			background-color: coral;
			padding: 20px;
			margin: 10px;
			width: 150px;
			}
	</style>
</head>
<body>
	<div class="flex-container">
		<div class="flex-item">Элемент 1</div>
		<div class="flex-item">Элемент 2</div>
		<div class="flex-item">Элемент 3</div>
		<div class="flex-item">Элемент 4</div>
		<div class="flex-item">Элемент 5</div>
	</div>
</body>
</html>
```
В этом примере, если ширины контейнера не хватит для всех элементов, они перенесутся на следующую строку. Измените размеры браузера (растяните или уменьшите окно) и проверьте на работоспособность.

## 4. Выравнивание элементов внутри контейнера
Flexbox позволяет легко выравнивать элементы внутри контейнера по горизонтали и вертикали. Для этого используются свойства `justify-content` и `align-items`.

- **`justify-content`** — выравнивание по горизонтали (основная ось):
    - **`flex-start`** — элементы прижаты к началу контейнера.
    - **`flex-end`** — элементы прижаты к концу контейнера.
    - **`center`** — элементы выровнены по центру.
    - **`space-between`** — элементы равномерно распределены с одинаковыми промежутками.
    - **`space-around`** — элементы равномерно распределены с промежутками вокруг каждого элемента.

- **`align-items`** — выравнивание по вертикали (перпендикулярная ось):
    - **`flex-start`** — элементы выравнены по верхнему краю.
    - **`flex-end`** — элементы выравнены по нижнему краю.
    - **`center`** — элементы выравнены по центру по вертикали.
    - **`stretch`** — элементы растягиваются по высоте контейнера (если не задана фиксированная высота).

```
<!DOCTYPE html> 
<html lang="ru"> 
<head>     
	<meta charset="UTF-8">     
	<meta name="viewport" content="width=device-width, initial-scale=1.0">     
	<title>Выравнивание Flex-элементов</title>     
	<style>         
		.flex-container {             
			display: flex;             
			justify-content: center;             
			align-items: center;             
			height: 300px;             
			background-color: lightgray;         
		}         
		.flex-item {             
			background-color: coral;             
			padding: 20px;             
			margin: 10px;         
		}     
	</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
Здесь элементы будут выровнены по центру как по горизонтали, так и по вертикали.

## 5. Гибкий размер элементов
Flexbox позволяет легко управлять размером элементов, используя свойство `flex`. Оно определяет, как элементы будут расти или сжиматься, чтобы заполнить доступное пространство.

Свойство `flex` состоит из трех значений:
- **`flex-grow`** — определяет, насколько элемент может увеличиваться.
- **`flex-shrink`** — определяет, насколько элемент может уменьшаться.
- **`flex-basis`** — определяет начальный размер элемента до того, как начнут применяться `flex-grow` и `flex-shrink`.

Чаще всего используется сокращенная запись `flex: 1;`, что означает, что элемент будет расти, занимая равное пространство с другими элементами.

```
<!DOCTYPE html> 
<html lang="ru"> 
<head>     
	<meta charset="UTF-8">     
	<meta name="viewport" content="width=device-width, initial-scale=1.0">     
	<title>Гибкий размер Flex-элементов</title>     
	<style>         
		.flex-container {             
			display: flex;             
			background-color: lightgray;             
			padding: 10px;         
		}         
		.flex-item {             
			background-color: coral;             
			padding: 20px;             
			margin: 10px;             
			flex: 1;         
		}     
	</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
Здесь все три элемента будут занимать равное пространство внутри контейнера, так как у них задано свойство `flex: 1;`. Если простыми словами, контейнеры будут растягиваться по мере изменения размеров окна браузера.

## Дополнительно

Рассматривая последнюю часть про flexbox, хочется показать примеры использования значений свойства flex:

`flex-grow`
Свойство `flex-grow` определяет, насколько элемент может увеличиваться по сравнению с другими элементами внутри flex-контейнера.
```
<!DOCTYPE html> 
<html lang="ru"> 
<head>     
	<meta charset="UTF-8">     
	<meta name="viewport" content="width=device-width, initial-scale=1.0">     
	<title>Пример flex-grow</title>     
	<style>         
		.flex-container {             
			display: flex;             
			background-color: lightgray;             
			height: 100px;         
		}         
		.flex-item {             
			background-color: coral;             
			padding: 20px;             
			margin: 10px;             
			flex-grow: 1; /* Все элементы будут расти равномерно */ 
		}         
		.flex-item:first-child {             
			flex-grow: 2; /* Первый элемент растет в два раза быстрее остальных */         
		}     
	</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
**Результат:** Первый элемент будет занимать больше места (в два раза больше) по сравнению с другими элементами, которые растут равномерно. Потяните за окно браузера для просмотра.

`flex-shrink`
Свойство `flex-shrink` определяет, насколько элемент может уменьшаться по сравнению с другими элементами, если контейнер становится меньше.
```
<!DOCTYPE html> 
<html lang="ru"> 
<head>     
	<meta charset="UTF-8">     
	<meta name="viewport" content="width=device-width, initial-scale=1.0">     
	<title>Пример flex-grow</title>     
	<style>         
		.flex-container { 
			display: flex; 
			background-color: lightgray; 
		} 
		.flex-item { 
			background-color: coral; 
			padding: 20px; 
			margin: 10px; 
			flex-basis: 50px; /* Начальный размер элементов */ 
		} 
		.flex-item:first-child { 
			flex-basis: 200px; /* Первый элемент будет иметь начальный размер 200px */ 
		}
	</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
**Результат:** Когда размер контейнера уменьшается, первый элемент будет уменьшаться быстрее остальных, потому что изначально больше. Потяните на окно браузера для просмотра эффекта.

`flex-basis`
Свойство `flex-basis` определяет начальный размер элемента до применения `flex-grow` или `flex-shrink`.
```
<!DOCTYPE html> <html lang="ru"> 
<head>     
	<meta charset="UTF-8">     
	<meta name="viewport" content="width=device-width, initial-scale=1.0">     
	<title>Пример flex-basis</title>     
	<style>         
		.flex-container {             
			display: flex;             
			background-color: lightgray;         
		}         
		.flex-item {             
			background-color: coral;             
			padding: 20px;             
			margin: 10px;             
			flex-basis: 100px; /* Начальный размер элементов */
		}         
		.flex-item:first-child {             
			flex-basis: 200px; /* Первый элемент будет иметь начальный размер 200px */         
		}     
	</style> 
</head> 
<body>     
	<div class="flex-container">         
		<div class="flex-item">Элемент 1</div>         
		<div class="flex-item">Элемент 2</div>         
		<div class="flex-item">Элемент 3</div>     
	</div> 
</body> 
</html>
```
**Результат:** Первый элемент начнет с ширины 200px, а остальные — с 100px, до применения гибкости по свойствам `flex-grow` или `flex-shrink`.

Может показаться, что все свойства делают одно и то же, и отчасти вы будете правы, ведь видимых изменений нет, но мы изменяем свойства того, как будут изменяться контейнеры. Для достижения одной цели мы можем использовать разные подходы.

## Важно
Если вы прочитали и ознакомились с дополнительным материалом, то наверное у вас возник вопрос: "Что за `:first-child`". Если коротко, такие вещи называются псевдо-классами, конкретно этот находит самый первый элемент с названием класса `flex-item` и применяет к нему определенные свойства. Более подробно о них мы поговорим позже, так как эта тема достаточно большая и сложная.