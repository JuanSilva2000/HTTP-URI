# HTTP-URI
La respuesta a la petición es un cuerpo html:
![Captura desde 2023-09-25 11-35-04](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/add546f3-de84-480a-b77f-bd61b1fe36b7)

Y lo que se muestra al abrir el link original es:
![Captura desde 2023-09-25 11-16-48](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/989dceca-cf61-4c97-a7a0-da42ee2ae022)

Notamos que en la peticion devuelve el código html que coindice con la del navegador, solo cambia la palabra generada aleatoriamente

Procedemos a guardar el archivo con el nombre saved.html
![Captura desde 2023-09-25 11-36-53](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/cd53b228-34c7-4bec-a792-2630229f6581)

Al abrir el saved.html en el navegador nos muestra lo siguiente:
![Captura desde 2023-09-25 11-23-13](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/e3a66c87-f7af-475e-8fd3-2a93bb939883)

Pregunta:¿Cuáles son las dos diferencias principales que has visto anteriormente y lo que ves en un navegador web 'normal'? ¿Qué explica estas diferencias?

-La primera diferencia es que no se puede ver la imagen en el archivo guardado (saved.html), esto es porque la solicitud curl solo devuelve el contenido html como respuesta mas no devuelve otros elementos como los css o imagenes, por eso no carga la imagen​

-La segunda diferencia es la palabra generada debajo de la imagen, idenpentiendmente que se haga la solicitud desde el navegador o desde la terminal, ambas son solicitudes indepentiendes y por lo tanto la respuesta será diferente (en la generacion del texto aleatorio)

Ahora veamos cómo cree el servidor que se ve una solicitud. Para ello, en otra pestaña o ventana de Terminal, nos haremos pasar por un servidor Web escuchando el puerto 8081: nc -l 8081

Pregunta: Suponiendo que estás ejecutando curl desde otro shell ¿qué URL tendrás que pasarle a curl para intentar acceder a tu servidor falso y por qué?
Rpta: curl http://localhost:8081​
Porque dado que queremos hacer una solicitud http debemos poner http, ponemos localhost pues el servidor esta en nuestra computadora local, y 8081 hace referencia al puerto en donde se encuentra el servidor falso
