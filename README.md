# Laravel Cheatsheet

## Command
- Create middleware
```
php artisan make:middleware EnsureTokenIsValid
```

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

  - namespace: Helpe organize controllers
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
- Query builder
1. Query

    - Selecting All Rows
    ```
    $users = DB::table('users')->get();
    ```
    - Selecting Specific Columns
    ```
    $users = DB::table('users')->select('name', 'email')->get();
    ```
    - Where Clauses
    ```
    $users = DB::table('users')->where('status', 'active')->get();
    ```
    - Basic Pagination
    ```
    $users = DB::table('users')->paginate(15);
    ```
2. Inserting Data

    - Single Row
    ```
    DB::table('users')->insert([
        'name' => 'John Doe',
        'email' => 'john@example.com',
        'password' => bcrypt('secret'),
    ]);
    ```
    - Multiple Rows
    ```
    DB::table('users')->insert([
        ['name' => 'John Doe', 'email' => 'john@example.com', 'password' => bcrypt('secret')],
        ['name' => 'Jane Doe', 'email' => 'jane@example.com', 'password' => bcrypt('secret')]
    ]);
    ```
3. Updating Data

    - Basic Update
    ```
    DB::table('users')
    ->where('id', 1)
    ->update(['name' => 'John Smith']);
    ```
    - Increment/Decrement
    ```
    DB::table('users')->increment('votes');
    DB::table('users')->decrement('votes', 5);
    ```
4. Deleting Data

    - Delete Rows
    ```
    DB::table('users')->where('votes', '<', 100)->delete();
    ```
    - Truncate Table
    ```
    DB::table('users')->truncate();
    ```
5. Aggregates  

    - Count, Max, Min, Avg, Sum
    ```
    $count = DB::table('users')->count();
    $max = DB::table('users')->max('price');
    $min = DB::table('users')->min('price');
    $avg = DB::table('users')->avg('price');
    $sum = DB::table('users')->sum('price');
    ```
6. Joins

    - Inner Join
    ```
    $users = DB::table('users')
            ->join('contacts', 'users.id', '=', 'contacts.user_id')
            ->select('users.*', 'contacts.phone')
            ->get();
    ```
    - Left Join
    ```
    $users = DB::table('users')
            ->leftJoin('posts', 'users.id', '=', 'posts.user_id')
            ->get();
    ```
7. Advanced Where Clauses

    - OR Clauses
    ```
    $users = DB::table('users')
            ->where('name', '=', 'John')
            ->orWhere('age', '>', 25)
            ->get();
    ```
    - Where Between
    ```
    $users = DB::table('users')
            ->whereBetween('votes', [1, 100])
            ->get();
    ```
    - Where In
    ```
    $users = DB::table('users')
            ->whereIn('id', [1, 2, 3])
            ->get();
    ```
    - Where Null
    ```
    $users = DB::table('users')
            ->whereNull('updated_at')
            ->get();
    ```
8. Ordering and Grouping

    - Order By
    ```
    $users = DB::table('users')
            ->orderBy('name', 'desc')
            ->get();
    ```
    - Group By
    ```
    $users = DB::table('users')
            ->select('department', DB::raw('count(*) as total'))
            ->groupBy('department')
            ->get();
    ```
9. Subqueries    

    - Select Subquery
    ```
    $latestPosts = DB::table('posts')
                 ->select('user_id', DB::raw('MAX(created_at) as last_post_created_at'))
                 ->groupBy('user_id');

    $users = DB::table('users')
            ->joinSub($latestPosts, 'latest_posts', function ($join) {
                $join->on('users.id', '=', 'latest_posts.user_id');
            })->get();
    ```
    - Union All

        Example1:
        ```
        $first = DB::table('users')
                ->whereNull('first_name');

        $users = DB::table('users')
                    ->whereNull('last_name')
                    ->union($first)
                    ->get();

        ```
        Example2:
        ```
        $firstQuery = DB::table('users')
                        ->whereNull('first_name')
                        ->select('id', 'name', 'role');

        $secondQuery = DB::table('admins')
                        ->select('id', 'name', 'role');

        $results = $firstQuery->unionAll($secondQuery)->get();

        ```
10. Raw Expressions
    - Raw Select
    ```
    $users = DB::table('users')
            ->select(DB::raw('count(*) as user_count, status'))
            ->where('status', '!=', 1)
            ->groupBy('status')
            ->get();
    ```
    - Where Raw
    ```
    $users = DB::table('users')
            ->whereRaw('age > ? and votes = 100', [25])
            ->get();
    ```
11. JSON Operations

    - Where JSON Field
    ```
    $users = DB::table('users')
            ->whereJsonContains('options->languages', 'en')
            ->get();
    ```
    - Updating JSON Fields
    ```
    DB::table('users')
        ->where('id', 1)
        ->update(['options->enabled' => true]);
    ```
12. Performance Optimization

    - Chunking Results
    ```
    DB::table('users')->orderBy('id')->chunk(100, function ($users) {
        foreach ($users as $user) {
            // Process each user...
        }
    });
    ```
    - Caching Queries
    ```
    $users = Cache::remember('users', 60, function () {
        return DB::table('users')->get();
    });
    ```

## Middleware

## Tip and Tric
- Why use ::class?
    - Refactor safety: make your code more maintainable. If you rename the class or change it's namespace, most modern IDEs will automatically update all instance of class
    - Readability
    - Avoid magic string 


