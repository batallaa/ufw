# UFW

## Especificacions de la màquina

- 8 GB RAM
- 4 Processadors
- 25 GB Disc Dur
- Interfícies: NAT i Host-Only

![alt text](img/image.png)

## Instal·lació

Instal·lem ssh i nginx:

```bash
sudo apt install ssh -y
sudo apt install nginx -y
```

![alt text](img/image-1.png)
![alt text](img/image-2.png)

Habilitem el firewall

```bash
sudo ufw enable
```

Després, comprovem l'estat

```bash
ufw status verbose
```

![alt text](img/image-3.png)

## Configuracions del Firewall

Definim el comportament del firewall per les connexions de negació (deny)

```bash
sudo ufw default deny
```

![alt text](img/image-4.png)

Configurem les connexions a aplicacions.

```bash
ufw app list
```

![alt text](img/image-5.png)

Després, donem permís a les aplicacions que vulguem.

```bash
sudo ufw allow ssh
sudo ufw allow "Nginx HTTPS"
```

![alt text](img/image-6.png)
![alt text](img/image-7.png)

Per permetre o denegar connexions a adreces determinades, introduïm la seguent comanda (exemple d'ip inventada):

**Per permetre la connexió:**
```bash
sudo ufw allow fromm 192.168.1.3
```

**Per denegar la connexió:**

```bash
sudo ufw deny from 192.168.1.2
``` 

**Per denegar totes les ips d'una xarxa:**

```bash
sudo ufw deny from 10.12.10.0/24
``` 

**Per denegar connexions d'adreces determinades:**

```bash
sudo ufw deny out to 192.168.14.23
```

![alt text](img/image-8.png)

Per combinar regles IP i port introduïm les seguents comandes:

**Per permetre connexió:**

```bash
sudo ufw allow 192.168.1.4 to any port 44
```

**Per denegar connexió:**

```bash
sudo ufw deny 136.132.0.0/16 to any port 22
```

**Per permetre connexió tcp però no udp:**

```bash
sudo ufw allow from 192.168.0.4 to any port 22 proto tcp
```

Podem veure les regles definides:

```bash
sudo ufw status numbered
```

![alt text](img/image-9.png)

Per eliminar una regla del firewall hem d'identificar el seu número:

```bash
sudo ufw status numbered
```

![alt text](img/image-10.png)

I després, introduïm la comanda amb el número per eliminar la regla.

```bash
sudo ufw delete [Numero]
```

![alt text](img/image-11.png)

## Activitats UFW

(Activitats fetes en terminal ssh)

## 1. Comprova l’estat del firewall i si cal habilita’l

Primer comprovem l’estat del firewall:

```bash
sudo ufw status verbose
```

![alt text](img/image-12.png)

Si el firewall està inactiu (`inactive`), l’habilitem amb:

```bash
sudo ufw enable
```

![alt text](img/image-13.png)

Tornem a comprovar l’estat:

```bash
sudo ufw status verbose
```

![alt text](img/image-14.png)

---

## 2. Mostra les regles que té definides. Quines són les regles per defecte?

Mostrem totes les regles definides:

```bash
sudo ufw status numbered
```

![alt text](img/image-15.png)

### Eliminar regles definides

Si hi ha regles creades, les eliminem deixant només el comportament per defecte.

Primer consultem els números:

```bash
sudo ufw status numbered
```

![alt text](img/image-16.png)

Eliminem les regles:

```bash
sudo ufw delete 1
sudo ufw delete 2
```

![alt text](img/image-17.png)

Comprovem de nou:

```bash
sudo ufw status numbered
```

![alt text](img/image-18.png)

---

## 3. Comprova la regla per defecte de deny pel trànsit d’entrada

Configurem la política per defecte d’entrada:

```bash
sudo ufw default deny incoming
```

![alt text](img/image-19.png)

Comprovem-ho:

```bash
sudo ufw status verbose
```

![alt text](img/image-20.png)

Ara intentem connectar-nos via SSH des de l’amfitrió:

```bash
ssh usuari@192.168.56.102
```

![alt text](img/image-21.png)

---

## 4. Aplica regla per defecte deny al trànsit de sortida

Configurem el trànsit de sortida:

```bash
sudo ufw default deny outgoing
```

![alt text](img/image-22.png)

Comprovem l’estat:

```bash
sudo ufw status verbose
```

![alt text](img/image-23.png)

Ara provem de fer ping a Google:

```bash
ping google.com
```

![alt text](img/image-24.png)

---

# Activitats-II

## 5. Aplica regla per defecte allow al trànsit de sortida

Permetem el trànsit de sortida:

```bash
sudo ufw default allow outgoing
```

![alt text](img/image-25.png)

Comprovem-ho:

```bash
sudo ufw status verbose
```

![alt text](img/image-26.png)

Provem de nou el ping:

```bash
ping google.com
```

![alt text](img/image-27.png)

---

## 6. Crear una regla per prohibir el trànsit cap a capgros.elnacional.cat

Creem la regla:

```bash
sudo ufw deny out to capgros.elnacional.cat
```

![alt text](img/image-28.png)

Si no funciona per DNS, primer obtenim la IP:

```bash
ping capgros.elnacional.cat
```

![alt text](img/image-29.png)

---

## 7. Habilita el trànsit d’entrada pel servei nginx per la IP de l’amfitrió (192.168.56.1)

Permetem només l’accés HTTP des de l’amfitrió:

```bash
sudo ufw allow from 192.168.56.1 to any port 80 proto tcp
```

![alt text](img/image-30.png)

Comprovem les regles:

```bash
sudo ufw status numbered
```

![alt text](img/image-31.png)

Des de l’amfitrió obrim el navegador i introduïm l'IP

Hauria d’aparèixer la pàgina per defecte de Nginx.

![alt text](img/image-32.png)

---

## 8. Mostra el conjunt de regles definides

Finalment mostrem totes les regles configurades:

```bash
sudo ufw status numbered
```

![alt text](img/image-33.png)

També podem veure informació detallada:

```bash
sudo ufw status verbose
```

![alt text](img/image-34.png)