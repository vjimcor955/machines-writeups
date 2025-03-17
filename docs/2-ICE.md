# 2 - ICE

**Plataforma:** TryHackMe
**Dificultad:** Fácil
**OS:** Windows

## Herramientas Utilizadas

- Nmap
- Metasploit

## Reconocimiento

### Escaneo de Puertos

- 1 . Escanear la dirección ip con un escaneo simple

  ![57320a347b0d933e0e3c8f3a61baec4d.png](./_resources/57320a347b0d933e0e3c8f3a61baec4d.png)

- 2 . Escanear los puertos encontrados con un escaneo mas agresivo

  ![8d371956d907fa7190620a2d50de02d1.png](./_resources/8d371956d907fa7190620a2d50de02d1.png)

  Con esto podemos saber que se trata de una maquina con Windows Server 2008 y algunos servicios interesantes que se están ejecutando.

Investigando sobre Icecast descubrimos la siguiente [vulnerabilidad](https://www.cvedetails.com/cve/CVE-2004-1561/):

![715f80c5fcf63b13312f194288cefaf5.png](./_resources/d202b256ae1547d2ba6f4c06d5b03489)

## Explotación

### Vulnerabilidad 1

Explotaremos la vulnerabilidad a través de Metasploit.

### Proceso de Explotación

- 1 . Buscar el exploit en Metasploit y cargarlo

  ![27b398079ad77bca8450ced4f6d92016.png](./_resources/27b398079ad77bca8450ced4f6d92016.png)

- 2 . Configurar el exploit y lanzarlo

  ![c27920a32ade894f2d2622ed4fb92c70.png](./_resources/c27920a32ade894f2d2622ed4fb92c70.png)

## Escalada de Privilegios

Al entrar vemos que estamos registrados como el usuario _Dark_.

### Método Utilizado

Lanzamos un segundo escaneo que nos revelara mas exploits que podremos usar para escalar privilegios

![8e895c962abc8ab852bdfac22915d645.png](./_resources/8e895c962abc8ab852bdfac22915d645.png)

### Proceso de Escalada

- 1 . Cargamos el segundo exploit que se muestra, configuramos el numero de sesion de nuestra shell y lo lanzamos

  ![75351651b1ac82153c25c80b10c12b82.png](./_resources/75351651b1ac82153c25c80b10c12b82.png)

- 2 . Listar los procesos y migrarnos a uno con permisos de administrador

  ![b5da4215b480b42f157e519757161ba2.png](./_resources/b5da4215b480b42f157e519757161ba2.png)

  ![2647f73eb21ec9f02b67bd5b6e8d35cf.png](./_resources/2647f73eb21ec9f02b67bd5b6e8d35cf.png)

- 3 . Una vez somos administradores cargamos la herramienta kiwi para el volcado de contraseñas

  ![9ba6ad60d0b498140a52663b3105b5e8.png](./_resources/9ba6ad60d0b498140a52663b3105b5e8.png)
  ![4b2636f14d24b6920a274d6c23d03b97.png](./_resources/4b2636f14d24b6920a274d6c23d03b97.png)

Una vez obtenida la contraseña del usuario _Dark_, podríamos acceder a ella desde un escritorio remoto.

...

## Flags

Sin flags

---

![e0f8b3a1e252391eed5c90bba89a4adc.png](./_resources/e0f8b3a1e252391eed5c90bba89a4adc.png)

---

Writeup hecho por Víctor Jiménez Corada
