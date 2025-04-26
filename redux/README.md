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
