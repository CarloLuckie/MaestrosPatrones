# Familia 1: Patrones Creacionales

Esta familia de patrones proporciona mecanismos de creación de objetos que incrementan la flexibilidad y la reutilización del código existente.

---

## 1. Singleton (Instancia Única)

**Categoría:** Creacional

**Propósito:**  
Garantiza que una clase tenga una única instancia en toda la aplicación y proporciona un punto de acceso global a ella.

**Estructura UML:**  
![Diagrama UML Singleton](./Imagenes/Creacionales/singleton.png)

**Lenguajes de referencia:**  
### Java
```Java 
public class Singleton {
    private static Singleton instance;
    public String value;

    private Singleton(String value) {
        this.value = value;
    }

    public static Singleton getInstance(String value) {
        if (instance == null) {
            instance = new Singleton(value);
        }
        return instance;
    }
}
```
### JavaScript
```JavaScript  
class Database {
  constructor() {
    if (Database.instance) {
      return Database.instance;
    }
    this.connection = "Conectado";
    Database.instance = this;
  }
}
```
---

## 2. Factory Method (Método Fábrica)

**Categoría:** Creacional

**Propósito:**  
Define una interfaz para crear un objeto, pero deja que las subclases decidan qué clase instanciar, delegando la creación a ellas.

**Estructura UML:**  
![Diagrama UML Factory Method](./Imagenes/Creacionales/factorymethod.jpg)

**Lenguajes de referencia:**  
### Java
```Java 
// Producto
interface Transporte {
    void entregar();
}

// Creador
abstract class Logistica {
    public abstract Transporte crearTransporte();
}

// Creador Concreto
class LogisticaMaritima extends Logistica {
    @Override
    public Transporte crearTransporte() {
        return new Barco();
    }
}
```
### JavaScript
```JavaScript  
class Carro {
    conducir() { return "Conduciendo un auto"; }
}

class Camion {
    conducir() { return "Manejando un camión"; }
}

class VehicleFactory {
    crearVehiculo(tipo) {
        if (tipo === "carro") return new Carro();
        if (tipo === "camion") return new Camion();
    }
}
```
---

## 3. Abstract Factory (Fábrica Abstracta)

**Categoría:** Creacional

**Propósito:**  
Permite crear familias de objetos relacionados o dependientes sin especificar sus clases concretas.

**Estructura UML:**  
*(Agregar imagen UML si aplica)*

**Lenguajes de referencia:**  
### Java
```Java 
// Interfaz de Fábrica
interface GUIFactory {
    Boton crearBoton();
    Checkbox crearCheckbox();
}

// Fábrica Concreta (Windows)
class WinFactory implements GUIFactory {
    public Boton crearBoton() { return new WinBoton(); }
    public Checkbox crearCheckbox() { return new WinCheckbox(); }
}
```
### JavaScript
```JavaScript  
// Fábrica de muebles modernos
const ModernFurnitureFactory = {
    createChair: () => new ModernChair(),
    createSofa: () => new ModernSofa()
};

// Fábrica de muebles victorianos
const VictorianFurnitureFactory = {
    createChair: () => new VictorianChair(),
    createSofa: () => new VictorianSofa()
};

// Cliente
function buildFurniture(factory) {
    const chair = factory.createChair();
    const sofa = factory.createSofa();
}
```
---

## 4. Builder (Constructor)

**Categoría:** Creacional

**Propósito:**  
Separa la construcción de un objeto complejo de su representación, permitiendo crear diferentes representaciones con el mismo proceso de construcción.

**Estructura UML:**  
*(Agregar imagen UML si aplica)*

**Lenguajes de referencia:**  
### Java
```Java 
public class Pizza {
    private String masa;
    private String salsa;
    
    // El Builder estático interno
    public static class Builder {
        private Pizza pizza;
        
        public Builder() { pizza = new Pizza(); }
        
        public Builder conMasa(String masa) {
            pizza.masa = masa;
            return this;
        }
        
        public Pizza build() { return pizza; }
    }
}

// Uso:
// Pizza p = new Pizza.Builder().conMasa("Fina").build();
```
### JavaScript
```JavaScript  
class UserBuilder {
    constructor(name) {
        this.user = { name: name };
    }

    setAge(age) {
        this.user.age = age;
        return this; // Retorna 'this' para encadenar métodos
    }

    setPhone(phone) {
        this.user.phone = phone;
        return this;
    }

    build() {
        return this.user;
    }
}

// Uso
const user = new UserBuilder("Carlos").setAge(25).build();
```
---

## 5. Prototype (Prototipo)

**Categoría:** Creacional

**Propósito:**  
Permite copiar objetos existentes sin que el código dependa de sus clases, delegando el proceso de clonación al propio objeto.

**Estructura UML:**  
*(Agregar imagen UML si aplica)*

**Lenguajes de referencia:**  
### Java
```Java 
abstract class Shape implements Cloneable {
    public int x, y;
    
    public Shape clone() {
        try {
            return (Shape) super.clone();
        } catch (CloneNotSupportedException e) {
            return null;
        }
    }
}

// Uso
// Shape circuloCopia = circuloOriginal.clone();
```
### JavaScript
```JavaScript  
const zombieOriginal = {
    comer: function() { console.log("Cerebros..."); },
    salud: 100
};

// Crear nuevo objeto usando 'zombieOriginal' como prototipo
const zombieCopia = Object.create(zombieOriginal);
zombieCopia.salud = 50; // Modificamos solo la copia

console.log(zombieOriginal.salud); // 100
console.log(zombieCopia.salud);    // 50
```