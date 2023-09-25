# HTTP-URI
----------Comprendiendo Request y Response--------
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

Resultado:

![Captura desde 2023-09-25 11-40-28](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/16e176b8-99d2-4aa3-a068-c937a6990a24)

Lo que sucede en el servidor:

![Captura desde 2023-09-25 11-41-20](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/4dd5827c-b7fd-40c3-ae73-e7a41d08774c)

Pregunta: La primera línea de la solicitud identifica qué URL desea recuperar el cliente. ¿Por qué no ves http://localhost:8081 en ninguna parte de esa línea?
Rpta: Porque el servidor falso está aceptando la solicitud desde un puerto LOCAL, por lo tanto no es necesario incluir localhost

Prueba curl --help para ver la ayuda y verificar que la línea de comando curl -i 'http://randomword.saasbook.info' mostrará ambos (BOTH) encabezados de respuesta del servidor y(AND) luego el cuerpo de la respuesta.
Como se puede ver en la imagen la primera parte es el encabezado y la segunda parte el cuerpo con el código html

![Captura desde 2023-09-25 11-45-16](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/6c57d992-2d56-4c20-a4a0-ae1fcc5cf998)

Pregunta: Según los encabezados del servidor, ¿cuál es el código de respuesta HTTP del servidor que indica el estado de la solicitud del cliente y qué versión del protocolo HTTP utilizó el servidor para responder al cliente?
Basicamente la linea de la flecha roja responde a la pregunta, el http/1.1 inidica la que la version de protocolo que se usó es 1.1 y el numero 200 indica que la solicitud se realizó con éxito.

![Captura desde 2023-09-25 11-49-35](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/8b1a918e-93a4-45a0-950b-204a4e3e7f77)

Pregunta: Cualquier solicitud web determinada puede devolver una página HTML, una imagen u otros tipos de entidades. ¿Hay algo en los encabezados que crea que le dice al cliente cómo interpretar el resultado?
Si, en la imagen de abajo se aprecia la informacion que proporciona el encabezado para que el cliente interprete el resultado, por ejemplo Content-Type indica el formato del cuerpo de la respuesta, ese este caso sera de formato html

![Captura desde 2023-09-25 11-55-47](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/0e0398a5-8387-44dc-abd6-4945eeb8216d)

----------¿Qué sucede cuando falla un HTTP request?-----------
Pregunta: ¿Cuál sería el código de respuesta del servidor si intentaras buscar una URL inexistente en el sitio generador de palabras aleatorias? Pruéba esto utilizando el procedimiento anterior.
Como se observa en la imagen de abajo, pusimos un link inexistente y no retorna un cuerpo html en la respuesta y en la primera linea del encabezado, devuelde el numero 404 este es un error que significa que lo que se solicito no se encontró
![Captura desde 2023-09-25 12-00-13](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/b209e03f-f0aa-4f1b-9af2-5d47b34fbe4f)


¿Qué otros códigos de error HTTP existen? Utiliza Wikipedia u otro recurso para conocer los significados de algunos de los más comunes: 200, 301, 302, 400, 404, 500. Ten en cuenta que estas son familias de estados: todos los estados 2xx significan funcionó, todos los 3xx son redireccionar etc.
200 (OK): Indica que la solicitud fue realizada con exito y si se encontró la información solicitada​

301 (Moved Permanently): indica que el host si ha sido capaz de comunicarse con el servidor pero que el recurso solicitado ha sido movido a otra dirección permanentemente. [1]​

302 (Found): se produce cuando el recurso solicitado ha sido trasladado temporalmente a una nueva ubicación [2]​

400 (Bad Request): El error 400 solicitud incorrecta ocurre cuando el servidor no puede entender la petición. Por lo tanto, no la procesa y te envía el código de error en su lugar. [3]​

404 (Not Found): Este error indica que la información solicitada al servidor no exite y por lo tanto no ha sido encontrada​

500 (Internal Server Error): El error HTTP 500, en particular, indica que el servidor ha encontrado una condición inesperada que le impidió cumplir con la solicitud.​ En otras palabras, el servidor de alojamiento no puede determinar el problema exacto y mostrar un mensaje más específico [4]

Tanto el encabezado 4xx como el 5xx indican condiciones de error. ¿Cuál es la principal diferencia entre 4xx y 5xx?.
Los errores del tipo 4xx son errores causados por el cliente, como por ejemplo poner una url inexistente en la solicitud (votará error 404) en cambio los errores del tipo 5xx son errores del servidor, no del cliente, al momento de procesar la solicitud del cliente

----------¿Qué es un cuerpo de Request?----------------------









-----HTTP sin estados y cookies--------

Pregunta: Prueba las dos primeras operaciones GET anteriores. El cuerpo de la respuesta para la primera debe ser "Logged in: false" y para la segunda "Login cookie set". ¿Cuáles son las diferencias en los encabezados de respuesta que indican que la segunda operación está configurando una cookie? 

Resultado del primer comando GET/​
![Captura desde 2023-09-25 12-09-51](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/be7bc2c3-0ae6-41f8-8b12-9f7f0cd62394)

Resultado del segundo comando GET/login

![Captura desde 2023-09-25 12-13-19](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/6f3efe45-f1b4-4bf5-b014-6c69c6b68d75)

La diferencia está en la flecha roja que indica una parte de la cabecera en donde se establece un cookie y se configura algunos parametros como logged_in=true etc.. Esto no se ecuentra en la anterior imagen GET/

Pregunta: Bien, ahora supuestamente "logged in" porque el servidor configuró una cookie que indica esto. Sin embargo, si intentaa GET / nuevamente, seguirá diciendo "Logged: false". ¿Qué está sucediendo? (Sugerencia: usa curl -v y observa los encabezados de solicitud del cliente).

Rpta:Lo que sucede es que la cookie solo se envia al servidor cuando el cliente lo especifica en la solicitud, es por eso que cuando hacemos el Get/ (curl -v 'http://esaas-cookie-demo.herokuapp.com') no especifimos alguna cookie (loggin_in = true) por lo tanto el servidor me responde como si no estuviera conectado

Ahora debemos decirle a curl que incluya las cookies apropiadas de este archivo cuando visite el sitio, lo cual hacemos con la opción -b:​
curl -v -b cookies.txt http://esaas-cookie-demo.herokuapp.com/
El resultado que se muestra el la flecha roja indica que la cookie ha sido enviado, y el servidor a respondido con un logged in: true

![Captura desde 2023-09-25 12-32-14](https://github.com/JuanSilva2000/HTTP-URI/assets/124120685/9fffc354-27a9-428d-aadd-62dfd21f269e)

Pregunta: Al observar el encabezado Set-Cookie o el contenido del archivo cookies.txt, parece que podría haber creado fácilmente esta cookie y simplemente obligar al servidor a creer que ha iniciado sesión. En la práctica, ¿cómo evitan los servidores esta inseguridad?

-Autenticación basada en token, cuando un usuario inicia sesion luego un servidor de autorización valida esa autenticación inicial y luego emite un token de acceso, que es un pequeño dato que le permite a una aplicación de cliente realizar una llamada o señal segura a un servidor API, de esta manera el token funciona como un boleto de acceso para que el usuario accesa a todos los recursos, el ciclo de vida del token finaliza cuando el usuario cierra sesion/abandoa sesión [5]
