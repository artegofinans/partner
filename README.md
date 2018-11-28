# Партнёрская программа

Для участия в партнёрской программе, необходимо подать заявку на support@artegofinas.ru

После утверждения заявки, вы получите ключ для доступа к сервису отправки форм заявок.

## Форма для отправки заявки на сервер АРТЕГОФинанс.

Форма должна быть отправлена на адрес `https://artegofinans.ru/forms/creditapplication.php` POST запросом.

Внешний вид формы на Вашем сайте на Ваше усмотрение.

### Параметры запроса:

- **type** - тип кредита (обязательное поле); возможные значения: `7` - Кредит бизнесу; `12` - Потребительский кредит; `15` - Залог автомобиля; `8` - Залог недвижимости; `9` - Рефинансирование; `10` - Ипотека
- **summ** - сумма кредита
- **firstname** - Имя
- **lastname** - Фамилия
- **phone** - телефон для связи (обязательное поле); формат +7 и символы 0-9()- и пробел
- **email** - email для связи
- **comment** - комментарий
- **inn** - ИНН
- **charset** - кодировка кирилистических символов формы; возможные значения: `cp1251` и `utf8` (если не указано - `utf8`)
- **key** - ключ, выданный Вам, для доступа к сервису (обязательное поле)
- **debug** - для тестов вашей формы; любой текст, например `YES` - запрос не будет регистрироваться в системе

Так же можно передавать любые поля начинающиеся на **af_** - они будут возвращены в ответе без изменений

Ответ возвращается на странице, с которой был отправлен запрос. В параметрах будет указан результат обработки запроса.

### Параметры ответа:

- **status** - статус обратки запроса; возможные значения: `done` - запрос принят успешно; `error` - при обработке обнаружены ошибки. Если ошибки касаются передаваемых полей, то в ответе будет параметр с сответствующим описанием ошибки для конкретного поля. 
- **error** - описание общией ошибки

### Пример формы отправки запроса:

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
	<input type="text" name="firstname" value="Ивайло">
	<input type="text" name="lastname" value="Тилев">
	<input type="text" name="phone" value="+7 (916) 123-45-67">
	<input type="text" name="email" value="support@artegofinans.ru">
	<input type="hidden" name="key" value="ваш-ключ-выданный-при-запросе">
	<input type="hidden" name="af_data" value="data">
	<input type="submit">
</form>
```

### Пример успешной отправки запроса:

`http://www.site.ru/page/?status=done`

### Пример отправки запроса с ошибками:

`http://www.site.ru/page/?status=error&phone=Введите+номер+телефона`

`http://www.site.ru/page/?status=error&error=Система+временно+недоступна`

Также можно использовать AJAX запрос - для этого в заголовках запроса нужно добавить `Accept: application/json`. В этом случае ответ будет в виде json масива. Поля такие же, как и при HTTP запросе/ответе.

В целях предотвращения спама отправка форм не чаще чем одну на 60 секунд.
