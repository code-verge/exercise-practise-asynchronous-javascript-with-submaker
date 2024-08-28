# Practise Asynchronous JavaScript with SubMaker

## Learning Goals

By completing this exercise, you will be able to:

- Implement asynchronous operations using Promises
- Use async/await syntax for handling asynchronous code
- Chain multiple asynchronous operations in a specific order
- Handle potential errors in asynchronous operations
- Simulate real-world scenarios using JavaScript in the browser

## Introduction

Welcome to SubMaker, the cutting-edge sandwich shop simulation!

As a talented front-end developer, you’ve been hired to create the digital backbone of this innovative eatery’s web application. Your mission is to implement the step-by-step process of creating and serving a sandwich, all while mastering the art of asynchronous JavaScript in the browser.

In this exercise, you’ll bring to life the intricate dance of sandwich creation, from choosing toppings to the final bite (or takeaway box). You’ll use Promises and async/await to ensure each step happens in the perfect order, just like in a real sandwich shop.

Are you ready to blend the world of culinary arts with the power of asynchronous JavaScript? Let’s dive in and create some code as delicious as the sandwiches we’re simulating!

## Getting Started

1. Fort this repository
2. Clone the repository to your computer
3. Open the repository in VS Code
4. Start the Live Server in VS Code
5. Follow instructions

## The Sandwich Making Process

Here are the steps involved in making a sandwich, always occuring in this specific order:

1. Choose Topping (e.g. Ham, Turkey, Beef, Chicken, Veggi)
2. Choose Bread (e.g. White, Whole Wheat, Rye, Sourdough, Ciabatta)
3. Choose Cheese (e.g. Cheddar, Swiss, Provolone, Mozzarella)
4. Toasted/Not Toasted
5. Choose Vegetables (e.g. Lettuce, Tomato, Onion, Cucumber, Peppers)
6. Choose Sauce (e.g. Mayonnaise, Mustard, Ranch, BBQ, Honey Mustard)
7. Wrap or Package the Sandwich (Eat in restaurant/takeout)
8. Pay with Cash/Pay with Card
9. If Eat in Restaurant: Eat in Restaurant
10. If Takeout: Leave Restaurant

## Instructions

### Part 1: Scaffold the Functions

1. Create separate functions for each step in the sandwich-making process. Each function should return a Promise that resolves after a random delay (between 1-3 seconds) to simulate the time takes for each step.

Example:

```javascript
// e.g. Ham, Turkey, Beef, Chicken, Veggi
function chooseTopping(topping) {
	return new Promise((resolve) => {
		setTimeout(() => {
			console.log(`Topping choses: ${topping}`);
			resolve(topping);
		}, Math.random() * 2000 + 1000 )
	}
}
```

1. Implement similar functions for all the steps mentioned above.

### Part 2: Chaining with Promises

1. Use the `.then()` syntax to chain all the functions together in the correct order.
2. Implement error handling using `.catch()`.

### Part 3: Implementing with Async/Await

1. Create an async function called `makeSandwich()` that uses await to call each step in order.
2. Use try/catch for error handling.

### Part 4: Adding Conditions

1. Implement the conditional steps (e.g. Eat in Restaurant/Take away) using if/else statements within your async function.
2. Ensure that the appropriate final step (Eat in Restaurant or Leave Restaurant) is called based on the earlier choice.

## Submission

When you've completed the exercise:
1.	Commit your changes:

```bash
git add .
git commit -m "Completed SubMaker exercise"
git push origin main
```

2.	Create a Pull Request
3.	Submit the URL of your Pull Request

## Bonus Challenges

### Let Chaos Reign

1. Adjust your existing functions so that promises fail occasionally.
2. Implement error handling for these occasional failures, ensuring your program gracefully recovers and continues the sandwich-making process.
3. Add a "retry" mechanism for failed steps, allowing the program to recover from failed steps and continue the program.

### Display Results in the Browser

1. Create a function `updateUI(message)` that adds the provided message to a list in the HTML.
2. Modify your step functions to call `updateUI(...)` with appropriate messages.

Hint: Use the following body for the `updateUI(...)` function:

```javascript
function updateUI(message) {
  const list = document.getElementById('order-steps');
  const listItem = document.createElement('li');
  listItem.textContent = message;
  list.appendChild(listItem);
}
```

> [!NOTE]  
> We’ll examine the DOM (Document Object Model) in great detail in the next couple of days and you’ll learn exactly what is happening in this couple of lines.

## You Got Questions? We Got Answers!

<details>
<summary>How can I simulate a network request in the browser without actually making one?</summary>

You can use setTimeout() to simulate the delay of a network request. For example:

```javascript
    function simulateNetworkRequest(data) {
    return new Promise((resolve) => {
        setTimeout(() => {
        resolve(data);
        }, Math.random() * 1000 + 500); // Random delay between 500-1500ms
    });
    }
```
This allows you to mimic the asynchronous nature of network requests without actually making any.
</details>
    
<details>    
<summary>How can I pass data between different steps of the sandwich-making process?</summary>

You can pass data between steps by returning values from each Promise and receiving them in the next .then() or await. For example:

```javascript
    async function makeSandwich() {
    try {
        const topping = await chooseToppings();
        const bread = await chooseBread(topping); // Pass topping to bread selection
        const cheese = await chooseCheese(topping, bread); // Pass previous choices
        // ... and so on
    } catch (error) {
        console.error("An error occurred:", error);
    }
    }
```
This allows each step to potentially influence the next steps.
</details>
    
<details>
<summary>How do I simulate a step that might fail occasionally?</summary>

You can use Math.random() to occasionally reject a Promise. For example:

```javascript
    function toastBread() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
        if (Math.random() < 0.1) { // 10% chance of failure
            reject(new Error("Toaster malfunction!"));
        } else {
            resolve("Bread toasted successfully");
        }
        }, Math.random() * 2000 + 1000);
    });
    }
```
This simulates a step that might occasionally fail, allowing you to practice error handling.
</details>
    

Remember, asynchronous programming is a crucial skill in JavaScript, especially in browser-based applications. Take your time to understand each concept, and don’t hesitate to experiment with different approaches.

Happy coding, sandwich artists!