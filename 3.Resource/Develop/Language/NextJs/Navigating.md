
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
- Dynamic Route : prefetching은 스킵되고 부분적인 prefetched를 이용한다.
	(부분적인 prefetched를 스킵하게 되면, Next.js는 유저가 방문하지 않아도 될 페이지의 불필요한 작업을 피할 수 있다, 그러나 사용자 입장에서는 앱이 작동하지 않는것처럼 느낄 수 있다. (느려서)

이것을 극복하기 위해   [streaming](https://nextjs.org/docs/app/getting-started/linking-and-navigating#streaming). streaming 을 사용할 수 있다.

---

### Streaming 

동적 라우트(dynamic route)에서 전체의 렌더링을 기다리다 보면 느릴 수 있다. 
이를 극복하기 위해 partially prefetched를 이용하여 

---
### Client-Side Transitions 

Traditionally, server-rendered page triggers a full page load,
Next.js avoids this with client-side transitions using the `<Link>` component 

- Keeping any shared layouts and UI.
- Replacing the current page with the prefetched loading state or a new page if available. 

Client-side transitions are what makes a server-rendered apps feel like client-rendered apps 

---


Next.js 공식문서 : https://nextjs.org/docs/app/getting-started/linking-and-navigating#client-side-transitions
