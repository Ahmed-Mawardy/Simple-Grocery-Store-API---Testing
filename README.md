# Simple Grocery Store API - Testing
This API allows you to place a grocery order which will be ready for pick-up in the store.
### API used
  Here you can find the documentation for the API:
  [Simple Grocery Store API](https://github.com/vdespa/Postman-Complete-Guide-API-Testing/blob/main/simple-grocery-store-api.md)
## Table of contents
* [Description](#Project-Description)
* [Prerequisites to run locally](#Prerequisites-to-run-locally)
* [Requests](#Requests-Sent-to-the-API)
* [Examples of Test Cases](#Test-Cases-Examples)
* [How to run in Github](#How-to-run-in-Github)  
## Project Description
The goal of this project is to test various endpoints of the Simple Grocery Store API by:
*   Sending requests to different API endpoints.
*   Validating responses with robust test cases to ensure:
    *   **Status codes** are as expected.
    *   **Response times** meet performance benchmarks.
    *   **Response body** includes the correct data.
    *   **Returned data** is consistent and accurate.
*   Ensuring proper **authentication** and **authorization** mechanisms.
*   Verifying the API's **response schema** against predefined standards.\
  ##  Technologies Used
<a href="https://www.postman.com/"><img src="https://user-images.githubusercontent.com/25181517/192109061-e138ca71-337c-4019-8d42-4792fdaa7128.png" title="POSTMAN" alt="POSTMAN" width="40" height="40"/></a>

![Newman](https://img.shields.io/badge/Newman-Command_Line-brightgreen)
## Prerequisites to run locally
  - Node.js and npm installed
  - Postman installed
  - Newman installed globally (`npm install -g newman`)
  - Download `collection.json` file, and import to Postman.
## Requests Sent to the API
+ `GET /status` - Returns the status of the API.
+ `POST /api-clients` - Registers a new clint to the API, and try to register a client that already registered.
+ `POST /carts` - Creates a new cart.
+ `GET /products` - Returnes a list of products, returns specific number of products, returns products from a specific category, and returnes only available products.
+ `POST /carts/:cartId/items` - Add an item to cart.
+ `GET /carts/:cartId` - Returns a cart, and try to return a cart with an invalid ID.
+ `GET /carts/:cartId/items` - Returnes a cart items, and try to return items of cart with invalid ID.
+ `PATCH /carts/:cartId/items/:itemId` - Modifies a quantity of specific item in the cart.
+ `PUT /carts/:cartId/items/:itemId` - Replaces an item in the cart with another product, and try to replace an item with invalid product ID.
+ `DEL /carts/:cartId/items/:itemId` - Removes an item from the cart.
+ `POST /orders` - Creates a new order by the registered client, and try to create an order with unauthorized user.
+ `GET /orders` - Returnes a list of orders created by the registered client, and try to retrieve orders with an unauthorized user.
+ `GET /orders/:orderId` - Returns a details of a specific order created by the user, and try to retrieve specific order with an unauthorized user.
+ `PATCH /orders/:orderId` - Updates order details that created by a registered user, try to update specific order with an unauthorized user, and try to update order with invalid ID.
+ `DEL /orders/:orderId` - Removes a specific order created by registered user, try to remove specific order with an unauthorized user, and try to remove order with invalid ID.
## Test Cases Examples
+ Check Status Code (200 OK, 401 Unauthorized, 404 Not found, etc.):
```
pm.test("Check that status code is 404", function () {
	pm.response.to.have.status(404);
});
```
+ Validate Error Message:
```
pm.test("Check that error message indicates an error in orderId", function () {
    pm.expect(pm.response.text().toLowerCase()).to.include("error", "order");
    pm.expect(pm.response.text().toLowerCase()).to.include("id");
});
```
+ Validate Response Time to be less than specific value:
```
pm.test("Verify that response time is less than 1500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1500);
});
```
+ Check for specific Key in the Response Body:
```
pm.test("Check that access token is returned", function () {
    pm.expect(pm.response.json()).to.have.property("accessToken");
});
```
+ Check that Response Body contains the same number of searched products:
```
pm.test("Chect that response body contains " + pm.collectionVariables.get("randomNumber") + " products", function () {
    pm.expect(pm.response.json().length).to.eql(pm.collectionVariables.get("randomNumber"));
});
```
+ Check that Response Body contains products of only searched categories:
```
pm.test("Check that response body only contains products of type: " + pm.collectionVariables.get("category"), function () {
    for (var i = 0; i < pm.response.json().length; i++)
        pm.expect(pm.response.json()[i].category).to.eql(pm.collectionVariables.get("category"));
});
```
+ Check that Response Body is written in JSON format:
```
pm.test("Check that returned data in json format", function () {
    pm.expect(pm.response.headers.get("Content-Type")).to.include("application/json;");
});
```
+ Validate that Response body has a valid schema:
```
// define the schema
var schema = {
    "type": "object",
    "required": ["id", "category", "name", "manufacturer", "price", "current-stock", "inStock"],
    "properties": {
        "id":                   {"type": "number"},
        "category":             {"type": "string"},
        "name":                 {"type": "string"},
        "manufacturer":         {"type": "string"},
        "price":                {"type": "number"},
        "current-stock":        {"type": "number"},
        "inStock":              {"type": "boolean"}
    }
};
// test the response with the schema
pm.test("Response has a valid Schema", function () {
    pm.response.to.have.jsonSchema(schema);
});
```
## How to run in Github
- Go to repository page.
- Click on `Actions` tap.
 ![Picture1](https://github.com/nourrrhan/GroceryAPI-Testing/assets/70220868/94697b91-dbc0-4d70-8457-a103989daad5)

- From the `Actions` side in the left, click on `Postman-Newman-Collection`.
 ![Picture2](https://github.com/nourrrhan/GroceryAPI-Testing/assets/70220868/772ca450-952c-4742-b217-2191578851a5)

- Click on `Run Workflow`.
 ![Picture3](https://github.com/nourrrhan/GroceryAPI-Testing/assets/70220868/8cbfd101-0167-4e6e-a71c-116bba8ec943)

- Wait untill the run starts, then click on the latest run, and wait untill it finishes.
 ![Picture4](https://github.com/nourrrhan/GroceryAPI-Testing/assets/70220868/eb40ebec-bbfa-4857-b5a8-80c608286f26)

- Scroll down to the `Artifacts` section.
 ![Picture5](https://github.com/nourrrhan/GroceryAPI-Testing/assets/70220868/3e281cc6-58f0-4ce3-80a3-02032322f513)

- Download `newman-reports` folder, and open the HTML file to see the report.
## Contact

If you have any questions, suggestions, or encounter any issues regarding this project, please don't hesitate to get in touch. Your feedback and contributions are greatly appreciated.
- **Email**: ahmedmawrdy20@gmail.com
- **linkedin**: https://www.linkedin.com/in/ahmed-mawardy-81757a153/

You're also welcome to open an issue in this repository or contact me directly. Thank you for your interest and support!




  
