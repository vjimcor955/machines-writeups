# 1 - Blue

- **Dificultad:** Fácil

## Herramientas Utilizadas

- Nmap
- Metasploit
- Hashcat

## Reconocimiento

### Escaneo de Puertos

1. Escanear la dirección ip con un escaneo simple

![109c21de116514491364ae58c92febbc.png](../_resources/109c21de116514491364ae58c92febbc.png)

2. Escanear los puertos encontrados con un escaneo mas agresivo 

![06c43778ae76ebd794ff6f1173ff4285.png](../_resources/06c43778ae76ebd794ff6f1173ff4285.png)

Con esto podemos saber que se trata de una maquina con Windows 7.

3. Lanzar un escaneo para detectar posibles vulnerabilidades

![2db2e90c8e64d58131519250e44b1a18.png](../_resources/2db2e90c8e64d58131519250e44b1a18.png)

Con esto podemos ver que la maquina es vulnerable al exploit **ms17-010**.

## Explotación

Para la explotación usare la herramienta Metasploit.

### MS17-010

1. Buscar el exploit en Metasploit

![619d2996687b37e7e8e3c0b4153a67e4.png](../_resources/619d2996687b37e7e8e3c0b4153a67e4.png)

2. Configurar los parámetros y el payload del exploit y lanzarlo

![f38ca0a0fa9b239b89d581c2c8818441.png](../_resources/f38ca0a0fa9b239b89d581c2c8818441.png)

![224dff66fda374647e5f51b337a2ef68.png](../_resources/224dff66fda374647e5f51b337a2ef68.png)

![bce22c53dae678b03a9a25161f3c89da.png](../_resources/bce22c53dae678b03a9a25161f3c89da.png)

## Escalada de Privilegios

### Método Utilizado

Para escalar privilegios mejorar la shell a una de meterpreter.

### Proceso de Escalada

1. Buscar información de que modulo usar para mejorar la shell

![ec1f7bf8111420fe50c93f0ceede14ce.png](../_resources/ec1f7bf8111420fe50c93f0ceede14ce.png)

2. Cargar, configurar y lanzar el modulo

![960681b580bfee89c31ef4ed459c3056.png](../_resources/960681b580bfee89c31ef4ed459c3056.png)

Esto crea una nueva sesión con la shell de meterpreter. 

3. Mirar proceso para escalar privilegios

Listar los procesos con ps y migrar el proceso a uno que se este ejecutando como NT AUTHORITY/SYSTEM

![f6d50970bab5568c3ab8742547af2adf.png](../_resources/f6d50970bab5568c3ab8742547af2adf.png)

Migro el proceso al proceso con id 668 ya que gestiona los servicios del sistema y es crucial para su funcionamiento.

![879696af58d8bebd70cee3bd4aed50fe.png](../_resources/879696af58d8bebd70cee3bd4aed50fe.png)

## Dumpeo

Obtener la contraseña del usuario no predeterminado y romperla

## Proceso

1. Ver los hashes de las contraseñas del sistema 

![b70559272cc63501898627f5cb730e8c.png](../_resources/b70559272cc63501898627f5cb730e8c.png)

2. Romper la contraseña

Para romper la contraseña usamos la herramienta Hashcat

![109b0e7fb5ff449fac811f0e1f3310d5.png](../_resources/109b0e7fb5ff449fac811f0e1f3310d5.png)
![a134510bf44143c4cc8aed1ecc614ce4.png](../_resources/a134510bf44143c4cc8aed1ecc614ce4.png)

## Flags

1. Flag 1

La primera flag se encuentra en el directorio root

![d9439b7825b2c9235e8d36dd9394e00a.png](../_resources/d9439b7825b2c9235e8d36dd9394e00a.png)

2. Flag 2

La segunda flag se encuentra donde se guardan las contraseñas en Windows, es decir, el directorio donde se encuentra el archivo SAM

![7f030616094f95e6f6e5795b9c76d07a.png](../_resources/7f030616094f95e6f6e5795b9c76d07a.png)
![163bc53c2930bb98110df9f25918759e.png](../_resources/163bc53c2930bb98110df9f25918759e.png)

3. Flag 3

La tercera flag se encuentra en el directorio de documentos del usuario

![56cca6f55187460d57510af547a040b7.png](../_resources/56cca6f55187460d57510af547a040b7.png)

---

![37be1cb052790bccaad71a867e5b3287.png](../_resources/37be1cb052790bccaad71a867e5b3287.png)

---

Writeup hecho por Víctor Jiménez Corada