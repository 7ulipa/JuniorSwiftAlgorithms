
[https://leetcode.com/problems/surrounded-regions](https://leetcode.com/problems/surrounded-regions/#/description)

```
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
```


```
class Solution {
    let X = "X".characters.first!
    let O = "O".characters.first!
    let I = "I".characters.first!
    
    func solve(_ board: inout [[Character]]) {
        var stack: [(Int, Int)] = []
        for x in (0..<board.count) {
            for y in (0..<board[x].count) {
                if board[x][y] == O {
                    stack.append((x, y))
                }
                while let next = stack.popLast() {
                    stack.append(contentsOf: solve(next, board: &board))
                }
            }
        }
        
        for x in (0..<board.count) {
            for y in (0..<board[x].count) {
                if board[x][y] == I {
                    board[x][y] = O
                } else if board[x][y] != X {
                    board[x][y] = X
                }
            }
        }
    }
    
    private func solve(_ position: (Int, Int), board: inout [[Character]]) -> [(Int, Int)] {
        if board[position.0][position.1] == O {
            if position.0 == 0 || position.1 == 0 || position.0 == board.count - 1 || position.1 == board[0].count - 1 || _neighbour(for: position, board: board).contains(where: { board[$0.0][$0.1] == I }) {
                board[position.0][position.1] = I
                return neighbour(for: position, board: board)
            }
        }
        return []
    }
    
    private func neighbour(for position: (Int, Int), board: [[Character]]) -> [(Int, Int)] {
        var result: [(Int, Int)] = []
        if position.0 + 1 < board.count && board[position.0 + 1][position.1] == O {
            result.append((position.0 + 1, position.1))
        }
        if position.1 + 1 < board[0].count && board[position.0][position.1 + 1] == O {
            result.append((position.0, position.1 + 1))
        }
        if position.0 - 1 >= 0 && board[position.0 - 1][position.1] == O {
            result.append((position.0 - 1, position.1))
        }
        if position.1 - 1 >= 0 && board[position.0][position.1 - 1] == O {
            result.append((position.0, position.1 - 1))
        }
        return result
    }
    
    private func _neighbour(for position: (Int, Int), board: [[Character]]) -> [(Int, Int)] {
        var result: [(Int, Int)] = []
        if position.0 + 1 < board.count {
            result.append((position.0 + 1, position.1))
        }
        if position.1 + 1 < board[0].count {
            result.append((position.0, position.1 + 1))
        }
        if position.0 - 1 >= 0 {
            result.append((position.0 - 1, position.1))
        }
        if position.1 - 1 >= 0 {
            result.append((position.0, position.1 - 1))
        }
        return result
    }
}

```

