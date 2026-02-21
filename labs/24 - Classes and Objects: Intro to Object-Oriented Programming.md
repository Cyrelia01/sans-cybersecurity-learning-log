Classes and Objects: Intro to Object-Oriented Programming

## Objective

Introduce object-oriented programming (OOP) concepts by creating two classes, Hero() and Monster(), and using them to instantiate objects (warrior and beast) that interact through class methods.

This lab demonstrates:
- Defining classes with attributes
- Creating object instances from classes
- Using methods with self
- Passing objects into methods (object-to-object interaction)
- Updating object state (health changes)
- Using conditional logic to trigger outcomes (monster runs away, hero dies)
- Exiting a program intentionally using sys.exit()

## Environment
- Linux lab container
- Python interpreter (python / python3)
- Source file: output.py

## Phase 1 – Defining Classes and Attributes

The lab begins by defining two classes: Hero() and Monster().

The hero class was created with base attributes:

```Python
class Hero():
  health = 100
  attack_damage = 20
  healing_increase = 50
```

The monster class was created with its own attributes:

```Python
class Monster():
  health = 100
  attack_damage = 30
```

These attributes represent “default” values for any object created from these classes.

### Phase 2 – Adding Methods to Classes

Two methods were added:
- drink_potion() for the hero to recover health
- roar() for the monster to roar

Hero method:

```Python
def drink_potion(self):
    self.health += self.healing_increase
    print("Ahhh, healing potion. I feel mighty again!")
    print(">> Hero's health: %s\n" % self.health)
```

Monster method:

```Python
def roar(self):
    print("RooooaarrRRRR!")
```

These methods introduce the use of self, which refers to the current object instance executing the method.

### Phase 3 – Creating Objects and Calling Methods

Two objects were created from the classes:
- warrior = Hero()
- beast = Monster()

A small “story” was started by calling methods:

warrior.drink_potion()
beast.roar()

Output:

```Python
Ahhh, healing potion. I feel mighty again!
>> Hero's health: 150

RooooaarrRRRR!
```
This confirmed:
- Objects were created successfully
- Methods executed correctly
- The hero’s health increased by the potion amount

### Phase 4 – Object Interaction via Attack Methods

A method was added to allow the hero to attack the monster.

Hero method:

```Python
def attack_monster(self, name):
    print("Take that you fiend!")
    name.health -= self.attack_damage
    print(">> Monster's health: %s\n" % name.health)
```

This method accepts the monster object as an argument (name) and reduces the monster’s health.

The story was updated:

warrior.attack_monster(beast)

Output:

```Python
Take that you fiend!
>> Monster's health: 80
```

Next, the monster was given the ability to attack the hero.

Monster method:

```Python
def attack_hero(self, name):
    print("Raaaaarrrrrrr!!")
    name.health -= self.attack_damage
    print(">> Hero's health: %s\n" % name.health)
```

The story was updated to attack twice:

beast.attack_hero(warrior)
beast.attack_hero(warrior)

Output:

```Python
Raaaaarrrrrrr!!
>> Hero's health: 120

Raaaaarrrrrrr!!
>> Hero's health: 90
```

This reinforced that:
- Objects can be passed into methods as arguments
- Methods can modify another object’s attributes directly
- Health values persist across method calls

### Phase 5 – Adding Conditions and Exit Behavior

The lab introduced game outcomes:
- If monster health drops below 30, it runs away
- If hero health reaches 0 or below, the hero dies

These outcomes terminate the program using sys.exit()

Because sys.exit() was introduced, the sys module was imported:

```Python
import sys
```

Monster run-away condition added inside attack_monster():

```Python
if name.health < 30:
      print("Begone you hellish brute!")
      print(">> The monster has run away\n")
      sys.exit()
```

Hero death condition added inside attack_hero():

```Python
if name.health <= 0:
      print("Raaar RaaarrrRR RRARRR!")
      print(">> The hero is no more\n")
      sys.exit()
```

This demonstrated:
- Conditional logic can enforce “game rules”
- Program termination can be used intentionally once a final outcome occurs

### Final Script and Story Flow

The story was expanded into a longer interaction:

Full code:

```Python
import sys

class Hero():
  health = 100
  attack_damage = 20
  healing_increase = 50

  def drink_potion(self):
    self.health += self.healing_increase
    print("Ahhh, healing potion. I feel mighty again!")
    print(">> Hero's health: %s\n" % self.health)

  def attack_monster(self, name):
    print("Take that you fiend!")
    name.health -= self.attack_damage
    print(">> Monster's health: %s\n" % name.health)
    if name.health < 30:
      print("Begone you hellish brute!")
      print(">> The monster has run away\n")
      sys.exit()

class Monster():
  health = 100
  attack_damage = 30

  def roar(self):
    print("RooooaarrRRRR!")

  def attack_hero(self, name):
    print("Raaaaarrrrrrr!!")
    name.health -= self.attack_damage
    print(">> Hero's health: %s\n" % name.health)
    if name.health <= 0:
      print("Raaar RaaarrrRR RRARRR!")
      print(">> The hero is no more\n")
      sys.exit()

warrior = Hero()
beast = Monster()

print("A monster leaps from its cave and strikes our hero!\n")
beast.attack_hero(warrior)
warrior.attack_monster(beast)
beast.attack_hero(warrior)
warrior.drink_potion()
beast.roar()
warrior.attack_monster(beast)
warrior.attack_monster(beast)
beast.attack_hero(warrior)
warrior.attack_monster(beast)
```

Final output:

```Python
A monster leaps from its cave and strikes our hero!

Raaaaarrrrrrr!!
>> Hero's health: 70

Take that you fiend!
>> Monster's health: 80

Raaaaarrrrrrr!!
>> Hero's health: 40

Ahhh, healing potion. I feel mighty again!
>> Hero's health: 90

RooooaarrRRRR!
Take that you fiend!
>> Monster's health: 60

Take that you fiend!
>> Monster's health: 40

Raaaaarrrrrrr!!
>> Hero's health: 60

Take that you fiend!
>> Monster's health: 20

Begone you hellish brute!
>> The monster has run away
```

The story ends when the monster’s health falls below 30 and triggers the run-away condition.

## Key Concepts 
- Classes define templates for objects
- Objects are instances created from classes
- Attributes represent object state (health, attack_damage)
- Methods define behaviors (attack, heal, roar)
- self refers to the current object instance
- Objects can be passed into methods and modified directly
- Conditional logic can enforce outcome rules
- sys.exit() terminates execution when an outcome is reached

## Conclusion

This lab introduced object-oriented programming in Python by building a simple battle simulation using classes, objects, attributes, and methods.

By progressively adding interaction and outcome logic, the exercise reinforced the difference between defining a class template and using objects as stateful entities that evolve during execution.

The final version demonstrated a complete OOP workflow:
- Define classes and attributes
- Add methods and behaviors
- Instantiate objects
- Execute interactions
- Trigger outcomes based on object state
