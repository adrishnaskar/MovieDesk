
# MovieDesk

![Screenshot 2023-01-31 095954](https://user-images.githubusercontent.com/37959710/215674426-b27ac693-af49-48a0-9cd6-c3583b5c7d7f.png)

--------------------------

![Screenshot 2023-01-31 100149](https://user-images.githubusercontent.com/37959710/215674452-1b8da99a-e61e-4bab-a6fb-5194100b35c6.png)

## What is used?
* Vue js 3
* CSS Grid & Flexbox
* MovieDB API
## Demo
<a href="https://sensational-queijadas-967222.netlify.app/" target="_blank">View Demo</a>



## Project setup
```
npm install
```
### API setup
* Signup on <a href="https://www.themoviedb.org/" target="_blank">MovieDB</a> and request an api key (Follow the <a href="https://www.themoviedb.org/documentation/api" target="_blank">Docs</a>)
* Add ```api_key.js``` in the root directory
* Paste the following code (replace API_KEY with your own API key) :
``` 
const MOVIE_API = 'API_KEY'
export default MOVIE_API 
```
    
    
alternatively you can use ```dotenv``` package with node js

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```


