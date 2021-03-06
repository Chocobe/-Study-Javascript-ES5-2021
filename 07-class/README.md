# 07 class

[π« λμκ°κΈ°](https://github.com/Chocobe/-Study-Javascript-ES5-2021)

<br/>

κ°μ²΄μ§ν₯ μΈμ΄μ ``Class`` λ¬Έλ² νμμ, Javascript μ ``Prototype`` μΌλ‘ λμΌνκ² λ§λ€ μ μμ΅λλ€.

``Prototype`` μΌλ‘ ``Class`` μ²λΌ λ§λ€κΈ° μν΄μλ κ΅¬νν΄μΌν  λΆλΆλ€μ΄ μμ§λ§, μ΄λ¬ν λΆλΆμ ``class`` ν€μλλ‘ κ°νΈνκ² λ§λ€ μ μμ΅λλ€.


<br/><br/>


## 1. ``class``

μμ±ν ``class`` λ₯Ό μ¬μ©νμ¬ κ°μ²΄λ₯Ό μμ±ν  μ μμ΅λλ€.

λ€μμ ``class`` μμ± λ° κ°μ²΄ μμ± λ°©λ² μλλ€.

```javascript
// class λ¬Έλ²
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  getInfo() {
    return `${this.name}: ${this.age}`;
  }
}

const kim = new Person("kim", 35);
console.log(kim.getInfo()); // "kim: 35" μΆλ ₯
```


<br/>

λ€μμ ``Prototype`` μΌλ‘ λμΌν κ°μ²΄λ₯Ό μμ±ν λ°©λ² μλλ€.

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.getInfo = function() {
  return `(proto) ${kim.getInfo()}`;
}

const kim = new Person("kim", 35);
console.log(kim.getInfo()); // "(proto) kim: 35" μΆλ ₯
```

|classλ‘ κ°μ²΄ μμ±|prototype μΌλ‘ κ°μ²΄ μμ±|
|:---:|:---:|
|<img src="./assets/class_01.png" width="500px"><br/>|<img src="./assets/class_02.png" width="500px"><br/>|


<br/><br/>


## 2. μμ

μμμ΄ μλ λ¨μΌ ``class`` λ ``prototype`` κ³Ό λμΌ νμμ΅λλ€.

νμ§λ§, ``prototype`` μΌλ‘ ``class`` μ λμΌνλλ‘ κ΅¬ννλ €λ©΄ λ€μκ³Ό κ°μ μ²λ¦¬κ° νμ ν©λλ€.
  1. ``λΆλͺ¨ class`` μ ν΄λΉνλ ``(λΆλͺ¨)μμ±μ ν¨μ`` μμ±
  2. ``μμ class`` μ ν΄λΉνλ ``(μμ)μμ±μ ν¨μ`` μμ±
  3. ``(λΆλͺ¨)μμ±μ ν¨μ`` μ ``(μμ)μμ±μ ν¨μ`` λ₯Ό μ°κ²° μν€κΈ° μν ``(μ€κ°)μμ±μ ν¨μ`` μμ±

<br/>

μ μ²λ¦¬κ° νμν μ΄μ λ, μμ±λ κ°μ²΄μ Propertyκ° ``class`` λ¬Έλ²κ³Ό λ¬λ¦¬ ``super`` ν€μλλ‘ Parameter λ₯Ό λκ²¨μ€ μ μκΈ° λλ¬Έμλλ€.

``Prototype`` μ μμ νμ§ μκ³ , μμννλ₯Ό μμ±νλ©΄, μμ λ°μ κ°μ²΄(λΆλͺ¨κ°μ²΄)μ ``μλͺ»λ Property`` κ° μκΈ°κ² λ©λλ€.

```javascript
// Person μμ±μ ν¨μ μ μΈ
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.getInfo = function() {
  return `${this.name}, ${this.age}`;
}

// Developer μμ±μ ν¨μ μ μΈ
function Developer(name, age, language) {
  this.name = name;
  this.age = age;
  this.language = language;
}

// Person μ μμλ°μ ν¨κ³Όλ₯Ό μν΄, Developer.prototype μ Personμ instanceλ₯Ό λμ
Developer.prototype = new Person();

// Developer μ μλ μμ±μ ν¨μλ₯Ό Developer λ‘ μμ 
Developer.prototype.constructor = Developer;

// Developer μ λ©μλ μμ±
Developer.prototype.getLanguage = function() {
  return this.language;
}

const kim = new Developer("kim", 35, "Javascript");

console.log(kim.getInfo());
console.log(kim.getLanguage());
console.log(kim);
```

<br/>

μ μμ λ₯Ό λΈλΌμ°μ μμ μ€ν μν€λ©΄ λ€μκ³Ό κ°μ κ²°κ³Όλ₯Ό μ»κ² λ©λλ€.

<img src="./assets/class_03.png"><br/>

<br/>

μ κ²°κ³Όμμ μμλ°μ λΆλͺ¨ κ°μ²΄μ ``name`` κ³Ό ``age`` λ₯Ό μ κ±°λ μνλ‘ ``Developer`` μ ``prototype`` μ λμλλλ‘ μμ ν΄μΌ ``κ°μ²΄μ§ν₯μ class`` λ₯Ό (μ μ¬)κ΅¬νν  μ μμ΅λλ€.

μ΄λ₯Ό κ΅¬ννκΈ° μν΄, λ€μκ³Ό κ°μ κ³Όμ μ μΆκ°ν΄ μ€λλ€.
1. Person μ λ΄λΆλ‘μ§μ μ μΈν, ``Person μ prototype`` λ§ κ°μ§λ ``μλ‘μ΄ μμ±μ ν¨μ`` μμ± (ExtendsBridge)
2. Developer μ prototype μ ``Person`` μ instance λμ ,  ``ExtendsBridge`` μ instance λ₯Ό λμ

<br/>

μλ μ½λλ μμμ κ΅¬νν μ΅μ’ μ½λ μλλ€.

```javascript
// Person μμ±μ ν¨μ μ μΈ
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.getInfo = function() {
  return `${this.name}, ${this.age}`;
}

// class μμμ (μ μ¬)κ΅¬ννκΈ° μν μ€κ°μ²λ¦¬μ© ``μμ±μ ν¨μ`` μ μΈ (Propertyλ₯Ό κ°μ§μ§ μμ)
function ExtendsBridge() {}
// ExtendsBridge λ Personμ Property λ κ°μ§μ§ μκ³ , prototype λ§ λμΌ
ExtendsBridge.prototype = Person.prototype;

// Person μ μμλ°μ μμ μμ±μ ν¨μ μ μΈ
function Developer(name, age, language) {
  this.name = name;
  this.age = age;
  this.language = language;
}

// Developer μ prototype μ ExtendsBridge instance λ‘ λμ
Developer.prototype = new ExtendsBridge();

// Developer μ μλ μμ±μ ν¨μλ₯Ό Developer λ‘ λ€μ μ§μ 
Developer.prototype.constructor = Developer;

// Developer μ λ©μλ μ μ
Developer.prototype.getLanguage = function() {
  return this.language;
}

const kim = new Developer("kim", 35, "Javascript");
console.log(kim.getInfo());
console.log(kim.getLanguage());
console.log(kim);
```

<br/>

μ μ½λλ₯Ό λΈλΌμ°μ μμ μ€ν μν€λ©΄, λΆλͺ¨ κ°μ²΄μ ``name`` κ³Ό ``age`` κ° κΉλνκ² μ κ±°λ μνλ₯Ό λ³Ό μ μμ΅λλ€.

<img src="./assets/class_04.png"><br/>


<br/><br/>


## 3. ``class`` μ ``prototype`` μ μμ λΉκ΅

μ§κΈκΉμ§μ ``class`` μ ``prototype`` μ μμμ νλμ λΉκ΅ν΄ λ³΄λ©΄ λ€μκ³Ό κ°μ΅λλ€.

<br/>

<details>
<summary>classμ μμ μ½λλ³΄κΈ°</summary>

```javascript
// λΆλͺ¨ class μμ±
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  getInfo() {
    return `${this.name}, ${this.age}`;
  }
}

// μμ class μμ±
class Developer extends Person {
  constructor(name, age, language) {
    super(name, age);
    this.language = language;
  }

  getLanguage() {
    return this.language;
  }
}

const kim = new Developer("kim", 35, "class μμ");

console.log(kim.getInfo());
console.log(kim.getLanguage());
console.log(kim);
```
</details>

<br/>

<details>
<summary>prototypeμ μμ μ½λλ³΄κΈ°</summary>

```javascript
// λΆλͺ¨ μμ±μ ν¨μ μ μΈ
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.getInfo = function() {
  return `${this.name}, ${this.age}`;
}

// λΆλͺ¨ property λ₯Ό μ λ¦¬νκΈ° μν λ€λ¦¬μ­ν  μμ±μ ν¨μ μ μΈ
function ExtendsBridge() {}

ExtendsBridge.prototype = Person.prototype;

// μμ μμ±μ ν¨μ μ μΈ
function Developer(name, age, language) {
  this.name = name;
  this.age = age;
  this.language = language;
}

// μμ μμ±μ ν¨μμ prototype μ λ€λ¦¬μ­ν  μμ±μ ν¨μμ instance λ‘ λ³κ²½
Developer.prototype = new ExtendsBridge();

// μμ μμ±μ ν¨μμ constructor λ₯Ό μλ μμ μ constructor λ‘ λ³΅κ΅¬
Developer.prototype.constructor = Developer;

Developer.prototype.getLanguage = function() {
  return this.language;
}

const kim = new Developer("kim", 35, "Javascript");

console.log(kim.getInfo());
console.log(kim.getLanguage());
console.log(kim);
```
</details>

<br/>

|class μμ|prototype μμ|
|:---:|:---:|
|<img src="./assets/class_05.png" width="500px">|<img src="./assets/class_06.png" width="550px">|