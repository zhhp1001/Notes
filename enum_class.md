# Why is enum class preferred over plain enum?

https://stackoverflow.com/questions/18335861/why-is-enum-class-preferred-over-plain-enum

C++ has two kinds of enum:

enum classes
Plain enums
Here are a couple of examples on how to declare them:

 enum class Color { red, green, blue }; // enum class
 enum Animal { dog, cat, bird, human }; // plain enum 
What is the difference between the two?

enum classes - enumerator names are local to the enum and their values do not implicitly convert to other types (like another enum or int)

Plain enums - where enumerator names are in the same scope as the enum and their values implicitly convert to integers and other types

Example:

enum Color { red, green, blue };                    // plain enum 
enum Card { red_card, green_card, yellow_card };    // another plain enum 
enum class Animal { dog, deer, cat, bird, human };  // enum class
enum class Mammal { kangaroo, deer, human };        // another enum class

void fun() {

    // examples of bad use of plain enums:
    Color color = Color::red;
    Card card = Card::green_card;

    int num = color;    // no problem

    if (color == Card::red_card) // no problem (bad)
        cout << "bad" << endl;

    if (card == Color::green)   // no problem (bad)
        cout << "bad" << endl;

    // examples of good use of enum classes (safe)
    Animal a = Animal::deer;
    Mammal m = Mammal::deer;

    int num2 = a;   // error
    if (m == a)         // error (good)
        cout << "bad" << endl;

    if (a == Mammal::deer) // error (good)
        cout << "bad" << endl;

}
Conclusion:
enum classes should be preferred because they cause fewer surprises that could potentially lead to bugs.