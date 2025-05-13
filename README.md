# 🚀 DevOps VProfile Monolithic Project v2

# Introducción

## 🧱 VProfile Project - Configuración Local (Aprovisionamiento Automatizado con Vagrant)

----------

### 📁 Carpeta `vagrant` y scripts por sistema operativo

-   Dentro del repositorio hay una carpeta llamada `vagrant`.
    
-   En ella encontrarás aprovisionamientos automatizados divididos por sistema operativo:
    
    -   💻 **Windows y MacOS con chip Intel** → usa la carpeta correspondiente.
        
    -   🍎 **MacOS con chip M1 o M2** → usa la otra carpeta disponible.
        

----------

### 🔍 Exploración del archivo `Vagrantfile`

-   Clona el codigo fuente en VSCode.
    
-   Al abrir el archivo `Vagrantfile`, verás que es similar al usado en el aprovisionamiento manual con una diferencia importante:  
    👉 Cada VM tiene asociado un **script de shell específico** que se ejecutará durante el aprovisionamiento.
    

----------

### 🖥️ Scripts de Shell para cada VM

Cada VM cuenta con un script `.sh` en la misma carpeta del `Vagrantfile`:

#### 📦 `mysql.sh` (para DB01)

-   Script simple de Bash que:
    
    -   Define una variable con la contraseña de la base de datos.
        
    -   Instala, inicia y habilita **MariaDB**.
        
    -   Clona el código fuente y despliega el esquema SQL.
        
    -   Si deseas ejecutar SQL desde shell:
        
        ```bash
        mysql -u usuario -p'contraseña' -e 'COMANDO_SQL'
        
        ```
        

#### 🧠 `memcache.sh`

-   Instalación y habilitación de Memcached.
    
-   Muy similar al script de MySQL.
    

#### 🐰 `rabbitmq.sh`

-   Instalación de RabbitMQ.
    
-   Incluye la instalación de Erlang, socat, etc.
    
-   También se inicia y habilita el servicio.
    

#### 🧪 `tomcat.sh`

-   🐧 Específico para Ubuntu.
    
-   Crea archivos usando `cat <<EOT ... EOT` para evitar abrir editores como `vim`.
    
-   Ejecuta:
    
    -   Instalación de Tomcat.
        
    -   Clonación de código fuente.
        
    -   Ejecución de `mvn install`.
        
    -   Despliegue del artifact.
        

#### 🌐 `nginx.sh`

-   Instala NGINX.
    
-   Crea el archivo de configuración.
    
-   Desactiva el sitio por defecto y activa el nuevo.
    
-   Inicia y habilita el servicio.
    
----------

## ▶️ Ejecución de `vagrant up`

1.  Abre **Git Bash**.
    
2.  Navega al directorio:
    
    ```bash
    cd ruta/al/codigo/vagrant/aprovisionamiento-automatizado
    ```
    
3.  Ejecuta:
    
    ```bash
    vagrant up
    ```
    

----------

### 🚀 Flujo de aprovisionamiento automatizado

1.  🔄 **`vagrant up`** inicia la creación de todas las VMs.
    
2.  🕒 Espera a que cada máquina esté estable antes de ejecutar su script.
    
3.  🟢 Se ejecutan los scripts en este orden:
    
    -   `mysql.sh` ✅
        
    -   `memcache.sh` ✅
        
    -   `rabbitmq.sh` ✅ (más lento por `yum update` y dependencias)
        
    -   `app01` con build de Maven ✅
        
    -   `web01` con NGINX ✅
        

> ⏳ El tiempo total de ejecución puede variar entre 15 y 30 minutos, dependiendo de tu velocidad de Internet.

----------

## 🌐 Validación desde el navegador

Puedes acceder a la aplicación vía:

```
http://web01
```

> O bien, usar la IP estática definida en el `Vagrantfile`.

1.  Inicia sesión:
    
    -   Usuario: `admin_vp`
        
    -   Contraseña: misma usada en el script
        
2.  ✅ Valida los componentes:
    
    -   Base de datos (MySQL)
        
    -   RabbitMQ
        
    -   Memcached (se insertan datos en caché y se validan)
        

----------

## 🧹 Apagar y reiniciar la pila

-   Detener todas las VMs:
    
    ```bash
    vagrant halt
    ```
    
-   Ver el estado:
    
    ```bash
    vagrant status
    ```
    
-   Levantar nuevamente:
    
    ```bash
    vagrant up
    ```
    

> ⚠️ El aprovisionamiento solo ocurre la primera vez que se crean las VMs.

----------

## 🔁 Conclusión

✅ Con un solo comando (`vagrant up`), aprovisionamos toda la pila de forma:

-   🔄 Repetible
    
-   ⚙️ Automatizada
    
-   🧾 Definida como **infraestructura como código**
    

----------
