  # SwiftCodingCheatSheet

<table><td>
  
- Array
  ```
  [Int](1...3) // [1, 2, 3]
  [1, 2] + [3] // [1, 2, 3]
  (arr[i], arr[j]) = (arr[j], arr[i]) // arr.swapAt(i,j)
  ```

- Array fast remove
  ```
  arr.swapAt(i, arr.count-1)
  arr.removeLast()
  ```

- 2D Array
  ```
  var arr3x3 = Array(repeating: [Int](0..<3), count:3)
  var arrRow1 = arr3x3[1]
  arrRow1[1] = 4
  arr3x3[1] = arrRow1 // must set back
  // or
  arr3x3[1][1] = 4
  ```

- Array as Queue
  ```
  arr.first, arr.last // Optional
  if !arr.isEmpty {
    let f = arr.removeFirst()
    //let e = arr.removeLast()
  }
  arr.remove(at: i)
  arr.insert(e, at: 0)
  arr.append(e)
  ```

- Sub Array
  ```
  // arr: [1, 2, 3, 4]
  var rest: ArraySlice = arr.dropFirst(2) // [3, 4]
  rest = arr[2..<array.count] //arr[2...array.count-1]
  let restArr = Array(rest)
  // first k subarray:
  Array(arr[0..<k])
  ```

- String
  ```
  str.count
  str.append("a") // str += "b"
  // get character at index
  // str[str.index(str.startIndex, offsetBy:index)]
  let arr = Array(str); arr[index] 
  ```

- String <-> Int
  ```
  Int(str)

  String(i)
  "\(i)"
  
  ```
  
  - String <-> Array
  ```
  Array(str)
  
  let a:[Character] = ["a", "b"]
  String(a)
  let b = ["a", "b"]
  b.joined()
  b.joined(separator: "")
  ```

- Character
  ```
  for (i, c) in str.enumerated() where c == " " {
    let a = Int(c.asciiValue! /*UInt8?*/)
  }
  for c in str.unicodeScalars { 
    let _ = Int(c.value /*UInt32*/) 
  }
  ```

- Reorder
  ```
  var arr = [1, 3, 2]
  arr.sort()// mutating func sort()
  arr.sort(by: >) // [3, 2, 1] 
  let sorted = arr.sorted() // func sorted() -> [Element]

  reverse() / reversed() / shuffle() / shuffled() 
  ```
  
</td>
<!--  -------------------------------------------------------------------------------------------------------------------------------  -->
<td>

- Dictionary
  ```
  var dic = [String: Int]()
  if let _ = dic[key] {
    dic[key] = nil   // dic.removeValue(forKey:key)
  }
  dic[key, default:0] += 1
  
  // sort keys by value
  let sortedKeys = dic.keys.sorted {
      return dic[$0]! > dic[$1]!
  }
  // To Array
  Array(dic.values)
  for value in dic.values {}
  ```

- Set
  ```
  var s = Set(arr)
  s.isEmpty
  s.contains(e)
  s.insert(e)
  s.remove(e)
  union、intersection、subtracting、symmetricDifference
  ```

- Random
  ```
  Int.random(in: 0..<6)
  arr.randomElement()
  ```

- Numbers

  ```
  max(4, 2, 1, 3, 5)
  min(1.0, 2.1)
  Int.min
  Int.max
  ```

- Enumeration

  ```
  for i in 1...10 {}
  for i in (0..<10).reversed() {}
  for i in stride(from:0, to:10, by:2){} // 0 2 4 6 8
  for i in stride(from: 2, through: 0, by: -1) {} // 2 1 0
  for (i, element) in arr.enumerated() {}
  for (i, element) in arr.enumerated() where element > 3 {}
  for (value, char) in zip(65...66, ["A", "B", "C"]) {} // (65, A) (66, B)
  let sum = nums.reduce(0, { x, y in
      x ^ y
  }) // nums.reduce(0, ^)


  ```

- Templates
  ```
  func dfs(_ result: inout [[Int]],
    _ path: inout [Int],
    _ visited: inout [Bool],
    _ arr: [Int], _ index: Int) {
    // if end condition { result.append(path); return }
    for i in 0..<arr.count {
        // if should filter out { continue }
        visited[i] = true
        path.append(nums[i])
        dfs(&result, &path, &visited, arr, i+1)
        path.removeLast()
        visited[i] = false
    }
  }
                           
  // Trie Node
  class TrieNode {
    var children = [Character: TrieNode]()
    var isEnd = false
  }
                           
  // Hashable                 
  extension TreeNode: Hashable {
    public static func ==(l: TreeNode, r: TreeNode) -> Bool {
        return l === r
    }
    public func hash(into hasher: inout Hasher) {
        hasher.combine(ObjectIdentifier(self).hashValue)
    }
  }
  var cache = [TreeNode: Int]()
  
  // 151. Reverse Words in a String
  s.split(separator: " ").reversed().joined(separator: " ")
  
  // monotonic stack (next greater element)
  var maxQueue = [Int](), result = [Int](repeating:-1, count:nums.count)
  for (i, num) in nums.enumerated() {
      while (!maxQueue.isEmpty && num > nums[maxQueue.last!]) {
          result[maxQueue.last!] = num
          maxQueue.removeLast()
      }
      maxQueue.append(i)
  }
  ```

</td></table>
