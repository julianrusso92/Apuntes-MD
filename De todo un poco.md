# De todo un poco

## Obtener certificado HTTPS gratis

- https://ardalis.com/add-https-to-any-site-for-free

## Code metrics values (Net)

- https://docs.microsoft.com/en-us/visualstudio/code-quality/code-metrics-values?view=vs-2019

## Smart Enum

- https://github.com/ardalis/SmartEnum

## When to use an abstract class vs. interface

- The short answer: An abstract class allows you to create functionality that subclasses can implement or override. An interface only allows you to define functionality, not implement it. And whereas a class can extend only one abstract class, it can take advantage of multiple interfaces.

## Constructor estático

- Se ejecuta solamente una vez, para todas las instancias.

## Constructores y Herencia

Para los ejemplos considerar clase padre mamifero y clases hijas caballo, humano, gorila 

- Si no ponemos constructor a una clase, por defecto utiliza el constructor por defecto 
  - Ej: mamifero () {} y si caballo hereda de mamifero, implementara :base()
- Pero si mamifero tiene un constructor Mamifero(string nombre) {_nombre = nombre}
  - En la clase hija, debemos implementar en constructor base pasandole el parametro.
  - caballo(string nombreCaballo) : base(nombreCaballo)

## Logs

### Serilog

