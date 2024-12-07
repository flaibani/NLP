instalar librerias

Se utiliza Selenium porque no fue posible el scrapping con Beautifulsoup por ser páginas dinámicas

descargar chromedrive

El atributo ng-href es común en aplicaciones basadas en AngularJS. Puedes usar su valor para construir selectores generales:
a.ng-binding[ng-href*="/boardgamedesigner/"]
a.ng-binding[ng-href*="/boardgame/"]
a.ng-binding[ng-href*="/boardgameartist/"]
a.ng-binding[ng-href*="/boardgamepublisher/"]

El selector `document.querySelector('a.ng-binding[ng-href*="/boardgamedesigner/"]')` funciona porque está dirigido específicamente a enlaces (`<a>`) con:

1. La clase `ng-binding`.
2. Un atributo `ng-href` que contiene la cadena `/boardgamedesigner/`.

Vamos a desglosar cómo puedes usar este enfoque de forma general para consultar cualquier dato en un sitio web.

---

### **1. Análisis del Enfoque General**

Cuando estás trabajando con Selenium (o inspeccionando un sitio web), necesitas:
- **Identificar un patrón único en el HTML** para el tipo de datos que buscas.
- **Construir un selector** que apunte a los elementos que contienen esos datos.
- **Aplicar el selector** para extraer la información relevante.

---

### **2. Patrón Común: `ng-href`**
El atributo `ng-href` es común en aplicaciones basadas en AngularJS. Puedes usar su valor para construir selectores generales. Por ejemplo:

#### Para Diseñadores:
```css
a.ng-binding[ng-href*="/boardgamedesigner/"]
```

#### Para Juegos:
```css
a.ng-binding[ng-href*="/boardgame/"]
```

#### Para Artistas:
```css
a.ng-binding[ng-href*="/boardgameartist/"]
```

#### Para Editores:
```css
a.ng-binding[ng-href*="/boardgamepublisher/"]
```

---

### **3. Implementación General en Selenium**

Podemos escribir una función general que tome como entrada:
- **Un patrón (`issue`)**: por ejemplo, `"boardgamedesigner"`, `"boardgameartist"`, etc.
- **El driver de Selenium**.

La función buscará los datos relacionados.

#### Código General:
```python
from selenium.webdriver.common.by import By

def get_data_by_issue(driver, issue):
    # Construir el selector dinámicamente según el patrón (issue)
    selector = f'a.ng-binding[ng-href*="/{issue}/"]'
    
    # Encontrar todos los elementos que coincidan con el selector
    elements = driver.find_elements(By.CSS_SELECTOR, selector)
    
    # Extraer y retornar los textos de los elementos
    data = [element.text.strip() for element in elements]
    return data

# Ejemplo de uso:
# Consultar diseñadores
designers = get_data_by_issue(driver, "boardgamedesigner")
print("Designers:", designers)

# Consultar artistas
artists = get_data_by_issue(driver, "boardgameartist")
print("Artists:", artists)

# Consultar editores
publishers = get_data_by_issue(driver, "boardgamepublisher")
print("Publishers:", publishers)
```

---

### **4. Paso a Paso para Usar `get_data_by_issue`**
1. **Entender el Patrón (`issue`)**:
   - Analiza el HTML y encuentra el valor único en el atributo `ng-href` relacionado con los datos que necesitas.
   - Por ejemplo:
     - Diseñadores: `"boardgamedesigner"`.
     - Artistas: `"boardgameartist"`.
     - Juegos: `"boardgame"`.

2. **Llamar a la Función**:
   - Usa la función `get_data_by_issue` para cada tipo de dato que necesites.
   - La función construye el selector dinámicamente con el patrón proporcionado.

3. **Recibir los Resultados**:
   - La función retorna una lista con los textos extraídos de los elementos que coinciden con el patrón.

---

### **5. Ejemplo de Resultados**
Supongamos que ejecutamos el código para los diseñadores y artistas:

#### Input:
```python
designers = get_data_by_issue(driver, "boardgamedesigner")
artists = get_data_by_issue(driver, "boardgameartist")
print("Designers:", designers)
print("Artists:", artists)
```

#### Output:
```
Designers: ['Inka Brand', 'Markus Brand']
Artists: ['Dennis Lohausen']
```

---

### **6. ¿Qué Pasa si el Dato No Existe?**
Si el patrón (`issue`) no coincide con ningún elemento:
- Selenium retorna una lista vacía (`[]`).
- Puedes manejar esto así:
```python
if not data:
    print(f"No data found for issue: {issue}")
else:
    print(f"{issue.capitalize()}s: {data}")
```

---

### **7. Ventajas de Este Enfoque**
- **Reutilizable**: Funciona para cualquier tipo de dato con un patrón claro.
- **Escalable**: Solo necesitas cambiar el valor del patrón (`issue`) para buscar datos distintos.
- **Flexible**: Si el sitio cambia su estructura, solo debes actualizar los selectores.

---

### **Conclusión**
Este método generaliza la búsqueda de datos dinámicos usando patrones predecibles en el HTML. Ahora puedes usar el mismo enfoque para cualquier tipo de información en el sitio que siga un formato similar.