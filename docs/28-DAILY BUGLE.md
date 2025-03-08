# 28 - Daily Bugle

## Escaneo de puertos

- Escaneo simple

```
sudo nmap 10.10.104.39 -sN
```

![a9d2b4054e1f8e57a7c5bd64789b7890.png](../_resources/a9d2b4054e1f8e57a7c5bd64789b7890.png)

- Escaneo agresivo

```
sudo nmap 10.10.104.39 -A -T4 -p 22 80 3306
```

![50ffa77e012d4099a62dac0135ac2418-copia.png](../_resources/50ffa77e012d4099a62dac0135ac2418-copia.png)

## Web

Al usar el addon Wappalyzer se puede ver que el gestor de contenidos de la pagina es Joomla:

![c950c221e0ff1fe91e46f15518df0d08.png](../_resources/c950c221e0ff1fe91e46f15518df0d08.png)

Obtener versión de Joomla a través de la herramienta **Joomscan**:

```
joomscan -u http://10.10.104.39
```

![03c53f6110f83495991abdf9bb626db6.png](../_resources/03c53f6110f83495991abdf9bb626db6.png)

Buscando vulnerabilidades para la versión 3.7.0 de Joomla encuentro la siguiente entrada en [exploit-db.com](https://www.exploit-db.com/):

![8f4ee980d9fc3a9483642aabf63a388e.png](../_resources/8f4ee980d9fc3a9483642aabf63a388e.png)

Buscando el CVE en internet llego al siguiente [repositorio](https://github.com/stefanlucas/Exploit-Joomla):

![ebb9a42f171c61c8757279890d55a1e3.png](../_resources/ebb9a42f171c61c8757279890d55a1e3.png)

Descargo el script de Python y exploto la vulnerabilidad:

![a33f434f2ba65211d5a6b517b5b0e2e7.png](../_resources/a33f434f2ba65211d5a6b517b5b0e2e7.png)
