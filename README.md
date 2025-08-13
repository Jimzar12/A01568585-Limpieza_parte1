
# Limpieza de Datos con Pandas

Este tutorial muestra cómo limpiar y preparar datos utilizando **Python** y la librería **Pandas**. Usaremos un archivo Excel llamado `Run Times.xlsx` que contiene información de tiempos de carrera, cuotas y otras variables.

## 📂 Archivos necesarios

- `Run Times.xlsx` — Dataset con los datos de tiempos de carrera.


## 1️⃣ Importar librerías y cargar datos

```python
import pandas as pd

# Cargar el archivo Excel
run_times = pd.read_excel('Run Times.xlsx')

# Ver los primeros registros
run_times.head()
````

***

## **2️⃣ Inspección inicial de los datos**

Podemos inspeccionar tipos de datos y estructura del DataFrame:

```
# Tipos de datos
run_times.dtypes

# Información general
run_times.info()
```

Observa que el tipo de dato de *Fee* es object, pero queremos que sea numérico

***

## 3️⃣ Limpieza de la columna

## **Fee**

La columna Fee contiene el símbolo $ y está almacenada como texto (tipo object). Para usarla en operaciones numéricas, debemos limpiar el símbolo y convertirla a un tipo numérico.

```
# Eliminar símbolo '$' y convertir a numérico
run_times.Fee = pd.to_numeric(run_times.Fee.str.replace('$', ''))

# Verificar cambios
run_times.info()
run_times.Fee.mean()
```

También es posible acceder a la columna con \[]:

```
run_times['Fee'].mean()
```

***

## **4️⃣ Limpieza de la columna**

## **Warm Up Time**

La columna Warm Up Time contiene valores como "3 min". Necesitamos remover la palabra "min" y convertir los valores a numérico.

```
# Remover ' min' y convertir a numérico
run_times['Warm Up Time'] = pd.to_numeric(
    run_times['Warm Up Time'].astype(str).str.replace(' min', ''),
    errors='coerce'
)

run_times['Warm Up Time'].head()
```

***

## **5️⃣ Conversión de datos booleanos a enteros**

La columna Rain es booleana (True/False). Podemos convertirla a enteros (1/0):

```
run_times['Rain'] = run_times.Rain.astype(int)
```

***

## **6️⃣ Resultado final**

Después de estas transformaciones, tendremos un DataFrame listo para análisis:

```
run_times.info()
run_times.head()
```

***

## **📊 Resumen de pasos realizados**

1. **Carga de datos** desde Excel con pd.read\_excel().

2. **Inspección de datos** con .dtypes y .info().

3. **Limpieza de valores monetarios** (remover $ y convertir a numérico).

4. **Limpieza de valores de tiempo** (remover " min" y convertir a numérico).

5. **Conversión de booleanos a enteros** (True → 1, False → 0).

***
