# Convolución, correlación y transformación
El presente informe explicará el desarrollo del laboratorio dos de Procesamiento Digital de Señales, en el cuál se implementaron las operaciones de convolución, correlación y análisis espectral, se tuvo que hacer cálculos y gráficas a mano, junto con la elaboración de un código en python compilado en Google Colab.
La guía está dividida en tres partes, la primera parte  se tenía que calcular la convolución de dos sistemas, el cual

h1(n)= {5, 6, 0, 0, 7, 1, 3}, 

x1(n)= {1, 0, 5, 3, 4, 4, 2, 3, 9, 9} es el código estudiantil y cédula  de una de las integrantes del grupo respectivamente, al igual para la otra intengrante:

h2(n)={5, 6, 0, 0, 7, 2, 1}, 

x2(n)={1, 0, 0, 0, 2, 4, 1, 8, 2, 2}.

Estos cálculos fueron posible realizarse gracias a la explicación de la docente, a continuación mostraremos los resultados obtenidos junto con las gráficas de cada sistema.
# Integrante 1
![image](https://github.com/user-attachments/assets/cc6dee0f-825c-4bf1-9e52-0e5c532c8243)
![image](https://github.com/user-attachments/assets/bf065dee-ed25-40ed-9935-e1e731be26f5)


# Integrante 2
![image](https://github.com/user-attachments/assets/74e5d430-629c-490d-bfb2-5c095d896caf)
![image](https://github.com/user-attachments/assets/f335a4e5-34ad-4e0d-b391-3446d14ed2a1)

En el segundo paso de la guía, se debía encontrar la correlación entre dos señales asignadas por la guía, donde la correlación cruzada mide la similitud entre dos señales en distintos desplazamientos. Además, se debía obtener la representación gráfica y secuencial. Para realizar este punto, utilizamos el siguiente código, el cual se explicará a continuación:

# CODIGO
```Python
fs = 1 / (1.25e-3)  # Frecuencia de muestreo
n = np.arange(9)  # 9 muestras

x1_n = np.cos(2 * np.pi * 100 * n * (1.25e-3))
x2_n = np.sin(2 * np.pi * 100 * n * (1.25e-3))
```
- `fs -`==1 / (1.25e-3): Calcula la frecuencia de muestreo en Hz.
 - `np.arange(9)  `= Genera una secuencia de 9 valores (índices del tiempo).
- ` x1_n `= Señal cosenoidal con frecuencia de 100 Hz.
- `x2_n `=Señal senoidal con frecuencia de 100 Hz.

A continuación, se calculará la correlación cruzada, la cual mide la similitud entre dos señales en distintos desplazamientos. En esencia, nos indica cuánto se asemeja una señal a otra cuando se desplaza en el tiempo. Para ello, se aplicará la siguiente línea de código entre x1_n y x2_n:
```Python
corr = correlate(x1_n, x2_n, mode='full')
```
Y por último se va a graficar el resultado esperado, para eso se utiliza las siguientes líneas de código que se explicaran a continuación:
```Python
fig, axs = plt.subplots(3, 1, figsize=(10, 8))
axs[0].stem(n, x1_n, basefmt=" ")
axs[0].set_title("Señal x1[n] = cos(2π100nTs)")
axs[0].set_xlabel("n")
axs[0].set_ylabel("x1[n]")

axs[1].stem(n, x2_n, basefmt=" ")
axs[1].set_title("Señal x2[n] = sin(2π100nTs)")
axs[1].set_xlabel("n")
axs[1].set_ylabel("x2[n]")

axs[2].stem(range(-len(n) + 1, len(n)), corr, basefmt=" ")
axs[2].set_title("Correlación cruzada entre x1[n] y x2[n]")
axs[2].set_xlabel("Desplazamiento")
axs[2].set_ylabel("Correlación")

plt.tight_layout()
plt.show()
```
- `plt.subplots(3, 1, figsize `=(10,8)) crea una figura (fig) con tres gráficos (axs[0], axs[1], axs[2]) organizados en una sola columna (1) y tres filas (3).
- `figsize `=(10,8) define el tamaño de la figura en pulgadas (10 de ancho y 8 de alto).
Esto va a permitir que se puedan visualizar tres señales al mismo tiempo para facilitar su comparación.
```Python
axs[0].stem(n, x1_n, basefmt=" ")
axs[0].set_title("Señal x1[n] = cos(2π100nTs)")
axs[0].set_xlabel("n")
axs[0].set_ylabel("x1[n]")
```
- `axs[0] ` se refiere al primer gráfico en la figura.
- `stem(n, x1_n, basefmt `=" ") genera un gráfico de tallos (stem plot) que representa la señal x1_n (cosenoidal).
- `set_title() `agrega el título del gráfico.
- `set_xlabel() y set_ylabel()-`etiquetan los ejes.
Por medio de esto nos permite observar el primer grafico que es x1n=cos(2π100nTs), una onda cosenoidal.
```Python
axs[1].stem(n, x2_n, basefmt=" ")
axs[1].set_title("Señal x2[n] = sin(2π100nTs)")
axs[1].set_xlabel("n")
axs[1].set_ylabel("x2[n]")
```
Para graficar la segunda señal x2n=sin(2π100nTs), una onda senoidal, donde se realizó el mismo procedimiento anterior y por ultimo para representar la correlación cruzada se hizo lo siguiente:
```Python
axs[2].stem(range(-len(n) + 1, len(n)), corr, basefmt=" ")
axs[2].set_title("Correlación cruzada entre x1[n] y x2[n]")
axs[2].set_xlabel("Desplazamiento")
axs[2].set_ylabel("Correlación")
```
- `axs[2]  ` representa el tercer gráfico, que muestra la correlación cruzada.
- ` stem(range(-len(n) + 1, len(n)), corr, basefmt `=" "):
- `Se usa range(-len(n) + 1, len(n)) ` para definir el eje de desplazamientos de la correlación.
- `Se grafica corr-`, que contiene los valores de la correlación entre x1_n y x2_n.
  

Para el ultimo punto de la guía se debía descargar una señal de physionet de EEG y realizar los siguientes puntos:

`i.` Caracterice la señal en función del tiempo, esto es, calcule sus estadísticos descriptivos, frecuencia de muestreo, etc.

`ii.` Describa la señal en cuanto a su clasificación. 

`iii.` Aplique la transformada de Fourier de la señal y grafique tanto su transformada, como su densidad espectral. 

`iv.` Analice los estadísticos descriptivos en función de la frecuencia:

      • Frecuencia media
      • Frecuencia mediana
      • Desviación estándar
      • Histograma de frecuencias

Para el punto i se realizo el siguiente codigo, que se explicara a continuación:
```Python
# Calcular estadísticas de la señal
mean_freq = np.mean(frequencies[:fs//2])
median_freq = np.median(frequencies[:fs//2])
std_freq = np.std(frequencies[:fs//2])

# Graficar histograma de frecuencias
plt.figure(figsize=(8, 4))
plt.hist(frequencies[:fs//2], bins=30, alpha=0.75, color='b', edgecolor='black')
plt.title("Histograma de Frecuencias")
plt.xlabel("Frecuencia [Hz]")
plt.ylabel("Ocurrencias")
plt.show()

# Mostrar estadísticas
print(f"Frecuencia media: {mean_freq:.2f} Hz")
print(f"Frecuencia mediana: {median_freq:.2f} Hz")
print(f"Desviación estándar: {std_freq:.2f} Hz")
```

Para calcular los datos estadisticos descriptivos se utilizo el siguiente codigo:
```Python
mean_freq = np.mean(frequencies[:fs//2])
median_freq = np.median(frequencies[:fs//2])
std_freq = np.std(frequencies[:fs//2])
```
- `np.mean(frequencies[:fs//2])`: Calcula la frecuencia media de la señal.
✅ np.median(frequencies[:fs//2]): Calcula la frecuencia mediana.
✅ np.std(frequencies[:fs//2]): Calcula la desviación estándar, indicando la dispersión de las frecuencias.


