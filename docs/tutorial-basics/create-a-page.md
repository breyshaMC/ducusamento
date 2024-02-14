---
sidebar_position: 2
---

# Manual de Instalación
<h2>Docker + GitLab + SSL</h2>

<p><strong>PRO 1 | PRO 2</strong></p>

<h3 class="anchor anchorWithStickyNavbar_LWe7" id="descripción">Descripción<a href="#descripción" class="hash-link" aria-label="Link directo Descripción" title="Link directo Descripción">​</a></h3>

<p>Hemos elaborado un script para uso en instancias Linux, este es un archivo .sh que actualiza el sistema, instala las herramientas, sus dependencias, configura un certificado SSL renovable cada 90 días que debe ser confirmado en el proceso con su dominio y realiza todas las configuraciones previas, dejando el aplicativo listo para probar en menos de 20 minutos , su ejecución es muy sencilla.</p>

<h3 class="anchor anchorWithStickyNavbar_LWe7" id="Requisitos">Requisitos<a href="#Requisitos" class="hash-link" aria-label="Link directo Requisitos" title="Link directo Requisitos">​</a></h3>

<ul>
  <li>
    <p>
      Tener acceso a su servidor, vps, máquina virtual o local via SSH, en las instalaciones que realizamos para AWS o Google Cloud, hacemos entrega del usuario, la IP del servidor y la clave ssh que puede ser un archivo .ppk o .pem.
    </p>
  </li>
  <li>
    <p>
      Tener instalado una versión de ssh en su máquina para conectarse de manera remota, puede utilizar putty, filezilla o una consola terminal.
    </p>
  </li>
    <li>
    <p>
      Es importante configurar su dominio apuntando a la IP de su instancia para que durante la ejecución del script se valide el certificado SSL y al finalizar la ejecución no tenga errores y todo esté listo para realizar pruebas. Edite los récords A y CNAME donde A debe contener su IP y CNAME el valor * (asterisco) para que se tomen los subdominios registrados por la herramienta.
      <img src="https://renzteya.github.io/docu-documentos/assets/images/Ejemplo-67d6c810b11e40045dced1135b28fb13.JPG"></img>
    </p>
  </li>
  <li>
    <p>
      Durante la ejecución del script deberá almacenar en su dominio dos registros TXT con unos valores que se mostrarán en pantalla, estos registros son validados en directo y no pueden tardar más de 2 minutos en validarse en su dominio.
    </p>
  </li>
  <li>
    <p>
      En caso de contar con servicios instalados en su instancia como mysql, apache o nginx, debe detenerlos, ya que estos ocupan los puertos que pasarán a usarse con el aplicativo y los contenedores de Docker.
    </p>
  </li>
</ul>
<h3 class="anchor anchorWithStickyNavbar_LWe7" id="Pasos">Pasos<a href="#Pasos" class="hash-link" aria-label="Link directo Pasos" title="Link directo Pasos">​</a></h3>

<ol>
  <li>
    <p>
      Acceder a su instancia vía `SSH`.
    </p>
  </li>
  <li>
    <p>
      Loguearse como super usuario 
      ejecute `sudo su`
    </p>
  </li>
  <li>
    <p>
      Ubicarse en la carpeta del usuario, por ejemplo:
    </p>
      ```bash
      cd /home/ubuntu/
        ```
  </li>
  <li>
    <p>
      Crear el archivo install ejecute:
    </p>
      ```bash
      touch install.sh
        ```
  </li>
  <li>
    <p>
      Editar el archivo con su editor preferido ejecute:
    </p>
      ```bash
      nano install.sh
        ```
  </li>
  <li>
    <p>
      En el archivo debe agregar el contenido del siguiente enlace:
      ```bash
      https://gitlab.com/snippets/1852652
      ```
      Observará a una página como la siguiente, donde debe copiar el contenido del script y pegarlo en su archivo install.sh, es importante que mantenga las estructura del mismo.
    </p>
    <img src='https://renzteya.github.io/docu-documentos/assets/images/ejemplo4-fcee64145ad4010ac2331a3b5b094bd9.JPG'></img>
  </li>
  <li>
    <p>
    Para salir de editor y guardar puede presionar `Ctrl + X` seguidamente se le consultará si desea guardar los cambios, confirme con `Y` y luego `Enter`.
    </p>
  </li>
    <li>
      <p>
        Debe darle permisos de ejecución al archivo:
        ```bash
        ejecute chmod +x install.sh
        ```
      </p>
  </li>
  <li>
    <p>
      El comando a utilizar requiere de dos parámetros principalmente:
      
      `./install.sh [repositorio] [dominio]`

      Por ejemplo:
      
      ```bash
      ./install.sh https://gitlab.com/rash07/facturadorpro2 elfacturador.com
      ```
    </p>
  </li>
  <li>
    <p>
    Una vez ejecutado el comando se iniciará un proceso donde debe ir aceptando las preguntas y que le mostrará en pantalla los valores que debe añadir en los 2 récords tipo TXT de su dominio con nombre.
    </p>
    <p> 
      a. <strong>_acme-challenge.example.com</strong> 
    </p>
    <p>
      b. <strong>_acme-challenge</strong> (casos como godday y puntope)
    </p>
    <p>
      En la siguiente imagen le muestran el valor como `v703JW....` debera copiarlo y añadirlo al primer record TXT, seguidamente pulsar enter, se le mostrará en pantalla un segundo valor para el segundo TXT.
    </p>
    <img src='https://renzteya.github.io/docu-documentos/assets/images/ejemplo2-403f0e6a263d96845a2bb295580a2dad.JPG'></img>
  </li>
  <li>
    <p>
      Editados los récords en su dominio, deberá aceptar para continuar y que el proceso verifique que sea exitoso, de ser exitoso obtendrá una pantalla similar a la siguiente.
    </p>
    <img src='https://renzteya.github.io/docu-documentos/assets/images/ejemplo5-710a1632712f24f2fbcf5001fe8ca4fc.JPG'></img>
  </li>
  <li>
    <p>
      Continuará el proceso de actualización del sistema, se le solicitará el usuario y contraseña de GitLab, para que se pueda clonar/descargar el proyecto en su instancia, luego culminará y tendrá los accesos listos en su dominio:
      ```bash
      Correo: admin@gmail.com
      Contraseña: 123456
      ```
    </p>
  </li>
</ol>
<p>
Una vez finalizado, puede proseguir con el manual de pruebas o demás documentación de cada proyecto, sus URL son:
</p>
<p>
  PRO 1: 
  https://gitlab.com/rash07/facturadorpro1
</p>
<p>
  PRO 2:
  https://gitlab.com/rash07/facturadorpro2
</p>

<h3 class="anchor anchorWithStickyNavbar_LWe7" id="Recomendaciones">Recomendaciones<a href="#Recomendaciones" class="hash-link" aria-label="Link directo Recomendaciones" title="Link directo Recomendaciones">​</a></h3>

<ul>
  <li>
    <p>
      Luego de instalar el facturador puede cambiar algunos parámetros en el archivo .env como:
      <ul>
        <li>
          <p>
          La dirección de envío de correos que utiliza el facturador para enviar los archivos pdf, xml y cdr a  sus clientes.
          </p>
        </li>
        <li>
          <p>
          Cambiar algunas configuraciones de plantillas de los pdf.
          </p>
        </li>
        <li>
          <p>
          Entre otros...
          </p>
        </li>
      </ul>
    </p>
  </li>
  <li>
    <p>
    Recuerde que siempre que se edita el archivo .env debe utilizar el comando “php artisan config:cache” dentro del contenedor de fpm1, para más detalles puede observar el manual de actualización <a href="https://docs.google.com/document/d/11PI1a9yjCPfH9CCuWmJSrdj1V8IEUffqurqvdkw29co/edit?usp=sharing">aquí</a>.
    </p>
  </li>
  <li>
    <p>
    La ruta donde ejecute el script será donde se clone el repositorio, debe verificar que los usuarios del servidor tengan permisos a dicha ruta si desea acceder desde ftp o scp.
    </p>
  </li>
</ul>
