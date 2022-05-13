# 快速上手 VuePress-20220402

## nextTick 实现原理

```
因为 vue 采用的异步更新策略，当监听到数据发生变化的时候不会立即去更新DOM，
而是开启一个任务队列，并缓存在同一事件循环中发生的所有数据变更;
这种做法带来的好处就是可以将多次数据更新合并成一次，减少操作DOM的次数，
如果不采用这种方法，假设数据改变100次就要去更新100次DOM，而频繁的DOM更新是很耗性能的；
```

### vue 源码

- 1 h 函数如何产生虚拟 DOM
- 2 新旧虚拟 dom 如何 DIFF
- 3 虚拟 dom 变为真实 DOM （上树）

### vue 初始化

- vue 构造函数初始化过程
- vue 实例化过程
- vue 实例首次渲染的过程

#### 模板编译后得到 render()函数，，render 函数返回 vnode 虚拟 dome 节点

真实 dom 属性很多，操作重，vnode，定义的一个对象属性少，操作轻，，节点与节点的比较，有差异了再更新

```
 setTimeout(() => {},0)
 目的==
0把任务放到宏任务队列，同步代码执行完之后，再执行宏任务，后执行

const cache=Object.create(null)


/**
 * Create a cached version of a pure function.
 */
export function cached<F: Function> (fn: F): F {
  const cache = Object.create(null)
  return (function cachedFn (str: string) {
    const hit = cache[str]
    return hit || (cache[str] = fn(str))
  }: any)
}


```

#### 虚拟 DOM

- 用 JavaScript 对象描述 DOM 的层次结构，DOM 中的一切属性都在虚拟 DOM 中有对应的属性
  diff 是发生在虚拟 DOM 上的，新旧虚拟 dom 对比计算出最小更新，最后反映到真实的 DOM 上
  -1 key 是节点的唯一标识，告诉 difff 算法，在更改前后他们是同一个 DOM 节点。
  -1 只有同一虚拟节点，才能进行精益化比较--如何定义同一个虚拟节点，选择器相同且 key 相同
  -1 只进行同一层次比较，不会进行跨层比较。

```
思考 1.这样的数据劫持方式对数组有什么影响？

这样递归的方式其实无论是对象还是数组都进行了观测 但是我们想一下此时如果 data 包含数组比如 a:[1,2,3,4,5] 那么我们根据下标可以直接修改数据也能触发 set 但是如果一个数组里面有上千上万个元素 每一个元素下标都添加 get 和 set 方法 这样对于性能来说是承担不起的 所以此方法只用来劫持对象

思考 2.Object.defineProperty 缺点？

对象新增或者删除的属性无法被 set 监听到 只有对象本身存在的属性修改才会被劫持

作者：Big shark@LX
链接：https://juejin.cn/post/6935344605424517128
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```