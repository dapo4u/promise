# promise


// Creating a new Promise
let myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation using setTimeout
  setTimeout(() => {
    let success = true; // Change this to false to test the reject path
    if (success) {
      resolve("The operation was successful!");
    } else {
      reject("The operation failed!");
    }
  }, 2000); // The operation takes 2 seconds to complete
});

// Using the promise
myPromise
  .then((message) => {
    // This block runs if the promise is resolved
    console.log(message); // Output: "The operation was successful!"
  })
  .catch((error) => {
    // This block runs if the promise is rejected
    console.log(error); // Output: "The operation failed!"
  });


A new promise is created using the Promise constructor.
The promise takes an executor function with two parameters: resolve and reject.
Inside the executor function, a simulated asynchronous operation is created using setTimeout.
After 2 seconds, the promise is either resolved with a success message or rejected with a failure message, depending on the value of the success variable.
The .then() method is used to handle the promise resolution, and the .catch() method is used to handle the promise rejection.
You can change the value of the success variable to false to see how the rejection path works

Project 1: User Data Fetching
Project Structure: it has both 

index.html
script.js

the index.html is
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Promise user-data</title>
</head>
<body>
    <h1>User Data Fetching </h1>
    <div id="user-data"></div>
    <script src="script.js"></script>
</body>
</html>
 the script.js is 
 // Simulate fetching user data from an API
function fetchUserData() {
    return new Promise((resolve, reject) => {
      // Simulating an asynchronous operation using setTimeout
      setTimeout(() => {
        const success = true; // Change this to false to test the reject path
        if (success) {
          const userData = {
            name: "John Doe",
            age: 30,
            email: "john.doe@example.com"
          };
          resolve(userData);
        } else {
          reject("Failed to fetch user data.");
        }
      }, 2000); // Simulating a 2 second delay
    });
  }
  
  // Function to display user data
  function displayUserData(userData) {
    const userDataDiv = document.getElementById("user-data");
    userDataDiv.innerHTML = `
      <p><strong>Name:</strong> ${userData.name}</p>
      <p><strong>Age:</strong> ${userData.age}</p>
      <p><strong>Email:</strong> ${userData.email}</p>
    `;
  }
  
  // Function to handle errors
  function displayError(error) {
    const userDataDiv = document.getElementById("user-data");
    userDataDiv.innerHTML = `<p style="color: red;">${error}</p>`;
  }
  
  // Using the promise
  fetchUserData()
    .then((userData) => {
      displayUserData(userData);
    })
    .catch((error) => {
      displayError(error);
    });


   to run the project,use live server to run the html file


 PROJECT 2: PROMISE-JOKE 
  This is a Promise code that fetches Jokes from an API
  THE HTML CODE IS
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joke </title>
</head>
<body>
    <h1>Joke Fetcher</h1>
    <button id="fetch-joke-button">Get a Joke</button>
    <div id="joke-container"></div>
    <script src="script.js"></script>
</body>
</html>

THE SCRIPT.JS CODE IS
// Function to fetch a random joke
function fetchJoke() {
    return new Promise((resolve, reject) => {
      const xhr = new XMLHttpRequest();
      xhr.open('GET', 'https://official-joke-api.appspot.com/random_joke');
      xhr.onload = () => {
        if (xhr.status === 200) {
          resolve(JSON.parse(xhr.responseText));
        } else {
          reject('Failed to fetch a joke.');
        }
      };
      xhr.onerror = () => reject('Network error.');
      xhr.send();
    });
  }
  
  // Function to display the joke
  function displayJoke(joke) {
    const jokeContainer = document.getElementById('joke-container');
    jokeContainer.innerHTML = `
      <p><strong>Setup:</strong> ${joke.setup}</p>
      <p><strong>Punchline:</strong> ${joke.punchline}</p>
    `;
  }
  
  // Function to display an error message
  function displayError(error) {
    const jokeContainer = document.getElementById('joke-container');
    jokeContainer.innerHTML = `<p style="color: red;">${error}</p>`;
  }
  
  // Adding an event listener to the button
  document.getElementById('fetch-joke-button').addEventListener('click', () => {
    fetchJoke()
      .then((joke) => {
        displayJoke(joke);
      })
      .catch((error) => {
        displayError(error);
      });
  });

   to run the project,use live server to run the html file


