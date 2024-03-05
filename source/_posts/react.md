---
title: react 基础
date: 
updated:
tags: react
categories: 前端
cover: https://s1.ax1x.com/2023/06/20/pC8kAgS.png
---

# react hook 函数

## useCallback

- 基本使用：

```typescript
const cachedFn = useCallback(fn, dependencies)
```

- 理解：

	只有在其中一个依赖项发生更改时才会更改。这在将回调传递给依赖引用相等性的优化子组件以防止不必要的渲染。

> 对于 react 来说，只有状态发生了改变，就会重新渲染该组件。为了避免重新渲染，我们应该用 <span style="background-color: yellow"> useCallback </span> 函数进行包起来。

- 应用场景：

保证每次组件不会重新渲染，只有依赖项改变时，才会重新渲染。

例子：

```typescript
// hook 函数
const [detail, setDetail] = useState([])
const [detailLoading, setDetailLoading] = useState(false)

const getDetail = useCallback(() => {
  // 写具体内容
  // detail 改变时
  detail = ['1']
  // detailLoading
  detailLoading = false;
}, [detail, detailLoading])
```

- <strong style="color: red">注意：</strong>
  - useCallback 仍然属于 hook，必须写在组件内
  - 依赖项必须明确，不能直接写`[]` , 这时跟没写 useCallback 一样。

## useMemo, useCallback, useEffect 三者区别

### useEffect 和 useMemo 区别

> 参考链接: [useMemo, useCallback, useEffect 三者区别 - 掘金 (juejin.cn)](https://juejin.cn/post/7008433550307360798)

- useEffect是在<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px"> DOM改变之后触发</span>，useMemo在<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">DOM渲染之前就触发</span>
- useMemo是在<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">DOM更新前触发的</span>，就像官方所说的，类比生命周期就是[shouldComponentUpdate]
- useEffect可以帮助我们在<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">DOM更新完成后执行某些副作用操作</span>，如数据获取，设置订阅以及手动更改 React 组件中的 DOM 等
- 不要在这个useMemo函数内部<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">执行与渲染无关的操作</span>，诸如<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">副作用这类的操作属于 useEffect 的适用范畴</span>，而不是 useMemo
- 在useMemo中使用<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">setState你会发现会产生死循环</span>，并且会有警告，因为useMemo是<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">在渲染中进行的</span>，你在其中操作<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">DOM</span>后，又会导致触发<span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">memo</span>

### useCallback 和 useMemo 区别

- 类似 <span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">shouldComponentUpdate</span>， 判定该组件的 props 和 state 是否有变化，从而避免每次父组件render时都去重新渲染子组件
- <span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">useCallback返回一个函数</span>，当把它返回的这个函数作为子组件使用时，可以避免每次父组件更新时都重新渲染这个子组件,子组件一般配合 <span style="background-color: #fff5f5;color: #ff502c;font-size: 14px">memo</span> 使用
