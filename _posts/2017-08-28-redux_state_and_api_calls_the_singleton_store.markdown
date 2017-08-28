---
layout: post
title:  "Redux state and API calls. The Singleton Store"
date:   2017-08-28 03:30:12 +0000
---

## Unified API calls with fetch.

In general an API call will have some headers required with it. You *can* use LocalStorage, but getting thouse headers in each place can be a bit of a pain. Another option would be to simply use a functional singleton like so:

```
import fetch from 'isomorphic-fetch';
export const API_URL = process.env.REACT_APP_API_URL;

export const headers = () => {
// get headers from storage and return the desired object
}

export const parseResponse = response => {
// handle any results that you may need
}

export default {
// wrapper functions for GET, POST, PATCH and DELETE if needed.
}
```

## Connection to state.
An interesting tidbit is that the redux store is actually a singleton. As such you can import it into your api singleton and use it to modify the apps state. Let's update our singleton.

```
import store from '../store';
import { logOut } from '../actions/login';

...
export headers = () => {
    const token = store.getState().login.token // get value from state, in this case the JWT token.
}

export const parseResponse = response => {
    return response.json()
		    .then(json => {
				    if(!response.ok && response.status === 401){
						   store.dispatch(logOut()); // you can dispatch actions as well, think of logging out if token is invalid
						}
				}
		}
}
```

Cool right!
