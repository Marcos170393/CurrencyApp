# Currency App

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

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Descripcion

En esta aplicacion, podremos seleccionar la divisa de la cual queremos saber su cotizacion segun el Banco de la Republica Oriental del Uruguay (BROU). Una vez seleccionada la divisa (Dolares / Euros / Reales / Argentinos) se mostrara el valor del dia, pero seleccionando la fecha en el calendario, veremos la fecha a la que cerro la cotizacion ese dia.

Debo agradecer el gran aporte de este desarrollador https://github.com/gmanriqueUy, el cual desarrollo una API que consume los datos que brinda el Instituto Nacional de Estadaisticas (INE) a traves de su historial de cotizaciones actualizado diariamente. Esta API es la utilizada por CurrencyApp para poder brindar los datos solicitados.
