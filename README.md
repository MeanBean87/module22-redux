
# Module 22: Redux Store 

## Description

Link to deployed application: [https://redux-refactor-5ea80906f00d.herokuapp.com/](https://redux-refactor-5ea80906f00d.herokuapp.com/)

This application was a refactoring of existing code that used "useContext" to "React Redux". This project involved determing the locations where the original global state management was used and to replace that code with code to make use of React-Redux  and Reduxjs/toolkit node package. This application was originally an e-commerce website for various fake goods and makes use of the stripe API to provide a payment portal for online transactions.

This application makes use of concurrently to install node packages for both client and server directories.

This application also makes use of GraphQl/Mongoose for storing use login data and product information. 

I do not accept responsibilities for any actions that may take place if the user enters credit card information in the stripe portal. 

#### Landing Page Example:

![1694141462922](image/README/1694141462922.png)

## Installation

For Development:

1. Clone or fork the repository from "git@github.com:MeanBean87/module22-redux.git"
2. Navigate to the root directory of the project using CLI.
3. Open in the code editor of your choice. ie vs-code - optional.
4. Install node modules using "npm install" in either CLI or integrated terminal - vs code.
5. Start the server with "npm run develop" - uses nodemon + hmr.

**Mongo DB and Node.js will need to be installed by the user before installing Node dependencies.**

Node can be installed directly from [https://nodejs.org/en](https://nodejs.org/en).

MongoDB can be installed directly from [https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/)

## Usage

1. Navigate to the deployed page by clicking this link: [https://redux-refactor-5ea80906f00d.herokuapp.com/](https://redux-refactor-5ea80906f00d.herokuapp.com/).
2. Sign-up and/or Login using the link on the nav bar.
3. Click on items to view a card of the item that contains additional information. and add them to the cart.
4. You can optionally signup to the website using first/last name, email and password.
5. When finished you can logout / login.
6. Clicking checkout will defer you to a stripe portal for payment - DO NOT ENTER ANY CREDIT CARD INFORMATION.

## Code Highlights

#### App.jsx:

```js
import { Outlet } from "react-router-dom";
import {
  ApolloClient,
  InMemoryCache,
  ApolloProvider,
  createHttpLink,
} from "@apollo/client";
import { setContext } from "@apollo/client/link/context";
// Importing Provider from react-redux
import { Provider } from "react-redux";
// Importing store from utils
import store from "./utils/store";

import Nav from "./components/Nav";


const httpLink = createHttpLink({
  uri: "/graphql",
});

const authLink = setContext((_, { headers }) => {
  const token = localStorage.getItem("id_token");
  return {
    headers: {
      ...headers,
      authorization: token ? `Bearer ${token}` : "",
    },
  };
});

const client = new ApolloClient({
  link: authLink.concat(httpLink),
  cache: new InMemoryCache(),
});

function App() {
  return (
    <ApolloProvider client={client}>
      <Provider store={store}>
        <Nav />
        <Outlet />
      </Provider>
    </ApolloProvider>
  );
}

export default App;

```

## Learning Points

Use of React, React-Redux, @Reactjs/toolkit and how to decomission code that is using "useContext" to a global statemanagement system.

## Badges

[![Node.js](https://camo.githubusercontent.com/0fad77ddd85292b8800107c5a51df2f64ff5126a0fe6dfa1eb7d4977032918e2/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4e6f64652532306a732d3333393933333f7374796c653d666f722d7468652d6261646765266c6f676f3d6e6f6465646f746a73266c6f676f436f6c6f723d7768697465)](https://img.shields.io/badge/Node%20js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white) [![JavaScript](https://camo.githubusercontent.com/93c855ae825c1757f3426f05a05f4949d3b786c5b22d0edb53143a9e8f8499f6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4a6176615363726970742d3332333333303f7374796c653d666f722d7468652d6261646765266c6f676f3d6a617661736372697074266c6f676f436f6c6f723d463744463145)](https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E) [![MongoDB](https://camo.githubusercontent.com/72e92f69f36703548704a9eeda2a9889c2756b5e08f01a9aec6e658c148d014e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d6f6e676f44422d3445413934423f7374796c653d666f722d7468652d6261646765266c6f676f3d6d6f6e676f6462266c6f676f436f6c6f723d7768697465)](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white) [![Mongoose](https://camo.githubusercontent.com/f4d9b04b57c01393bf5d05c019adff596b47cbca2f98ab897d5416289694354e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d6f6e676f6f73652d3544424636333f7374796c653d666f722d7468652d6261646765266c6f676f3d6d6f6e676f6462266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/f4d9b04b57c01393bf5d05c019adff596b47cbca2f98ab897d5416289694354e/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4d6f6e676f6f73652d3544424636333f7374796c653d666f722d7468652d6261646765266c6f676f3d6d6f6e676f6462266c6f676f436f6c6f723d7768697465) [![Apollo](https://camo.githubusercontent.com/cd847e0c87f014c47c1113992234359d466988e012c98e8f315f371454c61197/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f41706f6c6c6f2d3331314338373f7374796c653d666f722d7468652d6261646765266c6f676f3d61706f6c6c6f2d6772617068716c266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/cd847e0c87f014c47c1113992234359d466988e012c98e8f315f371454c61197/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f41706f6c6c6f2d3331314338373f7374796c653d666f722d7468652d6261646765266c6f676f3d61706f6c6c6f2d6772617068716c266c6f676f436f6c6f723d7768697465) [![GraphQL](https://camo.githubusercontent.com/9871c232160592c5388d9013a3f5d80eb3b36f2416e63927486890e79802c935/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4772617068514c2d4531303039383f7374796c653d666f722d7468652d6261646765266c6f676f3d6772617068716c266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/9871c232160592c5388d9013a3f5d80eb3b36f2416e63927486890e79802c935/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4772617068514c2d4531303039383f7374796c653d666f722d7468652d6261646765266c6f676f3d6772617068716c266c6f676f436f6c6f723d7768697465) [![React](https://camo.githubusercontent.com/1ed9d2404ae620a67a99495ae165ca9a5f5b61b87d79ecaeb1f2cab1cff05112/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f52656163742d3631444146423f7374796c653d666f722d7468652d6261646765266c6f676f3d7265616374266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/1ed9d2404ae620a67a99495ae165ca9a5f5b61b87d79ecaeb1f2cab1cff05112/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f52656163742d3631444146423f7374796c653d666f722d7468652d6261646765266c6f676f3d7265616374266c6f676f436f6c6f723d7768697465) [![React Router DOM](https://camo.githubusercontent.com/df8533da722650e40a251e6084ab564c759eee08c400f2ab92c309d3d4b6e473/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f52656163745f526f757465725f444f4d2d4341343234353f7374796c653d666f722d7468652d6261646765266c6f676f3d72656163742d726f75746572266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/df8533da722650e40a251e6084ab564c759eee08c400f2ab92c309d3d4b6e473/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f52656163745f526f757465725f444f4d2d4341343234353f7374796c653d666f722d7468652d6261646765266c6f676f3d72656163742d726f75746572266c6f676f436f6c6f723d7768697465) [![JWT](https://camo.githubusercontent.com/f44a28d0fd77ec46eb0b615ab9d93ff7fcdf83061830b7d7087681e0d88384c6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4a57542d3030303030303f7374796c653d666f722d7468652d6261646765266c6f676f3d4a534f4e253230576562253230546f6b656e73266c6f676f436f6c6f723d7768697465)](https://camo.githubusercontent.com/f44a28d0fd77ec46eb0b615ab9d93ff7fcdf83061830b7d7087681e0d88384c6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4a57542d3030303030303f7374796c653d666f722d7468652d6261646765266c6f676f3d4a534f4e253230576562253230546f6b656e73266c6f676f436f6c6f723d7768697465) ![React Redux](https://img.shields.io/badge/React-Redux-764ABC?logo=redux) ![Redux Toolkit](https://badgen.net/badge/Redux%20Toolkit/v1.6.1/green)

## Author

Michael Mattingly

* [GitHub](https://github.com/MeanBean87)
* [LinkedIn](https://www.linkedin.com/in/michael-mattingly-5580b1280/)

This project was created with source code provided from UC Berkeley Extension.

This project uses the following packages:

* Node.js - [https://nodejs.org/en](https://nodejs.org/en)
* Express - [http://expressjs.com/](http://expressjs.com/)
* MongoDB - [https://www.mongodb.com/](https://www.mongodb.com/)
* Mongoose - [https://mongoosejs.com/](https://mongoosejs.com/)
* Apollo - [https://www.apollographql.com/](https://www.apollographql.com/)
* GraphQL - [https://graphql.org/](https://graphql.org/)
* React - [https://react.dev/](https://react.dev/)
* React Router - [https://reactrouter.com/en/main](https://reactrouter.com/en/main)
* JWT - [https://jwt.io/](https://jwt.io/)
* React-Redux - [https://www.npmjs.com/package/react-redux](https://www.npmjs.com/package/react-redux)
* @Reduxjs/toolkit - [https://www.npmjs.com/package/@reduxjs/toolkit](https://www.npmjs.com/package/@reduxjs/toolkit)

## License

This project is licensed under the [MIT License](https://github.com/MeanBean87/readme-generator/blob/main/LICENSE). Please refer to the LICENSE file for more details.
