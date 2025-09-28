# Configuración de ESLint y Prettier en proyectos Angular

La implementación de buenas prácticas de código es fundamental para cualquier equipo de desarrollo que busque mantener un proyecto escalable y de alta calidad. En el ecosistema de Angular, existen herramientas específicas que nos ayudan a automatizar la detección y corrección de problemas comunes, permitiéndonos enfocarnos en lo que realmente importa: crear funcionalidades valiosas para nuestros usuarios.

## ¿Por qué son importantes las convenciones de código en Angular?

Uno de los mayores desafíos en equipos de desarrollo es lograr que todos los miembros sigan las mismas convenciones de código. Discusiones sobre si usar comillas simples o dobles, tabs versus espacios, y otras cuestiones similares pueden consumir tiempo valioso que podría invertirse en mejorar la aplicación.

Para solucionar este problema, existen dos tipos principales de herramientas:

- **Linters**: Aseguran que se sigan buenas prácticas de código y seguridad de forma automática, previniendo errores fáciles de detectar antes de que lleguen a la fase de revisión de código.
- **Formateadores**: Garantizan que todo el código tenga la misma estructura y sea fácil de leer, independientemente de quién lo haya escrito.
  En proyectos de JavaScript o TypeScript, las herramientas más utilizadas son ESLint y Prettier, que pueden configurarse específicamente para proyectos Angular.

## ¿Cómo aprovechar las migraciones automáticas de Angular?

Angular incluye herramientas de migración que ayudan a mantener buenas prácticas de código. Una de las más útiles es la migración **["clean out unused imports"](https://v19.angular.dev/reference/migrations/cleanup-unused-imports)**.

### Limpieza automática de importaciones no utilizadas

Para utilizar esta funcionalidad:

Detén el servidor de desarrollo si está en ejecución
Ejecuta el siguiente comando:

```
ng generate @angular/core:clean-up-unused-imports
```

Este comando analiza automáticamente tu código y elimina las importaciones de componentes, directivas o pipes que no estén siendo utilizados en tus templates. Por ejemplo, si has importado `HeaderComponent` pero no lo utilizas en tu HTML, Angular lo detectará y eliminará esa importación.

**Beneficios:**

- Reduce el tamaño final de la aplicación
- Mantiene el código limpio y legible
- Previene posibles confusiones sobre qué componentes están realmente en uso

## ¿Cómo implementar ESLint en un proyecto Angular?

Angular proporciona una guía de estilo oficial (Angular Core Style Guide) que establece convenciones para nombrar componentes, aplicar el principio de responsabilidad única y otras buenas prácticas. Sin embargo, confiar solo en documentación no garantiza que todos los desarrolladores sigan estas reglas.

### Instalación y configuración de ESLint

Para automatizar la verificación de estas buenas prácticas:

1. Ejecuta el siguiente comando:

```
ng add @angular-eslint/schematics
```

Este comando instalará ESLint configurado específicamente para Angular, creando archivos como `.eslintrc.js` y actualizando `package.json` y `angular.json`.

Una vez instalado, puedes ejecutar:

```
ng lint
```

Este comando mostrará todos los errores y advertencias en tu código, clasificados por gravedad. Algunos problemas comunes que detectará incluyen:

- Problemas de accesibilidad
- Importaciones no utilizadas
- Constructores vacíos innecesarios
- Convenciones de nomenclatura incorrectas

### Corrección automática de problemas
Para solucionar automáticamente los problemas que puedan ser corregidos sin intervención manual:

```
ng lint --fix
```

Este comando corregirá automáticamente las advertencias, aunque los errores más graves generalmente requerirán que los soluciones manualmente.

## ¿Cómo solucionar problemas específicos detectados por ESLint?

### Problemas en archivos TypeScript 
Algunos problemas comunes incluyen:

1. __Importaciones no utilizadas__: Simplemente elimina las importaciones que no estén siendo utilizadas en tu código.

2. __Constructores vacíos__: Si tienes un constructor que no hace nada, puedes eliminarlo completamente.

3. __Convenciones de nomenclatura__: Por ejemplo, las directivas personalizadas deberían tener un prefijo como "app" para evitar colisiones con otras bibliotecas.

### Problemas de accesibilidad en HTML
ESLint también puede detectar problemas en tus templates HTML, especialmente relacionados con accesibilidad:

1. __Imágenes sin atributos de accesibilidad__: Para imágenes que funcionan como botones, debes agregar atributos como:
```
<img [src]="product.image" (click)="onSelect()" tabindex="0" role="button" (keydown.enter)="onSelect()">
```

### Estos atributos permiten:
- tabindex="0": Hacer focus en el elemento
- role="button": Indicar a los lectores de pantalla que es un elemento clickeable
- (keydown.enter)="onSelect()": Permitir la navegación por teclado

### Beneficios de mejorar la accesibilidad:

- Mejor experiencia para usuarios con discapacidades visuales
- Cumplimiento de estándares web
- Mejor SEO y compatibilidad con diferentes dispositivos

Para visualizar mejor estos errores en tu editor, asegúrate de instalar la extensión de ESLint para tu IDE, que marcará los problemas directamente en el código mientras trabajas.

La implementación de estas herramientas no solo mejora la calidad de tu código, sino que también aumenta la productividad del equipo al automatizar tareas repetitivas de revisión.
