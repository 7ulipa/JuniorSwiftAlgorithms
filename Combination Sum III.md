
[https://leetcode.com/problems/combination-sum-iii](https://leetcode.com/problems/combination-sum-iii/#/description)

```
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.


Example 1:

Input: k = 3, n = 7

Output:

[[1,2,4]]

Example 2:

Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]
```


```
class Solution {
    func combinationSum3(_ k: Int, _ n: Int) -> [[Int]] {
        var result: [[Int]] = []
        with(base: [], more: k) {
            if $0.reduce(0, +) == n {
                result.append($0)
            }
        }
        return result
    }
    
    private func with(base: [Int], more: Int, block: ([Int]) -> Void) {
        let from = (base.last ?? 0) + 1
        guard from <= 9 else {
            return
        }
        if more == 1 {
            ((base.last ?? 0) + 1...9).forEach {
                var result = base
                result.append($0)
                block(result)
            }
        } else {
            ((base.last ?? 0) + 1...9).forEach {
                var result = base
                result.append($0)
                with(base: result, more: more - 1, block: block)
            }
        }
    }
}

```


