<p align="center">
<a href="https://github.com/maddog888/laravel-admin">
<h2 align="center">laravel-admin</h2>
</a>
</p>

<p align="center">Administrative interface builder for Laravel. Build CRUD backends with a few lines of code.</p>

<p align="center">
<a href="https://github.com/maddog888/laravel-admin">Repository</a> |
<a href="UPGRADE.md">Upgrade guide</a> |
<a href="#extensions">Extensions</a> |
<a href="CONTRIBUTING.md">Contribute</a>
</p>

<p align="center">
    <a href="https://github.com/maddog888/laravel-admin">
        <img src="https://img.shields.io/badge/PHP-8.2%2B-777BB4?style=flat-square" alt="PHP 8.2+">
    </a>
    <a href="https://github.com/maddog888/laravel-admin">
        <img src="https://img.shields.io/badge/Laravel-10%20%7C%2011%20%7C%2012%20%7C%2013-FF2D20?style=flat-square" alt="Laravel 10 to 13">
    </a>
</p>

<p align="center">
    Maintained independently from <a href="https://github.com/z-song/laravel-admin">z-song/laravel-admin</a>.
    The PHP namespace stays <code>Encore\Admin</code>. The Packagist name is <code>maddog888/laravel-admin</code>.
</p>

Requirements
------------

- PHP >= 8.2
- Laravel 10, 11, 12 or 13
- Fileinfo PHP Extension

Versions
------------

| Version | Branch   | PHP       | Laravel | Frontend                                              | Status |
|---------|----------|-----------|---------|-------------------------------------------------------|--------|
| 2.x     | `master` | 8.2+      | 10 – 13 | AdminLTE 4, Bootstrap 5.3, jQuery 3.7, Font Awesome 6 | active |
| 1.x     | `1.x`    | 7.2 – 8.x | 6 – 8   | AdminLTE 2, Bootstrap 3.4.1, jQuery 3.7 + migrate, FA 4 | legacy |

`master` is the 2.x line. Upgrading an existing 1.x app? Read [UPGRADE.md](UPGRADE.md).

Installation
------------

```bash
composer require maddog888/laravel-admin
```

Do not install this next to the original `encore/laravel-admin` package. Both ship the `Encore\Admin` namespace, so remove the old one first if it is already in the application.

Publish the assets and install the admin tables:

```bash
php artisan vendor:publish --provider="Encore\Admin\AdminServiceProvider"
php artisan admin:install
```

The config file is `config/admin.php`. It controls the route prefix, database connection, and table names.

Open `http://localhost/admin/` and log in with username `admin` and password `admin`.

Configurations
------------

`config/admin.php` holds the admin settings.

Right to left support
------------

The RTL build of AdminLTE loads automatically for right-to-left locales (`ar`, `fa`, `he`, `ur`, ...).
Set `rtl` in `config/admin.php` to `true` or `false` to force it on or off.

Dark mode
------------

Set `theme` in `config/admin.php` to `light`, `dark` or `auto`. Users can switch the color mode from the navbar.

Global search
------------

The navbar search box (`/` or `Ctrl+K`) searches the menu and every model you register, for example in `app/Admin/bootstrap.php`:

```php
Admin::globalSearch(App\Models\Post::class)
    ->label('Posts')
    ->columns(['title', 'author.name'])   // `relation.column` searches through a relation
    ->subtitle('author.name')
    ->url('posts/{id}/edit')
    ->permission('posts');                // hidden from users without this permission
```

You can also list resources under `global_search.resources` in `config/admin.php`.

Trash for soft deletes
------------

For models that use `SoftDeletes`, `$grid->enableTrash()` adds an *All / Trash* switch to the grid. Deleting a row still only soft-deletes it. In the trash view each row, or a batch selection, can be restored or deleted permanently.

Security
------------

- **Two-factor authentication**: each admin can turn on TOTP (Google Authenticator, Authy, 1Password, ...) from *Settings*. Recovery codes are included. Disable the feature with `ADMIN_TWO_FACTOR=false`.
- **Login throttling**: 5 failed attempts per username and IP lock the login for 60 seconds (`auth.throttle`).
- **Operation log**: passwords, tokens and 2FA codes are masked. Add more keys in `operation_log.hidden_fields`.
- **Uploads**: files get random names so they can't overwrite each other. Use `->originalName()` to keep the client file name.

## Contribute

Bug reports and pull requests are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) for how to report a bug and how the `master` and `1.x` branches differ.

<a href="https://github.com/maddog888/laravel-admin/graphs/contributors">People who already contributed</a>

Other
------------

2.x is built on:

- [Laravel](https://laravel.com/)
- [AdminLTE 4](https://adminlte.io/)
- [Bootstrap 5](https://getbootstrap.com/)
- [jQuery](https://jquery.com/)
- [Font Awesome](https://fontawesome.com/)
- [flatpickr](https://flatpickr.js.org/)
- [select2](https://select2.org/)
- [bootstrap-fileinput](https://github.com/kartik-v/bootstrap-fileinput)
- [jquery-pjax](https://github.com/defunkt/jquery-pjax)
- [Nestable](http://dbushell.github.io/Nestable/)
- [toastr](https://github.com/CodeSeven/toastr)
- [SweetAlert2](https://github.com/sweetalert2/sweetalert2)
- [OverlayScrollbars](https://github.com/KingSora/OverlayScrollbars)
- [fontawesome-iconpicker](https://github.com/farbelous/fontawesome-iconpicker)

License
------------

`laravel-admin` is licensed under [The MIT License (MIT)](LICENSE).
