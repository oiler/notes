# Laravel

## Getting Started

### Composer
[Download Composer](https://getcomposer.org/download/)
```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
and if you need to move composer to a custom php bin, pick one of the following (not both)
```bash
mv composer.phar /usr/local/bin/composer
mv composer.phar /Applications/MAMP/bin/php/php7.2.1/bin/composer
```

### Create project
new project in existing folder
```bash
composer create-project laravel/laravel --prefer-dist 
```
new project in new folder
```bash
composer create-project laravel/laravel newFolder
```

### Views
display data
{{ //code }}

layouts
```laravel
@extends('layouts.master')
```
modules
```laravel
@yields('content')
```
inheritance
```laravel
@section('content)
//stuff
@endsection
```
partial views
```laravel
@include
```
control structures
```laravel
@if(2 === 2)
    <div>this is true</div>
@else
    <div>this is false</div>
@endif

@for($i=0; $i<5; $i++)
    <div>{{ $i }}. iteration</div>
@endfor
```
xss protection
```laravel
{{ "<div>normal output <script>alert('hello');</script></div>" }}
{!! "<div>unescaped output <script>alert('hello');</script></div>" !!}

```
facades - static file including
```laravel
{{ URL::to('css/styles.css') }}
```

### Routing
named routes
```laravel
Route::get('page/about', function() {
	return view('page.about');
})->name('page.about');
```
usage: `{{ route('page.about') }}`

route parameters
```laravel
Route::get('post/{id}', function() {
	return view('posts.index');
})->name('posts.post');
```
usage: `{{ route('posts.post', ['id' => 1]) }}`

http post routes
```laravel
Route::post('admin/create', function() {
	return view('posts.index');
})->name('admin.create');
```
usage: `<form action="{{ route('admin.create')" method="post">`

group routes together
```laravel
Route::group(['prefix' => 'admin'], function() {
    Route::get('', function() {
        return view('admin.index');
    })->name('admin.index');
    Route::get('create', function() {
        return view('admin.create');
    })->name('admin.create');
});
```


