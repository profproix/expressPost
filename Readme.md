# POST

## Learning Goals

- [ ] **Understand the request response cycle**
- [ ] **Recall HTTP Requests and VERBS**
- [ ] **Configure an express server**
- [ ] **Configure an express cors**
- [ ] **Create a POST route that receives data from request parameters**

## Note about this lab

This Lab will be similar to the Express lab but weill be looking at a POST requests and testing them in Postman

## Postman

We typically make requests from the frontend client, but when we are working on the backend API it’s often necessary to test our routes without using the client. **Postman** is a tool that lets you send HTTP requests directly so you can verify that your API endpoints work.

Sign up for a free account here:  
[Postman](https://www.postman.com/)

## Review as necessary

This content is the same as in the Express lab. Review it if you need a refresher, but feel free to skip it if you’re already familiar with the material.

## Review: The Request-Response Cycle

Client-server architecture is widely used in modern software development. In this model, a client application, such as a web browser on a phone, sends a request to a backend server. The server processes the request and sends a response back to the client.

## Review: HTTP Requests (Hypertext Transfer Protocol)

HTTP is a protocol for transferring data over the web in a client–server model. It’s language-agnostic, meaning it works with many different programming languages.

Think of it like sending a letter back and forth between your computer and a server. Just as a letter has stamps, an address, and a return address, an HTTP request has key parts that help it do its job. Here are some of the most important:

- **Request URL**: The “address” of the request—where it’s being sent.
- **HTTP headers**: Extra information (metadata) that accompanies the request or response.
- **HTTP methods (verbs)**: Indicate the purpose of the request, whether you’re reading data, creating new data, updating existing data, or deleting data.
- **HTTP status codes**: Show the outcome of the request—whether it succeeded or failed. A common example you may already know is **404**, which means the requested resource was not found.

Find more info on [HTTP in the MDN docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview)

## Review: HTTP Method

As mentioned above, the HTTP method determines what action the request is asking the server to perform.

| HTTP Verb | Description                                  | Example Use Case                               |
| --------- | -------------------------------------------- | ---------------------------------------------- |
| GET       | Retrieve data from the server                | Fetching a list of restaurants                 |
| POST      | Send data to the server to create a resource | Adding a new restaurant to the database        |
| PUT       | Update an existing resource entirely         | Updating the details of an existing restaurant |
| PATCH     | Partially update an existing resource        | Changing a restaurant's hours of operation     |
| DELETE    | Remove a resource from the server            | Deleting a restaurant from the database        |

## Review JSON

JavaScript Object Notation (JSON) is the format used to transfer data across the web.  
It’s technically plain text, which makes it lightweight and perfect for sending data quickly.

JSON looks very similar to JavaScript object literals, but **all keys must be strings**.

```
{"name": "rose", "age": 14}
```

## Lab Deliverables

1. Configure express

- Import `restaurants` from `data.js`.
- Invoke `express` and assign it to a variable called `app`.
- Create a variable called `port` and set it to `3000`.
- Call `app.use` and pass it `cors()` to enable cross-origin requests.
  - CORS is a security feature that typically prevents communication between servers and clients on different domains. Here, we’re allowing this communication.
- Call `app.use` and pass it `express.json()`. This middleware parses incoming JSON requests and converts them into JavaScript objects.
- Leave some blank space for additional code to be added later.
- Call `app.listen`, passing the `port` variable and a callback function.
- In the callback, create a `console.log` that says `Server running on http://localhost:${port}`.

<details>
  <summary>Click Here to view solution</summary>

```

import express  from 'express'
import cors from 'cors'
import {restaurants} from './data.js'
const app = express();
const port = 3000;
app.use(cors());
app.use(express.json());


//Leave space here for more code


app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});


```

</details>

2. Create a POST request that receives data from the client

- Invoke `app.post`, passing it the path `'/restaurants'` and a callback function with parameters `req` and `res`.
- Inside the callback, create a variable called `newRestaurant` and set it to an object literal. Set the keys of the object to `name`, `address`, `phone`, `cuisine`, `rating`, `hours`, and `menu`. Use the corresponding data from the request body, e.g., `req.body.name`.
- Push `newRestaurant` to the `restaurants` array.
- Invoke `res.status(201)` and chain `.json()`, passing `newRestaurant` as the response.
- Verify your work using Postman.
  ![postman image select plus button](images/postman1.png)
- Navigate to a new workspace and select the pluse button
  ![postman image select POST from method drop down ](images/postman2.png)
- Click the drop down menu that says GET and select POST
  ![postman image fill out url, select body, select raw and enter a json object ](images/postman2.png)
- Enter the **Request URL** to your server.
- Select the **Body** tab and choose **raw**.
- Enter a JSON object with keys matching the parameters from your POST request:  
  `name`, `address`, `phone`, `cuisine`, `rating`, `hours`, and `menu`.

<details>
  <summary>Click Here to view solution</summary>

```

app.post('/restaurants', (req, res) => {
  const newRestaurant = {
    id: restaurants.length + 1,
    name: req.body.name,
    address: req.body.address,
    phone: req.body.phone,
    cuisine: req.body.cuisine,
    rating: req.body.rating,
    hours:req.body.hours,
    menu: req.body.menu,
    image: req.body.image,
  };

  restaurants.push(newRestaurant);
  res.status(201).json(newRestaurant);
});


```

</details>

3. Close down your server by hitting `cmd + c` (on macOS) or `ctrl + c` (on Windows/Linux)

## Submission Instructions

1. Push your code to GitHub.
2. Submit the link to your GitHub repository URL.
