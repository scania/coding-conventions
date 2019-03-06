# Corporate Coding Conventions

Coding practices are a source of a lot of arguments among programmers. Coding standards, to some degree, help us to put certain questions to bed and resolve stylistic debates. No coding standard makes everyone happy and even their existence is sure to make some unhappy. What follows are the standards we put together within the developer community, which have become the general coding standard for all programming teams on new code development. We’ve tried to balance the need for creating a common, recognizable and readable code base with not unduly burdening the programmer with minor code formatting concerns.

## Table Of Contents

- [Why we need Coding Standards](#why-we-need-coding-standards)
- [Context is Important](#context-is-important)
- [Stylistic Standards](#stylistic-standards)
  * [Namespaces](#namespaces)
  * [Naming Conventions](#naming-conventions)
    + [Local variables](#local-variables)
    + [Member variables](#member-variables)
    + [Type names (struct, class, enum)](#type-names-struct-class-enum)
    + [Standard types](#standard-types)
    + [Other](#other)
    + [Enumerated values and constants](#enumerated-values-and-constants)
    + [Pointers](#pointers)
    + [CPP Macros](#cpp-macros)
    + [Namespaces](#namespaces-1)
    + [Source code file and directory names](#source-code-file-and-directory-names)
    + [Whitespace](#whitespace)
    + [Variable Declaration](#variable-declaration)
    + [switch statements](#switch-statements)
- [Coding Standard: Nomenclature](#coding-standard-nomenclature)
  * [Spelling](#spelling)
  * [Accessors](#accessors)
  * [Opposites](#opposites)
    + [Create/Destroy](#createdestroy)
    + [Init/Shutdown](#initshutdown)
    + [Start/Stop](#startstop)
    + [Suspend/Resume](#suspendresume)
    + [Begin/End](#beginend)
    + [Enter/Exit](#enterexit)
    + [Add/Remove](#addremove)
    + [Open/Close](#openclose)
    + [Acquire/Release](#acquirerelease)
- [Coding Standards](#coding-standards)
  * [Use a struct for passive data carriers, a class for everything else](#use-a-struct-for-passive-data-carriers-a-class-for-everything-else)
  * [Data members of a struct must be public](#data-members-of-a-struct-must-be-public)
  * [Data members of a class must be private](#data-members-of-a-class-must-be-private)
  * [No friend declarations](#no-friend-declarations)
  * [Constructors should not do any real work](#constructors-should-not-do-any-real-work)
  * [Perform object initialization in Create() or TryCreate()](#perform-object-initialization-in-create-or-trycreate)
  * [All destructors should be empty](#all-destructors-should-be-empty)
  * [Perform object clean up in Destroy()](#perform-object-clean-up-in-destroy)
  * [Integer scalars should be signed](#integer-scalars-should-be-signed)
  * [Only specify integer width on data members (and always do so then)](#only-specify-integer-width-on-data-members-and-always-do-so-then)
  * [Do not use enum types as data members](#do-not-use-enum-types-as-data-members)
  * [Parameters passed by reference must be const](#parameters-passed-by-reference-must-be-const)
  * [Function parameter order: output, update, input](#function-parameter-order-output-update-input)
  * [Header files must begin with #pragma once](#header-files-must-begin-with-pragma-once)
  * [Don't use #include if a forward declaration would suffice](#dont-use-include-if-a-forward-declaration-would-suffice)
  * [Byte, Size, Count](#byte-size-count)
  * [Singletons](#singletons)
  * [Casting](#casting)
  * [No Booleans in aggregates](#no-booleans-in-aggregates)
  * [No booleans as function parameters](#no-booleans-as-function-parameters)
  * [Booleans in local scope or as return values](#booleans-in-local-scope-or-as-return-values)
  * [C Bit fields](#c-bit-fields)
  * [Memory and the CRT](#memory-and-the-crt)
  * [No control flow macros](#no-control-flow-macros)
  * [Do not use named number constants](#do-not-use-named-number-constants)
  * [SPU/PPU aliased data structures](#spuppu-aliased-data-structures)
  * [Const correctness](#const-correctness)
  * [Conditionals require explicit braces](#conditionals-require-explicit-braces)
  * [Header files must contain all their dependencies](#header-files-must-contain-all-their-dependencies)
- [Best Practices](#best-practices)
  * [Avoid "magic values"](#avoid-magic-values)
  * [Keep implementation details out of the public interface](#keep-implementation-details-out-of-the-public-interface)
  * [Non-trivial code should be kept out of headers](#non-trivial-code-should-be-kept-out-of-headers)
  * [Avoid negative flags](#avoid-negative-flags)
  * [Consider using a struct to return multiple items](#consider-using-a-struct-to-return-multiple-items)
  * [Prune commented-out and unused code](#prune-commented-out-and-unused-code)
  * [Compile without warnings](#compile-without-warnings)
  * [Add comments identify #else/#elif/#endif statements](#add-comments-identify-elseelifendif-statements)
- [Further Reading](#further-reading)

# Why we need Coding Standards

The [first section](#stylistic-standards) of this document concerns style choices. The choices are largely arbitrary, although given equivalent choices we erred on the side of forms that would work best with our Visual Studio based editing tools.
The [second section](#coding-standard-nomenclature) and [third section](#coding-standards) address more substantive topics. The rules seek to find a balance between code which is more robust and not too much of a burden to the programmer to write. We've sought to back each item up with a rationale and citation of supporting documentation.
The [fourth section](#best-practices) contains a set of best practices. These are guidelines which can change strongly depending on the context in which they come up and we weren't comfortable layout out a blanket rule to cover them.
Conformity in the API is important to help the user develop an intuition for how to use it. Although every programmer is encouraged to bring their own insight and wisdom to the project, we must also ensure that there is enough consistency so that we can read, use, debug, and maintain each others code. Also, we must consider our direct customers, the users of the engine, i.e. the gameplay and tools programmers, and present them with a consistent and easy to understand interface.

Write your code as if you are writing it for someone else. Which, in fact, you are.

# Context is Important

The rules and guidelines here derive from the tools we use, the architectures we work on, and the kind of problems we have to solve. There are situations where doing things the standard way may not be easy (say, on the SPU). If a rule or guideline makes it substantially more difficult to solve something, use your best discretion about how to resolve it, and let it be known so that this standard can reflect the experience.

# Stylistic Standards

Issues of style are in essence a matter of taste, and as such, are both arbitrary and subject to fruitless debate. That said a consistent set of aesthetic conventions helps readers – especially unfamiliar readers – read and understand code.  So some style elements are included, and are not subject for debate.  In general these reflect current practice.

## Namespaces

The public API for core (and non-core) services should be wrapped in an appropriate namespace, with the exception of the following Core APIs which are in the global namespace.

```
Foundation/Assert
Foundation/Color
Foundation/Common
Foundation/Container
Foundation/DataFile
Foundation/FileSystem
Foundation/Geometry
Foundation/Math
Foundation/Profile
Foundation/Time
```

Do not use the using keyword. All namespaces should be explicitly referenced, everywhere.

Namespaces must not be hierarchical, they should be one level deep only.

Functions in namespace scope in source files should be fully qualified, and not rely on being enclosed in a namespace.

```cpp
// System.h
namespace System
{
  void Function();
}
```

```cpp
// RIGHT

// System.cpp
#include "System.h"

void System::Function()
{
}
```

```cpp
// WRONG

// System.cpp
#include "System.h"

namespace System
{
  void Function()
  {
  }
}
```

## Naming Conventions

When choosing a name, prefer long names to abbreviated names. Prefer descriptive names to arbitrary ones.

We generally use a PascalCase convention for types, identifiers, and namespaces. In cases when a word is composed of acronyms, it is acceptable to either use all initials for the acronym portion, or PascalCase.

```cpp
namespace DDL // okay
{
  namespace ThreadLocal { ... }
}

namespace Ddl // also okay
{
  namespace ThreadLocal { ... }
}

namespace Ddl
{
  namespace THREADLOCAL { ... } // WRONG
}
```

Variables have a different naming convention depending on their scope:

### Local variables

- No leading underscores
- No trailing underscores

Note: this applies to function parameters as well.

`lower_case_underscores`


### Member variables

- Initial m_
- Use PascalCase
- No other underscores

`m_PascalCase`

### Type names (struct, class, enum)


- PascalCase
- No underscores.

`ModelInstance`

### Standard types

Use standard type definitions. e.g. uint32_t, uint16_t, size_t, etc. e.g. float, double, etc.

### Other

All variables outside of local-lifetime scope:

- leading indicator of scope
    - s_ for static scope (file static, class static, or function static)
    - g_ for global scope

- Use PascalCase

`s_PascalStatic`
`g_PascalGlobal`

### Enumerated values and constants

- Initial k
- PascalCase

`kPascalCase`

Enumerators must be scoped either in a namespace or class scope. They should not be "warted" in the C style.

```cpp
namespace Foo
{
  enum
  {
    kInit   = (1 << 0),
    kActive = (1 << 1)
  };
}
```

### Pointers

- The asterisk is grouped with the type, not the variable.

`float* a;`

- Do not typedef pointer types. This includes function pointer types.

```cpp
typedef int* int_pointer; //WRONG
int_pointer foo; // WRONG

int* foo; // RIGHT
```

- This includes function pointer types. Typedef of function signatures is fine.

```cpp
// RIGHT
typedef int (foo)(int, float);
foo* my_func;

// WRONG
int (*foo)(int, float);
foo my_func;
```

### CPP Macros

- All uppercase

`UPPERCASE_UNDERSCORES()`

### Namespaces

- PascalCase
- No underscores

### Source code file and directory names

- PascalCase
- No prefix (i.e., prefer PascalCase to igPascalCase)

NOTE: In no case should any name or label (for a variable, class, namespace, file, and so on) run words together without any kind of delineation (such as an underscore or a change in case according to the standards above).

### Whitespace

- Indents (C/C++/CG/etc.) should always be two spaces. NO TAB CHARACTERS EVER!
- You do not need to wrap lines. However, you may optionally wrap at about 100-characters.
- In assembly or microcode, space-align the first parameter of each block of instructions.
- A space should follow a comma in general (C/C++/CG/etc.)
- A space should not proceed a comma in general (C/C++/CG/etc.)
- The last character in a file should be a linefeed (C/C++/CG/etc.)

### Variable Declaration

- Do not use the comma operator to declare multiple variables on the same line. Declare them on separate lines.

```cpp
// WRONG
float* a, b;

// RIGHT
float* a;
float b;
```

### switch statements

```cpp
switch ()
{
  case x:
  {        <- Always use brackets. Even one liners.
    stuff
    break; <- With break before brackets.
  }
  <- If break is not desired, comment goes here.
}
```


# Coding Standard: Nomenclature

## Spelling

We use American English spelling throughout. So it is "Color" and not "Colour", "Serialize" and not "Serialise".

## Accessors

Accessors should start with "Set" or "Get". Exception: if an accessor reads the value of a bool, it may begin with "Is", or "Does", whichever reads more like natural English.

```cpp
void SetSpeed (float speed);
float GetSpeed() const;

void SetActive (bool active);
bool IsActive() const;

void SetSnapToGrid (bool snap);
bool DoesSnapToGrid() const;
```

## Opposites

### Create/Destroy

Of an object, where a C++ constructor is not appropriate. This is the case if an object can be re-created multiple times. Use this instead of placement new if possible. It makes the code clearer.

Create must return a success flag.

### Init/Shutdown

Used for systems and managers.

### Start/Stop

Start() is used to start something running, either synchronously or asynchronously, until Stop() is called. For example: a particle effect, a music track, a streaming system, or a timer.

### Suspend/Resume

For use between Start/Stop, to temporarily suspend that what is running.

### Begin/End

Used to bracket some kind of aggregation or definition, such as a triangle strip, command buffer, goal list.

### Enter/Exit

Of a state or mode.

### Add/Remove

An element in a collection.

### Open/Close

Of a data stream. Input/output, or between processes.

### Acquire/Release

Exclusive ownership of a resource. Acquire must return an error code.

# Coding Standards

## Use a struct for passive data carriers, a class for everything else

A struct may have associated constants, but lacks any functionality other than access to the data members. Field access is direct rather than through accessors. Methods should not provide behavior, they should only be used to set up the data members, e.g. constructor, destructor, Reset(), or Validate().

_Rationale_
This is to make a distinction between objects in the C++ sense (class) and data structures that aren't expected to be used in OOP fashion

## Data members of a struct must be public

A struct is used to conveniently tie together strongly related data, and it has no "moving parts". The need for accessors is minimal and it would reduce the convenience.

## Data members of a class must be private

All data members of a class must be accessed through accessors.

_Rationale_
Accessors allow a place for breakpoints, instrumentation, validation. They make it possible to change implementation without changing the interface. For example, you may want to replace a bool with a bit flag. They also allow you to run extra code when a value is changed. For example, you may want to set a flag to indicate that a change has occurred. Although you may not need any of these things at the time of initial implementation, you may need it later, or someone else may need it.

Note that this rule implies that class data members must not be protected.

The rationale for the use of accessors is not limited to the public interface, but also applies to inheritance. There should be exactly one point where a data member is accessed, and that is the accessors in the class where the data member is defined. If access to a data member must be restricted to derived classes, you can declare the accessors protected.

_Exceptions_
Member constants may be public.

Aggregates where a specific memory layout is required and instances are intended to be worked with in an aliased way may have public data members. For example, four-float vector objects should have public x, y, z, w.

## No friend declarations

All external work must be possible using the public interface. No friend functions.

## Constructors should not do any real work

A constructor should only be used to initialize member variables. It should do nothing that can fail. It should not have any side effects. A "side effect" is any change outside the object itself (ex: memory allocation (because it changes a heap, which is outside the object), acquisition of any resource, registration with a manager, updating a counter).

Real initialization is done in the [Create](#perform-object-initialization-in-create-or-trycreate) function.

_Rationale_
Since we don't use exception handling, it's not possible to handle errors in constructors. If an error occurs in a constructor, you end up with an invalid object.

_Exceptions_
For debugging purposes during development, it may be desirable to track construction and destruction of a particular class of objects. That usually involves the registration of the object in the constructor.

Classes that are specifically designed to use scope lifetime to invoke side-effect functions (such as profiling timers).

## Perform object initialization in Create() or TryCreate()

Create performs object initialization (in contrast to the constructor). Create does not return a success flag, the caller is not expected to deal with initialization failure.

TryCreate performs object initialization and returns whether or not that object was able to be initialized.

In cases where object initialization is reasonably expected to be able to fail and the caller is intended to handle that, provide TryCreate. Otherwise, provide Create.

## All destructors should be empty

The object must be deinitialized, memory freed, resources released, in the [Destroy()](#perform-object-clean-up-in-destroy) function, and not in the destructor. There is nothing for a destructor to do. However, the destructor is a good place for debug code to assert that [Destroy()](#perform-object-clean-up-in-destroy) has indeed been called, and all resources have been released.

_Exception_
Classes that are specifically designed to use scope lifetime to invoke side-effect functions (such as profiling timers).

## Perform object clean up in Destroy()

Objects should have an explicit Destroy method which performs the shutdown code matching that in Create (or TryCreate).

Do not put shutdown code in the object destructor, or in a method with a name other than Destroy.

## Integer scalars should be signed

Signed integers should be used unless you're relying on unsigned semantics explicitly or using an integer type in a non-numeric way (ex: using a uint32_t as a bit pattern, or set of bit flags, or relying on a specific representation to allow optimized transformations).

_Rationale_
Even though your index or counter may never be negative, you (or someone else) may want to test it for underflow, use it in an expression, subtract it from another index or counter or v.v. Also, unsigned integers don't mix well with signed integers. For example if a number of elements in an array is presented as an unsigned integer, any loop counter for it must be unsigned also. That would make it very hard to iterate backward. Unsigned integers have no benefit other than that they can represent values larger than 2,147,483,647. (If you need that kind of range, use int64_t)

## Only specify integer width on data members (and always do so then)

Where storage and value range of an integer scalar are not a concern, use native type int. In aggregates, use explicitly width.

- int32_t (etc) is preferred for data members.
- int is preferred for parameters, return values, and local variables.

_Rationale_
Specifying int32_t (etc) where plain int can be used restricts steps that a compiler can take to optimize the compiled code.

## Do not use enum types as data members

Do not use enum types as data members. Use an explicitly sized integer type instead.

_Rationale_
Enum types are of implementation dependent width. Their use as data members can lead to complications maintaining alignment and aggregate size across platforms.

## Parameters passed by reference must be const

Never use a reference parameter for output. Parameters that are used for output must be passed in by pointer.

Some programmers describe a reference as "a pointer that can't be NULL". If you must make sure that a pointer is not NULL, simply assert that it isn't.

_Rationale_
References can be confusing. They have value syntax but pointer semantics. On the caller's side, the code looks like you are passing the argument by value, therefore it should also behave like you are passing the argument by value.

## Function parameter order: output, update, input

Place output parameters on the left, followed by update parameters (i.e. those that are input as well as output), and put input parameters at the end.

```cpp
void DoFoo(char* output, const char* input0, int input1, int input2);
```

_Rationale_
This provides a predictable order for arguments.

## Header files must begin with #pragma once

This replaces the traditional #ifndef _FOO_INCLUDED_ include guards.

_Rationale_
It's supported on all our platforms and universally faster.

## Don't use #include if a forward declaration would suffice

If a particular header dependency can be fulfilled with a forward declaration instead of the full definition, use the forward declaration.

You can significantly minimize the number of header files you need to include in your own header files by using forward declarations. For example, if your header file uses the File class in ways that do not require access to the declaration of the File class, your header file can just forward declare class File; instead of having to #include "file/base/file.h".

Never include `<windows.h>` in a header. If you must include it in a source file, define WIN32_LEAN_AND_MEAN before including it.

_Rationale_
When you include a header file you introduce a dependency that will cause your code to be recompiled whenever the header file changes. If your header file includes other header files, any change to those files will cause any code that includes your header to be recompiled. Therefore, we prefer to minimize includes, particularly includes of header files in other header files.

_Exception_
Some D3D code required inclusion of d3d11.h, which includes windows.h.

Not an exception but a proviso that we are not using a [PIMPL](https://web.archive.org/web/20120106230448/http://en.wikipedia.org/wiki/Opaque_pointer) style interface. Use forward declarations when possible, but don't unnecessarily abstract an interface just to do so.

## Byte, Size, Count

When refering to the size of something in bytes, a variable or type name should contain the bytes. When referring to it in terms of another fundamental type name it explicitly in the variable name (words, dword, qwords).

When refering to the size of something in elements, a variable or type name should contain the count or cnt.

When needing to alias a pointer with an integer, use uintptr_t. Be aware that pointer widths are not uniform across the game and tools.

We follow the PowerPC 64 bit ABI conventions for talking word length. Specifically, a word is 4 bytes, double word is 8 bytes, and a quadword is 16 bytes. http://refspecs.linuxfoundation.org/ELF/ppc64/PPC-elf64abi-1.9.html#FUND-TYPE . Using the Win32 API convention is acceptable when using the Win32 API, in which case however you must use the appropriate typedefs (WORD, DWORD etc).

_Rationale_
It's important to maintain the distinction between the two (never use count to refer to the byte size of something, even byte-sized elements) to make the use of a variable obvious from its name. This also helps improve the discoverability of variables (to avoid having to guess whether the author used size or bytes.

## Singletons

When exposing a singleton, it should be explicitly constructed and its object globally accessible:

```cpp
class FooSingleton

{

  // ...

};

extern FooSingleton g_FooSingleton;
```

The public interface should be implemented as non-static member functions:

```cpp
class FooSingleton
{

  // ...

public:

  bool Init();

  void Update(float dt);

  bool Shutdown();

};

// ...

g_FooSingleton.Update(0.33f);
```

## Casting

- Use C-style casts. Do not use C++ style (static_cast, dynamic_cast, reinterpret_cast).
- Do not use void*. Use char* for untyped data.

_Rationale_
The brevity of the C-style cast outweighs the semantic benefits of explicitness of C++-style casts.

Data pointed through to char* is guaranteed to alias any other data type. Also, it avoids having to explicitly convert to a sized type when address arithmetic is required.

## No Booleans in aggregates

Do not use bool or an equivalent boolean type in an aggregate. Prefer a bit set in an integer type instead.

_Rationale_
It's rare for only one boolean state to be present on something. Generally we need to encode more than one. Also it encourages processing of elements where the boolean is continually checked. Also, bool types are of implementation dependent width. Their use as data members can lead to complications maintaining alignment and aggregate size across platforms.

## No booleans as function parameters

No bools in function parameter lists.

_Rationale_
Boolean function arguments hide important information in the calling code. They can almost always be expressed more clearly with explicit constants.

http://blogs.msdn.com/b/oldnewthing/archive/2006/08/28/728349.aspx

_Exception_
Really simple accessors can take one boolean argument.

```cpp
class foo
{
  uint32_t m_Flags;

  public:
  void SetBarEnabled(bool value)
  {
    m_Flags &= ~kBar;
    if (value)
      m_Flags |= kBar;
  }
};
```

## Booleans in local scope or as return values

Bools are acceptable in local scope.

Bools are acceptable return values, however they imply an unsorted data set and a branch at every caller. That should be carefully considered and fixed at the data design instead, where appropriate.

## C Bit fields

Don't use use C bit fields. For data that must be tightly packed, prefer explicit flags stored in integers or a higher-level structure (like a MemAllocBitSet) instead.

_Rationale_
The code generated from C bit fields is usually worse than explicit bit manipulation and the specific memory layout is implementation dependent.

## Memory and the CRT

Do not use malloc, calloc, memalign, or free. Do not use any new operator except for placement new. Use an Insomniac memory allocator dedicated for the purpose that you need memory or the stack.

Do not use functions which implicitly allocate memory using these functions if at all possible.

_Rationale_
We have custom allocators for different allocation patterns for performance, auditing, and fragmentation reasons. Use of the CRT memory allocators circumvents our memory allocation schemes and in most cases is a poorer alternative.

_Exceptions_
Some middleware will not offer the ability to override their memory allocators, or implicitly use CRT memory through libc functions.

## No control flow macros

Do not use macros to hide control flow logic, for example, FOREACH.

## Do not use named number constants

Don't use named number constants like kTwoFloat = 2.0f or kOneOverTen = .1f. Use the literal instead.

_Exceptions_
Named number constants for well known constants, or those with more than one significant digit, can be named. For example, M_PI.

## SPU/PPU aliased data structures

Structures which are operated on both the PPU and SPU should not have any virtual functions.

If they contain internal pointers, they should be encoded using the following convention:

- The member must be a uint32_t on the SPU, a typed pointer on the PPU
- The name must be the same, except Ea is appended to the end on the SPU

```cpp
#ifdef SPU
  uint32_t m_DataNameEa;
#else
  typed_data* m_DataName;
#endif
```

## Const correctness

Member functions should be declared const unless there is a reason to do otherwise. If it is possible to trivially rewrite a member function to allow it to be const, it should be.

Under no circumstances should the keyword 'mutable' be used.

## Conditionals require explicit braces

Use explicit braces with conditional blocks, even in cases with one-statement. This applies to if and while statements.

```cpp
if(foo)
{
  DoBar(); // Right
}

if (foo)
  DoBar() // WRONG
```

_Rationale_
It's possible for someone to mistake indentation for control flow and neglect to include a conditional statement in the right block.

## Header files must contain all their dependencies

Header files should contain all files required to include them (note: if the header is includable and generally compilable without including a header – say, through the use of a forward declaration – it is not necessary to include it). The user should be able to expect that if he wants to use a function declared in a header, he should be able to include just that file.

Additionally, if there is a corresponding source file (e.g. EditorAssetManager.cpp to EditorAssetManager.h), the source file should include that header first (after the precompiled header, if using precompiled headers). This mechanism helps enforce this rule.

```cpp
MemViewer.h:
#include "Foundation/Common/Common.h"
#include "Foundation/Common/Printf.h"

namespace MemViewer {
  // ...
}

MemViewer.cpp:
#include "Foundation/Common/Common.h"
#include "Foundation/Memory/MemViewer.h"
```

_Rationale_
This reduces the amount of work a user must do to start using an API by removing the need to discover dependencies. This also reduces the mechanisms for ensuring dependency satisfaction to one location (the header), making it easier to keep up to date and remove redundant includes.

# Best Practices

## Avoid "magic values"

Avoid overloading integer or float variables which take a range of values with a magic number. For example, having a number which represents a length of time with -1 meaning infinite.

_Rational_
It's generally not obvious that magic numbers of special significance. Also, they harm the discoverability of interfaces.

_Exceptions_
For things with discrete enumerated values, like ids, having a sentinel for "invalid" is okay, but keep make it an explicit constant. For example, the are encoding of DYN_JOINT_ID_INVALID (0xffffffff) in the old dynamic joint code is an appropriate use of sentinel values.

## Keep implementation details out of the public interface

Unless a detail is necessary for the use of the public interface, it should not be visible by a programmer using the interface.

_Rationale_
By presenting a concise interface, the user will be more likely to use it correctly, and the implementor will have more freedom to change internal implementation details without worrying about harming calling code.

## Non-trivial code should be kept out of headers

By default, code should not be in header files. It should be in source files.

_Rationale_
Maintaining code in header files instead of source files increases the number of files which must be recompiled. In addition, the extent to which the compiler can and will inline code is implementation and configuration dependent, which can result in multiple definitions across translation units which increases link time.

_Exceptions_
Code which is extremely trivial – simple accessors, for example – are acceptable in headers.

## Avoid negative flags

When possible, make the boolean value true equivalent to enable , or execute , or success . Avoid flags that have negative meanings, where boolean value true means "disable", "skip", or "failure".

_Rationale_
Negative logic harms readability.

## Consider using a struct to return multiple items

Some functions need to return more than one item. For example, a pointer and a count value. Although it is acceptable to place a return value at an address that is passed in an an argument, it is more explicit to define a struct for the purpose.

```cpp
// Acceptable:
const Vec3* GetPoints( int* result_count ) const;

// Better:
struct PointsResult
{
 const Vec* points;
 int32_t    count;
};
PointsResult GetPoints() const;
```

## Prune commented-out and unused code

Don't leave large blocks of code commented out in your source files. Also, if a function or group of functions are no longer being used, remove them. You can always rely on the perforce revision history to see what the file used to contain.

This improves the readability of code and reduces the amount which must be examined when debugging.

## Compile without warnings

Generally speaking, your code shouldn't have warnings. You should make every effort to change the offending code until it compiles and links without warnings.

_Exceptions_
If you believe a warning to be spurious, it may be acceptable to turn it off under certain circumstances. Before you do please talk to someone who knows about these things.

When using middleware, it may be unavoidable to avoid warnings. It may be possible to suppress the warnings before including code via header, you should make the effort to do so if necessary.

## Add comments identify #else/#elif/#endif statements

Any #endif, #else or #elif statement associated with a #if or #ifdef statement should be commented with the relevant condition unless it is extremely obvious.

The first case in this example shows use of comments, the second a case where comments are not necessary.

e.g.:
```cpp
#if defined(__PS3__)
#if defined(_DEBUG)
   DoSomethingPS3();
#endif // _DEBUG

   // code elided

#endif // __PS3__

// trail
#if defined(__XBOX__)
   DoSomethingXbox();
#endif
```

# Further Reading

More reading for more solid, readable C++ code can be found in the following publications.

- [The Practice of Programming – Kernigan, Pike](https://web.archive.org/web/20120106230448/http://amzn.com/020161586X)
- [Google C++ Style Guide](https://web.archive.org/web/20120106230448/http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml)
