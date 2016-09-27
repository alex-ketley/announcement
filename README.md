![Announcement](http://demo.hocza.com/github/laravel-announcement/laravel-announcement.png)
# Laravel Announcement

A package that simplifies the management of site-wide announcements. With "Laravel Announcement" you can display auto-expiring announcements.

## Installation

1- `composer require laravelhungary/announcement`
- plz note that the package use `predis/predis` for all of its operation.

2- Add the followings to `config/app.php`

```php
'providers' => [
    ...

    LaravelHungary\Announcement\PackageServiceProvider::class,
],

'aliases' => [
    ...

    'Announce' => LaravelHungary\Announcement\Facades\Announce::class,
]
```

3- run `php artisan vendor:publish`

4- That's it.

> if you need to broadcast the announcements through something like web-sockets please check [Event Broadcasting](https://laravel.com/docs/5.3/broadcasting)

## Usage

### Normal
#### Create Announcement
`Announce::create($title, $message, $type, $ttl);`

Params
* `title` a short message.

> For example: Breaking news!

* `message` A bit longer message.

> For example: Our servers are under a DDoS attack. We are trying hard to mitigate it.

* `type` Type of the announcement.

> For example: success,info,danger,warning (or anything you would like to use) , Default is: info

* `ttl` When should the announcement expire. [Time to live] in seconds.

> Default is: 60 seconds

#### Display of Announcements

put `{!! Announce::display() !!}` anywhere you want your announcement to be visible.

===

### Broadcasting
#### Create Announcement
`Announce::broadcast($title, $message, $type, $ttl, $transition);`

Params
* `title`,`message`,`type`,`ttl` same as the [normal](#normal) announcement

* `transition` what is animation type you want.

> For example: fade , bounce, etc... [Check Vue Transition](http://vuejs.org/guide/transitions.html#CSS-Transitions) , Default is: fade

#### Display of Announcements
- note that the package doesnt care what driver you use `pusher` or `socket.io` , it will just work 🍺.
- we also use **VueJs**, but if you want to use something else then ignore the below and you are free to build your own.

1- put `Vue.component('my-announcement', require('./components/Announcement-bootstrap.vue'));` into your **app.js** file

2- put `<my-announcement></my-announcement>` anywhere you want this announcement to show up. For example: your **layout.blade.php** file

>  if you want to use `Animate.css` follow [Custom Transition Classes](https://vuejs.org/guide/transitions.html#Custom-Transition-Classes)
