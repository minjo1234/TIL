
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
client must 


---
### Client-Side Transitions 

Traditionally, server-rendered page triggers a full page load,
Next.js avoids this with client-side transitions using the `<Link>` component 

-  Keeping any shared layouts and UI.
- Replacing the current page with the prefetched loading state or a new page if available. 

Client-side transitions are what makes a server-rendered apps feel like client-rendered apps 

---
