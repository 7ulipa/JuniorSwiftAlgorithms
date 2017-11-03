
```
func merge_sort(input: [Int]) -> [Int] {
    if input.count <= 1 {
        return input
    } else if input.count == 2 {
        return input.first! > input.last! ? [input.last!, input.first!] : input
    } else {
        let count = input.count / 2
        let left = merge_sort(input: Array(input.prefix(count)))
        let right = merge_sort(input: Array(input.suffix(from: count)))
        var result: [Int] = []
        var i = 0
        var j = 0
        while i < left.count && j < right.count {
            if left[i] > right[j] {
                result.append(right[j])
                j += 1
            } else {
                result.append(left[i])
                i += 1
            }
        }
        result.append(contentsOf: left.suffix(from: i))
        result.append(contentsOf: right.suffix(from: j))
        return result
    }
}

debugPrint(merge_sort(input: [3, 2, 1, 9, 10, 33, 1, 4, 6, 2, 9]))
```
