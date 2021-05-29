# Reference VS Primitive Values

## # What are Primitives?

```js
    var age= 28
    var name ='Max'
    var isMale=true
```

- The **age** variable( you could also use let or const by the way ) stores a number value. The number **28**.
- Number  values are called "primitive values" because they're very simple building blocks of JavaScript apps.
- So number, string and boolean - these are probably very well-known to you. **undefined** and **null** are additional primitive types.

## # What are Reference Types Then?

- So we learned what "Primitives" ( or "primitive types") are.
- What are "reference types" then?
  - Objects And Arrays!

```js
    var person = {
        name:'Max',
        age:28,
    }

    var hobbies = ['Sports','Cooking']
```

- Here **person** is a object and therefore a so-called reference type. Please note that it holds properties that in turn have primitive values. This doesn't affect the object being a reference type though. And you could of course also nested objects or arrays inside the **person** object.
- The **hobbies** array is also a reference type - in this case, it holds a list of strings. A **string** is a primitive value/types as you learned but this doesn't affect the **array**. Arrays are **always** reference types.

## # What's the Difference?

- Cool, we got two difference types of values. What's the idea behind all of that?
- It's related to memory management.
- Behind the scenes, JavaScript of course has to store the values you assign to properties or variable in memory.
- JavaScript knows two types of memory: The **Stack** and the **Heap**.
- Here's a super-short summary: The stack is essentially an easy-to-access memory that simply manages its items as a-well-stack. This is the case of numbers, strings, booleans.
- The heap is a memory for items of which you can't pre-determine the exact size and structure. Since objects and arrays can be mutated and change at runtime,they have to go into the heap therefore.
- Obviously, there's more to it but this rough differentiation wil do for now.
- For each heap item, the exact address is stored in a pointer which points at the item in the heap. This pointer in turn is stored on the stack. That will become import in a second.

<p align="center">
  <img src="https://user-images.githubusercontent.com/30569818/120061612-40317380-c088-11eb-9b69-e6ce66ba6ed8.png">
</p>

- Okay, so we got different memories. But how does that make a difference to us, the developer?

### # Strange Behavior of "Reference Types"?

- The fact that only pointers are stored on the stack for reference types matters a lot!
- What's actually stored in the **person** variable in the following snippet?

```js
    var person = {name: 'Max'}
```

- Is it:
  - The object ( { name:'Max' } )
  - The pointer to the object
  - A pointer to the name property?
- It's b). A pointer to the person object is stored in the variable. The same would be the case for the hobbies array.
- What does the following code spit out then?

```js
    var person = { name: 'Max' }
    var newPerson = person
    newPerson.name = ' Anna '
    console.log(person.name) // What does this line print?
```

- You'll see **'Anna'** in the console
- Why?
- Because you never copied the person object itself to **newPerson**. You only copied the pointer! It still points at the same address in memory through. Hence changing **newPerson.name** also change **person.name** because newPerson points at the exactly same object!
- This is really important to understand! You're pointing at the same object, you didn't copy the object.
- It's the same for arrays

```js
    var hobbies = ['Sports', 'Cooking']
    var copiedHobbies = hobbies
    copiedHobbies.push('Music')
    console.log(hobbies[2]) // What dows this line print?
```

- This prints **'Music'** - for the exact same reason as stated above.

### # How can you copy the actual Value?

- Now that we know that only the pointer - how can we actually copy the value behind the pointer? The actual object or array?
- You basically need to construct a new object or array and immediately fill it with the properties or elements of the old object or array.
- You got multiple ways of doing this - also depending on which kind of JavScript version you are using(during developmennt)

