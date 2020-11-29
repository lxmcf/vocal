<h1 align="center">Vocal Syntax</h1>

<p align="center">
    <a href="#styling">Styling</a> |
    <a href="#naming-conventions">Naming Conventions</a> |
    <a href="#coding-conventions--rules">Coding Conventions & Rules</a>
</p>

Vocal (Vala C like) syntax is a syntax and coding style designed for Vala styled towards stand alone game development and prototype code.

A lot of the current syntax is borrowed from the [elementary OS](https://docs.elementary.io/develop/writing-apps/code-style) style guide.

## Styling

---

The following style guidelines do not explicitly conform to the naming conventions and final syntax listed at the end of the styling section, this is to allow examples to be short and to the point.

### Columns Per Row

It is recommended to keep your columns below 120 however the hard limit should be treated as 160, it is recommended to take use of your editor of choices ruler or line width guides.

### Whitespace

Whitespace should always go between parentheses and braces.

```vala
public void foo (string lorem) {
    // ..
}

if (bar == "lorem ipsum") {
    return "dolor sit amet";
}

for (int i = 0; i < 16; i++) {
    // ..
}

foo ("lorem ipsum")

Foo* bar = new Foo ();
```

When performing math, all arguments must be seperated by whitespaces, for example:

```vala
public int average (int first, int second, int third) {
    return (first + second + third) / 3;
}
```

Blank lines should be found between each line unless you are performing 1 form of action in a row, for examlpe:

```vala
if (statement) {
    // ..
}

warning ("Lorem");
error ("ipsum!");

int nice = (8 * 8) + 5;
```

### Parentheses, braces, brackets & chevrons

All parentheses must be surrounded by whitespace (or a semicolon), braces should open on the same line and follow the below styling.

Brackets and chevrons should never begin with whitespace.

```vala
if (condition) {
    // ..
} else {
    // ..
}

string[] foo = string[1];
List<string> foo = new List<string> ();
```

### Indentation

Vocal Syntax should use either 1 tab or 4 spaces (Mixing these is a forbidden form of devil worship), to keep this consistent; it is recommend to use [EditorConfig](https://editorconfig.org/) if supported by your editor.

Each new block of code within a set of braces should increment the current indentation by 1 unit (1 tab or 4 spaces).

```vala
public int? multiply_values (int a, int b, int c, int d, int multiplier, bool cout) {
    if (multiplier == 0) {
        warning ("Cannot divide by 0");

        return null;
    }

    return (a + b + c + d) * multiplier;
}
```

The only exception to the above is if your conditional statement is followed by a single line of code, for example see the first return statement:

```vala
public int print_debug (string message) {
    if (message == "") return 1;

    warning (message);

    return 0;
}
```

Switch statements follow a very similar indentation format as braces but fall short at the break point, for example:

```vala
switch (year) {
    case 1998:
        message ("Not a bad year");
        break;

    case 1969:
    case 1960:
        message ("Pretty spicy!");

    case 2020:
        error ("Let's not talk about it");

    default:
        message ("Nothing else matters");
}
```

### Comments & Code Documentation

Comments should always be given a new line and never be inline with code:

```vala
public enum OperatingSystem { // Inline comment, not to be done!
    ELEMENTARY,
    UBUNTU,
    ARCH,

    // New line comment, to be used
    UNKNOWN
}
```

Comments should be used to mark points of interest in code such as known errors or mark things you need to do, please see the below example:

```vala
// TODO: Work out some funny things to hide
// FIXME: Find the spelling mistake in this code example
// BUG: Another word for an insect
```

Comments should be kept short and sweet, but if you require to write multiple lines of text, do not use the `//` syntax, please use the `/* .. */` syntax as follows:

```vala
/*
 * I know I should not be using these types of comments but
 * lets be honest no one is going to read this!
 */
```

Comments should be used on any code that may be hard to understand at first glance and **NEVER** contain emoji's or emoticons as these practices can clutter your code as well as provide no assitance, for example the following comment's should never be present:

```vala
// Sets variable 'a' to 0 :-)
int a = 0;

// Sets variable 'b' to 1 😀
int b = 1;

// The main entry point for my program
public static int main (string[] args) {
    // ..
}

```

## Naming Conventions

---

### Variable & Function

Variable's should never use shorthand terms as these can easily be confused for alternate words, a longer variable name may look messier in cases but can remove the need for unnecessary comments, the following example should **NOT** be used:

```vala
// Window x position
int win_x = 0;

// Winner x position
int winn_x = 0;
```

As you can see, this looks horrible and will become very easy to mistype, the following example is the recommended format:

```vala
int window_x = 0;
int winner_x = 0;
```

Public variable's inside a struct or class should be prefix with `m_` while private variable's should be prefixed with `p_`; then followed by the first letter of its type, both instances should be lower case:

```vala
struct FooBar {
    public string m_sMessage;
    public int m_iNumber;
}
```

Global scope varaibles follow a similar style as the above but should be prefixed with `g_`:

```vala
public static string g_sGlobalString;

public static int main (string[] args) {
    // ..
}
```

As Vocal Syntax recommends using Vala's pointer syntax, if you are not using a standard data type for your variable (`string`, `int`, `float`, ETC), you should define your variable with it's scope prefix (`g_`, `m_` or `p_`) followed by a lower case `p` for pointer, the following example assumes you are using SDL2:

```vala
// Global
public static SDL.Window* g_pWindow = new SDL.Window ();

// Within class or struct
public struct Example {
    public SDL.Window* m_pWindow;

    private SDL.Renderer* p_pRenderer;
}
```

Variable's in the user facing space should follow a `CamalCase` style of naming, however when within a function it is recommend to use a `snake_case` or a `CamalCase` prefixed with an underscore:

```vala
// snake_case
public void foo () {
    string lorem_ipsum = "dolor sit amet";
    int foo_bar = 42;
}

// CamalCase
public void bar () {
    string _LoremIpsum = "dolor sit amet";
    int _FooBar = 42;
}
```

Function's should always follow a `snake_case` style to keep inline with the majority of vala bindings out in the wild:

```vala
public void foo_bar () {
    // ..
}

public int lorem_ipsum () {
    // ..
}
```

### Constant & Enum

Constant's should always be written in upper case regardless of scope with each word seperated by an underscore:

```vala
public const string TARGET = "elementary OS";
public const int PROJECT_VERSION = 6;
```

Enums follow a similar style however only the enum members should be capatalised with the enum name being `CamalCase`:

```vala
public enum OperatingSystem {
    ELEMENTARY,
    UBUNTU,
    ARCH
}
```

### Struct and Class

As outlined in [Coding Conventions]("#"), you should use never mix the use of class and struct and instead choose 1, however both will follow the same `CamalCase` naming convention:

```vala
struct FooBar {
    // ..
}

class LoremIpsum {
    // ..
}
```

### Namespace

As outlined in [Coding Conventions]("#"), you should be using 1 namespace at max; if any, however if you must use a namespace; it is to be using `CamalCase`:

```vala
namespace FooBar {
    public void lorem_ipsum () {
        // ..
    }
}
```

## Coding Conventions & Rules

[Coming soon]
