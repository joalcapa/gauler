
![image GIF Meuler](https://dl.dropboxusercontent.com/s/l63oki54lkx3ule/gauler%20logo.png?dl=0){ width="800" height="600" style="display: block; margin: 0 auto" }

### Api  Rest

Gauler es una iniciativa de modelo orientado a las convenciones estándares de api Rest,
propuestas en el año 2000 por Roy Thomas Fielding, en el cual definen los procedimientos 
necesarios para la implementación de una Interfaz de programación para aplicaciones de alto nivel, persistencia de datos atravez del protocolo HTTP.

## Controladores RestFull

La existencia del modelo, requiere de un controlador propio que maneje 
su lógica de negocios es por esto que existen propiedades, que están 
sujetas a la forma como se accede a la api, y al endpoint que se realizá, entre los metodos RestFull como Index, Show, Store, Update, Destory.

## FUNDAMENTARY el nucleo RestFull

Fundamentary es el nucleo por el cual Gauler ejecutá el proceso RestFull, Fundamentary proporcioná
un completo y sincronizado sistema de busqueda del modelo asociado al endpoint, a su vez la ejecución de
un método middleware en conjunto al modelo, por encambio si resulta ser la necesidad del proceso de filtrado
para todos los métodos RestFull, Fundamentary ejecutá un closure.
