# 06 Prototype

[π« λμκ°κΈ°](https://github.com/Chocobe/-Study-Javascript-ES5-2021)

<br/>

## 1. μμ±μ ν¨μ ``constructor()``

Javascript μ ``new`` ν€μλλ₯Ό μ¬μ©ν κ°μ²΄ μμ±μ ``constructor()`` λΌλ ``μμ±μ`` λ©μλκ° λ§λ€μ΄ λ°ννλ μλ‘μ΄ κ°μ²΄ μλλ€.

μμ±λ κ°μ²΄μμ λ°λΌλ³Ό λ, ``constructor()`` μ κ²½λ‘λ ``κ°μ²΄.__proto__.constructor()`` μ§λ§, ``__proto__`` κ²½λ‘λ₯Ό μλ΅νκ³  μ κ·Όνμ¬λ μ μ μ κ·Όμ΄ κ°λ₯ν©λλ€.

κ°μ²΄μ νΉμ  νλ‘νΌν°μ μ κ·Όνμ λ, μκΈ° μμ μκ² μλ€λ©΄, ``Prototype`` μ μ°Έμ‘°κ°μ²΄μμ μ°ΎκΈ° λλ¬Έμ, ``__proto__`` κ²½λ‘λ₯Ό μλ΅ν΄λ, μμ μ ``constructor`` μ μ κ·Όν  μ μλ κ²μλλ€. (super κ°μ²΄ μ κ·Ό λ°©μ)

``constructor`` λΏλ§ μλλΌ, ``Prototype`` μ μ μν ``λ©μλ`` , ``λ³μ`` λͺ¨λ ν΄λΉ λ©λλ€.

<br/>

μμ±μ ν¨μλ₯Ό μ¬μ©νμ¬ κ°μ²΄λ₯Ό μμ±νλ©΄, λ€μκ³Ό κ°μ΅λλ€.

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.getOld = function() {
  console.log(this.age);
}

const kim = new Person("kim", 35);
```

<br/>

``Person(name, age)`` ν¨μ μμμμ ``this`` λ ``new`` ν€μλλ‘ μ¬μ©νκ² λμ΄, ``this === μλ‘ μμ±λ  κ°μ²΄`` κ° λ©λλ€.

κ·Έλ¦¬κ³  μμ±μ ν¨μλ‘ μ¬μ©ν ``Person(name, age)`` ν¨μλ ``constructor()`` ν¨μκ° λ©λλ€.

``kim`` κ°μ²΄λ₯Ό λμν νλ©΄ λ€μκ³Ό κ°μ΅λλ€.

```bash
kim
  βββ name
  βββ age
  βββ __proto__
        βββ constructor()
        β     === function Person(name, age)
        β
        βββ __proto__
              βββ Object()
```

<br/>

μ λμμμμ ``constructor()`` λ ``__proto__`` κ°μ²΄ μμ μμ΅λλ€.

νμ§λ§, ``constructor()`` μ μ κ·Όν  λλ ``__proto__`` λ₯Ό μλ΅ ν  μ μμΌλ―λ‘, λ€μκ³Ό κ°μ΄ μ κ·Όν  μλ μμ΅λλ€.

```javascript
kim.constructor()
=== kim.__proto__.constructor()
```


<br/><br/>


## 2. ``prototype`` μ λ©μλ λ±λ‘

μμ±μ ν¨μμ ``__proto__`` νλ‘νΌν°λ₯Ό ν΅ν΄ ``prototype`` μ μ κ·Όν  μ μμ΅λλ€.

μ΄ ``prototype`` μ νλ‘νΌν°λ‘ λ©μλλ₯Ό μΆκ°ν  μ μμ΅λλ€.

```javascript
function Persion(name, age) {
  this.name = name;
  this.age = age;
}

// Person μμ±μ ν¨μμ Prototype μ "getOld()`` λ©μλ ννμ μΆκ°
Person.__proto__.getOld = function() {
  return this.age;
}
```

<br>

μμ κ°μ΄ ``Prototype`` μ μΆκ°λ νλ‘νΌν°λ, ``λμΌν μμ±μ`` λ₯Ό μ¬μ©νμ¬ μμ±ν κ°μ²΄λ€μκ²λ ``λͺ¨λ μ μ©`` λ©λλ€.

μ΄μ λ λμΌν ``μμ±μ ν¨μ (constructor())`` λ₯Ό μ°Έμ‘°νκ³  μκΈ° λλ¬Έμλλ€.

<br/>

``Prototype`` μ ``λ©μλ νλ‘νΌν°`` λ₯Ό μΆκ°νμ¬ μ¬μ©ν  κ²½μ°, μ£Όμν  μ μ΄ μμ΅λλ€.

1. ``Prototype`` μ μΆκ°ν ``λ©μλ νλ‘νΌν°`` μ λ΄λΆμμ μ¬μ©νλ ``this`` λ νΈμΆμμ λ°λΌ ``κ°μ²΄κ° λ¬λΌμ§λλ€`` (Execute Context)

    ```javascript
      function Person(name, age) {
        this.name = name;
        this.age = age;
      }

      Person.__proto__.getOld = function() {
        return this.age;
      }

      // ``new`` ν€μλμ μν΄, age λ kimκ°μ²΄μ νλ‘νΌν°
      const kim = new Person("kim", 35);

      // μ€ν μ»¨νμ€νΈκ° kim κ°μ²΄μ΄λ―λ‘, this === kimκ°μ²΄
      console.log(kim.getOld()); // 35 μΆλ ₯

      // μ€ν μ»¨νμ€νΈκ° kim.__proto__ κ°μ²΄μ΄λ―λ‘, this === kim.__proto__
      // kim.__proto__ κ°μ²΄μλ ``age νλ‘νΌν°κ° μμ``
      console.log(kim.__proto__.getOld()) // undefined μΆλ ₯
    ```

2. ``ν¨μ ννμ`` μ΄λ―λ‘, ``Hoisting`` μ΄ ``μ μ©λμ§ μμ΅λλ€``

    ```javascript
      function Person(name, age) {
        this.name = name;
        this.age = age;
      }

      const kim = new Person("kim", 35);

      console.log(kim.getOld()); // μλ¬λ°μ μμΉ

      Person.__proto__.getOld = function() {
        return this.age;
      }

      console.log(kim.getOld()); // μ μλμ μμΉ
    ```