***PROYECTO FINALIZADO***

# Sistemas escalables
## Primera étapa, sistema monólitico: 


### **Setup de las máquinas virtuales:**

En esta primera étapa, iniciamos creando dos máquinas virtuales (EC2) de manera individual y en estas máquinas desplegar una app básica con wordpress, estas máquina tenían asociadas una IP elástica para evitar que la IP fuese variando con el tiempo y pudiese asociarse adecuadamente a un DNS. También logramos asociarles un certificado SSL a estas máquinas virtuales.

**lastimosamente por razones ajenas, las máquinas dentro del curso fueron canceladas.**

Como estrategia alternativa, creamos nuevamente una máquina virtual para empezar a trabajar en el proyecto, alcanzamos a montarle nuevamente una aplicación wordpress, pero antes de añadirle el certificado SSL, **surgieron nuevos problemas con el acceso a la máquina, aunque esta vez no fue tumbada**, por estos incovenientes no tenemos pruebas de la configuración de la máquina en EC2.

### **Solicitud de dominio y administración del DNS:**

- Teniendo ya una máquina virtual funcionando con wordpress, utilizamos un dominio ofrecido por freenom "atenea.ml"

![freenom](images/img1.JPG)

- Luego de tener el dominio, nos registramos en cloudflare para asociarle este dominio, inicialmente registramos el sitio: 

![cloudflare](images/img2.JPG)

- Después de tener registrado el dominio, configuramos los registros DNS para que nuestro dominio resolviera la ip elástica de nuestra máquina virtual.

![DNS](images/img3.JPG)

- Finalmente, para poder que clodflare fuera el encargado de administrar este dominio, nos ofrecía dos DNS autoritarios, los cuales cambiamos en freenom, para que quedaran delegados a estos mismos. 

![autoritarios](images/img4.JPG)

![autoritariosCf](images/img5.JPG)


### **Características funcionales:**

A la hora de montar la estructura del WordPress, y pensando en los requisitos de lo que debía ser el sistema, “una comunidad de aprendizaje” en la cual se puedan crear grupos y compartir información entre estudiantes en diferentes materias de interés.

ATENEA implemento una red social de aprendizaje en la cual puedes contar con perfiles, grupos, interacción con otros usuarios, mensajería, entre otras funcionalidades, para esta se utilizó diversos pluggins de WordPress, entre ellos BUDDYPRESS para montar la red social, WOOSTIFY el cual es el tema inicial para que la vista sea un poco más agradable para el usuario, Activity Plus Reloaded for BuddyPress para subir archivos a los grupos y BuddyPress Edit Activity para realizar ediciones a los contenidos subidos previamente.  

Cabe mencionar que estos pluggins son iniciales para esta comunidad de aprendizaje y en futuras entregas se modificaran elementos para perfeccionar funcionalidades 

 

Por problemas de verificación y certificación SSL, por el momento tenemos el login por defecto en WordPress 

![wordpress](images/img6.jpg)

Tenemos un menú principal básico

![menu](images/img7.jpg)

En el menú GRUPOS tenemos los diferentes tipos de grupos creados por usuarios. 

![grupos](images/img8.jpg)

En los grupos podemos visualizar los miembros, administradores del grupo, un apartado de invitar al grupo, y los administradores pueden gestionar el grupo. 
Nota: podemos notar que se pueden subir archivos, videos y fotos al grupo, además del propietario poder editarlos. 

![gruposCaracteristicas](images/img9.jpg)

En el apartado miembros tenemos los diferentes usuarios que están en la plataforma, aquí se puede enviar la solicitud de amistad para así interactuar uno con el otro 

![miembros](images/img10.jpg)

En actividad están todas las interacciones que han realizado los usuarios, es algo similar al inicio de FACEBOOK 

![actividades](images/img11.jpg)


**Integrantes:**
- Juan Pablo Castaño Duque: jpcastand@eafit.edu.co
- Mateo Montes Loaiza: mmontesl1@eafit.edu.co

**URL:**
- www.atenea.ml
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Segunda étapa, sistema escalable: 

**Integrantes:**
- Juan Pablo Castaño Duque: jpcastand@eafit.edu.co
- Mateo Montes Loaiza: mmontesl1@eafit.edu.co

**URL:**
- www.ateneatest.tk

para la realizacion del sistema escalable, Atenea Interprise realizo una serie de pasos en las cuales tuve que crear diversos elemento los cuales se mencionaran en el siguiente documento.
inicialmente se creo un VPC en AWS el cual su principal mision es lanzar recursos de AWS en una red virtual, esta red es identica a las redes tradicionales que utilizan propios centros de datos, con los beneficios que supone utilizar la infraestructura escalable de AWS.

![WhatsApp Image 2021-05-20 at 14 04 43](https://user-images.githubusercontent.com/35698081/119044160-79c6f800-b97f-11eb-8a84-1d4558dab1f6.jpeg)

posteriormente se crean 4 tipos de subredes en las cuales encontramos 2 privadas y 2 publicas
![WhatsApp Image 2021-05-20 at 14 05 06](https://user-images.githubusercontent.com/35698081/119044329-b0047780-b97f-11eb-8a3d-6c1dfe681f05.jpeg)

### **route tables**
![WhatsApp Image 2021-05-20 at 14 05 29](https://user-images.githubusercontent.com/35698081/119044464-d5918100-b97f-11eb-8c9f-440ff7257104.jpeg)

### **se asocio el NAT con el SUBNET privado ya que por si solo no tiene salida a internet, este funciona como un intermediario para su conexión**
![WhatsApp Image 2021-05-20 at 14 06 11](https://user-images.githubusercontent.com/35698081/119044602-0671b600-b980-11eb-8162-727484d30865.jpeg)

### **montamos el internet gateways el cual es la conexion a internet de las cosas que hay en el vpc**
![WhatsApp Image 2021-05-20 at 14 06 23 (1)](https://user-images.githubusercontent.com/35698081/119044846-53558c80-b980-11eb-8c45-f2f4f6a4ce17.jpeg)

### **posteriormente se realiza la asociacion del internet gateway y el subnet**
![WhatsApp Image 2021-05-20 at 14 07 00](https://user-images.githubusercontent.com/35698081/119044922-68322000-b980-11eb-873a-5921b4cc1fbe.jpeg)

### **se crea el security Group**
![WhatsApp Image 2021-05-20 at 14 07 20](https://user-images.githubusercontent.com/35698081/119045030-8a2ba280-b980-11eb-9932-0be075e4e89f.jpeg)

### **se realiza las instancias NAT para permitir a las privadas acceso a internet**
![WhatsApp Image 2021-05-20 at 14 07 40](https://user-images.githubusercontent.com/35698081/119045212-c4953f80-b980-11eb-8065-6937d8cce69f.jpeg)

### **la funcionalidad del Bastion es ofrecer seguridad a la red interna, por lo que ha sido especialmente configurado para la recepción de ataques.**
![WhatsApp Image 2021-05-20 at 14 07 49](https://user-images.githubusercontent.com/35698081/119045395-07571780-b981-11eb-8a8f-0afb5692b4ae.jpeg)

### **Base de datos**
![WhatsApp Image 2021-05-20 at 14 08 19](https://user-images.githubusercontent.com/35698081/119045417-0f16bc00-b981-11eb-991e-b9a0d9af583f.jpeg)

### **Sistema de archivos**
![WhatsApp Image 2021-05-20 at 14 08 34](https://user-images.githubusercontent.com/35698081/119045548-3bcad380-b981-11eb-8233-e7d75175259a.jpeg)

### **Web server, aqui se almacena la imagen (las plantillas por si se caen)**
![WhatsApp Image 2021-05-20 at 14 08 51](https://user-images.githubusercontent.com/35698081/119045661-5c932900-b981-11eb-8f62-e845538b52cd.jpeg)

### **El Balanceador de carga direcciona a un cliente al servidor web que se encuentre con mayor disponibilidad entre los que cuentan con el mismo contenido**
![WhatsApp Image 2021-05-20 at 14 09 08](https://user-images.githubusercontent.com/35698081/119045726-73398000-b981-11eb-9d3c-f5d1db229ee5.jpeg)

### **Configuración de lanzamiento para que posteriormente en Auto Scaling suba las maquinas**
![WhatsApp Image 2021-05-20 at 14 09 21](https://user-images.githubusercontent.com/35698081/119045825-92381200-b981-11eb-8fb4-f9abb31b7bc0.jpeg)

### **Auto scaling realiza la accion de subir las maquinas**
![WhatsApp Image 2021-05-20 at 14 09 34](https://user-images.githubusercontent.com/35698081/119045869-9e23d400-b981-11eb-9494-f37f6712643f.jpeg)

### **DNS almacenados en cloudflare**
![image](https://user-images.githubusercontent.com/35698081/119046721-a9c3ca80-b982-11eb-9a78-d89e86c79eb3.png)

### **certificado de seguridad SSL para demostrar al usuario final que la pagina a la cual ingresara es segura y confiable**
![image](https://user-images.githubusercontent.com/35698081/119047171-2f477a80-b983-11eb-96df-f779290952ea.png)

# CARACTERISTICAS FUNCIONALES

*SISTEMA DE LOGIN SSO*
![image](https://user-images.githubusercontent.com/35698081/119048364-c103b780-b984-11eb-88fd-b56ba642bdd5.png)

### **comunidad de aprendizaje**
A la hora de montar la estructura del WordPress, y pensando en los requisitos de lo que debía ser el sistema, “una comunidad de aprendizaje” en la cual se puedan crear grupos y compartir información entre estudiantes en diferentes materias de interés.

ATENEA implemento una red social de aprendizaje en la cual puedes contar con perfiles, grupos, interacción con otros usuarios, mensajería, entre otras funcionalidades, para esta se utilizó diversos pluggins de WordPress, entre ellos BUDDYPRESS para montar la red social, WOOSTIFY el cual es el tema inicial para que la vista sea un poco más agradable para el usuario, Activity Plus Reloaded for BuddyPress para subir archivos a los grupos y BuddyPress Edit Activity para realizar ediciones a los contenidos subidos previamente. 

*Existen diversos grupos los cuales tienen distintos tipos de interes, como se muestra en la imagen*

![image](https://user-images.githubusercontent.com/35698081/119049077-ba297480-b985-11eb-8727-e68bf429c58b.png)

*En estos grupos se pueden realizar publicaciones, montar imaneges, archivos, textos, videos entre otras* 

![image](https://user-images.githubusercontent.com/35698081/119049313-01176a00-b986-11eb-867d-ef1c5a6a6907.png)

*hay un apartado el cual muestra todos los miembros de la comunidad*

![image](https://user-images.githubusercontent.com/35698081/119049476-36bc5300-b986-11eb-9189-115ab401e6d9.png)

*Actividad reciente*
![image](https://user-images.githubusercontent.com/35698081/119049580-55bae500-b986-11eb-86ad-607c10e1ac94.png)

*Un apartado Perfil el cual se puede personalizar y se muestra notificaciones, solicitudes de amistad, comentarios de mis publicaciones, entre otras*

![image](https://user-images.githubusercontent.com/35698081/119049810-a16d8e80-b986-11eb-8f75-0ff9bf44b613.png)
