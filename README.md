# Mi proyecto

Herramienta de consola desarrollada en Python para procesar una cartera de créditos, clasificar el riesgo de sus clientes y generar un archivo para su revisión.

## Que area usa esta herramienta

El área de Créditos y Riesgos utiliza la herramienta para conocer el saldo pendiente de la cartera e identificar los clientes con mayor exposición.

## Que problema resuelve

El área recibe datos en un CSV que puede contener campos vacíos, formatos distintos de números y fechas, y registros duplicados.

La herramienta valida los datos, registra los rechazos con su fila y motivo, elimina duplicados por RUC y guarda los clientes válidos en SQLite. Después permite calcular indicadores, consultar clientes y exportar la cartera clasificada.

Los datos utilizados son ficticios y fueron creados con el generador del curso.

## Como se ejecuta

Se utilizó Python 3.12. desde la terminal de VS Code, ubicada en la carpeta del proyecto, se puede preparar el entorno con estos comandos.

```
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Para iniciar la aplicación se ejecuta este comando.

```
.\.venv\Scripts\python.exe .\main.py
```

El archivo de entrada debe estar ubicado en `data/data_mipe.csv`.

## Indicadores que calcula

- Distribución por riesgo indica cuántos clientes pertenecen a cada nivel de riesgo.
- Exposición total es la suma del saldo actual de todos los clientes.
- Exposición por riesgo es la suma de los saldos de los clientes de cada nivel.
- Saldo promedio por sector es el promedio del saldo actual de los clientes de cada sector.
- Diez clientes con mayor exposición identifica los diez saldos pendientes más altos.

## Mi regla de negocio

El nivel inicial se asigna según los días de atraso.

| Días de atraso | Nivel inicial |
|---|---|
| De 0 a 8 | Normal |
| De 9 a 30 | Con Problemas |
| De 31 a 60 | Deficiente |
| De 61 a 120 | Dudoso |
| Más de 120 | Pérdida |

Para este proyecto, se eligió subir un nivel cuando el saldo actual es positivo y alcanza al menos el 50 % de las ventas anuales. El nivel máximo es Pérdida.

Por ejemplo, un cliente con 12 días de atraso comienza en Con Problemas. Si tiene un saldo de 60 000 y ventas anuales de 100 000, pasa a Deficiente.