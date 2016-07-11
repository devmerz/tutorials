---
layout:	post
title: "Tutorial: Java Web Start"
categories: tutorial javaWebStart java jnlp  
---

**Un poco de teoria**


>El software de Java Web Start permite descargar y ejecutar aplicaciones Java desde la Web.


* Permite activar las aplicaciones con un simple clic
* Garantiza que se está ejecutando la última versión de la aplicación
* Elimina complejos procedimientos de instalación o actualización
* Se puede colocar una sola aplicación Java en un servidor web para su despliegue en una amplia variedad de plataformas, incluyendo Windows, Linux y Solaris.
* Los usuarios pueden crear un acceso directo del escritorio para iniciar una aplicación Java Web Start fuera de un navegador.

Entonces, Java Web Start permite ejecutar aplicaciones Java dando un click a un enlace, dicho enlace apunta hacia un archivo  `JNLP`, el archivo  `.jnlp` tiene instrucciones para descargar y correr la aplicacion Java.

**Crear el archivo .jnlp**

Crearemos un archivo llamado  `lanzador.jnlp` en el escritorio, con las siguientes configuraciones.


{% highlight Java %}

<?xml version="1.0" encoding="utf-8"?> 
<jnlp spec="1.0+" codebase="http://localhost:8080/" href="Test.jnlp">
	<information>
		<title>Archivo JNLP</title>
		<vendor>Propietario</vendor>
	</information>
	<security>
		<all-permissions/>
	</security>
	<resources>
		<j2se version="1.6+" />
		<jar href="MiAplicacion.jar" />
	</resources>
	<application-desc
         name="Mi Aplicacion"
         main-class="com.dez.ApplicacionJava"
         width="300"
         height="300">
     </application-desc>
     <update check="background"/>
</jnlp>
{% endhighlight %}

Recuerda que estas configuraciones son muy importantes.

**Archivo .jar**

Para este ejemplo simple el .jar que se ejecutara sera un mensaje "Hola JWS"

![My helpful screenshot]({{ site.url }}/assets/jar.png)

**Firmar el .jar**

{% highlight Java %}
keytool -genkey -keystore Keys -alias exampleJws
{% endhighlight %}

- Nos pedira una contrasena.
- Cu?les son su nombre y su apellido?
- Cu?l es el nombre de su unidad de organizaci?n?
- Cu?l es el nombre de su organizaci?n?
- Cu?l es el nombre de su ciudad o localidad?
- Cu?l es el nombre de su estado o provincia?
- Cu?l es el c?digo de pa?s de dos letras de la unidad?
- Introduzca la contrase?a de clave para <exampleJws> (INTRO si es la misma contrase?a que la del almac?n de claves):

**Asigancion Keystore a .jar**

{% highlight Java %}
jarsigner -keystore Keys HolaMundo.jar exampleJws 
{% endhighlight %}

Nos pedira la contrasena del **keystore**


**Probando desde terminal**

Una manera rapida de saber si nuestro .jnlp esta bien configurado es probarlo desde terminal. Abrimos una y nos dirigimos a la ruta donde esta el archivo `lanzador.jnlp` y ejecutamos lo siguiente.



{% highlight Java %}
javaws lanzador.jnlp
{% endhighlight %}

**Enlaces de referencia**


[https://docs.oracle.com/javase/tutorial/deployment/webstart/](https://docs.oracle.com/javase/tutorial/deployment/webstart/)

[https://docs.oracle.com/javase/tutorial/deployment/webstart/deploying.html](https://docs.oracle.com/javase/tutorial/deployment/webstart/deploying.html)

