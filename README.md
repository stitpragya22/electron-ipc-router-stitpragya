# electron-ipc-router
> electron-ipc-router is used to send messages between the main, and the renderer process.
> and helps debug the main process.    

[![NPM](https://img.shields.io/npm/v/@open_brainiac/electron-ipc-router.svg)](https://www.npmjs.com/package/@open_brainiac/electron-ipc-router) 

##Install
```bash
npm i @open_brainiac/electron-ipc-router
```
## 🚀 Usage:
```javascript
// main process
import {subscriber} from "@open_brainiac/electron-ipc-router"

const routes = {
  foo: function(a,b){
    return a+b;
  },
  bar: async function(){
    // getData is an async function, like getting data from DB
    let data = await getData()
    return  data;
  }
}

subscriber({routes})
```

```html
<!--  Renderer process -->
<script>
    import {ipc} from "@open_brainiac/electron-ipc-router"
    console.log(ipc("foo", 1,2))// => prints: 3
    ipc("bar").then(res=>console.log(res)) // => prints the data variable
</script>
```
### Debugging server
Using the electron-ipc-router you can start a node server that exposes the functions of the routes
object.

**Note:** this functionality should be used only for debugging the routes and not for production.

```javascript
  let options = {
    routes,
    server: true,
    port: 3000,
  }
  subscriber(options)
```

```bash
  curl --location --request POST 'http://localhost:3000/foo' \ // => the name of the function
  --header 'Content-Type: application/json' \
  --data-raw '{
      "args": [1,2] //=> array of the function arguments
  }'
```     
## 🤝 Contributing
Contributions, issues and feature requests are welcome!

## 📝 License
This project is **MIT** licensed

