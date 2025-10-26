
🧠 Control II — Lenguajes de Programación II (2025)
Profesor: Alonso Inostrosa Psijas
Fecha de entrega: 28/10/2025
Tema: Ejecución Especulativa en Go


👥 Integrantes

Nikolas Lagos
Dante Chavez


🔗 Enlace al repositorio
Repositorio GitHub: Próximamente


⚙️ Instrucciones de compilación y ejecución
🔧 Requisitos

Tener instalado Go (v1.20 o superior).
Clonar o descargar este proyecto en una carpeta local.
▶️ Ejecución
En la terminal, ubicarse dentro del directorio raíz del proyecto y ejecutar:
go run main.go


El programa:

Ejecuta 30 veces el modo especulativo (rutinas/rutinas.go)
Luego ejecuta 30 veces el modo secuencial (lineal/lineal.go)
Registra todos los resultados en el archivo resultados.txt


🧩 Análisis de rendimiento (reporte simple)
El análisis se realizó comparando las ejecuciones secuencial (no especulativa) y especulativa (concurrencia con goroutines).
1️⃣ Ejecución Secuencial

Implementada en el archivo lineal/lineal.go
No utiliza goroutines ni canales.
Flujo de ejecución:Determina primero la condición (rama ganadora).
Luego ejecuta la tarea correspondiente de forma lineal.
2️⃣ Ejecución Especulativa (Concurrente)

Implementada en el archivo rutinas/rutinas.go
Ambas ramas (EncontrarPrimosConCancelacion y CalcularTrazaConCancelacion) se lanzan en paralelo con goroutines y se coordinan mediante canales (chan).
Cuando se determina la condición, el programa cancela la rama no necesaria utilizando context.Cancel.
Los inputs fijos utilizados para ambas estrategias están configurados en main.go:
iteraciones := 30
maxPrimos := "30000000"
maxMatriz := "1200"
ruta := "A"
mainWork := "6"


El archivo de salida resultados.txt contiene las 30 ejecuciones de cada tipo, registrando los tiempos individuales y luego el promedio.
3️⃣ Resultados promedio y Speedup
De acuerdo con los datos procesados en Excel (datoss.xlsx):

Estrategia	Tipo de ejecución	Tiempo promedio (s)	Speedup
Lineal	Secuencial (no especulativa)	23.5	—
Rutinas	Concurrente (especulativa)	20.2	1.16x

Fórmula utilizada:
\text{Speedup} = \frac{T_{secuencial}}{T_{especulativo}} = \frac{23.5}{20.2} = 1.16

Por lo tanto, la ejecución especulativa fue aproximadamente 16 % más rápida que la versión secuencial.


🧾 Archivos incluidos

main.go → Programa principal de medición
lineal/lineal.go → Implementación secuencial
rutinas/rutinas.go → Implementación especulativa
resultados.txt → Resultados crudos de las 30 ejecuciones
datoss.xlsx → Promedios y cálculo de Speedup
