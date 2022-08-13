## NEXTとDaiDaiとGO API通信プロセス

```mermaid
sequenceDiagram
    participant DAIDAI 
    participant NEXT FRONT
    participant NEXT SERVER
    participant GO API
    DAIDAI->>NEXT FRONT: http-proxy-middleware('/nextAPI')
    NEXT FRONT->>NEXT SERVER: Axios: '/api/*'(API Routes)
    NEXT SERVER->>GO API: Axios: 'http://GO-URL:GO-PORT/v1/api/*'
    GO API->>NEXT SERVER: JSON Response(async/await)
    NEXT SERVER->>NEXT FRONT: JSON Response(async/await)
    NEXT FRONT->>NEXT FRONT: File System Base(Dynamic Routes)
    NEXT FRONT->>DAIDAI SERVER: window.location
```

> **Attention:**

- NEXT(HTTP) ----> DotNet Core(HTTPS)
    - サーバー内部通信(Axios: Https Agent)
    - ブラウザ外部通信(CORS: api server need to add trust origin url)
- DotNet Core(HTTPS) ----> NEXT(HTTP)
    - SPA Proxy(publish file)

