# JavaScript 类的写法

1. 拥有私有方法的类示例：

  ```javascript
  var Person = (function() {

    var sayHello;

    // 构造函数
    function Person() {}

    // 这是一个私有方法（Private Method）
    sayHello = function(to) {
      return console.log("Hello, " + to + ".");
    };

    // 这是一个实例方法（Instance Method）
    Person.prototype.helloWorld = function() {
      return sayHello("world");
    };

    return Person;

  })();
  ```

2. 拥有类方法和类字段的类示例：

  ```javascript

  var Songs = (function() {

    // 这是一个类字段（Class Field）；
    Songs._titles = 0;

    // 这是一个类方法（Class Method），可不经实例化直接调用。
    Songs.getCount = function() {
      return this._titles;
    };

    // 构造函数
    function Songs(artist, title) {
      // 属性（Property）
      this.artist = artist;
      this.title = title;

      // 类字段均通过实例的 constructor 的属性访问
      this.constructor._titles++;
    }

    return Songs;

  })();
  ```

3. 如何在私有方法中操作对象属性：

  ```javascript
  var Sorcerer = (function() {

    var conjureSpell;

    conjureSpell = null;

    function Sorcerer(spell) {
      this.spell = spell;

      conjureSpell = (function(_this) {
        return function() {
          return _this.spell.conjure();
        };
      })(this);
    }

    Sorcerer.prototype.useSpell = function() {
      conjureSpell();
      return this.spell.use();
    };

    return Sorcerer;

  })();
  ```
