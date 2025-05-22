---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

<!--###########################################################################################################################
##############################################################################################################################
#############################################################################################
-->

+++

(U1)=
# Unidad 1

+++

## Introducción

**¿Cómo aproximaron $\pi$ los antiguos griegos?** Arquímedes (287 a.C.-212 a.C.) comenzó inscribiendo un héxagono regular en un círculo y calculando los perímetros de polígonos obtenidos al duplicar sucesivamente el número de lados hasta alcanzar los 96 lados.

```{figure} circunf_poligono.png
---
height: 200px
name: circunf_poligono
---
Aproximación por Polígonos Inscritos y Circunscritos
```

Esto le llevó a determinar que

$$
3\frac{10}{71}<\pi<3\frac{10}{70}
$$

Este procedimiento de inscribir y circunscribir polígonos regulares para aproximar un resultado se denomina **método exhaustivo**.

## Sumas de Riemann

Podemos aplicar el método exhaustivo para calcular el área $S$ que se encuentra bajo el gráfico de la función $y=f(x)$, cuando $x\in[a,b]$. 

```{figure} area1.png
---
height: 200px
name: area1
---
Área encerrada por el gráfico de $f$ en el intervalo $[a,b]$, cuando $f$ es positiva.
```

Por ejemplo, tratemos de aproximar el área encerrada por $y=f(x)=x^2$ cuando $x\in[0,1]$. 

```{figure} area2.png
---
height: 200px
name: area2
---
Área encerrada por el gráfico de $f(x)=x^2$ en el intervalo $[0,1]$.
```

Para ello dividimos o **particionamos** el intervalo $[0,1]$ en, por ejemplo, $8$ subintervalos del mismo ancho (**partición regular**)
 
$$
\Delta x=\dfrac{1-0}{8}=\dfrac{1}{8},~\text{subintervalos}~\left[0,\frac1{8}\right],\left[\frac1{8},\frac2{8}\right],\ldots,\left[\frac7{8},1\right]
$$ 

Luego, aproximamos el área encerrada usando **rectángulos** cuya base es el largo $\Delta x$ de cada subintervalo, y su altura corresponde a la función $f(x)$ evaluada en un **punto de muestra** de cada subintervalo (un punto particular cualquiera). Es común elegir el extremo izquierdo o derecho de cada subintervalo como punto de muestra, pero no son las únicas posibilidades.

```{figure} area3.png
---
height: 200px
name: area3
---
Suma inferior y suma superior.
```

La primera suma **inferior** se calcula usando los puntos donde la función alcanza sus valores mínimos (o ínfimos) y corresponden a los *puntos extremos izquierdos* de cada subintervalo. Así 

\begin{eqnarray*}
s_8&=&f\left(0\right)\cdot\frac1{8}+f\left(\frac{1}{8}\right)\cdot\frac1{8}+\cdots+f\left(\frac{7}{8}\right)\cdot\frac1{8}\\
&=& 0^2\cdot\frac1{8}+\left(\frac{1}{8}\right)^2\cdot\frac1{8}+\cdots+\left(\frac{7}{8}\right)^2\cdot\frac1{8}\\ 
&=&\frac{35}{128}=0.2734375
\end{eqnarray*}

La segunda suma **superior** se calcula usando los puntos donde la función alcanza sus valores máximos (o supremos) y corresponden a los *puntos extremos derechos* de cada subintervalo. Así 

\begin{eqnarray*}
S_8&=&f\left(\frac{1}{8}\right)\cdot\frac1{8}+f\left(\frac{2}{8}\right)\cdot\frac1{8}+\cdots+f\left(1\right)\cdot\frac1{8}\\
&=& \left(\frac{1}{8}\right)^2\cdot\frac1{8}+\left(\frac{2}{8}\right)^2\cdot\frac1{8}+\cdots+1^2\cdot\frac1{8}\\ 
&=&\frac{51}{128}=0.3984375
\end{eqnarray*}

¿Por qué solamente elegimos 8 subintervalos? ¿Es posible hacerlo con más, es decir, una cantidad arbitraria $n$ de ellos? La respuesta es que sí y  el procedimiento es completamente análogo a los cálculos anteriores: 

<!-- 
### Ejercicios

```{code-cell}
:tags: [Fun2D]
:tags: [hide-input]
:mystnb:
:  code_prompt_show: "Mostrar el código fuente"
:  code_prompt_hide: "Ocultar el código"
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

def f(x, y):
    return 4*x**2 + y**2  # Ejemplo de función

# Crear una malla de puntos en el espacio XY
x = np.linspace(-5, 5, 100)
y = np.linspace(-5, 5, 100)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)

# Crear la figura y los ejes en 3D
fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')

# Graficar la superficie
ax.plot_surface(X, Y, Z, cmap='viridis', edgecolor='none')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('f(x,y)')
ax.set_title('Gráfica de f(x,y)')

# Mostrar la gráfica
plt.show()
```

```{admonition} Ejercicio 
Sea $f(x,y)=\sqrt{1-2x^2-4y^2}$. ¿Cuál de las siguientes alternativas ilustra el $Dom(f)$?
``` -->
