# Create React and Node application

### 1. Create React client application

1. create frontend folder name "client"

```sh
npx create-react-app client
```

2. Start frontend applicatino

```sh
npm start
```

### 2. Create Express backend application

1. create backend folder name "api"

```sh
> npx express-generator api
```

2. change directory: `cd api`
3. install dependencies: `npm install`
4. run the app:

```sh
> SET DEBUG=api:* & npm start
```

### 3. Create API Controller in backend

1. Create new route in routes folder named "testAPI.js"

```js
var express = require('express');
var router = express.Router();

router.get('/', (req, res, next) => {
	res.send('API is working properly');
});

module.exports = router;
```

2. Go to the app.js

```js
var testAPIRouter = require('./routes/testAPI');

...

app.use('/testAPI', testAPIRouter);
```

### 4. Utilize API in front-end react

Go to the `App.js` of client/react

```js
import React from 'react';
import logo from './logo.svg';
import './App.css';
import { render } from '../../api/app';

class App extends React.Component {
	constructor(props) {
		super(props);
		this.state = { apiResponse: '' };
	}

	callAPI() {
		fetch('https://localhost:9000/testAPI')
			.then((res) => res.text())
			.then((res) => this.setState({ apiResponse: res }));
	}

	componentWillMount() {
		this.callAPI();
	}

	render() {
		return (
			<div className="App">
				<header className="App-header">
					<img src={logo} className="App-logo" alt="logo" />
				</header>
				<p>{this.state.apiResponse}</p>
			</div>
		);
	}
}
export default App;
```

### 5. CORS Policy (Cross Origin Resource Sharing)

- to allow react application interct with another hosted domain.
- install `cors`

```sh
npm install --save cors
```

- `--save` indicates that it's going to do a global install for all applications that are on this particular system.
- go to `app.js` of "api" folder/backend and add following code:

```js
var cors = require('cors');
app.use(cors());
```

### 6. Finally run both client and api folder

- Backend

```sh
D:\MERN\react_node_app\api> npm start
```

- Frontend

```sh
PS D:\MERN\react_node_app\client> npm start
```
