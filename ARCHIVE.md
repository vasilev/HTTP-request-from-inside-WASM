ARCHIVE of "Make HTTP request from inside WebAssembly" list
===========================================================

> [!CAUTION]
> Approaches listed on this page are deprecated or/and do not longer work. 
> They are collected here for historical purposes.
 
Each item has hyperlink to up-to-date alternative in the [main list](README.md).

### Contents
<table>
<tr>
<th>Language</th>
<th>Browsers and V8-based runtimes</th>
<th>Standalone / server-side / WASI runtimes</th>
</tr>
<tr>
<td>PHP</td>
<td>

[PIB aka php-wasm](#php)

</td>
<td></td>
</tr>
</table>

### PHP
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[PIB: PHP in Browser aka php-wasm](https://github.com/seanmorris/php-wasm/)

<sub>

> [!CAUTION]
> This code do not work in php-wasm v0.0.8.


> [!TIP]
> Use [up-to-date method](README.md#php-wasm) instead.

</sub>

</td>
<td>

```php
$js=<<<JSCODE
var xhr=new XMLHttpRequest();
xhr.open('GET', 'https://httpbin.org/anything', 0);
xhr.send();

xhr.responseText;
JSCODE;

var_dump(vrzno_eval($js));
```

</td>
<td>

[Example](https://github.com/WordPress/wordpress-playground/blob/bb148069e37d8b7f3314a3e675abb316f7749e4e/src/wordpress-playground/mu-plugins/includes/requests_transport_fetch.php#L68)

</td>
<td>

[Doc](https://github.com/seanmorris/vrzno#usage)

</td>
<td>

* [Demo](https://seanmorris.github.io/php-wasm/?autorun=0&persist=0&single-expression=0&code=%253C%253Fphp%250A%2524js%253D%253C%253C%253CJSCODE%250Avar%2520xhr%253Dnew%2520XMLHttpRequest%28%29%253B%250Axhr.open%28%27GET%27%252C%2520%27https%253A%252F%252Fhttpbin.org%252Fanything%27%252C%25200%29%253B%250Axhr.send%28%29%253B%250A%250Axhr.responseText%253B%250AJSCODE%253B%250A%250Avar_dump%28vrzno_eval%28%2524js%29%29%253B%250A)
* [Playground](https://seanmorris.github.io/php-wasm/)

</td>
<td>Browser, Node.js, and maybe Deno</td>
<td>

Manual JS `XMLHttpRequest` interop using [`vrzno`](https://github.com/seanmorris/vrzno/blob/228514316299f8d1dbc8abcff51523ed37929f1f/vrzno.c#L36) PHP extension.

</td>
</tr>
</table>
