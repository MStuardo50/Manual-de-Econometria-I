---
title: "Manual de Econometría I"
author: "Joakina Quezada & Maximiliano Stuardo"
date: "2026-08-11"
site: bookdown::bookdown_site
documentclass: book
geometry: "left=2.5cm, right=2.5cm, top=2.5cm, bottom=2.5cm"
description: "Manual práctico de Econometría I"
---



# Sobre los Autores {-}

<div style="display: flex; gap: 20px; flex-wrap: wrap; margin-top: 20px;">

<div style="flex: 1; min-width: 280px; background-color: #f8fafc; padding: 20px; border-radius: 12px; border-left: 5px solid #0284c7; box-shadow: 0 2px 8px rgba(0,0,0,0.08); display: flex; gap: 15px; align-items: center;">
<img src="https://github.com/identicons/joakina.png" alt="Joakina Quezada" style="width: 140px; height: 140px; object-fit: cover; border-radius: 8px; border: 3px solid #0284c7; flex-shrink: 0;"/>
<div>
<h3 style="margin: 0 0 8px 0; color: #0f172a; font-size: 1.1em;">Joakina Quezada Mejía</h3>
<p style="margin: 0 0 6px 0; color: #334155; font-size: 0.9em; font-weight: 600;">Estudiante de Ingeniería Comercial mención Economía / Macroeconometrista.</p>
<p style="margin: 0; color: #64748b; font-size: 0.85em;"><strong style="color: #0284c7;">Áreas de interés:</strong> Macroeconomía, Variables Macroeconómicas.</p>
</div>
</div>

<div style="flex: 1; min-width: 280px; background-color: #f8fafc; padding: 20px; border-radius: 12px; border-left: 5px solid #0284c7; box-shadow: 0 2px 8px rgba(0,0,0,0.08); display: flex; gap: 15px; align-items: center;">
<img src="https://github.com/MStuardo50.png" alt="Maximiliano Stuardo" style="width: 140px; height: 140px; object-fit: cover; border-radius: 8px; border: 3px solid #0284c7; flex-shrink: 0;"/>
<div>
<h3 style="margin: 0 0 8px 0; color: #0f172a; font-size: 1.1em;">Maximiliano Stuardo Marticorena</h3>
<p style="margin: 0 0 6px 0; color: #334155; font-size: 0.9em; font-weight: 600;">Estudiante de Ingeniería Comercial mención Economía / Microeconometrista.</p>
<p style="margin: 0; color: #64748b; font-size: 0.85em;"><strong style="color: #0284c7;">Áreas de interés:</strong> Microeconomía, Organización Industrial, Derecho de la Competencia.</p>
</div>
</div>

</div>

<br>

# Introducción: ¿Qué es la Econometría? {-}

## Definición de Econometría

La econometría es la disciplina que combina la teoría económica, la estadística y las matemáticas para analizar datos económicos y probar hipótesis. Su objetivo principal es cuantificar relaciones económicas y hacer predicciones basadas en modelos matemáticos.

## Importancia de la Econometría

La importancia de la econometría radica en su capacidad para proporcionar herramientas que permiten a los economistas y analistas tomar decisiones informadas. A través del análisis de datos, la econometría ayuda a:

1. Evaluar políticas económicas.
2. Predecir tendencias económicas.
3. Identificar relaciones causales entre variables económicas.


## Correlación y Causalidad

Es fundamental entender la diferencia entre correlación y causalidad en econometría. La correlación indica que dos variables están relacionadas, pero no necesariamente que una cause la otra. La causalidad, por otro lado, implica que un cambio en una variable provoca un cambio en otra.

Entonces, correlación no implica por ningún motivo causalidad. Por ejemplo, si observamos que el consumo de helado y los casos de insolación aumentan durante el verano, podemos decir que hay una correlación entre estas dos variables. Sin embargo, no podemos concluir que comer helado cause insolación; ambos fenómenos están relacionados con la temporada de verano.

<!--chapter:end:index.Rmd-->

# Regresión Lineal Simple

## Definición

Un modelo de Regresión Lineal Simple es aquel modelo en donde nosotros deseamos observar el impacto que tiene una variable independiente (o regresor) $X$ en nuestra variable dependiente (o regresada) $Y$. De manera poblacional, el un modelo de regresión lineal simple se construye de la siguiente manera:

$$
Y = \beta_0 + \beta_1X + \varepsilon
$$

Donde tendremos a $\beta_0$ como intercepto, $\beta_1$ como la pendiente de esta recta y por último un término de error $\varepsilon$ que interpretaremos más adelante.

La idea de hacer esto es la siguiente:


```
## `geom_smooth()` using formula = 'y ~ x'
```



\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-1-1} \end{center}

Teniendo un set de datos donde tenemos muchos puntos dispersos (podrían ser muestras pequeñas, o muestras enormes), intentaremos encontrar la recta que \textbf{minimiza la suma cuadrática de los errores}. En primer lugar, se hace con el cuadrado de los errores ya que la suma de los errores es cero. (Ver demostración en Anexo). Y en segundo lugar, minimizar la suma cuadrática de los errores es, ajustar la recta para que los errores que cometemos en nuestra estimación no sean ni tan grandes, ni tan pequeños, definiendo así el método de estimación por \textbf{Mínimos Cuadrados Ordinarios (MCO)}. Los estimadores para $\hat{\beta_0}$ y $\hat{\beta_1}$ son (revisar demostración en Anexo):

$$
\hat{\beta_0} = \bar{y} - \hat{\beta_1}\bar{x}
$$
$$
\hat{\beta_1} = \frac{Cov(Y,X)}{Var(X)}
$$

Los cuales, por supuestos Gauss-Markov (ver en la siguiente sección) ambos estimadores son insesgados.

## Supuestos Gauss-Markov

Para que los estimadores de nuestro modelo obtenidos a través de Mínimos Cuadrados Ordinarios (MCO) sean el \textbf{Mejor Estimador Lineal Insesgado} (MELI) o en inglés \textbf{Best Linear Unbiased Estimator} (BLUE), realizaremos una serie de supuestos detallados a continuación:

1) **Linealidad en los parámetros:**  El modelo es $y = \beta_0 + \beta_1 x_1 + \dots + u$, donde todos los parámetros de la recta no tienen transformaciones no-lineales.
2) **Media Condicional Cero (Exogeneidad):** $E(u | x_1, \dots, x_k) = 0$. Este es el supuesto más crítico para la insesgadez.
3) **Homocedasticidad:** La varianza del error es constante para cualquier valor de $X$: $Var(u | X) = \sigma^2$.
4) **Mínima Varianza:** Un estimador MELI si o si debe cumplir con tener la mínima varianza, pues, es más fácil concluir que tiene significancia en el modelo.
5) **No Autocorrelación:** La autocorrelación de los residuos es 0 ($Cov(\varepsilon_1, \varepsilon_2) = 0$). \textbf{Nota: Este supuesto es más fuerte en Series de Tiempo.}
6) **No Multicolinealidad Perfecta:** No debe existir una relación lineal perfecta entre las variables independientes, ni se puede escribir alguna variable como combinación lineal de otra. En el caso de la regresión simple, este supuesto se cumple automáticamente.

En un capítulo más adelante veremos que ocurre si se viola el supuesto de **Heterocedasticidad** y de **Exogeniedad**.

## Especificaciones

No solamente podemos escribir un modelo tal como lo definimos en la primera sección (el cual se conoce como Nivel-Nivel), si no, podemos aplicar transformaciones lineales (la más típica es la transformación logarítmica), que podría quedar de la siguiente manera:

1) **Modelo Nivel-Nivel:** $Y = \beta_0 + \beta_1X + \varepsilon$  Se interpreta como: "Un cambio de 1 unidad en $x$ se asocia con un cambio de $\beta_1$ unidades en $y$".
2) **Modelo Log-Nivel:** $Y = \beta_0 + \beta_1\ln(X) + \varepsilon$  Se interpreta como: "Un cambio de 1% en $x$ se asocia con un cambio de $\frac{\beta_1}{100}$ unidades en $y$".
3) **Modelo Nivel-Log:** $Y = \beta_0 + \beta_1X + \varepsilon$  Se interpreta como: "Un cambio de 1 unidad en $x$ se asocia con un cambio de $\beta_1*100$% en $y$".
4) **Modelo Log-Log:** $Y = \beta_0 + \beta_1\ln(X) + \varepsilon$  Se interpreta como: "Un cambio de 1% en $x$ se asocia con un cambio de $\beta_1$% en $y$".

## Inferencia Estadística

Ya sabemos cómo crear un modelo, cómo especificarlo y qué cambios hacerle en base a la pregunta de investigación que queremos responder, pero: ¿son nuestros parámetros estimados significativos a nivel individual? Esta pregunta se puede resolver realizando **Pruebas de Hipótesis**.

Una prueba de hipótesis busca concluir si una suposición sobre la población es cierta utilizando datos muestrales. En este caso nos interesa saber si tanto $\hat{\beta}_0$ como $\hat{\beta}_1$ son relevantes o, en términos sencillos, distintos de cero. La notación para una prueba de hipótesis de significancia individual (bilateral) es la siguiente:

$$H_0: \beta_i = 0$$
$$H_A: \beta_i \neq 0$$

Para realizar una prueba de hipótesis mediante el método del valor crítico, calculamos el estadístico de prueba $t$. Bajo los supuestos del modelo clásico de regresión lineal (o por el **Teorema del Límite Central** en muestras grandes), este estadístico se construye de la siguiente manera:

$$t_c = \frac{\hat{\beta}_i - \beta_{H_0}}{se(\hat{\beta}_i)}$$

Donde $\beta_{H_0} = 0$ bajo la hipótesis nula, y $se(\hat{\beta}_i)$ es el error estándar del estimador.

Luego, se compara el valor absoluto del estadístico $|t_c|$ con el valor crítico $t_{critico}$ obtenido de la distribución correspondiente ($t$-Student con $n-k-1$ grados de libertad o Normal Estándar en muestras grandes cuando $n\rightarrow \infty$) a un nivel de significancia $\alpha$ (niveles habituales de $10\%$, $5\%$ y $1\%$).

Para la distribución Normal Estándar, los valores críticos bilaterales más comunes son:

| Nivel de Significancia | Valor Crítico |
|------------------------|----------------|
| 10%                    | 1.645          |
| 5%                     | 1.960          |
| 1%                     | 2.576          | 

El criterio de rechazo es: Si $|t_c| > t_{critico}$, existe evidencia estadística suficiente para rechazar la hipótesis nula ($H_0$), lo que significa que el parámetro estimado es \textbf{estadísticamente significativo} a un nivel de confianza del $(1-\alpha)\%$.

De manera equivalente, podemos construir un intervalo de confianza para llegar a la misma conclusión. Si realiza ambos métodos para la misma prueba pero obtiene conclusiones distintas, revise sus cálculos, pues existe un error. La fórmula para construir un intervalo de confianza \textbf{bilateral} al $(1-\alpha)\%$ es:

$$IC = \hat{\beta}_i \pm t_{\alpha/2, n-k-1} \cdot se(\hat{\beta}_i)$$

Si el valor hipotético ($\beta_i = 0$) **no pertenece** al intervalo de confianza, se rechaza la hipótesis nula.

<!--chapter:end:01-regresion-simple.rmd-->

# Modelo de Regresión Lineal Múltiple

## Definición

A diferencia de un modelo de Regresión Lineal Simple, el modelo de Regresión Lineal Múltiple permite estudiar el impacto de $k$ variables regresoras $X$ en una variable regresada $Y$. Inicialmente tenemos que:

\[
\begin{bmatrix}
    Y_1 \\
    Y_2 \\
    \vdots \\
    Y_n
\end{bmatrix}
=
\begin{bmatrix}
    1 & x_{11} & x_{12} \\
    1 & x_{21} & x_{22} \\
    \vdots & \vdots & \vdots \\
    1 & x_{n1} & x_{n2}
\end{bmatrix}
\begin{bmatrix}
    \beta_0 \\
    \beta_1 \\
    \vdots \\
    \beta_{k-1}
\end{bmatrix}
+
\begin{bmatrix}
    \varepsilon_1 \\
    \varepsilon_2 \\
    \vdots \\
    \varepsilon_n
\end{bmatrix}
\]

Donde la matriz de $Y's$ es de orden $\mathbb{M}_{n\times 1}$, la matriz de $\varepsilon's$ es de orden $\mathbb{M}_{n\times 1}$, la matriz de $\beta's$ es de orden $\mathbb{M}_{k\times 1}$ y la matriz de covariadas es de orden $\mathbb{M}_{n\times k}$. Finalmente, de manera formal definimos el modelo de regresión múltiple tal que:

$$
Y = X\beta + \xi
$$

Donde tenemos que el estimador para la matriz de parámetros es la siguiente:

$$\hat{\beta} = (X^TX)^{-1}X^TY$$

Y la varianza del estimador es:

$$Var(\beta|X) = \sigma^2(X^TX)^{-1}$$

Donde la varianza del vector de estimaciones se construye en base al supuesto de Homocedasticidad. (Véase la demostración de ambas en el Anexo)

## Bondad de Ajuste

### $R^2$

La bondad de ajuste mide simplemente que porcentaje de la variabilidad de la variable regresada es explicada por la o las variables regresoras. Esto se mide a través del $R^2$. Como nota, no hay que obsesionarse con esto ya que, solamente representa lo mencionado en la definición y no así la robustez del modelo (un $R^2$ alto da una falsa sensación de robustez). El $R^2$ se obtiene de la siguiente manera:

$$
R^2 = \frac{SCE}{SCT} = 1- \frac{SCR}{SCT}
$$

Donde $R^2 \in \{0,1\}$. Usando la siguiente relación: $SCT = SCE + SCR$, si el modelo se ajusta perfectamente, es decir, $SCR = 0$, entonces el $R^2 = 1$. De lo contrario, si el modelo no se ajusta de ninguna manera $SCE = 0$, entonces el $R^2 = 0$. 

El $R^2$ se interpreta como: El modelo logra capturar un $R^2\%$ de la variabilidad de $Y$.

### Overfitting

También, otra de las razones por las cuales no obsesionarse con el $R^2$ es por el **overfitting**. El overfitting es simplemente el acto de incluir variables inexplicativas a un modelo, generando relaciones espurias. Esto podría ''inflar'' el $R^2$, concluyendo un ajuste que sobredimensiona el ajuste real. Suponga que que tenemos el siguiente modelo poblacional (que claro, no conocemos):

$$
Y = \gamma_0 + \gamma_1X_1 + \gamma_2X_2 + u
$$

Donde este modelo tiene un $R^2 = 0.7$. En teoría, intentando estimar este mismo modelo, el máximo $R^2$ que podemos ostentar sería uno igual a $0.8$. Ahora, imaginemos que este fue el modelo que estimamos:

$$
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \beta_3X_3 + \varepsilon
$$

Con un ''impresionante'' $R^2 = 0.8$. En este caso estamos sobreajustando el modelo, incluyendo una variable que genera una relación espuria con la variable regresada.

## Inferencia Estadística

Para esta sección, utilizaremos la misma manera de realizar pruebas de significancia individual que en el capítulo de \textit{Regresión Lineal Simple}. Ahora, añadiremos 3 pruebas de hipótesis importantes para analizar un modelo.

### Prueba de Significancia Global

La prueba de hipótesis global tiene por premisa ver si todos los parámetros son significativos en conjunto a nivel poblacional. Por ende, la notación en este caso es la siguiente:

$$H_0: \beta_1 = \beta_2 = ... = \beta_k = 0$$
$$H_A: \text{Al menos uno de los $\beta$ es distinto de 0.}$$

En este caso utilizaremos nuevamente el método del valor crítico, pero, en este caso nuestro estadístico de prueba distribuye en una distribución F de Snedecor. Nuestro estadístico de prueba es el siguiente:

$$
F_c = \frac{R^2/k}{(1-R^2)/(n-k-1)}
$$

Donde compararemos este estadístico con un valor crítico $F$, que depende de los grados de libertad del numerador y grados de libertad del denominador, y, la manera de comparar es la misma: Si $F_c > F_{df1,df2}$ (donde $df1 = k$ y $df2 = n-k-1$) entonces existe suficiente evidencia estadística para rechazar la hipótesis nula, es decir, los parámetros son significativos en conjunto.

## Prueba de Significancia de Combinaciones de Parámetros

Inicialmente hemos hecho pruebas de hipótesis para significancia individual de un solo parámetro. Pero, también nos interesaría estudiar por ejemplo si los efectos de dos variables son iguales, es decir $\beta_1 = \beta_2$. En este caso la idea cambia un poco, pues, tenemos que realizar ciertas transformaciones para hacer el proceso más sencillo. La notación para este ejemplo sería:

\begin{center}
    $H_0: \beta_1 - \beta_2 = 0$\\
    $H_A = \beta_1 - \beta_2 \ne 0$
\end{center}

Y así, tenemos que obtener un estadístico $t_c$ el cual obtenemos derivando de la mísma fórmula de la prueba de hipótesis individual pero cambiando ciertas cosas:

$$
t_c = \frac{(\widehat{\beta_1} - \widehat{\beta_2}) - \beta_{H_0}}{\sqrt{Var(\widehat{\beta_1} - \widehat{\beta_2})}}
$$

Donde luego, haremos la misma comparación, con los mismos valores de la distribución $t$ o de una distribución normal estándar mediante TLC.

## Múltiples Restricciones Lineales

Ya hemos realizado distintos tipos de prueba de hipótesis, pero, de todas maneras también querríamos estudiar si es que varias restricciones se cumplen a la vez, es decir algo de este estilo:

$$H_0:\beta_1 + \beta_3 = 3$$
$$\frac{1}{3}\beta_1 + \beta_2 = 4$$
$$H_1 = \text{Al menos una de las restricciones no se cumple}$$

Entonces no podemos hacer una prueba de hipótesis con un estadístico t normal, si no más bien, vamos a estimar un modelo (a través de MCO) en donde SI SE CUMPLAN estas restricciones. Entonces sea el modelo acorde al ejemplo definido como $Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \beta_3X_3 + \varepsilon$ Vamos a armar una matriz $R\beta = q$ donde R son los coeficientes de los betas bajo la hipótesis nula, $\beta$ nuestro vector de betas y $q$ el lado derecho del igual de nuestras hipótesis nulas. Entonces definimos:

$$
R = \begin{pmatrix}
    0 & 1 & 0 & 1 \\
    0 & \frac{1}{3} & 1 & 0
\end{pmatrix}
$$

$$
q = \begin{pmatrix}
    3 \\
    4
\end{pmatrix}
$$

y planteamos el problema que deseamos resolver:

 $$\text{min}: U^TU$$
 $$\text{s.a}: R\beta = q$$

Y sabemos que $U^TU = [Y - X\beta]^T[Y - X\beta]$.

Por lo tanto resolveremos el problema de minimización a través de multiplicadores de Lagrange, entonces el Lagrangeano nos queda:

$$
\mathcal{L} = [Y - X\beta]^T[Y - X\beta] + 2\lambda[R\beta-q]
$$

Y por tanto, para resolver se debe cumplir que:

 $$\frac{\partial\mathcal{L}}{\partial\lambda} = 0 \land \frac{\partial\mathcal{L}}{\partial\beta} = 0$$

La primera ecuación corresponde a la restricción, y la segunda ecuación correspondería a:


$$2(X^TX)\beta - 2X^TY + 2R^T\lambda = 0$$

Finalmente, desarrollando esto (véase en el Anexo) nuestro estimador de este modelo con las restricciones impuestas, al cual llamaremos \textbf{Mínimos Cuadrados Restringidos} es el siguiente:

$$
\widetilde{\beta} = (X^TX)^{-1}X^TY - (X^TX)^{-1}R^T\lambda
$$

Si nosotros deseamos calcular la varianza del estimador, tenemos lo siguiente:

$$
V(\widetilde{\beta}) = V(\widehat{\beta}) - \textbf{terminos positivos}
$$

Podemos ver entonces que, la varianza del estimador de MCR es menor a la de MCO \textbf{siempre y cuando las restricciones NO SE CUMPLAN}, en el caso contrario, la varianza de MCR y la varianza de MCO son iguales.

Luego de esto, derivando obtenemos que:

$$
\widetilde{\xi}^T\widetilde{\xi} = \widehat{\xi}^T\widehat{\xi} + (\widetilde{\beta} - \widehat{\beta})^TX^TX- 2(\widetilde{\beta} - \widehat{\beta})^TX^T\widehat{\xi}
$$

Concluyendo entonces que:

$$
\widetilde{\xi}^T\widetilde{\xi} \ge \widehat{\xi}^T\widehat{\xi}
$$

Por lo tanto, así $F_c = \frac{(\widetilde{\xi}^T\widetilde{\xi} - \widehat{\xi}^T\widehat{\xi})/q}{\widehat{\xi}^T\widehat{\xi}/(n-k)}$. Y amplificando por $\frac{1}{SCT}$ tenemos que:

$$
F_c = \frac{(R^2 - R^2_{r})/q}{(1-R^2)/(n-k-1)}
$$

Donde $q$ es el número de restricciones.

La conclusión es que, si $F_c > F_{df1,df2}$ (donde $df1 = q$ y $df2 = n-k-1$) entonces existe suficiente evidencia estadística para rechazar la hipótesis nula, es decir, las restricciones no se cumplen.

<!--chapter:end:02-regresion-multiple.rmd-->

---
output:
  html_document: default
  pdf_document: default
---
# Multicolinealidad

## Multicolinealidad Perfecta

La multicolinealidad perfecta es cuando tenemos dentro de un modelo, una variable regresora que se puede escribir como combinación lineal de otra. Sea el siguiente modelo:

$$Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \varepsilon$$

Donde $X_2 = 2X_1$, por ejemplo. Si reemplazamos esa especificación para \$X_24 tendríamos que:

$$Y = \beta_0 + \beta_1X_1 + \beta_2 \cdot 2X_1 + \varepsilon$$

Y luego:

$$Y = \beta_0 + [\beta_1 + 2\beta_2]X_1 + \varepsilon$$

Y a esta combinación lineal de betas que está multiplicando a $X_1$ le llamaremos $\beta^*$, tal que:

$$Y = \beta_0 + \beta^*X_1 + \varepsilon$$

Matemáticamente lo que esta ocurriendo es que, al ser $X_2$ combinación lineal de $X_1$ (devolviéndonos al estimador del vector de parámetros) incurriríamos en el siguiente problema:

$$\hat{\beta} = (X^TX)^{-1}X^TY$$

Como tenemos dos columnas que son combinaciones lineales, el determinante de la matriz $(X^TX) = 0$, por lo tanto la inversa de dicha matriz **no está definida.** De otra manera, cuando hay multicolinealidad perfecta, la correlación entre una y otra o varias variables es 1.

## Multicolinealidad No Perfecta

En este caso cuando existe multicolinealidad no perfecta, a diferencia del caso anterior, observamos que existe una fuerte correlación entre ciertas variables, pero no perfecta.

Esto genera distintas cosas, tales como:

1.  **Varianza Alta:** Los coeficientes cambian sustancialmente ante mínimos cambios en los datos.
2.  **Errores Estándar Altos:** Los intervalos de confianza se hacen más amplios, lo cual dificulta rechazar la hipótesis nula, es decir, pierde significancia el coeficiente.
3.  **Dificultad para interpretar:** Resulta complejo aislar el efecto individual de cada coeficiente.

## Factor Inflacionario de la Varianza

Una de las formas de detectar multicolinealidad entre variables se puede realizar a través del **Factor Inflacionario de la Varianza (VIF).** Por definición, el factor inflacionario de la varianza mide cuanto aumenta la varianza de un coeficiente debido a la correlación entre las variables regresoras. Por fórmula cuando hay únicamente dos regresores:

$$VIF = \frac{1}{Corr^2(X_1,X_2)}$$
Por el contrario, si tuviésemos más regresoras la fórmula corresponde a:

$$VIF = \frac{1}{1-R^2_j}$$
Donde $R^2_j$ corresponde al R-cuadrado de una regresión auxiliar que resulta de regresionar la variable $X_j$ con los demás regresores tal que:

$$X_j = \gamma_0 + \gamma_1X_1 + \gamma_2X_2 + ... + \gamma_nX_n + u$$
Si analizamos esto, podemos ver que si los demás regresores explican completamente la variable, es decir $R^2_j = 1$, entonces $VIF \rightarrow \infty$, y por otra parte si los demás regresores no explican nada de la variable, es decir, $R^2_j = 0$, entonces $VIF = 0$, por lo tanto no existe multicolinealidad. Como el $R^2 \in \{0,1\}$ entonces el dominio del $VIF$ es $Dom: \{0,1\}$ y el $VIF$ puede tomar valores en el intervalo $[0,\infty[$.

Gráficamente el $VIF$ se ve de la siguiente manera:


\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-2-1} \end{center}

Una ''solución'' a la multicolinealidad es eliminar la variable que genera multicolinealidad, con el riesgo de tener sesgo por variable omitida. En teoría con esto tenemos un trade-off entre multicolinealidad y sesgo, el cual depende necesariamente de la pregunta de investigación o propósito de realizar el modelo.

<!--chapter:end:03-multicolinealidad.rmd-->

# Variables Dummy

Una variable Dummy (o típicamente variable indicadora) es una variable que toma el valor de 1 o 0 dependiendo de si se cumple o no una condición. Por ejemplo, si queremos estudiar el efecto de ser hombre o mujer en los ingresos, podemos crear una variable Dummy que tome el valor de 1 si la persona es hombre y 0 si es mujer.

## Modelo de Regresión Simple con Variables Dummy
 
En términos univariados el modelo queda escrito de la siguiente manera:

$$
Y = \beta_0 + \beta_1D + \varepsilon
$$

Donde el valor esperado para una persona hombre es:

$$
E(Y | D=1) = \beta_0 + \beta_1
$$

Así, el valor esperado para una persona mujer es:

$$
E(Y | D=0) = \beta_0
$$

La interpretación de $\beta_1$ es el cambio en los ingresos esperado al cambiar de mujer a hombre. Gráficamente, el modelo se ve de la siguiente manera:



\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-3-1} \end{center}

## Modelo de Regresión Múltiple con Variables Dummy

En contextos multivariados, podemos incluir variables Dummy junto con otras variables continuas. Por ejemplo, si queremos estudiar el efecto de la educación y el género en los ingresos, podemos tener un modelo como:

$$
Y = \beta_0 + \beta_1D + \beta_2X + \varepsilon
$$

Donde la interpretación cambiará dependiendo de la variable Dummy y la variable continua. En este caso, $\beta_1$ representará el efecto del género en los ingresos, mientras que $\beta_2$ representará el efecto de la educación en los ingresos. Por lo tanto, el valor esperado de los ingresos para una persona hombre con un nivel de educación $X$ será:

$$
E(Y | D=1, X) = \beta_0 + \beta_1 + \beta_2X
$$

Así, el valor esperado para una persona mujer con el mismo nivel de educación $X$ será:

$$
E(Y | D=0, X) = \beta_0 + \beta_2X
$$

La interpretación de $\beta_1$ es el cambio en los ingresos esperado al cambiar de mujer a hombre, manteniendo constante el nivel de educación.

Gráficamente, el modelo se ve de la siguiente manera:


```
## `geom_smooth()` using formula = 'y ~ x'
```



\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-4-1} \end{center}

## Interacciones

En nuestro modelo, también podemos incluir interacciones entre variables Dummy y continuas. Por ejemplo, si queremos ver si el efecto de la educación en los ingresos difiere entre hombres y mujeres, podemos incluir un término de interacción:

$$
Y = \beta_0 + \beta_1D + \beta_2X + \beta_3(D \times X) + \varepsilon
$$

En este caso, $\beta_3$ nos dirá si el efecto de la educación en los ingresos es diferente para hombres y mujeres. Si $\beta_3$ es positivo, significa que el retorno a la educación es mayor para los hombres que para las mujeres, y viceversa.

Entonces, el valor esperado de los ingresos para una persona hombre con un nivel de educación $X$ será:

$$
E(Y | D=1, X) = \beta_0 + \beta_1
    + \beta_2X + \beta_3X
$$

$$
E(Y | D=1, X) = (\beta_0 + \beta_1) + (\beta_2 + \beta_3)X
$$

Así mismo, el efecto de los ingresos de una persona mujer con el mismo nivel de educación $X$ será:

$$
E(Y | D=0, X) = \beta_0 + \beta_2X
$$

Gráficamente, el modelo con interacción se ve de la siguiente manera:


```
## `geom_smooth()` using formula = 'y ~ x'
```



\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-5-1} \end{center}

<!--chapter:end:04-variables-dummy.rmd-->

# Heterocedasticidad

## Definición

Anteriormente, por supuestos Gauss-Markov habíamos asumido que estábamos en presencia de homocedasticidad, es decir, la varianza de los residuos es constante. Pero, lamentablemente en la realidad esto es casi imposible que ocurra. Definimos anteriormente, la varianza del parámetro como:

$$V(\widehat{\beta}) = (X^TX)^{-1}X^TE[UU^T]X(X^TX)^{-1}$$

Donde asumíamos que $E[UU^T] = \sigma^2I$ obviamente por el supuesto de Homocedasticidad. En presencia de heterocedasticidad esto ya no ocurre, por lo que a esta expresión la denotaremos por $\Omega$. Por tanto la varianza del parámetro queda como:

$$V(\widehat{\beta}) =  (X^TX)^{-1}X^T\Omega X(X^TX)^{-1}$$

Donde $\Omega$ es una matriz diagonal con elementos $\sigma_i^2$ en la diagonal, es decir, la varianza de los residuos no es constante. Por lo tanto, el estimador de MCO sigue siendo insesgado, pero ya no es eficiente. Por lo que necesitamos un estimador robusto a heterocedasticidad.

Gráficamente, la heterocedasticidad se puede presentar de la siguiente forma:


\begin{center}\includegraphics[width=1\linewidth]{manual_files/figure-latex/unnamed-chunk-6-1} \end{center}

Si observan, a medida que aumenta el valor de $X$, en el caso heterocedástico vemos que cada vez más aumenta el error. Esto podría suceder de forma de abanico creciente, decreciente o en forma de U, cualquiera de las tres mencionadas son casos de heterocedasticidad. Lo que a nosotros nos gustaría ver es que se forme una nube sin forma, que en promedio oscile en un valor constante para cada valor de $X$.

## Consecuencias para MCO

Las consecuencias que sufrirían nuestros parámetros estimados por MCO son que dejan de ser eficientes (ya no son BLUE) y la inferencia es inválida, pues, los estadísticos de prueba y los intervalos de confianza están ''manchados'' por este problema de heterocedasticidad.

Entonces, en teoría los argumentos Gauss-Markov ya no se cumplen, por lo que necesitamos solucionar este problema, y para ello existen diversas soluciones, dentro de las cuales están:

1) **Trasnformaciones de Variables:** Por ejemplo, si tenemos un modelo de Nivel-Nivel, podríamos transformarlo a Log-Log, lo cual podría ayudar a estabilizar la varianza de los residuos.
2) **Mínimos Cuadrados Generalizados (MCG):** Este método es una extensión de MCO, que permite corregir la heterocedasticidad, pero requiere conocer la forma funcional de la heterocedasticidad.
3) **Mínimos Cuadrados Ponderados (MCP):** Este método es una variante de MCG, que permite corregir la heterocedasticidad, pero requiere conocer la forma funcional de la heterocedasticidad.
4) **Estimadores Robustos a Heterocedasticidad:** Este método es una variante de MCO, que permite corregir la heterocedasticidad, pero no requiere conocer la forma funcional de la heterocedasticidad. En R, se puede implementar con el paquete `sandwich`.

## Detección de Heterocedasticidad

Para detectar heterocedasticidad, existen dos maneras principales para detectarlo, las cuales son:

1) **Test de Breusch-Pagan:** Este test es un test de hipótesis que busca determinar si la varianza de los residuos es constante o no. La hipótesis nula es que la varianza es constante (homocedasticidad) y la alternativa es que la varianza no es constante (heterocedasticidad). El estadístico de prueba sigue una distribución Chi-cuadrado con grados de libertad igual al número de variables independientes en el modelo.
Matemáticamente, el test de Breusch-Pagan se puede expresar como:

$$
BP = n \cdot R^2_{\text{aux}}
$$

Donde el $R^2_{\text{aux}}$ es el $R^2$ de la regresión auxiliar, que se obtiene al regredir los residuos al cuadrado del modelo original sobre las variables independientes del modelo original, tal que:

$$
e_i^2 = \alpha + \beta_1 X_1 + \beta_2 X_2 + \epsilon_i
$$

La conclusión se obtiene a través de comparar el estadístico de prueba con el valor crítico de la distribución Chi-cuadrado con grados de libertad igual al número de variables independientes en el modelo. Si el estadístico de prueba es mayor que el valor crítico, se rechaza la hipótesis nula y se concluye que hay evidencia de heterocedasticidad.

2) Test de White: Este test es un test de hipótesis que busca determinar si la varianza de los residuos es constante o no. La hipótesis nula es que la varianza es constante (homocedasticidad) y la alternativa es que la varianza no es constante (heterocedasticidad). El estadístico de prueba sigue una distribución Chi-cuadrado con grados de libertad igual al número de variables independientes en el modelo más el número de variables independientes al cuadrado.
Matemáticamente el test de White es exactamente igual que el test de Breusch-Pagan, pero la diferencia es que en la regresión auxiliar se incluyen los términos al cuadrado y los términos de interacción de las variables independientes del modelo original, tal que:

$$
e_i^2 = \alpha + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_1^2 + \beta_4 X_2^2 + \beta_5 (X_1 \times X_2) + \epsilon_i
$$

Y la conclusión es exactamente la misma que en el test de Breusch-Pagan, se compara el estadístico de prueba con el valor crítico de la distribución Chi-cuadrado con grados de libertad igual al número de variables independientes en el modelo más el número de variables independientes al cuadrado. Si el estadístico de prueba es mayor que el valor crítico, se rechaza la hipótesis nula y se concluye que hay evidencia de heterocedasticidad.

<!--chapter:end:05-heterocedasticidad.rmd-->

# Endogeneidad: Variables Instrumentales

## Definición

Ahora hablaremos de un problema que ocurre cuando no se cumple el supuesto de exogeneidad, es decir, cuando $E(u | X) \neq 0$. En este caso, los estimadores obtenidos a través de Mínimos Cuadrados Ordinarios (MCO) serán sesgados e inconsistentes.

La endogeneidad por definición es un problema que ocurre cuando una o más variables explicativas están correlacionadas con el término de error. Esto puede suceder por varios tipos de sesgo, los cuales son:

1. **Sesgo por variable omitida:** Ocurre cuando se omite una variable que afecta tanto a la variable dependiente como a una o más variables independientes, lo que genera una correlación entre las variables explicativas y el término de error.
2. **Sesgo por simultaneidad:** Ocurre cuando la variable dependiente y una o más variables independientes se determinan de manera simultánea, lo que genera una correlación entre las variables explicativas y el término de error.
3. **Sesgo por error de medición:** Ocurre cuando una o más variables independientes se miden con error, lo que genera una correlación entre las variables explicativas y el término de error.

## Solución: Variables Instrumentales

Para solucionar este problema de endogeneidad utilizaremos Variables Instrumentales (VI). Una variable instrumental es una variable que está correlacionada con la variable endógena, pero no está correlacionada con el término de error. Esto nos permite aislar la variación exógena de la variable endógena y obtener estimadores consistentes.

Entonces, para que una variable sea un buen instrumento debe cumplir con dos condiciones:

1. **Relevancia:** La variable instrumental debe estar correlacionada con la variable endógena ($Cov(Z, X) \neq 0$). Esto se puede verificar mediante un test de relevancia, como el test de F de la primera etapa (ya se mencionará esto más adelante).
2. **Exogeneidad:** La variable instrumental no debe estar correlacionada con el término de error ($Cov(Z, u) = 0$). Esto no es posible determinarlo mediante test, si no, a través de argumentos teóricos o evidencia empírica.

## Mínimo Cuadrados en Dos Etapas (MC2E)

Para estimar un modelo con variables instrumentales utilizaremos el método de Mínimos Cuadrados en Dos Etapas (MC2E). Este método consiste en dos etapas:

1. La primera etapa corresponde a regresionar la variable endógena sobre las variables instrumentales y las variables exógenas del modelo. Esto nos permitirá obtener los valores ajustados de la variable endógena, que son puramente exógenos. Luego, antes de seguir se realiza el test de relevancia para verificar que los instrumentos son relevantes. Se debe cumplir que el estadístico F de la primera etapa sea mayor a 10, de lo contrario, los instrumentos son débiles y no se puede confiar en los resultados.
2. Recuperamos la variable endógena ajustada de la primera etapa y la utilizamos en la segunda etapa para estimar el modelo original mediante MCO. Esto nos permitirá obtener estimadores consistentes de los parámetros del modelo.

## Implicancias de Mínimos Cuadrados en Dos Etapas

De por si, la solución al problema de endogeneidad es un gran avance, pero debemos tener en cuenta que el método de Mínimos Cuadrados en Dos Etapas tiene algunas implicancias:

1. Los errores estándar obtenidos a través de la segunda etapa de MC2E son más altos que en MCO, lo que significa que los intervalos de confianza serán más amplios y las pruebas de hipótesis serán menos poderosas. Esto ocurre porque al estimar la variable endógena en la primera etapa, se introduce un error adicional en la estimación de los parámetros del modelo.
2. La interpretación de los coeficientes estimados a través de MC2E es diferente. En el caso de MC2E, la interpretación de los coeficientes ahora es el efecto causal de la variable endógena sobre la variable dependiente, mientras que en MCO, la interpretación es el efecto total de la variable endógena sobre la variable dependiente, incluyendo tanto el efecto directo como el efecto indirecto a través de otras variables.

## Test de Hausman

El test de Hausman es una prueba estadística que nos permite determinar si un modelo es consistente o no. En el contexto de variables instrumentales, el test de Hausman nos permite comparar los estimadores obtenidos a través de MCO y MC2E para determinar si la variable endógena es realmente endógena o no. 
Para realizar este test se debe cumplir con las siguientes hipótesis:  

$$
H_0: \text{La variable endógena es exógena, por lo tanto, MCO es consistente.}
$$
$$
H_A: \text{La variable endógena es endógena, por lo tanto, MCO es inconsistente y MC2E es consistente.}
$$

Primero, para realizar este test se especifica el modelo. Por ejemplo:

$$
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + u
$$

Luego, se estima la primera etapa del modelo de la variable endógena $X_1$ sobre las variables instrumentales $Z$ y las variables exógenas $X_2$:

$$
X_1 = \pi_0 + \pi_1Z + \pi_2X_2 + v
$$

De esta regresión se obtiene el residuo $\hat{v}$, que representa la parte de $X_1$ que no está explicada por las variables instrumentales y las variables exógenas. Luego, se estima el modelo original incluyendo el residuo $\hat{v}$ como una variable adicional:

$$
Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \gamma\hat{v} + u
$$

Ahora se realiza un test de hipótesis sobre el coeficiente $\gamma$:

$$
H_0: \gamma = 0 \quad \text{(La variable endógena es exógena, MCO es consistente)}
$$

$$
H_A: \gamma \neq 0 \quad \text{(La variable endógena es endógena, MCO es inconsistente y MC2E es consistente)}
$$

Se realiza un estadístico de prueba $t$ para el coeficiente $\gamma$ y se compara con el valor crítico correspondiente al nivel de significancia deseado. Si se rechaza la hipótesis nula, se concluye que la variable endógena es endógena y que los estimadores obtenidos a través de MCO son inconsistentes, por lo tanto, se debe utilizar MC2E para obtener estimadores consistentes.

<!--chapter:end:06-endogeneidad.rmd-->

# Anexo

## Regresión Lineal Simple

### Demostración del estimador de $\hat{\beta}_0$ y $\hat{\beta}_1$ mediante MCO

$$
\text{Problema:} \quad \min_{\beta_0, \beta_1} \sum_{i=1}^{n}\varepsilon_i^2 = \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i)^2
$$

**Para $\hat{\beta}_0$:**

$$
\frac{\partial \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i)^2}{\partial \beta_0} = 0
$$

$$
-2\sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i) = 0
$$

$$
\sum_{i=1}^{n} y_i - n\beta_0 - \beta_1 \sum_{i=1}^{n} x_i = 0
$$

$$
n\beta_0 = \sum_{i=1}^{n} y_i - \beta_1 \sum_{i=1}^{n} x_i
$$

$$
\widehat{\beta}_0 = \frac{1}{n} \sum_{i=1}^{n} y_i - \hat{\beta}_1 \frac{1}{n} \sum_{i=1}^{n} x_i
$$

$$
\widehat{\beta}_0 = \bar{y} - \widehat{\beta}_1\bar{x}
$$

**Luego, para $\hat{\beta}_1$:**

$$
\frac{\partial \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i)^2}{\partial \beta_1} = 0
$$

$$
-2\sum_{i=1}^{n} x_i (y_i - \beta_0 - \beta_1 x_i) = 0
$$

$$
\sum_{i=1}^{n} x_i y_i - \beta_0 \sum_{i=1}^{n} x_i - \beta_1 \sum_{i=1}^{n} x_i^2 = 0
$$

Sabiendo que $\hat{\beta}_0 = \bar{y} - \hat{\beta}_1\bar{x}$, podemos sustituirlo en la ecuación anterior:

$$
\sum_{i=1}^{n} x_i y_i - (\bar{y} - \hat{\beta}_1\bar{x}) \sum_{i=1}^{n} x_i - \hat{\beta}_1 \sum_{i=1}^{n} x_i^2 = 0
$$

$$
\sum_{i=1}^{n} x_i y_i - \bar{y} \sum_{i=1}^{n} x_i + \hat{\beta}_1\bar{x} \sum_{i=1}^{n} x_i - \hat{\beta}_1 \sum_{i=1}^{n} x_i^2 = 0
$$

Reordenando los términos con $\hat{\beta}_1$:

$$
\sum_{i=1}^{n} x_i y_i - \bar{y} \sum_{i=1}^{n} x_i = \hat{\beta}_1 \left( \sum_{i=1}^{n} x_i^2 - \bar{x} \sum_{i=1}^{n} x_i \right)
$$

Despejando $\hat{\beta}_1$:

$$
\hat{\beta}_1 = \frac{\sum_{i=1}^{n} x_i y_i - \bar{y} \sum_{i=1}^{n} x_i}{\sum_{i=1}^{n} x_i^2 - \bar{x} \sum_{i=1}^{n} x_i}
$$

Dividiendo numerador y denominador por $n$ y asumiendo datos i.i.d.:

$$
\hat{\beta}_1 = \frac{Cov(Y,X)}{Var(X)}
$$

---

### Demostración de Insesgadez para $\hat{\beta}_0$ y $\hat{\beta}_1$

**Primero, para $\hat{\beta}_0$:**

$$
E[\hat{\beta}_0] = E[\bar{y} - \hat{\beta}_1\bar{x}]
$$

$$
E[\hat{\beta}_0] = E[\bar{y}] - \bar{x}E[\hat{\beta}_1]
$$

Sabemos que $\bar{y} = \beta_0 + \beta_1\bar{x} + \bar{\varepsilon}$, entonces:

$$
E[\hat{\beta}_0] = E[\beta_0 + \beta_1\bar{x} + \bar{\varepsilon}] - \bar{x}E[\hat{\beta}_1]
$$

Por esperanza condicional cero, $E[\bar{\varepsilon}] = 0$:

$$
E[\hat{\beta}_0] = \beta_0 + \beta_1\bar{x} - \bar{x}E[\hat{\beta}_1]
$$

Dado que $E[\hat{\beta}_1] = \beta_1$:

$$
E[\hat{\beta}_0] = \beta_0 + \beta_1\bar{x} - \beta_1\bar{x} = \beta_0
$$

**Luego, para $\hat{\beta}_1$:**

$$
E[\hat{\beta}_1] = E\left[\frac{Cov(Y,X)}{Var(X)}\right]
$$

Dado que $Y = \beta_0 + \beta_1X + \varepsilon$:

$$
E[\hat{\beta}_1] = E\left[\frac{Cov(\beta_0 + \beta_1X + \varepsilon, X)}{Var(X)}\right]
$$

Por propiedades de la covarianza:

$$
E[\hat{\beta}_1] = E\left[\frac{Cov(\beta_1X, X) + Cov(\varepsilon, X)}{Var(X)}\right]
$$

Por exogeneidad estricta, $Cov(\varepsilon, X) = 0$:

$$
E[\hat{\beta}_1] = E\left[\frac{\beta_1 Cov(X, X)}{Var(X)}\right]
$$

Como $Cov(X, X) = Var(X)$:

$$
E[\hat{\beta}_1] = E\left[\frac{\beta_1 Var(X)}{Var(X)}\right] = E[\beta_1] = \beta_1
$$

---

### Demostración de la varianza de $\hat{\beta}_1$

Escribiendo el estimador en términos de los errores $\varepsilon_i$:

$$
\hat{\beta}_1 = \beta_1 + \frac{\sum_{i=1}^{n}(x_i - \bar{x})\varepsilon_i}{\sum_{i=1}^{n}(x_i - \bar{x})^2}
$$

Aplicando el operador varianza condicional a $X$:

$$
Var(\hat{\beta}_1 | X) = Var\left( \beta_1 + \frac{\sum_{i=1}^{n}(x_i - \bar{x})\varepsilon_i}{\sum_{i=1}^{n}(x_i - \bar{x})^2} \ \Bigg|\  X \right)
$$

Como $\beta_1$ es una constante y asumiendo homocedasticidad ($Var(\varepsilon_i|X) = \sigma^2$) e independencia de los errores:

$$
Var(\hat{\beta}_1 | X) = \frac{\sum_{i=1}^{n}(x_i - \bar{x})^2 Var(\varepsilon_i | X)}{\left(\sum_{i=1}^{n}(x_i - \bar{x})^2\right)^2}
$$

$$
Var(\hat{\beta}_1 | X) = \frac{\sigma^2 \sum_{i=1}^{n}(x_i - \bar{x})^2}{\left(\sum_{i=1}^{n}(x_i - \bar{x})^2\right)^2}
$$ 

Simplificando el término del sumatorio y amplificando todo por $\frac{1}{n}$ tenemos que:

$$
Var(\hat{\beta_1}| X) = \frac{\sigma^2}{nVar(X)}
$$

## Regresión Lineal Múltiple

### Demostración del Estimador del Vector de $\hat{\beta}$ bajo el supuesto de Homocedasticidad

Partimos desde el problema a resolver:

$$
\text{Problema:} \quad \min_{\beta} \xi^T\xi
$$

Sabiendo que $Y = X\beta + \xi$, entonces, $\xi = Y - X\beta$, por tanto el problema se convierte en:

$$
\text{Problema:} \quad \min_{\beta} [Y-X\beta]^T[Y-X\beta]
$$

Por propiedades de matrices, trasponiendo $[Y - X\beta]$ se tiene que:

$$
\text{Problema:} \quad \min_{\beta} [Y^T - \beta^T X^T][Y-X\beta]
$$

Luego, distribuyendo el paréntesis se tiene que:

$$
\text{Problema:} \quad \min_{\beta} Y^TY - Y^TX\beta - \beta^T X^T Y + \beta^T X^T X \beta
$$

Dado que, cada término es igual a un escalar, es decir, una matriz $in \mathbb{M}_1$, entonces un término es igual a su propia transpuesta, por lo que el tercer término queda como:

$$
\text{Problema:} \quad \min_{\beta} Y^TY - Y^TX\beta - Y^TX\beta + \beta^T X^T X \beta
$$

Y por tanto reduciendo queda:

$$
\text{Problema:} \quad \min_{\beta} Y^TY - 2 Y^TX\beta + \beta^T X^T X \beta
$$

Ahora, para minimizar esto, debemos derivar todo con respecto a $\beta$, tal que:

$$
\frac{\partial \xi^T\xi}{\partial \beta} = 0
$$

Donde, derivando obtenemos:

$$
-2X^TY + 2X^TX\hat{\beta} = 0
$$

Factorizando y dividiendo a ambos lados por $2$ tenemos que:

$$
X^TY - X^TX\hat{\beta} = 0
$$
 
Luego, despejamos el término que contiene $\hat{\beta}$:

$$
X^TX\hat{\beta} = X^TY
$$

Utilizando la propiedad $AA^{-1} = I$, entonces multiplicamos a ambos lados **por la izquierda** por $(X^TX)^{-1}$, por lo tanto:

$$
\hat{\beta} = (X^TX)^{-1}X^TY
$$

### Demostración de Insesgadez del Vector de $\hat{\beta}$

Sabemos que el vector de $\hat{\beta}$ está determinado por:

$$
\hat{\beta} = (X^TX)^{-1}X^TY
$$

y sabemos también que $Y = X\beta + \xi$, por lo que al reemplazar:

$$
\hat{\beta} = (X^TX)^{-1}X^T(X\beta + \xi)
$$

aplicando operador de esperanza a ambos lados, condicional a $X$ se tiene que:

$$
E[\hat{\beta}|X] = E[(X^TX)^{-1}X^T(X\beta + \xi)|X]
$$

aplicando propiedad distributiva se tiene que:

$$
E[\hat{\beta}|X] = E[(X^TX)^{-1}X^TX\beta + (X^TX)^{-1}X^T\xi|X]
$$


Ahora, sabiendo dos cosas:

1. $AA^{-1} = I$
2. $E(\xi|X) = 0$

Podemos eliminar el segundo término, pues, es cero y el primer término se reduce a:

$$
E[\hat{\beta}|X] = E[\beta]
$$

Y la esperanza de una constante es simplemente la constante, por lo tanto queda demostrado que el estimador de beta es insesgado:

$$
E[\hat{\beta}|X] = \beta
$$

### Demostración de la Varianza de $\hat{\beta}$ bajo el supuesto de Homocedasticidad

Por definición matricial, la varianza del estimador se puede escribir tal que:

$$
Var(\hat{\beta}|X) = E[\hat{\beta} - \beta][\hat{\beta} - \beta]^T
$$

Si nosotros volvemos hacia atrás sabemos que:

$$
\hat{\beta} = \beta + (X^TX)^{-1}X^T\xi
$$

Por tanto podemos definir que:

$$
\hat{\beta} - \beta = (X^TX)^{-1}X^T\xi
$$

Luego, en la fórmula matricial que definimos para la varianza, tenemos que:

$$
Var(\hat{\beta}|X) = E[(X^TX)^{-1}X^T\xi][(X^TX)^{-1}X^T\xi]^T
$$

Transponiendo el segundo paréntesis se tiene:

$$
Var(\hat{\beta}|X) = E[(X^TX)^{-1}X^T\xi][\xi^TX(X^TX)^{-1}]
$$

Multiplicando:

$$
Var(\hat{\beta}|X) = E[(X^TX)^{-1}X^T\xi\xi^TX(X^TX)^{-1}]
$$

Luego, todo lo que sea $X$ sale del operador de esperanza:

$$
Var(\hat{\beta}|X) = (X^TX)^{-1}X^TE[\xi\xi^T]X(X^TX)^{-1}
$$

Ahora bien, según el supuesto de homocedasticidad de Gauss-Markov $E[\xi\xi^T] = \sigma^2I$, por lo tanto se tiene que:

$$
Var(\hat{\beta}|X) = (X^TX)^{-1}X^T\sigma^2IX(X^TX)^{-1}
$$

Como la multiplicación por la matriz identidad es similar a multiplicar por 1, desaparece. Luego, como $\sigma^2$ es una constante, podemos colocarla hacia el frente, tal que:

$$
Var(\hat{\beta}|X) = \sigma^2(X^TX)^{-1}X^TX(X^TX)^{-1}
$$

Finalmente, usando propiedades de matrices, todo el término se reduce a:

$$
Var(\hat{\beta}|X) = \sigma^2(X^TX)^{-1}
$$

### Demostración de $\tilde{\beta}$

Se formaliza el problema de la siguiente manera:

$$
\text{Problema:} \quad \min_{\beta} \xi^T\xi
$$
$$
\text{s.a} R\beta = q
$$

Donde $R$ es la matriz de coeficientes de las restricciones que queremos estudiar y $q$ es el lado derecho de la restricción.
 Se arma el Lagrangeano de la siguiente manera (Sabiendo que la función objetivo corresponde a algo que hemos visto antes, lo que es $Y^TY - 2 Y^TX\beta + \beta^T X^T X \beta$):

$$
\mathcal{L} =  Y^TY - 2 Y^TX\beta + \beta^T X^T X \beta + 2\lambda^T(R\beta - q)
$$

Luego derivamos con respecto a la variable $\beta$ y a $\lambda$ tal que:

$$
\frac{\partial \mathcal{L}}{\partial \beta} = 0 \land \frac{\partial \mathcal{L}}{\partial \lambda} = 0
$$

Donde la segunda ecuación corresponde a $R\beta = q$, es decir, la restricción. Por otra parte tenemos que:

$$
\frac{\partial \mathcal{L}}{\partial \lambda} = -2X^TY + 2X^TX\beta + 2R^T\lambda = 0
$$

Despejando

$$
-X^TY + X^TX\beta + R^T\lambda = 0
$$

$$
X^TX\beta = X^TY -R^T\lambda
$$

Multiplicando por $(X^TX)^{-1}$ por la izquierda obtenemos:

$$
\widetilde{\beta} = (X^TX)^{-1}X^TY - (X^TX)^{-1}R^T\lambda
$$

$$
\widetilde{\beta} = \hat{\beta} - (X^TX)^{-1}R^T\lambda
$$

Luego, para hallar el valor de $\lambda$, mutliplicamos la ecuación obtenida anteriormente por la matriz de restricciones $R$:

$$
R\widetilde{\beta} = R\hat{\beta} - R(X^TX)^{-1}R^T\lambda
$$

Como sabemos que $R\beta = q$ entonces:

$$
q = R\hat{\beta} - R(X^TX)^{-1}R^T\lambda
$$

Despejando:

$$
R(X^TX)^{-1}R^T\lambda = R\hat{\beta} - q 
$$

Como la matriz $R$ tiene rango completo, entonces existe necesariamente la inversa de dicha matriz, por lo tanto:

$$
\lambda = [R(X^TX)^-1R^T]^{-1}(R\hat{\beta}-q)
$$

Sustituyendo $\lambda$ en la primera ecuación, finalmente obtenemos:

$$
\widetilde{\beta} = \hat{\beta} - (X^TX)^{-1}R^T[R(X^TX)^-1R^T]^{-1}(R\hat{\beta}-q)
$$

Donde, en resumidas cuentas, el estimador de MCR es igual al de MCO pero con una corrección proporcional al tamaño del error de la hipótesis. En el supuesto de que, las restricciones fuesen ciertas, entonces esa corrección sería 0 y por lo tanto el estimador de MCR es igual al estimador de MCO.

<!--chapter:end:07-anexos.Rmd-->

