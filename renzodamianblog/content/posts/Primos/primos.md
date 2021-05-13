---
title: "Generar Primos en python"
date: 2021-05-12T21:09:31-05:00
description: "Los números primos son esenciales en la criptografía ya que son ellos los que se encargan de dar seguridad a los datos encriptados, su generación rápida y eficaz permite encriptar datos al instante logrando ser parte de varias aplicaciones del día a día (whatsapp, facebook, criptomonedas,twitter..)"
---

Los números primos son esenciales en la criptografía ya que son ellos los que se encargan de dar seguridad a los datos encriptados, su generación rápida y eficaz permite encriptar datos al instante logrando ser parte de varias aplicaciones del día a día (whatsapp, facebook, criptomonedas,twitter..).

Pero, **cómo se generan números primos de forma rápida?**

## Fermat little Theorem

Fermat demostró que **p **es primo si para todo **a **dentro de **1<a<p **se cumple que **a^(p-1) mod p = 1.**

![](https://cdn-images-1.medium.com/max/2000/1*1rItGKOLDAgwc_9hQfBXrg.png)

En python se escribiría así:

![](https://cdn-images-1.medium.com/max/2812/1*5fVNvgigCK_txJyai1y2sg.png)

Sin embargo, existen 2 problemas:

* Existen los llamados **Carmichael numbers** que son números que pasan el test de Fermat pero no son primos.

* Si queremos comprobar que un número es primo, el programa tiene que probar todas las **a **dentro del espectro 1<a<p-1 y si el número **p** tiene 15 cifras y es primo el programa tiene que realizar 10¹⁵ operaciones. Que ,incluso para una computadora potente, tomaría unos **20 minutos**.

<iframe src="https://medium.com/media/9c0a0b4e1efd7a08a667e4e18c403fdf" frameborder=0></iframe>
> Si queremos generar números primos grandes Fermat tomaría demasiado tiempo.

## Test de probabilidad Miller-Rabin

Miller y Rabin descubrieron la siguiente teoría basada en el teorema de Fermat que simplifica las operaciones por realizar pero la teoría es más compleja.

1. Generamos un número **n** que sea impar.

1. Hallamos **s** y **r** tal que **n-1 = 2^s * r**

1. Escogemos aleatoriamente un **a** entre **<1**,**n]**

1. **n** es un primo potencial si se cumple **a^r mod n =1** o **a^((2^j) * r) mod n = n-1**para algun j entre **0<j<s**. 

1. Si no se cumple ningunas de las dos condiciones entonces **n es compuesto**

Si pasa el test entonces hay una posibilidad de 1/4 de que sea compuesto, por lo tanto, para asegurar el mínimo de probabilidad de que resulte compuesto, realizaremos el test 128 veces. Entonces la probabilidad que sea compuesto se reduce a 0,25¹²⁸.

![Por esta razón es el algoritmo más usado en criptografía](https://cdn-images-1.medium.com/max/2000/1*k9Xp9kf-1ay-Ne_Nuil3mA.gif)*Por esta razón es el algoritmo más usado en criptografía*

Ejemplo para hallar r y s:
> n = 29  
>r =29–1  
>r= 28/2=14 , s=1  
r= 14/2 = 7 , s=2 #7 no es divisible entre 2 entonces:  
r= 7, s = 2  
n-1 = 2^s * r  
29–1 = 2²*7

Ahora a programarlo:

![](https://cdn-images-1.medium.com/max/3596/1*0p-cw_BuRH5BYXu5TapzUw.png)

Con este algoritmo el número de iteraciones en el peor de los casos se reduce a **s-1** y es mucho más rápido.

Para generar nuestro número primo de 30 cifras o más, simplemente generamos un número aleatorio impar y lo validamos con el algoritmo, si resulta que el número es compuesto, se genera otro número y se repite el proceso hasta que el número generado sea primo.

<iframe src="https://medium.com/media/d8a66b22ebf9a6623ca4a3540d5139b4" frameborder=0></iframe>

Y así es cómo podemos generar números primos de 40, 50 o 60 cifras en un instante.
