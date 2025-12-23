# 🚀 JMeter Template

Este repositorio contiene un plan de pruebas de JMeter (.jmx) diseñado exclusivamente para el **análisis de rendimiento (Performance Testing)** de APIs REST. El objetivo principal es medir la eficiencia, tiempos de respuesta y estabilidad de los endpoints bajo una carga controlada.


## 🏗️ Arquitectura del Script

El script está optimizado para capturar métricas de rendimiento precisas mediante una configuración técnica detallada:

* ⏱️ Control de Concurrencia: Configurado con 15 hilos (threads) y un ramp-up de 5 segundos para estabilizar las mediciones de rendimiento.
* 🔐 Ciclo de Vida de Autenticación: 
    - Gestión dinámica de tokens (Access/Refresh) mediante JSON PostProcessors.
    - Reutilización de identidad para evitar latencias innecesarias en cada petición.
* 🔗 Dinamismo de Datos: Extrae IDs aleatorios de productos en tiempo real para asegurar que las pruebas de rendimiento en los métodos PUT y PATCH no se vean afectadas por el almacenamiento en caché del servidor.
* ⚙️ Centralización de Umbrales: Permite definir el SLA (Service Level Agreement) de tiempo de respuesta global mediante la variable `response_time`.


## 🧪 Validaciones de Rendimiento (Assertions)

Para asegurar que el rendimiento sea aceptable, cada petición incluye verificaciones automáticas:

1. Duration Assertion: El test falla automáticamente si el tiempo de respuesta supera el umbral configurado (ej. 1500ms).
2. Size Assertion: Verifica que el servidor no solo responda rápido, sino que entregue el volumen de datos correcto.
3. Response & JSON Assertion: Garantiza que la latencia medida corresponde a una respuesta exitosa y estructuralmente válida.


## 🛠️ Tecnologías Usadas

| Herramienta | Versión | Uso |
|-----------|---------|-----|
| Apache JMeter | 5.6.3+ | Motor de análisis de performance |
| Java JRE | 17+ | Entorno de ejecución |
| DummyJSON API | - | Backend de pruebas para benchmarking |


## ▶️ Ejecución y Análisis

Para obtener resultados de rendimiento confiables, se recomienda la ejecución mediante línea de comandos para minimizar el consumo de recursos locales:

jmeter -n -t "Plan de Pruebas.jmx" -l resultados.jtl -e -o ./dashboard_rendimiento

Esto generará un **Dashboard HTML** con gráficos de:
* Tiempos de respuesta (Over Time).
* Latencia vs. Tamaño de respuesta.
* Percentiles de rendimiento.


## 📄 Escenarios de Rendimiento Cubiertos

1. Performance de Autenticación: Medición del tiempo de login.
2. Rendimiento de Lectura (GET): Análisis de tiempos en listados y perfiles de usuario.
3. Rendimiento de Escritura (POST/PUT/PATCH): Evaluación de la latencia en operaciones de persistencia de datos.


## ⭐ Conclusión

Este template es una herramienta ideal para establecer líneas base de rendimiento (baselines) y validar que los cambios en el código no introduzcan degradaciones en la velocidad de respuesta de la API.

## Licencia

Este proyecto utiliza la [Licencia MIT](https://opensource.org/licenses/MIT).