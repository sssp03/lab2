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


Luego de haber realizado esos puntos a manos, procedimos a calcular y1(n) ,   y2(n), junto con sus gráficas respectivas usando Python. 
El primer paso fue instalar las siguientes librerías

```Python
import numpy as np
import matplotlib.pyplot as plt
```
•	numpy : Para trabajar con arreglos numéricos 

•	 matplotlib.pyplot : Para generar gráficos.

Después, se establecieron los valores cómo se había hecho anteriormente con los datos de las integrantes

```Python
h1_n = np.array([5, 6, 0, 0, 7, 1, 3])
x1_n = np.array([1, 0, 5, 3, 4, 4, 2, 3, 9, 9])
h2_n = np.array([5, 6, 0, 0, 7, 2, 1])
x2_n = np.array([1, 0, 0, 0, 2, 4, 1, 8, 2, 2])
```
•	np.array : Utilizado para definir los datos como vectores

Ya teniendo los datos, procedemos a calcular la convolución en el programa

```Python
y1_n = np.convolve(x1_n, h1_n, mode='full')
y2_n = np.convolve(x2_n, h2_n, mode='full')
```
•	np.convolve(): Es una función de numpy que calcula la convolución entre dos secuencias.

•	mode='full': Devuelve la convolución completa, sin recortar valores.

Con la convolución ya calculada podemos empezar a graficar para y1(n), y2(n) por aparte 

```Python
plt.figure(figsize=(10, 5))
```
•	plt.figure:  Crea una nueva figura con un tamaño específico.

# Gráfica para y1(n)

```Python
plt.subplot(2, 1, 1)
plt.stem(y1_n)
plt.xlabel('n')
plt.ylabel('y1(n)')
plt.title('Convolución de h1(n) y x1(n)')
plt.grid()
```

•	plt.subplot(2,1,1): Se divide la figura en 2 filas y 1 columna, seleccionando la primera fila.

•	plt.stem(y1_n): Se dibuja la señal y1_n en forma de gráfico de puntos y líneas verticales (gráfico de señales discretas).

•	plt.grid():  en Matplotlib se usa para agregar una cuadrícula a un gráfico, lo que facilita la visualización de los datos.

•	plt.xlabel: Utiliza para poner títulos en la gráficas dependiendo el eje

# Gráfica para y2(n)

```Python
plt.subplot(2, 1, 2)
plt.stem(y2_n)
plt.xlabel('n')
plt.ylabel('y2(n)')
plt.title('Convolución de h2(n) y x2(n)')
plt.grid()
```
Mismos pasos que antes, pero graficando y2(n).

Por último, se muestran y se ajustan las gráficas realizadas

```Python
plt.tight_layout()
plt.show()
```
•	plt.tight_layout(): Ajusta los subgráficos para que no se superpongan.

•	plt.show(): Muestra la figura en pantalla.

Se imprimen los valores

```Python
print("y1(n) =", y1_n)
print("y2(n) =", y2_n)
```


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

![image](https://github.com/user-attachments/assets/56c6f4c9-4708-47ce-931a-c081dbf934ad)

  
Para el último punto de la guía, se debía descargar una señal de EEG desde PhysioNet. Esta señal corresponde al primer segmento de los datos de EEG del paciente 0284 de la cohorte de pacientes de I-CARE. El registro comienza 4 horas, 7 minutos y 23 segundos después del paro cardíaco y finaliza 4 horas, 59 minutos y 59 segundos después del evento.  

El archivo de encabezado en texto plano 0284_001_004_EEG.hea proporciona detalles sobre el contenido de la señal, incluyendo la hora de inicio, la hora de finalización y la frecuencia de la red eléctrica (también conocida como frecuencia de línea o de la red eléctrica).  

A partir de esta señal, se debían realizar los siguientes análisis:

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
import numpy as np
import matplotlib.pyplot as plt

# ================================
# 1️⃣ DEFINIR LA SEÑAL Y FRECUENCIA DE MUESTREO
# ================================
fs = 1000  # Frecuencia de muestreo en Hz
t = np.linspace(0, 1, fs, endpoint=False)  # 1 segundo de datos

# Generar una señal de prueba con ruido (puedes cambiarla según tu caso)
signal = np.sin(2 * np.pi * 50 * t) + 0.5 * np.sin(2 * np.pi * 120 * t) + np.random.normal(0, 0.2, len(t))

# ================================
# 2️⃣ CÁLCULO DE ESTADÍSTICOS DESCRIPTIVOS
# ================================
mean_value = np.mean(signal)  # Media de la señal
median_value = np.median(signal)  # Mediana de la señal
std_value = np.std(signal)  # Desviación estándar
max_value = np.max(signal)  # Valor máximo
min_value = np.min(signal)  # Valor mínimo
rms_value = np.sqrt(np.mean(signal**2))  # Valor RMS (Root Mean Square)

# ================================
# 3️⃣ MOSTRAR LOS RESULTADOS
# ================================
print(f"Frecuencia de muestreo: {fs} Hz")
print(f"Media de la señal: {mean_value:.4f}")
print(f"Mediana de la señal: {median_value:.4f}")
print(f"Desviación estándar: {std_value:.4f}")
print(f"Valor máximo: {max_value:.4f}")
print(f"Valor mínimo: {min_value:.4f}")
print(f"Valor RMS: {rms_value:.4f}")

# ================================
# 4️⃣ GRAFICAR LA SEÑAL EN FUNCIÓN DEL TIEMPO
# ================================
plt.figure(figsize=(10, 4))
plt.plot(t, signal, label="Señal", color='b')
plt.xlabel("Tiempo [s]")
plt.ylabel("Amplitud")
plt.title("Señal en el dominio del tiempo")
plt.legend()
plt.grid()
plt.show()

# ================================
# 5️⃣ HISTOGRAMA DE LA DISTRIBUCIÓN DE LA SEÑAL
# ================================
plt.figure(figsize=(8, 4))
plt.hist(signal, bins=30, alpha=0.75, color='c', edgecolor='black')
plt.xlabel("Amplitud de la señal")
plt.ylabel("Frecuencia")
plt.title("Histograma de la señal")
plt.grid()
plt.show()
```
Como primer paso definimos la señal y la frecuencia de muestreo:
```Python
fs = 1000  # Frecuencia de muestreo en Hz
t = np.linspace(0, 1, fs, endpoint=False)  # 1 segundo de datos
```
-fs = 1000: Indica que la señal está muestreada a 1000 Hz (1000 puntos por segundo).
-t = np.linspace(0, 1, fs, endpoint=False): Genera un vector de tiempo de 1 segundo con 1000 puntos.
Despues va a generar un a señal de prueba
```Python
signal = np.sin(2 * np.pi * 50 * t) + 0.5 * np.sin(2 * np.pi * 120 * t) + np.random.normal(0, 0.2, len(t))
```
-`np.sin(2 * np.pi * 50 * t)`: Componente senoidal a 50 Hz.
-`0.5 * np.sin(2 * np.pi * 120 * t)`: Componente senoidal más débil a 120 Hz.
-`np.random.normal(0, 0.2, len(t))`: Ruido aleatorio con media 0 y desviación 0.2 (para simular una señal real).

Se va a calcular los estadisticos descriptivos por medio del siguiente codigo:
```Python
mean_value = np.mean(signal)  # Media de la señal
median_value = np.median(signal)  # Mediana de la señal
std_value = np.std(signal)  # Desviación estándar
max_value = np.max(signal)  # Valor máximo
min_value = np.min(signal)  # Valor mínimo
rms_value = np.sqrt(np.mean(signal**2))  # Valor RMS
```
-`Media (mean)`: Promedio de todos los valores de la señal.
  
-` Mediana (median)`: Valor central cuando los datos están ordenados.

-`Desviación estándar (std)`: Cuánto varían los datos respecto a la media.

-`Máximo y mínimo (max y min)`: Valores extremos de la señal.

-`Valor RMS (Root Mean Square)`: Indica la potencia de la señal (común en ingeniería eléctrica).
Para realizar el histograma de la distribucion de valores de la señal se necesitaron las siguientes lineas de codigo:
```Python
plt.figure(figsize=(8, 4))
plt.hist(signal, bins=30, alpha=0.75, color='c', edgecolor='black')
plt.xlabel("Amplitud de la señal")
plt.ylabel("Frecuencia")
plt.title("Histograma de la señal")
plt.grid()
plt.show()
```
Donde `plt.hist(signal, bins=30)`: Crea un histograma con 30 intervalos (bins).
![image](https://github.com/user-attachments/assets/861a73f0-391f-421c-bc0f-7b03257e24d5)

En el punto ii, se puede afirmar que una señal de EEG es originalmente continua en el tiempo, ya que es una señal biológica análoga que varía de manera suave y sin interrupciones. Sin embargo, al ser registrada digitalmente en un sistema de adquisición de datos, se convierte en una señal discreta, debido a que es muestreada a intervalos regulares de tiempo. Esto ocurre porque los dispositivos de EEG capturan la señal a una frecuencia de muestreo específica, que puede ser de 250 Hz, 500 Hz o incluso 1000 Hz. Como resultado, en lugar de tener un valor en cada instante de tiempo, solo se registran valores en momentos determinados.

Para realizar el iii se realizo el siguiente procedimiento:
```Python
fft_values = np.fft.fft(signal)
frequencies = np.fft.fftfreq(len(signal), 1/fs)
```
-`np.fft.fft(signal)`:Calcula la Transformada de Fourier de la señal, convirtiéndola del dominio del tiempo al dominio de la frecuencia, devuelve un array complejo donde la magnitud indica la intensidad de cada frecuencia y el ángulo indica la fase.
-`np.fft.fftfreq(len(signal), 1/fs)`:Calcula las frecuencias correspondientes a cada componente en la FFT.fs es la frecuencia de muestreo, por lo que 1/fs es el período de muestreo.

Para graficar el espectro de frecuencia se realizo el sguiente codigo:
```Python
axs[0].plot(frequencies[:fs//2], np.abs(fft_values[:fs//2]))
axs[0].set_title("Espectro de frecuencia (FFT)")
axs[0].set_xlabel("Frecuencia [Hz]")
axs[0].set_ylabel("Magnitud")
```
-`np.abs(fft_values[:fs//2])`:Obtiene la magnitud de la Transformada de Fourier, se usa [:fs//2] para mostrar solo la mitad positiva del espectro, ya que la FFT genera valores simétricos alrededor de 0.
Cálculo de la Densidad Espectral de Potencia (PSD):
```Python
psd = np.abs(fft_values) ** 2
```
Eleva al cuadrado la magnitud de la FFT para obtener la potencia de cada componente de frecuencia,cuanto mayor sea este valor, más energía tiene la señal en esa frecuencia.

![image](https://github.com/user-attachments/assets/5adf5835-46b3-4b35-ae5c-3f79ac9079c4)

Donde se puede observar que entre 50hz y 120 hz tiene mas picos es porque en esa parte hay mayor energia.

A partir de la señal seleccionada, procedimos a calcular los estadísticos descriptivos

```Python
mean_freq = np.mean(frequencies[:fs//2])
median_freq = np.median(frequencies[:fs//2])
std_freq = np.std(frequencies[:fs//2])
```

•	frequencies[:fs//2]: frequencies contiene las frecuencias obtenidas con la Transformada de Fourier (FFT). fs//2 significa tomar solo la mitad positiva del espectro, ya que la FFT genera valores simétricos en torno a cero. La frecuencia máxima en la FFT es la frecuencia de Nyquist (fs/2f_s/2).

•	np.mean(frequencies[:fs//2]) :Calcula la frecuencia media, que representa el promedio de las frecuencias en la señal.

•	np.median(frequencies[:fs//2]) :Calcula la frecuencia mediana, el valor que divide en dos partes iguales el conjunto de frecuencias.

•	np.std(frequencies[:fs//2]):Calcula la desviación estándar, que indica cuánta variación hay en las frecuencias respecto a la media.

Luego de haber realizados los respectivos cálculos, se graficó el histograma

```Python
plt.figure(figsize=(8, 4))
plt.hist(frequencies[:fs//2], bins=30, alpha=0.75, color='b', edgecolor='black')
plt.title("Histograma de Frecuencias")
plt.xlabel("Frecuencia [Hz]")
plt.ylabel("Muestras")
plt.show()
```

Donde:
•	plt.figure(figsize=(8, 4)):Crea una nueva figura con tamaño de 8x4 pulgadas.

•	plt.hist(frequencies[:fs//2], bins=30, alpha=0.75, color='b', edgecolor='black')

•	plt.hist() : Crea un histograma, que es una gráfica de barras que muestra la distribución de valores.

•	frequencies[:fs//2]: Usa solo la parte positiva del espectro.

•	bins=30: Divide el rango de frecuencias en 30 intervalos.

•	alpha=0.75: Ajusta la transparencia de las barras.

•	color='b': Usa color azul para las barras.

•	edgecolor='black': Contorno negro para las barras.

•	plt.title("Histograma de Frecuencias") : Título del gráfico

•	plt.xlabel("Frecuencia [Hz]"): Titulo del eje X   

•	plt.ylabel("Muestras"): Titulo del eje Y

•	plt.show() Muestra el gráfico

Se imprime la información:

```Python
print(f"Frecuencia media: {mean_freq:.2f} Hz")
print(f"Frecuencia mediana: {median_freq:.2f} Hz")
print(f"Desviación estándar: {std_freq:.2f} Hz")
```

•	print(f"Frecuencia media: {mean_freq:.2f} Hz"): Muestra la frecuencia media con 2 decimales.

•	print(f"Frecuencia mediana: {median_freq:.2f} Hz"): Muestra la frecuencia mediana con 2 decimales.

•	print(f"Desviación estándar: {std_freq:.2f} Hz"): Muestra la desviación estándar, indicando qué tan dispersas están las frecuencias alrededor de la media.























