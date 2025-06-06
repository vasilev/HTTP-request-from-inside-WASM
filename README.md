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
<td>Ada</td>
<td>

[AdaWebPack](#ada)

</td>
<td></td>
</tr>
<tr>
<td>AssemblyScript</td>
<td>

[as-fetch](#assemblyscript)

</td>
<td>

[wasi-http](#assemblyscript-wasi)

</td>
</tr>
<tr>
<td>BASIC</td>
<td>

[EndBASIC, gobasic](#basic)

</td>
<td></td>
</tr>
<tr>
<td>C# / .Net</td>
<td>

[Blazor, OpenSilver, RestSharp, System.Net.Http.HttpClient, Uno Platform](#csharp)

</td>
<td>

[Extism PDK for .NET, Spin SDK for .NET, wasi-http](#csharp-wasi)

</td>
</tr>
<tr>
<td>C / C++</td>
<td>

[Emscripten, xxhr](#cpp)

</td>
<td>

[Extism PDK for C, httpclient_wasmedge_socket, wasi-http](#cpp-wasi)

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
<td>Dart</td>
<td>

[package:http, package:web, dio, fetch_api, fetch_client, dart:js_interop, requests, Cloudflare Workers SDK](#dart)

</td>
<td></td>
</tr>
<tr>
<td>Forth</td>
<td>

[WAForth](#forth)

</td>
<td></td>
</tr>
<tr>
<td>Golang / TinyGo</td>
<td>

[net/http, wasm-fetch, Nigel2392/requester, Anko, Risor, Tengo, Hogosuru, Vecty, Vugu, Yaegi](#golang)

</td>
<td>

[Capsule, Extism PDK for Go, go-plugin, Spin SDK for Go, dispatchrun/net, wasi-http,
wasi-http-go, Wasm Workers Server](#golang-wasi)

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

[Goja, gojax/fetch, Jint, libcurl.js, Otto, quickjs-emscripten, sebastianwessel/quickjs](#javascript)

</td>
<td>

[WasmEdge-QuickJs, Extism PDK for JS, Spin SDK for JS / TS, Wasm Workers Server](#javascript-wasi)

</td>
</tr>
<tr>
<td>Kotlin</td>
<td>

[Kotlin/Wasm](#kotlin)

</td>
<td></td>
</tr>
<tr>
<td>Lisp</td>
<td>

[Janet](#lisp)

</td>
<td></td>
</tr>
<tr>
<td>Lua</td>
<td>

[Wasmoon, gluahttp, lmodhttpclient, gopher-lua-libs, Pluto](#lua)

</td>
<td></td>
</tr>
<tr>
<td>PHP</td>
<td>

[php-wasm](#php)

</td>
<td></td>
</tr>
<tr>
<td>Pascal</td>
<td>

[Free Pascal](#pascal)

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
<td>Prolog</td>
<td>

[ichiban/prolog, Scryer Prolog, SWI-Prolog, trealla-js](#prolog)

</td>
<td>

[Spin SDK for Prolog](#prolog-wasi)

</td>
</tr>
<tr>
<td>Python</td>
<td>

[RustPython, Pyodide, pyodide-http, GPython, JupyterLite, PyScript, Panel, PocketPy, RPython, Stlite,
 urllib3, micropython-wasm](#python)

</td>
<td>

[componentize-py, Extism PDK for Python, Spin SDK for Python](#python-wasi)

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

[wasm-bindgen, Cloudflare Workers SDK, ehttp, gloo_net, httpc, http-client, 
iced, leptos, localghost, MoonZoon, quad-net,
reqwasm, reqwest, sauron, seed, surf,
sycamore](#rust) Scripting: [Rune](#rust-scripting) 

</td>
<td>

[reqwest, http_req, Extism PDK for Rust, Spin SDK for Rust, waki,
wasi-http, Wasm Workers Server](#rust-wasi)

</td>
</tr>
<tr>
<td>Starlark</td>
<td>

[starlark-go, starlark-go-nethttp, starlib, starlight, starlight-enhanced](#starlark)

</td>
<td></td>
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

[criTiCaL, Wacl](#tcl)

</td>
<td></td>
</tr>
<tr>
<td>Wonkey</td>
<td>

[Wonkey/httprequest](#wonkey)

</td>
<td></td>
</tr>
<tr>
<td>Zig</td>
<td></td>
<td>

[Extism PDK for Zig, Spin SDK for Zig](#zig-wasi)

</td>
</tr>
<tr>
<td>Misc langs</td>
<td>

Berry: [berry](#berry)
, Expression: [Cel-go, Expr](#expression)
, Rebol: [rye](#rebol)

</td>
<td>

MoonBit: [Extism PDK for MoonBit](#moonbit-wasi), 
Virgil: [Extism PDK for Virgil](#virgil-wasi)

</td>
</tr>
</table>

Browser WASM runtimes and V8-based runtimes like Node.js and Deno, also Bun
---------------------------------------------------------------------------

### Ada
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[AdaWebPack](https://github.com/godunko/adawebpack)

</td>
<td>

```ada
L   : aliased Listener;
xhr : Web.XHR.Requests.XML_Http_Request;

overriding procedure Handle_Event
  (Self : in out Listener; Event : in out Web.DOM.Events.Event'Class)
is
  use type Web.XHR.Requests.State;
begin
  if xhr.Get_Ready_State = Web.XHR.Requests.DONE then
    WASM.Console.Log (xhr.Get_Response_Text);
  end if;
end Handle_Event;

procedure Initialize_Example is
begin
  xhr := Web.XHR.Requests.Constructors.New_XML_Http_Request;
  xhr.Open ("GET", "https://httpbin.org/anything");
  xhr.Send ("");
  xhr.Add_Event_Listener ("readystatechange", L'Access);
end Initialize_Example;
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/ada/blob/ab7150f3e05aae7d61a195fc7d59cd57e2fbed79/browser/example.adb#L30)

</td>
<td></td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/ada/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/ada)

</td>
<td>

Browser

</td>
<td>

Manual JS `XMLHttpRequest` interop by using the
[wrapper](https://github.com/godunko/adawebpack/blob/22.1.0/source/xhr/web-xhr-requests.adb#L300)
for [imported](https://github.com/godunko/adawebpack/blob/22.1.0/source/xhr/web-xhr-requests.adb#L321)
JS-side [code](https://github.com/godunko/adawebpack/blob/22.1.0/source/adawebpack.mjs#L613).

</td>
</tr>
</table>

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

<a id="basic"></a>
### BASIC

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[EndBASIC](https://github.com/endbasic/endbasic)

</td>
<td>

```basic
DIM res AS STRING
' Custom function
res = HTTPGET("https://httpbin.org/anything")
PRINT res 
```

</td>
<td>

[Example for `LOGIN` command](https://github.com/endbasic/endbasic/blob/endbasic-0.10.0/client/src/cloud.rs#L178)

</td>
<td>

[Some info](https://github.com/endbasic/endbasic/blob/endbasic-0.10.0/core/examples/dsl.rs#L158)

</td>
<td>

[Playground](https://repl.endbasic.dev/)

<sub>Type ` LOGIN "usr","pwd" ` there, and it will invoke a POST request</sub>

</td>
<td>

Browser

</td>
<td>

[Using](https://github.com/endbasic/endbasic/blob/endbasic-0.10.0/client/src/cloud.rs#L92) [reqwest](#reqwest) for API calls in REPL

</td>
</tr>
<tr>
<td>

[gobasic](https://github.com/skx/gobasic)

</td>
<td>

```basic
REM Custom function
res$ = HTTPGET ("https://httpbin.org/anything")
PRINT res$
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/main.go#L16)

</td>
<td>

[Readme](https://github.com/skx/gobasic/tree/release-2.2#70-print-embedding)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/basic-in-go/gobasic/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/basic-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/README.md#test-with-deno).

</td>
<td>

[Uses](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/main.go#L28)
Golang's [`"net/http"`](#go-net-http) in
a [custom function](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/main.go#L26)
[injected](https://github.com/wasm-outbound-http-examples/basic-in-go/blob/f5bd5ea140ae7567047fb6fae2a867ba05fe2d4b/browser-and-deno-gobasic/main.go#L37)
into the language.

</td>
</tr>
</table>

### Berry

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Berry](https://github.com/berry-lang/berry)

</td>
<td>

```berry
# custom function
print(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/berry/blob/4e6f6ecd2cfca5fbbd9b7f8539b69540aaf04a29/browser-sync-xhr/main.c#L44)

</td>
<td>

* [Doc](https://github.com/berry-lang/berry_doc/blob/0e3c2938e04b1ba154cf70026bb344ce4643ed4e/docs/source/en/Chapter-9.rst#use-native-function)
* [Doc](https://github.com/berry-lang/berry_doc/blob/0e3c2938e04b1ba154cf70026bb344ce4643ed4e/docs/source/en/FFI-Example.rst#making-a-native-function)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/berry/sync-xhr/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/berry)

</td>
<td>Browser</td>
<td>

JS `XMLHttpRequest` interop by [invoking](https://github.com/wasm-outbound-http-examples/berry/blob/4e6f6ecd2cfca5fbbd9b7f8539b69540aaf04a29/browser-sync-xhr/main.c#L20) [`emscripten_fetch()`](#emscripten_fetch)
from a custom [host function](https://github.com/wasm-outbound-http-examples/berry/blob/4e6f6ecd2cfca5fbbd9b7f8539b69540aaf04a29/browser-sync-xhr/main.c#L8)
[injected](https://github.com/wasm-outbound-http-examples/berry/blob/4e6f6ecd2cfca5fbbd9b7f8539b69540aaf04a29/browser-sync-xhr/main.c#L43) as native function into Berry.

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

[OpenSilver](https://github.com/OpenSilver/OpenSilver)

<sub>Silverlight / WPF revived in WASM form</sub>

</td>
<td>

```csharp
using System;
using System.Net.Http;

HttpClient client = new HttpClient();
string uri = "https://httpbin.org/anything";
string responseText = await client.GetStringAsync(uri);

Console.WriteLine("text: " + responseText);
```

</td>
<td>

* [Example](https://github.com/OpenSilver/OpenSilver.Samples.Showcase/blob/368fef402c6f8eb6a4a05797fcae14ab798f7e92/src/Samples/Client_Server/REST_WebClient/REST_WebClient_Demo.xaml.cs#L42)
* [Example for POST](https://github.com/OpenSilver/OpenSilver.Samples.Showcase/blob/368fef402c6f8eb6a4a05797fcae14ab798f7e92/src/Samples/Client_Server/REST_WebClient/REST_WebClient_Demo.xaml.cs#L96)

</td>
<td>

[Doc](https://github.com/OpenSilver/OpenSilver.Documentation/blob/d9b2baece1c540c41ba69db71d311de11cfee5e0/documentation/in-depth-topics/wcf-and-webclient.md)

</td>
<td>

[Demo](https://opensilvershowcase.azurewebsites.net/#/Client_Server)

</td>
<td>

Browser

</td>
<td>

* Recommended: just directly invoke .NET's [`"Http.HttpClient"`](#dotnet-system-net-http-httpclient).
* In [`OpenSilver.Compatibility.WebClient` wrapper](https://github.com/OpenSilver/OpenSilver/blob/OpenSilver-2.2.0/src/Runtime/Runtime/System.Net/WebClient.cs#L39): 
[JS `XMLHttpRequest` interop](https://github.com/OpenSilver/OpenSilver/blob/OpenSilver-2.2.0/src/Runtime/Runtime/Core/WebRequestHelper/INTERNAL_WebRequestHelper_JSOnly.cs#L350).

</td>
</tr>
<tr>
<td>

[RestSharp](https://github.com/restsharp/RestSharp)

</td>
<td>

```csharp
using System;
using RestSharp;

var client = new RestClient();
var req = new RestRequest("http://httpbin.org/anything");
var res = await client.ExecuteGetAsync(req);

Console.WriteLine("text: " + res.Content);
```

</td>
<td>

* [Example](https://github.com/wasm-outbound-http-examples/dotnet/blob/f8587fdf9340925e1c829ec7aec31af3fcd7dd02/browser-and-node-RestSharp/Program.cs#L10)
* [Test](https://github.com/restsharp/RestSharp/blob/112.1.0/test/RestSharp.Tests/Auth/AuthenticatorTests.cs#L18)

</td>
<td>

[Doc](https://github.com/restsharp/RestSharp/blob/112.1.0/docs/docs/usage/request.md)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dotnet/restsharp/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dotnet)

</td>
<td>

Browser,
[Node](https://github.com/wasm-outbound-http-examples/dotnet/blob/f8587fdf9340925e1c829ec7aec31af3fcd7dd02/browser-and-node-RestSharp/node/README.md#test-with-nodejs),
[Bun](https://github.com/wasm-outbound-http-examples/dotnet/blob/f8587fdf9340925e1c829ec7aec31af3fcd7dd02/browser-and-node-RestSharp/node/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/dotnet/blob/f8587fdf9340925e1c829ec7aec31af3fcd7dd02/browser-and-node-RestSharp/node/README.md#test-with-deno).

</td>
<td>

[wrapper](https://github.com/restsharp/RestSharp/blob/112.1.0/README.md?plain=1#L5) [around](https://github.com/restsharp/RestSharp/blob/112.1.0/src/RestSharp/RestClient.cs#L48)
.NET's [`"Http.HttpClient"`](#dotnet-system-net-http-httpclient).

</td>
</tr>
<tr>
<td>
<a id="dotnet-system-net-http-httpclient"></a>

[System.Net. Http.HttpClient](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httpclient)

<sub>Standard library</sub>

</td>
<td>

```csharp
using System;
using System.Net.Http;

HttpClient client = new HttpClient();
string uri = "https://httpbin.org/anything";
string responseText = await client.GetStringAsync(uri);

Console.WriteLine("body: " + responseText);
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/dotnet/blob/397d898b51e4396b32b3f2eb568eed140603d636/browser-and-node/Program.cs#L6)

</td>
<td>

* [Doc](https://learn.microsoft.com/en-us/dotnet/api/system.net.http.httpclient)
* [Doc](https://github.com/dotnet/runtime/blob/v9.0.2/src/mono/wasm/features.md#fetch---http-client)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dotnet)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dotnet)

</td>
<td>

Browser, 
[Node](https://learn.microsoft.com/en-us/aspnet/core/client-side/dotnet-interop?view=aspnetcore-9.0#nodejs-console-app), 
[Bun](https://github.com/wasm-outbound-http-examples/dotnet/blob/main/browser-and-node/node/README.md#test-with-bun), 
and [Deno](https://github.com/wasm-outbound-http-examples/dotnet/blob/main/browser-and-node/node/README.md#test-with-deno).

</td>
<td>

[JS `fetch` interop](https://github.com/dotnet/runtime/blob/v9.0.2/src/mono/browser/runtime/loader/polyfills.ts#L122)
<sub>([for Node](https://github.com/dotnet/runtime/blob/v9.0.2/src/mono/browser/runtime/loader/polyfills.ts#L97))</sub>
from [managed code](https://github.com/dotnet/runtime/blob/v9.0.2/src/libraries/System.Net.Http/src/System/Net/Http/BrowserHttpHandler/BrowserHttpHandler.cs#L275)
by [importing](https://github.com/dotnet/runtime/blob/v9.0.2/src/libraries/System.Net.Http/src/System/Net/Http/BrowserHttpHandler/BrowserHttpInterop.cs#L71)
a TS [wrapper](https://github.com/dotnet/runtime/blob/v8.0.0-rc.2.23479.6/src/mono/wasm/runtime/http.ts#L70).

</td>
</tr>
<tr>
<td>
<a id="uno-platform"></a>

[Uno Platform](https://platform.uno/)

</td>
<td>

```csharp
using System;
using System.Net.Http;

HttpClient client = new HttpClient();
string uri = "https://httpbin.org/anything";
string txt = await client.GetStringAsync(uri);

Console.WriteLine("text: " + txt);
```

</td>
<td>

[Example](https://github.com/unoplatform/Uno.Samples/blob/master/UI/TheCatApiClient/TheCatApiClient/TheCatApiClient.Shared/WebServices/WebApiBase.cs#L46)

</td>
<td>

[Tutorial](https://platform.uno/docs/articles/howto-consume-webservices.html)

</td>
<td>



</td>
<td>Browser</td>
<td>

[Using](https://github.com/unoplatform/Uno.Samples/blob/master/UI/TheCatApiClient/TheCatApiClient/TheCatApiClient.Shared/WebServices/WebApiBase.cs#L24)
.NET's [`"Http.HttpClient"`](#dotnet-system-net-http-httpclient).

</td>
</tr>
</table>

<a id="cpp"></a>
### C / C++

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>
<a id="emscripten_fetch"></a>

[Emscripten](https://github.com/emscripten-core/emscripten)

</td>
<td>

```c
#include <emscripten/fetch.h>

void requestOnSuccess(emscripten_fetch_t *fetch)
{
    char dat[fetch->numBytes + 1];
    memcpy(dat, fetch->data, fetch->numBytes);
    dat[fetch->numBytes] = '\0';
    printf("data: %s \n", dat);
    emscripten_fetch_close(fetch);
}

emscripten_fetch_attr_t attr;
emscripten_fetch_attr_init(&attr);
strcpy(attr.requestMethod, "GET");
attr.attributes = EMSCRIPTEN_FETCH_LOAD_TO_MEMORY;
attr.onsuccess = requestOnSuccess;
emscripten_fetch(&attr, "https://httpbin.org/anything");
```

</td>
<td>

* [Example with callbacks](https://github.com/wasm-outbound-http-examples/emscripten/blob/0f0730aa9d3087bb6ec6c930970ac2556cad0114/browser-callbacks/main.c#L28)
* [Example for sync XHR](https://github.com/wasm-outbound-http-examples/emscripten/blob/0f0730aa9d3087bb6ec6c930970ac2556cad0114/browser-sync-xhr/main.c#L11)

</td>
<td>

[Doc](https://emscripten.org/docs/api_reference/fetch.html#introduction)

</td>
<td>

* [Demo for callbacks](https://wasm-outbound-http-examples.github.io/emscripten/callbacks/)
* [Demo for sync XHR](https://wasm-outbound-http-examples.github.io/emscripten/sync-xhr/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/emscripten)

</td>
<td>

Browser

</td>
<td>

[JS `XMLHttpRequest` interop](https://github.com/emscripten-core/emscripten/blob/3.1.61/src/Fetch.js#L437) 
[mapped](https://github.com/emscripten-core/emscripten/blob/3.1.61/src/library_fetch.js#L26) to be 
[used](https://github.com/emscripten-core/emscripten/blob/3.1.61/system/lib/fetch/emscripten_fetch.c#L145) in
[`emscripten_fetch()`](https://github.com/emscripten-core/emscripten/blob/3.1.61/system/lib/fetch/emscripten_fetch.c#L70).

</td>
</tr>
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

### Dart

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[package:dio](https://pub.dev/packages/dio)

</td>
<td>

```dart
import 'package:dio/dio.dart';

final dio = Dio();
Response response = await dio.get(
  'https://httpbin.org/anything');
print(response);
```

</td>
<td>

* [Example](https://github.com/cfug/dio/blob/dio_v5.7.0/dio/example/dio.dart#L6)
* [Example](https://github.com/cfug/dio/blob/dio_v5.7.0/example_dart/lib/dio.dart#L41)
* [Example](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-package-dio/web/main.dart#L5)

</td>
<td>

[Readme](https://github.com/cfug/dio/blob/dio_v5.7.0/dio/README.md#examples)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-dio/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc]

</td>
<td>

JS `XMLHttpRequest` [interop](https://github.com/cfug/dio/blob/dio_v5.7.0/plugins/web_adapter/lib/src/adapter.dart#L290)
inside [`BrowserHttpClientAdapter`](https://github.com/cfug/dio/blob/dio_v5.7.0/plugins/web_adapter/lib/src/adapter.dart#L13-L14) class.

</td>
</tr>
<tr>
<td>
<a id="dart-package-fetch-api"></a>

[package:fetch_api](https://pub.dev/packages/fetch_api)

</td>
<td>

```dart
import 'package:fetch_api/fetch_api.dart';

final resp = await fetch(
  'https://httpbin.org/anything');
final txt = await resp.text();
print('${txt}');
```

</td>
<td>

* [Example](https://github.com/Zekfad/fetch_api/blob/2.2.0/example/fetch_api_example.dart#L6)
* [Example using `Request`](https://github.com/Zekfad/fetch_api/blob/2.2.0/example/fetch_api_request.dart#L16)
* [Example](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-api/web/main.dart#L4)

</td>
<td>

[Some doc](https://github.com/Zekfad/fetch_api/blob/2.2.0/README.md#some-notes-about-fetch-and-request)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-fetch-api/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc],
[Node.js](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-api/README.md#test-with-nodejs),
and [Deno](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-api/README.md#test-with-deno).

</td>
<td>

JS `fetch` [interop](https://github.com/Zekfad/fetch_api/blob/2.2.0/lib/src/fetch.dart#L31)
using [imported by `@JS`](https://github.com/Zekfad/fetch_api/blob/2.2.0/lib/src/fetch.dart#L7) function.

</td>
</tr>
<tr>
<td>

[package:fetch_client](https://pub.dev/packages/fetch_client)

</td>
<td>

```dart
import 'package:fetch_client/fetch_client.dart';

final client = FetchClient(
  mode: RequestMode.cors);
final uri = Uri.parse(
  'https://httpbin.org/anything');
final resp = await client.get(uri);

print('${resp.body}');
client.close();
```

</td>
<td>

* [Example](https://github.com/Zekfad/fetch_client/blob/1.1.2/example/fetch_client_example.dart#L10)
* [Example](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-client/web/main.dart#L6)

</td>
<td>

[Some doc](https://github.com/Zekfad/fetch_client/blob/1.1.2/README.md#notes)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-fetch-client/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc],
[Node.js](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-client/README.md#test-with-nodejs),
and [Deno](https://github.com/wasm-outbound-http-examples/dart/blob/3ff1759caa2a67de6cd1c37b5abab13e0edecbe5/browser-and-node-package-fetch-client/README.md#test-with-deno).

</td>
<td>

[Extends](https://github.com/Zekfad/fetch_client/blob/1.1.2/lib/src/fetch_client.dart#L31) the 
[`BaseClient`](https://github.com/dart-lang/http/blob/http-v1.2.1/pkgs/http/lib/src/base_client.dart#L20)
by [using](https://github.com/Zekfad/fetch_client/blob/1.1.2/lib/src/fetch_client.dart#L142)
[imported](https://github.com/Zekfad/fetch_client/blob/1.1.2/lib/src/fetch_client.dart#L5)
[package:fetch_api](#dart-package-fetch-api).

</td>
</tr>
<tr>
<td>
<a id="dart-package-http"></a>

[package:http](https://pub.dev/packages/http)

</td>
<td>

```dart
import 'package:http/http.dart' as http;

final resp = await http.get(
  Uri.parse('https://httpbin.org/anything'));
print('${resp.body}');
```

</td>
<td>

* [Example](https://github.com/dart-lang/http/blob/http-v1.2.1/pkgs/http/example/main.dart#L12)
* [Example](https://github.com/dart-lang/site-www/blob/9bf986bc133ab07d216cba8d84a5072276d2f262/src/content/tutorials/server/fetch-data.md?plain=1#L276)
* [Example](https://github.com/wasm-outbound-http-examples/dart/blob/50a6e363e099f4e2e4c28cd459e1815e1805bf24/browser-package-http/web/main.dart#L4)

</td>
<td>

[Doc](https://dart.dev/tutorials/server/fetch-data)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-http/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)
* [Playground](https://dart.dev/#try-dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc]

</td>
<td>

JS `XMLHttpRequest` [interop](https://github.com/dart-lang/http/blob/http-v1.2.1/pkgs/http/lib/src/browser_client.dart#L101)
inside [`BrowserClient`](https://github.com/dart-lang/http/blob/http-v1.2.1/pkgs/http/lib/src/browser_client.dart#L29-L37) class.

</td>
</tr>
<tr>
<td>

[package:requests](https://github.com/jossef/requests)

</td>
<td>

```dart
import 'package:requests/requests.dart';

final resp = await Requests.get(
  'https://httpbin.org/anything');
print('body: ${resp.content()}');
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/dart/blob/1d3d0a789b5518aa00a11dfa508caa040541cc21/browser-package-requests/web/main.dart#L4)

</td>
<td>

[Readme](https://github.com/jossef/requests/tree/5.0.0#usage)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-requests/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc]

</td>
<td>

[Wrapper](https://github.com/jossef/requests/blob/5.0.0/lib/src/client/io_client.dart#L11) over [package:http](#dart-package-http).

</td>
</tr>
<tr>
<td>

[package:web](https://pub.dev/packages/web)

</td>
<td>

```dart
import 'package:web/web.dart' as web;

final resp = await web.window.fetch(
  'https://httpbin.org/anything'.toJS).toDart;
final txt = await resp.text().toDart;
print('${txt}');
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/dart/blob/50a6e363e099f4e2e4c28cd459e1815e1805bf24/browser-package-web/web/main.dart#L6)

</td>
<td>

[Doc](https://dart.dev/interop/js-interop/package-web)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/package-web/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)
* [Playground](https://dart.dev/#try-dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc]

</td>
<td>

Direct `fetch` interop with [help](https://github.com/dart-lang/sdk/blob/3.4.0/sdk/lib/js_interop/js_interop.dart#L556)
of [some extension types](https://github.com/dart-lang/web/blob/v0.5.1/lib/src/dom/fetch.dart#L385).

</td>
</tr>
<tr>
<td>

[dart:js_interop](https://dart.dev/interop/js-interop)

</td>
<td>

```dart
import 'dart:js_interop';

@JS()
external JSPromise<Response> fetch(JSString _);

extension type Response(JSObject _)
 implements JSObject {
  @JS()
  external JSPromise<JSString> text();
}

final Response resp = await fetch(
  'https://httpbin.org/anything'.toJS).toDart;
final txt = await resp.text().toDart;
print('body: ${txt}');
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/web/main.dart#L12)

</td>
<td>

[Doc](https://dart.dev/interop/js-interop/usage#interop-types)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/dart/js-interop-extension-type-fetch/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/dart)

</td>
<td>

Browser with Wasm-GC support enabled[^browser-with-wasm-gc],
[Node.js](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/README.md#test-with-nodejs),
[Bun](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/README.md#test-with-deno).

</td>
<td>

Direct JS `fetch` interop by [importing](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/web/main.dart#L3-L4) it
and [wrapping](https://github.com/wasm-outbound-http-examples/dart/blob/0265d9e11d2268ca1ac560027704f558df2dedd9/browser-and-node-js_interop-extension_type-fetch/web/main.dart#L6-L9) its promise
with an extension type.

</td>
</tr>
<tr>
<td>

[SDK for writing Cloudflare Workers in Dart aka cf_workers.dart](https://github.com/a-skua/cf_workers.dart)

</td>
<td>

```dart
import 'package:http/http.dart';
import 'package:cf_workers/cf_workers.dart';
import 'package:cf_workers/http.dart';

Future<void> main() {
  return Workers((JSRequest req) async {
    return fetch(Request('GET', Uri.parse(
      'https://httpbin.org/anything')).toJS);
  }).serve();
}
```

</td>
<td>

[Example](https://github.com/a-skua/cf_workers.dart/blob/1.0.0-rc.2/example/example.dart#L9)

</td>
<td>

[Readme](https://github.com/a-skua/cf_workers.dart/blob/1.0.0-rc.2/README.md#usage)

</td>
<td>

* [Dev Container](https://github.com/codespaces/new/wasm-outbound-http-examples/dart?devcontainer_path=.devcontainer%2Fcf-workers%2Fdevcontainer.json)

</td>
<td>

[workerd, Cloudflare's JavaScript/ Wasm Runtime](https://github.com/cloudflare/workerd)

</td>
<td>

JS `fetch` interop [using](https://github.com/a-skua/cf_workers.dart/blob/1.0.0-rc.2/lib/src/http/extern.dart#L8) the `fetch()`
[imported](https://github.com/a-skua/cf_workers.dart/blob/1.0.0-rc.2/lib/src/http/extern.dart#L4-L5) from CF Workers runtime.

</td>
</tr>
</table>

<a id="expression"></a>
### Expression evaluation languages

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Cel-go](https://github.com/google/cel-go)

<sub>Common Expression Language</sub>

</td>
<td>

```js
// two custom functions
println(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/cel-go/blob/03d6888a314f21714423a7174c538b04077e436e/browser-and-deno/main.go#L59)

</td>
<td>

[Doc](https://github.com/google/cel-go/blob/v0.23.2/examples/README.md#define-custom-global-function)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/cel-go/cel/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/cel-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/cel-go/blob/03d6888a314f21714423a7174c538b04077e436e/browser-and-deno/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/cel-go/blob/03d6888a314f21714423a7174c538b04077e436e/browser-and-deno/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/cel-go/blob/03d6888a314f21714423a7174c538b04077e436e/browser-and-deno/main.go#L25)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/cel-go/blob/03d6888a314f21714423a7174c538b04077e436e/browser-and-deno/main.go#L18)
a custom function into Cel-go.

</td>
</tr>
<tr>
<td>

[Expr](https://github.com/expr-lang/expr)

</td>
<td>

```js
// two custom functions
println(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/expr-lang/blob/917f83ab18c1a36cc8b3612569bd755d2aa4086b/browser-and-deno/main.go#L25)

</td>
<td>

[Doc](https://github.com/expr-lang/expr/blob/v1.16.9/docs/functions.md#functions)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/expr-lang/expr/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/expr-lang)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/expr-lang/tree/917f83ab18c1a36cc8b3612569bd755d2aa4086b/browser-and-deno#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/expr-lang/tree/917f83ab18c1a36cc8b3612569bd755d2aa4086b/browser-and-deno#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/expr-lang/blob/917f83ab18c1a36cc8b3612569bd755d2aa4086b/browser-and-deno/main.go#L14)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/expr-lang/blob/917f83ab18c1a36cc8b3612569bd755d2aa4086b/browser-and-deno/main.go#L13)
a custom function into Expr-lang.

</td>
</tr>
</table>

### Forth

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[WAForth](https://github.com/remko/waforth)

</td>
<td>

```forth
: URL$  S" https://httpbin.org/anything" ;
( custom word )
URL$ HTTPGET
```

</td>
<td>

* [Example](https://github.com/remko/waforth/blob/v0.20.1/src/web/examples/fetch/fetch.ts#L45)
* [Example](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/index.html#L55)
* [Example for NodeJS](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/httpget.mjs#L33)

</td>
<td>

[Readme](https://github.com/remko/waforth/tree/v0.20.1?#asynchronous-bindings)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/waforth/bindAsync/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/waforth)

</td>
<td>

Browser,
[NodeJS](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/README.md#test-with-nodejs),
[Bun](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/README.md#test-with-deno).

</td>
<td>

JS [`fetch` interop](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/index.html#L35) by
[invoking](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/index.html#L51)
a custom host function, 
[bound](https://github.com/wasm-outbound-http-examples/waforth/blob/4865721a5bf826c5644af092fe841d19f93b1d8e/browser-and-node/index.html#L32)
info Forth's dictionary/namespace.

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
<tr>
<td>

[Hogosuru](https://github.com/realPy/hogosuru)

<sub>SPA framework</sub>

</td>
<td>

```go
import (
"github.com/realPy/hogosuru"
"github.com/realPy/hogosuru/base/fetch"
"github.com/realPy/hogosuru/base/promise"
"github.com/realPy/hogosuru/base/response"
)

f, err := fetch.New("https://httpbin.org/anything", nil)
f.Then(func(r response.Response) *promise.Promise {
  txtpromise, _ := f.Then(
    func(r response.Response) *promise.Promise {
      if prm, err := r.Text(); hogosuru.AssertErr(err) {
        return &prm
      }
      return nil
    }, nil)

  txtpromise.Then(func(i interface{}) *promise.Promise {
    fmt.Println(i.(string))
    return nil
  }, nil)
return nil
}, nil)
```

</td>
<td>

* [Example](https://github.com/realPy/learn-hogosuru/blob/08bf39e0f7e2139445b4a09a8263682d703f9034/jsonfetch/main.go#L20)
* [Example for POST](https://github.com/realPy/learn-hogosuru/blob/08bf39e0f7e2139445b4a09a8263682d703f9034/iofetch/front/main.go#L27)
* [Example for Example for XHR and POST](https://github.com/realPy/learn-hogosuru/blob/08bf39e0f7e2139445b4a09a8263682d703f9034/ioxmlhttprequest/front/main.go#L39)
* [Example](https://github.com/wasm-outbound-http-examples/go/blob/6b024c87340895fb8e7e45d2ff41b09834286b6a/browser-hogosuru/main.go#L44)

</td>
<td>

* [Doc](https://hogosuru.v-ip.fr/guides/load-and-parse-a-json-data#example-with-a-json-file)
* [Doc](https://hogosuru.v-ip.fr/guides/network-io-an-example-with-gofiber#fetch)
* [Doc for XHR](https://hogosuru.v-ip.fr/guides/network-io-an-example-with-gofiber#xmlhttprequest)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/go/hogosuru/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

Browser

</td>
<td>

Manual low-level JS `fetch` and `XMLHttpRequest` interop using [Go wrappers for Web API](https://github.com/realPy/hogosuru/tree/v1.5.1#how-it-work):
[`fetch`](https://github.com/realPy/hogosuru/blob/v1.5.1/base/fetch/fetch.go#L30),
[`XHR`](https://github.com/realPy/hogosuru/blob/v1.5.1/base/xmlhttprequest/xmlhttprequest.go#L43).

</td>
</tr>
<tr>
<td>

[Vecty](https://github.com/hexops/vecty)

<sub>UI library</sub>

</td>
<td>

```go
import "io"
import "log"
import "net/http"

go func() {
  resp, _ := http.Get(action.Url)
  defer resp.Body.Close()
  body, _ := io.ReadAll(resp.Body)
  log.Println(string(body))
}()
```

</td>
<td>

* [Example](https://github.com/soypat/vecty-examples/blob/24a203ddc5116c32ee23389c0682924b3cef647a/basic-material-ui/views/components.go#L61)
* [Example](https://github.com/wasm-outbound-http-examples/go/blob/f151a9ca1234ce3ba70997766c8ccc80f097f7cd/browser-vecty/views/body.go#L62)

</td>
<td>

* [Use `go func()`](https://withblue.ink/2020/10/03/go-webassembly-http-requests-and-promises.html#making-http-requests-from-go-code)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/go/vecty/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

Browser

</td>
<td>

Has no built-in solutions, just directly [invoking](https://github.com/wasm-outbound-http-examples/go/blob/f151a9ca1234ce3ba70997766c8ccc80f097f7cd/browser-vecty/store/store.go#L36)
Golang's [`"net/http"`](#go-net-http)

</td>
</tr>
<tr>
<td>

[Vugu](https://github.com/vugu/vugu)

<sub>UI library</sub>

</td>
<td>

```go
import "io"
import "log"
import "net/http"

resp, _ := http.Get("https://httpbin.org/anything")
defer resp.Body.Close()
body, _ := io.ReadAll(resp.Body)
log.Println(string(body))
```

</td>
<td>

[Example](https://github.com/vugu/vugu/blob/v0.3.5/examples/fetch-and-display/root.vugu#L41)

</td>
<td></td>
<td>

Possible with
[Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

Browser

</td>
<td>

Has no built-in solutions, just directly invoking Golang's [`"net/http"`](#go-net-http)

</td>
</tr>
<tr>
<td>

[Yaegi](https://github.com/traefik/yaegi)

<sub>It's VM / interpreter</sub>

</td>
<td>

```go
import (
  "fmt"; "io"; "net/http"
)

resp, _ := http.Get("https://httpbin.org/anything")
defer resp.Body.Close()
body, _ := io.ReadAll(resp.Body)
fmt.Println(string(body))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/yaegi/blob/deecf7e8840e5c5b7e15921aec4c2c29d03838e6/browser-and-deno/main.go#L21)

</td>
<td>

[Some doc](https://github.com/traefik/yaegi/tree/v0.15.1#usage)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/yaegi/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/yaegi)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/yaegi/blob/deecf7e8840e5c5b7e15921aec4c2c29d03838e6/browser-and-deno/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/yaegi/blob/deecf7e8840e5c5b7e15921aec4c2c29d03838e6/browser-and-deno/README.md#test-with-deno).

</td>
<td>

Directly invoking 
Golang's [`"net/http"`](#go-net-http) via
[mapping](https://github.com/traefik/yaegi/blob/v0.15.1/stdlib/go1_20_net_http.go#L54).

</td>
</tr>
</table>

#### Golang-like languages

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Anko](https://github.com/mattn/anko)

</td>
<td>

```js
var http = import("net/http")
var ioutil = import("io/ioutil")

var url = "https://httpbin.org/anything"
res, _ = http.DefaultClient.Get(url)
b, _ = ioutil.ReadAll(res.Body)
println(toString(b))
res.Body.Close()
```

</td>
<td>

* [Example](https://github.com/mattn/anko/blob/v0.1.9/_example/scripts/http.ank#L5)
* [Test](https://github.com/mattn/anko/blob/v0.1.9/vm/example_packages_test.go#L109)
* [Example](https://github.com/wasm-outbound-http-examples/anko/blob/aa01ffaad3153254ae2abbf432b16b33b315574e/browser/main.go#L18)

</td>
<td></td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/anko/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/anko)

</td>
<td>Browser and maybe Node</td>
<td>

Directly invoking
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/mattn/anko/blob/v0.1.9/packages/net.http.go#L14).

</td>
</tr>
<tr>
<td>

[Risor](https://github.com/risor-io/risor)

</td>
<td>

```go
url := "https://httpbin.org/anything"
resp := fetch(url)
print(resp.text())
```

</td>
<td>

* [Example](https://github.com/risor-io/risor/blob/v1.1.1/examples/scripts/stargazers.risor#L6)
* [Example](https://github.com/wasm-outbound-http-examples/risor/blob/0e6a935c8124bf11fd100bea600dd0eb4ed7cd37/browser/main.go#L13)

</td>
<td>

[Doc](https://risor.io/examples/fetch)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/risor/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/risor)

</td>
<td>Browser and maybe Node</td>
<td>

[Using](https://github.com/risor-io/risor/blob/v1.1.1/modules/fetch/fetch.go#L46)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/risor-io/risor/blob/v1.1.1/modules/fetch/fetch.go#L58).

</td>
</tr>
<tr>
<td>

[TengoHTTP](https://github.com/damiva/TengoHTTP) 

<sub>for [Tengo](https://github.com/d5/tengo)</sub>

</td>
<td>

```go
fmt := import("fmt")
http := import("httpclient")

resp := http.request("https://httpbin.org/anything", "GET")
fmt.print(is_error(resp) ? resp : resp.body)
```

</td>
<td>

* [Example](https://github.com/damiva/TengoHTTP/blob/v0.5.0/README.md?plain=1#L31)
* [Example](https://github.com/wasm-outbound-http-examples/tengo/blob/964f7a4d17449e3fccd7a908314513d932b10514/browser-and-deno-tengohttp/main.go#L15)

</td>
<td>

[Readme](https://github.com/damiva/TengoHTTP/tree/v0.5.0#functions)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/tengo/tengohttp/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/tengo)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/tengo/tree/964f7a4d17449e3fccd7a908314513d932b10514/browser-and-deno-tengohttp#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/tengo/tree/964f7a4d17449e3fccd7a908314513d932b10514/browser-and-deno-tengohttp#test-with-deno).

</td>
<td>

[Using](https://github.com/damiva/TengoHTTP/blob/v0.5.0/request.go#L100) 
Golang's [`"net/http"`](#go-net-http) via 
[mapping](https://github.com/wasm-outbound-http-examples/tengo/blob/964f7a4d17449e3fccd7a908314513d932b10514/browser-and-deno-tengohttp/main.go#L25-L26).

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

### JavaScript

#### Using browser's own JavaScript VM

_Possible, but why?_

##### Libraries to use from JavaScript

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[libcurl.js](https://github.com/ading2210/libcurl.js)

<sub>Requires server-side counterpart</sub>

</td>
<td>

```js
libcurl.set_websocket(
  'wss://your-wisp-proxy.yoursite.tld/');
let res = await libcurl.fetch(
  'https://httpbin.org/anything');
console.log(await res.text());
```

</td>
<td>

* [WebWorker Example](https://github.com/ading2210/libcurl.js/blob/4d64b27a8293de87d7e39b30685ca17ee9c324a3/client/worker.html#L10)
* [Example](https://github.com/wasm-outbound-http-examples/libcurl-js/blob/261b08b14c3373900f3fb05e43f56c5cce78d9f7/index.html#L13)
* [Test for POST](https://github.com/ading2210/libcurl.js/blob/4d64b27a8293de87d7e39b30685ca17ee9c324a3/client/tests/scripts/test_post.js#L3)

</td>
<td>

[Doc](https://github.com/ading2210/libcurl.js/blob/4d64b27a8293de87d7e39b30685ca17ee9c324a3/README.md#making-http-requests)

</td>
<td>

* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/libcurl-js)

</td>
<td>Browser</td>
<td>

[Tunneling](https://github.com/ading2210/libcurl.js/blob/4d64b27a8293de87d7e39b30685ca17ee9c324a3/client/javascript/http.js#L86) TCP to WebSocket using protocols "wisp" or "wsproxy" .

</td>
</tr>
</table>

#### JavaScript VM or interpreter compiled to WASM

##### JavaScript built with Emscripten

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>
<a id="quickjs-emscripten"></a>

[quickjs-emscripten](https://github.com/justjake/quickjs-emscripten)

</td>
<td>

```js
// Host function
const txt = await fetch('https://httpbin.org/anything');
console.log(txt);
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/httpget.mjs#L31)

</td>
<td>

[Doc](https://github.com/justjake/quickjs-emscripten?tab=readme-ov-file#exposing-apis)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/quickjs-emscripten/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/quickjs-emscripten)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/README.md#test-with-bun),
[Deno](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/README.md#test-with-deno),
and [Node](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/README.md#test-with-nodejs).

</td>
<td>

JS [`fetch` interop](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/httpget.mjs#L23) by
[injecting](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/httpget.mjs#L28) 
a custom [host function](https://github.com/wasm-outbound-http-examples/quickjs-emscripten/blob/fbf9bb14272a1fa703991cf25e033515d77f3fb5/browser-and-node/httpget.mjs#L19) 
into QuickJS's global namespace.

</td>
</tr>
<tr>
<td>

[sebastianwessel/quickjs]( https://github.com/sebastianwessel/quickjs)

</td>
<td>

```js
const fn = async () => {
 // Host function   
 const res = await fetch(
   'https://httpbin.org/anything');

 return res.text();
}

export default await fn();
```

</td>
<td>

* [Example](https://github.com/sebastianwessel/quickjs/blob/v2.0.1/example/basic/index.ts#L25)
* [Example for browser](https://github.com/wasm-outbound-http-examples/sebastianwessel-quickjs/blob/e05dcb0c5b28b0bcd8fa17604e1877a56db0ac50/browser-and-node/index.html#L18)
* [Example for Node](https://github.com/wasm-outbound-http-examples/sebastianwessel-quickjs/blob/e05dcb0c5b28b0bcd8fa17604e1877a56db0ac50/browser-and-node/httpget.mjs#L13)

</td>
<td>

[Doc](https://github.com/sebastianwessel/quickjs/blob/v2.0.1/website/docs/fetch.md)

</td>
<td>

* [Playground](https://sebastianwessel.github.io/quickjs/playground.html)
* [Demo](https://wasm-outbound-http-examples.github.io/sebastianwessel-quickjs/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/sebastianwessel-quickjs)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/sebastianwessel-quickjs/blob/e05dcb0c5b28b0bcd8fa17604e1877a56db0ac50/browser-and-node/README.md#test-with-bun),
[Deno](https://github.com/wasm-outbound-http-examples/sebastianwessel-quickjs/blob/e05dcb0c5b28b0bcd8fa17604e1877a56db0ac50/browser-and-node/README.md#test-with-deno),
and [Node](https://github.com/wasm-outbound-http-examples/sebastianwessel-quickjs/blob/e05dcb0c5b28b0bcd8fa17604e1877a56db0ac50/browser-and-node/README.md#test-with-nodejs).

</td>
<td>

Wrapper over [quickjs-emscripten](#quickjs-emscripten).
[Uses](https://github.com/sebastianwessel/quickjs/blob/v2.0.1/src/adapter/fetch.ts#L156) host function `fetch()`. 

</td>
</tr>
</table>

##### JavaScript implemented in .NET

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Jint](https://github.com/sebastienros/jint)

</td>
<td>

```js
// custom object
http.get('https://httpbin.org/anything');
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/js-in-dotnet/blob/0ce787266260bda0a3152ffc6826c7b2b16d8ad4/browser-and-node-Jint/Program.cs#L16)

</td>
<td>

[Readme](https://github.com/sebastienros/jint/blob/v4.0.3/README.md#examples)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/js-in-dotnet/Jint/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/js-in-dotnet)

</td>
<td>

Browser

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/js-in-dotnet/blob/0ce787266260bda0a3152ffc6826c7b2b16d8ad4/browser-and-node-Jint/Program.cs#L34)
.NET's [`"Http.HttpClient"`](#dotnet-system-net-http-httpclient) via [mapping](https://github.com/wasm-outbound-http-examples/js-in-dotnet/blob/0ce787266260bda0a3152ffc6826c7b2b16d8ad4/browser-and-node-Jint/Program.cs#L12)
a custom object inside JS.

</td>
</tr>
</table>

##### JavaScript implemented in Golang

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Goja](https://github.com/dop251/goja)

</td>
<td>

```js
const res = httpget('https://httpbin.org/anything');
console.log(res);
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/js-in-go/blob/7ed91aaa8dad2cb322a4dddab8df76a9194dfe8f/browser-and-deno-goja/main.go#L29)

</td>
<td>

[Some doc](https://github.com/dop251/goja/blob/b396bb4c349df65109dea3df00fb60f6a044950d/README.md?plain=1#L288)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/js-in-go/goja/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/js-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/js-in-go/blob/7ed91aaa8dad2cb322a4dddab8df76a9194dfe8f/browser-and-deno-goja/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/js-in-go/blob/7ed91aaa8dad2cb322a4dddab8df76a9194dfe8f/browser-and-deno-goja/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/js-in-go/blob/7ed91aaa8dad2cb322a4dddab8df76a9194dfe8f/browser-and-deno-goja/main.go#L19)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/js-in-go/blob/7ed91aaa8dad2cb322a4dddab8df76a9194dfe8f/browser-and-deno-goja/main.go#L27)
a custom function inside JS.

</td>
</tr>
<tr>
<td>

[gojax/fetch](https://github.com/olebedev/gojax/tree/master/fetch)

</td>
<td>

```js
fetch('https://httpbin.org/anything')
  .then(function(res) {
    return res.text();
  }).then(function(txt) {
    console.log(txt);
    exitloop();
  });
```

</td>
<td>

* [Example](https://github.com/olebedev/gojax/blob/bb153be84336f26925890502929cc363477df7ad/fetch/README.md?plain=1#L37)
* [Test](https://github.com/olebedev/gojax/blob/bb153be84336f26925890502929cc363477df7ad/fetch/fetch_test.go#L82)
* [Example](https://github.com/wasm-outbound-http-examples/js-in-go/blob/e175161fa6639b56fd6b2f59517d56e3d6112222/browser-and-deno-gojax-fetch/main.go#L30)

</td>
<td>

[Readme](https://github.com/olebedev/gojax/blob/bb153be84336f26925890502929cc363477df7ad/fetch/README.md#usage)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/js-in-go/gojax-fetch/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/js-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/js-in-go/blob/e175161fa6639b56fd6b2f59517d56e3d6112222/browser-and-deno-gojax-fetch/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/js-in-go/blob/e175161fa6639b56fd6b2f59517d56e3d6112222/browser-and-deno-gojax-fetch/README.md#test-with-deno).

</td>
<td>

[Injecting](https://github.com/olebedev/gojax/blob/bb153be84336f26925890502929cc363477df7ad/fetch/fetch.go#L33) a custom function into JS.
That func [uses](https://github.com/olebedev/gojax/blob/bb153be84336f26925890502929cc363477df7ad/fetch/fetch.go#L94) the goproxy as HTTP client,
which is a [wrapper](https://github.com/elazarl/goproxy/blob/v1.1/README.md?plain=1#L14) for Golang's [`"net/http"`](#go-net-http).

</td>
</tr>
<tr>
<td>

[Otto](https://github.com/robertkrimen/otto)

</td>
<td>

```js
const res = httpget('https://httpbin.org/anything');
console.log(res);
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/js-in-go/blob/3c6ca09b95a5fd33d02756bd3b6015f0e70793ac/browser-and-deno-otto/main.go#L25)

</td>
<td>

[Some doc](https://github.com/robertkrimen/otto/blob/v0.3.0/README.md?plain=1#L77)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/js-in-go/otto/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/js-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/js-in-go/blob/3c6ca09b95a5fd33d02756bd3b6015f0e70793ac/browser-and-deno-otto/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/js-in-go/blob/3c6ca09b95a5fd33d02756bd3b6015f0e70793ac/browser-and-deno-otto/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/js-in-go/blob/3c6ca09b95a5fd33d02756bd3b6015f0e70793ac/browser-and-deno-otto/main.go#L14)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/js-in-go/blob/3c6ca09b95a5fd33d02756bd3b6015f0e70793ac/browser-and-deno-otto/main.go#L23)
a custom function inside JS.

</td>
</tr>
</table>

### Kotlin
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Kotlin/Wasm](https://kotl.in/wasm)

<sub>still Alpha</sub>

</td>
<td>

```kotlin
import kotlinx.browser.window

window.fetch("https://httpbin.org/anything").then {
  if (it.ok) {
    it.text().then {
      println(it)
      null
    }
  }
  null
}
```

</td>
<td>

* [Example 1](https://github.com/Kotlin/kotlin-wasm-examples/blob/ea1a989bbf179dfccbc970d73e41d128e1b965af/browser-example/src/wasmJsMain/kotlin/Simple.kt#L43)
* [Example 2](https://github.com/wasm-outbound-http-examples/kotlin/blob/893cc8c505839aabbbb2ecdcd69c419b8feb4a5a/browser/src/wasmJsMain/kotlin/Main.kt#L4)
* [Node.js/Deno Example](https://github.com/wasm-outbound-http-examples/kotlin/blob/893cc8c505839aabbbb2ecdcd69c419b8feb4a5a/node-and-deno/src/wasmJsMain/kotlin/Main.kt#L7)

</td>
<td>

[Readme](https://github.com/Kotlin/kotlin-wasm-examples/tree/ea1a989bbf179dfccbc970d73e41d128e1b965af/browser-example#kotlinwasm-browser-example)

</td>
<td>

* [Playground](https://pl.kotl.in/TOU_L89rx)
* [Demo 1](https://zal.im/wasm/example)
* [Demo 2](https://wasm-outbound-http-examples.github.io/kotlin/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/kotlin)

</td>
<td>

Browser with Wasm-GC and Wasm-Exception-Handling support enabled[^browser-with-wasm-gc], Node v21 and above, Deno v1.38 and above.

</td>
<td>

Direct `fetch` interop using [exposed](https://github.com/JetBrains/kotlin/blob/v1.9.21/libraries/stdlib/wasm/js/src/org.w3c/org.w3c.dom.kt#L3080) JS `window` object.
For Node/Deno, just [import](https://github.com/wasm-outbound-http-examples/kotlin/blob/893cc8c505839aabbbb2ecdcd69c419b8feb4a5a/node-and-deno/src/wasmJsMain/kotlin/Main.kt#L4).

</td>
</tr>
</table>

### Lisp

#### Clojure-like languages

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Janet](https://github.com/janet-lang/janet)

</td>
<td>

```janet
# custom function
(print (httpget `https://httpbin.org/anything`))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/janet/blob/8608c9cfe1b2466deb645021e6130c2ca062b65f/browser-sync-xhr/main.c#L38)

</td>
<td>

[Some doc](https://janet-lang.org/capi/writing-c-functions.html)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/janet/sync-xhr/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/janet)

</td>
<td>

Browser and maybe Node

</td>
<td>

JS `XMLHttpRequest` interop by [invoking](https://github.com/wasm-outbound-http-examples/janet/blob/8608c9cfe1b2466deb645021e6130c2ca062b65f/browser-sync-xhr/main.c#L15) `emscripten_fetch()`
from a custom [host function](https://github.com/wasm-outbound-http-examples/janet/blob/8608c9cfe1b2466deb645021e6130c2ca062b65f/browser-sync-xhr/main.c#L6)
[injected](https://github.com/wasm-outbound-http-examples/janet/blob/8608c9cfe1b2466deb645021e6130c2ca062b65f/browser-sync-xhr/main.c#L36) into Janet.

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

* [Demo](https://wasm-outbound-http-examples.github.io/lua-in-go/gluahttp/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/lua-in-go)

</td>
<td>Browser and maybe Node</td>
<td>

[Using](https://github.com/cjoudrey/gluahttp/blob/25003d9adfa90bf4c4609bcebdf2061a5636d532/gluahttp.go#L218)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/cjoudrey/gluahttp/blob/25003d9adfa90bf4c4609bcebdf2061a5636d532/gluahttp.go#L38).

</td>
</tr>
<tr>
<td>

[gopher-lua-libs](https://github.com/vadv/gopher-lua-libs)

</td>
<td>

```lua
local http = require('http')
local client = http.client()
local req = http.request('GET', 
  'https://httpbin.org/anything')
local res, err = client:do_request(req)
print(res.body)
```

</td>
<td>

* [Test](https://github.com/vadv/gopher-lua-libs/blob/v0.5.0/http/client/client_example_test.go#L17)
* [Example](https://github.com/vadv/gopher-lua-libs/blob/v0.5.0/examples/slack-alertmanager-silence-bot/bot.lua#L72)
* [Example](https://github.com/wasm-outbound-http-examples/lua-in-go/blob/edde8a27b0c34d50b89640ba40f64152d94ae8cb/browser-gopher-lua-libs/main.go#L17)

</td>
<td>

[Doc](https://pkg.go.dev/github.com/vadv/gopher-lua-libs/http)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/lua-in-go/gopher-lua-libs/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/lua-in-go)

</td>
<td>Browser and maybe Node</td>
<td>

[Using](https://github.com/vadv/gopher-lua-libs/blob/v0.5.0/http/client/client.go#L67)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/vadv/gopher-lua-libs/blob/v0.5.0/http/client/loader.go#L23).

</td>
</tr>
<tr>
<td>

[erdian718/lmodhttpclient](https://github.com/erdian718/lmodhttpclient) 
<sub>aka ofunc/lmodhttpclient</sub>

</td>
<td>

```lua
local io = require('io')
local httpclient = require('http/client')

local res = httpclient.get(
  'https://httpbin.org/anything')
io.copy(res, io.stdout)
res:close()
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/lua-in-go/blob/af18668722420a3547f9554e8ee2c408afda2617/browser-lmodhttpclient/main.go#L19)

</td>
<td>

[Readme](https://github.com/erdian718/lmodhttpclient/tree/master#usage)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/lua-in-go/lmodhttpclient/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/lua-in-go)

</td>
<td>Browser and maybe Node</td>
<td>

[Using](https://github.com/erdian718/lmodhttpclient/blob/d87d685c200b19b4e1c3753146d064288dbe112b/mod.go#L72)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/erdian718/lmodhttpclient/blob/d87d685c200b19b4e1c3753146d064288dbe112b/mod.go#L47-L48).

</td>
</tr>
</table>

#### Lua dialects

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Pluto](https://github.com/PlutoLang/Pluto)

</td>
<td>

```lua
local http = require 'pluto:http'

http.request('https://httpbin.org/anything')
|> print
```

</td>
<td>

* [Example 1](https://github.com/PlutoLang/plutolang.github.io/blob/8fc3eaa1b0fe0d2fe38125f7f80d26af7b298106/docs/Runtime%20Environment/HTTP.md?plain=1#L36)
* [Example 2](https://github.com/PlutoLang/plutolang.github.io/blob/8fc3eaa1b0fe0d2fe38125f7f80d26af7b298106/docs/New%20Operators.md?plain=1#L142)

</td>
<td>

* [Doc](https://pluto-lang.org/docs/Runtime%20Environment/HTTP)
* [Doc for pipe](https://pluto-lang.org/docs/New%20Operators#pipe-operator)

</td>
<td>

* [JSON Demo](https://pluto-lang.org/web/#code=local%20%7B%20http%2C%20json%20%7D%20%3D%20require%20%22pluto%3A*%22%0D%0A%0D%0Ahttp.request(%22https%3A%2F%2Fhttpbin.org%2Fget%22)%0D%0A%7C%3E%20json.decode%0D%0A%7C%3E%20dumpvar%0D%0A%7C%3E%20print%0D%0A)
* [Demo](https://pluto-lang.org/web/#code=local%20http%20%3D%20require%20%22pluto%3Ahttp%22%0D%0Alocal%20body%2C%20status_code%2C%20headers%2C%20status_text%20%3D%20http.request(%22https%3A%2F%2Fhttpbin.org%2Fanything%22)%0D%0Aprint(status_code..%22%20%22..status_text)%0D%0Aif%20os.platform%20!%3D%20%22wasm%22%20then%0D%0A%20%20%20%20print(dumpvar(headers))%0D%0Aend%0D%0Aprint(body))
* [Demo](https://pluto-lang.org/web/#code=local%20http%20%3D%20require%20'pluto%3Ahttp'%0A%0Ahttp.request('https%3A%2F%2Fhttpbin.org%2Fanything')%0A%7C%3E%20print%0A)

</td>
<td>

Browser and maybe Node.

</td>
<td>

JS `XMLHttpRequest` interop by [invoking](https://github.com/PlutoLang/Pluto/blob/0.9.2/src/vendor/Soup/soup/HttpRequestTask.cpp#L260) `emscripten_fetch()`.

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
<a id="php-wasm"></a>

[php-wasm](https://github.com/seanmorris/php-wasm)

<sub>Fork of [PIB](https://github.com/oraoto/pib)</sub>

</td>
<td>

```php
$url = 'https://httpbin.org/anything';

$window = new Vrzno();
$window->fetch($url)
->then(function($res) { return $res->text(); })
->then(var_dump(...));
```

</td>
<td>

* [Example](https://github.com/seanmorris/php-wasm/blob/v0.0.8/docs/scripts/fetch.php#L6)
* [Example](https://github.com/wasm-outbound-http-examples/php/blob/1ab3f308dcd43f455d5ffa1cc6a569dec3d1ed72/browser-and-node-php-wasm/index.html#L22)
* [Node.js / Deno / Bun example](https://github.com/wasm-outbound-http-examples/php/blob/1ab3f308dcd43f455d5ffa1cc6a569dec3d1ed72/browser-and-node-php-wasm/httpget.mjs#L14)

</td>
<td>

* [Doc](https://github.com/seanmorris/vrzno/blob/0e557d7138f51f4cda65fb338e35adb4f787acde/README.md#new-vrzno)
* [CloudFlare note](https://github.com/seanmorris/vrzno/blob/0e557d7138f51f4cda65fb338e35adb4f787acde/README.md?plain=1#L25)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/php/php-wasm/)
* [Demo in playground](https://seanmorris.github.io/php-wasm/?code=%253C%253Fphp%2520%252F%252F%2520%257B%2522autorun%2522%253Atrue%252C%2520%2522persist%2522%253Atrue%252C%2520%2522single-expression%2522%253A%2520false%252C%2520%2522render-as%2522%253A%2520%2522text%2522%257D%250A%250A%2524url%2520%253D%2520%27https%253A%252F%252Fapi.weather.gov%252Fgridpoints%252FTOP%252F40%252C74%252Fforecast%27%253B%250A%250A%2524window%2520%253D%2520new%2520Vrzno%253B%250A%2524window-%253Efetch%28%2524url%29%250A-%253Ethen%28function%28%2524r%29%2520%257B%2520return%2520%2524r-%253Ejson%28%29%253B%2520%257D%29%250A-%253Ethen%28var_dump%28...%29%29%253B%250A%250Aecho%2520%2522Yeah%252C%2520its%2520async.%255Cn%255Cn%2522%253B%250A&autorun=1&persist=1&single-expression=0&render-as=text&demo=fetch.php)<sub>(80M download)</sub>
* [Playground](https://seanmorris.github.io/php-wasm/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/php)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/php/blob/1ab3f308dcd43f455d5ffa1cc6a569dec3d1ed72/browser-and-node-php-wasm/README.md#test-with-bun),
[Deno](https://github.com/wasm-outbound-http-examples/php/blob/1ab3f308dcd43f455d5ffa1cc6a569dec3d1ed72/browser-and-node-php-wasm/README.md#test-with-deno),
[Node](https://github.com/wasm-outbound-http-examples/php/blob/1ab3f308dcd43f455d5ffa1cc6a569dec3d1ed72/browser-and-node-php-wasm/README.md#test-with-nodejs),
and [CloudFlare Workers](https://github.com/seanmorris/php-wasm/blob/v0.0.8/README.md?plain=1#L61).

</td>
<td>

Manual JS `fetch` interop using [`vrzno`](https://github.com/seanmorris/vrzno/blob/0e557d7138f51f4cda65fb338e35adb4f787acde/vrzno_functions.c#L104-L107) PHP extension.

</td>
</tr>
</table>

### Pascal
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Free Pascal](https://www.freepascal.org)

</td>
<td>

```pascal
function httpGet(url: ShortString; Var str_out:
    ShortString): ShortString; external 'js';

var out_str : ShortString;
begin
        out_str:= DupeString( ' ' , 255 );
        httpGet('https://httpbin.org/anything', out_str);
        writeln(out_str);
end.
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/freepascal/blob/daf03bf8a4f09307ad49076b11790d689716344d/browser-sync-xhr-shortstring/main.pp#L14)

</td>
<td></td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/freepascal/sync-xhr-shortstring/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/freepascal)

</td>
<td>Browser and maybe Node</td>
<td>

Direct [`XMLHttpRequest` interop](https://github.com/wasm-outbound-http-examples/freepascal/blob/daf03bf8a4f09307ad49076b11790d689716344d/browser-sync-xhr-shortstring/index.html#L31) in
[sync](https://github.com/wasm-outbound-http-examples/freepascal/blob/daf03bf8a4f09307ad49076b11790d689716344d/browser-sync-xhr-shortstring/index.html#L30) mode 
via [importing](https://github.com/wasm-outbound-http-examples/freepascal/blob/daf03bf8a4f09307ad49076b11790d689716344d/browser-sync-xhr-shortstring/main.pp#L6-L7) 
the JS function into Pascal with [mapping](https://github.com/wasm-outbound-http-examples/freepascal/blob/daf03bf8a4f09307ad49076b11790d689716344d/browser-sync-xhr-shortstring/index.html#L42).

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

### Prolog
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Scryer Prolog](https://github.com/mthom/scryer-prolog)

</td>
<td>

```prolog
:- use_module(library(wasm)).
```

```prolog
?- js_eval("const xhr=new XMLHttpRequest(); xhr.open('GET','https://httpbin.org/anything',false); xhr.send(); xhr.responseText;", Txt), format("~s", [Txt]).
```

</td>
<td>

&lt;--

</td>
<td>

* [Doc](https://www.scryer.pl/wasm)
* [Readme](https://github.com/mthom/scryer-prolog/tree/v0.9.4#building-webassembly)

</td>
<td>

* Example code works in [Playground](https://play.scryer.pl/)

</td>
<td>

Browser

</td>
<td>

Manual JS `XMLHttpRequest` interop using [`js_eval`](https://github.com/mthom/scryer-prolog/blob/v0.9.4/src/machine/system_calls.rs#L4907) predicate.

</td>
</tr>
<tr>
<td>

[SWI-Prolog](https://github.com/SWI-Prolog/swipl-devel)

</td>
<td>

```prolog
fetch('https://httpbin.org/anything', text, Out).
```

</td>
<td>

&lt;--

</td>
<td>

[Doc](https://www.swi-prolog.org/pldoc/man?predicate=fetch/3)

</td>
<td>

* Example code works in [Playground](https://wasm.swi-prolog.org/wasm/shell)

</td>
<td>

Browser and Node

</td>
<td>

JS `fetch` [interop](https://github.com/SWI-Prolog/swipl-devel/blob/V9.3.19/src/wasm/prolog.js#L578) by declaring the
[predicate](https://github.com/SWI-Prolog/swipl-devel/blob/V9.3.19/library/wasm.pl#L460).

</td>
</tr>
<tr>
<td>

[trealla-js](https://github.com/guregu/trealla-js)

</td>
<td>

```prolog
js_eval("return fetch('https://httpbin.org/anything').then(r => r.text());", Txt).
```

</td>
<td>

* [Example](https://github.com/guregu/trealla-js/blob/84e02da3abb755568e1450321c6262130a004681/README.md?plain=1#L165)
* [Example](https://github.com/guregu/trealla-js/blob/84e02da3abb755568e1450321c6262130a004681/example/yield.js#L9)

</td>
<td>

[Readme](https://github.com/guregu/trealla-js/blob/84e02da3abb755568e1450321c6262130a004681/README.md#evaluating-js-code-from-prolog)

</td>
<td>

Example code works in [Playground](https://php.energy/trealla.html)

</td>
<td>

Browser and [Node](https://github.com/guregu/trealla-js/blob/84e02da3abb755568e1450321c6262130a004681/example/node.mjs#L1)

</td>
<td>

Manual invoking of JS `fetch` using [`js_eval`](https://github.com/guregu/trealla-js/blob/84e02da3abb755568e1450321c6262130a004681/src/interop.ts#L97) predicate.

</td>
</tr>
</table>

##### Prolog implemented in Golang

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[ichiban/prolog](https://github.com/ichiban/prolog)

</td>
<td>

```prolog
% custom predicate
httpget("https://httpbin.org/anything", RespTxt).
```

</td>
<td>

* [Example](https://github.com/ichiban/prolog/blob/v1.2.2/examples/call_go_from_prolog/main.go#L44)
* [Example](https://github.com/wasm-outbound-http-examples/prolog-in-go/blob/42ffa56cd751befda7c925918763b3deac50918d/browser-and-deno-ichiban-prolog/main.go#L41)

</td>
<td>

[Readme](https://github.com/ichiban/prolog/blob/v1.2.2/README.md#usage)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/prolog-in-go/ichiban-prolog/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/prolog-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/prolog-in-go/blob/42ffa56cd751befda7c925918763b3deac50918d/browser-and-deno-ichiban-prolog/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/prolog-in-go/blob/42ffa56cd751befda7c925918763b3deac50918d/browser-and-deno-ichiban-prolog/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/ichiban/prolog/blob/v1.2.2/examples/call_go_from_prolog/main.go#L23)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/ichiban/prolog/blob/v1.2.2/examples/call_go_from_prolog/main.go#L15)
a custom predicate inside Prolog.

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

[urllib3](https://github.com/urllib3/urllib3)

<sub>Since [2.2.0](https://github.com/urllib3/urllib3/releases/tag/2.2.0)</sub>

</td>
<td>

```python
import micropip
await micropip.install('urllib3')

import urllib3
res = urllib3.request('GET', 'https://httpbin.org/anything')
print(res.data.decode('utf-8'))
```

```python
# using requests
import micropip
await micropip.install('requests')

import requests
res = requests.get('https://httpbin.org/anything')
print(res.text)
```

</td>
<td>

* [Example](https://github.com/urllib3/urllib3/blob/2.2.0/docs/reference/contrib/emscripten.rst?plain=1#L42)
* [requests Example](https://github.com/urllib3/urllib3/blob/2.2.0/docs/reference/contrib/emscripten.rst?plain=1#L56)

</td>
<td>

[Doc](https://urllib3.readthedocs.io/en/2.2.0/reference/contrib/emscripten.html)

</td>
<td>

[Playground](https://pyodide.org/en/stable/console.html)

</td>
<td>

Browser [only (yet)](https://github.com/urllib3/urllib3/blob/2.2.0/docs/reference/contrib/emscripten.rst?plain=1#L19)

</td>
<td>

JS [`fetch` interop](https://github.com/urllib3/urllib3/blob/2.2.0/src/urllib3/contrib/emscripten/emscripten_fetch_worker.js#L70)
or
[`XMLHttpRequest` interop](https://github.com/urllib3/urllib3/blob/2.2.0/src/urllib3/contrib/emscripten/fetch.py#L380) 
if `fetch` [is not available](https://github.com/urllib3/urllib3/blob/2.2.0/docs/reference/contrib/emscripten.rst?plain=1#L8-L10).

</td>
</tr>
<tr>
<td>

[GPython](https://github.com/go-python/gpython)

</td>
<td>

```python
import httpclient

print(httpclient.Get('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/gpython/blob/f389d141e039d507c00610dd9230ddd23cd89faa/browser-and-deno/main.go#L48)

</td>
<td>

[Some doc](https://github.com/go-python/gpython/tree/v0.2.0/examples/embedding#but-what-about-the-lack-of-python-modules)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/gpython/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/gpython)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/gpython/tree/f389d141e039d507c00610dd9230ddd23cd89faa/browser-and-deno#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/gpython/tree/f389d141e039d507c00610dd9230ddd23cd89faa/browser-and-deno#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/gpython/blob/f389d141e039d507c00610dd9230ddd23cd89faa/browser-and-deno/main.go#L65)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/gpython/blob/f389d141e039d507c00610dd9230ddd23cd89faa/browser-and-deno/main.go#L31-L39).

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
<tr>
<td>

[PocketPy](https://github.com/pocketpy/pocketpy)

<sub>lightweight Python 3.x</sub>

</td>
<td>

```python
# custom module
import http

print(http.get('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/pocketpy/blob/ba1cd1ab25c877f3d349384674f444e338be1874/browser-sync-xhr/main.c#L34)

</td>
<td>

[Some doc](https://pocketpy.dev/bindings/)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/pocketpy/sync-xhr/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/pocketpy)

</td>
<td>Browser</td>
<td>

JS `XMLHttpRequest` interop by [invoking](https://github.com/wasm-outbound-http-examples/pocketpy/blob/ba1cd1ab25c877f3d349384674f444e338be1874/browser-sync-xhr/main.c#L17) [`emscripten_fetch()`](#emscripten_fetch)
from a custom [host function](https://github.com/wasm-outbound-http-examples/pocketpy/blob/ba1cd1ab25c877f3d349384674f444e338be1874/browser-sync-xhr/main.c#L7)
[injected](https://github.com/wasm-outbound-http-examples/pocketpy/blob/ba1cd1ab25c877f3d349384674f444e338be1874/browser-sync-xhr/main.c#L31-L32) as module function into Python.

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

[webR](https://github.com/r-wasm/webr)

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

* [Playground](https://webr.r-wasm.org/latest/)
* [Old Playground](https://webr.gwstagg.co.uk/)

</td>
<td>Browser and Node</td>
<td>

Implemented [`xhr` transport](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/patches/R-4.1.3/emscripten-xhr-download.diff#L102) which uses
JS `XMLHttpRequest` interop by [calling](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/patches/R-4.1.3/emscripten-xhr-download.diff#L184) [web worker](https://github.com/georgestagg/webR/blob/2ed96ed1db6a54209db6677b4358bb59c5d2f67a/src/webR/webr-worker.ts#L278) 
using Emscripten APIs.

</td>
</tr>
</table>

### Rebol

#### Rebol-like languages

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Rye](https://github.com/refaktor/rye)

</td>
<td>

```clojure
go does { get https://httpbin.org/anything |print }
```

</td>
<td>

 * [Example](https://github.com/refaktor/rye/blob/873f3096853cd85d2cb910c7d64c06bec5426574/examples/examples-wip/shopify2cebelca/main.rye#L20)
 * [Example](https://github.com/refaktor/rye/blob/873f3096853cd85d2cb910c7d64c06bec5426574/examples/examples-wip/cgi/call_webhook_fns.ryego#L8)
 * [Example](https://github.com/wasm-outbound-http-examples/rye/blob/b2c1728e220db1a6bfcb6f85fd7f676b244fa573/README.md?plain=1#L20)

</td>
<td>

[Some doc for embedding](https://github.com/refaktor/rye-website/blob/1bea85013b9873168952683ef4472dc9bf836f18/content/cookbook/deployment/console.md?plain=1#L42)

</td>
<td>

* [Playground](https://ryelang.org/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/rye)

</td>
<td>

Browser

</td>
<td>

[Using](https://github.com/refaktor/rye/blob/v0.0.32/evaldo/builtins_io.go#L143)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/refaktor/rye/blob/v0.0.32/evaldo/builtins_io.go#L813)
to a Rye *word*.

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

[Iced](https://crates.io/crates/iced)

</td>
<td>

```rust
// uses reqwest

let txt = reqwest::get("https://httpbin.org/anything")
  .await?.text().await?;

log::info!("text: {}", txt);
```

</td>
<td>

* [Example 1](https://github.com/iced-rs/iced/blob/0.12/examples/download_progress/src/download.rs#L24)
* [Example 2](https://github.com/iced-rs/iced/blob/0.12/examples/pokedex/src/main.rs#L162)
* [Example 3](https://github.com/zupzup/rust-frontend-example-iced/blob/d94782952c21419f36d89e091df5790082600d08/src/data.rs#L25)

</td>
<td></td>
<td></td>
<td>

Browser

</td>
<td>

Has no built-in solutions, just uses any suitable 3rd-party lib, such as:
[reqwest](#reqwest).

</td>
</tr>
<tr>
<td>

[Leptos](https://crates.io/crates/leptos)

</td>
<td>

```rust
// uses reqwasm or gloo_net for CSR

use leptos_dom::logging::console_log;

let txt = reqwasm::http::Request::get(
    "https://httpbin.org/anything")
  .send().await?.text().await?;
console_log(txt.as_str());
```

</td>
<td>

* [Example using reqwasm](https://github.com/leptos-rs/leptos/blob/v0.6.5/examples/fetch/src/lib.rs#L21)
* [Example using gloo_net](https://github.com/leptos-rs/leptos/blob/v0.6.5/examples/hackernews_js_fetch/src/api.rs#L27)
* [Example using reqwest for SSR](https://github.com/leptos-rs/leptos/blob/v0.6.5/examples/hackernews/src/api.rs#L45)

</td>
<td></td>
<td></td>
<td>

Browser

Also server-side rendering (SSR)

</td>
<td>

Has no built-in solutions, just uses any suitable 3rd-party lib, such as:
[reqwest](#reqwest),
[gloo_net](#gloo_net),
[reqwasm](#reqwasm).

</td>
</tr>
<tr>
<td>

[localghost](https://crates.io/crates/localghost)

</td>
<td>

```rust
use localghost::prelude::*;
use localghost::{log, net};

let res = net::Request::get(
  "https://httpbin.org/anything").send().await?;
log::info!("text: {:?}", res.body_string().await?);
```

</td>
<td>

* [Example](https://github.com/mild-times/localghost/blob/v0.3.0/examples/fetch/src/lib.rs#L9)
* [Example](https://github.com/mild-times/localghost/blob/v0.3.0/src/lib.rs#L20)

</td>
<td>

[Doc](https://docs.rs/localghost/0.3.0/localghost/)

</td>
<td></td>
<td>

Browser and maybe Node

</td>
<td>

[JS `fetch` Interop](https://github.com/mild-times/localghost/blob/v0.3.0/src/net/request.rs#L111) using [wasm-bindgen](#wasm-bindgen)

</td>
</tr>
<tr>
<td>

[MoonZoon](https://github.com/MoonZoon/MoonZoon)

</td>
<td>

```rust
use zoon::{println, *};

let txt = reqwest::get("https://httpbin.org/anything")
  .await?
  .error_for_status()?
  .text()
  .await?;
println!("text: {}", txt);
```

</td>
<td>

[Example](https://github.com/MoonZoon/MoonZoon/blob/fc73b0d90bf39be72e70fdcab4f319ea5b8e6cfc/examples/custom_http_client/frontend/src/main.rs#L18)

</td>
<td>

[Doc](https://github.com/MoonZoon/MoonZoon#documentation)

</td>
<td></td>
<td>Browser</td>
<td>

Has no built-in solutions, just uses any suitable 3rd-party lib, such as:
[reqwest](#reqwest).

</td>
</tr>
<tr>
<td>

[quad-net](https://crates.io/crates/quad-net)

<sub>Plugin for [miniquad](https://crates.io/crates/miniquad) and [macroquad](https://crates.io/crates/macroquad)</sub>

</td>
<td>

```rust
use quad_net::http_request::RequestBuilder;

let mut request = RequestBuilder::new(
  "https://httpbin.org/anything").send();
loop {
  if let Some(data) = request.try_recv() {
    info!("Done! {}", data.unwrap());
  }
  next_frame().await;
}
```

</td>
<td>

[Example](https://github.com/not-fl3/quad-net/blob/31796d4ed5c9cce57c7702d18b6140d5ffacfccf/examples/http_request.rs#L7)

</td>
<td>

[Some Readme](https://github.com/not-fl3/quad-net/blob/31796d4ed5c9cce57c7702d18b6140d5ffacfccf/examples/web/README.md)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/rust/quad-net/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/rust)

</td>
<td>

Browser

</td>
<td>

JS `XMLHttpRequest` [interop](https://github.com/not-fl3/quad-net/blob/31796d4ed5c9cce57c7702d18b6140d5ffacfccf/js/quad-net.js#L118) 
in the [imported](https://github.com/not-fl3/quad-net/blob/31796d4ed5c9cce57c7702d18b6140d5ffacfccf/src/http_request.rs#L45) host function.

</td>
</tr>
<tr>
<td>
<a id="reqwest"></a>

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
<a id="reqwasm"></a>

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

[sauron](https://crates.io/crates/sauron)

</td>
<td>

```rust
use sauron::dom::{Http, spawn_local};

spawn_local(async move {
  let txt = Http::fetch_text(
    "https://httpbin.org/anything").await.unwrap();
  log::trace!("{}", txt);
});
```

</td>
<td>

* [Example](https://github.com/ivanceras/sauron/blob/8b079a7deb5b9a051ce069cfc76272c353820b24/examples/fetch-data/src/lib.rs#L63)
* [Example for component](https://github.com/ivanceras/sauron/blob/f1d56fe18e435023d3a3110f30c6fb43fc14480d/examples/fetch-data-component/src/fetcher.rs#L56)

</td>
<td>

[Doc](https://docs.rs/sauron/0.60.7/sauron/prelude/dom/struct.Http.html#method.fetch_text)

</td>
<td></td>
<td>
Browser

Also server-side rendering (SSR)
</td>
<td>

[JS `fetch` interop](https://github.com/ivanceras/sauron/blob/f1d56fe18e435023d3a3110f30c6fb43fc14480d/crates/sauron-core/src/dom/http.rs#L38) using [wasm-bindgen](#wasm-bindgen)

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
<tr>
<td>

[sycamore](https://crates.io/crates/sycamore)

</td>
<td>

```rust
// uses reqwasm
use reqwasm::http::Request;

let url = "https://httpbin.org/anything";
let res = Request::get(&url).send().await?;

let txt = res.text().await?;
log::info!("{}", txt);
```

</td>
<td>

* [Example](https://github.com/sycamore-rs/sycamore/blob/0.9.0-beta.2/examples/http-request/src/main.rs#L16)
* [Example for Builder API](https://github.com/sycamore-rs/sycamore/blob/0.9.0-beta.2/examples/http-request-builder/src/main.rs#L18)

</td>
<td></td>
<td></td>
<td>

Browser

</td>
<td>

Has no built-in solutions, just uses any suitable 3rd-party lib, such as:
[reqwasm](#reqwasm).

</td>
</tr>

</table>

<a id="rust-scripting"></a>
#### Scripting languages for Rust
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Rune](https://github.com/rune-rs/rune)

</td>
<td>

```rust
let req = http::get(
  "https://httpbin.org/anything").await?;
let txt = req.text().await?;
println(txt);
```

</td>
<td>

* [Async example](https://github.com/rune-rs/rune/blob/0.13.4/scripts/book/async/async_blocks.rn#L3)
* [Stream example](https://github.com/rune-rs/rune/blob/0.13.4/scripts/book/streams/basic_stream.rn#L5)
* [Json example](https://github.com/rune-rs/rune/blob/0.13.4/scripts/book/objects/json.rn#L5-L6)

</td>
<td>

[Some doc](https://github.com/rune-rs/rune/blob/0.13.4/book/src/async.md#async-functions)

</td>
<td>

[Playground](https://rune-rs.github.io/play/?c=cHViIGFzeW5jIGZuIG1haW4oKXsKbGV0IHJlcXVlc3QgPSBodHRwOjpnZXQoImh0dHBzOi8vaHR0cGJpbi5vcmcvYW55dGhpbmciKS5hd2FpdD87CmxldCB0eHQgPSByZXF1ZXN0LnRleHQoKS5hd2FpdD87CnByaW50bG4odHh0KTsKfQ%3D%3D)

</td>
<td>

Browser

</td>
<td>

[Uses](https://github.com/rune-rs/rune/blob/0.13.4/crates/rune-modules/src/http.rs#L269) [reqwest](#reqwest).

</td>
</tr>
</table>

### Starlark

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[starlark-go](https://github.com/google/starlark-go)

</td>
<td>

```starlark
# custom function
print(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/ab9da9b5d1de8768f00f0a58bc782a0473a1bb82/browser-and-deno/main.go#L13)

</td>
<td>

[Readme](https://github.com/google/starlark-go/blob/ee8ed142361c69d52fe8e9fb5e311d2a0a7c02de/README.md?plain=1#L94)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/starlark-in-go/starlark/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/starlark-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/ab9da9b5d1de8768f00f0a58bc782a0473a1bb82/browser-and-deno/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/ab9da9b5d1de8768f00f0a58bc782a0473a1bb82/browser-and-deno/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/ab9da9b5d1de8768f00f0a58bc782a0473a1bb82/browser-and-deno/main.go#L23)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/ab9da9b5d1de8768f00f0a58bc782a0473a1bb82/browser-and-deno/main.go#L32)
a custom function inside Starlark.

</td>
</tr>
<tr>
<td>

[starlark-go-nethttp](https://github.com/pcj/starlark-go-nethttp)

</td>
<td>

```starlark
res = http.get('https://httpbin.org/anything')
print(res.body)
```

</td>
<td>

* [Test](https://github.com/pcj/starlark-go-nethttp/blob/4f030cb7e2df93d73297c4cdbf7c7fdbfc6290d7/get_test.go#L29)
* [Example](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-nethttp/main.go#L11)

</td>
<td>

[Readme](https://github.com/pcj/starlark-go-nethttp/blob/4f030cb7e2df93d73297c4cdbf7c7fdbfc6290d7/README.md#getting-started)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/starlark-in-go/nethttp/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/starlark-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-nethttp#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-nethttp#test-with-deno).

</td>
<td>

[Using](https://github.com/pcj/starlark-go-nethttp/blob/4f030cb7e2df93d73297c4cdbf7c7fdbfc6290d7/get.go#L18)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/pcj/starlark-go-nethttp/blob/4f030cb7e2df93d73297c4cdbf7c7fdbfc6290d7/module.go#L16).

</td>
</tr>
<tr>
<td>

[qri-io/starlib](https://github.com/qri-io/starlib)

<sub>_"Starlark's missing stdlib"_</sub>

</td>
<td>

```starlark
load('http.star', 'http')

res = http.get('https://httpbin.org/anything')
print(res.body())
```

</td>
<td>

* [Test](https://github.com/qri-io/starlib/blob/v0.5.0/http/testdata/test.star#L4)
* [Example](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/fe339ccb1aaf552e5b62a33550b424a85ff5fbc0/browser-and-deno-starlib/main.go#L12)

</td>
<td>

[Doc](https://github.com/qri-io/starlib/tree/v0.5.0/http#functions)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/starlark-in-go/starlib/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/starlark-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/starlark-in-go/tree/fe339ccb1aaf552e5b62a33550b424a85ff5fbc0/browser-and-deno-starlib#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/starlark-in-go/tree/fe339ccb1aaf552e5b62a33550b424a85ff5fbc0/browser-and-deno-starlib#test-with-deno).

</td>
<td>

[Using](https://github.com/qri-io/starlib/blob/7fb7ff9ec804789a6dd0c1470abc5f07ba4a0c46/http/http.go#L134)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/qri-io/starlib/blob/7fb7ff9ec804789a6dd0c1470abc5f07ba4a0c46/http/http.go#L78).

</td>
</tr>
<tr>
<td>

[starlight-go/starlight](https://github.com/starlight-go/starlight)

</td>
<td>

```starlark
# custom function
print(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/8ac2f92995e40b29f97f716707b1f16cbc82277b/browser-and-deno-starlight/main.go#L27)

</td>
<td>

[Readme](https://github.com/starlight-go/starlight/tree/b06f321544f32fa1ece751522f04f6629b15c3b6?tab=readme-ov-file#functions)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/starlark-in-go/starlight/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/starlark-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/8ac2f92995e40b29f97f716707b1f16cbc82277b/browser-and-deno-starlight/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/8ac2f92995e40b29f97f716707b1f16cbc82277b/browser-and-deno-starlight/README.md#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/8ac2f92995e40b29f97f716707b1f16cbc82277b/browser-and-deno-starlight/main.go#L12)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/8ac2f92995e40b29f97f716707b1f16cbc82277b/browser-and-deno-starlight/main.go#L22)
a custom function inside Starlark.

</td>
</tr>
<tr>
<td>

[Starlight Enhanced](https://github.com/1set/starlight)

<sub>Maintained fork of Starlight</sub>

</td>
<td>

```starlark
# custom function
print(httpget('https://httpbin.org/anything'))
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-starlight-enhanced/main.go#L27)

</td>
<td>

[Readme](https://github.com/1set/starlight/tree/v0.1.1?tab=readme-ov-file#simplified-script-execution)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/starlark-in-go/starlight-enhanced/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/starlark-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-starlight-enhanced#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-starlight-enhanced#test-with-deno).

</td>
<td>

[Using](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-starlight-enhanced/main.go#L12)
Golang's [`"net/http"`](#go-net-http) via [mapping](https://github.com/wasm-outbound-http-examples/starlark-in-go/blob/35d67e6d47ed13b6290bb9cf2765df7d9d61f00d/browser-and-deno-starlight-enhanced/main.go#L22)
a custom function inside Starlark.

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

[criTiCaL](https://github.com/skx/critical)

</td>
<td>

```tcl
# custom command
puts [httpget "https://httpbin.org/anything"]
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/main.go#L13)

</td>
<td>

[Readme](https://github.com/skx/critical/blob/44b41592cc897cf9f7aaa9e108df76fab848ebdc/README.md?plain=1#L65)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/tcl-in-go/critical/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/tcl-in-go)

</td>
<td>

Browser,
[Bun](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/README.md#test-with-bun),
and [Deno](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/README.md#test-with-deno).

</td>
<td>

[Uses](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/main.go#L23)
Golang's [`"net/http"`](#go-net-http) in
a [custom command](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/main.go#L21)
[injected](https://github.com/wasm-outbound-http-examples/tcl-in-go/blob/8333daaf436b0ab8aa1d67724a09c800868507f2/browser-and-deno-critical/main.go#L32)
into the language.

</td>
</tr>
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

### Wonkey

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Wonkey/httprequest](https://github.com/wonkey-coders/wonkey)

</td>
<td>

```monkey
Local request := New HttpRequest
request.ReadyStateChanged = Lambda()
  If request.ReadyState = ReadyState.Done Then
    Print "Body: " + request.ResponseText
  End
End

request.Open("GET", "https://httpbin.org/anything")
request.Send()
```

</td>
<td>

* [Example 1](https://github.com/wonkey-coders/wonkey/blob/v2022.04/modules/httprequest/tests/simple_get.wx#L41)
* [Example 2](https://github.com/wasm-outbound-http-examples/wonkey/blob/f0a6f30dedcc8363b949d9e58833beabb8b91e89/browser/httpget.wx#L27)

</td>
<td>

[Some doc](https://wonkey-coders.github.io/docs/modules/httprequest/httprequest-module/)

</td>
<td>

* [Demo](https://wasm-outbound-http-examples.github.io/wonkey/)
* [Dev Container](https://codespaces.new/wasm-outbound-http-examples/wonkey)

</td>
<td>Browser</td>
<td>

JS `fetch` interop [using](https://github.com/wonkey-coders/wonkey/blob/v2022.04/modules/httprequest/httprequest_emscripten.wx#L28) Emscripten APIs.

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

<a id="assemblyscript-wasi-http"></a>
[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [dispatchrun/wasi-go](https://github.com/dispatchrun/wasi-go)

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
2. Wazero in [wasi-go version 0.7](https://github.com/dispatchrun/wasi-go/pull/56#issuecomment-1615514341) and above

</td>
<td>

[Calling](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/request.ts#L112) to
[imported](https://github.com/dev-wasm/dev-wasm-ts/blob/1b4ec0d01e6fdb576e18126d92b23a90709630d0/http/raw.ts#L35)

1. Wasmtime's [host function](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L47),
   which, in turn, [performs](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L179) real request using
   [`hyper`](https://github.com/hyperium/hyper): [https](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L130),
   [http](https://github.com/bytecodealliance/wasmtime/blob/v10.0.1/crates/wasi-http/src/http_impl.rs#L145).

2. Wazero's [host function](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

</td>
</tr>
</table>

<a id="csharp-wasi"></a>
### C# / .Net

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request </th></tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for .NET](https://github.com/extism/dotnet-pdk)

</td>
<td>

```csharp
using Extism;

var req = new HttpRequest(
    "https://httpbin.org/anything")
{
    Method = HttpMethod.GET
};
var res = Pdk.SendRequest(req);
Pdk.SetOutput(res.Body);
```

</td>
<td>

* [Example](https://github.com/extism/dotnet-pdk/blob/v1.0.0-rc3/samples/KitchenSink/Program.cs#L77)
* [Example](https://github.com/wasm-outbound-http-examples/extism-dotnet-pdk/blob/b42f25ad08c3a82e5dbab982055747c87cde1b3d/Program.cs#L9)

</td>
<td>

[Doc](https://github.com/extism/dotnet-pdk/tree/v1.0.0-rc3#making-http-calls)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/extism-dotnet-pdk)

</td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.0.0-rc0/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v0.3.0/go.mod#L10) Wazero

</td>
<td>

[Calling](https://github.com/extism/dotnet-pdk/blob/v1.0.0-rc3/src/Extism.Pdk/Interop.cs#L305) 
[C-level-imported](https://github.com/extism/dotnet-pdk/blob/v1.0.0-rc3/src/Extism.Pdk/Native.cs#L60-L61)
runtime's [host function](https://github.com/extism/extism/blob/v1.0.0-rc0/runtime/src/pdk.rs#L146)
[exported](https://github.com/extism/extism/blob/v1.0.0-rc0/runtime/src/plugin.rs#L188) for plugins,
which [makes](https://github.com/extism/extism/blob/v1.0.0-rc0/runtime/src/pdk.rs#L214) actual request using `ureq`.

</td>
</tr>
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

<a id="csharp-wasi-http"></a>
[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [dispatchrun/wasi-go](https://github.com/dispatchrun/wasi-go)

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
2. Wazero in [wasi-go version 0.7](https://github.com/dispatchrun/wasi-go/pull/56#issuecomment-1615514341) and above

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

2. Wazero's [host function](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

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

[Extism Plug-in Development Kit (PDK) for C](https://github.com/extism/c-pdk)

</td>
<td>

```cpp
#define EXTISM_IMPLEMENTATION
#include "extism-pdk.h"
#include <stdint.h>
#include <string.h>

int32_t EXTISM_EXPORTED_FUNCTION(httpget) {
  const char *r = "{\"url\": \"https://httpbin.org/anything\"}";
  ExtismHandle req = extism_alloc_buf_from_sz(r);
  ExtismHandle res = extism_http_request(req, 0);

  extism_output_set_from_handle(res, 0, extism_length(res));
  return 0;
}
```
</td>
<td>

* [Example](https://github.com/extism/c-pdk/blob/v1.0.1/README.md?plain=1#L294)
* [Example](https://github.com/wasm-outbound-http-examples/extism-c-pdk/blob/7cc9ca97de72922d7754834dc9cc383b6fcb4e8b/httpget.c#L11)
* [Low-level API Example](https://github.com/wasm-outbound-http-examples/extism-c-pdk/blob/7cc9ca97de72922d7754834dc9cc383b6fcb4e8b/deprecated-extismpointer/httpget.c#L12)

</td>
<td>

[Doc](https://github.com/extism/c-pdk/blob/v1.0.1/README.md#http)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/extism-c-pdk)

</td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.5.0/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v1.5.2/go.mod#L15) Wazero

</td>
<td>

Calling
[C-level-imported](https://github.com/extism/c-pdk/blob/v1.0.1/extism-pdk.h#L47)
runtime's [host function](https://github.com/extism/extism/blob/v1.5.0/runtime/src/pdk.rs#L156)
[exported](https://github.com/extism/extism/blob/v1.5.0/runtime/src/plugin.rs#L230) for plugins,
which [makes](https://github.com/extism/extism/blob/v1.5.0/runtime/src/pdk.rs#L235) actual request using `ureq`.

</td>
</tr>
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

<a id="cpp-wasi-http"></a>
[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [dispatchrun/wasi-go](https://github.com/dispatchrun/wasi-go)

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
2. Wazero in [wasi-go version 0.7](https://github.com/dispatchrun/wasi-go/pull/56#issuecomment-1615514341) and above

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

2. Wazero's [host function](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

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

[knqyf263/go-plugin](https://github.com/knqyf263/go-plugin)

</td>
<td>

```go
hostFunctions := protobufs.NewHostFunctions()

resp, err := hostFunctions.HttpGet(ctx,
  &protobufs.HttpGetRequest{Url: "https://httpbin.org/anything"})
```

</td>
<td>

* [Example](https://github.com/knqyf263/go-plugin/blob/v0.8.0/examples/host-functions/plugin/plugin.go#L29)
* [Example](https://github.com/wasm-outbound-http-examples/go-plugin/blob/29ec93663b5bb6feb1e21c340441614ad7dfcb1c/plugin/plugin.go#L22)
* [Usage from host program](https://github.com/wasm-outbound-http-examples/go-plugin/blob/29ec93663b5bb6feb1e21c340441614ad7dfcb1c/main.go#L25-L27)

</td>
<td>

[Readme](https://github.com/knqyf263/go-plugin/tree/v0.8.0#usage)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/go-plugin)

</td>
<td>

go-plugin [uses](https://github.com/knqyf263/go-plugin/tree/v0.8.0#under-the-hood) wazero

</td>
<td>

[Invoking](https://github.com/knqyf263/go-plugin/blob/v0.8.0/examples/host-functions/plugin/plugin.go#L29) the  
[bound](https://github.com/knqyf263/go-plugin/blob/v0.8.0/examples/host-functions/main.go#L28) 
[host function](https://github.com/knqyf263/go-plugin/blob/v0.8.0/examples/host-functions/main.go#L52).

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
<a id="golang-wasi-http"></a>

[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [dispatchrun/wasi-go](https://github.com/dispatchrun/wasi-go)

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
2. Wazero in [wasi-go version 0.7](https://github.com/dispatchrun/wasi-go/pull/56#issuecomment-1615514341) and above

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

2. Wazero's [host function](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

</td>
</tr>
<tr>
<td>

[wasi-http-go](https://github.com/ydnar/wasi-http-go)

</td>
<td>

```go
import ("io"; "log"; "net/http"
 _ "github.com/ydnar/wasi-http-go/wasihttp"
)

req, _ := http.NewRequest("GET",
  "https://httpbin.org/anything", http.NoBody)

resp, _ := http.DefaultClient.Do(req)
defer resp.Body.Close()
body, _ := io.ReadAll(resp.Body)
log.Println(string(body))
```

</td>
<td>

[Example](https://github.com/ydnar/wasi-http-go/blob/333b54c12051db648940280f9cb6ae9c604d6e4f/examples/proxy/proxy.go#L37)

</td>
<td>

[How to run](https://github.com/ydnar/wasi-http-go/blob/333b54c12051db648940280f9cb6ae9c604d6e4f/examples/proxy/proxy.go#L3-L5)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/tinygo)

</td>
<td>

Runtime supporting wasip2-http (only Wasmtime at the moment)

</td>
<td>

[Wrapper](https://github.com/ydnar/wasi-http-go/blob/333b54c12051db648940280f9cb6ae9c604d6e4f/wasihttp/transport.go#L42) for
[wasi-http](#golang-wasi-http) using [overrides](https://github.com/ydnar/wasi-http-go/blob/333b54c12051db648940280f9cb6ae9c604d6e4f/wasihttp/transport.go#L15-L19).

</td>
</tr>
<tr>
<td>

[dispatchrun/net](https://github.com/dispatchrun/net)

<sub>f.k.a. stealthrocket/net</sub> 

</td>
<td>

```go
import ( 	"fmt" ; "io" ; "net/http"
  _ "github.com/dispatchrun/net/http"
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

* [Test](https://github.com/dispatchrun/net/blob/v0.1.4/http/http_wasip1_test.go#L33)
* [HTTP Example](https://github.com/wasm-outbound-http-examples/go/blob/c48072d362c953ef88498967fe20efb642959527/wasi-stealthrocket-net/httpget.go#L12)
* [HTTPS Example](https://github.com/wasm-outbound-http-examples/go/blob/c48072d362c953ef88498967fe20efb642959527/wasi-stealthrocket-net/httpsget.go#L22)

</td>
<td>

[Readme](https://github.com/dispatchrun/net/blob/v0.1.4/README.md#configuration)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/go)

</td>
<td>

[Wazero and WasmEdge](https://github.com/dispatchrun/net/blob/v0.1.4/README.md?plain=1#L10-L11)

</td>
<td>

[Hotpatching](https://github.com/dispatchrun/net/blob/v0.1.4/http/http_wasip1.go#L13) on module import `http.DefaultTransport` with
`wasip1.DialContext`
which refers to 
[imported `sock_conn()`](https://github.com/dispatchrun/net/blob/v0.1.4/wasip1/syscall_wasmedge_wasip1.go#L143) in the case of WasmEdge
and to [`syscall.Connect()`](https://github.com/dispatchrun/wasi-go/blob/v0.6.9/internal/sockets/dial.go#L24) in the case of Wazero.

</td>
</tr>
<tr>
<td>

[VMware OCTO / Wasm Workers Server](https://workers.wasmlabs.dev)

</td>
<td>

```go
import (
  "log"; "net/http"
  "github.com/vmware-labs/wasm-workers-server/kits/go/worker"
)

req, _ := http.NewRequest(http.MethodGet,
  "https://httpbin.org/anything", nil)
res, _ := worker.SendHttpRequest(req)
defer res.Body.Close()
body, _ := io.ReadAll(res.Body)
log.Println(string(body))
```

</td>
<td>

[Example](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/examples/go-fetch/main.go#L29)

</td>
<td>

[Doc](https://workers.wasmlabs.dev/docs/languages/go#send-an-http-request)

</td>
<td></td>
<td>

[Wasm Workers Server](https://github.com/vmware-labs/wasm-workers-server)
[uses](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/docs/docs/get-started/how-it-works.md?plain=1#L24)
[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[Calling](https://github.com/vmware-labs/wasm-workers-server/blob/main/kits/go/worker/worker.go#L241) to 
[Go-wrapped](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/go/worker/bindings/bindings.go#L252), to
[C-wrapped](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/go/worker/bindings/bindings.c#L176), to
[C-level imported](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/go/worker/bindings/bindings.c#L4)
[host function](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L56)
which [makes](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L129)
request using [reqwest](#reqwest).

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
import { fetch } from 'http'

const res = await fetch('https://httpbin.org/anything')
print(await res.text())
```

</td>
<td>

* [Example](https://github.com/second-state/wasmedge-quickjs/blob/4afed4460a0db22be1b16d2bbfc83d328e3cefae/example_js/wasi_https_fetch.js#L5)
* [Example for http](https://github.com/second-state/wasmedge-quickjs/blob/4afed4460a0db22be1b16d2bbfc83d328e3cefae/example_js/wasi_http_fetch.js#L5)

</td>
<td>

[Doc](https://wasmedge.org/docs/develop/javascript/networking/#fetch-client)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/wasmedge-quickjs)

</td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[Distinguished](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/modules/http.js#L204-L208) by URL scheme 
[raw socket write](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/modules/http.js#L224)
to
(1) [`WasiTcpConn`](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/src/internal_module/wasi_net_module.rs#L393)
which is [wrapper](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/src/event_loop/mod.rs#L68)
to Wasmedge's implementation of WASI Socket
or
(2) [`WasiTlsConn`](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/src/internal_module/wasi_net_module.rs#L190)
which is [wrapper](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/src/event_loop/mod.rs#L122)
to [`wasmedge_rustls_api`](https://github.com/second-state/wasmedge_rustls_api).

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
<tr>
<td>

[VMware OCTO / Wasm Workers Server](https://workers.wasmlabs.dev)

</td>
<td>

```js
const resp = await fetch('https://httpbin.org/anything');
const txt = await resp.text();
console.log(txt);
```

</td>
<td>

[Example](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/examples/js-fetch/index.js#L17)

</td>
<td>

[Doc](https://workers.wasmlabs.dev/docs/languages/javascript/#send-an-http-request-fetch)

</td>
<td></td>
<td>

[Wasm Workers Server](https://github.com/vmware-labs/wasm-workers-server)
[uses](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/docs/docs/get-started/how-it-works.md?plain=1#L24)
[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[Calling](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/javascript/shims/bindings.js#L27) 
[bound to JS](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/javascript/src/bindings.rs#L23) 
[`send_http_request()`](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/javascript/src/bindings.rs#L72) 
the [host function](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L56)  
which [makes](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L129) 
request using [reqwest](#reqwest).

</td>
</tr>
</table>

<a id="moonbit-wasi"></a>
### MoonBit
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for MoonBit](https://github.com/extism/moonbit-pdk)

<sub>Experimental</sub>

</td>
<td>

```rust
pub fn https_get() -> Int {
  let req : Unit = @http.new_request(
    @http.Method::GET,
    "https://httpbin.org/anything",
  )
  let resp : Unit = req.send()
  resp.output()
  return 0
}
```

</td>
<td>

* [Example](https://github.com/extism/moonbit-pdk/blob/c7b2a166d7097bd61b3b7cfc32215ce63fdfb85e/examples/http-get/http-get.mbt#L13)
* [Example](https://github.com/extism/moonbit-pdk/blob/c7b2a166d7097bd61b3b7cfc32215ce63fdfb85e/examples/kitchen-sink/kitchen-sink.mbt#L16-L17)

</td>
<td>

* [Doc](https://mooncakes.io/docs/#/extism/moonbit-pdk/pdk/http/members)
* [Readme](https://github.com/extism/moonbit-pdk/blob/c7b2a166d7097bd61b3b7cfc32215ce63fdfb85e/README.md#http)

</td>
<td></td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.4.1/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v1.5.2/go.mod#L15) Wazero

</td>
<td>

[Calling](https://github.com/extism/moonbit-pdk/blob/0a43ef6c5e4a27f1a78f65e1e4ab1ce671a85252/pdk/http/http.mbt#L37)
[imported](https://github.com/extism/moonbit-pdk/blob/0a43ef6c5e4a27f1a78f65e1e4ab1ce671a85252/pdk/extism/env.mbt#L81)
runtime's [host function](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L156)
[exported](https://github.com/extism/extism/blob/v1.4.1/runtime/src/plugin.rs#L228) for plugins,
which [makes](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L235) actual request using `ureq`.

</td>
</tr>
</table>

<a id="prolog-wasi"></a>
### Prolog
<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[trealla-spin](https://github.com/guregu/trealla-spin)

<sub>Spin SDK for Prolog</sub>

</td>
<td>

```prolog
:- use_module(library(spin)).

http_fetch("https://httpbin.org/anything", Resp, []),
write(Resp), nl.
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/spin/blob/17a47bb177721b64f97eeed4c342dcc621721a37/trealla-spin/init.pl#L7)

</td>
<td>

[Doc](https://developer.fermyon.com/wasm-languages/prolog)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/spin)

</td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[Invoking](https://github.com/guregu/trealla/blob/v0.27.22/src/wasm/wasi-outbound-http.c#L115) `wasi-outbound-http`
by [binding](https://github.com/guregu/trealla/blob/v0.27.22/src/bif_contrib.c#L862) to 
[`http_fetch`](https://github.com/guregu/trealla/blob/v0.27.22/library/spin.pl#L208-L210) predicate.

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

[componentize-py](https://github.com/bytecodealliance/componentize-py)

</td>
<td>

```python
import poll_loop
from proxy.imports.types import (
  SchemeHttps, OutgoingRequest )

req = OutgoingRequest(Fields.from_list([]))
req.set_scheme(SchemeHttps())
req.set_authority('httpbin.org')
req.set_path_with_query('/anything')

resp = await poll_loop.send(req)

stream = poll_loop.Stream(resp.consume())
buf = b''
while True:
  chunk = await stream.next()
  if chunk is None:
    break
  else:
    buf += chunk

print(buf.decode('utf-8'))
```

</td>
<td>

[Example](https://github.com/bytecodealliance/componentize-py/blob/a7376083f9f34e6e6fa3d012ab184308529bfa4c/examples/http/app.py#L112)

</td>
<td>

[Readme](https://github.com/bytecodealliance/componentize-py/blob/a7376083f9f34e6e6fa3d012ab184308529bfa4c/examples/http/README.md)

</td>
<td></td>
<td>

Wasmtime version 15.0, maybe incl. Spin.

</td>
<td>

Genetaring Python bindings to wasi-http based on [wit files](https://github.com/bytecodealliance/componentize-py/blob/a7376083f9f34e6e6fa3d012ab184308529bfa4c/wit/deps/http/types.wit#L244) under the scenes during `componentize` process.

</td>
</tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for Python](https://github.com/extism/python-pdk)

</td>
<td>

```python
import extism

@extism.plugin_fn
def httpget():
  res = extism.Http.request(
    'https://httpbin.org/anything')
  extism.output_str(res.data_str())
```

</td>
<td>

[Example](https://github.com/wasm-outbound-http-examples/extism-python-pdk/blob/0912a23e235b76307dd677a3c8bd3d386f18698b/httpget.py#L5)

</td>
<td>

[Readme](https://github.com/extism/python-pdk#exports)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/extism-python-pdk)

</td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.7.0/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v1.5.4/go.mod#L15) Wazero

</td>
<td>

`Http.request()` method [calls](https://github.com/extism/python-pdk/blob/v0.1.0/lib/src/prelude.py#L370)
the [FFI function](https://github.com/extism/python-pdk/blob/v0.1.0/lib/src/py_module.rs#L139)
[injected](https://github.com/extism/python-pdk/blob/v0.1.0/lib/src/py_module.rs#L346) into Python's "native" `ffi` module.
It [calls](https://github.com/extism/python-pdk/blob/v0.1.0/lib/src/py_module.rs#L145) the
[`http::request()`](https://github.com/extism/rust-pdk/blob/v1.2.1/src/http.rs#L35)
from [Extism PDK for Rust](#extism-rust-pdk).

</td>
</tr>
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
  {}, None))

print(str(response.body, 'utf-8'))
```

</td>
<td>

[Example](https://github.com/fermyon/spin-python-sdk/blob/v0.3.2/examples/outbound_http/app.py#L7)

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

A Python [`spin_http` module](https://github.com/fermyon/spin-python-sdk/blob/v0.3.2/crates/spin-python-engine/src/lib.rs#L266-L272)
[calls](https://github.com/fermyon/spin-python-sdk/blob/v0.3.2/crates/spin-python-engine/src/lib.rs#L233) [imported](https://github.com/fermyon/spin-python-sdk/blob/v0.3.2/crates/spin-python-engine/src/lib.rs#L16)
via [Rust Spin SDK](https://github.com/fermyon/spin-python-sdk/blob/v0.3.2/crates/spin-python-engine/Cargo.toml#L14) 
Spin's [host function](https://github.com/fermyon/spin/blob/v2.1.0/crates/outbound-http/src/host_impl.rs#L78).

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
pub fn https_get(_: ()) -> FnResult<Memory> {
  let req = HttpRequest::new("https://httpbin.org/anything");
  let resp = http::request::<()>(&req, None)?;
  Ok(resp.into_memory())
}
```

</td>
<td>

* [Example](https://github.com/extism/rust-pdk/blob/v1.2.0/examples/http.rs#L8)
* [Example](https://github.com/extism/plugins/blob/v1.0.0/http/src/lib.rs#L5)

</td>
<td>

* [Doc](https://github.com/extism/rust-pdk/blob/v1.2.0/README.md#http)
* [Doc](https://docs.rs/extism-pdk/1.2.0/extism_pdk/struct.HttpRequest.html)

</td>
<td>

Possible with
[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-rust) _by brendandburns_

</td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.4.1/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v1.5.2/go.mod#L15) Wazero

</td>
<td>

[Calling](https://github.com/extism/rust-pdk/blob/v1.2.0/src/http.rs#L46)
[C-level-imported](https://github.com/extism/rust-pdk/blob/v1.2.0/src/extism.rs#L19)
runtime's [host function](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L156)
[exported](https://github.com/extism/extism/blob/v1.4.1/runtime/src/plugin.rs#L228) for plugins,
which [makes](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L235) actual request using `ureq`.

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
println!("body: {}", String::from_utf8_lossy(&writer));
```

</td>
<td>

[Example](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/examples/get_https.rs#L5)

</td>
<td>

[Doc](https://wasmedge.org/docs/develop/rust/http_service/client)

</td>
<td></td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[Writes](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/src/request.rs#L486) to 
[`wasmedge_wasi_socket`](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/src/request.rs#L20) stream.
For SSL, the stream is [wrapped](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/src/request.rs#L946) 
[with](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/src/tls.rs#L36) 
[rustls's stream](https://github.com/second-state/http_req/blob/35af6c133c28dd3a84aac318985842c674afc36b/src/tls.rs#L181).

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

[reqwest_wasi](https://crates.io/crates/reqwest_wasi)

as part of

[WasmEdge Sockets](https://wasmedge.org/docs/start/wasmedge/extensions/unique_extensions#available-extensions)

Any code based on WasmEdge's forks of [tokio-rs](https://github.com/WasmEdge/tokio)
or [mio](https://github.com/WasmEdge/mio)
is [expected to work in Wasmedge runtime](https://github.com/tokio-rs/tokio/issues/5331)

</td>
<td>

```rust
let res = reqwest::get("https://httpbin.org/anything").await?;
let body = res.text().await?;
println!("text: {}", body);
```

</td>
<td>

[Example](https://github.com/WasmEdge/wasmedge_reqwest_demo/blob/2f02f82028f78797352f729da648aff84b2a0fbc/src/https.rs#L8)

</td>
<td>

* [Doc](https://wasmedge.org/docs/develop/rust/socket_networking/client/)
* [Doc](https://docs.rs/reqwest_wasi/)

</td>
<td></td>
<td>

[WasmEdge](https://wasmedge.org/)

</td>
<td>

[Wrapping](https://github.com/WasmEdge/reqwest/blob/c4b9abea7f775c5fa2b9736a73e371073c8151d9/src/connect.rs#L338-L356)
internal stream with [WasmEdgeTls](https://github.com/second-state/wasmedge_hyper_rustls), which is built on top of
[WasmEdge's implementation of WASI Socket](https://github.com/second-state/wasmedge_wasi_socket).

</td>
</tr>
<tr>
<td>

[Waki](https://crates.io/crates/waki)

<sub>new gen of [wasi-http-client](https://crates.io/crates/wasi-http-client)</sub>

</td>
<td>

```rust
use waki::Client;

let res = Client::new()
  .get("https://httpbin.org/anything")
  .send().unwrap();
let body = String::from_utf8(
  res.body().unwrap()).unwrap();
println!("body:{}", body);
```

</td>
<td>

[Example](https://github.com/wacker-dev/waki/blob/v0.5.0/examples/client/src/main.rs#L21)

</td>
<td>

[Some doc](https://github.com/wacker-dev/waki/blob/v0.5.0/examples/client/README.md#http-client)

</td>
<td>

[Dev Container](https://codespaces.new/wasm-outbound-http-examples/rust)

</td>
<td>

[Wasmtime](https://wasmtime.dev/) version 
[17 and above](https://github.com/rust-lang/rust/blob/1.83.0/src/doc/rustc/src/platform-support/wasm32-wasip2.md#platform-requirements)

</td>
<td>

[Uses](https://github.com/wacker-dev/waki/blob/v0.5.0/waki/src/request.rs#L247)
[imported](https://github.com/wacker-dev/waki/blob/v0.5.0/waki/Cargo.toml#L41)
[wasmtime-wasi-http](#wasi-http).

</td>
</tr>
<tr>
<td>

<a id="wasi-http"></a>
[wasi-http](https://github.com/WebAssembly/wasi-http)

<sub>implementations:</sub>

1. [wasmtime-wasi-http](https://crates.io/crates/wasmtime-wasi-http)


2. [dispatchrun/wasi-go](https://github.com/dispatchrun/wasi-go)

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

[Readme](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/README.md#wasi-http)

</td>
<td>

Possible with
[Dev Container](https://codespaces.new/dev-wasm/dev-wasm-rust) _by brendandburns_

</td>
<td>

1. [Wasmtime version 9.0](https://github.com/bytecodealliance/wasmtime/blob/v9.0.0/RELEASES.md?plain=1#L21) and above.
2. Wazero in [wasi-go version 0.7](https://github.com/dispatchrun/wasi-go/pull/56#issuecomment-1615514341) and above

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

2. Wazero's [host function](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/default_http/request.go#L18),
   which [performs](https://github.com/dispatchrun/wasi-go/blob/v0.7.3/imports/wasi_http/types/request.go#L67) a request using `"net/http"`.

</td>
</tr>
<tr>
<td>

[VMware OCTO / Wasm Workers Server](https://workers.wasmlabs.dev)

</td>
<td>

```rust
let req = Request::builder()
  .uri("https://httpbin.org/anything")
  .body(String::new()).unwrap();

let res = bindings::send_http_request(req).unwrap();

let data = res.body();
let txt = String::from_utf8_lossy(&data);
println!("text: {txt}");
```

</td>
<td>

[Example](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/examples/rust-fetch/src/main.rs#L26)

</td>
<td>

[Doc](https://workers.wasmlabs.dev/docs/languages/rust#send-an-http-request)

</td>
<td></td>
<td>

[Wasm Workers Server](https://github.com/vmware-labs/wasm-workers-server) 
[uses](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/docs/docs/get-started/how-it-works.md?plain=1#L24) 
[Wasmtime](https://wasmtime.dev/)

</td>
<td>

[Calling](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/rust/src/bindings.rs#L66) 
[imported](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/kits/rust/src/bindings.rs#L7) 
[host function](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L56) 
which [makes](https://github.com/vmware-labs/wasm-workers-server/blob/v1.7.0/crates/worker/src/bindings/http.rs#L129) 
request using [reqwest](#reqwest).

</td>
</tr>
</table>

<a id="virgil-wasi"></a>
### Virgil

<table>
<tr><th>Product / Implementation</th><th>TLDR: Usage</th><th>TLDR: Example code</th>
<th>Doc</th>
<th>Online demo</th>
<th>WASM Runtime</th><th>Internals: method to do real request</th></tr>
<tr>
<td>

[Extism Plug-in Development Kit (PDK) for Virgil](https://github.com/titzer/virgil/tree/master/lib/pdk)

</td>
<td>

```python
var req = Http.newRequest(Method.GET, 
  "https://httpbin.org/anything");
def res = req.send(null);

res.output();
```

</td>
<td>

[Example](https://github.com/titzer/virgil/blob/ed46f7abecfaa55d7bea7b968bec3dc2a537f4bf/apps/Extism/http-get/HttpGet.v3#L11)

</td>
<td>

[Readme](https://github.com/titzer/virgil/blob/master/apps/Extism/http-get/README.md)

</td>
<td></td>
<td>

* Extism [uses](https://github.com/extism/extism/blob/v1.4.1/runtime/Cargo.toml#L12) Wasmtime
* Extism CLI [uses](https://github.com/extism/cli/blob/v1.5.2/go.mod#L15) Wazero

</td>
<td>

[Calling](https://github.com/titzer/virgil/blob/ed46f7abecfaa55d7bea7b968bec3dc2a537f4bf/lib/pdk/Http.v3#L19)
[C-level-imported](https://github.com/titzer/virgil/blob/ed46f7abecfaa55d7bea7b968bec3dc2a537f4bf/lib/pdk/Extism.v3#L83)
runtime's [host function](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L156)
[exported](https://github.com/extism/extism/blob/v1.4.1/runtime/src/plugin.rs#L228) for plugins,
which [makes](https://github.com/extism/extism/blob/v1.4.1/runtime/src/pdk.rs#L235) actual request using `ureq`.

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

[Spin SDK for Zig](https://github.com/dasimmet/zig-spin)

* <sub>Unofficial</sub>
* <sub>Fork of deleted [orig repo](https://github.com/tensorush/zig-spin)</sub>

</td>
<td>

```zig
const spin = @import("spin");

const req = spin.http.Request{ .method = .GET, 
  .url = "https://httpbin.org/anything" };
const res = spin.http.send(req) catch unreachable;
```

</td>
<td>

[Example](https://github.com/dasimmet/zig-spin/blob/4c411236f94dd3e829d7e9f9a13115db1dcc082a/examples/http-out/main.zig#L14-L15)

</td>
<td></td>
<td></td>
<td>

[Spin](https://developer.fermyon.com/spin/)
(uses [Wasmtime](https://wasmtime.dev/))

</td>
<td>

[Calling](https://github.com/dasimmet/zig-spin/blob/4c411236f94dd3e829d7e9f9a13115db1dcc082a/src/http.zig#L160)
to C-level [import](https://github.com/dasimmet/zig-spin/blob/4c411236f94dd3e829d7e9f9a13115db1dcc082a/include/wasi-outbound-http.h#L81)
of 
Spin's [host function](https://github.com/fermyon/spin/blob/v2.2.0/crates/outbound-http/src/host_impl.rs#L78).

</td>
</tr>
</table>


[^browser-with-wasm-gc]: Firefox 120+, and all based on Chrome(ium) 119+.
