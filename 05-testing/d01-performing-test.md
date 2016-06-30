

## Introduction: Performing a test

Performing a test is straight forward: All you have to do is look at the conditions of a test case and check if the test case's **assertions** are true.

To **assert** something is to state that something is true.

Example: The Login screen

- **Condition**: The user can login successfully
- **Assertion**: After entering their username and password, the user will be logged in and looking at the home page


To perform this test condition, you would attempt to login and check if the assertion is true. If it, for instance, brought you to the forget password screen when the condition asserted that you would see the home page, the test would fail.

A test case's condition can also make multiple assertions, if necessary.

Example: The Login screen

- **Condition**: The user is able to sign in as a guest
- **Assertion 1**: After clicking the "Sign in as Guest" button, the user will looking at the home page
- **Assertion 2**: On the home page, the user name should say "Guest"
- **Assertion 3**: A "Login" button is visible



#### Independent Practice

> ***Note:*** _This is a pair programming activity._

In the previous examples, we tested if a house was indeed a house. On the whiteboard, list of other real world things (*objects*) that can be tested. No more than 4 options.

Examples: Car, Cafe, Cell Phone, Television, Laptop, etc.

Team up and do the following:

* Create at least 3 test cases that define the main features of the thing
* State the user story for each test case
* List the conditionals for each test case





## Conclusion

* What is a test case?
* What is a user story?
* Why is testing a feature important?
* Predict: What do you think "Test-Driven Development" means?
