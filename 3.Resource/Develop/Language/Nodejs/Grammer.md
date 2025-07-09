
### await  eqaul .then or callback 

Javascript is impatient, so the code of the javascript implement immediately 
If you use await , the runtime engine wait the awiat code 

`await ~~~ code` 


but mongodb force using await 

```
  
example) 

app.get("/list", async (request, response) => {

db.collection("post")

.find()

.toArray()

.then(() => {

console.log(result);

});

});

```


----
