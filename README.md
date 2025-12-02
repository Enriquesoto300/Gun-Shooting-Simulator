from abc import ABC, abstractmethod

# --- 1. CLASE BASE (ABSTRACCIÓN Y ENCAPSULAMIENTO) ---
class Weapon(ABC):
    def __init__(self, name, ammo, damage):
        self.__name = name      # Privado: Solo accesible dentro de esta clase
        self.__ammo = ammo      # Privado: Protege la cantidad de balas
        self._damage = damage   # Protegido: Accesible por las clases hijas

    @property
    def name(self):             # Getter: Permite leer el nombre sin modificarlo
        return self.__name

    def reload(self, amount):   # Método compartido por todas las armas
        self.__ammo += amount
        print(f"🔄 {self.__name} recargada. Balas: {self.__ammo}")

    def _use_ammo(self):        # Helper interno para gestionar munición
        if self.__ammo > 0:
            self.__ammo -= 1
            return True
        print(f"❌ {self.__name} hizo click (Sin munición)")
        return False

    @abstractmethod             # Obliga a las hijas a tener su propia versión de 'shoot'
    def shoot(self):
        pass

# --- 2. SUBCLASES (HERENCIA Y POLIMORFISMO) ---
class Rifle(Weapon):
    def shoot(self):            # Implementación única para Rifle
        if self._use_ammo():
            print(f"💥 {self.name} dispara una ráfaga precisa. Daño: {self._damage}")

class Shotgun(Weapon):
    def shoot(self):            # Implementación única para Escopeta
        if self._use_ammo():
            print(f"💥 {self.name} dispara perdigones dispersos. Daño masivo: {self._damage * 3}")

# --- 3. CLASE GESTORA (COMPOSICIÓN) ---
class ShootingRange:
    def __init__(self):
        self.weapons = []       # Composición: El campo de tiro "tiene" armas

    def add_weapon(self, weapon):
        self.weapons.append(weapon)

    def start(self):
        print("\n--- INICIO DE SIMULACIÓN ---")
        for weapon in self.weapons:  # Itera sin importar qué tipo de arma sea
            weapon.shoot()           # Polimorfismo: Cada arma sabe cómo disparar
            weapon.reload(5)
            weapon.shoot()
            print("---")

# --- EJECUCIÓN ---
if __name__ == "__main__":
    # Creamos las armas
    ak47 = Rifle("AK-47", 0, 30)
    mossberg = Shotgun("Mossberg 500", 0, 50)

    # Configuramos el simulador
    sim = ShootingRange()
    sim.add_weapon(ak47)
    sim.add_weapon(mossberg)

    # Corremos el programa
    sim.start()
