# [libelula-dashboard] [![version][version-badge]][CHANGELOG] [![license][license-badge]][LICENSE]

## Instruções
Abrir um terminal e correr estes comandos:

`git clone https://github.com/jpmarques19/libelula-dashboard.git`   

`npm install`   

`npm run dev`   

Neste momento é necessário configurar manualmente o IP do ARTIK,    
na linha 64 do ficheiro

`/src/components/Dashboard/Views/Overview.vue`  

onde se lê 

`var socket = io('http://localhost:3001')`
   
---
   
This project is a vue version of [Paper-dashboard](https://www.creative-tim.com/product/paper-dashboard)
designed for vue js.The dashboard includes vue-router and vuex

Check the [Live Demo here](https://cristijora.github.io/vue-paper-dashboard).

![](http://i.imgur.com/3iC1hOs.gif)


[CHANGELOG]: ./CHANGELOG.md
[LICENSE]: ./LICENSE.md
[version-badge]: https://img.shields.io/badge/version-1.0.0-blue.svg
[license-badge]: https://img.shields.io/badge/license-MIT-blue.svg
