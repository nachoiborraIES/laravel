# Ejercicios propuestos - Parte 6

## Ejercicio 1

Sobre el proyecto **blog** de la sesión anterior, vamos a añadir estos cambios:

* Modifica el archivo `config/auth.php` para que el *provider* acuda al modelo correcto de usuario.
* Modifica el *factory* de usuarios para que los passwords se encripten con *bcrypt*. Para que sea fácil de recordar, haz que cada usuario tenga como password su mismo login encriptado. Ejecuta después `php artisan migrate:fresh --seed` para actualizar toda la base de datos.
* Crea un formulario de login junto con un controlador asociado, y las rutas pertinentes para mostrar el formulario o autenticar, como hemos hecho en el ejemplo para la biblioteca. Recuerda llamar "login" a la ruta que muestra el formulario de login. 
* En el controlador de posts, protege todas las opciones menos las de `index` y `show`.
* Añade una opción de *Login* en el menú de navegación superior, que sólo esté visible si el usuario no se ha autenticado aún
* Haz que sólo se muestren los enlaces y botones de crear, editar o borrar posts cuando el usuario esté autenticado. En ese mismo caso, haz que también se muestre una opción de *logout* en el menú superior, que deberás implementar.
* Finalmente, añade la funcionalidad de que el usuario autenticado sólo puede editar y borrar sus propios posts, pero no los de los demás usuarios.
  
## Ejercicio 2

Crea un proyecto desde cero llamado `pruebaAuth` con mecanismos de autenticación ya pre-incorporados. Una vez creado, sigue los pasos a continuación:

* Crea una base de datos llamada `pruebaAuth` en *phpMyAdmin*, y modifica el archivo `.env` del proyecto para que conecte con esa base de datos.
* Lanza las migraciones predefinidas para crear las tablas necesarias para la gestión de usuarios (`php artisan migrate:fresh`)
* Registra (empleando el formulario de registro) un par de usuarios con sus respectivas contraseñas.
* Crea un controlador llamado `ProtegidoController`, sin métodos. Define luego un método interno llamado `protegido` que simplemente devuelva el mensaje "*Bienvenido/a a la zona protegida*. Define una ruta llamada `protegido` en `routes/web.php`, protegida con autenticación. Comprueba que sólo puedes acceder a la ruta estando validado.

## Ejercicio 3

***Opcional***

Continuamos con el proyecto **blog** anterior. Sigue estos pasos para definir una autenticación basada en roles:

* Crea una nueva migración que modifique la tabla de *usuarios* para añadir un nuevo campo llamado *rol*, de tipo *string*. Asegúrate de que la migración sea de modificación, y no de creación de tabla. Después, ejecútala para crear el nuevo campo.
* Haz que alguno de los usuarios de la tabla tenga un rol de *admin* (edítalo a mano desde *phpMyAdmin*), y el resto serán de tipo *editor*.
* Crea un nuevo middleware llamado `RolCheck`, con una función que compruebe si el usuario tiene el rol indicado, como en el ejemplo visto antes en los apuntes. Regístralo adecuadamente en el archivo `App/Http/Kernel.php`, como se ha explicado.
* Modifica las vistas necesarias para que, si el usuario es de tipo *admin* pueda ver los botones de edición y borrado de cualquier post, aunque no sean suyos.
* Modifica los métodos `edit`, `update` y `destroy` de `PostController` para que redirijan a `posts.index` si el usuario no es administrador, o si no es el propietario del post a editar o borrar.

**¿Qué entregar?**

Como entrega de esta sesión deberás adjuntar lo siguiente: 

* Comprimir el proyecto **blog** con todos los cambios incorporados, y eliminando las carpetas `vendor` y `node_modules` como se explicó en las sesiones anteriores. Renombra el archivo comprimido a `blog_07.zip`.
* Comprimir el proyecto **pruebaAuth** (nuevamente sin las carpetas `vendor` y `node_modules`) como `pruebaAuth.zip`.

Entrega ambos archivos por separado en la tarea de la sesión, o bien comprimidos los dos en otro archivo ZIP llamado `sesion7.zip`.