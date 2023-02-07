Make HTTP request from inside WebAssembly
=========================================

(Wannabe-awesome) list of approaches (recipes, frameworks, http client libraries, etc) to make outbound HTTP(S) requests from inside WebAssembly.

### Contents
<table>
<tr>
<th>Language</th>
<th>Browsers and V8-based runtimes</th>
<th>Standalone / server-side / WASI runtimes</th>
</tr>
<tr>
<td>C#</td>
<td>

[Blazor](#csharp)

</td>
<td>

[Spin SDK for .NET](#csharp-wasi)

</td>
</tr>
<tr>
<td>C++</td>
<td>

[xxhr](#cpp)

</td>
<td></td>
</tr>
<tr>
<td>Golang / TinyGo</td>
<td>

["net/http", "wasm-fetch"](#golang)

</td>
<td>

[Capsule, Spin SDK for Go](#golang-wasi)

</td>
</tr>
<tr>
<td>JavaScript</td>
<td>

_Possible, but why?_

</td>
<td>

[WasmEdge-QuickJs](#javascript)

</td>
</tr>
<tr>
<td>PHP</td>
<td>

[PIB aka php-wasm](#php)

</td>
<td></td>
</tr>
<tr>
<td>Perl</td>
<td>

[WebPerl](#perl)

</td>
<td></td>
</tr>
<tr>
<td>Python</td>
<td>

[RustPython, Pyodide, pyodide-http](#python)

</td>
<td></td>
</tr>
<tr>
<td>R</td>
<td>

[webR](#rlang)

</td>
<td></td>
</tr>
<tr>
<td>Ruby</td>
<td>

[ruby.wasm](#ruby)

</td>
<td></td>
</tr>
<tr>
<td>Rust</td>
<td>

[wasm-bindgen, ehttp, gloo_net, httpc, reqwasm, surf](#rust)

</td>
<td>

[reqwest, http_req, Spin SDK for Rust](#rust-wasi)

</td>
</tr>
</table>

Browser WASM runtimes and V8-based runtimes like Node.js and Deno
-----------------------------------------------------------------

<a id="csharp"></a>
### C#

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Blazor](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor)

</td>
<td>

```csharp
@using System.Net.Http.Json
@inject HttpClient HttpClient

@code {
var data = await HttpClient.GetFromJsonAsync<JsonElement>("https://httpbin.org/anything");
}
```

</td>
<td>

[Example](https://github.com/cornflourblue/blazor-webassembly-http-get-request-examples/blob/dc43c77c738076a7f56805bc664bf269a6cdedbf/Components/GetRequestDynamicResponse.razor#L16)

</td>
<td>

* [Tutorial](https://learn.microsoft.com/en-us/aspnet/core/blazor/call-web-api?view=aspnetcore-7.0)
* [Doc](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.json?view=net-7.0)

</td>
<td>

[Demo](https://cornflourblue.github.io/blazor-webassembly-http-get-request-examples/) _by JasonWatmore_
<sub>[Demo source](https://github.com/cornflourblue/blazor-webassembly-http-get-request-examples/tree/master/Components)</sub>

</td>
<td>Browser, also server-side</td>
<td>

[JS `fetch` interop](https://learn.microsoft.com/en-us/aspnet/core/blazor/call-web-api?view=aspnetcore-7.0&pivots=webassembly#httpclient-and-httprequestmessage-with-fetch-api-request-options)

</td>
</tr>
</table>

<a id="cpp"></a>
### C++

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[nxxm/xxhr](https://nxxm.github.io/xxhr/)

</td>
<td>

```cpp
#include <xxhr/xxhr.hpp>

using namespace xxhr;
 
GET( "https://httpbin.org/anything"s, 
  on_response = [](auto res) { std::cout << res.text; }
);
```

</td>
<td>

[Example](https://github.com/nxxm/xxhr/blob/v1.0.2/examples/getting_started.cpp#L14)

</td>
<td>

[Doc](https://nxxm.github.io/xxhr/html/getting-started-cpp.html)

</td>
<td></td>
<td>

Browser, [Node.js](https://www.npmjs.com/package/xmlhttprequest-ssl), and [Deno](https://deno.land/x/xhr)

</td>
<td>

[JS `XMLHttpRequest` Interop](https://github.com/nxxm/xxhr/blob/v1.0.2/xxhr/impl/session-emscripten.hpp#L273)

</td>
</tr>
</table>

### Golang

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr><td>

[Golang](https://go.dev/)

</td>
<td>

```go
import "net/http"

resp, err := http.Get("https://httpbin.org/anything")
```

</td>
<td>

* [Sample by SamDz16](https://github.com/SamDz16/goWasm-http-request/blob/master/main.go#L40)
* [Sample by salrashid123](https://github.com/salrashid123/wasm_http_go/blob/main/main.go#L56)

</td>
<td>

[fetch options](https://github.com/golang/go/wiki/WebAssembly#configuring-fetch-options-while-using-nethttp)

</td>
<td></td>
<td>

Browser and [Node.js](https://github.com/golang/go/wiki/WebAssembly#executing-webassembly-with-nodejs)

</td>
<td>

[JS `fetch` Interop](https://github.com/golang/go/blob/go1.19.4/src/net/http/roundtrip_js.go#L115)

</td>
</tr>

<tr><td>

[marwan.io/wasm-fetch](https://pkg.go.dev/marwan.io/wasm-fetch)

<sub>Save 4 MB of wasm binary size</sub>

</td>
<td>

```go
import "marwan.io/wasm-fetch"

resp, err := fetch.Fetch("https://httpbin.org/anything", 
    &fetch.Opts{})

if err == nil {
	println(string(resp.Body))
}
```

</td>
<td>

[Example](https://github.com/marwan-at-work/wasm-fetch/tree/e4e5f93254680e5f64e37a500e2f3a73c374907f#example)

</td>
<td>

[Doc](https://pkg.go.dev/marwan.io/wasm-fetch#section-documentation)

</td>
<td></td>
<td>

Browser and [Node.js](https://github.com/golang/go/wiki/WebAssembly#executing-webassembly-with-nodejs)

</td>
<td>

Direct [JS `fetch` Interop](https://github.com/marwan-at-work/wasm-fetch/blob/e4e5f93254680e5f64e37a500e2f3a73c374907f/fetch.go#L127)

</td>
</tr>
</table>

### PHP
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[PIB: PHP in Browser aka php-wasm](https://github.com/seanmorris/php-wasm/)

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

### Perl
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[WebPerl](https://webperl.zero-g.net/)

</td>
<td>

```perl
use WebPerl qw/js js_new sub_once/;

my $xhr = js_new('XMLHttpRequest');
$xhr->addEventListener('load', sub_once {
    print 'Done: '.$xhr->{responseText};
});
$xhr->open('GET', 'https://httpbin.org/anything', 0);
$xhr->send();
```

</td>
<td>

* [Example 1](https://github.com/haukex/webperl/blob/16bc09d89a8a42d8cf68b434b126bd0f916192dc/experiments/use_http.html#L40)
* [Example 2](https://github.com/haukex/webperl/blob/16bc09d89a8a42d8cf68b434b126bd0f916192dc/experiments/gui_basic/web/web.pl#L37)

</td>
<td>

[Forum post](https://www.perlmonks.org/?node_id=1225420)

</td>
<td>

* [Demo](https://webperl.zero-g.net/democode/perleditor.html#%7B%22cmdline%22%3A%22perl%20script.pl%22%2C%22script%22%3A%22use%20WebPerl%20qw%2Fjs%20js_new%20sub_once%2F%3B%5Cn%5Cnmy%20%24xhr%20%3D%20js_new('XMLHttpRequest')%3B%5Cn%24xhr-%3EaddEventListener('load'%2C%20sub_once%20%7B%5Cn%20%20%20%20print%20'Done%3A%20'.%24xhr-%3E%7BresponseText%7D%3B%5Cn%7D)%3B%5Cn%24xhr-%3Eopen('GET'%2C%20'https%3A%2F%2Fhttpbin.org%2Fanything'%2C%200)%3B%5Cn%24xhr-%3Esend()%3B%22%2C%22script_fn%22%3A%22script.pl%22%2C%22mergeStdOutErr%22%3Atrue%7D)
* [Playground](https://webperl.zero-g.net/democode/index.html)

</td>
<td>Browser, Node.js, and Deno</td>
<td>

Manual JS `XMLHttpRequest` interop using [`WebPerl.pm`](https://github.com/haukex/emperl5/blob/webperl_v0.09-beta/ext/WebPerl/lib/WebPerl.pm#L74) module.

</td>
</tr>
</table>

### Python

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr><td>

[RustPython](https://rustpython.github.io/)

</td><td>

```python
from browser import fetch

fetch('https://httpbin.org/anything').then(
    lambda resp: print((resp)))
```

</td>

<td>

[Example](https://github.com/RustPython/RustPython/blob/0.1.0/wasm/example/src/main.py#L9)

</td>
<td></td>
<td>

[Playground](https://rustpython.github.io/demo/)

<sub>[source of demo](https://github.com/RustPython/RustPython/blob/0.1.0/wasm/demo/snippets/fetch.py#L6)</sub>

</td>
<td>

Browser, [Node.js](https://gitter.im/rustpython/Lobby?at=600063a5d5f4bf2965e74e2f), and maybe Deno

</td><td>

[JS `fetch` Interop](https://github.com/RustPython/RustPython/blob/0.1.0/wasm/lib/src/browser_module.rs#L104)

</td></tr>
<tr><td>

[Pyodide](https://pyodide.org)

</td><td>

```python
from pyodide.http import pyfetch

response = await pyfetch("https://httpbin.org/anything")
```

</td>
<td>

* [3 Ways to Implement Network Requests in Pyodide _by lwebapp_](https://lwebapp.com/en/post/pyodide-fetch)
* [some code](https://github.com/pyodide/pyodide/blob/0.22.0/docs/usage/faq.md#how-can-i-load-external-files-in-pyodide)
* [StackOverflow question](https://stackoverflow.com/questions/64789154/how-can-i-do-http-post-requests-on-pyodide)

</td>
<td>

[pyodide.http Doc](https://pyodide.org/en/stable/usage/api/python-api/http.html)

</td>
<td>

* [Playground](https://pyodide.org/en/stable/console.html)
* [`fetch` Playground by lwebapp](https://lwebapp.com/en/post/pyodide-fetch)

</td>
<td>

Browser, Node.js, and [maybe Deno](https://github.com/pyodide/pyodide/pull/3421)

</td><td>

[JS `fetch` Interop](https://github.com/pyodide/pyodide/blob/0.22.0/src/py/pyodide/http.py#L235)

</td>
</tr>
<tr>
<td>

[koenvo/pyodide-http](https://github.com/koenvo/pyodide-http)

[`requests`](https://requests.readthedocs.io/en/latest/)
and [`urlopen`](https://docs.python.org/3/library/urllib.request.html#urllib.request.urlopen) in Pyodide

</td>
<td>

```python
# needs `await micropip.install(['pyodide-http', 'requests'])`

import pyodide_http     
pyodide_http.patch_all()

import requests
response = requests.get("https://httpbin.org/anything")
```

</td>
<td>

[Example](https://github.com/koenvo/pyodide-http#usage)

</td>
<td>

[Supported packages](https://github.com/koenvo/pyodide-http#supported-packages)

</td>
<td>

[Playground](https://pyodide.org/en/stable/console.html)

</td>
<td>Browser and maybe Node.js</td>
<td>

JS [`fetch`](https://github.com/koenvo/pyodide-http/blob/0.2.0/pyodide_http/_streaming.py#L102) and
[`XMLHttpRequest`](https://github.com/koenvo/pyodide-http/blob/0.2.0/pyodide_http/_core.py#L77) Interop
using Pyodide's [`js`](https://pyodide.org/en/stable/usage/api/python-api.html) scope.


</td>
</tr>
</table>

<a id="rlang"></a>
### R

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[webR](https://github.com/georgestagg/webR)

</td>
<td>

```rlang
df <- read.csv("https://httpbin.org/anything")
print(df)
// All works: read.table() variants, download.file(), scan(), url(), etc
```

</td>
<td></td>
<td>

[Doc](https://cran.r-project.org/doc/manuals/r-release/R-data.html)

</td>
<td>

[Playground](https://webr.gwstagg.co.uk/)

</td>
<td>Browser and Node</td>
<td>

Implemented [`xhr` transport](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/patches/R-4.1.3/emscripten-xhr-download.diff#L102) which uses
JS `XMLHttpRequest` interop by [calling](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/patches/R-4.1.3/emscripten-xhr-download.diff#L184) [web worker](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/src/webR/webr-worker.ts#L278) 
using Emscripten APIs.

</td>
</tr>
</table>

### Ruby

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[ruby.wasm](https://ruby.github.io/ruby.wasm/)

</td>
<td>

```ruby
require 'js'

resp = JS.global.fetch('https://httpbin.org/anything').await
puts resp.text.await
```

</td>
<td>

* [Example 1](https://github.com/keyasuda/bormashino/blob/29f15349bda4415f6febeab66a1f6417cd42a0d0/test-app/src/app.rb#L42) from _bormashino_
* [Example 2](https://github.com/kou/ruby-wasm-duckdb/blob/54e8d408d38fa269020b132fb3b270881909550d/duckdb.rb#L34) from _ruby-wasm-duckdb_
* [Example 3](https://github.com/kateinoigakukun/irb.wasm/blob/1d6696ea1c6fa5206b7e6a0eab3468c409545c8c/src/terminals/xterm.ts#L148) from _irb.wasm_
* [Example 4](https://github.com/kateinoigakukun/irb.wasm/blob/1d6696ea1c6fa5206b7e6a0eab3468c409545c8c/src/ruby/rubygems_compat.rb#L24) from _irb.wasm_

</td>
<td>

[Doc](https://ruby.github.io/ruby.wasm/JS.html)

</td>
<td>

* [TryRuby Demo](https://try.ruby-lang.org/playground/#code=+require+'js'%0A+promise+%3D+JS.global.call%28%3Afetch%2C+'https%3A%2F%2Fhttpbin.org%2Fanything'%29%0A+promise.call%28%3Athen%2C%0A+++-%3E%28r%29+%7B+p2%3D+r.call%28%3Atext%29%3B+p2.call%28%3Athen%2C+%0A+++++-%3E%28t%29+%7B+puts+%22text%3D%23%7Bt%7D%22+%7D+%29%7D+%0A+%29&engine=cruby-3.3.0dev)
* [irb-wasm Playground](https://irb-wasm.vercel.app/)

</td>
<td>

[Browser](https://github.com/ruby/ruby.wasm/blob/ruby-head-wasm-wasi-0.5.0/packages/npm-packages/ruby-head-wasm-wasi/README.md#quick-start-for-browser), [Node.js](https://github.com/ruby/ruby.wasm/blob/ruby-head-wasm-wasi-0.5.0/packages/npm-packages/ruby-head-wasm-wasi/README.md#quick-start-for-nodejs), and maybe Deno

</td>
<td>

Direct [JS `fetch` Interop](https://github.com/ruby/ruby.wasm/blob/293e7c20ff2a1db51cd1de3c88feb627b37dd95e/ext/js/lib/js.rb#L141)

</td>
</tr>
</table>

### Rust

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr><td>
<a id="wasm-bindgen"></a>

[wasm-bindgen](https://rustwasm.github.io/docs/wasm-bindgen/)

</td>
<td>

```rust
let window = web_sys::window().unwrap();
let resp_val = JsFuture::from(
  window.fetch_with_str("https://httpbin.org/anything")).await?;
```

</td>
<td>

[Example](https://github.com/rustwasm/wasm-bindgen/blob/0.2.83/examples/fetch/src/lib.rs#L21)

</td>
<td>

[Fetch API docs](https://rustwasm.github.io/wasm-bindgen/api/web_sys/struct.Window.html#method.fetch_with_request)

</td>
<td>

[Demo](https://rustwasm.github.io/wasm-bindgen/exbuild/fetch/)

<sub>Prints to browser
console, [source](https://github.com/rustwasm/wasm-bindgen/blob/0.2.83/examples/fetch/index.js#L6)</sub>

</td>
<td>

Browser, [Node.js](https://rustwasm.github.io/wasm-bindgen/reference/deployment.html?highlight=Nodejs#nodejs),
and [Deno](https://rustwasm.github.io/wasm-bindgen/reference/deployment.html?highlight=Deno#deno)

</td>
<td>

[JS `fetch` Interop](https://github.com/rustwasm/wasm-bindgen/blob/0.2.83/crates/web-sys/src/features/gen_Window.rs#L2575)

</td>
</tr>
<tr>
<td>

[ehttp](https://crates.io/crates/ehttp)

</td>
<td>

```rust
let request = ehttp::Request::get("https://httpbin.org/anything");
ehttp::fetch(request, move |result: ehttp::Result<ehttp::Response>| {
    println!("Text: {:?}", result.unwrap().text());
});
```

</td>
<td>

[Example](https://github.com/emilk/ehttp/blob/0.2.0/example_eframe/src/lib.rs#L55)

</td>
<td>

[Doc](https://docs.rs/ehttp/0.2.0/ehttp/)

</td>
<td>

[Demo](https://emilk.github.io/ehttp/index.html)

</td>
<td>Browser, Node.js, and Deno.

Also  [native](https://github.com/emilk/ehttp/blob/0.2.0/ehttp/src/native.rs#L17)

</td>
<td>

[JS `fetch` Interop](https://github.com/emilk/ehttp/blob/0.2.0/ehttp/src/web.rs#L42) using [wasm-bindgen](#wasm-bindgen)

</td>
</tr>
<tr>
<td>

[httpc](https://crates.io/crates/httpc)

</td>
<td>

```rust
let uri = Uri::from_static("https://httpbin.org/anything");
let req = Request::get(uri).body(None).unwrap();
let client = web_sys::window();
let resp = client.issue(req).await.unwrap();
println!("{}", resp.body());
```

</td>
<td>

[Test](https://github.com/d-e-s-o/httpc/blob/766936027513ea02fc3eb0aca8af81a8d9452b67/tests/request.rs#L120)

</td>
<td>

[Doc](https://docs.rs/crate/httpc/)

</td>
<td></td>
<td>Browser, Node.js, and Deno.

Also  [native](https://github.com/d-e-s-o/httpc/blob/766936027513ea02fc3eb0aca8af81a8d9452b67/src/native.rs#L38)

</td>
<td>

[JS `fetch` Interop](https://github.com/d-e-s-o/httpc/blob/766936027513ea02fc3eb0aca8af81a8d9452b67/src/wasm.rs#L107) using [wasm-bindgen](#wasm-bindgen)

</td>
</tr>
<tr>
<td>
<a id="gloo_net"></a>

[Gloo](https://gloo-rs.web.app/)'s [gloo-net](https://crates.io/crates/gloo-net)

</td>
<td>

```rust
use gloo_net::http::Request;

let resp = Request::get("https://httpbin.org/anything").send()
    .await.unwrap();
```

</td>
<td>

* [yew's demo](https://github.com/yewstack/yew/blob/yew-v0.20.0/examples/async_clock/src/services.rs#L31)
* [Test](https://github.com/rustwasm/gloo/blob/0.8.0/crates/net/tests/http.rs#L11)
* [yew's tutorial](https://yew.rs/docs/tutorial#fetching-data-using-external-rest-api)

</td>
<td>

[Doc](https://docs.rs/gloo-net/latest/gloo_net/http/index.html)

</td>
<td>

[Demo](https://examples.yew.rs/async_clock/)

<sub>[source](https://github.com/yewstack/yew/blob/yew-v0.20.0/examples/async_clock/src/services.rs#L31)</sub>

</td>
<td>Browser, Node.js, and Deno</td>
<td>

[JS `fetch` Interop](https://github.com/rustwasm/gloo/blob/6617d0ee0c552e3ba31e112591e33b98274739f6/crates/net/src/http/mod.rs#L261) using [wasm-bindgen](#wasm-bindgen)

</td>
</tr>
<tr>
<td>

[reqwasm](https://crates.io/crates/reqwasm)

</td>
<td>

```rust
use reqwasm::http::Request;

let resp = Request::get("https://httpbin.org/anything").send()
    .await.unwrap();
```

</td>
<td>

[Example](https://github.com/security-union/yew-weather/blob/5ddd9490bc9047fc27caccdb5fc776966fceaebc/src/main.rs#L68)

</td>
<td>

[Doc](https://docs.rs/reqwasm/0.5.0/reqwasm/http/index.html)

</td>
<td></td>
<td>Browser, Node.js, and Deno</td>
<td>

[Wrapper](https://github.com/hamza1311/reqwasm/blob/0.5.0/src/lib.rs#L6) for [gloo_net](#gloo_net)

</td>
</tr>
<tr>
<td>

[surf](https://crates.io/crates/surf)

</td>
<td>

```rust
let mut resp = surf::get("https://httpbin.org/anything").await?;
println!("{}", resp.body_string().await?);
```

</td>
<td>

[Example](https://github.com/http-rs/surf/blob/v2.3.2/examples/hello_world.rs#L6)

</td>
<td>

[Doc](https://docs.rs/surf)

</td>
<td></td>
<td>Browser, Node.js, and Deno

Also [native](https://github.com/http-rs/surf/blob/v2.3.2/src/lib.rs#L83)
</td>
<td>

[JS `fetch` Interop](https://github.com/http-rs/http-client/blob/v6.5.3/src/wasm.rs#L226) using [wasm-bindgen](#wasm-bindgen)

</td>
</tr>


</table>


Standalone and server-side runtimes (mostly WASI-Socket-enabled), incl containers, FaaS, Edge Computing, etc
------------------------------------------------------------------------------------------------------------

<a id="csharp-wasi"></a>
### C#

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Spin SDK for .NET](https://github.com/fermyon/spin-dotnet-sdk)

</td>
<td>

```csharp
using Fermyon.Spin.Sdk;
using System.Net;

var req = new HttpRequest { Url = "https://httpbin.org/anything" };
var resp = HttpOutbound.Send(req);
```

</td>
<td>

[Example](https://github.com/fermyon/spin-dotnet-sdk/blob/0b320bad3c661bb2d3af5950f1b76af8f7fb655d/samples/hello-world/Handler.cs#L43)

</td>
<td>

[Doc](https://github.com/fermyon/spin-dotnet-sdk#making-outbound-http-requests)

</td>
<td></td>
<td>

[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[C level](https://github.com/fermyon/spin-dotnet-sdk/blob/0b320bad3c661bb2d3af5950f1b76af8f7fb655d/src/native/wasi-outbound-http.c#L95) 
[binding](https://github.com/fermyon/spin-dotnet-sdk/blob/0b320bad3c661bb2d3af5950f1b76af8f7fb655d/src/HttpInterop.cs#L269) to  
Wasmtime's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
</table>

<a id="golang-wasi"></a>
### Golang (Tinygo)

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr><td>

[Capsule](https://bots-garden.github.io/capsule/)

</td>
<td>

```go
import (
    hf "github.com/bots-garden/capsule/capsulemodule/hostfunctions"
)
res, err := hf.Http("https://httpbin.org/anything", "GET", nil, "")
```

</td>
<td>

[Example](https://github.com/bots-garden/capsule/blob/v0.3.0/wasm_modules/capsule-http-get/hello.go#L19)

</td>
<td>

[HTTP request docs](https://bots-garden.github.io/capsule/host-functions-http/)

</td>
<td>

</td>
<td>

[wazero](https://wazero.io/)

</td>
<td>

[wazero's Host Functions feature](https://github.com/bots-garden/capsule/blob/v0.3.0/capsule-launcher/hostfunctions/http.go#L47)

</td>
</tr>
<tr>
<td>

[(Tiny)Go SDK for Spin](https://developer.fermyon.com/spin/go-components)

</td>
<td>

```go
import (
    spinhttp "github.com/fermyon/spin/sdk/go/http"
)

resp, err := spinhttp.Get("https://httpbin.org/anything")
```

</td>
<td>

* [Example 1](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/examples/http-tinygo-outbound-http/main.go#L14)
* [Example 2](https://github.com/fermyon/spin-kitchensink/blob/855f9477f9090b9cb54e2454b158ef9515f54644/go-outbound-http/main.go#L16)

</td>
<td>

[Doc](https://developer.fermyon.com/spin/go-components#sending-outbound-http-requests)

</td>
<td></td>
<td>

[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[C level](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/sdk/go/http/outbound_internals.go#L66) 
[binding](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/sdk/go/http/wasi-outbound-http.c#L95) to  
Wasmtime's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
</table>

### JavaScript

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr><td>

[wasmedge-quickjs](https://github.com/second-state/wasmedge-quickjs)

</td>
<td>

```js
// no SSL support yet
let res = await fetch('http://httpbin.org/anything')
```

</td>
<td>

[Example](https://github.com/second-state/wasmedge-quickjs/blob/v0.4.0-alpha/example_js/wasi_http_fetch.js#L5)

</td>
<td>

[Doc](https://wasmedge.org/book/en/write_wasm/js/networking.html#fetch-client)

</td>
<td>

</td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[Raw socket write](https://github.com/second-state/wasmedge-quickjs/blob/v0.4.0-alpha/modules/http.js#L205)
to [`WasiTcpConn`](https://github.com/second-state/wasmedge-quickjs/blob/v0.4.0-alpha/src/internal_module/wasi_net_module.rs#L187)
which is [`C` binding](https://github.com/second-state/wasmedge-quickjs/blob/v0.4.0-alpha/src/event_loop/wasi_sock.rs#L606)
to
Wasmedge's implementation of WASI Socket

</td>
</tr>
</table>

<a id="rust-wasi"></a>
### Rust

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[http_req_wasi](https://crates.io/crates/http_req_wasi)

</td>
<td>

```rust
use http_req::request;

let mut writer = Vec::new();
let res = request::get("https://httpbin.org/anything", 
    &mut writer).unwrap();
```

</td>
<td>

[Example](https://github.com/second-state/http_req/blob/cd9f9e086145741e2ee287364c2f6097dd92f7e1/examples/get_https.rs#L5)

</td>
<td>

[Doc](https://wasmedge.org/book/en/write_wasm/rust/networking-https.html)

</td>
<td></td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

C level [wrapper](https://github.com/second-state/http_req/blob/cd9f9e086145741e2ee287364c2f6097dd92f7e1/src/sslwrapper.rs#L10) over [`wasmedge_httpsreq` plugin](https://github.com/WasmEdge/WasmEdge/tree/master/plugins/wasmedge_httpsreq) (`libwasmedgePluginHttpsReq.so` as usual). And
[wasmedge_wasi_socket](https://github.com/second-state/http_req/blob/cd9f9e086145741e2ee287364c2f6097dd92f7e1/src/request.rs#L20) for non-SSL.

</td>
</tr>
<tr>
<td>

[Spin SDK for Rust](https://github.com/fermyon/spin/tree/v0.8.0/sdk/rust)

</td>
<td>

```rust
let mut res = spin_sdk::http::send(
  http::Request::builder()
  .method("GET")
  .uri("https://httpbin.org/anything")
  .body(None)?,
)?;
```

</td>
<td>

[Example](https://github.com/fermyon/spin/blob/v0.8.0/examples/http-rust-outbound-http/src/lib.rs#L10)

</td>
<td>

[Doc](https://github.com/fermyon/spin/tree/v0.8.0/sdk/rust#making-outbound-http-requests)

</td>
<td></td>
<td>

[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[Calling](https://github.com/fermyon/spin/blob/v0.8.0/sdk/rust/src/outbound_http.rs#L43) [imported](https://github.com/fermyon/spin/blob/v0.8.0/crates/trigger/src/lib.rs#L100)
Wasmtime's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).
</td>
</tr>
<tr><td>

Any code based on WasmEdge's forks of [tokio-rs](https://github.com/WasmEdge/tokio)
or [mio](https://github.com/WasmEdge/mio)
is [expected to work in Wasmedge runtime](https://github.com/tokio-rs/tokio/issues/5331)

</td>
<td>

```rust
// using fork https://github.com/WasmEdge/reqwest , no SSL yet
let res = reqwest::get("http://httpbin.org/anything").await?;
```

</td>
<td>

[Example](https://github.com/WasmEdge/wasmedge_reqwest_demo/blob/main/src/main.rs#L8)

</td>
<td>

[Doc](https://wasmedge.org/book/en/write_wasm/rust/networking.html)

</td>
<td></td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[WasmEdge's implementation of WASI Socket](https://github.com/second-state/wasmedge_wasi_socket)

</td>
</tr>
</table>


