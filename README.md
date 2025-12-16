# Grupo11_Cerrojo

# Manual de Desarrollo: Proyecto Cerrojo (Grupo 11)

Este documento sirve como **guía paso a paso** para que todos los integrantes del grupo trabajen de forma coordinada, evitando conflictos en el código y manteniendo el repositorio limpio.

---

0.  **PROTOCOLO ANTI-BORRADO (STM32CubeIDE) - ¡LEER O MORIR! 💀**
Mucho cuidado cuando cambiéis un pin o la configuración del reloj en el archivo de diseño (`.ioc`). Al darle al botón de generar código (el engranaje ⚙️), el programa **BORRA Y REESCRIBE** archivos enteros.

* **EL PELIGRO:** El archivo `main.c` es propiedad de STM32. Si escribes tu código suelto por ahí, al regenerar los pines, el programa pensará que es suciedad y **LO BORRARÁ** sin piedad. Adios trabajo.

* **LA SOLUCIÓN (Los Búnkeres):**
 El código es educado y respeta unas "Zonas Seguras". Tienes que escribir **EXCLUSIVAMENTE** entre las líneas de comentarios que dicen `USER CODE BEGIN` y `USER CODE END`.
        
        * **ASÍ SÍ (Se guarda para siempre):**
            ```c
            /* USER CODE BEGIN 2 */
               // Tu código aquí está blindado 🛡️
               juego_iniciar();
            /* USER CODE END 2 */
            ```
            
        * **ASÍ NO (Se borrará al actualizar pines):**
            ```c
            int main(void) {
               HAL_Init();
               // Mi código aquí suelto... ¡PELIGRO! ☠️
            ```

    * **TRUCO PRO:** Si creáis vuestros propios archivos (ej: `juego.c` y `juego.h`), esos **NUNCA** se tocan. Es el territorio más seguro.
>>>>>>> 5da854bc11ef9ee3a7d296229ac67b98cd5486a9

---

## 1. Configuración Inicial (Solo la primera vez)

Antes de empezar a trabajar, es necesario configurar Git para que sepa quién está realizando los cambios.

1.  Abre el terminal **Git Bash**, no el terminal de Windows.
2.  Ejecuta los siguientes comandos (sustituyendo los datos por los tuyos):

```bash
# Configura tu nombre de usuario (aparecerá en el historial)
git config --global user.name "gbfaz2"

# Configura tu email (debe ser el mismo que usas en GitHub)
git config --global user.email "tu_email@ejemplo.com"
```

---

## 2. Descargar el Proyecto (Clonar)

Para descargar el proyecto en el Escritorio y no perderlo por el ordenador:

1.  Abre el terminal **Git Bash**.

2.  Escribe este comando para moverte al Escritorio:
    ```bash
    cd Desktop
    ```
    **NOTA:** Si te da error, prueba con `cd OneDrive/Desktop` o `cd OneDrive/Escritorio`, depende de tu Windows.

    **NOTA:** A mi no me funcionaba, así que lo metí en una carpeta creada, simplemente arrastra la carpeta al git bash y te escribirá la ruta de la carpeta en donde quieres que se te clone el repo

3.  Descarga el proyecto aquí dentro:
    ```bash
    git clone https://github.com/gbfaz2/Grupo11_GeneradorDeColores
    ```
    *(No cambiar el user, solo copiar y pegar esa línea, pues es la ruta del repo)*


4.  Entra en la carpeta del proyecto que se acaba de crear:
    ```bash
    cd Grupo11_GeneradorDeColores
    ```


> **NOTA:** Ahora tendrás en tu Escritorio (o dentro de la carpeta) proyecto github. ¡No la borres!


> **NOTA IMPORTANTE SOBRE VIVADO:** Es normal que al descargar el proyecto falten carpetas como `.cache`, `.hw` o `.sim`. Estas carpetas son archivos temporales de Vivado que **NO** deben subirse a GitHub. Vivado las regenerará automáticamente al abrir el archivo `.xpr`.

---

## 3. Sistema de Ramas (Branches)

Para evitar sobrescribir el trabajo de los compañeros, **nunca trabajaremos directamente sobre la rama `main`**. Cada integrante debe crear su propia "rama" (su espacio de trabajo personal).

### Crear tu rama personal:
En el terminal Git Bash, dentro de la carpeta del proyecto github:

```bash
# Crea una rama nueva con tu nombre y te cambia a ella automáticamente
# La bandera '-b' significa "crear rama nueva"
git checkout -b rama-nombre
```
*(Ejemplo: `git checkout -b rama-tudor`)*

Verifica que estás en tu rama si al final de la línea de comandos aparece el nombre entre paréntesis, por ejemplo: `(rama-tudor)`.

---

## 4. Flujo de Trabajo Diario (Rutina)

Cada vez que trabajes en el proyecto (añadir un módulo, modificar código, corregir errores), sigue estos pasos **estrictamente**:

### Paso A: Trabajar en Vivado
1.  Abre el proyecto en Vivado.
2.  Edita tus archivos VHDL (`.vhd`) o crea los nuevos en la carpeta `src`.
3.  **Guarda todo** en Vivado (File -> Save All) antes de ir al terminal.

### Paso B: Subir los cambios a GitHub
Vuelve al terminal **Git Bash** y ejecuta estos 3 comandos en orden:

1.  **Añadir cambios al paquete:**
    Este comando prepara todos los archivos modificados para ser guardados.
    ```bash
    git add .
    ```

2.  **Confirmar los cambios (Commit):**
    Crea un punto de guardado en el historial. Es obligatorio poner un mensaje explicando qué has hecho.
    ```bash
    git commit -m "Explicación breve de los cambios realizados hoy"
    ```

3.  **Enviar a la nube (Push):**
    Sube los cambios a tu rama en GitHub.
    * **Si es la PRIMERA VEZ que subes esta rama:**
        ```bash
        git push -u origin nombre-de-tu-rama
        ```
    * **Para todas las veces siguientes:**
        ```bash
        git push
        ```

---

## 5. Integrar cambios (Merge / Pull Request)

Cuando hayas terminado tu parte y funcione correctamente, es hora de juntarla con el proyecto principal (`main`).

1.  Entra en la página web del repositorio en GitHub.
2.  Verás un aviso amarillo indicando que tu rama tiene cambios recientes. Haz clic en el botón verde **"Compare & pull request"**.
3.  Escribe un título y descripción de lo que has añadido.
4.  Haz clic en **"Create pull request"**.
5.  Avisa a los compañeros para que revisen el código y acepten la fusión (botón **"Merge pull request"**).

---

## 6. Actualizar tu proyecto (Descargar lo de los demás)

Si un compañero ha subido cambios al `main` (por ejemplo, el TOP actualizado) y necesitas tenerlos en tu ordenador:

1.  Cámbiate a la rama principal:
    ```bash
    git checkout main
    ```
2.  Descarga la última versión:
    ```bash
    git pull origin main
    ```
3.  (Opcional) Si quieres llevar esos cambios a tu rama personal para seguir trabajando:
    ```bash
    git checkout nombre-de-tu-rama
    git merge main
    ```

---

## 7. Reglas de Oro (NO IGNORAR)

1.  **El archivo `.gitignore` es intocable:** Este archivo evita que subamos basura al servidor. No lo borres ni le cambies el nombre.
2.  **Conflictos:** Si al subir cambios Git te avisa de un "CONFLICT", **no borres nada**. Significa que dos personas han tocado la misma línea de código. Avisad al grupo para resolverlo juntos.
<<<<<<< HEAD
3.  **Orden:** Los archivos fuente (`.vhd`) deben estar siempre dentro de la carpeta `src` (o `sources_1/new`). No creéis archivos sueltos en la raíz del proyecto.
=======
3.  **Orden:** Los archivos fuente (`.vhd`) deben estar siempre dentro de la carpeta `src` (o `sources_1/new`). No creéis archivos sueltos en la raíz del proyecto.
>>>>>>> 5da854bc11ef9ee3a7d296229ac67b98cd5486a9
