title: "Laravel permission Zizaco/Entrust"
date: 2015-03-22 17:07:07
tags: laravel
categories: Laravel
---

Zizaco/Entrust是一套權限控制系統，跟sentry不同的是他是獨立的權限系統，這對於已有原本user系統的開發者相當有幫助。

<!-- more -->

[Github](https://github.com/Zizaco/entrust)

>Laravel 4


## 安裝
`composer.json`
``` bash
"zizaco/entrust": "1.3.0"
```

``` bash
composer update
```


`config/app.php`

``` bash
Provider
    'Zizaco\Entrust\EntrustServiceProvider',

alias
    'Entrust' => 'Zizaco\Entrust\EntrustFacade',
```

Entrust會使用`config/auth.php`來決定用哪個user table

`Migration`
生成migration檔案到`database/migration`
``` bash
php artisan entrust:migration
```

``` bash
php artisan migrate
```

## 建立對應model
`app/models/Role.php`

``` php
    <?php

    use Zizaco\Entrust\EntrustRole;

    class Role extends EntrustRole
    {

    }
```

`app/models/Permission.php`

``` php
use Zizaco\Entrust\EntrustPermission;

class Permission extends EntrustPermission
{

}
```

`app/models/User.php`
加入hasRole trait

``` php
<?php

use Zizaco\Entrust\HasRole;

class User extends Eloquent /* or ConfideUser 'wink' */{
    use HasRole; // Add this trait to your user model
```

``` php
composer dump
```

that's it, 接下來就可以用上權限了。

##Example

>上面的設定步驟相信不會卡住，但主要是官方github說明真的太過跳躍，所以會有點卡住，這邊提供一個範例幫助大家理解。

[參考網址](https://phphub.org/topics/166)

部份引用

基础概念
三个主要数据对象, 以及他们之间的关系:

    * User - 用户, 一个用户可以属于多个用户组, 不直接挂钩权限, 让用户组和权限绑定;
    * Roles - 用户组, 一个用户组可以拥有多个权限;
    * Permission - 权限;

四个数据库表说明:

    * roles - 用户组信息表;
    * assigned_roles - 用户和用户组之间的对应关系;
    * permissions - 权限信息表;
    * permission_role - 权限和用户组之间的对应关系.

>建議先在route那邊先試過再佈署。

`建立一個名為Admin的群組`
``` php
    $admin = new Role;
    $admin->name = 'Admin';
    $admin->save();
```

`建立使用的權限說明`
``` php
$manageUsers = new Permission;
$manageUsers->name = 'manage_users';
$manageUsers->display_name = 'Manage Users';
$manageUsers->save();
```

>到此為止，這兩個新建資料還沒有關連，因此我們必須說他們是有關連的

`關聯群組與權限`
像是只有admin群組的人才能管理user
``` php
$admin = Role::find(1);
$manageUsers = Permission::find(1);
$admin->perms()->sync(array($manageUsers->id));
```

Ok, 關連好了，那麼接下來就要把user添加到這個群組裡，在admin的群組裡可以管理user

``` php
    $user = User::find(1); //find user
    $admin = Role::find(1); //find group
    $user->attachRole($admin);
```
    *或者你可以使用`$user->roles->attach($admin->id);`這邊只允許id進來

>到這邊我們終於把群組、群組權限、以及user加入到了群組，接下來就要告訴laravel哪時候要判斷

`判斷是否為某群組`
``` php
$user = User::find(1);
$user->hasRole("Admin");
```

`群組通過後，是否擁有某權限`
``` php
$user = User::find(1);
$user->can("manage_users");
```

`也可以多重判斷群組或權限，只要滿足其一條件過通過了`
``` php
$user = User::find(1);
$user->ability(['Admin','Owner'], ['manage_posts','manage_users']);
```

`Route filter`

``` php
    // 有 `manage_posts` 权限的用户, 才能访问 `admin/posts` 开头的链接
    Entrust::routeNeedsPermission( 'admin/post*', 'manage_posts' );

    // 属于 `Owner` 用户组的人, 才能访问 `admin/advanced*` 开头的链接
    Entrust::routeNeedsRole( 'admin/advanced*', 'Owner' );

    // 可以在第二个选项传参数组, 当前用户需要符合所有传参的用户组或者权限,
    // 才能授权成功
    Entrust::routeNeedsPermission( 'admin/post*', ['manage_posts','manage_comments'] );
    Entrust::routeNeedsRole( 'admin/advanced*', ['Owner','Writer'] );
```

That's it, enjoy it.
