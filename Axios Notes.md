

# Executing Code Globally - Interceptors



**Interceptors:** 
You can intercept requests or responses before they are handled by then or catch. They are functions you can define globally 
that will be executed for every request leaving your app, and every response returning into it.


### Manipulating Requests and Responses

In index.js:

```
// Add a request interceptor
axios.interceptors.request.use( config => {
    // Do something before request is sent
    return config;
  }, error => {
    // Do something with request error
    return Promise.reject(error);
  });

// Add a response interceptor
axios.interceptors.response.use(response => {
    // Do something with response data
    return response;
  }, error => {
    // Do something with response error
    return Promise.reject(error);
  });
```

You have to return the request config, otherwise you're blocking the request.

### Defaults
-
Assume you're always sending requests to the same URL. Or you want to set a common header.

In index.js:

```
axios.defaults.baseURL = 'https://json....';
axios.defaults.headers.common['Authorization'] = 'AUTH TOKEN';
axios.defaults.headers.post['Content-Type'] = 'application/json'; // This is default
```

In the third case, you're only setting the defaults for post request.

### Instances

What if you don't want to have the same baseURL for your entire application, but only for parts of it? The same with headers and so on. Instances come to the rescue.

Create a new file axios.js in the source folder.

```
import axios from 'axios';

const instance = axios.create({
    baseURL: 'https://wagaboobi...'
});
```

By default, this instance will also assume the defaults set up in index.js but override anything that it sets up above. 

Now after creating the baseURL, we can do as follows:

```
instance.defaults.headers.common['Authorization'] = 'AUTH TOKEN FROM INSTANCE';
```

Now, we can use this instance in our components and containers.
