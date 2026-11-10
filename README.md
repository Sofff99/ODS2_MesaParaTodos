[documentaci_n_del_proyecto.md](https://github.com/user-attachments/files/34607132/documentaci_n_del_proyecto.md)
# Documentación del Proyecto Integrador - MVP (Tkinter)

## 1. Descripción General del Proyecto

Este proyecto es un **Producto Mínimo Viable (MVP)** desarrollado en **Python** utilizando la librería nativa de interfaz gráfica **Tkinter** (y sus módulos derivados como `ttk`). La aplicación funciona mediante un menú principal interactivo desde el cual se ejecutan diferentes módulos modulares en ventanas secundarias (`Toplevel`).

El objetivo principal es demostrar componentes clave de la construcción de interfaces gráficas de usuario (GUI) en Python, tales como formulación de datos, manipulación de listas (CRUD básico), representación visual en tablas (Treeview) y renderizado de gráficos/formas (Canvas).

---

## 2. Estructura de Archivos y Configuración (`launch.json`)

De acuerdo a la estructura del workspace, el código fuente está organizado dentro de un directorio `src/`, con el punto de entrada situado en `src/app/main.py`.

### Configuración de Depuración de VS Code (`.vscode/launch.json`)

Para asegurar que los módulos locales dentro del directorio `src/` puedan ser importados correctamente sin problemas de rutas (`ModuleNotFoundError`), se configuró la variable de entorno `PYTHONPATH`.

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Programa con PYTHONPATH=src",
            "type": "python",
            "request": "launch",
            "program": "${workspaceFolder}/src/app/main.py",
            "cwd": "${workspaceFolder}",
            "env": { 
                "PYTHONPATH": "${workspaceFolder}/src" 
            },
            "console": "integratedTerminal",
            "justMyCode": true
        }
    ]
}
```

* **`program`**: Define la ruta raíz de ejecución en `${workspaceFolder}/src/app/main.py`.
* **`env.PYTHONPATH`**: Agrega la carpeta `${workspaceFolder}/src` al path de ejecución de Python para permitir importaciones absolutas entre módulos.

---

## 3. Explicación de los Componentes y Ventanas

A continuación se detalla la arquitectura de la interfaz gráfica compuesta por 6 ventanas/secciones:

### 3.1. Ventana Principal: Menú de Navegación (`Proyecto Integrador - MVP`)
* **Propósito**: Actúa como la ventana raíz (`Tk()`).
* **Componentes**: Contiene un título principal ("Aplicación Demo (tkinter)"), una serie de botones alineados verticalmente que despliegan cada sub-ventana y un botón para salir de la aplicación.
* **Flujo**: Cada botón activa un callback que instancia la ventana gráfica correspondiente sin bloquear la ventana principal.

---

### 3.2. Módulo 1: Home / Bienvenida
* **Propósito**: Pantalla de presentación simple.
* **Componentes**:
  * Etiqueta de saludo (`Label`): "¡Bienvenid@s!" y texto informativo.
  * Botón "Mostrar mensaje": Dispara una ventana emergente de diálogo (`messagebox.showinfo`).
  * Botón "Cerrar": Cierra la ventana emergente actual mediante el método `.destroy()`.

---

### 3.3. Módulo 2: Formulario
* **Propósito**: Captura de datos básicos de entrada por parte del usuario.
* **Componentes**:
  * Campos de entrada (`Entry`): Captura de "Nombre" y "Edad".
  * Botón "Guardar": Procesa o procesaría los datos ingresados en los campos de texto.
  * Botón "Cerrar": Destruye el objeto de la ventana actual.

---

### 3.4. Módulo 3: Lista (CRUD Básico)
* **Propósito**: Demostración de operaciones básicas de alta, baja y limpieza sobre una lista de elementos en memoria.
* **Componentes**:
  * Cuadro de lista (`Listbox`): Visualiza los elementos insertados.
  * Campo de texto (`Entry`): Entrada para ingresar nuevos datos.
  * Botón "Agregar": Inserta el texto digitado al `Listbox`.
  * Botón "Eliminar seleccionado": Remueve el elemento seleccionado del `Listbox`.
  * Botón "Limpiar": Vacía todos los registros de la lista.

---

### 3.5. Módulo 4: Tabla (Treeview)
* **Propósito**: Visualización estructurada de datos tabulares en columnas.
* **Componentes**:
  * Componente `ttk.Treeview`: Configurado con tres columnas primarias: **Nombre**, **Valor1** y **Valor2**.
  * Adecuado para conectar posteriormente con fuentes de datos relacionales (bases de datos SQL o archivos CSV/JSON).

---

### 3.6. Módulo 5: Canvas (Dibujo)
* **Propósito**: Demostración de gráficos 2D y renderizado vectorial básico dentro de Tkinter.
* **Componentes**:
  * Lienzo (`Canvas`): Espacio de dibujo vectorial con bordes definidos.
  * Figuras trazadas:
    * `create_rectangle(...)`: Rectángulo con borde negro.
    * `create_oval(...)`: Círculo/Óvalo con relleno azul claro (`fill`).
    * `create_line(...)`: Línea diagonal.
    * `create_text(...)`: Texto incrustado en el lienzo ("¡Hola Canvas!").

---

## 4. Recomendaciones para Evolución del Proyecto

1. **Separación de Responsabilidades (MVC)**:
   * Mover la lógica de eventos y estado (ej. la lista de elementos o datos de la tabla) fuera de la capa de vista a controladores o clases model de Python.
2. **Persistencia de Datos**:
   * Conectar los formularios y el módulo CRUD a una base de datos liviana como `SQLite` o a archivos JSON.
3. **Manejo de Excepciones**:
   * Agregar validaciones en la ventana de **Formulario** (ej. validar que la "Edad" sea un valor numérico entero positivo).
