multi-language support
- create dictionary  

supported by method:  
```php
App:setLocale('en');
App:setLocale('id');
```

supported by folder: 
```
lang
> en > id.php 
> id > id.php
```

`id.php`: returns key value pairs of a text
```php
?php

return [
	'title' => 'Pendaftaran Penumpang',
	'name' => 'Nama',
	'division' => 'Divisi',
]; 
```

id.php values can be called using:
```php
{{__('id.title')}}
@lang('id.division')
```