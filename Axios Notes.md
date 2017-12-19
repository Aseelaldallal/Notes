

# Executing Code Globally - Interceptors



**Interceptors:** 
You can intercept requests or responses before they are handled by then or catch. They are functions you can define globally 
that will be executed for every request leaving your app, and every response returning into it.

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
