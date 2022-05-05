# 快速上手 VuePress-20220402

### 1 aaaaaaaaaaaaa

### dddddddd

###

- 1 vue 构造函数初始化过程
- 2 vue 实例化过程
  -3 vue 实例首次渲染的过程

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
