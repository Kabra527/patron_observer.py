# patron_observer.py
"""Actividad 3 Patrones de diseño""" 
"""
Este módulo implementa el patrón de diseño Observer en Python.

Clases:
- Subject: Mantiene una lista de observadores y los notifica de cambios.
- Observer: Interfaz base para los observadores.
- ConcreteObserver: Implementación concreta del observador.

Ejemplo de uso:
    subject = Subject()
    observer = ConcreteObserver("Observador 1")
    subject.attach(observer)
    subject.notify("Mensaje de prueba")
"""

from abc import ABC, abstractmethod

class Subject:
    """Clase que representa un sujeto observado por múltiples observadores."""
    
    def __init__(self):
        """Inicializa la lista de observadores."""
        self._observers = set()  # Usamos un conjunto para evitar duplicados

    def attach(self, observer):
        """Agrega un observador a la lista."""
        self._observers.add(observer)

    def detach(self, observer):
        """Elimina un observador de la lista si existe."""
        self._observers.discard(observer)

    def notify(self, message):
        """Notifica a todos los observadores sobre un cambio."""
        for observer in self._observers:
            observer.update(message)

class Observer(ABC):
    """Interfaz base para los observadores."""
    
    @abstractmethod
    def update(self, message):
        """Método abstracto que se implementará en las subclases."""
        
class ConcreteObserver(Observer):
    """Implementación concreta del observador."""
    
    def __init__(self, name):
        """Inicializa el observador con un nombre."""
        self.name = name

    def update(self, message):
        """Recibe la notificación del sujeto y la imprime."""
        print(f"{self.name} recibió el mensaje: {message}")

if __name__ == "__main__":
    subject = Subject()
    observer1 = ConcreteObserver("Observador 1")
    observer2 = ConcreteObserver("Observador 2")

    subject.attach(observer1)
    subject.attach(observer2)
    subject.attach(observer1)  # Ya no hay duplicados gracias al conjunto

    print("Enviando primera notificación:")
    subject.notify("Cambio en el estado del sujeto")

    subject.detach(observer1)
    
    print("\nEnviando segunda notificación:")
    subject.notify("Otro cambio en el estado del sujeto")
