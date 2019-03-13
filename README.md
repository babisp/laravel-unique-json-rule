# Laravel Unique Json


#### Check if a record value in a JSON column is unique in the database.

Implementations of Json field unqiue validation rule and inspired by codezero-be/laravel-unique-translation

## Requirements

-   PHP >= 7.0
-   MySQL >= 5.7
-   [Laravel](https://laravel.com/) >= 5.5


## Installation

Require the package via Composer:

```
composer require topview-digital/laravel-unique-json-rule
```
Laravel will automatically register the [ServiceProvider](https://github.com/robinhoo1973/laravel-unique-json-rule/blob/master/src/UniqueJsonServiceProvider.php).

## Usage

For the following examples

### Validate an Array of Contacts

Your form can also submit an array of contact.

```html
<input name="contact[name]">
<input name="contact[email]">
<input name="contact[phone]">
```

We need to validate the entire array in this case. Mind the `contact.*` key.

```php
$attributes = request()->validate([
    'contact.name' => 'unique_json:clients,contact->name',
    'contact.email' => UniqueJsonRule::for('clients','contact->email'),
]);
```

### Ignore a Record with ID

If you're updating a record, you may want to ignore the post itself from the unique check.


```php
$attributes = request()->validate([
    'contact.name' => 'unique_json:clients,contact->name,{$client->id}',
    'contact.email' => UniqueJsonRule::for('clients','contact->email')->ignore($client->id),
]);
```

### Ignore Records with a Specific Column and Value

If your ID column has a different name, or you just want to use another column:

```php
$attributes = request()->validate([
    'contact.name' => 'unique_json:clients,contact->name,{$client->id},id',
    'contact.email' => UniqueJsonRule::for('clients','contact->email')->ignore($client->id,'id'),
]);
```


## Error Messages


You can pass your own error message with any of the following keys. The first one found will be used.

```php
$attributes = request()->validate([
    'contact.name' => 'unique_json:clients,contact->name,{$client->id}',
], [
    'contact.name.unique_json' => 'Your custom :attribute error.',
]);
```
## Changelog

See a list of important changes in the [changelog](https://github.com/robinhoo1973/laravel-unique-json-rule/blob/master/CHANGELOG.md).

## License

The MIT License (MIT). Please see [License File](https://github.com/robinhoo1973/laravel-unique-json-rule/blob/master/LICENSE.md) for more information.