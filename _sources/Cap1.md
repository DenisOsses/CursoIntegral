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


### Ejercicios

```{code-cell}
:tags: [Fun2D]
:tags: [hide-input]
:mystnb:
:  code_prompt_show: "Mostrar el código fuente"
:  code_prompt_hide: "Ocultar el código"
import numpy as np
import matplotlib.pyplot as plt
from ipywidgets import interact, IntSlider, FloatSlider, Dropdown
from IPython.display import display

functions = {
        'x^2': lambda x: x**2,
        'sen(x)': lambda x: np.sin(x),
        'e^x': lambda x: np.exp(x),
        'cos(x)': lambda x: np.cos(x)
    }

def plot_riemann_sums(a, b, N, selected_function):
        f = functions[selected_function] # Get the selected function
        n = 10 # Use n*N+1 points to plot the function smoothly

        x = np.linspace(a, b, N+1)
        y = f(x)

        X = np.linspace(a, b, n*N+1)
        Y = f(X)

        plt.figure(figsize=(15, 5))

        plt.subplot(1, 3, 1)
        plt.plot(X, Y, 'b')
        x_left = x[:-1] # Left endpoints
        y_left = y[:-1]
        plt.plot(x_left, y_left, 'b.', markersize=10)
        plt.bar(x_left, y_left, width=(b-a)/N, alpha=0.2, align='edge', edgecolor='b')
        plt.title('Left Riemann Sum, N = {}'.format(N))

        plt.subplot(1, 3, 2)
        plt.plot(X, Y, 'b')
        x_mid = (x[:-1] + x[1:])/2 # Midpoints
        y_mid = f(x_mid)
        plt.plot(x_mid, y_mid, 'b.', markersize=10)
        plt.bar(x_mid, y_mid, width=(b-a)/N, alpha=0.2, edgecolor='b')
        plt.title('Midpoint Riemann Sum, N = {}'.format(N))

        plt.subplot(1, 3, 3)
        plt.plot(X, Y, 'b')
        x_right = x[1:] # Left endpoints
        y_right = y[1:]
        plt.plot(x_right, y_right, 'b.', markersize=10)
        plt.bar(x_right, y_right, width=-(b-a)/N, alpha=0.2, align='edge', edgecolor='b')
        plt.title('Right Riemann Sum, N = {}'.format(N))

        plt.show()

interact(plot_riemann_sums,
             a=FloatSlider(min=-10, max=10, step=0.1, value=0, description='a:'),
             b=FloatSlider(min=-10, max=10, step=0.1, value=5, description='b:'),
             N=IntSlider(min=1, max=50, step=1, value=10, description='N:'),
             selected_function=Dropdown(options=functions.keys(), value='x^2', description='Function:')
            );
```

```{admonition} Ejercicio 
Sea 
```