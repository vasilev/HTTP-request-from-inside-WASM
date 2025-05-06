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
<th>Browsers and JS runtimes</th>
<th>Standalone / server-side / WASI runtimes</th>
</tr>
<tr>
<td>AssemblyScript</td>
<td></td>
<td>

[wasi-experimental-http, wasi-http-ts](#assemblyscript-wasi)

</td>
</tr>
<tr>
<td>C# / .Net</td>
<td>

[Uno Platform](#csharp)

</td>
<td>

[wasi-experimental-http](#csharp-wasi)

</td>
</tr>
<tr>
<td>C / C++</td>
<td>



</td>
<td>

[wasi-experimental-http](#cpp-wasi)

</td>
</tr>
<tr>
<td>Golang / TinyGo</td>
<td></td>
<td>

[wasi-experimental-http](#golang-wasi)

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
<td>Python</td>
<td>

[requests-wasm-polyfill](#python)

</td>
<td></td>
</tr>
<tr>
<td>Rust</td>
<td></td>
<td>

[wasi-experimental-http](#rust-wasi)

</td>
</tr>
<tr>
<td>Zig</td>
<td></td>
<td>

[wasi-experimental-http](#zig-wasi)

</td>
</tr>
</table>

Browser WASM runtimes and standalone JS runtimes like Node.js and Deno (and other V8-based), also Bun
-----------------------------------------------------------------------------------------------------

<a id="csharp"></a>
### C#

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Uno Platform](https://platform.uno/)

> [!CAUTION]
> <sub>`Uno.UI.Wasm. WasmHttpHandler` deprecated since .NET 6</sub>


> [!TIP]
> <sub>[Use](README.md#uno-platform) `System.Net. Http.HttpClient` instead.</sub>

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

### PHP
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[PIB: PHP in Browser aka php-wasm](https://github.com/seanmorris/php-wasm/)

> [!CAUTION]
> <sub>This code does not work in php-wasm v0.0.8.</sub>


> [!TIP]
> <sub>Use [up-to-date method](README.md#php-wasm) instead.</sub>

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


### Python

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[requests-wasm-polyfill](https://github.com/emscripten-forge/requests-wasm-polyfill)

<sub>For [pyjs](https://github.com/emscripten-forge/pyjs)</sub>

> [!CAUTION]
> <sub>Repo was [archived](https://github.com/emscripten-forge/requests-wasm-polyfill/issues/7) and package was [dropped from recipes](https://github.com/emscripten-forge/recipes/pull/796) on Feb 6, 2024.</sub>


> [!TIP]
> <sub>[Use](https://github.com/emscripten-forge/requests-wasm-polyfill/blob/568560020f74704c183fe49f8e527942d19e276c/README.md?plain=1#L8) the official `requests` instead.</sub>

</td>
<td>

```python
import requests

r = requests.get('https://httpbin.org/anything')
result = r.text
print(result)
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/pyjs/blob/596d23d2dcd930ec7025eb734feaaffa478c13f5/requests-wasm-polyfill/script.js#L26)

</td>
<td></td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/pyjs/requests-wasm-polyfill/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/pyjs)

</td>
<td>

Browser

</td>
<td>

Direct [`XMLHttpRequest` interop](https://github.com/emscripten-forge/requests-wasm-polyfill/blob/0.3.0/requests/api.py#L41) in
[sync](https://github.com/emscripten-forge/requests-wasm-polyfill/blob/0.3.0/requests/api.py#L27) mode.

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
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[wasi-experimental-http](https://www.npmjs.com/package/@deislabs/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#assemblyscript-wasi-http) instead.</sub>

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

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#assemblyscript-wasi-http) instead.</sub>

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

&lt;--

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
</table>


<a id="csharp-wasi"></a>
### C# / .Net

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#csharp-wasi-http) instead.</sub>

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
</table>


<a id="cpp-wasi"></a>
### C / C++

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#cpp-wasi-http) instead.</sub>

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
</table>


<a id="golang-wasi"></a>
### Golang (Tinygo)

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#golang-wasi-http) instead.</sub>

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
</table>


<a id="rust-wasi"></a>
### Rust

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<tr>
<td>

<a id="wasi-experimental-http"></a>
[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use [wasi-http](README.md#wasi-http) instead.</sub>

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


<a id="zig-wasi"></a>
### Zig

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[wasi-experimental-http](https://crates.io/crates/wasi-experimental-http)

> [!CAUTION]
> <sub>[Repo](https://github.com/deislabs/wasi-experimental-http) was archived on Feb 22, 2024.</sub>


> [!TIP]
> <sub>Use wasi-http instead.</sub>

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
