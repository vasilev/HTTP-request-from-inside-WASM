Make HTTP request from inside WebAssembly
=========================================

(Wannabe-awesome) list of approaches (recipes, frameworks, http client libraries, etc) to send outbound HTTP(S) requests from inside WebAssembly.

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

[wasi-experimental-http, wasi-http-ts, wasi-http](#assemblyscript-wasi)

</td>
</tr>
<tr>
<td>C#</td>
<td>

[Blazor, Uno Platform](#csharp)

</td>
<td>

[Spin SDK for .NET, wasi-experimental-http, wasi-http](#csharp-wasi)

</td>
</tr>
<tr>
<td>C / C++</td>
<td>

[xxhr](#cpp)

</td>
<td>

[httpclient_wasmedge_socket, wasi-experimental-http, wasi-http](#cpp-wasi)

</td>
</tr>
<tr>
<td>Crystal</td>
<td>

[crystal-js](#crystal)

</td>
<td></td>
</tr>
<tr>
<td>Golang / TinyGo</td>
<td>

[net/http, wasm-fetch, Nigel2392/requester](#golang)

</td>
<td>

[Capsule, Extism PDK for Go, Spin SDK for Go, stealthrocket/net, wasi-experimental-http, wasi-http](#golang-wasi)

</td>
</tr>
<tr>
<td>Haskell</td>
<td></td>
<td>

[Extism PDK for Haskell](#haskell-wasi)

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

[WasmEdge-QuickJs, Extism PDK for JS, Spin SDK for JS / TS](#javascript-wasi)

</td>
</tr>
<tr>
<td>Lua</td>
<td>

[Wasmoon, gluahttp](#lua)

</td>
<td></td>
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

[RustPython, Pyodide, pyodide-http, JupyterLite, PyScript, Panel, RPython, Stlite, micropython-wasm](#python)

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

[reqwest, http_req, Extism PDK for Rust, Spin SDK for Rust, wasi-experimental-http, wasi-http](#rust-wasi)

</td>
</tr>
<tr>
<td>Swift</td>
<td>

[SwiftWasm](#swift)

</td>
<td></td>
</tr>
<tr>
<td>Tcl</td>
<td>

[Wacl](#tcl)

</td>
<td></td>
</tr>
<tr>
<td>Zig</td>
<td></td>
<td>

[Extism PDK for Zig, wasi-experimental-http](#zig-wasi)

</td>
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

<a id="crystal"></a>
### Crystal

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[lbguilherme/crystal-js](https://github.com/lbguilherme/crystal-js)

</td>
<td>

```crystal
require "js"

class XMLHttpRequest < JS::Reference
  @[JS::Method]
  def self.new : self
    <<-js
      return new XMLHttpRequest();
    js
  end

  js_getter responseText : String

  js_method send
  js_method open(method : String, url : String, async : Int32)
end

req = XMLHttpRequest.new
req.open("GET", "https://httpbin.org/anything", 0)
req.send
JS.console.log req.response_text
```

</td>
<td>

* [Example 1](https://github.com/lbguilherme/crystal-js/blob/6fb85504c5393d4fdcd7f080dc0bd6bbb5fbd7a3/README.md?plain=1#L245)
* [Example 2](https://github.com/wasm-outbound-http-examples/crystal/blob/e9cd47aeb218d9e4986ce9cd79329abf9586effb/browser/src/httpget.cr#L18)

</td>
<td>

[Readme](https://github.com/lbguilherme/crystal-js/blob/main/README.md#defining-raw-javascript-methods)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/crystal/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/crystal)

</td>
<td>

Browser, Node.js, and Deno

</td>
<td>

Manual JS `XMLHttpRequest` interop by creating the 
[wrapper](https://github.com/lbguilherme/crystal-js/blob/6fb85504c5393d4fdcd7f080dc0bd6bbb5fbd7a3/README.md?plain=1#L220) 
using [`crystal-js`](https://github.com/lbguilherme/crystal-js) shard.

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
<a id="go-net-http"></a>

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
<tr>
<td>

[Nigel2392/requester](https://github.com/Nigel2392/requester)

</td>
<td>

```go
import "github.com/Nigel2392/requester"

var client = requester.NewAPIClient()
client.Get("https://httpbin.org/anything").Do(
  func(response *http.Response) {
    body, err := io.ReadAll(response.Body)
    if err == nil {
        fmt.Println(string(body))
    }
  }
)
```

</td>
<td>

* [Test](https://github.com/Nigel2392/requester/blob/v1.0.0/client_test.go#L96)
* [Example](https://github.com/wasm-outbound-http-examples/go/blob/48e9b5945a059b5448e88a961d396270a8eccd90/browser-requester/http-get.go#L14)

</td>
<td>

[Sources](https://github.com/Nigel2392/requester/blob/v1.0.0/client_all.go#L72-L118)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/go/requester/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

Browser and maybe Node.js

</td>
<td>

[Uses](https://github.com/Nigel2392/requester/blob/v1.0.0/client.go#L56)
Golang's [`"net/http"`](#go-net-http)

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

### Lua
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Wasmoon](https://github.com/ceifa/wasmoon)

</td>
<td>

```lua
local resp = fetch('https://httpbin.org/anything'):await()
local text = resp:text():await()
print(text)
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/lua/blob/c40b25566336cbb05122937117c6b55bf78742f7/browser-and-node/src/httpget.mjs#L11)

</td>
<td>

[Some doc](https://github.com/ceifa/wasmoon#api-usage)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/lua)

</td>
<td>

[Browser, Node.js, and Deno](https://github.com/ceifa/wasmoon/blob/b4bd60d5fdcc29f51d42286b8183ba89f287ae81/README.md?plain=1#L9)

</td>
<td>

Direct `fetch` interop by manually importing it into Lua using 
[`lua.global.set()`](https://github.com/ceifa/wasmoon/blob/b4bd60d5fdcc29f51d42286b8183ba89f287ae81/src/global.ts#L131).

</td>
</tr>
</table>

#### Lua implemented in Golang
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[cjoudrey/gluahttp](https://github.com/cjoudrey/gluahttp)

</td>
<td>

```lua
local http = require('http')
local res, err = http.request('GET', 
  'https://httpbin.org/anything', {
  headers={
    ['User-Agent']='gluahttp/wasm'
  }
})
print(res.body)
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/lua-in-go/blob/017112ee99c0a0b14a511729310252c1d2fe68ee/browser-gluahttp/main.go#L19)

</td>
<td>

[Readme](https://github.com/cjoudrey/gluahttp#usage)

</td>
<td>

* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/lua-in-go)

</td>
<td>Browser and maybe Node</td>
<td>

[Using](https://github.com/cjoudrey/gluahttp/blob/25003d9adfa90bf4c4609bcebdf2061a5636d532/gluahttp.go#L218)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/cjoudrey/gluahttp/blob/25003d9adfa90bf4c4609bcebdf2061a5636d532/gluahttp.go#L38).

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

<sub>Also note that the [pyodide-http](#pyodide-http) is [bundled](https://github.com/pyodide/pyodide/pull/3355) in Pyodide.</sub>

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
<a id="pyodide-http"></a>

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

* [Example](https://github.com/koenvo/pyodide-http/tree/0.2.1#usage)
* [Patching example](https://github.com/koenvo/pyodide-http/blob/0.2.1/examples/pyvo.html#L12-L13)
* [Patching example](https://github.com/holoviz/panel/blob/v1.1.0/panel/io/pyodide.py#L55-L56) from _panel_

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

[Doc](https://github.com/holoviz/panel/blob/v1.1.0/doc/how_to/wasm/convert.md#handling-http-requests)

</td>
<td></td>
<td>Browser</td>
<td>

[Employs](https://github.com/holoviz/panel/blob/v1.1.0/panel/io/pyodide.py#L56) [koenvo/pyodide-http](#pyodide-http). Also direct [`XMLHttpRequest` interop](https://github.com/holoviz/panel/blob/v1.1.0/panel/io/pyodide.py#L356) for image data.

</td>
</tr>
<tr>
<td>

[JupyterLite](https://github.com/jupyterlite/jupyterlite)

</td>
<td>

```python
# using Pandas
import pyodide_http; pyodide_http.patch_all()
import pandas as pd

data = pd.read_json('https://httpbin.org/json')
data
```

```python
# using js.fetch
from js import fetch
res = await fetch('https://httpbin.org/anything')
text = await res.text()
print(text)
```

```python
# using requests
import micropip; await micropip.install(['requests'])
import pyodide_http; pyodide_http.patch_all()

import requests
res = requests.get("https://httpbin.org/anything")
print(res.text)
```

</td>
<td>

* [Example](https://github.com/jupyterlite/jupyterlite/blob/v0.1.1/examples/pyodide/plotly.ipynb?short_path=7be76b8#L75)
* [Example](https://github.com/jupyterlite/jupyterlite/blob/v0.1.1/examples/python.ipynb?short_path=d44a323#L194)
* [Example](https://github.com/jupyterlite/jupyterlite/blob/v0.1.1/docs/howto/content/python.md?plain=1#L73)

</td>
<td>

[Doc](https://github.com/jupyterlite/jupyterlite/blob/v0.1.1/docs/howto/content/python.md#fetching-remote-content)

</td>
<td>

[Playground](https://jupyterlite.readthedocs.io/en/latest/_static/lab/index.html)

</td>
<td>Browser</td>
<td>

Employing [`pyodide-http`](#pyodide-http) and [Pyodide](https://github.com/jupyterlite/pyodide-kernel/blob/v0.1.0/jupyterlite_pyodide_kernel/constants.py#L32)'s own facilities.

</td>
</tr>
<tr>
<td>

[micropython-wasm](https://github.com/rafi16jan/micropython-wasm)

</td>
<td>

```python
import js

fetch = JS('fetch')

response = fetch('https://httpbin.org/anything').wait()
text = response.text().wait()
print(text)
```

</td>
<td>

* [Example 1](https://github.com/rafi16jan/micropython-wasm/blob/74d3da30dd9baa39aa1429bb1548d49b7a1662e1/README.md?plain=1#L141)
* [Example 2](https://github.com/wasm-outbound-http-examples/micropython/blob/7cd478c7654c00a12dce887f9119a771d8bd1286/browser-and-node/src/httpget-node.js#L11)

</td>
<td>

[Readme](https://github.com/rafi16jan/micropython-wasm/blob/74d3da30dd9baa39aa1429bb1548d49b7a1662e1/README.md?plain=1#L69)

</td>
<td>

* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/micropython)

</td>
<td>

Browser and Node.js

</td>
<td>

Direct `fetch` interop using [js](https://github.com/rafi16jan/micropython-wasm/blob/74d3da30dd9baa39aa1429bb1548d49b7a1662e1/js.py#L111) module, by employing Emscripten APIs.

</td>
</tr>
<tr>
<td>

[Stlite](https://github.com/whitphx/stlite)

<sub>a port of [Streamlit](https://streamlit.io/) to Wasm</sub>

</td>
<td>

```python
from pyodide.http import pyfetch
import streamlit as st

response = await pyfetch("https://httpbin.org/anything")
body = await response.string()
st.write(body)
```

</td>
<td>

* [Example 1](https://github.com/whitphx/stlite/blob/v0.38.0/packages/sharing-editor/public/samples/011_component_gallery/pages/charts.audio.py#L16)
* [Example 2](https://github.com/whitphx/stlite/blob/v0.38.0/README.md?plain=1#L322)
* [Pandas + open_url example](https://github.com/whitphx/stlite/blob/v0.38.0/packages/sharing-editor/public/samples/012_custom_components/pages/aggrid.py#L11)

</td>
<td>

[Readme](https://github.com/whitphx/stlite#example-2-pyodidehttppyfetch)

</td>
<td>

[Playground](https://edit.share.stlite.net/)

</td>
<td>Browser</td>
<td>

[Uses](https://github.com/whitphx/stlite/blob/v0.38.0/packages/kernel/package.json#L30) [pyodide](#pyodide)'s [facilities](https://github.com/whitphx/stlite/blob/v0.38.0/README.md?plain=1#L271).

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

### Tcl

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Wacl](https://github.com/ecky-l/wacl)

</td>
<td>

```tcl
set func_ptr_number 2
puts [::wacl::jscall $func_ptr_number "string" "string" "https://httpbin.org/anything"]
```

Needs a JavaScript-side function registered using `jswrap()`:
```js
wacl.onReady(function (interpreter) {
  const wrappedFuncName = interpreter.jswrap(function (ptrUrl) {
    const url = interpreter.ptr2str(ptrUrl);
    const xhr = new XMLHttpRequest();
    xhr.open('GET', url, false);
    xhr.send();
    return interpreter.str2ptr(xhr.responseText);
  }, 'string', 'string');
});
```

</td>
<td>

* [Example](https://github.com/wasm-outbound-http-examples/tcl/blob/1d5be00db183cba88da520b0ef8352ab31e48909/index.html#L31)
* [`jswrap` example](https://github.com/wasm-outbound-http-examples/tcl/blob/1d5be00db183cba88da520b0ef8352ab31e48909/index.html#L40)

</td>
<td>

[Readme](https://github.com/ecky-l/wacl/blob/9daacabb0102a9986f33263261350edfeebdd83b/README.md?plain=1#L17)

</td>
<td>

[Demo / Playground](https://wasm-outbound-http-examples.github.io/tcl/)

</td>
<td>

Browser

</td>
<td>

Manual JS `XMLHttpRequest` interop by 
[registering](https://github.com/wasm-outbound-http-examples/tcl/blob/1d5be00db183cba88da520b0ef8352ab31e48909/index.html#L40) 
a function on JS side using 
[`jswrap()`](https://github.com/ecky-l/wacl/blob/master/js/preJsRequire.js#L82-L85) via Emscripten `addFunction()` API
and then [calling](https://github.com/wasm-outbound-http-examples/tcl/blob/1d5be00db183cba88da520b0ef8352ab31e48909/index.html#L31) it
using [`::wacl::jscall`](https://github.com/ecky-l/wacl/blob/9daacabb0102a9986f33263261350edfeebdd83b/opt/wacl.c#L205-L209) 
by its registration number.

</td>
</tr>
</table>


Standalone and server-side runtimes (mostly WASI and WASI-Socket-enabled), incl containers, FaaS, Edge Computing, etc
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

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=wasi-experimental-http&repo=656267188) _created by brendandburns_

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
[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=wasi-experimental-http&repo=656267188) _created by brendandburns_

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
<tr>
<td>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [stealthrocket/wasi-go](https://github.com/stealthrocket/wasi-go)

</td>
<td>

```typescript
import { Console } from "as-wasi/assembly";
import { request } from "./request";
export function cabi_realloc(a: usize, b: usize,
                             c: usize, len: usize): usize {
 return heap.alloc(len);
}

let response = request("GET", "https://httpbin.org/anything", null,
  [{ name: "User-Agent", value: "wasi-http" }]);

Console.log(response.Body);
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/main.ts#L9)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-ts) _by brendandburns_

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/stealthrocket/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/request.ts#L112) to
[imported](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/raw.ts#L35)

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

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

[Readme](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=wasi-experimental-http&repo=650329121) _created by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/WasiHttpHandler.cs#L158) [imported](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/WasiHttpExperimental.cs#L25) via [C level](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/req.h#L26)
[bindings](https://github.com/dev-wasm/dev-wasm-dotnet/blob/a08955929b18352c1ff4916a3ecd5aca9237539c/http/wasi_http.c#L93) the [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
<tr>
<td>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [stealthrocket/wasi-go](https://github.com/stealthrocket/wasi-go)

</td>
<td>

```csharp
// *Still* identical to wasi-experimental-http's code. 
using Wasi.Http;

var client = new HttpClient(new WasiHttpHandler());
var result = await client.GetAsync("https://httpbin.org/anything", 
 System.Threading.CancellationToken.None);
var content = await result.Content.ReadAsStringAsync();
Console.WriteLine(content);
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/Program.cs#L34)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-dotnet) _by brendandburns_

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/stealthrocket/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

<sub>Sequence: .Net -> C -> WASI</sub>

[Calling](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/WasiHttpHandler.cs#L194) 
[imported](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/WasiHttpExperimental.cs#L25) 
C-level
[Mono binding](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/wasi_http.c#L171) 
which [calls](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/wasi_http.c#L53)
[generated](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/README.md?plain=1#L111-L121)
(<sub>by [`wit-bindgen`](https://github.com/bytecodealliance/wit-bindgen) from the [wit template](https://github.com/WebAssembly/wasi-http/blob/19a019bd5917da7e110ef1b7e6bed6e22297d436/wit/outgoing-handler.wit#L14)</sub>)
code, which calls [imported](https://github.com/dev-wasm/dev-wasm-dotnet/blob/25872298e129526b2b127c930dbebc84ce7e69e4/http/proxy.c#L213)

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

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

[Readme](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=wasi-experimental-http&repo=648389246) _created by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/main.c#L14) [imported](https://github.com/dev-wasm/dev-wasm-c/blob/37e5fcc2cad204ed2534762e81bbceaa32399952/http/req.h#L26) [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
<tr>
<td>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [stealthrocket/wasi-go](https://github.com/stealthrocket/wasi-go)

</td>
<td>

<details>

<summary>

```C
// snippet, expand it for full code
types_outgoing_request_t request = types_new_outgoing_request(
        &method, &path, &query, &scheme, &domain, headers);

response = default_outgoing_http_handle(request, NULL);

types_future_incoming_response_get(response, &result);

types_incoming_response_consume(result.val.ok, &stream);

streams_read(stream, len, &body_res, &err);

```

</summary>

--------

```C
#include "proxy.h" // Generated by wit-bindgen
// from https://github.com/WebAssembly/wasi-http/tree/main/wit
#include <stdio.h>

void http_handle(uint32_t arg, uint32_t arg0) {}

int main() {
    types_headers_t headers = types_new_fields(NULL);
    types_method_t method = {.tag = TYPES_METHOD_GET};
    types_scheme_t scheme = {.tag = TYPES_SCHEME_HTTPS};
    proxy_string_t path, domain, query;
    proxy_string_set(&domain, "httpbin.org");
    proxy_string_set(&path, "/anything");
    proxy_string_set(&query, "");

    types_outgoing_request_t request = types_new_outgoing_request(
        &method, &path, &query, &scheme, &domain, headers);
    types_future_incoming_response_t response;

    response = default_outgoing_http_handle(request, NULL);

    proxy_result_incoming_response_error_t result;
    types_future_incoming_response_get(response, &result);

    types_incoming_stream_t stream;
    types_incoming_response_consume(result.val.ok, &stream);

    int32_t len = 16 * 1024;
    proxy_tuple2_list_u8_bool_t body_res;
    streams_stream_error_t err;
    streams_read(stream, len, &body_res, &err);

    printf("Response body: %s\n", body_res.f0.ptr);

    proxy_tuple2_list_u8_bool_free(&body_res);
    types_drop_outgoing_request(request);
    streams_drop_input_stream(stream);
    types_drop_incoming_response(result.val.ok);

    return 0;
}
```

</details>

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-c/blob/b79356766301744b4d879c0be9feeababb17e445/http/main.c#L50)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-c/blob/main/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-c) _by brendandburns_

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/stealthrocket/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-c/blob/b79356766301744b4d879c0be9feeababb17e445/http/main.c#L50)
a function [generated](https://github.com/dev-wasm/dev-wasm-c/blob/b79356766301744b4d879c0be9feeababb17e445/http/Makefile#L9)
by [`wit-bindgen`](https://github.com/bytecodealliance/wit-bindgen) from the [wit template](https://github.com/WebAssembly/wasi-http/blob/19a019bd5917da7e110ef1b7e6bed6e22297d436/wit/outgoing-handler.wit#L14),
which calls the 

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

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

[Extism Plug-in Development Kit (PDK) for (Tiny)Go](https://github.com/extism/go-pdk)

</td>
<td>

```go
import "github.com/extism/go-pdk"

req := pdk.NewHTTPRequest("GET", "https://httpbin.org/anything")
resp := req.Send()

pdk.OutputMemory(resp.Memory())
```

</td>
<td>

[Example](https://github.com/extism/go-pdk/blob/v.0.1.0/example/http.go#L14)

</td>
<td>

[Doc](https://extism.org/docs/write-a-plugin/go-pdk/#using-extism-built-in-http)

</td>
<td></td>
<td>

Extism [uses](https://github.com/extism/extism/blob/v0.4.0/runtime/Cargo.toml#L12) Wasmtime

</td>
<td>

[Calling](https://github.com/extism/go-pdk/blob/v.0.1.0/extism_pdk.go#L257)
[C-level-imported](https://github.com/extism/go-pdk/blob/v.0.1.0/extism-pdk.h#L47-L48)
runtime's [host function](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L297)
[exported](https://github.com/extism/extism/blob/v0.4.0/runtime/src/plugin.rs#L112) for plugins,
which [makes](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L358) actual request using `ureq`.

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

[Readme](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://github.com/codespaces/new?hide_repo_select=true&ref=wasi-experimental-http&repo=648324699) _created by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/req.go#L64) [imported](https://github.com/dev-wasm/dev-wasm-go/blob/d7482362e292598bdb04493a6b664272a60e9c71/http/req.go#L36-L38) [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238) implemented in [wasi-experimental-http-wasmtime](https://github.com/deislabs/wasi-experimental-http/tree/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime) Wasmtime's WASI module.

</td>
</tr>
<tr>
<td>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [stealthrocket/wasi-go](https://github.com/stealthrocket/wasi-go)

</td>
<td>

```go
import (
  "io/ioutil"
  "net/http"
  wasiclient "github.com/dev-wasm/dev-wasm-go/client"
)

client := http.Client{
  Transport: wasiclient.WasiRoundTripper{},
}
response, err := client.Get("https://httpbin.org/anything")
defer response.Body.Close()

body, err := ioutil.ReadAll(response.Body)
if err == nil {
  println(string(body))
}
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/main.go#L27)

</td>
<td>

[Readme](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/README.md#experimental-http-client-example)

</td>
<td>

[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-go) _by brendandburns_
<sub>needs plenty of RAM to compile (~4G), so may cause OOM on 2-core instance</sub>

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/stealthrocket/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

<sub>Sequence: Go -> C -> WASI</sub>

[Calling](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/client/transport.go#L113)
a [method](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/proxy/proxy.go#L1504)
[generated](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/README.md?plain=1#L22)
by [`wit-bindgen`](https://github.com/bytecodealliance/wit-bindgen) from the [wit template](https://github.com/WebAssembly/wasi-http/blob/19a019bd5917da7e110ef1b7e6bed6e22297d436/wit/outgoing-handler.wit#L14).
That method [calls](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/proxy/proxy.go#L1538) 
the generated C-level-bound [function](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/proxy/proxy.c#L1289),
which [calls](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/proxy/proxy.c#L1349)
the [imported](https://github.com/dev-wasm/dev-wasm-go/blob/9373e164f38a5e07f73fe232636687545694f373/http/proxy/proxy.c#L228)

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

</td>
</tr>
<tr>
<td>

[stealthrocket/net](https://github.com/stealthrocket/net)

<sub>Use `gotip` until [Go 1.21](https://github.com/stealthrocket/net/blob/v0.1.4/README.md?plain=1#L18) is released.</sub> 

</td>
<td>

```go
import ( 	"fmt" ; "io" ; "net/http"
  _ "github.com/stealthrocket/net/http"
)

response, err := http.Get("http://httpbin.org/anything")
if err != nil {
  fmt.Println(err)
}
defer response.Body.Close()

body, err := io.ReadAll(response.Body)
if err == nil {
  fmt.Println(string(body))
}
```

</td>
<td>

* [Test](https://github.com/stealthrocket/net/blob/v0.1.4/http/http_wasip1_test.go#L33)
* [HTTP Example](https://github.com/wasm-outbound-http-examples/go/blob/c48072d362c953ef88498967fe20efb642959527/wasi-stealthrocket-net/httpget.go#L12)
* [HTTPS Example](https://github.com/wasm-outbound-http-examples/go/blob/c48072d362c953ef88498967fe20efb642959527/wasi-stealthrocket-net/httpsget.go#L22)

</td>
<td>

[Readme](https://github.com/stealthrocket/net/blob/v0.1.4/README.md#configuration)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

[Wazero and WasmEdge](https://github.com/stealthrocket/net/blob/v0.1.4/README.md?plain=1#L10-L11)

</td>
<td>

[Hotpatching](https://github.com/stealthrocket/net/blob/v0.1.4/http/http_wasip1.go#L13) on module import `http.DefaultTransport` with
`wasip1.DialContext`
which refers to 
[imported `sock_conn()`](https://github.com/stealthrocket/net/blob/v0.1.4/wasip1/syscall_wasmedge_wasip1.go#L143) in the case of WasmEdge
and to [`syscall.Connect()`](https://github.com/stealthrocket/wasi-go/blob/v0.6.9/internal/sockets/dial.go#L24) in the case of Wazero.

</td>
</tr>
</table>

<a id="haskell-wasi"></a>
### Haskell

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for Haskell](https://github.com/extism/haskell-pdk)

</td>
<td>

```haskell
module Main where

import Extism.PDK
import Extism.PDK.HTTP

https_get = do
  let url = "https://httpbin.org/anything"
  let req = newRequest url
  resp <- sendRequest req Nothing
  outputMemory (memory resp)

foreign export ccall "https_get" https_get :: IO ()

main = https_get
```

</td>
<td>

[Example](https://github.com/extism/haskell-pdk/blob/f5d768c8fee67cae176eed22dcb3276577ecf46b/examples/HTTPGet.hs#L12)

</td>
<td>

[Doc](https://extism.org/docs/write-a-plugin/haskell-pdk/#using-extism-built-in-http)

</td>
<td></td>
<td>

Extism [uses](https://github.com/extism/extism/blob/v0.4.0/runtime/Cargo.toml#L12) Wasmtime

</td>
<td>

[Calling](https://github.com/extism/haskell-pdk/blob/f5d768c8fee67cae176eed22dcb3276577ecf46b/src/Extism/PDK/HTTP.hs#L71)
[imported](https://github.com/extism/haskell-pdk/blob/f5d768c8fee67cae176eed22dcb3276577ecf46b/src/Extism/PDK/Bindings.hs#L43)
runtime's [host function](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L297)
[exported](https://github.com/extism/extism/blob/v0.4.0/runtime/src/plugin.rs#L112) for plugins,
which [makes](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L358) actual request using `ureq`.

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

[Extism Plug-in Development Kit (PDK) for JavaScript](https://github.com/extism/js-pdk)

</td>
<td>

```js
function https_get() {
  let resp = Http.request(
    {
      url: 'https://httpbin.org/anything',
      method: 'GET',
      headers: { 'User-Agent': 'extism_pdk' }
    },
    null
  );
  Host.outputString(resp.body);
}
module.exports = { https_get }
```

</td>
<td>

[Example](https://github.com/extism/js-pdk/blob/v0.5.0/script.js#L49)

</td>
<td>

[Some doc](https://extism.org/docs/write-a-plugin/js-pdk/)

</td>
<td></td>
<td>

Extism [uses](https://github.com/extism/extism/blob/v0.4.0/runtime/Cargo.toml#L12) Wasmtime

</td>
<td>

`Http` object [injected](https://github.com/extism/js-pdk/blob/v0.5.0/crates/core/src/globals.rs#L21) into QuickJS's
global namespace. It [calls](https://github.com/extism/js-pdk/blob/v0.5.0/crates/core/src/globals.rs#L176) the 
[`http::request()`](https://github.com/extism/rust-pdk/blob/v0.3.3/src/http.rs#L35)
from [Extism PDK for Rust](#extism-rust-pdk).

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
<a id="extism-rust-pdk"></a>

[Extism Plug-in Development Kit (PDK) for Rust](https://github.com/extism/rust-pdk)

</td>
<td>

```rust
use extism_pdk::*;

#[plugin_fn]
pub fn https_get(_:()) -> FnResult<HttpResponse> {
  let req = HttpRequest::new("https://httpbin.org/anything");
  let resp = http::request::<()>(&req, None)?;
  Ok(resp)
}
```

</td>
<td>

[Example](https://github.com/extism/rust-pdk/blob/v0.3.3/examples/http.rs#L8)

</td>
<td>

[Doc](https://extism.org/docs/write-a-plugin/rust-pdk/#using-extism-built-in-http)

</td>
<td>

Possible with
[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-rust) _by brendandburns_

</td>
<td>

Extism [uses](https://github.com/extism/extism/blob/v0.4.0/runtime/Cargo.toml#L12) Wasmtime

</td>
<td>

[Calling](https://github.com/extism/rust-pdk/blob/v0.3.3/src/http.rs#L46)
[C-level-imported](https://github.com/extism/rust-pdk/blob/v0.3.3/src/bindings.rs#L17)
runtime's [host function](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L297)
[exported](https://github.com/extism/extism/blob/v0.4.0/runtime/src/plugin.rs#L112) for plugins,
which [makes](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L358) actual request using `ureq`.

</td>
</tr>
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

[WasmEdge Sockets](https://wasmedge.org/docs/develop/wasmedge/extensions/unique_extensions#available-extensions)

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
<tr>
<td>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [stealthrocket/wasi-go](https://github.com/stealthrocket/wasi-go)

</td>
<td>

```rust
let headers = types::new_fields(&[("User-agent", "WASI-HTTP")]);
let request = types::new_outgoing_request(
  types::MethodParam::Get, "/anything", "",
  Some(types::SchemeParam::Https), "httpbin.org", headers,
);

let future_response = default_outgoing_http::handle(request, None);

types::drop_outgoing_request(request);
let response = types::future_incoming_response_get(future_response)
  .ok_or_else(|| anyhow!("response is available immediately"))?
  .map_err(|err| anyhow!("response error: {err:?}"))?;
types::drop_future_incoming_response(future_response);
let stream = types::incoming_response_consume(response)
  .map_err(|()| anyhow!("response has no body stream"))?;
let mut body = Vec::new();
let mut is_eof = false;
while !is_eof {
  let (mut chunk, stream_at_end) = streams::read(stream, u64::MAX)?;
  is_eof = stream_at_end;
  body.append(&mut chunk);
}
streams::drop_input_stream(stream);
types::drop_incoming_response(response);
println!("body: {}", str::from_utf8(&body).unwrap());
```

</td>
<td>

[Example](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/test-programs/wasi-http-tests/src/bin/outbound_request.rs#L62)

</td>
<td>

[Readme](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/README.md#wasi-http)

</td>
<td>

Possible with
[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-rust) _by brendandburns_

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/stealthrocket/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

Rust code 
[generated](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/test-programs/wasi-http-tests/src/lib.rs#L3)
(<sub>by [`wit-bindgen`](https://github.com/bytecodealliance/wit-bindgen) from the [wit template](https://github.com/WebAssembly/wasi-http/blob/acbc244dfafbabc08c895b839698fe7aad5f8c5a/wit/outgoing-handler.wit#L14)</sub>)
calls imported

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/stealthrocket/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

</td>
</tr>
</table>

<a id="zig-wasi"></a>
### Zig

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for Zig](https://github.com/extism/zig-pdk)

</td>
<td>

```zig
const std = @import("std");
const extism_pdk = @import("extism-pdk");
const allocator = std.heap.wasm_allocator;

export fn https_get() i32 {
const plugin = extism_pdk.Plugin.init(allocator);
var req = extism_pdk.http.HttpRequest.init(allocator, "GET", 
  "https://httpbin.org/anything");
defer req.deinit();
req.setHeader("User-Agent", "extism_pdk") catch unreachable;

const resp = plugin.request(req, null) catch unreachable;
defer resp.deinit();

plugin.outputMemory(resp.memory);
return 0;
}
```

</td>
<td>

[Example](https://github.com/extism/zig-pdk/blob/55bde28e8ef1adfe505b15485ae4dafcd5e6a805/examples/basic.zig#L62)

</td>
<td>

[Some doc](https://extism.org/docs/write-a-plugin/zig-pdk#example-usage)

</td>
<td></td>
<td>

Extism [uses](https://github.com/extism/extism/blob/v0.4.0/runtime/Cargo.toml#L12) Wasmtime

</td>
<td>

[Calling](https://github.com/extism/zig-pdk/blob/55bde28e8ef1adfe505b15485ae4dafcd5e6a805/src/main.zig#L138)
[imported](https://github.com/extism/zig-pdk/blob/55bde28e8ef1adfe505b15485ae4dafcd5e6a805/src/ffi.zig#L17)
runtime's [host function](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L297)
[exported](https://github.com/extism/extism/blob/v0.4.0/runtime/src/plugin.rs#L112) for plugins,
which [makes](https://github.com/extism/extism/blob/v0.4.0/runtime/src/pdk.rs#L358) actual request using `ureq`.

</td>
</tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

</td>
<td>

```zig
var gp_all = std.heap.GeneralPurposeAllocator(.{}){};
const allocator = gp_all.allocator();
var status: u16 = 0;
var handle: u32 = 0;

_ = request("https://httpbin.org/anything", "GET", "", "", &status, &handle);
defer _ = close(@bitCast(i32, handle));

var headers_buffer = try allocator.alloc(u8, 1024);
var header_len: u32 = 0;
_ = header(handle, "content-length", headers_buffer, &header_len);
const length = try std.fmt.parseInt(u32, headers_buffer[0..header_len], 10);
var buffer = try allocator.alloc(u8, length + 1);
defer allocator.free(buffer);

var written: u32 = 0;
_ = body_read(handle, &buffer[0], @bitCast(i32, buffer.len), &written);
try std.io.getStdOut().writer().print("{s}\n", .{buffer[0..written]});
```

</td>
<td>

[Example](https://github.com/dev-wasm/dev-wasm-zig/blob/84c2edf33e025103aae4d0861177585cc56fac8e/src/http.zig#L32)

</td>
<td>

[Doc](https://docs.rs/wasi-experimental-http/0.10.0/wasi_experimental_http/)

</td>
<td>

[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-zig) _by brendandburns_

</td>
<td>

Wasmtime with integrated `wasi-experimental-http` crate, e.g. [brendandburns's fork](https://github.com/brendandburns/wasmtime/commit/e2a567c4ca38190a74a7eca62cf65892547f2f3b)

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-zig/blob/84c2edf33e025103aae4d0861177585cc56fac8e/src/http.zig#L17) 
[imported](https://github.com/dev-wasm/dev-wasm-zig/blob/84c2edf33e025103aae4d0861177585cc56fac8e/src/http.zig#L1) 
Wasmtime's [host function](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L238).
The actual request is [here](https://github.com/deislabs/wasi-experimental-http/blob/8291baece45cc51e18e69d7d5ad39ca20744e9f9/crates/wasi-experimental-http-wasmtime/src/lib.rs#L516).

</td>
</tr>
</table>


