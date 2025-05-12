# 🚀 DevOps VProfile Project v2

# Introducción

## 🧱 VProfile Project - Configuración Local (Automatizado)

### 1.- 🎯 Esta es la versión 2 del proyecto de VProfile. En ésta version, a comparación con la anterior, se automatiza todo el proceso de aprovisionamiento.


#### 🎓 Explicación del Aprovisionamiento Automatizado con Vagrant

##### 📁 Carpeta `vagrant` en el repositorio

> **"Automated provisioning"**  
> Escoge la carpeta según tu sistema operativo:

-   💻 **Windows** o **Mac con chip Intel** ➡️ Usa la carpeta estándar.
    
-   🍎 **Mac con chip M1/M2** ➡️ Usa la carpeta específica para ARM.
    

----------

#### 🔍 Visualización desde VSCode

Clona este repositorio y:

1.  Abre el proyecto en **VSCode**.
    
2.  Navega a la carpeta de **aprovisionamiento automatizado**.
    
3.  Revisa el archivo `Vagrantfile`.
    

> 💡 _Es muy similar al usado en el aprovisionamiento manual, pero..._
> 
> 📌 **Cada VM ahora ejecuta un script adicional automáticamente.**

----------

#### 📜 Scripts individuales por VM

Cada VM tiene asociado un **script `.sh`** para su configuración. Ejemplos:

-   `DB01` ejecuta 👉 `mysql.sh`
    
-   En esa misma carpeta está el archivo `mysql.sh`
    

💬 _“No te preocupes, son scripts de Bash bastante simples.”_

----------

#### 🧪 Revisión de `mysql.sh`

-   Al inicio está el clásico _shebang_:
    

```bash
#!/bin/bash
```

-   Se declara una variable con la contraseña de MySQL.
    
-   Se instalan, inician y habilitan servicios como `mariadb`.
    
-   Luego se clona el código fuente y se ejecutan comandos SQL.
    

💡 Puedes usar este comando para ejecutar SQL desde el shell:

```bash
mysql -u usuario -p contraseña -e "CONSULTA_SQL"

```

----------

#### 🔥 Configuración de firewall

-   Al final del script se incluyen comandos para configurar el firewall.
    
----------

📌 En `tomcat.sh` se usa el comando `cat` para crear archivos de configuración directamente desde el script, ya que no se puede usar el editor VIM al automatizar:

```bash
cat <<EOT > /ruta/al/archivo
(contenido del archivo)
EOT
```

----------

#### 🔁 ¿Qué hace cada script?

1.  Crea archivos de sistema necesarios.
    
2.  Inicia y habilita servicios como `Tomcat`.
    
3.  Clona el código fuente.
    
4.  Ejecuta `mvn install`.
    
5.  Despliega el artefacto (WAR).
    
6.  Configura NGINX (`nginx.sh`) y desactiva el sitio por defecto.
