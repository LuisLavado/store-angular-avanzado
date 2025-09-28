# Formateo de Código con Prettier y ESLint en Proyectos Angular

La estandarización del código es un pilar fundamental en el desarrollo de software profesional. Cuando trabajamos en equipos, las diferencias en estilos de escritura pueden generar problemas de legibilidad y mantenimiento. En este artículo, exploraremos cómo implementar Prettier en un proyecto Angular para garantizar un formato de código consistente, complementando las capacidades de análisis de ESLint.

## ¿Cuál es la diferencia entre ESLint y Prettier?

Antes de sumergirnos en la implementación, es importante entender la distinción entre estas dos herramientas fundamentales:

- **ESLint**: Se enfoca en analizar la calidad del código, identificando malas prácticas y problemas de accesibilidad. No está diseñado principalmente para formatear código.

- **Prettier**: Es un formateador de código que establece un estilo consistente en todo el proyecto. Su objetivo es que todos los desarrolladores escriban código con el mismo formato, independientemente de sus preferencias personales.

La documentación oficial de ESLint reconoce esta diferencia y recomienda usar Prettier como complemento para el formateo de código. Esta combinación nos permite mantener tanto la calidad como la consistencia en nuestros proyectos.

### ¿Por qué necesitamos un formateador de código?

La estandarización del formato ofrece múltiples beneficios:

- Mejora la legibilidad: Un código con formato consistente es más fácil de leer para todos los miembros del equipo.
- Facilita las revisiones de código: Los revisores pueden centrarse en la lógica y no en detalles de formato.
- Evita commits innecesarios: Elimina cambios en el control de versiones que solo modifican el formato.
- Reduce debates improductivos: Elimina discusiones sobre preferencias de estilo que no aportan valor al proyecto.

## ¿Cómo instalar y configurar Prettier en un proyecto Angular?

La instalación de Prettier es sencilla y puede integrarse perfectamente con tu flujo de trabajo existente. Sigue estos pasos:

**Instalación básica**

```
npm install prettier -D
```

El flag `-D` (o `--save-dev`) indica que Prettier es una dependencia de desarrollo, ya que no es necesaria en el entorno de producción.

**Configuración en package.json**  
Una vez instalado, es recomendable crear un comando npm para ejecutarlo fácilmente:

```
"scripts": {
  "format": "prettier --write ."
}
```

Este comando permite formatear todo el proyecto con un simple npm run format. La opción `--write` indica a Prettier que corrija automáticamente los problemas de formato en lugar de solo reportarlos.

**Nota**: Puedes limitar el alcance del formateo a directorios específicos, como src, si no deseas aplicarlo a archivos de configuración:

```
"format": "prettier --write src"
```

### Creación de un archivo de configuración

Para personalizar el comportamiento de Prettier según las preferencias de tu equipo, puedes crear un archivo `.prettierrc.json` en la raíz del proyecto:

```
{
  "tabWidth": 2,
  "useTabs": false,
  "singleQuote": true,
  "semi": true,
  "bracketSpacing": true,
  "arrowParens": "avoid",
  "trailingComma": "es5",
  "bracketSameLine": true,
  "printWidth": 80,
}
```

Algunas opciones comunes incluyen:

- **tabWidth**: Define el número de espacios por nivel de indentación (2 es el estándar en JavaScript/HTML).
- **useTabs**: Determina si se usan tabulaciones en lugar de espacios.
- **singleQuote**: Establece si se prefieren comillas simples sobre dobles.
- **semi**: Controla si se añaden puntos y coma al final de las declaraciones.

## ¿Cómo integrar Prettier con ESLint?

Para que ESLint y Prettier trabajen en armonía, es necesario instalar algunos paquetes adicionales:

```
npm install prettier-eslint eslint-config-prettier eslint-plugin-prettier -D
```

Estos paquetes evitan conflictos entre las reglas de ESLint y el formateo de Prettier.

### Configuración en el archivo ESLint

Para completar la integración, modifica tu archivo `.eslintrc.js` añadiendo:

```
module.exports = {
  // Configuración existente...
  extends: [
    // Otras extensiones...
    'plugin:prettier/recommended'
  ],
  // Para archivos TypeScript
  overrides: [
    {
      files: ['*.ts'],
      extends: [
        // Otras extensiones...
        'plugin:prettier/recommended'
      ]
    },
    // Para archivos HTML
    {
      files: ['*.html'],
      extends: [
        // Otras extensiones...
        'plugin:prettier/recommended'
      ]
    }
  ]
}
```

Esta configuración asegura que ESLint respete el formateo de Prettier y que ambas herramientas funcionen correctamente juntas.

### Beneficios de la integración

Con esta configuración:

- ESLint mostrará errores de formato: Los problemas de formato aparecerán como advertencias o errores en tu editor.
- Evitarás reglas contradictorias: Las reglas de ESLint que entren en conflicto con Prettier serán desactivadas automáticamente.
- Mantendrás un flujo de trabajo coherente: Ambas herramientas trabajarán juntas sin problemas.

## ¿Qué mejoras aporta Prettier a nuestro código?

Después de ejecutar Prettier, notarás varias mejoras en la estructura de tu código:

### En archivos HTML

Prettier organiza los atributos de las etiquetas HTML para mejorar la legibilidad:

```
<!-- Antes -->
<img src="assets/logo.png" alt="Logo" class="header-logo" width="100" height="50">

<!-- Después -->
<img
  src="assets/logo.png"
  alt="Logo"
  class="header-logo"
  width="100"
  height="50"
>
```

Esta disposición vertical facilita la lectura cuando hay múltiples atributos.

### En archivos TypeScript/JavaScript

Prettier estandariza la indentación, espaciado y uso de comillas:

```
// Antes (inconsistente)
function calculateTotal(items){
    return items.reduce((total,item)=>{
  return total+item.price;
},0);
}

// Después (formateado)
function calculateTotal(items) {
  return items.reduce((total, item) => {
    return total + item.price;
  }, 0);
}
```

### Compatibilidad con Angular

Prettier soporta la nueva sintaxis de Angular, asegurando que incluso las características más recientes del framework se formateen correctamente.

La implementación de Prettier en tu proyecto Angular es una inversión que pagará dividendos en términos de productividad y calidad de código. Al establecer un estándar de formato consistente, tu equipo puede centrarse en lo que realmente importa: desarrollar funcionalidades valiosas para tus usuarios.
