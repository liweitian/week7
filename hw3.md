# Homework #3

**30 points**

**DUE: Tuesday, Nov 28, 6pm.**

Your task is to build a modern, functioning web service.  

You can build the service described here, or you can choose your own.
If you choose to build your own, you must submit a brief overview to me
no later than Thursday, Nov 9.

Please note that I will not read your code.  All grading is based on live, discoverable functionality.

## Web Service: Warehouse Fulfillment Center

The logistics industry is primarily concerned with the movement of
physical goods from one place to another.  You will implement a typical
segment of this industry: the warehouse fulfillment center.

A typical warehouse fulfillment center is responsible for the following:

* Storing items in the warehouse on behalf of a seller
* Shipping an item to a customer on behalf of a seller
* Receiving new items for storage in the warehouse
* Handling returned items from a customer

A 21st-century fulfillment center also does the following:

* Provides a modern, HTTP-based web service so that sellers can
build their own internal tools to keep track of their warehouse
activities.

You can earn up to 30 points by choosing any combination of the following
requirements.  Your score cannot exceed 30 points.


## Requirements

You are required to build a working web service written in Ruby, Python,
or JavaScript.  Your web service should consist of:

* A website that enables a seller's technical employees to sign up for
a developer account, so that they can gain access to the web service.
* A good set of documentation so that developers know how to setup their
developer accounts, how to acquire API keys or tokens (if you decide that those are necessary),
learn about any account restrictions/rate limiting, read sample code or
tutorials, and how to make HTTP calls to your service.
* API endpoints that enable developers to use your service to store items, ship items,
and be notified of returned items, etc.

Below are specific requirements related to each.

<hr>

### (Required) [5 points] Landing Page, Sign Up, and Documentation

* The home page of your service should be able to respond to HTML requests and
display a landing page that identifies your service.
* Provide a way to sign up for a developer account.
* Provide a way for a developer to delete their account.
* API documentation should be clear and readable, and be organized to help
new developers learn how to use your service.

Considerations:

* Do you support OAuth signups, such as logging in with GitHub or Facebook?


<hr>

### (Required) [5 points] Inventory Status

- **Required Endpoint 1:** `GET /api/inventory`
- **Browser Accessible?** Yes
- **Expected Response:** A data structure representing the current inventory status of all items owned by the seller.

* Each item is identified by its SKU, using any numbering/naming scheme you believe to be appropriate.
* Each item has an associated quantity and status.
* Each item has a status:
  * In Stock
  * Preparing for Shipment
  * Shipped
  * Returned in Good Condition
  * Returned in Bad Condition

In this example, items `A123` and `B987` each started with 1000 units and now show the following:

|SKU|Status|Qty|
|----|------|---|
|A123|In Stock|600|
|A123|Shipped|300|
|A123|Preparing for Shipment|50|
|A123|Returned in Good Condition|40|
|A123|Returned in Bad Condition|10|
|B987|In Stock|981|
|B987|Shipped|19|

- **Required Endpoint 2:** `GET /api/inventory/{item sku}`
- **Browser Accessible?** Yes
- **Expected Response:** A data structure representing the current inventory status of the requested item.

`GET /api/inventory/B987`

|SKU|Status|Qty|
|----|------|---|
|B987|In Stock|981|
|B987|Shipped|19|


Considerations:

* What error conditions might occur?  Are those errors documented?

<hr>

### (Required) [5 points] Inventory Replenishment

- **Required Endpoint:** `POST /api/inventory`
- **Browser Accessible?** No
- **Expected Request Body:** A data structure sufficient for notifying the warehouse that
the seller has provided a batch of items for storage.
- **Expected Response:** This is up to you to decide.

Considerations:

* Does the warehouse have a limit on how many items can be stored?
* What error conditions might occur?  Are those errors documented?

<hr>

### (Optional) [10 points] Place Order for Shipment

- **Required Endpoint:** `POST /api/orders`
- **Browser Accessible?** No
- **Expected Request Body:** A data structure sufficient for telling the warehouse which item to ship,
how many, and where (a street address)
**Expected Response:** A data structure representing acknowledgement of the order, if successful.

Considerations:

* Do you support international shipping, or only within one country?
* What error conditions might occur?  Are those errors documented?

<hr>

### (Optional) [10 points] JavaScript Drop-In

* Provide a file of JavaScript code that can be used by developers
to make their front-end code easier to write.  
* Provide an HTML snippet that developers can copy and paste in order
to include your JavaScript library.
* Document how to use your code.
* For a real-world example, see the <em>[Hello World](https://developers.google.com/maps/documentation/javascript/tutorial)</em> tutorial for the Google Maps API.

Example HTML Snippet: `<script src="/api/inventory.js>`

Example Usage:
``` js
let warehouse = new Warehouse();

// Gets current inventory status of all items
let items = warehouse.items();

// Access individual item properties,
// for example:
console.debug(items[0].sku)
console.debug(items[0].qty)
```


Considerations:

* Does the warehouse have a limit on how many items can be stored?
* What error conditions might occur?  Are those errors documented?



<hr>

### (Optional) [10 points] Push Notifications

Sellers often like to be notified whenever an item changes status.  
For returned items, it is often critical that the seller be notified that
a customer has returned an item in real-time, so that refunds can be issued.

* Notifications are sent to the seller via HTTP POST requests.  
* The seller must provide the warehouse with a URL endpoint.
* Your documentation should show an example of a notification JSON payload.

Considerations:

* For returned items, you could allow the seller to respond with a message
that the returned item should be put back in stock or not.
* What error conditions might occur?  How would you handle them?


### How To Submit Your Project

You have two choices:

[0 points] Submit a GitHub repository of the  source code along with an automated shell
script that will setup your application on a Linux-based system.  I can
only accept code that use SQLite, Postgresql, or MySQL.

[3 points] Deploy your web service so that I can reach it over HTTP (Heroku, AWS, Digital Ocean, etc)

Submit your URL via Canvas (either GitHub URL or live service URL).

### Comparison Examples
