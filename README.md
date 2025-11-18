#  Gun Shooting Simulator - OOP Concepts Guide

## Overview
This  OOP example demonstrates **ALL major object-oriented programming concepts** through an interactive gun shooting simulation. Each concept is clearly explained with practical examples.

---

## 🔒 1. ENCAPSULATION
**Definition**: Hiding internal state and requiring all interaction through methods.

### Features Demonstrated:
- **Private Attributes**: `__name`, `__damage`, `__current_ammo`
- **Property Getters**: `@property` for controlled read access
- **Property Setters**: Validation in `@damage.setter`
- **Data Protection**: Private methods prevent external access

### Code Example:
```python
class Weapon(ABC):
    def __init__(self, name: str, damage: int, ...):
        self.__name = name  # Private attribute
        self.__damage = damage
    
    @property
    def name(self) -> str:  # Controlled read access
        return self.__name
    
    @damage.setter
    def damage(self, value: int):  # Controlled write with validation
        if value > 0:
            self.__damage = value
        else:
            raise ValueError("Damage must be positive")
```

---

## 🧬 2. INHERITANCE
**Definition**: Creating new classes based on existing ones, inheriting attributes and methods.

### Features Demonstrated:
- **Base Class**: `Weapon` (abstract)
- **Subclasses**: `Gun` → `Rifle`, `Pistol`, `Shotgun`
- **Method Inheritance**: All subclasses inherit `shoot()`, `reload()`
- **Attribute Inheritance**: All subclasses inherit base weapon properties

### Code Example:
```python
class Weapon(ABC):  # Base class
    def __init__(self, name, damage, ...):
        self.__name = name
        ...

class Gun(Weapon):  # Inherits from Weapon
    def __init__(self, name, damage, fire_rate, ...):
        super().__init__(name, damage, ...)  # Call parent constructor

class Rifle(Gun):  # Inherits from Gun → Weapon
    def __init__(self, name="Assault Rifle"):
        super().__init__(name, damage=35, ...)  # Call parent constructor
```

---

## 🎭 3. POLYMORPHISM
**Definition**: Same interface, different implementations.

### Features Demonstrated:
- **Method Overriding**: `shoot()`, `__str__()`, `get_fire_rate()`
- **Same Interface**: All weapons respond to `shoot()` differently
- **Runtime Dispatch**: Correct method called based on object type

### Code Example:
```python
# Same method, different implementations
def shoot(self) -> dict:  # Base Weapon class
    # Generic shooting logic

def get_fire_rate(self) -> float:  # Rifle
    return self.__fire_rate

def sniper_shot(self) -> dict:  # Rifle special method
    # Rifle-specific sniper shot

def spread_shot(self) -> dict:  # Shotgun special method
    # Shotgun-specific spread shot
```

---

## 🧩 4. ABSTRACTION
**Definition**: Hiding complex implementation, showing only essential features.

### Features Demonstrated:
- **Abstract Base Class**: `Weapon` cannot be instantiated
- **Abstract Methods**: `get_fire_rate()`, `get_projectile_speed()`
- **Interface Definition**: Defines what weapons must implement
- **Implementation Hiding**: Complex logic hidden in concrete classes

### Code Example:
```python
from abc import ABC, abstractmethod

class Weapon(ABC):  # Abstract class
    @abstractmethod
    def get_fire_rate(self) -> float:  # Must be implemented
        pass
    
    @abstractmethod
    def get_projectile_speed(self) -> float:
        pass

# Cannot do this:
weapon = Weapon("Test", 10, 10, 1.0)  # ❌ TypeError!

# Must do this:
rifle = Rifle("AK-47")  # ✅ Concrete implementation
```

---

## 🔗 5. COMPOSITION
**Definition**: Objects containing other objects (has-a relationships).

### Features Demonstrated:
- **Has-A Relationships**: `ShootingRange` has `Weapon` objects
- **Object Aggregation**: Range manages multiple weapons
- **Delegation**: Range methods delegate to weapon methods
- **Lifecycle Management**: Range controls weapon lifecycle

### Code Example:
```python
class ShootingRange:  # Main class
    def __init__(self, name: str):
        self.weapons = []  # Composition: has weapons
    
    def add_weapon(self, weapon: Weapon):  # Add weapon to range
        self.weapons.append(weapon)
    
    def simulate_firefight(self, duration_seconds: int = 10):
        for weapon in self.weapons:  # Use contained objects
            result = weapon.shoot()  # Delegate to weapon methods
```

---

##  Practical Simulation Features

### Realistic Gun Mechanics:
- **Fire Rate Control**: Respects time between shots
- **Ammo Management**: Automatic reload when empty
- **Damage Calculation**: Different weapons have different damage
- **Projectile Physics**: Speed calculations for bullet trajectory

### Specialized Abilities:
- **Rifle**: Sniper shots with enhanced damage
- **Pistol**: Quick draw for emergency reloads
- **Shotgun**: Spread shots with multiple pellets

### Advanced Features:
- **Firefight Simulation**: Automated combat scenarios
- **Performance Statistics**: Track weapon effectiveness
- **Real-time Feedback**: Live ammo and damage updates

---

##  Learning Outcomes

After studying this code, you will understand:

1. **Encapsulation**: How to protect data with private attributes and controlled access
2. **Inheritance**: How to create class hierarchies and reuse code
3. **Polymorphism**: How same interface can have different implementations
4. **Abstraction**: How to define interfaces without implementation details
5. **Composition**: How to build complex systems from simpler components

### Key Programming Concepts:
- Abstract classes and methods
- Property decorators (getters/setters)
- Method overriding and super() calls
- Private attributes and name mangling
- Type hints and documentation
- Error handling and validation
- Real-time simulation logic

---

##  How to Use

### Run the Demonstration:
```bash
python gun_shooting_simulator.py
```

### Modify and Experiment:
1. Create new weapon types (machine guns, sniper rifles)
2. Add new abilities (grenade launchers, explosive rounds)
3. Implement new simulation scenarios
4. Add damage calculation models



---

