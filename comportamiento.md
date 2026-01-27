
PATRÓN 1
Nombre: Chain of Responsibility
Categoría: Comportamiento
Propósito: Permite pasar una solicitud a través de una cadena de objetos manejadores hasta que uno de ellos la procesa, evitando el acoplamiento directo entre el emisor y el receptor.
Código de referencia (Python):
class Handler:
    def __init__(self, next_handler=None):
        self.next = next_handler

    def handle(self, request):
        if self.next:
            return self.next.handle(request)

class LowHandler(Handler):
    def handle(self, request):
        if request <= 10:
            return "Handled by LowHandler"
        return super().handle(request)

class HighHandler(Handler):
    def handle(self, request):
        if request > 10:
            return "Handled by HighHandler"

chain = LowHandler(HighHandler())
print(chain.handle(15))
Código de referencia (Java):
abstract class Handler {
    protected Handler next;
    public void setNext(Handler next) { this.next = next; }
    public abstract void handle(int request);
}

class LowHandler extends Handler {
    public void handle(int request) {
        if (request <= 10) System.out.println("LowHandler");
        else if (next != null) next.handle(request);
    }
}

PATRÓN 2
Nombre: Command
Categoría: Comportamiento
Propósito: Encapsula una petición como un objeto, permitiendo parametrizar clientes con diferentes solicitudes, colas o registros de acciones.
Código de referencia (Python):
class Light:
    def on(self):
        print("Luz encendida")

class Command:
    def execute(self): pass

class LightOn(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.on()

LightOn(Light()).execute()
Código de referencia (Java):
interface Command {
    void execute();
}

class Light {
    void on() {
        System.out.println("Luz encendida");
    }
}

class LightOn implements Command {
    Light light;
    LightOn(Light light) { this.light = light; }
    public void execute() {
        light.on();
    }
}
PATRÓN 3
Nombre: Interpreter
Categoría: Comportamiento
Propósito: Define una representación para la gramática de un lenguaje y un intérprete que usa esa representación para interpretar expresiones.
Código de referencia (Python):
class Number:
    def __init__(self, value):
        self.value = value
    def interpret(self):
        return self.value

print(Number(5).interpret())
Código de referencia (Java):
interface Expression {
    int interpret();
}

class Number implements Expression {
    int value;
    Number(int value) { this.value = value; }
    public int interpret() { return value; }
}

PATRÓN 4
Nombre: Iterator
Categoría: Comportamiento
Propósito: Proporciona una forma de acceder secuencialmente a los elementos de una colección sin exponer su estructura interna.
Código de referencia (Python):
items = [1, 2, 3]
for item in items:
    print(item)
Código de referencia (Java):
List<Integer> items = List.of(1, 2, 3);
Iterator<Integer> it = items.iterator();
while(it.hasNext()) {
    System.out.println(it.next());
}

PATRÓN 5
Nombre: Mediator
Categoría: Comportamiento
Propósito: Define un objeto que centraliza la comunicación entre varios objetos, reduciendo las dependencias directas entre ellos.
Código de referencia (Python):
class Mediator:
    def send(self, msg):
        print("Mensaje:", msg)

class User:
    def __init__(self, mediator):
        self.mediator = mediator
    def send(self, msg):
        self.mediator.send(msg)

User(Mediator()).send("Hola")
Código de referencia (Java):
interface Mediator {
    void send(String msg);
}

class Chat implements Mediator {
    public void send(String msg) {
        System.out.println("Mensaje: " + msg);
    }
}

PATRÓN 6
Nombre: Memento
Categoría: Comportamiento
Propósito: Permite capturar y restaurar el estado interno de un objeto sin violar el principio de encapsulación.
Código de referencia (Python):
class Memento:
    def __init__(self, state):
        self.state = state

text = "Hola"
saved = Memento(text)
text = saved.state
Código de referencia (Java):
class Memento {
    String state;
    Memento(String state) { this.state = state; }
    String getState() { return state; }
}

PATRÓN 7
Nombre: Observer
Categoría: Comportamiento
Propósito: Define una dependencia de uno a muchos entre objetos, de modo que cuando uno cambia su estado, todos los dependientes son notificados automáticamente.
Código de referencia (Python):
class Observer:
    def update(self):
        print("Notificado")

class Subject:
    def __init__(self):
        self.observers = []
    def add(self, o):
        self.observers.append(o)
    def notify(self):
        for o in self.observers:
            o.update()

s = Subject()
s.add(Observer())
s.notify()
Código de referencia (Java):
interface Observer {
    void update();
}

class Subject {
    List<Observer> observers = new ArrayList<>();
    void add(Observer o) { observers.add(o); }
    void notifyAllObservers() {
        for(Observer o : observers) o.update();
    }
}

PATRÓN 8
Nombre: State
Categoría: Comportamiento
Propósito: Permite que un objeto altere su comportamiento cuando cambia su estado interno, aparentando cambiar de clase.
Código de referencia (Python):
class Green:
    def action(self):
        print("Avanzar")

state = Green()
state.action()
Código de referencia (Java):
interface State {
    void action();
}

class Green implements State {
    public void action() {
        System.out.println("Avanzar");
    }
}

PATRÓN 9
Nombre: Strategy
Categoría: Comportamiento
Propósito: Define una familia de algoritmos, los encapsula y los hace intercambiables en tiempo de ejecución.
Código de referencia (Python):
class Add:
    def execute(self, a, b):
        return a + b

print(Add().execute(2,3))
Código de referencia (Java):
interface Strategy {
    int execute(int a, int b);
}

class Add implements Strategy {
    public int execute(int a, int b) {
        return a + b;
    }
}

PATRÓN 10
Nombre: Template Method
Categoría: Comportamiento
Propósito: Define el esqueleto de un algoritmo en una operación, delegando algunos pasos a subclases.
Código de referencia (Python):
class Process:
    def run(self):
        self.step()

    def step(self):
        print("Paso")

Process().run()
Código de referencia (Java):
abstract class Process {
    final void run() {
        step();
    }
    abstract void step();
}

PATRÓN 11
Nombre: Visitor
Categoría: Comportamiento
Propósito: Permite definir nuevas operaciones sobre una estructura de objetos sin modificar las clases de los elementos sobre los que opera.
Código de referencia (Python):
class Visitor:
    def visit(self):
        print("Visitando")

Visitor().visit()
Código de referencia (Java):
interface Visitor {
    void visit();
}

class PrintVisitor implements Visitor {
    public void visit() {
        System.out.println("Visitando");
    }
}

