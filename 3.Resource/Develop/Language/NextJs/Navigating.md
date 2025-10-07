
Next.js offer four options for waiting people 

- prefetching 
- streaming 
- client-side transitions 
- server-rendering 



---
### Client-Side Transitions 

Traditionally, server-rendered page triggers a full page load,
Next.js avoids this with client-side transitions using the `<Link>` component 

-  Keeping any shared layouts and UI.
- Replacing the current page with the prefetched loading state or a new page if available.
