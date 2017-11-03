
```
class Node<T> {
    var next: Node<T>?
    let value: T
    init(value: T, next: Node<T>?) {
        self.value = value
        self.next = next
    }
    func reverse() -> Node {
        return _reverse(left: nil, right: self)
    }
    
    func _reverse(left: Node?, right: Node?) -> Node {
        if let right = right {
            let next = right.next
            right.next = left
            return _reverse(left: right, right: next)
        } else {
            return left!
        }
    }
    
    var desc: String {
        if let next = next {
            return "\(value) -> \(next.desc)"
        } else {
            return "\(value)"
        }
    }
}


let node = Node(value: 1, next: Node(value: 2, next: Node(value: 3, next: Node(value: 4, next: Node(value: 5, next: Node(value: 6, next: nil))))))

debugPrint(node.desc)

debugPrint(node.reverse().desc)


```


output:

```
"1 -> 2 -> 3 -> 4 -> 5 -> 6"
"6 -> 5 -> 4 -> 3 -> 2 -> 1"
```

