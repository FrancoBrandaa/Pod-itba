# Guías prácticas — Programación de Objetos Distribuidos

Repositorio de resoluciones y material de apoyo para las guías prácticas de la materia **Programación de Objetos Distribuidos (POD)**.

## Requisitos

- Java 25 (JDK)
- Maven
- IntelliJ IDEA, sugerido por la cátedra pero no obligatorio

Antes de compilar, verificá que Maven use Java 25:

```bash
./mvn-java25 -version
```

## Organización

Cada trabajo práctico es un módulo Maven independiente dentro de `practicas/`.

```text
practicas/
  tp-XX-nombre-de-la-guia/
    README.md
    pom.xml
    enunciados/
      ejercicio-XX.md
    soluciones/
      ejercicio-XX.md
    src/main/java/
```

- `enunciados/` conserva cada consigna en Markdown.
- `soluciones/` contiene el razonamiento y la respuesta de cada ejercicio.
- `src/main/java/` se utiliza cuando un ejercicio requiere código Java.
- Se agregan tests únicamente si la consigna lo solicita.

## Compilación

Desde la raíz del repositorio:

```bash
./mvn-java25 verify
```

El script `mvn-java25` selecciona el JDK 25 instalado por Homebrew para este proyecto, sin modificar el Java global de la terminal.
