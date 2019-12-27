```plantuml
User -> Browser: URI 
alt Если нет соответствия в HSTS
Browser -> OS: Вызов функции gethostbyname
alt Если нет соответствия в кэше или в hosts файле
OS -> DNS_server: ARP request
DNS_server --> OS: ARP reply с IP 
else Если есть соответствие в кэше или в hosts
OS -> OS: IP
end
else Если есть соответствие в HSTS
Browser -> OS: IP 
end
OS -> Server_OS: TSP Handshake
OS -> Server_OS: SYN
Server_OS -> OS: SYN, ACK
OS -> Server_OS: ACL
OS -> Browser: Соединение установлено
Browser -> OS: HTTP запрос
OS-> Server_OS: TCP пакет
Server_OS -> HTTP_Server: HTTP запрос
activate HTTP_Server
HTTP_Server -> Server_OS: HTTP ответ
deactivate HTTP_Server
Server_OS -> OS: TCP пакет
OS -> Browser: HTTP ответ
activate Browser
alt Выключен keep-alive
OS -> Server_OS: FIN
Server_OS -> OS: ACK, FIN
OS -> Server_OS: ACK
end
Browser -> User: Отрисованная страница
deactivate Browser
```

![img_alt](https://www.websequencediagrams.com/cgi-bin/cdraw?lz=VXNlciAtPiBCcm93c2VyOiBVUkkgCmFsdCDQldGB0LvQuCDQvdC10YIg0YHQvtC-0YLQstC10YLRgQAFBbjRjyDQsiBIU1RTCgA8ByAtPiBPUzog0JLRi9C30L7QsiDRhNGD0L3QutGG0LjQuCBnZXRob3N0YnluYW1lADsx0LrRjdGI0LUg0LgAgRkGsiBob3N0cyDRhNCw0LnQu9C1Ck9TIC0-IEROU19zZXJ2ZXI6IEFSUCByZXF1ZXN0CgAOCiAtAIEmBwAZBnBseSDRgSBJUCAKZWxzZQCBeAu10YHRgtGMAIFuF9C1AH0cAIEHB09TOiBJUAplbmQAKTQAgk4UAIEjBW5kAIFnB1MAgWUFX09TOiBUU1AgSGFuZHNoYWtlAA0SU1lOCgAlCQCDJwhTWU4sIEFDSwA8EkFDTACCSgcAhBwJ0KHQvtC10LTQuNC90LXQvQCBfgXRgwCEEAWw0L3QvtCy0LsAFAW-AIQHEEhUVFAg0LfQsNC_0YDQvtGBCk9TAIEvD0NQINC_0LDQutC10YIAgRwOSFRUUF8AgWQGADcUYWN0aXZhdGUAHAwKACkLAIIZDwCBBgYAhUsJCmRlACwVAIIbEQCBEw8Agg4PAEYQAIEMCQCGXQcAhlgGktGL0LrQu9GO0YfQtdC9IGtlZXAtYWxpdgCDHhNGSQCDHhNBQ0ssABUFAIMeE0sAhGIFAIcGC1UAgzEGntGC0YDQuACHRgWyAIMlBb3QsNGPIACFWQWAAIM2BbjRhtCwAIF-DACBLggK&s=modern-blue)