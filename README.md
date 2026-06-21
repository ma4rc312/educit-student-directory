
# Directorio de Estudiantes EDUCIT — Prueba Técnica INGENIA BPM

Solución al estudio de caso técnico: corrección de bugs y nueva funcionalidad de búsqueda en tiempo real.

---

## Errores encontrados y cómo los resolví

* **Bug 1 — CSS (error tipográfico):** El botón no tomaba ningún estilo porque la clase en el CSS estaba escrito como `.btn-primery` (con "e"), pero en el HTML el botón usaba `.btn-primary` (con "a"). El navegador nunca encontraba la regla. Lo resolví corrigiendo el nombre de la clase en el CSS para que coincidiera exactamente con el HTML.
* **Bug 2 — JavaScript (propiedades incorrectas del JSON):** Los usuarios no aparecían en pantalla porque el código accedía a `user.full_name` y `user.email_address`, propiedades que no existen en la respuesta de la API. La API de JSON devuelve los datos como `user.name` y `user.email`. Lo resolví corrigiendo los nombres de las propiedades en el `innerHTML`.
* **Bug 3 — SQL (sintaxis rota e inyección SQL):** La consulta original `INSERT INTO estudiantes (nombre, correo) VALUES (userName)` tenía dos problemas: declaraba dos columnas pero pasaba un solo valor en `VALUES`, lo cual genera un error en cualquier motor SQL y concatenaba una variable directamente en la consulta, abriendo la puerta a SQL Injection. Lo resolví usando una sentencia preparada: `INSERT INTO estudiantes (nombre, correo) VALUES (?, ?)` pasando los valores como parámetros externos, lo que separa los datos de la instrucción y elimina el riesgo de inyección.

---

## Nueva funcionalidad — Búsqueda en tiempo real

* Agregué un `<input type="search">` que filtra los usuarios por nombre a medida que el usuario escribe, sin recargar la página.
* Al cargar los usuarios, los guardo en una variable global `allUsers`. La función `handleSearch()` filtra sobre esa lista en memoria cada vez que cambia el input.
* El campo de búsqueda permanece oculto hasta que los usuarios se cargan exitosamente, para no confundir al usuario.
* Si el filtro no encuentra coincidencias, se muestra un mensaje informativo en lugar de una lista vacía.
