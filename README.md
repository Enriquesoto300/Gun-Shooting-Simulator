from abc import ABC, abstractmethod

# ---------------------------------------------------------
# 1. ABSTRACCIÓN & ENCAPSULAMIENTO
# ---------------------------------------------------------

class Weapon(ABC): # ABC convierte esta clase en Abstracta (no se puede crear directamente)
    def __init__(self, name, ammo, damage):
        self.__name = name      # Privado (__): Solo accesible dentro de esta clase
        self.__ammo = ammo      # Privado (__): Protege el estado interno
        self._damage = damage   # Protegido (_): Accesible por clases hijas

    # Getter: Permite leer el atributo privado de forma segura
    @property
    def name(self):
        return self.__name

    # Método común: Todas las armas comparten esta lógica (Herencia de comportamiento)
    def reload(self, amount):
        self.__ammo += amount
        print(f"🔄 {self.__name} recargada. Balas actuales: {self.__ammo}")

    # Método para usar munición internamente (Acceso controlado)
    def _use_ammo(self):
        if self.__ammo > 0:
            self.__ammo -= 1
            return True
        print(f"❌ {self.__name} hizo click (Sin munición)")
        return False

    # Método Abstracto: Obliga a las hijas a definir CÓMO disparan (Polimorfismo)
    @abstractmethod
    def shoot(self):
        pass

# ---------------------------------------------------------
# 2. HERENCIA & POLIMORFISMO
# ---------------------------------------------------------

class Rifle(Weapon): # Hereda todo de Weapon
    def shoot(self):
        # Polimorfismo: Implementación específica para Rifle
        if self._use_ammo():
            print(f"💥 {self.name} disparó una ráfaga precisa! Daño: {self._damage}")

class Shotgun(Weapon): # Hereda todo de Weapon
    def shoot(self):
        # Polimorfismo: Implementación diferente (dispersión)
        if self._use_ammo():
            print(f"💥 {self.name} disparó perdigones dispersos! Daño: {self._damage * 3} (Corto alcance)")

class Pistol(Weapon): # Hereda todo de Weapon
    def shoot(self):
        # Polimorfismo: Implementación diferente (tiro rápido)
        if self._use_ammo():
            print(f"💥 {self.name} disparó rápido. Daño: {self._damage}")

# ---------------------------------------------------------
# 3. COMPOSICIÓN
# ---------------------------------------------------------

class ShootingRange:
    def __init__(self):
        self.weapons = [] # Composición: Esta clase "TIENE" una lista de objetos Weapon

    def add_weapon(self, weapon: Weapon):
        self.weapons.append(weapon)

    def start_simulation(self):
        print("\n--- INICIANDO SIMULACIÓN DE TIRO ---")
        # Itera sobre la lista (La clase contenedora gestiona a las contenidas)
        for weapon in self.weapons:
            weapon.shoot() 
            weapon.reload(5)
            weapon.shoot()
            print("-" * 30)

# ---------------------------------------------------------
# EJECUCIÓN
# ---------------------------------------------------------

if __name__ == "__main__":
    # Instanciamos las clases concretas
    my_rifle = Rifle(name="AK-47", ammo=10, damage=30)
    my_shotgun = Shotgun(name="Mossberg", ammo=2, damage=50)
    
    # Usamos la composición (El campo de tiro contiene las armas)
    range_sim = ShootingRange()
    range_sim.add_weapon(my_rifle)
    range_sim.add_weapon(my_shotgun)

    # Corremos la lógica
    range_sim.start_simulation()
