# vue-app

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
In order to deploy to the webserver, perform these commands on the webserver, from whatever directory you want.
```
git clone git@github.com:{user}/hart-data-Vue.git
cd hart-data-Vue
npm install
npm run build
su -c "cp -r /dist/* /var/www/html"
```
### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
