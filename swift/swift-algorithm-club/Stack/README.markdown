# 스택

A stack is like an array but with limited functionality. You can only *push* to add a new element to the top of the stack, *pop* to remove the element from the top, and *peek* at the top element without popping it off.
스택은 배열과 유사하면서도 배열보다는 제한된 기능을 가진다. 스택의 맨 앞에 새로운 요소를 추가하기 위해서는 *푸시* (*push*)만 사용할 수 있고, 맨 앞에 있는 요소를 제거하기 위해서는 *팝*(*pop*) 만을 사용할 수 있으며, 맨 앞의 요소를 팝 하지 않는 경우에는 *픽*(*peek*) 을 사용할 수 있다.

Why would you want to do this? Well, in many algorithms you want to add objects to a temporary list at some point and then pull them off this list again at a later time. Often the order in which you add and remove these objects matters.
왜 이러한 동작을 하고자 할까? 글쎄, 많은 알고리즘에서 여러분은 같은 포인트의 임시 리스트에 객체를 추가한 다음 나중에 이 리스트에서 객체를 다시 꺼내고 싶어 한다. 보통 이러한 객체를 추가하거나 제거하는 순서가 중요하다.

A stack gives you a LIFO or last-in first-out order. The element you pushed last is the first one to come off with the next pop. (A very similar data structure, the [queue](../Queue/), is FIFO or first-in first-out.)
스택은 여러분에게 LIFO 또는 마지막에 입력 첫 번째 출력(last-in first out)이라 부르는 기능를 제공한다. 여러분이 마지막에 추가한 요소는 다음번에 꺼내는 첫 번째요소가 된다.(이는 FIFO 또는 첫 번째 입력 첫 번째 출력(first-in first-out)불리는 기능을 제공하는 자료구조인 [큐](../Queue/)와 매우 유사하다.)

For example, let's push a number on the stack:
예를 들어, 스택에 숫자를 푸시해 보도록 하자. 

```swift
stack.push(10)
```

The stack is now `[ 10 ]`. Push the next number:
이제 스택은 `[10]`이 되었다. 다음 숫자를 푸시해 보자.

```swift
stack.push(3)
```

The stack is now `[ 10, 3 ]`. Push one more number:
이제 스택은 `[10, 3]`이 되었다. 숫자를 하나 더 푸시해 보도록 하자.

```swift
stack.push(57)
```

The stack is now `[ 10, 3, 57 ]`. Let's pop the top number off the stack:
이제 스택은 `[10, 3, 57]`이 되었다. 이번에는 스택에 제일 위에 있는 숫자를 팝 해 보도록 하자.

```swift
stack.pop()
```

This returns `57`, because that was the most recent number we pushed. The stack is `[ 10, 3 ]` again.
위 코드는 `57`을 반환하는데, 이는 `57`이 가장 최근에 추가한 숫자 이기 때문이다. 스택은 다시 `[10, 3]`이 되었다.

```swift
stack.pop()
```

This returns `3`, and so on. If the stack is empty, popping returns `nil` or in some implementations it gives an error message ("stack underflow").
위 코드는 계속해서 `3`을 반환한다. 만약 스택이 비어있다면, 팝 하는 동작은 `nil`을 반환하거나 in some implementations 에러 메시지를 반환한다.(“stack underflow”)

A stack is easy to create in Swift. It's just a wrapper around an array that just lets you push, pop, and peek:
스위프트에서는 스택을 생성 하기가 매우 쉽다. 스택은 단지 푸시(push), 팝(pop) 그리고 픽(peek)을 할 수 있도록 배열을 감싼 것에 불과하다.

```swift
public struct Stack<T> {
  private var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }

  public mutating func push(element: T) {
    array.append(element)
  }

  public mutating func pop() -> T? {
    return array.popLast()
  }

  public func peek() -> T? {
    return array.last
  }
}
```

Notice that a push puts the new element at the end of the array, not the beginning. Inserting at the beginning of an array is expensive, an **O(n)** operation, because it requires all existing array elements to be shifted in memory. Adding at the end is **O(1)**; it always takes the same amount of time, regardless of the size of the array.

Fun fact about stacks: Each time you call a function or a method, the CPU places the return address on a stack. When the function ends, the CPU uses that return address to jump back to the caller. That's why if you call too many functions -- for example in a recursive function that never ends -- you get a so-called "stack overflow" as the CPU stack has run out of space.

*Written for Swift Algorithm Club by Matthijs Hollemans*
