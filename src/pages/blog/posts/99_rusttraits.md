---
titulo: "Rust traits blew my mind"
id: '99_rusttraits'
descricao: "A quick talk about traits in Rust and how they compare to interfaces in Java."
layout: ../../../layouts/PostLayout.astro
---

I like OOP. Really. Java was my favorite language for a short while, and it's way of enforcing OOP was one of the selling points to me. It's curious how i never thought about what i was doing (not that i had done anything complex). I just followed the same project structure, patterns and conventinons i learned from an Udemy course and that was it: my new Spring Boot API was ready. Java can be verbose, but the ecosystem is incredible, and the language is very mature. I still like it, but...

<h2 className="text-2xl font-bold mt-9 mb-9"> ...the feeling that you could do better is always there.</h2>

I really like to learn new things and search for the absolute "best" way to do stuff. Often, the "best" way doesn't exist, but a "better" way always does. This search lend me to the Rust world, where i discovered about traits.

<h2 className="text-2xl font-bold mt-9 mb-9">A glorified interface.</h2>

Traits are a way to define a set of methods that a type must implement. It's like an interface, but with a lot more power:

<br>

```rust	

    // The trait

    trait Animal {
        fn make_sound(&self);
    }

    // The type definitions

    struct Dog {
        name: String
    }

    struct Cat {
        name: String
    }

    // The implementations

    impl Animal for Dog {
        fn make_sound(&self) {
            println!("{} says: Woof!", self.name);
        }
    }

    impl Animal for Cat {
        fn make_sound(&self) {
            println!("{} says: Meow!", self.name);
        }
    }


```

<br>
This is similar to the classic OOP example where you have a base class Animal and two subclasses Dog and Cat. The difference is that in Rust, you can implement the trait for any type, even if you don't own it.
<br />
<br />

```rust

    impl Animal for i32 {
        fn make_sound(&self) -> &'static str {
            println!("i32!");
        }
    }


```


<br />

Without having to create any kind of wrapper, i was able to extend the functionality of an existing type (and i don't even own it!). Here i used an i32, but it could be a type from a third party library. You get all the benefits from interfaces, but with a lot more flexibility.

<br>
 This can't be done in Java, for example, because the only way to add methods to a class is by implementing it on the class definition.
<br>
<br />


```java

    //you can only implement it when you define the class
    class Dog implements Animal { 
        public void makeSound() {
            System.out.println("Woof!");
        }
    }


```
<br>
But you usually don't have access to the source code of the classes you use (and even if you do, it's usually better to keep it the way it is), so you can't implement interfaces on them. 

<h2 className="text-2xl font-bold mt-9 mb-9">Conclusion.</h2>

 Rust is punching me on the face a lot (i'm still learning how to punch back), but those little differences from other languages really make it stand out. I hope you enjoyed this post, and if you have any questions or suggestions, feel free to contact me. Let's talk about C# or idk.