
Next.js offer four options for waiting people 

- prefetching (미리 데이터가 로드되어 페이지 로드시간을 단축)
- streaming 
- client-side transitions 
- server-rendering 

---
### Server-Rendaring 

rendaring has a two types 

- Static  Rendaring - revalidation (cached data)
- Dynamic  Rendaring  - clicnet request 


The trade off(하나를 가지기 위해서 하나를 포기해야 하는) server rendaring is that the 
client must wait for the servers to respond before the new route can be shown,

this delay by  [prefetching](https://nextjs.org/docs/app/getting-started/linking-and-navigating#prefetching) routes and visit the performing client-side-transitions 

---
### Prefeching 

Prefetching이란 Instant Loading(즉시 전환)을 가능하게 해주는 Next.js의 특징이다.
새로운 페이지로의 로드전에 클라이언트가 prefetch 신호를 보내 서버로부터 데이터를 가져오는 것이다.

```typescript
{ /* prefetcing */ }
<Link href="/blog">Blog</Link> 

{ /* No patching */ }
<a href="/contact">Contact</a> 
```

- Static Route : 전체 route prefetching 
- Dynamic Route : prefetching


---
### Client-Side Transitions 

Traditionally, server-rendered page triggers a full page load,
Next.js avoids this with client-side transitions using the `<Link>` component 

- Keeping any shared layouts and UI.
- Replacing the current page with the prefetched loading state or a new page if available. 

Client-side transitions are what makes a server-rendered apps feel like client-rendered apps 

---
