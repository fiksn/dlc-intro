# schnorr-intro
A gentle introduction to Schnorr signature scheme using Eliptic Curve Cryptograph (ECC)

It was invented by german mathematician Claus-Peter Schnorr. Unfortunately he patented the scheme in 1988 (patend expired in February 2008). So during the creation of Bitcoin it was "free", unfortunately the space lacked any kind of libraries. Therefore ECDSA scheme was used.

## Eliptic Curve Cryptography 101

An elliptic curve is defined by formula:

![equation](http://www.sciweavers.org/tex2img.php?eq=y%5E2%3Dx%5E3%2Bax%2Bb&bc=Black&fc=White&im=jpg&fs=12&ff=arev&edit=)

![image](ecc.png)

a and b are parameters that define the curve and are carefully tuned.

Secp256k1 curve used by Bitcoin (and others) has the formula

![equation](http://www.sciweavers.org/tex2img.php?eq=y%5E2%3Dx%5E3%2B7&bc=Black&fc=White&im=jpg&fs=12&ff=arev&edit=) (a = 0, b = 7) and looks like this:

![image](Secp256k1.png)

### Operations

We operate on points on the curve A, B, C, G, P (upper-case letters) all define points on the curve with an (x, y) coordinate.

#### Addition

We can define addition of two points A and B by drawing a line through those two points and where the line intersects the curve is the negative of the new point. After transposition over the x axis (y = 0) we get the actual result

![image](addition.gif)

The operation is commutative (A + B = B + A)

#### Multiplications with a scalar


## Schnorr signature scheme
