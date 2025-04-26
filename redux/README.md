# REDUX (library)

- It is a predictable state container for Javascript apps.
- Helps manage the global state of your application.
- react-redux is a library that provides bindings to connect Redux with React apps.

3 concepts
1. Store - Holds the state of your application.
2. Action - Plain JS objects that describe an intention to change the state.
3. Reducer -  A pure function that takes the current state and action, and returns the new state.

## Store
- Holds application state
- Provides access to state via getState().
- Updates state using dispatch(action).
- Registers change listeners via subscribe(listener).
- Allows unsubscribe via the function returned from subscribe()

## Actions
- Actions are plain JS objects with a type field.Optionally contain a payload with extra data.

## Action Creator
- An action creator is simply a function that returns an action 

## Reducers
- Pure functions: (state, action) => newState
- Must not mutate state directly.
- Use switch-case on action types.

## Middleware
- Redux Thunk is a middleware that lets you write functions inside your actions — instead of just plain objects — to handle asynchronous logic like API calls.
- Redux Logger logs actions and state changes to console.

```

import { applyMiddleware, combineReducers, createStore } from "redux";
import logger from "redux-logger";
import { thunk } from "redux-thunk";
import axios from "axios";

const bakeryState = {
  icecream: 10,
  cake: 20,
};

const BUY_CAKE = "BUY_CAKE";
const BUY_ICECREAM = "BUY_ICECREAM";

const buyCake = () => {
  return {
    type: BUY_CAKE,
  };
};

const buyIcecream = () => {
  return {
    type: BUY_ICECREAM,
  };
};

const bakeryReducer = (state = bakeryState, action) => {
  switch (action.type) {
    case BUY_ICECREAM:
      return {
        ...state,
        icecream: state.icecream - 1,
      };
    case BUY_CAKE:
      return {
        ...state,
        cake: state.cake - 1,
      };
    default:
      return state;
  }
};

const userState = {
  loading: false,
  users: [],
  error: "",
};

const GET_USERS_LOADING = "GET_USERS_LOADING";
const GET_USERS_SUCCESS = "GET_USERS_SUCCESS";
const GET_USERS_FAILURE = "GET_USERS_FAILURE";

const getUsersLoading = () => {
  return {
    type: GET_USERS_LOADING,
  };
};

const getUsersSuccess = (data) => {
  return {
    type: GET_USERS_SUCCESS,
    payload: data,
  };
};

const getUsersFailure = (err) => {
  return {
    type: GET_USERS_FAILURE,
    payload: err,
  };
};

const userReducer = (state = userState, action) => {
  switch (action.type) {
    case GET_USERS_LOADING:
      return {
        ...state,
        loading: true,
      };
    case GET_USERS_SUCCESS:
      return {
        ...state,
        loading: false,
        error: "",
        users: action.payload,
      };
    case GET_USERS_FAILURE:
      return {
        ...state,
        loading: false,
        users: [],
        error: action.payload,
      };
    default:
      return state;
  }
};

export const getUsers = () => {
  return function (dispatch) {
    dispatch(getUsersLoading());
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        dispatch(getUsersSuccess(res.data));
      })
      .catch((err) => dispatch(getUsersFailure(err.message)));
  };
};

const rootReducer = combineReducers({
  bakeryReducer,
  userReducer,
});

const store = createStore(rootReducer, applyMiddleware(logger, thunk));

console.log(store.getState(), "state");

const unsubscribe = store.subscribe(() => {
  console.log(store.getState());
});

store.dispatch(buyCake());
store.dispatch(buyCake());
store.dispatch(buyIcecream());
store.dispatch(getUsers());

unsubscribe();

```

##  react-redux

- react-redux is a library that provides bindings to connect Redux with React apps.

**store.js**

```

import { createStore, applyMiddleware, combineReducers } from "redux";
import { bakeryReducer } from "./bakeryReducer";
import { userReducer } from "./userReducer";
import thunk from "redux-thunk";
import logger from "redux-logger";

const rootReducer = combineReducers({
  bakery: bakeryReducer,
  user: userReducer,
});

export const store = createStore(rootReducer, applyMiddleware(thunk, logger));

```

**index.js (or your app entry)**

```

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { Provider } from "react-redux";
import { store } from "./store";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);

```

**connect()**

```

import React from "react";
import { connect } from "react-redux";
import { buyCake, buyIcecream } from "./bakeryReducer";

const BakeryComponentConnect = ({ cake, icecream, buyCake, buyIcecream }) => {
  return (
    <div>
      <h2>Bakery Items (Connect Way)</h2>
      <p>Cakes: {cake}</p>
      <p>Icecreams: {icecream}</p>
      <button onClick={buyCake}>Buy Cake</button>
      <button onClick={buyIcecream}>Buy Icecream</button>
    </div>
  );
};

const mapStateToProps = (state) => {
  return {
    cake: state.bakery.cake,
    icecream: state.bakery.icecream,
  }
}

const mapDispatchToProps = (dispatch)=>{
  return {
    buyCake:()=>dispatch(buyCake()),
    buyIcecream:()=>dispatch(buyIcecream()),
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(BakeryComponentConnect);

```

**Hooks**

```

import React, { useEffect } from "react";
import { useSelector, useDispatch } from "react-redux";
import { getUsers } from "./userReducer";

const UserComponentHooks = () => {
  const { loading, users, error } = useSelector((state) => state.user);
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(getUsers());
  }, [dispatch]);

  return (
    <div>
      <h2>Users (Hooks Way)</h2>
      {loading && <p>Loading...</p>}
      {error && <p>Error: {error}</p>}
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
};

export default UserComponentHooks;

```

## Redux toolkit
- Redux toolkit is the library for the efficient redux development
- It simplifies the process of writing Redux logic.
- It comes with utilities like createSlice, configureStore, and built-in redux-thunk for async logic.

- configureStore() - Simplified version of createStore, automatically sets up Redux DevTools and accepts middleware easily.
- createSlice() - Combines action creators + reducer logic into one piece.
- createAsyncThunk() - Simplifies async API calls like fetching users.

npm i @reduxjs/toolkit

**bakerySlice.js**

```

import { createSlice } from '@reduxjs/toolkit';

const bakerySlice = createSlice({
  name: 'bakery',
  initialState: {
    cake: 20,
    icecream: 10,
  },
  reducers: {
    buyCake: (state) => {
      state.cake--; // RTK uses Immer.js, so direct state mutation is allowed safely
    },
    buyIcecream: (state) => {
      state.icecream--;
    },
  },
});

export const { buyCake, buyIcecream } = bakerySlice.actions;
export default bakerySlice.reducer;

```

**userSlice.js**

```

import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import axios from 'axios';

// Async thunk for fetching users
export const fetchUsers = createAsyncThunk('users/fetchUsers', async () => {
  const response = await axios.get('https://jsonplaceholder.typicode.com/users');
  return response.data;
});

// Because async/await makes the code cleaner, easier to read, and avoid deep .then() chains:
// Easier to add try/catch for error handling later.

(or)

// export const fetchUsers = createAsyncThunk('users/fetchUsers', () => {
//   return axios.get('https://jsonplaceholder.typicode.com/users')
//     .then((response) => response.data);
// });

const userSlice = createSlice({
  name: 'users',
  initialState: {
    loading: false,
    users: [],
    error: '',
  },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.loading = true;
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.loading = false;
        state.users = action.payload;
        state.error = '';
      })
      .addCase(fetchUsers.rejected, (state, action) => {
        state.loading = false;
        state.users = [];
        state.error = action.error.message;
      });
  },
});

export default userSlice.reducer;

```

**store.js**

```

import { configureStore } from '@reduxjs/toolkit';
import bakeryReducer from './bakerySlice';
import userReducer from './userSlice';
import logger from 'redux-logger';

const store = configureStore({
  reducer: {
    bakery: bakeryReducer,
    users: userReducer,
  },
  middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(logger),
  devTools: true,
});

export default store;

```

**App.js**

```

import React, { useEffect } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { buyCake, buyIcecream } from './bakerySlice';
import { fetchUsers } from './userSlice';

const App = () => {
  const bakery = useSelector((state) => state.bakery);
  const users = useSelector((state) => state.users);
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch(fetchUsers());
  }, [dispatch]);

  return (
    <div>
      <h2>Bakery</h2>
      <p>Cakes: {bakery.cake}</p>
      <p>Icecreams: {bakery.icecream}</p>
      <button onClick={() => dispatch(buyCake())}>Buy Cake</button>
      <button onClick={() => dispatch(buyIcecream())}>Buy Icecream</button>

      <h2>Users</h2>
      {users.loading && <p>Loading...</p>}
      {users.error && <p>Error: {users.error}</p>}
      {users.users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
};

export default App;

```

**index.js**

```

import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

```

**You can also access all this properties in thunkApi**

```

export const fetchUsers = createAsyncThunk(
  'users/fetchUsers',
  async (payload, thunkAPI) => {
    console.log(payload); // the data you pass when dispatching
    console.log(thunkAPI.getState()); // Redux state
    console.log(thunkAPI.dispatch); // dispatch function
    console.log(thunkAPI.signal); // AbortController for cancellation

    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/users');
      return response.data;
    } catch (err) {
      return thunkAPI.rejectWithValue(err.message); // better error control
    }
  }
);

```
