# 🔌 API Testing

Коллекция Postman для тестирования REST на примере проекта **DemoShopping** и SOAP API. Коллекции включают автотесты, переменные окружения и примеры валидации ответов.

---

## 📦 Коллекции

<table>
	<thead>
		<tr>
			<th>Тип API</th>
			<th>Ссылка</th>
			<th>Описание</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>REST API</td>
			<td><a href="https://www.postman.com/altimetry-administrator-42467067/workspace/rest">Открыть в Postman</a> / <a href="https://github.com/KiwiGhxst/API-testing/blob/main/DemoShopping.postman_collection.json">Смотреть JSON</a></td>
			<td>Тестирование основных REST-эндпоинтов: /login, /products, /cart, /orders</td>
		</tr>
		<tr>
			<td>SOAP API</td>
			<td><a href="https://www.postman.com/altimetry-administrator-42467067/workspace/rest](https://www.postman.com/altimetry-administrator-42467067/workspace/soap/collection/39730520-f11f7ee0-8b68-42d7-8540-6e6bf2956739?action=share&creator=39730520">Открыть в Postman</a> / <a href="https://github.com/KiwiGhxst/API-testing/blob/main/SOAP%20Test.postman_collection.json">Смотреть JSON</a></td>
			<td>Примеры SOAP-запросов: аутентификация, получение данных</td>
		</tr>
	</tbody>
</table>

---

## 🧪 Покрытие REST API

Тестируются ключевые сценарии пользовательского пути:

- 🔐 **Авторизация**: login → token
- 📦 **Продукты**: GET `/products`, фильтрация, сортировка
- 🛒 **Корзина**: добавление, удаление, изменение количества
- 🧾 **Заказы**: оформление, история

Все запросы снабжены автотестами с валидацией структуры, типов и логики данных.

---

## 🧠 Примеры тестов

```js
pm.test("Статус-код 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Время ответа < 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});

pm.test("Ответ — массив продуктов", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.be.an("array");
});

pm.test("Каждый продукт имеет нужные поля и типы", function () {
    const jsonData = pm.response.json();

    jsonData.forEach(product => {
        pm.expect(product).to.have.property("product_id").that.is.a("number");
        pm.expect(product).to.have.property("name").that.is.a("string");
        pm.expect(product).to.have.property("description").that.is.a("string");
        pm.expect(product).to.have.property("price").that.is.a("string");
        pm.expect(product).to.have.property("category").that.is.a("string");
        pm.expect(product).to.have.property("manufacturer").that.is.a("string");
        pm.expect(product).to.have.property("imageUrl").that.is.a("string");
        pm.expect(product).to.have.property("freeShipping").that.is.a("number");
    });
});

