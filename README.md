# Clínica Veterinaria Patitas - TPO Programación Orientada a Objetos

Trabajo práctico obligatorio de POO (2026, 2do cuatrimestre). Elegimos la **Propuesta B: Clínica veterinaria**.

El sistema maneja los dueños y sus mascotas (perros, gatos, aves y conejos), los turnos de cada veterinario sin superposiciones, las urgencias, la historia clínica con consultas, tratamientos y vacunas, el stock de medicamentos e insumos por lote, la facturación con distintos medios de pago y el plan de salud, y los recordatorios de vacunas. Se usa por consola con un menú y los datos se guardan en un archivo para que no se pierdan al cerrar.

## Integrantes

- Bustamante, Enrique
- Franco, Tomás
- Suárez, Elian

## Requisitos

- Java 17 o superior (lo probamos con Java 17 y 21)
- Maven 3.8 o superior (o un IDE que abra proyectos Maven, como IntelliJ IDEA o Eclipse)

## Cómo ejecutarlo

Desde la carpeta del proyecto:

```
mvn package
java -jar target/clinica-patitas.jar
```

`mvn package` compila, corre las pruebas unitarias y arma el jar en `target/`.

Desde IntelliJ: abrir la carpeta del proyecto (lo reconoce como proyecto Maven) y ejecutar la clase `clinica.Main`.

Si en la consola de Windows los acentos se ven raros, ejecutar antes `chcp 65001` o correrlo desde la consola de IntelliJ.

## Cómo correr las pruebas

```
mvn test
```

Son 54 pruebas unitarias con JUnit 5 sobre la lógica de negocio (están en `/test`).

## Datos de prueba

La primera vez que se ejecuta, como no existe `datos/clinica.dat`, el programa carga datos de prueba. Las fechas se calculan a partir del día en que se ejecuta. Para volver a empezar de cero, borrar la carpeta `datos/`.

| Tipo | Datos |
|---|---|
| Veterinaria | Laura Gómez, DNI **30111222**, clínica general, lunes a sábado de 9 a 19, **de guardia** |
| Veterinario | Martín Pérez, DNI **28999888**, cirugía, lun/mié/vie de 9 a 13 y mar/jue de 14 a 19 |
| Recepcionista | Sofía Ruiz, DNI **35123456** (sirve para probar que no puede cargar diagnósticos) |
| Administrador | Carlos Díaz, DNI 25987654 |
| Dueña con plan de salud | Ana López, DNI 40111222. Mascotas: #1 Firulais (perro), #2 Michi (gata) |
| Dueño sin plan | Juan Martínez, DNI 38222333. Mascotas: #3 Kiwi (ave), #4 Copo (conejo) |
| Dueño con 3 ausencias | Pedro Sosa, DNI 41333444 (tiene que pagar seña). Mascota: #5 Toby (cachorro de 1 mes) |
| Medicamentos | AMOX (Amoxicilina), MELOX (Meloxicam, ya está en el stock mínimo) |
| Insumos | JER (jeringas, queda 1 por encima del mínimo), GAS (gasas) |
| Vacunas (productos) | V-ANT (tiene un lote vencido), V-SEX, V-TRI, V-MIX |
| Catálogo de vacunas | Antirrábica, Séxtuple, Triple felina, Mixomatosis |

También hay turnos cargados para el próximo día hábil (Laura: 10:00 Firulais, 10:30 Michi, 11:00 Kiwi) y una cirugía de Copo con Martín. Firulais y Copo tienen un refuerzo de vacuna dentro de los próximos días, así aparecen en el reporte de vacunas próximas a vencer.

En las opciones de cancelar turno, registrar ausencia y registrar urgencia se puede ingresar la fecha y hora del momento (o dejarlo vacío para usar la actual). Lo pusimos así para poder probar las reglas que dependen del horario.

## Archivos que genera

- `datos/clinica.dat`: todos los datos (se guarda al salir o con la opción 7 del menú)
- `datos/notificaciones.txt`: los avisos a dueños y al administrador (turnos, urgencias, recordatorios, stock bajo)
- `datos/reporte.txt`: el reporte del administrador (opción 6 > 7)

## Estructura del repositorio

```
/docs                 enunciado, documento de la Etapa 1, informe final y plan de pruebas
/docs/uml             diagramas de clases implementados (.png y fuente .mmd de Mermaid)
/docs/pruebas         entrada y salida de la ejecución del plan de pruebas funcionales
/src/clinica          código fuente
    /modelo           personas, mascotas, turnos, historia, stock, facturacion
    /controladores    un controlador por grupo de casos de uso
    /servicios        stock, recordatorios y notificaciones
    /persistencia     repositorios y guardado en archivo
    /excepciones      excepciones propias
    /vista            menú por consola
/test                 pruebas unitarias (JUnit 5)
pom.xml
```
