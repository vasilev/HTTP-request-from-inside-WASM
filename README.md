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
<td>AssemblyScript</td>
<td>

[as-fetch](#assemblyscript)

</td>
<td>

[wasi-experimental-http, wasi-http-ts](#assemblyscript-wasi)

</td>
</tr>
<tr>
<td>C#</td>
<td>

[Blazor, Uno Platform](#csharp)

</td>
<td>

[Spin SDK for .NET, wasi-experimental-http](#csharp-wasi)

</td>
</tr>
<tr>
<td>C / C++</td>
<td>

[xxhr](#cpp)

</td>
<td>

[httpclient_wasmedge_socket, wasi-experimental-http](#cpp-wasi)

</td>
</tr>
<tr>
<td>Golang / TinyGo</td>
<td>

["net/http", "wasm-fetch"](#golang)

</td>
<td>

[Capsule, Spin SDK for Go, wasi-experimental-http](#golang-wasi)

</td>
</tr>
<tr>
<td>Java</td>
<td>

[Bytecoder](#java)

</td>
<td>

[spin-teavm-example](#java-wasi)

</td>
</tr>
<tr>
<td>JavaScript</td>
<td>

_Possible, but why?_

</td>
<td>

[WasmEdge-QuickJs, Spin SDK for JS / TS](#javascript-wasi)

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

[RustPython, Pyodide, pyodide-http, PyScript, Panel, RPython](#python)

</td>
<td>

[Spin SDK for Python](#python-wasi)

</td>
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

[wasm-bindgen, Cloudflare Workers SDK, ehttp, gloo_net, httpc, http-client, reqwasm, reqwest, seed, surf](#rust)

</td>
<td>

[reqwest, http_req, Spin SDK for Rust, wasi-experimental-http](#rust-wasi)

</td>
</tr>
<tr>
<td>Swift</td>
<td>

[SwiftWasm](#swift)

</td>
<td></td>
</tr>
</table>

Browser WASM runtimes and V8-based runtimes like Node.js and Deno
-----------------------------------------------------------------

### AssemblyScript
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[as-fetch](https://github.com/JairusSW/as-fetch)

</td>
<td>

```typescript
import { fetch } from "as-fetch/assembly";

export { responseHandler } from "as-fetch/assembly";

fetch("https://httpbin.org/anything", {
  method: "GET",
  mode: "no-cors",
  headers: [],
  body: null,
}).then((resp) => {
  const text = resp.text();
});
```

</td>
<td>

[Example](https://github.com/JairusSW/as-fetch/blob/503cb7804d3aeaa9a5dd86b0f6ef3907ce6def1b/assembly/test.ts#L10)

</td>
<td>

[Readme](https://github.com/JairusSW/as-fetch#usage)

</td>
<td></td>
<td>Browser, Node.js, and Deno</td>
<td>

[JS `fetch` interop](https://github.com/JairusSW/as-fetch/blob/503cb7804d3aeaa9a5dd86b0f6ef3907ce6def1b/assembly/src/fetch.ts#L25)
by [importing](https://github.com/JairusSW/as-fetch/blob/503cb7804d3aeaa9a5dd86b0f6ef3907ce6def1b/assembly/src/fetch.ts#L3) the function from runtime

</td>
</tr>
</table>

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
var data = await HttpClient.GetFromJsonAsync<JsonElement>(
  "https://httpbin.org/anything");
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
<td>

Browser, also _native_ server-side

</td>
<td>

[JS `fetch` interop](https://github.com/dotnet/runtime/blob/699acfac91ed44790e528cceae16377ba10a899c/src/libraries/System.Net.Http/src/System/Net/Http/BrowserHttpHandler/BrowserHttpHandler.cs#L224)
 by [calling](https://github.com/dotnet/runtime/blob/v7.0.2/src/libraries/System.Net.Http/src/System/Net/Http/BrowserHttpHandler/BrowserHttpInterop.cs#L51)
 to TS [wrapper](https://github.com/dotnet/runtime/blob/9e8d0a81a35f05eaa2c4d0ab258ed9a1f4e2ec76/src/mono/wasm/runtime/http.ts#L60)

</td>
</tr>
<tr>
<td>

[Uno Platform](https://platform.uno/)

</td>
<td>

```csharp
// Uno Platform's own way
// Deprecated since .NET 6,
// use 'System.Net.Http.HttpClient' and 'HttpHandler' instead
// See https://github.com/unoplatform/uno/issues/9665
using System.Net.Http;

using (var handler = new Uno.UI.Wasm.WasmHttpHandler())
using (var client = new HttpClient(handler))
{
var request = new HttpRequestMessage(HttpMethod.Get,
  new Uri("https://httpbin.org/anything"));
var response = await client.SendAsync(request);
var content = await response.Content.ReadAsStringAsync();
}
```

</td>
<td>

[Test](https://github.com/unoplatform/uno/blob/4.7.37/src/SamplesApp/SamplesApp.Shared/Samples/UnitTests/HttpUnitTests.xaml.cs#L33)

</td>
<td>

[Tutorial](https://platform.uno/docs/articles/howto-consume-webservices.html)

</td>
<td>

[Playground](https://playground.platform.uno/)

</td>
<td>Browser</td>
<td>

[JS Interop](https://github.com/unoplatform/uno/blob/4.7.37/src/Uno.UI.Runtime.WebAssembly/WasmHttpHandler.cs#L62) invokes the TS
 [wrapper](https://github.com/unoplatform/uno/blob/4.7.37/src/Uno.UI/ts/HttpClient.ts#L27) for `fetch`

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

<a id="java"></a>
### Java / JVM

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[mirkosertic/Bytecoder](https://github.com/mirkosertic/Bytecoder)

<sub>transpile JVM bytecode to Wasm</sub>

</td>
<td>

```java
import de.mirkosertic.bytecoder.api.web.*;

final Window win = Window.window();
final Console con = Console.console();

win.fetch("https://httpbin.org/anything").then(
 new Promise.Handler<Response>() {
  @Override
  public void handleObject(final Response resp) {
    resp.text().then(new StringPromise.Handler() {
      @Override
      public void handleString(final String text) {
        con.log(text);
      }
    });
  }
});
```

</td>
<td>

[Test](https://github.com/mirkosertic/Bytecoder/blob/2023-04-24/core/src/test/java/de/mirkosertic/bytecoder/core/OpaqueReferenceTest.java#L105)

</td>
<td>

[Some doc](https://github.com/mirkosertic/Bytecoder/blob/2023-04-24/manual/content/chapter-1/page-1-f.md?plain=1#L40)

</td>
<td></td>
<td>

Browser, Node.js, and Deno

</td>
<td>

Direct [`fetch`](https://github.com/mirkosertic/Bytecoder/blob/2023-04-24/classlib/bytecoder.web/src/main/java/de/mirkosertic/bytecoder/api/web/WindowOrWorkerGlobalScope.java#L22)  
interop using [imported](https://github.com/mirkosertic/Bytecoder/blob/2023-04-24/classlib/bytecoder.web/src/main/java/de/mirkosertic/bytecoder/api/web/Window.java#L23) 
JS [`window`](https://github.com/mirkosertic/Bytecoder/blob/2023-04-24/core/src/main/resources/wasmruntime.js#L637) object.

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
<a id="pyodide"></a>

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

* [Example](https://github.com/koenvo/pyodide-http#usage)
* [Patching example](https://github.com/holoviz/panel/blob/v1.0.0a5/panel/io/pyodide.py#L49-L50) from _panel_

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
<tr>
<td>

[PyScript](https://pyscript.net)

</td>
<td>

```python
from pyodide.http import pyfetch, FetchResponse
import asyncio

async def req() -> FetchResponse:
  response = await pyfetch("https://httpbin.org/anything")
  print(await response.string())

asyncio.ensure_future(req())
```

</td>
<td>

[Example](https://github.com/pyscript/pyscript/blob/2023.03.1/docs/guides/http-requests.md?plain=1#L38)

</td>
<td>

[Doc](https://docs.pyscript.net/2023.03.1/guides/http-requests.html)

</td>
<td>

* [Playground 1](https://pyscript.net/examples/repl.html)
* [Playground 2](https://pyscript.net/examples/repl2.html)

</td>
<td>Browser</td>
<td>

[Uses](https://github.com/pyscript/pyscript/blob/2023.03.1/pyscriptjs/src/pyconfig.ts#L57) [pyodide](#pyodide)'s facilities 

</td>
</tr>
<tr>
<td>

[Panel](https://panel.holoviz.org)

</td>
<td>

```python
response = requests.get("https://httpbin.org/anything")
```

</td>
<td>

* [Example](https://github.com/awesome-panel/panel-highcharts/blob/f5a7e13bee6f6bc1c6b8897368a28b50ab3ca30a/examples/reference/HighStock.ipynb?short_path=2854328#L104)
* [Old example](https://github.com/holoviz-demos/webcam_classifier/blob/efe8d1a906b2a75e55c49410e73643b3c623b101/app.ipynb?short_path=2854328#L176)

</td>
<td>

[Doc](https://panel.holoviz.org/user_guide/Running_in_Webassembly.html#handling-http-requests)

</td>
<td></td>
<td>Browser</td>
<td>

[Employs](https://github.com/holoviz/panel/blob/v1.0.0a5/panel/io/pyodide.py#L50) [koenvo/pyodide-http](#pyodide-http). Also direct [`XMLHttpRequest` interop](https://github.com/holoviz/panel/blob/v1.0.0a5/panel/io/pyodide.py#L287) for image data.

</td>
</tr>
</table>

#### Python-like languages
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[soIu/rpython](https://github.com/soIu/rpython)

<sub>It's compiler</sub>

</td>
<td>

```python
from javascript import Object, asynchronous, JSON

@asynchronous
def send_request(url):
  fetch = Object('fetch')
  res = fetch.call(url).wait()
  text = res['text'].call().wait()
  print(text)
  return text
  
def target(*args): return main, None

def main(argv):
  send_request('https://httpbin.org/anything')
  return 0

if __name__ == '__main__':
  import sys
  main(sys.argv)

```

</td>
<td>

[Example](https://github.com/soIu/rpython/blob/d6ae1b2d4be426fa7894c7bf3043976d8ac4948d/README.md?plain=1#L74)

</td>
<td>

[Some doc](https://github.com/soIu/rpython#asynchronous-execution)

</td>
<td></td>
<td>Browser, Node.js, and Deno</td>
<td>

Direct `fetch` interop using [javascript](https://github.com/soIu/rpython/blob/d6ae1b2d4be426fa7894c7bf3043976d8ac4948d/javascript/emscripten.py#L141) module, by employing Emscripten APIs.

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

```r
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

* [TryRuby Demo](https://try.ruby-lang.org/playground/#code=+require+'js'%0A+promise+%3D+JS.global.call%28%3Afetch%2C+'https%3A%2F%2Fhttpbin.org%2Fanything'%29%0A+promise.call%28%3Athen%2C%0A+++-%3E%28r%29+%7B+p2%3D+r.call%28%3Atext%29%3B+p2.call%28%3Athen%2C+%0A+++++-%3E%28t%29+%7B+puts+%22text%3D%23%7Bt%7D%22+%7D+%29%7D+%0A+%29&engine=cruby-3.2.0)
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

[Rust SDK for writing Cloudflare Workers aka workers-rs](https://crates.io/crates/worker)

</td>
<td>

```rust
let mut resp = Fetch::Url(
  "https://httpbin.org/anything"
    .parse().unwrap(),
)
.send().await?;
let txt = resp.text().await?;
```

</td>
<td>

* [Example 1](https://github.com/cloudflare/workers-rs/blob/v0.0.13/worker-sandbox/src/lib.rs#L543)
* [Example 2](https://github.com/cloudflare/workers-rs/blob/v0.0.13/worker-sandbox/src/lib.rs#L331)

</td>
<td>

[Doc](https://docs.rs/worker/latest/worker/enum.Fetch.html)

</td>
<td></td>
<td>

[workerd, Cloudflare's JavaScript/ Wasm Runtime](https://github.com/cloudflare/workerd)

</td>
<td>

[JS `fetch` interop](https://github.com/cloudflare/workers-rs/blob/d21e52bd5b9d2cc6386c31aa7201bd74e772e4d0/worker/src/global.rs#L40) using [wasm-bindgen](#wasm-bindgen)

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
<a id="http-rs-http-client"></a>

[http-client](https://crates.io/crates/http-client)

</td>
<td>

```rust
use http_client::HttpClient;
use http_types::{Method, Request};
use http_client::wasm::WasmClient as Client;

let client = Client::new();
let req = Request::new(Method::Get, "https://httpbin.org/anything");
client.send(req).await.unwrap();
dbg!(client);
```

</td>
<td>

[Example](https://github.com/http-rs/http-client/blob/v6.5.3/examples/print_client_debug.rs#L19)

</td>
<td>

[Doc](https://docs.rs/http-client/6.5.3/http_client/index.html)

</td>
<td></td>
<td>

Browser, Node.js, and Deno

Also [native](https://github.com/http-rs/http-client/blob/v6.5.3/src/native.rs) (and others).

</td>
<td>

[JS `fetch` Interop](https://github.com/http-rs/http-client/blob/v6.5.3/src/wasm.rs#L226) using [wasm-bindgen](#wasm-bindgen)

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

[reqwest](https://crates.io/crates/reqwest)

</td>
<td>

```rust
let txt = reqwest::get("https://httpbin.org/anything")
    .await?.text().await?;

println!("Text: {:?}", txt);
```

</td>
<td>

* [Example](https://github.com/seanmonstar/reqwest/blob/v0.11.14/examples/wasm_github_fetch/src/lib.rs#L38)
* [Example](https://github.com/seanmonstar/reqwest/blob/v0.11.14/examples/simple.rs#L24)

</td>
<td>

[Doc](https://docs.rs/reqwest/)

</td>
<td></td>
<td>
Browser, Node.js, and Deno

Also [native](https://github.com/seanmonstar/reqwest/blob/v0.11.14/src/async_impl/client.rs#L1570)

</td>
<td>

[JS `fetch` Interop](https://github.com/seanmonstar/reqwest/blob/v0.11.14/src/wasm/client.rs#L27) using [wasm-bindgen](#wasm-bindgen)

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

[Seed](https://seed-rs.org)

</td>
<td>

```rust
use seed::{prelude::*, *};

let response = fetch("https://httpbin.org/anything").await?;
let body = response.text().await?;
```

</td>
<td>

[Example](https://github.com/seed-rs/seed/blob/0.9.2/examples/fetch/src/simple.rs#L33)

</td>
<td>

* [Doc](https://seed-rs.org/0.8.0/time_tracker_fetch)
* [Doc](https://docs.rs/seed/0.9.2/seed/browser/fetch/)

</td>
<td></td>
<td>Browser, Node.js, and Deno</td>
<td>

[JS `fetch` interop](https://github.com/seed-rs/seed/blob/0.9.2/src/browser/fetch.rs#L81) using [wasm-bindgen](#wasm-bindgen)

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

[Doc](https://docs.rs/surf/2.3.2/surf/index.html)

</td>
<td></td>
<td>Browser, Node.js, and Deno

Also [native](https://github.com/http-rs/surf/blob/v2.3.2/src/lib.rs#L83)

</td>
<td>

[Uses](https://github.com/http-rs/surf/blob/v2.3.2/src/client.rs#L15) [http-rs/http-client](#http-rs-http-client) as WASM backend

</td>
</tr>


</table>

### Swift

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[SwiftWasm](https://swiftwasm.org/)

</td>
<td>

```swift
import JavaScriptEventLoop
import JavaScriptKit

JavaScriptEventLoop.installGlobalExecutor()

let fetch = JSObject.global.fetch.function!
let resp = try! await JSPromise(
  fetch("https://httpbin.org/anything").object!)!.value
let text = try! await JSPromise(resp.text().object!)!.value
print(text)
```

</td>
<td>

* [Example 1](https://github.com/swiftwasm/JavaScriptKit/blob/0.18.0/Example/JavaScriptKitExample/Sources/JavaScriptKitExample/main.swift#L36)
* [Example 2](https://github.com/swiftwasm/swift-web-github-example/blob/d4fd6d3b83835396a6208ad412b91899c8a80973/Sources/GitHubExampleWeb/WebBindings/WebFetch.swift#L6)
* [Example 3](https://github.com/TokamakUI/Tokamak/blob/0.11.1/Sources/TokamakDemo/Modifiers/TaskDemo.swift#L54) from _Tokamak_

</td>
<td>

* [Doc](https://book.swiftwasm.org/getting-started/concurrency.html?highlight=fetch#javascript-event-loop-based-task-executor)
* [JS interop doc](https://book.swiftwasm.org/getting-started/javascript-interop.html)

</td>
<td>

* [Demo](https://swiftwasm.org/swift-web-github-example/)
* [Playground](https://pad.swiftwasm.org/)

</td>
<td>

Browser, [Node.js](https://book.swiftwasm.org/getting-started/javascript-interop.html?highlight=node.js#javascript-interoperation), and Deno

</td>
<td>

Direct `fetch` interop using [JavaScriptKit](https://github.com/swiftwasm/JavaScriptKit) framework

</td>
</tr>
</table>

Standalone and server-side runtimes (mostly WASI-Socket-enabled), incl containers, FaaS, Edge Computing, etc
------------------------------------------------------------------------------------------------------------

<a id="assemblyscript-wasi"></a>
### AssemblyScript

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```typescript
import { 
  Method, RequestBuilder, Response 
} from "@deislabs/wasi-experimental-http";
import { Console } from "as-wasi/assembly";

let resp = new RequestBuilder("https://httpbin.org/anything")
    .header("User-Agent", "wasm32-wasi-http")
    .method(Method.GET)
    .send();

let text = String.UTF8.decode(resp.bodyReadAll().buffer);
Console.log(text);
```

</td>
<td>

* [Example 1](https://github.com/dev-wasm/dev-wasm-ts/blob/a7eb8737aa12b87f55c60acd6d3dd8be0c9d8508/http/main.ts#L15)
* [Example 2](https://github.com/fermyon/spin-kitchensink/blob/c0d0f2b0487df0cb9f151b7dd8f7cd13f9ab1087/assemblyscript-outbound-http/index.ts#L11) _from [old](https://github.com/fermyon/spin/pull/699) Spin_

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-ts/blob/a7eb8737aa12b87f55c60acd6d3dd8be0c9d8508/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=575631506) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)
or [**old** Spin](https://github.com/fermyon/spin/pull/699)

</td>
<td>

[Importing](https://github.com/dev-wasm/dev-wasm-ts/blob/a7eb8737aa12b87f55c60acd6d3dd8be0c9d8508/http/package.json#L18)
[npm package](https://www.npmjs.com/package/@deislabs/wasi-experimental-http) which [calls](https://github.com/deislabs/wasi-experimental-http/blob/v0.5.0/crates/as/index.ts#L202)
[imported](https://github.com/deislabs/wasi-experimental-http/blob/v0.5.0/crates/as/raw.ts#L113)
[host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
<tr>
<td>

[brendandburns/wasi-http-ts](https://github.com/brendandburns/wasi-http-ts)

</td>
<td>

```typescript
// Identical to wasi-experimental-http currently
// Needs `npm i https://github.com/brendandburns/wasi-http-ts`
import { 
  Method, RequestBuilder 
} from "@brendandburns/wasi-http-ts";
import { Console } from "as-wasi/assembly";

let resp = new RequestBuilder("https://httpbin.org/anything")
    .header("User-Agent", "wasm32-wasi-http")
    .method(Method.GET)
    .send();

let text = String.UTF8.decode(resp.bodyReadAll().buffer);
Console.log(text);
```

</td>
<td>

<--

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-ts/blob/a7eb8737aa12b87f55c60acd6d3dd8be0c9d8508/http/README.md#experimental-http-client-example)
_from dev-wasm-ts_

</td>
<td>

Possible with 
[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=575631506) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

Using [client lib](https://github.com/brendandburns/wasi-http-ts) which [calls](https://github.com/brendandburns/wasi-http-ts/blob/1f8c7d7e48a79575df080a77fe589cf5cf2309ac/index.ts#L202)
[imported](https://github.com/brendandburns/wasi-http-ts/blob/1f8c7d7e48a79575df080a77fe589cf5cf2309ac/raw.ts#L113)
[host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
</table>

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

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[C level](https://github.com/fermyon/spin-dotnet-sdk/blob/0b320bad3c661bb2d3af5950f1b76af8f7fb655d/src/native/wasi-outbound-http.c#L95) 
[binding](https://github.com/fermyon/spin-dotnet-sdk/blob/0b320bad3c661bb2d3af5950f1b76af8f7fb655d/src/HttpInterop.cs#L269) to  
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```csharp
using Wasi.Http;

var client = new HttpClient(new WasiHttpHandler());
var result = await client.GetAsync("https://httpbin.org/anything", 
 System.Threading.CancellationToken.None);
var content = await result.Content.ReadAsStringAsync();
Console.WriteLine(content);
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/Program.cs#L34)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-dotnet/blob/main/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=575630606) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/WasiHttpHandler.cs#L158) [imported](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/WasiHttpExperimental.cs#L25) via [C level](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/req.h#L26)
[bindings](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/wasi_http.c#L93) the [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
</table>

<a id="cpp-wasi"></a>
### C / C++

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[httpclient_wasmedge_socket](https://github.com/hangedfish/httpclient_wasmedge_socket)

</td>
<td>

```cpp
// no SSL support yet
std::array<char, 4096> buf{};
fetchIO *io = fetchGetURL("http://httpbin.org/anything", "4");
int nbytes = fetchIO_read(io, buf.data(), buf.size());
fetchIO_close(io);
std::cout << buf.data() << std::endl;
```

</td>
<td>

[Example](https://github.com/hangedfish/httpclient_wasmedge_socket/blob/2ef71f3cb2e8d05c0d88188df738ba84c865647f/http_get.cpp#L8)

</td>
<td></td>
<td></td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[Raw](https://github.com/hangedfish/httpclient_wasmedge_socket/blob/fde38a90e623e4cb67ed05ffa1fa4acd9b5ee0ae/libfetch/common.c#L802) [socket write](https://github.com/hangedfish/httpclient_wasmedge_socket/blob/fde38a90e623e4cb67ed05ffa1fa4acd9b5ee0ae/libfetch/http.c#L889)
using [WasmEdge Socket SDK for C/C++](https://github.com/hangedfish/wasmedge_wasi_socket_c), which [imports](https://github.com/hangedfish/httpclient_wasmedge_socket/blob/2ef71f3cb2e8d05c0d88188df738ba84c865647f/wasmedge_wasi_socket_c/wasi_socket_ext.c#L133) Wasmedge's implementation of WASI Socket

</td>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```C
#include "req.h"
#include <string.h>
#include <stdio.h>

const char* url =  "https://httpbin.org/anything";
const char* headers = "User-agent: wasm32-wasi-http";
size_t length = 1024 * 1024;
char* buffer = (char*) malloc(length);
uint16_t code;
ResponseHandle handle;

HttpError err = req(url, strlen(url), "GET", 3, headers, 
  strlen(headers), "", 0, &code, &handle);

size_t written;
err = bodyRead(handle, buffer, length, &written);
close(handle);

printf("%s\n", buffer);

free(buffer);
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/main.c#L14)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-c/blob/main/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=575629237) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/main.c#L14) [imported](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/req.h#L26) [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

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

[Spin SDK for (Tiny)Go](https://github.com/fermyon/spin/tree/v1.0/sdk/go)

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

* [Example 1](https://github.com/fermyon/spin/blob/v1.0/examples/http-tinygo-outbound-http/main.go#L14)
* [Example 2](https://github.com/fermyon/spin-kitchensink/blob/855f9477f9090b9cb54e2454b158ef9515f54644/go-outbound-http/main.go#L16)

</td>
<td>

* [Doc](https://developer.fermyon.com/spin/go-components#sending-outbound-http-requests)
* [Doc](https://developer.fermyon.com/spin/http-outbound)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[C level](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/sdk/go/http/outbound_internals.go#L66) 
[binding](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/sdk/go/http/wasi-outbound-http.c#L95) to  
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```go
response, err := Request(
  "https://httpbin.org/anything", "GET",
  "User-agent: wasm32-wasi-http", "")
defer response.Close()

body, err := response.Body()
if err == nil {
  println(string(body))
}
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/main.go#L8)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-go/blob/main/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=575629782) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/req.go#L64) [imported](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/req.go#L36-L38) [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
</table>

<a id="java-wasi"></a>
### Java

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[dicej/spin-teavm-example](https://github.com/dicej/spin-teavm-example)

Uses [forked TeaVM](https://github.com/fermyon/teavm-wasi) as compiler.

</td>
<td>

```java
import wit_wasi_outbound_http.WasiOutboundHttp.*;

Result<Response, HttpError> result =
  WasiOutboundHttp.request(
    new Request(Method.GET, "https://httpbin.org/anything", 
    new ArrayList<>(), new ArrayList<>(), null));

Response resp = result.getOk();
String body = new String(resp.body, UTF_8);
```

</td>
<td>

[Example](https://github.com/dicej/spin-teavm-example/blob/1f4f83bf1ac710a2c38b80be83a808c4570772b6/src/main/java/wit_spin_http/SpinHttpImpl.java#L35-L36)

</td>
<td>

[Readme](https://github.com/dicej/spin-teavm-example/blob/main/README.md)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

Direct [invocation](https://github.com/dicej/spin-teavm-example/blob/1f4f83bf1ac710a2c38b80be83a808c4570772b6/src/main/java/wit_wasi_outbound_http/WasiOutboundHttp.java#L99) 
of [imported](https://github.com/dicej/spin-teavm-example/blob/1f4f83bf1ac710a2c38b80be83a808c4570772b6/src/main/java/wit_wasi_outbound_http/WasiOutboundHttp.java#L49-L50) 
Spin's [host function](https://github.com/fermyon/spin/blob/v0.8.0/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
</table>

<a id="javascript-wasi"></a>
### JavaScript and TypeScript

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

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
<tr>
<td>

[Spin SDK for JavaScript](https://github.com/fermyon/spin-js-sdk)

</td>
<td>

```js
const resp = await fetch('https://httpbin.org/anything');
const decoder = new TextDecoder('utf-8');
const body = decoder.decode(await resp.arrayBuffer());
```

</td>
<td>

[Example](https://github.com/fermyon/spin-js-sdk/blob/v0.4.0/examples/javascript/outbound-http/src/index.js#L5)

</td>
<td>

* [Doc](https://developer.fermyon.com/spin/javascript-components#sending-outbound-http-requests)
* [Doc](https://developer.fermyon.com/spin/http-outbound)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[Invocation](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/js_sdk/modules/spinSdk.ts#L100)
of [bound](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L741)
[JS SDK function](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L111), 
which [calls](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L130)
via [Rust Spin SDK](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/Cargo.toml#L19)
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
<tr>
<td>

[Spin SDK for TypeScript](https://github.com/fermyon/spin-js-sdk)

</td>
<td>

```typescript
const resp = await fetch('https://httpbin.org/anything');
const body = await resp.text();
```

</td>
<td>

[Example](https://github.com/fermyon/spin-js-sdk/blob/v0.4.0/examples/typescript/outbound_http/src/index.ts#L8)

</td>
<td>

* [Doc](https://developer.fermyon.com/spin/javascript-components#sending-outbound-http-requests)
* [Doc](https://developer.fermyon.com/spin/http-outbound)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[Invocation](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/js_sdk/modules/spinSdk.ts#L100)
of [bound](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L741)
[JS SDK function](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L111),
which [calls](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/src/lib.rs#L130)
via [Rust Spin SDK](https://github.com/fermyon/spin-js-sdk/blob/f8833c51ee734e7ad296f7458205b4ff11d1a156/crates/spin-js-engine/Cargo.toml#L19)
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

</td>
</tr>
</table>

<a id="python-wasi"></a>
### Python
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Spin SDK for Python](https://github.com/fermyon/spin-python-sdk)

</td>
<td>

```python
from spin_http import Request, http_send

response = http_send(
  Request('GET', 
  'https://httpbin.org/anything', 
  [], None))

print(str(response.body, 'utf-8'))
```

</td>
<td>

[Example](https://github.com/fermyon/spin-python-sdk/blob/v0.1.1/examples/outbound_http/app.py#L6)

</td>
<td>

* [Doc](https://developer.fermyon.com/spin/python-components#an-outbound-http-example)
* [Doc](https://developer.fermyon.com/spin/http-outbound)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

A Python [`spin_http` module](https://github.com/fermyon/spin-python-sdk/blob/v0.1.1/crates/spin-python-engine/src/lib.rs#L191-L193)
[calls](https://github.com/fermyon/spin-python-sdk/blob/v0.1.1/crates/spin-python-engine/src/lib.rs#L158) [imported](https://github.com/fermyon/spin-python-sdk/blob/v0.1.1/crates/spin-python-engine/src/lib.rs#L16)
via [Rust Spin SDK](https://github.com/fermyon/spin-python-sdk/blob/v0.1.1/crates/spin-python-engine/Cargo.toml#L14) 
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

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

[Spin SDK for Rust](https://github.com/fermyon/spin/tree/v1.0/sdk/rust)

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

* [Example 1](https://github.com/fermyon/spin/blob/v1.0/examples/http-rust-outbound-http/src/lib.rs#L10)
* [Example 2](https://github.com/fermyon/spin-kitchensink/blob/c0d0f2b0487df0cb9f151b7dd8f7cd13f9ab1087/rust-outbound-http/src/lib.rs#L19)
* [Example 3](https://github.com/fermyon/spin/blob/v1.0/sdk/rust/readme.md?plain=1#L46) <sub>(uses [alias](https://github.com/fermyon/spin/blob/v1.0/sdk/rust/src/lib.rs#L36))</sub>

</td>
<td>

* [Doc](https://developer.fermyon.com/spin/rust-components#sending-outbound-http-requests)
* [Doc](https://github.com/fermyon/spin/tree/v1.0/sdk/rust#making-outbound-http-requests)
* [Doc](https://developer.fermyon.com/spin/http-outbound)

</td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[Calling](https://github.com/fermyon/spin/blob/v0.8.0/sdk/rust/src/outbound_http.rs#L43) [imported](https://github.com/fermyon/spin/blob/v0.8.0/crates/trigger/src/lib.rs#L100)
Spin's [host function](https://github.com/fermyon/spin/blob/6cf7447036b7c9238cfa6383cf769b4500e29a38/crates/outbound-http/src/lib.rs#L57).

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
<tr>
<td>

<a id="wasi-experimental-http"></a>
[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```rust
use http;
use wasi_experimental_http;

let req = http::request::Builder::new()
  .uri("https://httpbin.org/anything").body(None).unwrap();
let resp = wasi_experimental_http::request(req);
let data = std::str::from_utf8(&resp.body_read_all().unwrap())
  .unwrap().to_string();
println!("{}", data);
```

</td>
<td>

[Test](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/tests/rust/src/lib.rs#L7)

</td>
<td>

[Doc](https://docs.rs/wasi-experimental-http/0.10.0/wasi_experimental_http/)

</td>
<td></td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/deislabs/wasi-experimental-http/blob/v0.5.0/crates/wasi-experimental-http/src/raw.rs#L180) [imported](https://github.com/deislabs/wasi-experimental-http/blob/v0.5.0/crates/wasi-experimental-http/src/raw.rs#L163-L165) Wasmtime's [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238). The actual request is [here](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L516).

</td>
</tr>
</table>


