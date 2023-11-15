# Factory Method and Examples

> Define an interface for creating an object, **but let subclasses decide which class to instantiate**. Factory Method lets a class defer instantiation to subclasses.

Definitions of the codes are below them.

## Example in Rust

```rust
trait Sizes {
    fn get_width(&self) -> f64;
    fn get_height(&self) -> f64;
}

enum Color {
    Walnut,
    Crimson,
    Pine,
}

impl Color {
    fn as_str(&self) -> &str {
        match self {
            Color::Walnut => "walnut brown",
            Color::Crimson => "crimson red",
            Color::Pine => "pine green",
        }
    }
}

trait Colors {
    fn get_color(&self) -> &str;
}

struct Door {
    width: f64,
    height: f64,
    color: Color,
}

impl Door {
    fn new(width: f64, height: f64, color: Color) -> Self {
        Door {
            width,
            height,
            color,
        }
    }
}

impl Sizes for Door {
    fn get_width(&self) -> f64 {
        self.width
    }

    fn get_height(&self) -> f64 {
        self.height
    }
}

impl Colors for Door {
    fn get_color(&self) -> &str {
        self.color.as_str()
    }
}

fn main() {
    let brown_door = Door::new(210.00, 70.50, Color::Walnut);
    println!("What is the width size of the door? {}", brown_door.get_width());
    println!("What is the color of the door? {}", brown_door.get_color());
}

```

> In the Factory Method pattern, you define an interface (or a trait in Rust) for creating an object, but you leave the choice of its type to the subclasses (or implementing types). In your case, the Door struct and the Color enum act as components of this pattern.
>
> Here's how your code aligns with the Factory Method pattern:
>
> Trait/Interface: In your code, you have two traits, Sizes and Colors, which define the interface for objects that implement these traits. These traits provide the behavior that can vary across different implementations.
>
> Concrete Implementations: The Door struct and the Color enum are the concrete implementations. The Door struct acts as the product that is being created, and the Color enum provides a mechanism for choosing among different variants of colors.
>
> Factory Method: In the code, the Door::new function serves as a factory method. It allows you to create instances of Door with different properties, including the color, without specifying the exact implementation details in the client code. This is similar to how factory methods in design patterns allow you to create objects without knowing their specific types.
>
> Client Code: In your main function, you create instances of Door using the factory method (Door::new) and don't need to be aware of the specific          implementation details. This separation of client code from the details of object creation is a key characteristic of the Factory Method pattern.
>
> Overall, while it's not a strict implementation of the Factory Method pattern, your code exhibits elements of it by abstracting the creation of Door objects and providing flexibility in specifying their properties, particularly the color.


## Example in TypeScript

```typescript
interface Sizes {
    get_width(): number;
    get_height(): number;
}

enum Color {
    Walnut = "walnut brown",
    Crimson = "crimson red",
    Pine = "pine green",
    // Add more colors as needed
}

interface Colors {
    get_color(): string;
}

class Door implements Sizes, Colors {
    constructor(
      private width: number,
      private height: number,
      private color: Color
    ) {}

    get_width(): number {
        return this.width;
    }

    get_height(): number {
        return this.height;
    }

    get_color(): string {
        return this.color;
    }
}

const brown_door = new Door(210.00, 70.50, Color.Walnut);
console.log("What is the width size of the door?", brown_door.get_width());
console.log("What is the color of the door?", brown_door.get_color());
```

> In this TypeScript code:
>
> - We use interfaces (Sizes and Colors) to define the structure of the objects.
> - We use an enum (Color) to define the different color options.
> - The Door class implements the Sizes and Colors interfaces.
> - The constructor of the Door class initializes the width, height, and color.
> - The get_width(), get_height(), and get_color() methods are implemented to return the corresponding values.
> - We create a brown_door object with the Color.Walnut enum variant to specify the color.
>
> This TypeScript code mirrors the structure and behavior of the Rust code you provided, making it a TypeScript equivalent of the original Rust code.


## Example in C++

```cpp
#include <iostream>
#include <string>

class Sizes {
public:
    virtual double get_width() = 0;
    virtual double get_height() = 0;
};

enum class Color {
    Walnut,
    Crimson,
    Pine,
    // Add more colors as needed
};

class Colors {
public:
    virtual std::string get_color() = 0;
};

class Door : public Sizes, public Colors {
private:
    double width;
    double height;
    Color color;

public:
    Door(double width, double height, Color color)
        : width(width), height(height), color(color) {}

    double get_width() override {
        return width;
    }

    double get_height() override {
        return height;
    }

    std::string get_color() override {
        switch (color) {
            case Color::Walnut:
                return "walnut brown";
            case Color::Crimson:
                return "crimson red";
            case Color::Pine:
                return "pine green";
            // Add more cases for additional colors
        }
        return "unknown";
    }
};

int main() {
    Door brown_door(210.00, 70.50, Color::Walnut);
    std::cout << "What is the width size of the door? " << brown_door.get_width() << std::endl;
    std::cout << "What is the color of the door? " << brown_door.get_color() << std::endl;
    return 0;
}
```

> In this C++ code:
>
> - We use classes to define the Sizes and Colors interfaces.
> - We use an enumeration (Color) to define the different color options.
> - The Door class inherits from Sizes and Colors and provides implementations for the respective virtual functions.
> - The Color enum is used within the Door class to specify the color.
> - In the main function, we create a brown_door object with the Color::Brown enum variant and call methods to access the width and color.
>
> This C++ code replicates the structure and behavior of the TypeScript code, making it a C++ equivalent of the original TypeScript code.
