Начнем с того, что же такое HTML? Представьте, что вам нужно, чтобы браузер понял что вы ему передаете, так вот HTML будет инструментом, с помощью которого браузер будет знать что вы ему хотите сказать.
Если говорить правильнее, это язык разметки, мы заполняем HTML документ своим материалом, а браузер, понимая какая информация содержится в таком документе, отображает ее в интернете пользователю.

Структура такого документа всегда идентичная, мы используем теги для выделения конкретных блоков информации в документе. Что такое теги? Это своеобразная обертка над текстом\картинкой\видео, которая указывает браузеру что мы ему передаем. Более подробно написано во 2 главе "Теги в HTML".

Чем можно запустить html файл? Самое простое - создать обычный файлик Блокнота и сохранить его с расширением .html . Но давайте опираться на реальную разработку, для этого нам потребуется Visual Studio Code, как его установить и начать использовать можно узнать в папке "IDE, Node, Git"

Теперь, поняв, что такое теги и что такое html, давайте рассмотрим простую структуру сайта с использованием этого языка разметки:
```
<!DOCTYPE html> 
<html lang="ru"> 
	<head> 
		<meta charset="UTF-8"> 
		<title>Пример страницы</title> 
	</head> 
	<body> 
		<p>Введите ваше имя:</p> 
		<input type="text" name="name"> 
	</body> 
</html>
```

Если запустить этот документ, мы увидим:
![[Pasted image 20240805231821.png]]
Наш первый сайт называется "Пример страницы", а так же содержит строку "Введите ваше имя" и поле для ввода текста.


`<!DOCTYPE html>` - указываем, что используем актуальную версию HTML.
`<html lang="ru">`-главный тег, который содержит все тело нашего документа, внутри него содержаться остальные теги, а за пределами ничего не пишется.
`<head>`- html документ делится на условные блоки, первый из них head - из перевода понятно, что это заголовок, в нем мы указываем все ссылки на сторонние ресурсы, всю необходимую информацию и файлы. В данном случае указываем кодировку с помощью мета-тега `<meta charset="UTF-8">` и название сайта (которое мы видим на вкладке в браузере) с помощью `<title>Пример страницы</title>`.
`<body>` - вторая часть нашего сайта, в нем мы прописываем все теги, которые содержат какую либо информацию для нашего сайта, будто то текст, видео, картинки и тд. 
`<p></p>` - это тег параграфа, в нем мы прописываем текст, который должен находится один на строке.
`<input>` - тег окна ввода текста, внутри него мы можем указать тип (type="text") и название окна (name="name").


Попробуйте поменять самостоятельно название и текст, а может еще и добавить кнопку, прописав тег `<button>`: `<button>Кнопка</button>`

Угадайте, где она должна прописываться в таком документе, не расстраивайтесь если не получится с первого раза, на ошибках мы учимся и получаем ценный опыт.

Итак, html - это язык разметки, мы его используем чтобы собрать нашу html-страницу (сайт). Структура всегда одинаковая, есть главный тег `<html></html>` , внутри которого мы "собираем" наш сайт. Основные и главные блоки в таком сайте оборачиваются `<head></head> и <body></body>` , в первом мы указываем все дополнительные ссылки, стили и тд, а во втором весь материал, который хотим видеть на сайте.

