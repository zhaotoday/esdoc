## 介绍
ESDoc 是一个 JavaScript 文档生成器，按照规范编写代码注释，即可生成友好的注释文档。

## 参考
- https://esdoc.org/
- https://esdoc.org/manual/usage/tags.html

## 举个栗子
```js
/**
 * 一个关于动物的类
 * 如果你想了解关于人的类的详情，请参考 {@link Person}
 * @see https://github.com/zhaotoday
 * @todo 需要完善某些功能
 * @example
 * const dog = new Animal()
 */
class Animal {
  /**
   * 构造方法
   * @param name {string} 名字
   * @param age {number} 年龄
   * @param abilities {string[]} 拥有的能力
   */
  constructor(name, age, abilities) {
    this.name = name
    this.age = age
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
      name: 'zhao',
      age: 30
    }
  }

  /**
   * 获取
   * @type {string}
   */
  get value() {
    return this.name
  }

  /**
   * 设置
   * @type {string}
   */
  set value(name) {
    this.name = name
  }

  /**
   * 吃饭方法（该方法必须被子类重写）
   * @abstract
   */
  eat() {
  }
}

/**
 * 一个关于人的类，继承自 Animal 类
 * @extends {Animal}
 */
class Person extends Animal {
  /**
   * 吃饭方法
   * @override
   */
  eat() {
    console.log('I eat food.')
  }

  /**
   * 获取他说的话
   * @param {string} [words = ''] 话
   * @return {string}
   */
  getWords(words = '') {
    return `${this.name} said: ${words}`
  }

  /**
   * 获取人的信息
   * @return {Object}
   * @property {string} name 名称
   * @property {number} age 年龄
   */
  getInfo() {
    return {
      name: this.name,
      age: this.age
    }
  }

  /**
   * 设置人的信息
   * @param {Object} param
   * @param {string} param.name 名称
   * @param {number} [param.age = 10] 年龄
   */
  setInfo({name, age = 10}) {
    this.name = name
    this.age = age
  }
}
```
