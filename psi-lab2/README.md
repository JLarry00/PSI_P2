# PSI_P2

## Configuración de DEVTOOLS

Para habilitar Vue Devtools, revisa la siguiente configuración en los archivos:

- `tutorial-vue/vite.config.js`
- `tutorial-vue/src/main.js` (si aplica)

> **Nota:**  
> En `vite.config.js`, asegúrate de tener la siguiente línea en el bloque de configuración:
> 
> ```js
> define: {
>   __VUE_PROD_DEVTOOLS__: true // (o false) Enable Vue Devtools in production CAREFUL
> }
> ```
> 
> En `main.js`, asegúrate de tener la siguiente línea:
> 
> ```js
> app.config.devtools = true // (o false) Enable devtools in production (use with caution)
> ```
> 
> Esto permitirá el uso de Vue Devtools durante el desarrollo.