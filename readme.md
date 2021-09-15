## Installing

```
yarn
```

## Run app
```
yarn serve
```

## Instructions
- On mount of the `Home` component make a rest API GET request using Axios to this mock users endpoint: https://jsonplaceholder.typicode.com/users
- Create a table (either in the `Home` component, or in a new child component) showing the users. Omit the address and company fields
- Make it possible to update user properties in the table (the user id shouldn't be editable, if you’ve added that as a column) - send Axios PUT request with updated user on button click
- Make it possible to create new users - send Axios POST request with new user

## Notes
- Documentation for the mock API: https://jsonplaceholder.typicode.com/guide/ 
- Axios documentation: https://www.npmjs.com/package/axios
- We’re looking for a simple, user friendly interface