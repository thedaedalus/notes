## Core Object Oriented Programming Concepts
### 1. Class and Object
- **Class**: a blueprint (defines data + behaviour).
- **Object/ Instance**: a concrete thing created from a class.
	- In Python:
```python
	class Player:
    def __init__(self, name):
        self.name = name
p = Player("Alice")  # p is an object
```

### 2. Attributes and Methods

- **Attributes**: data stored on an object (fields).
- **Methods**: functions defined inside a class that operate on the object.
- `self` refers to “this particular instance”
### 3. Encapsulation

- Group related data and behavior together in a class.
- Hide internal details, expose a clear interface.
- Use naming conventions for privacy:
  - `_name`: “internal use” (convention).
  - `_name`: name-mangled, harder to access from outside.

### 4. Inheritance

- A class can **inherit** from another class and reuse/extend its behavior.
- Parent/base/superclass → child/subclass.
- Child class inherits attributes and methods from parent class.
- In Python:
```python
class Enemy:
     pass

class Dragon(Enemy):  # Dragon is an Enemy
    pass
```

- Use `super()` to call parent methods:
```python
super().__init__(...)
```
### 5. Polymorphism

- Different classes can provide the same method name but with different implementations.
- Code can call `obj.do_thing()` without knowing the exact type, as long as that method exists.
- Common with overridden methods in subclasses.
- Also includes operator overloading, where operators like `+` call special methods (e.g. `__add__`) and behave differently for different types.
  - Some common ones:
    - `__add__(self, other)` → `a + b`
    - `__sub__(self, other)` → `a - b`
    - `__mul__(self, other)` → `a * b`
    - `__eq__(self, other)` → `a == b`
    - `__lt__(self, other)` → `a < b`
    - `__str__(self)` → `str(a)` / `print(a)`

- **Table of Special Methods** [Link to special method Python Docs](https://docs.python.org/3/reference/datamodel.html#special-method-names)


| Operation             | Operator | Method        |
|----------------------:|:--------:|:--------------|
| Addition              | `+`      | `__add__`     |
| Subtraction           | `-`      | `__sub__`     |
| Multiplication        | `*`      | `__mul__`     |
| Power                 | `**`     | `__pow__`     |
| Division              | `/`      | `__truediv__` |
| Floor Division        | `//`     | `__floordiv__`|
| Remainder (modulo)    | `%`      | `__mod__`     |
| Bitwise Left Shift    | `<<`     | `__lshift__`  |
| Bitwise Right Shift   | `>>`     | `__rshift__`  |
| Bitwise AND           | `&`      | `__and__`     |
| Bitwise OR            | `\|`     | `__or__`      |
| Bitwise XOR           | `^`      | `__xor__`     |
| Bitwise NOT           | `~`      | `__invert__`  |
| String                | `""`     | `__str__`     |

```python
SUITS = ["Clubs", "Diamonds", "Hearts", "Spades"]

RANKS = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King", "Ace"]


class Card:
    def __init__(self, rank, suit):
        self.rank = rank
        self.suit = suit
        self.rank_index = RANKS.index(self.rank)
        self.suit_index = SUITS.index(self.suit)

    def __eq__(self, other):
        return (
            self.rank_index == other.rank_index and self.suit_index == other.suit_index
        )



    def __lt__(self, other):
        return (
            self.rank_index < other.rank_index
            or (self.rank_index == other.rank_index and self.suit_index < other.suit_index)
        )
         
    def __gt__(self, other):
        return ( 
            self.rank_index > other.rank_index
            or (self.rank_index == other.rank_index and self.suit_index > other.suit_index)
        )
         
    # don't touch below this line

    def __str__(self):
        return f"{self.rank} of {self.suit}"
```

### 6. Abstraction

- Focus on **what** an object does, not **how** it does it.
- Hide complex internals behind simple methods.
- Example idea: `shape.area()` without caring how circles vs rectangles compute it.

### 7. Composition

- Build complex objects by combining other objects.
- “Has-a” relationship instead of “is-a”.
- Example: `Car` has an `Engine` object as an attribute.

### 8. Method Types (Python-specific)

- **Instance methods**: `def method(self, ...)` → act on one object.
- **Class methods**: `@classmethod def method(cls, ...)` → act on the class.
- **Static methods**: `@staticmethod def method(...)` → utility, no self or cls.

## Geometry concepts used

- Inheritance and `super()`
  - A child class can reuse and extend a parent class.
  - Use `super().__init__(...)` to call the parent’s constructor and initialize shared attributes.

- Center-based rectangles
  - Sometimes an object’s position is stored as its center (pos_x, pos_y) plus a width and height.
  - To get rectangle corners from center and size:
    - `left = center_x - width / 2`
    - `right = center_x + width / 2`
    - `bottom = center_y - height / 2`
    - `top = center_y + height / 2`

- Composition
  - A class can contain another object to represent part of its behavior or state (e.g. a “hit box” rectangle stored as a `Rectangle` instance).

- Instance vs class
  - To create an object, call the class like a function: `obj = ClassName(...)`.
  - Instance methods are called on objects, not on the class:
    - `obj.method(other_obj) instead of ClassName.method(obj, other_obj)`.

- Overlap checking
  - Rectangles can define an `overlaps(other)` method that checks if their ranges on the x-axis and y-axis intersect.
  - Higher-level classes can use this to answer questions like “am I in this area?” by delegating to the rectangle’s `overlaps` method.
