## 介绍
ESDoc 是一个 JavaScript 文档生成器，按照规范编写代码注释，即可生成友好的 JavaScript 代码文档。

## 应用场景
目前，我们前端团队在开发通用组件（React 和 Vue）、工具和类库等时，强制要求按照 ESDoc 规范编写注释，便于团队其他成员快速阅读和使用，减少沟通成本。

## 尝试
把自己的代码贴进来试试：https://try.esdoc.org/ 。

## 参考
- https://esdoc.org/
- https://esdoc.org/manual/usage/tags.html

## 类似的东西
- [JSDoc](http://usejsdoc.org/index.html)

## @param、@return 特别说明
@return 后面的 {...} 首字母需大写的情况：
- return 的是某个对象（如：String、Person、Array、Object 等）的实例；
- return 的是一个引用类型数据（如：return []、return {}、return function () {} 等）；
> function getString 例子，@return 后面的 {string} 和 {String} 首字母有大小写之分，这是因为 new String('abc') 是 new SomeObject() 形式，返回的是 String 对象的一个实例。
```js
/**
 * 返回字符串
 * @return {string}
 */
function getString () {
  return 'abc'
}

/**
 * 返回 String 的实例
 * @return {String}
 */
function getString () {
  return new String('abc')
}

/**
 * 返回 Object 的实例
 * @return {Object}
 */
function getObject () {
  return new Object()
}

/**
 * 返回函数
 * @return {Function}
 */
function getFunction () {
  return function () {
  }
}

/**
 * 返回数组
 * @return {Array}
 */
function getArray () {
  return []
}

/**
 * 返回 Person 的实例
 * @return {Person}
 */
function getPerson () {
  return new Person()
}
```

## 比较完整的例子
```js
/**
 * @deprecated 该类已弃用，请用 Animal 代替
 */
class MyAnimal {
  // MyAnimal 的实现代码
}

/**
 * 一个关于动物的类
 * 如果你想了解关于人的类的详情，请参考 {@link Person}
 * @author 赵金添 <729234283@qq.com>
 * @see https://github.com/zhaotoday/esdoc
 * @todo 需要完善某些功能
 * @example
 * const dog = new Animal()
 */
class Animal {
  /**
   * 构造方法
   * @param {string} [name=''] 名字
   * @param {number} [age=0] 年龄
   * @param {string[]} [abilities=[]] 拥有的能力
   */
  constructor ({name = '', age = 0, abilities = []}) {
    /**
     * 名字
     * @type {string}
     */
    this.name = name

    /**
     * 年龄
     * @type {number}
     */
    this.age = age

    /**
     * 拥有的能力
     * @type {string[]}
     */
    this.abilities = abilities

    /**
     * 拥有的腿的数量
     * @type {number}
     */
    this.legs = 4

    /**
     * 朋友
     * @type {Object}
     * @property {number} friend.name 名字
     * @property {string} friend.age 年龄
     */
    this.friend = {
      name: 'chen',
      age: 30
    }
  }

  /**
   * 获取
   * @type {string}
   */
  get value () {
    return this.name
  }

  /**
   * 设置
   * @type {string}
   */
  set value (name) {
    this.name = name
  }

  /**
   * 吃饭方法（该方法必须被子类重写）
   * @abstract
   */
  eat () {
  }
}

/**
 * 一个关于人的类，继承自 Animal 类
 * @extends {Animal}
 * @example
 * const person = new Person({
 *   name: 'zjt',
 *   age: 29,
 *   abilities: ['eat', 'speak', 'run']
 * })
 */
class Person extends Animal {
  /**
   * 财产
   * @type {number}
   */
  _money = 100

  /**
   * 吃饭方法（重写了父类的 eat 方法）
   * @override
   */
  eat () {
    console.log('I eat food.')
  }

  /**
   * 获取他说的话
   * @param {string} [words=''] 话
   * @return {string}
   */
  getWords (words = '') {
    return `${this.name} said: ${words}`
  }

  /**
   * 获取人的信息
   * @return {Object}
   * @property {string} name 名称
   * @property {number} age 年龄
   */
  getInfo () {
    return {
      name: this.name,
      age: this.age
    }
  }

  /**
   * 设置人的信息
   * @param {string} name 名称
   * @param {number} [age=10] 年龄
   */
  setInfo ({name, age = 10}) {
    this.name = name
    this.age = age
  }

  /**
   * 添加能力
   * @param {...string} abilities 欲添加的能力
   */
  addAbilities (...abilities) {
    this.abilities.push(...abilities)
  }

  /**
   * 获取财产
   * @return {number}
   */
  _getMoney () {
    return this._money
  }
}

// 创建 person 对象
const person = new Person({
  name: 'zjt',
  age: 29,
  abilities: ['eat', 'speak', 'run']
})

person.name = 'zhaojintian'
person.addAbilities('sing', 'ask')
console.log(person.getWords('Hello.'))
console.log(person)
```
