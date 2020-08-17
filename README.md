# Crossbeam Coding Challenge

## Sibilant
Welcome to the Crossbeam challenge project!

This project uses a language called Sibilant. Sibilant is very simple and can be learned quickly. A comprehensive walkthrough of the language is here: https://sibilant.org/


To install Sibilant, run: 
`npm install -g sibilant`


To run my code solution, use:
`sibilant -x -f crossbeam.sibilant`

## The challenge
The challenge: You are given a list of tasks, some of which depend on others. Write a function which will takes a subset of those tasks and returns an ordered list of all the tasks to run.

(def determine-order (tasks, chosen-tasks) null)

Examples:

(var example-tasks
[{task "make a sandwich", depends ["buy groceries"]}
{task "buy groceries", depends ["go to the store"]}
{task "go to the store", depends []}])

The following should print:

Output: [ 'go to the store', 'buy groceries', 'make a sandwich' ]
From: (console.log (determine-order example-tasks ["make a sandwich"]))

The following should also print:

Output: [ 'go to the store', 'buy groceries', 'make a sandwich' ]
From: (console.log (determine-order example-tasks ["buy groceries" "make a sandwich"]))

Write any additional test cases which demonstrate the correctness of your solution.

Please also write a description of how your algorithm works.

# My Solution
In the file crossbeam.sibilant you will find my algorithm solution to this problem along with some test data and test results. Running the solution using `sibilant -x -f crossbeam.sibilant` will print out all the test info and results for you to verify.

Based on the test data that was provided with this challenge, my solution makes the following assumptions:
- That the example-tasks data will be an ordered array that starts with the final result tasks (one where no other task depends on it) and ends with the beginning tasks (one that has no dependents)
- That the example task subset array will be in order from beginning tasks (one that has no dependents) and ends with the final result tasks (one where no other task depends on it)

Using the assumptions above, we know that the last task in the example-task subset input will be the farthest along in the example tasks that we will need output along with any tasks that are its dependents (directly or through another task). Since the example-task array is ordered from final task to beginning task, we can work out way backwards in through that array, building a new array of just the object "task" values until we find a match where the object task equals that last task in the example-task subset array. Once we reach that point we know that we do not need to add any more tasks so we can break out of the loop and return the array we created with the ordered list of al the tasks to run. If we make it all the way through the array and we have not found a match where object task equals that last task in the example-task subset array then we know that the task was not part of the example tasks and we will set our needed-tasks-arr to an empty array to return.

If the assumptions above about the data are not correct, and the example tasks were not provided in an ordered array, I think the best way to handle it would be to create a recursive function that started at the initial task (one with no dependents) and worked its way through the objects by matching on task value to depends value. We could use this function to create an ordered array which would work with the function I created. 





