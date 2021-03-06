---
title: react diff
date: 2021-03-17 23:08:10
tags: react diff
categories: react
---

# react diff 算法的理解

diff 算法主要有三个策略（观察的规律）

- DOM 节点的跨层级移动的操作特别少，可以忽略不计
- 拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构
- 对于同一层级的一组子节点，可以通过唯一的 id 进行区分

## tree diff

diff 算法只会对相同层级的 DOM 节点进行比较。
如果发现节点不存在 那么会将该节点以及其子节点完全删除 不会再继续比较。如
果出现了 DOM 节点的跨层级的移动操作，那么会删除改节点以及其所有的子节点，然后再移动后的位置重新创建

## component diff

如果是同一类型的组件，那么会继续对比 VM 数。
如果不是同一类型的组件，那么会将其和其子节点完全替换，不会再进行比对同一类型的组件用户可以设置 shouldComponentUpdate() 来判断是否需要进行 diff 算法。

## element diff

当节点处于同一层级的时候时，有三种操作：插入、 移动、 删除
这里 React 有一个优化策略，对于同一层级的同组子节点，添加唯一的 key 进行区分。这样的话，就可以判断出来是否是移动节点。通过 key 发现新旧集合中的节点都是相同的节点，就只需要进行移动操作就可以。
