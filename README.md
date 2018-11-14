# Партнёрская программа

Для участия в партнёрской программе, необходимо подать заявку на support@aretgofinas.ru
После утверждения заявки, вы получите ключ для доступа к сервису отправки форм заявок.

## Форма для отправки заявки на сервер АРТЕГОФинанс.

Форма должна быть отправлена на адрес https://artegofinans.ru/forms/creditapplication.php POST запросом.

Параметры запроса:

- **credit** - тип кредита (обязательное поле); возможные значения: 7 - Кредит бизнесу; 12 - Потребителский кредит; 15 - Залог автомобиля; 8 - Залог недвижимости; 9 - Рефинансирование; 10 - Ипотека
- **summ** - сумма кредита
- **name** - Имя
- **surname** - Фамилия
- **phone** - телефон для связи (обязательное поле); формат +7 и символы 0-9()- и пробел
- **email** - email для связи
- **comment** - комментарий
- **charset** - кодировка кирилистических символов формы; возможные значения: cp1251 и utf8 (если не указано - utf8)
- **key** - ключ, выданный Вам, для доступа к сервису (обязательное поле)

Так же можно передавать любые поля начинающиеся на **af_** - они будут возвращены в ответе без изменений

Ответ возвращается на странице, с которой был отправлен запрос. В параметрах будет указан результат обработки запроса.

Параметры ответа:

**status** - статус обратки запроса; возможные значения: `done` - запрос принят успешно; `error` - при обработке обнаружены ошибки. Если ошибки касаются передаваемых полей, то в ответе будет параметр с сответствующим описанием ошибки для конкретного поля. Общие ошибки передаются в параметре **error**

Пример формы отправки запроса:

```html
<form method="post" action="https://artegofinans.ru/forms/creditapplication.php">
	<select name="credit">
		<option value="0">Выбрать</option>
		<option value="7">Кредит бизнесу</option>
		<option value="12">Потребительский кредит</option>
		<option value="15">Залог автомобиля</option>
		<option value="8">Залог недвижимости</option>
		<option value="9">Рефинансирование</option>
		<option value="10">Ипотека</option>
	</select>
	<input type="text" name="summ" value="1000000">
	<input type="text" name="name" value="Ивайло">
	<input type="text" name="surname" value="Тилев">
	<input type="text" name="phone" value="+7 (916) 123-45-67">
	<input type="text" name="email" value="support@artegofinans.ru">
	<input type="hidden" name="key" value="mM27EwM6zd9QB4a9lLP0m4iV3zJf2FN8">
	<input type="hidden" name="af_data" value="data">
	<input type="submit">
</form>
```

Пример успешной отправки запроса:

http://www.yoursite.ru/credit/?status=done

Пример отправки запроса с ошибками:

http://www.yoursite.ru/credit/?status=error&phone=Введите+номер+телефона

http://www.yoursite.ru/credit/?status=error&error=Система+временно+недоступна
