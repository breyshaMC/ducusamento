---
sidebar_position: 1
---

# Manual para Script de Instalación
<h2>Docker | GitLab | Opción SSL | Opción SSH</h2>

<p><strong>Facturador PRO 4</strong></p>

<h3 class="anchor anchorWithStickyNavbar_LWe7" id="descripción">Descripción<a href="#descripción" class="hash-link" aria-label="Link directo Descripción" title="Link directo Descripción">​</a></h3>

<p>
Hemos elaborado un script para uso en instancias Linux con Ubuntu 18 o superior, este es un archivo que actualiza el sistema, instala las herramientas, sus dependencias y realiza todas las configuraciones previas, dejando el aplicativo listo para probar en menos de 20 minutos (siempre y cuando el dominio ya esté configurado hacia la instancia), su ejecución es muy sencilla.
</p>

<h2 class="anchor anchorWithStickyNavbar_LWe7" id="Requisitos">Requisitos<a href="#Requisitos" class="hash-link" aria-label="Link directo Requisitos" title="Link directo Requisitos">​</a></h2>

<ol>
  <li>
    <p>
    Tener acceso a su servidor, vps, máquina virtual o local via SSH, en las instalaciones que realizamos para AWS o Google Cloud, hacemos entrega del usuario, la IP del servidor y la clave ssh que puede ser un archivo .ppk o .pem, recuerde almacenarlas en su equipo local.
    </p>
  </li>
  <li>
    <p>
    Tener instalado una versión de ssh en su máquina para conectarse de manera remota, puede utilizar putty, filezilla o una consola terminal. para mayor información sobre el acceso SSH visite los siguientes manuales:

    <a href="https://docs.google.com/document/d/1PmQejvNd_dkXVm8DPUYlQTag0wvES46tMpxX3MPhkNY/edit#">guía para acceder con Putty (gestión de servidor)</a>.

    <a href="https://docs.google.com/document/d/1Xpri2102N4b5C-dG-FVPXW5ZWjEz5S4iDjpvl7Zwq2E/edit#">guía para acceder con Winscp (gestión de archivos con aplicación de escritorio)</a>.
    </p>
  </li>
  <li>
    <p>
    Si es posible configurar su dominio apuntando a su instancia para que al finalizar la instalación se encuentre disponible el aplicativo. Edite los récords A y CNAME donde A debe contener su IP y CNAME el valor * (asterisco) para que se tomen los subdominios registrados por la herramienta.
    <img src='https://renzteya.github.io/docu-documentos/assets/images/Ejemplo-67d6c810b11e40045dced1135b28fb13.JPG'></img>
    </p>
  </li>
  <li>
    En caso de contar con servicios instalados en su instancia como mysql, apache o nginx, debe detenerlos, ya que estos ocupan los puertos que pasarán a usar el aplicativo con los contenedores de Docker.
  </li>
</ol>

<h2 class="anchor anchorWithStickyNavbar_LWe7" id="Pasos">Pasos<a href="#Pasos" class="hash-link" aria-label="Link directo Pasos" title="Link directo Pasos">​</a></h2>

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
      Clonar el snippet de gitlab que contiene el script
    </p>
    `git clone https://gitlab.com/snippets/2079063.git script`
  </li>
  <li>
    <p>
      Ingrese a la carpeta clonada
      `cd script`
    </p>
  </li>
  <li>
    <p>
      Dar permisos de ejecución al script
      `chmod +x install.sh`
    </p>
  </li>
  <li>
    <p>
      El comando a utilizar para iniciar el despliegue requiere de un parámetro principalmente:
      
      `./install.sh [dominio]`

      por ejemplo:

      ```bash
      ./install.sh facturador.pro
      ```
    </p>    
  </li> 
  <li>
    <p>
    Una vez ejecutado el comando iniciará el proceso de actualización del sistema, en el proceso se le solicitará:
    </p>
    <p> 
      a. El usuario y contraseña de GitLab, para que se pueda descargar el proyecto en su instancia
    </p>
    <p> 
      b. Si desea instalar  SSL gratuito, tenga en cuenta que este debe ser actualizado cada 90 días, el mensaje será el siguiente:
      
      ```bash
      instalar con SSL? (debe tener acceso al panel de su dominio para editar/agregar records TXT). si[s] no[n]
      ```
      <p>
        i. Deberá contestar con “s” o “n” para continuar

        ii. Si selecciona `SÍ`, deberá contestar las siguientes preguntas con “y”, son 2 en total, seguidamente se le ofrecerá un código que debe añadir en un récord tipo TXT en su dominio quedando como `_acme-challenge.example.com` o simplemente `_acme-challenge` dependerá de su proveedor.
      </p>
    </p>
    <img src='https://renzteya.github.io/docu-documentos/assets/images/ejemplo2-403f0e6a263d96845a2bb295580a2dad.JPG'></img>
  </li>
    <p>
    iii. para continuar presione `enter`, luego deberá repetir las acciones para añadir un segundo código y habrá finalizado la configuración, si el proceso es exitoso la ejecución del script continuará.
    </p>
    <p>
    c. Si desea obtener y gestionar actualizaciones automáticas, deberá disponer de su sesión de gitlab al momento
    </p>
    ```bash
    configurar clave SSH para actualización automática? (requiere acceso a https://gitlab.com/profile/keys). si[s] no[n]
    ```
    <p>
      i. Deberá contestar con “s” o “n” para continua
    </p>
    <p>
      ii . De seleccionar `SÍ`, al final del despliegue se le dará un extracto de texto que debe añadir a su configuración de gitlab
    </p>
    <img src= 'https://jeremyabel710.github.io/Trabajo2/assets/images/ejemplo3-441dad1bc1a7317c4061c4c5c7bbe667.JPG'> </img>
    <li>
    Finalizado el script y dependiendo de sus selecciones anteriores, se le entregará varios datos que debe guardar, como:
      <ul>
        <li>
          usuario administrador
        </li>
        <li>
          contraseña para usuario administrador
        </li>
        <li>
          url del proyecto
        </li>
        <li>
          ubicación del proyecto dentro del servidor
        </li>
        <li>
          clave ssh para añadir a gitlab (obligatorio para quienes seleccionan la instalación de SSH)
        </li>
      </ul>
    </li>
</ol>

<h2 class="anchor anchorWithStickyNavbar_LWe7" id="Enlaces">Enlaces De Interes<a href="#Enlaces" class="hash-link" aria-label="Link directo Enlaces" title="Link directo Enlaces">​</a></h2>
<ul>
  <li>
    <a href="https://gitlab.com/b.mendoza/facturadorpro3/snippets/1955372">Actualización de SSL</a>.
  </li>
  <li>
    <a href="https://gitlab.com/b.mendoza/facturadorpro3/-/wikis/Script-Update-Docker">Actualización mediante ejecución Script para instalaciones Docker</a>.
  </li>
  <li>
    <a href="https://docs.google.com/document/d/1D87YJ9fq9yHiAauu6SGVugiC3m_i42DrFUt6VKYXuDI/edit?usp=sharing">Gestión de SSL independiente, no el que incorpora el Script</a>.
  </li>
  <li>
    <a href="https://gitlab.com/b.mendoza/facturadorpro3/snippets/1971490">Guía gitlab para la instalación, contiene el script usado en el presente manual</a>, además posee los parámetros extras que pueden usarse en la ejecución del paso 6   
  </li>
</ul>