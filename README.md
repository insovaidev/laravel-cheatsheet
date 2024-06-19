# Laravel Cheatsheet

## Routes
```
- route param:
- name route: it usefull for crete url to redirect without need route path 
- route-groups: allow u applies attributes to multiple routes. Common attributes applied in route group middleware, namespace, prefix, nameprefix, controller
  Ex:
  - middleware:
  Route::middleware(['auth'])->group(function () {
      Route::get('/dashboard', function () {
          // Uses 'auth' middleware
      });

      Route::get('/settings', function () {
          // Uses 'auth' middleware
      });
  });

  - namespace: Help oranize controller
  Route::namespace('Admin')->group(function () {
    // Controllers within the "App\Http\Controllers\Admin" namespace

    Route::get('/users', 'UserController@index'); // Refers to App\Http\Controllers\Admin\UserController@index
    Route::get('/products', 'ProductController@index'); // Refers to App\Http\Controllers\Admin\ProductController@index
  });
  - prefix: A prefix can be add to the URL of each route in the group. This useful for versioning APIs, organize route by section.

```

## Request
- Retrieving Input
    1. all(): Retrieve all input data as an associative array.
        ```
        $input = $request->all();
        ```
    2. input($key, $default = null): Retrieve a specific input value or return a default value if the input does not exist.
        ```
        input($key, $default = null): Retrieve a specific input value or return a default value if the input does not exist.
        ```
    3. only(array $keys): Retrieve only the specified input values.
        ```
        $data = $request->only(['name', 'email']);
        ```
    4. except(array $keys): Retrieve all input values except for the specified keys.
        ```
        $data = $request->except(['password']);
        ```
    5. has($key): Determine if the request contains a specific input value
        ```
        if ($request->has('name')) {
            // Do something
        }
        ```

- Query Parameters
    1. query($key = null, $default = null): Retrieve a query parameter or all query parameters if no key is specified.
        ```
        $page = $request->query('page', 1);
        $queryParams = $request->query();
        ```
- Headers
    1. query($key = null, $default = null): Retrieve a query parameter or all query parameters if no key is specified.
        ```
        $contentType = $request->header('Content-Type');
        $headers = $request->header();
        ```
- Files
    1. file($key = null, $default = null): Retrieve an uploaded file or all files if no key is specified.
        ```
        $file = $request->file('photo');
        $files = $request->file();
        ```
    2. hasFile($key): Determine if the request contains an uploaded file.
        ```
        if ($request->hasFile('photo')) {
            // Do something
        }
        ```
- Cookies
    1. cookie($key = null, $default = null): Retrieve a cookie value or all cookies if no key is specified.
        ```
        $cookie = $request->cookie('name');
        ```
- URL and Path
    1. url(): Retrieve the URL of the request.
        ```
        $url = $request->url();
        ```
    2. fullUrl(): Retrieve the full URL including the query string.
        ```
        $fullUrl = $request->fullUrl();
        ```
    3. path(): Retrieve the path of the request.
        ```
        $path = $request->path();
        ```
    2. fullUrl(): Retrieve the full URL including the query string.
        ```
        $fullUrl = $request->fullUrl();
        ```
    2. fullUrl(): Retrieve the full URL including the query string.
        ```
        $fullUrl = $request->fullUrl();
        ```
    2. fullUrl(): Retrieve the full URL including the query string.
        ```
        $fullUrl = $request->fullUrl();
        ```
- Cookies
    1. cookie($key = null, $default = null): Retrieve a cookie value or all cookies if no key is specified.
        ```
        $cookie = $request->cookie('name');
        ```


## Response

## Database

## Tip and Tric

## Road Map:
- Database
- 


