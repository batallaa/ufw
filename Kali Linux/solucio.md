# Kali Linux

## 1. Requisits de la màquina

- 8 GB de RAM
- 8 Processadors
- 25 GB de disc dur
- Interfície: Adaptador Pont

![alt text](img/image.png)

## 2. Instal·lació Inicial

Al arrancar la màquina, ens preguntarà l'idioma. Seleccionem Català.

![alt text](img/image-2.png)

Seleccionem la localització. Seleccionem Espanya.

![alt text](img/image-3.png)

Posem el teclat en català.

![alt text](img/image-4.png)

Configurem la xarxa. En el meu cas utilitzaré l'ip:

```bash
192.168.4.4
```

![alt text](img/image-5.png)

Com a porta d'enllaç deixem la que ens posa per defecte:

```bash
192.168.4.1
```

Com a DNS utilitzem el determinat i introduïm el de google.

```bash
192.168.4.1
8.8.8.8
```

![alt text](img/image-6.png)

Introduïm el nom de màquina.

![alt text](img/image-7.png)

I després, introduïm el nom del domini.

![alt text](img/image-8.png)

Indiquem el nom d'usuari, i després la contrasenya.

![alt text](img/image-9.png)
![alt text](img/image-10.png)

Configurem la zona horària.

![alt text](img/image-11.png)

Indiquem que utilitzi el disc sencer.

![alt text](img/image-12.png)

Seleccionem la primera opció.

![alt text](img/image-13.png)

Pressionem tot següent i després esperem a que s'instal·li el sistema base.

![alt text](img/image-14.png)

## 3. Netdiscover

Un cop completada la instal·lació, ens demanarà iniciar sessió dins.

![alt text](img/image-15.png)

### 3.0 IP

Com aquesta tasca la faig amb el router de casa, utilitzaré el següent:

![alt text](img/image-23.png)

### 3.1 Mode actiu

Anem a netdiscover i introduïm la seguent comanda:

```bash
sudo netdiscover -i eht0 -r 192.168.1.0/24
```

![alt text](img/image-24.png)

### 3.2 Mode passiu

Anem a netdiscover i introduïm la seguent comanda:

```bash
sudo netdiscover -p
```

![alt text](img/image-25.png)

### 3.3 Diferències

En el mode actiu netdiscover envia paquets a tota la xarxa, mentre que el mode passiu netdiscover no envia res i només escolta el tràfic que ja hi havia anteriorment.

## 4. Nmap

Per repetir el mateix però amb l'explorador nmap introduïm la seguent comanda:

```bash
sudo nmap -sn 192.168.1.0/24
```

Això ens permet veure els equips ja actius sense mirar els ports.

![alt text](img/image-27.png)

### 4.1 Sistema d'equips detectats

Per detectar els equips amb els ports, hem d'introduir una sèrie de comandes més a la comanda:

```bash
sudo nmap -O -sV 192.168.1.1
```

![alt text](img/image-28.png)

## 5. Detecció de sistema operatiu i ports oberts

```bash
sudo nmap -O -sV 192.168.1.1
sudo nmap -O -sV 192.168.1.7
sudo nmap -O -sV 192.168.1.15
sudo nmap -O -sV 192.168.1.22
sudo nmap -O -sV 192.168.1.33
sudo nmap -O -sV 192.168.1.45
```

### 5.1 192.168.1.1

![alt text](img/image-29.png)

Ports oberts:
- 20 TCP
- 80 TCP
- 443 TCP

### 5.2 192.168.1.7

![alt text](img/image-30.png)

Ports oberts:
- 22 TCP
- 21 TCP
- 80 TCP

### 5.3 192.168.1.15

![alt text](img/image-31.png)

Ports oberts:

- 22 TCP
- 53 TCP
- 80 TCP

### 5.4 192.168.1.22

![alt text](img/image-32.png)

Ports oberts:
- 22 TCP
- 139 TCP
- 445 TCP

### 5.5 192.168.1.33

![alt text](img/image-33.png)

Ports oberts:
- 23 TCP
- 80 TCP
- 8291 TCP

### 5.6 192.168.1.45

![alt text](img/image-34.png)

Ports oberts:
- 22 TCP
- 80 TCP








