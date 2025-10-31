
---

# ¿Qué es rockyou.txt?

**rockyou.txt** es una _wordlist_ (lista de contraseñas) formada originalmente a partir de los datos robados en la brecha de seguridad contra la compañía RockYou en 2009: los atacantes obtuvieron millones de contraseñas almacenadas en texto plano y esas contraseñas se publicaron y con el tiempo se convirtieron en una lista de uso común para pruebas y ataques. [Wikipedia](https://en.wikipedia.org/wiki/RockYou?utm_source=chatgpt.com)

# ¿Qué contiene y cuánto pesa?

La versión clásica contiene **millones de entradas** (la familia “rockyou” y sus derivados hablan de ~14 millones de contraseñas únicas en el set más usado), muchas repeticiones y numerosas contraseñas triviales (123456, password, nombres, combinaciones sencillas). Por eso es especialmente útil para detectar contraseñas débiles/ comunes. [Kaggle+1](https://www.kaggle.com/datasets/bwandowando/original-rockyou2024-text-file-11-parts?utm_source=chatgpt.com)

# ¿Dónde suele estar y cómo se obtiene?

En distribuciones orientadas a pentesting (p. ej. Kali Linux) suele venir empaquetado como `/usr/share/wordlists/rockyou.txt.gz` y se instala con el paquete de _wordlists_. Para usarlo hay que descomprimirlo (`gzip -d rockyou.txt.gz` o `gunzip`).

