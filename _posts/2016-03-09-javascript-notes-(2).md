---
layout: post
title:  "JavaScript Notes (2)"
date:   2016-03-10 01:47:38 
categories: programming-notes
tags: 
- javascript-programming
comments: true
identifier: 000000000110
language: english
---

After some basic knowledge, I will read some books and gather some useful tips for future reference. 

## JavaScripts: The Good Part


### Object

Number, String, Bool, null and undefined are not objects. JavaScript Object are class-free. They look like a python dictionary.

#### Retrieval

"||" can be used to initialize value


    var middle = storage['middle-name'] || "(none)";
    // if storage['middle-name'] is undefined, middle = "(none)"
    var status = flight.status || "unknown";
    // if flight.status is undefined, status = "unknown"


"&&" can be used to look up an undefined value without TypeError


    flight.equipment                           // undefined
    flight.equipment.model                     // throw "TypeError"
    fllght.equipment && flight.equipment.model // undefined


### Reference

object is always refered not copied.


    var a = {}, b = {}, c = {};   // a, b, c are three different empty objects
    var a = b = c = {};           // a, b, c all refers to the same empty object


### Prototype


    if (typeof Object.beget !== 'function') {
        Object.beget = function (o) {
            var F = function () {};
            F.prototype = o;
            return new F();
        };
    }
    var another_stooge = Object.beget(stooge);  // heritage from prototype stooge


### Global Abatement

Only create a single global variable to avoid various issues.


    var MYAPP = {};
    MYAPP.variables = {
        "first-name": "Joe",
        "last-name": "Howard"
    };


Make MYAPP as a variable container.


## Functions

### Invocation Pattern

**The Method**

this binds to the owner object

**The Function**

this binds to global variable instead of the owner object which is a bad design. Do the below to avoid.


    myObject.double = funcion () {
        var that = this;
        var helper = function () {
            that.value = add(that.value, that.value); // this does not work here
        };
        helper();
    };


**The Constructor**

with a new in front of the constructor, this will bind to the new object.


    var Quo = function (string) {
        this.status = string
    };

    var myQuo = new Quo("confused"); // do not forget "new"


This is actually not a very good way to make a constructor.

**The Apply**

apply will take an owner object as parameter too.


    var sum = add.apply(null, [3, 4]); // null will be assigned to this

### Augmenting Types

Add method to Function.prototype to make this method available to all functions.


    Function.prototype.method = function (name, func) {
        this.prototype[name] = func;
        return this;
    }; // this is not a function defination, so a ';' is needed
    // Function.prototype.method = an anonymous function;
    // this function add a method to the owner object

    Number.method('interger', function () {
        return Math[this < 0 ? 'ceiling' : 'floor'](this);
    });

    document.writeln((-10 / 3).integer()); // -3