# CLRQL . LEETCODE 600

## 1-bit-and-2-bit-characters

```golang
func isOneBitCharacter(bits []int) bool {
    i := 0
    for i < len(bits)-1 {
        if bits[i] == 0 {
            i++
        } else {
            i += 2
        }
    }
    return i == len(bits)-1
}

```

---

## 132-pattern

```golang
func find132pattern(nums []int) bool {
    n := len(nums)
    if n < 3 {
        return false
    }
    
    minStack := make([]int, n)
    minStack[0] = nums[0]
    
    for i := 1; i < n; i++ {
        minStack[i] = min(minStack[i-1], nums[i])
    }
    
    stack := []int{}
    
    for j := n - 1; j >= 0; j-- {
        if nums[j] > minStack[j] {
            for len(stack) > 0 && stack[len(stack)-1] <= minStack[j] {
                stack = stack[:len(stack)-1]
            }
            if len(stack) > 0 && stack[len(stack)-1] < nums[j] {
                return true
            }
            stack = append(stack, nums[j])
        }
    }
    
    return false
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## 3sum

```golang
func threeSum(nums []int) [][]int {
    // sort the array
    sort.Ints(nums)
    // initialize an empty result slice
    result := [][]int{}
    
    // iterate over each number in the array
    for i := 0; i < len(nums)-2; i++ {
        // check for duplicates
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        // initialize left and right pointers
        left := i+1
        right := len(nums)-1
        
        // move left and right pointers toward each other
        for left < right {
            // check for duplicates
            if left > i+1 && nums[left] == nums[left-1] {
                left++
                continue
            }
            if right < len(nums)-1 && nums[right] == nums[right+1] {
                right--
                continue
            }
            
            // check if current triplet sums to 0
            sum := nums[i] + nums[left] + nums[right]
            if sum == 0 {
                result = append(result, []int{nums[i], nums[left], nums[right]})
                left++
                right--
            } else if sum < 0 {
                left++
            } else {
                right--
            }
        }
    }
    return result
}

```

---

## 3sum-closest

```golang
func threeSumClosest(nums []int, target int) int {
    // Ordena la lista de números para simplificar el proceso de búsqueda.
    sort.Ints(nums)
    
    closest := nums[0] + nums[1] + nums[2]
    
    for i := 0; i < len(nums) - 2; i++ {
        left, right := i+1, len(nums)-1
        
        for left < right {
            sum := nums[i] + nums[left] + nums[right]
            
            if abs(sum - target) < abs(closest - target) {
                closest = sum
            }
            
            if sum < target {
                left++
            } else if sum > target {
                right--
            } else {
                // No puedes obtener una suma más cercana que esta, así que retorna inmediatamente.
                return sum
            }
        }
    }
    
    return closest
}

func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}
```

---

## 4sum

```golang
func fourSum(nums []int, target int) [][]int {
    // sort the array
    sort.Ints(nums)
    // initialize an empty result slice
    result := [][]int{}
    
    // iterate over each number in the array
    for i := 0; i < len(nums)-3; i++ {
        // check for duplicates
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }
        // iterate over each number in the array
        for j := i+1; j < len(nums)-2; j++ {
            // check for duplicates
            if j > i+1 && nums[j] == nums[j-1] {
                continue
            }
            // initialize left and right pointers
            left := j+1
            right := len(nums)-1
            
            // move left and right pointers toward each other
            for left < right {
                // check for duplicates
                if left > j+1 && nums[left] == nums[left-1] {
                    left++
                    continue
                }
                if right < len(nums)-1 && nums[right] == nums[right+1] {
                    right--
                    continue
                }
                
                // check if current quadruplet sums to target
                sum := nums[i] + nums[j] + nums[left] + nums[right]
                if sum == target {
                    result = append(result, []int{nums[i], nums[j], nums[left], nums[right]})
                    left++
                    right--
                } else if sum < target {
                    left++
                } else {
                    right--
                }
            }
        }
    }
    return result
}

```

---

## actors-and-directors-who-cooperated-at-least-three-times

```pythondata
import pandas as pd

def actors_and_directors(actor_director: pd.DataFrame) -> pd.DataFrame:
    # Group by actor_id and director_id, then count the occurrences
    counts = actor_director.groupby(['actor_id', 'director_id']).size().reset_index(name='count')
    
    # Filter the pairs that have a count of at least three
    result = counts[counts['count'] >= 3][['actor_id', 'director_id']]
    
    return result

```

---

## add-binary

```golang
func addBinary(a string, b string) string {
    var result string
    carry := 0
    i, j := len(a)-1, len(b)-1
    
    for i >= 0 || j >= 0 || carry > 0 {
        sum := carry

        if i >= 0 {
            sum += int(a[i] - '0')
            i--
        }

        if j >= 0 {
            sum += int(b[j] - '0')
            j--
        }

        result = strconv.Itoa(sum%2) + result
        carry = sum / 2
    }

    return result
}

```

---

## add-digits

```python
class Solution(object):
    def addDigits(self, num):
        """
        :type num: int
        :rtype: int
        """
        if num == 0:
            return 0
        return 1 + (num-1)%9
        
```

---

## add-strings

```golang

func addStrings(num1 string, num2 string) string {
	i := len(num1) - 1
	j := len(num2) - 1
	carry := 0
	var result strings.Builder

	for i >= 0 || j >= 0 || carry > 0 {
		sum := carry

		if i >= 0 {
			sum += int(num1[i] - '0')
			i--
		}

		if j >= 0 {
			sum += int(num2[j] - '0')
			j--
		}

		result.WriteString(strconv.Itoa(sum % 10))
		carry = sum / 10
	}

	// Reverse the result
	bytes := []byte(result.String())
	for left, right := 0, len(bytes)-1; left < right; left, right = left+1, right-1 {
		bytes[left], bytes[right] = bytes[right], bytes[left]
	}

	return string(bytes)
}
```

---

## add-to-array-form-of-integer

```golang
func addToArrayForm(num []int, k int) []int {
    n := len(num)
    carry := 0
    result := make([]int, n)

    for i := n - 1; i >= 0; i-- {
        digitSum := num[i] + k%10 + carry
        carry = digitSum / 10
        result[i] = digitSum % 10
        k /= 10
    }

    // Process any remaining carry from k
    for k > 0 {
        digitSum := k%10 + carry
        carry = digitSum / 10
        result = append([]int{digitSum % 10}, result...)
        k /= 10
    }

    // Process any remaining carry
    for carry > 0 {
        result = append([]int{carry % 10}, result...)
        carry /= 10
    }

    return result
}

```

---

## add-two-numbers

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        current = dummy
        carry = 0

        p = l1
        q = l2

        while p is not None or q is not None:
            x = p.val if p else 0
            y = q.val if q else 0

            total = x + y + carry
            carry = total // 10

            current.next = ListNode(total % 10)
            current = current.next

            if p:
                p = p.next
            if q:
                q = q.next

        if carry > 0:
            current.next = ListNode(carry)

        return dummy.next
```

---

## add-two-numbers-ii

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    // Reverse the input lists
    l1 = reverseList(l1)
    l2 = reverseList(l2)
    
    // Initialize variables
    var head *ListNode
    carry := 0
    
    // Iterate through the lists and add the corresponding digits
    for l1 != nil || l2 != nil || carry != 0 {
        sum := carry
        
        if l1 != nil {
            sum += l1.Val
            l1 = l1.Next
        }
        
        if l2 != nil {
            sum += l2.Val
            l2 = l2.Next
        }
        
        digit := sum % 10
        carry = sum / 10
        
        // Create a new node with the calculated digit
        newNode := &ListNode{Val: digit, Next: head}
        head = newNode
    }
    
    return head
}

// Helper function to reverse a linked list
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    
    for head != nil {
        next := head.Next
        head.Next = prev
        prev = head
        head = next
    }
    
    return prev
}
```

---

## add-two-promises

```javascript
/**
 * @param {Promise} promise1
 * @param {Promise} promise2
 * @return {Promise}
 */
var addTwoPromises = async function(promise1, promise2) {
    return new Promise((resolve) => {
        let cnt = 2, res = 0;
        const handler = (n) => {
            res += n, cnt--;
            if (!cnt) resolve(res)
        }
        promise1.then(handler)
        promise2.then(handler)
    })
};

/**
 * addTwoPromises(Promise.resolve(2), Promise.resolve(2))
 *   .then(console.log); // 4
 */
```

---

## allow-one-function-call

```javascript
/**
 * @param {Function} fn
 * @return {Function}
 */
var once = function(fn) {
    let used = false;
    return function(...args){
        if (used) return undefined;
        used = true;
        return fn(...args);
    }
};

/**
 * let fn = (a,b,c) => (a + b + c)
 * let onceFn = once(fn)
 *
 * onceFn(1,2,3); // 6
 * onceFn(2,3,6); // returns undefined without calling fn
 */
```

---

## apply-transform-over-each-element-in-array

```javascript
/**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
var map = function(arr, fn) {
    for (let i = 0; i<arr.length; i++) {
        arr[i] = fn(arr[i], i);
    }
    return arr;
};
```

---

## arranging-coins

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var arrangeCoins = function(n) {
    let left = 0;
  let right = n;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);
    let coinsNeeded = (mid * (mid + 1)) / 2;

    if (coinsNeeded === n) {
      return mid;
    } else if (coinsNeeded < n) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return right;
};
```

---

## array-partition

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var arrayPairSum = function(nums) {
    nums.sort((a, b) => a-b);
    let sum = 0;
    for (let i = 0; i < nums.length; i+=2) {
        sum += nums[i];
    }
    return sum;
};
```

---

## array-prototype-last

```javascript
Array.prototype.last = function() {
    if (!this.length) return -1;
    return this[this.length-1];
};

/**
 * const arr = [1, 2, 3];
 * arr.last(); // 3
 */
```

---

## array-reduce-transformation

```javascript
/**
 * @param {number[]} nums
 * @param {Function} fn
 * @param {number} init
 * @return {number}
 */
var reduce = function(nums, fn, init) {
  let acc = init;
  for (let i = 0; i < nums.length; i++) {
    acc = fn(acc, nums[i]);
  }
  return acc;
};
```

---

## array-wrapper

```javascript
/**
 * @param {number[]} nums
 */
var ArrayWrapper = function(nums) {
    this.nums = nums;
};

ArrayWrapper.prototype.valueOf = function() {
    return this.nums.reduce((acc, curr) => acc+curr, 0);
}

ArrayWrapper.prototype.toString = function() {
    return JSON.stringify(this.nums);
}

/**
 * const obj1 = new ArrayWrapper([1,2]);
 * const obj2 = new ArrayWrapper([3,4]);
 * obj1 + obj2; // 10
 * String(obj1); // "[1,2]"
 * String(obj2); // "[3,4]"
 */
```

---

## article-views-i

```mysql
# Write your MySQL query statement below


select distinct author_id as id
from Views
where author_id = viewer_id
order by id asc;
```

---

## assign-cookies

```javascript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function(g, s) {
    g.sort((a, b) => a - b); // Sort greed factors in ascending order
  s.sort((a, b) => a - b); // Sort cookie sizes in ascending order

  let contentChildren = 0;
  let cookieIndex = 0;

  for (let i = 0; i < g.length; i++) {
    while (cookieIndex < s.length && s[cookieIndex] < g[i]) {
      cookieIndex++;
    }

    if (cookieIndex < s.length) {
      contentChildren++;
      cookieIndex++;
    } else {
      break; // No more cookies available
    }
  }

  return contentChildren;
};
```

---

## asteroid-collision

```golang
func asteroidCollision(asteroids []int) []int {
	stack := make([]int, 0)

	for _, asteroid := range asteroids {
		collided := false

		for len(stack) > 0 && asteroid < 0 && stack[len(stack)-1] > 0 {
			if stack[len(stack)-1] < -asteroid {
				stack = stack[:len(stack)-1]
				continue
			} else if stack[len(stack)-1] == -asteroid {
				stack = stack[:len(stack)-1]
			}
			collided = true
			break
		}

		if !collided {
			stack = append(stack, asteroid)
		}
	}

	return stack
}

```

---

## available-captures-for-rook

```golang
func numRookCaptures(board [][]byte) int {
    var rookRow, rookCol int

    // Find the position of the white rook 'R'
    for i := 0; i < 8; i++ {
        for j := 0; j < 8; j++ {
            if board[i][j] == 'R' {
                rookRow, rookCol = i, j
                break
            }
        }
    }

    // Define the four cardinal directions (north, east, south, west)
    directions := [][2]int{{-1, 0}, {0, 1}, {1, 0}, {0, -1}}

    captures := 0

    for _, direction := range directions {
        row, col := rookRow, rookCol

        // Simulate rook's movement in the current direction
        for {
            row += direction[0]
            col += direction[1]

            // Check if the rook is out of the board or blocked by a white bishop 'B'
            if row < 0 || row >= 8 || col < 0 || col >= 8 || board[row][col] == 'B' {
                break
            }

            // Check if the rook captures a black pawn 'p'
            if board[row][col] == 'p' {
                captures++
                break
            }
        }
    }

    return captures
}

```

---

## average-of-levels-in-binary-tree

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var averageOfLevels = function(root) {
  const result = [];
  if (!root) return result;

  const queue = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;
    let levelSum = 0;

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      levelSum += node.val;

      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    const average = levelSum / levelSize;
    result.push(average);
  }

  return result;
}
```

---

## average-selling-price

```mysql
# Write your MySQL query statement below

select u.product_id, round(
    sum(u.units * p.price) /
    sum(u.units), 2
) as average_price
from UnitsSold u
join Prices p on u.product_id = p.product_id
    and u.purchase_date >= p.start_date
    and u.purchase_date <= p.end_date
group by u.product_id;
```

---

## average-time-of-process-per-machine

```mysql
# Write your MySQL query statement below

select machine_id, round(avg(end_time - start_time), 3) as processing_time
from (
    select machine_id, process_id,
        min(timestamp) as start_time,
        max(timestamp) as end_time
    from Activity
    group by machine_id, process_id
) as subquery
group by machine_id;

```

---

## backspace-string-compare

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var backspaceCompare = function(s, t) {
    const getNextValidCharIndex = (str, index) => {
        let backspaceCount = 0;
        while (index >= 0) {
            if (str[index] === '#') {
                backspaceCount++;
            } else if (backspaceCount > 0) {
                backspaceCount--;
            } else {
                break;
            }
            index--;
        }
        return index;
    }

    let sIndex = s.length - 1;
    let tIndex = t.length - 1;

    while (sIndex >= 0 || tIndex >= 0) {
        sIndex = getNextValidCharIndex(s, sIndex);
        tIndex = getNextValidCharIndex(t, tIndex);

        if (sIndex < 0 && tIndex < 0) {
            return true;
        }
        if (sIndex < 0 || tIndex < 0 || s[sIndex] !== t[tIndex]) {
            return false;
        }

        sIndex--;
        tIndex--;
    }

    return true;
};
```

---

## balanced-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isBalanced(root *TreeNode) bool {
	if root == nil {
		// An empty tree is considered balanced
		return true
	}

	// Check if the left and right subtrees are balanced
	leftHeight := getHeight(root.Left)
	rightHeight := getHeight(root.Right)
	heightDiff := math.Abs(float64(leftHeight - rightHeight))

	if heightDiff > 1 {
		// If the height difference is more than 1, the tree is not balanced
		return false
	}

	// Recursively check if both subtrees are balanced
	return isBalanced(root.Left) && isBalanced(root.Right)
}

func getHeight(node *TreeNode) int {
	if node == nil {
		// Base case: an empty subtree has height 0
		return 0
	}

	// Recursively compute the height of the left and right subtrees
	leftHeight := getHeight(node.Left)
	rightHeight := getHeight(node.Right)

	// The height of the current node is the maximum height of its subtrees plus 1
	return int(math.Max(float64(leftHeight), float64(rightHeight))) + 1
}

```

---

## base-7

```javascript
/**
 * @param {number} num
 * @return {string}
 */
var convertToBase7 = function(num) {
    if (num === 0) return '0';
    let res = '';
    let neg = num < 0;
    num = Math.abs(num);
    while (num > 0) {
        let rem = num % 7;
        res = rem.toString() + res;
        num = Math.floor(num/7);
    }
    return neg ? '-'+res : res;
};
```

---

## baseball-game

```golang
func calPoints(operations []string) int {
    stack := make([]int, 0)

    for _, op := range operations {
        switch op {
        case "C":
            stack = stack[:len(stack)-1]
        case "D":
            score := stack[len(stack)-1] * 2
            stack = append(stack, score)
        case "+":
            score := stack[len(stack)-1] + stack[len(stack)-2]
            stack = append(stack, score)
        default:
            score, _ := strconv.Atoi(op)
            stack = append(stack, score)
        }
    }

    sum := 0
    for _, score := range stack {
        sum += score
    }

    return sum
}

```

---

## basic-calculator

```golang
func calculate(s string) int {
	stack := make([]int, 0)
	sign := 1 // represents the sign of the current expression
	result := 0
	num := 0

	for i := 0; i < len(s); i++ {
		if isDigit(s[i]) {
			// Calculate the number by iterating over consecutive digits
			num = num*10 + int(s[i]-'0')
		} else if s[i] == '+' {
			// Add the number to the result with the appropriate sign
			result += sign * num
			num = 0 // reset the number
			sign = 1 // reset the sign for the next expression
		} else if s[i] == '-' {
			// Add the number to the result with the appropriate sign
			result += sign * num
			num = 0 // reset the number
			sign = -1 // reset the sign for the next expression
		} else if s[i] == '(' {
			// Push the result and sign onto the stack
			stack = append(stack, result, sign)
			result = 0 // reset the result for the sub-expression
			sign = 1 // reset the sign for the sub-expression
		} else if s[i] == ')' {
			// Evaluate the sub-expression by popping the result and sign from the stack
			result += sign * num
			num = 0 // reset the number

			sign = stack[len(stack)-1] // restore the sign
			stack = stack[:len(stack)-1] // pop the sign from the stack
			prevResult := stack[len(stack)-1] // get the previous result
			stack = stack[:len(stack)-1] // pop the previous result from the stack
			result = prevResult + sign*result // calculate the new result
			sign = 1 // reset the sign for the next expression
		}
	}

	// Add the last number to the result with the appropriate sign
	result += sign * num

	return result
}

func isDigit(ch byte) bool {
	return ch >= '0' && ch <= '9'
}


```

---

## best-time-to-buy-and-sell-stock

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let maxProfit = 0;
    let minPrice = prices[0];

    for (let i = 1; i < prices.length; i++) {
        // Update the minimum price if a lower price is found
        minPrice = Math.min(minPrice, prices[i]);

        // Calculate the potential profit if selling at the current price
        let profit = prices[i] - minPrice;

        // Update the maximum profit if a higher profit is found
        maxProfit = Math.max(maxProfit, profit);
    }

    return maxProfit;
}
```

---

## best-time-to-buy-and-sell-stock-ii

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  let maxProfit = 0;
  
  for (let i = 1; i < prices.length; i++) {
    if (prices[i] > prices[i - 1]) {
      maxProfit += prices[i] - prices[i - 1];
    }
  }
  
  return maxProfit;
}

```

---

## best-time-to-buy-and-sell-stock-iii

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  const n = prices.length;

  // Create two arrays to store the maximum profit for the first and second transactions
  const profits1 = new Array(n).fill(0);
  const profits2 = new Array(n).fill(0);

  let minPrice = prices[0];
  let maxProfit1 = 0;

  // Calculate the maximum profit for the first transaction
  for (let i = 1; i < n; i++) {
    minPrice = Math.min(minPrice, prices[i]);
    maxProfit1 = Math.max(maxProfit1, prices[i] - minPrice);
    profits1[i] = maxProfit1;
  }

  let maxPrice = prices[n - 1];
  let maxProfit2 = 0;
  let maxProfit = 0;

  // Calculate the maximum profit for the second transaction and overall maximum profit
  for (let i = n - 2; i >= 0; i--) {
    maxPrice = Math.max(maxPrice, prices[i]);
    maxProfit2 = Math.max(maxProfit2, maxPrice - prices[i]);
    profits2[i] = maxProfit2;
    maxProfit = Math.max(maxProfit, profits1[i] + profits2[i]);
  }

  return maxProfit;
}
```

---

## best-time-to-buy-and-sell-stock-iv

```javascript
/**
 * @param {number} k
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(k, prices) {
  const n = prices.length;
  
  // If k is greater than or equal to half the length of prices,
  // we can make as many transactions as we want, so we can use
  // a greedy approach to find the maximum profit.
  if (k >= Math.floor(n / 2)) {
    let maxProfit = 0;
    for (let i = 1; i < n; i++) {
      if (prices[i] > prices[i - 1]) {
        maxProfit += prices[i] - prices[i - 1];
      }
    }
    return maxProfit;
  }
  
  // Initialize the dp array
  const dp = new Array(n);
  for (let i = 0; i < n; i++) {
    dp[i] = new Array(k + 1).fill(0);
  }
  
  // Fill in the dp array
  for (let j = 1; j <= k; j++) {
    let maxDiff = -prices[0];
    for (let i = 1; i < n; i++) {
      dp[i][j] = Math.max(dp[i - 1][j], prices[i] + maxDiff);
      maxDiff = Math.max(maxDiff, dp[i - 1][j - 1] - prices[i]);
    }
  }
  
  return dp[n - 1][k];
}

```

---

## best-time-to-buy-and-sell-stock-with-transaction-fee

```golang
func maxProfit(prices []int, fee int) int {
    n := len(prices)
    if n <= 1 {
        return 0
    }
    
    // Initialize variables to track the maximum profit with and without stock
    cash := 0
    hold := -prices[0]
    
    // Iterate through the prices and update the variables
    for i := 1; i < n; i++ {
        prevCash := cash
        cash = max(cash, hold+prices[i]-fee)
        hold = max(hold, prevCash-prices[i])
    }
    
    // Return the maximum profit without stock (cash)
    return cash
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## big-countries

```mysql
# Write your MySQL query statement below

select name, population, area from World
where area >= 3000000 or population >= 25000000
```

---

## biggest-single-number

```mysql
# Write your MySQL query statement below

select max(num) as num from (
  select num from MyNumbers
  group by num having count(*) = 1
) as single_nums;
```

---

## binary-gap

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var binaryGap = function(n) {
    const binaryString = n.toString(2);
    let maxGap = 0;
    let currentGap = 0;
    let foundOne = false;
    for (let i = 0; i < binaryString.length; i++) {
        if (binaryString[i] === "1") {
            if (foundOne) {
                maxGap = Math.max(maxGap, currentGap)
            }
            currentGap = 1;
            foundOne = true;
        } else {
            if (foundOne) {
                currentGap++;
            }
        }
    }
    return maxGap;
};
```

---

## binary-number-with-alternating-bits

```golang
func hasAlternatingBits(n int) bool {
    binary := fmt.Sprintf("%b", n)

    for i := 1; i < len(binary); i++ {
        if binary[i] == binary[i-1] {
            return false
        }
    }

    return true
}

```

---

## binary-search

```golang
func search(nums []int, target int) int {
    left := 0
    right := len(nums) - 1

    for left <= right {
        mid := (left + right) / 2
        
        if nums[mid] == target {
            return mid
        } else if nums[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return -1
}
```

---

## binary-search-tree-iterator

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
type BSTIterator struct {
	stack []*TreeNode
}

func Constructor(root *TreeNode) BSTIterator {
	stack := make([]*TreeNode, 0)
	current := root

	for current != nil {
		stack = append(stack, current)
		current = current.Left
	}

	return BSTIterator{stack: stack}
}

func (it *BSTIterator) Next() int {
	node := it.stack[len(it.stack)-1]
	it.stack = it.stack[:len(it.stack)-1]

	current := node.Right
	for current != nil {
		it.stack = append(it.stack, current)
		current = current.Left
	}

	return node.Val
}

func (it *BSTIterator) HasNext() bool {
	return len(it.stack) > 0
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * obj := Constructor(root);
 * param_1 := obj.Next();
 * param_2 := obj.HasNext();
 */
```

---

## binary-tree-inorder-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
	if root == nil {
		return []int{}
	}

	stack := []*TreeNode{}
	result := []int{}
	curr := root

	for curr != nil || len(stack) > 0 {
		// Traverse left subtree
		for curr != nil {
			stack = append(stack, curr)
			curr = curr.Left
		}

		// Visit the current node
		curr = stack[len(stack)-1]
		stack = stack[:len(stack)-1]
		result = append(result, curr.Val)

		// Traverse right subtree
		curr = curr.Right
	}

	return result
}
```

---

## binary-tree-level-order-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func levelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }
    
    queue := []*TreeNode{root}
    result := [][]int{}
    
    for len(queue) > 0 {
        levelSize := len(queue)
        currentLevel := []int{}
        
        for i := 0; i < levelSize; i++ {
            node := queue[0]
            queue = queue[1:]
            currentLevel = append(currentLevel, node.Val)
            
            if node.Left != nil {
                queue = append(queue, node.Left)
            }
            
            if node.Right != nil {
                queue = append(queue, node.Right)
            }
        }
        
        result = append(result, currentLevel)
    }
    
    return result
}

```

---

## binary-tree-maximum-path-sum

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxPathSum(root *TreeNode) int {
	maxSum := math.MinInt32
	maxPathSumRecursive(root, &maxSum)
	return maxSum
}

func maxPathSumRecursive(node *TreeNode, maxSum *int) int {
	if node == nil {
		return 0
	}

	leftSum := max(maxPathSumRecursive(node.Left, maxSum), 0)
	rightSum := max(maxPathSumRecursive(node.Right, maxSum), 0)

	currentSum := node.Val + leftSum + rightSum
	*maxSum = max(*maxSum, currentSum)

	return node.Val + max(leftSum, rightSum)
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

```

---

## binary-tree-paths

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func binaryTreePaths(root *TreeNode) []string {
	if root == nil {
		return nil
	}

	var paths []string
	dfs(root, "", &paths)
	return paths
}

func dfs(node *TreeNode, path string, paths *[]string) {
	if node.Left == nil && node.Right == nil {
		// Reached a leaf node, append the path to the result
		*paths = append(*paths, path+strconv.Itoa(node.Val))
		return
	}

	// Append the current node's value to the path
	path += strconv.Itoa(node.Val) + "->"

	if node.Left != nil {
		dfs(node.Left, path, paths)
	}

	if node.Right != nil {
		dfs(node.Right, path, paths)
	}
}

/*
In this implementation, the binaryTreePaths function takes a pointer to the root of the binary tree and returns a slice of strings representing all root-to-leaf paths.

The dfs function performs a depth-first search starting from the given node. It takes the current node, the current path string, and a pointer to the result slice of paths. If the current node is a leaf node (no left or right children), it appends the current node's value to the path and adds the path to the result slice. If the current node has a left child, it recursively calls dfs on the left child, passing the updated path. Similarly, if the current node has a right child, it recursively calls dfs on the right child, passing the updated path.
*/
```

---

## binary-tree-postorder-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func postorderTraversal(root *TreeNode) []int {
	if root == nil {
		return nil
	}

	var result []int
	stack := []*TreeNode{root}

	for len(stack) > 0 {
		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		// Insert node's value at the beginning of the result slice
		result = append([]int{node.Val}, result...)

		// Push left child first so that right child is processed first
		if node.Left != nil {
			stack = append(stack, node.Left)
		}

		// Push right child
		if node.Right != nil {
			stack = append(stack, node.Right)
		}
	}

	return result
}

/*
In this implementation, the postorderTraversal function takes a pointer to the root of the binary tree and returns a slice containing the postorder traversal of the tree. It initializes an empty result slice and a stack to store the nodes. It starts with the root node and pushes it onto the stack. Then, it enters a loop where it pops a node from the stack, inserts its value at the beginning of the result slice, and pushes its left and right children onto the stack (right child first to ensure left child is processed first in postorder traversal). The loop continues until the stack is empty. Finally, it returns the result slice containing the postorder traversal. The main function demonstrates several test cases and prints the respective postorder traversals of the binary trees.
*/
```

---

## binary-tree-preorder-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func preorderTraversal(root *TreeNode) []int {
	if root == nil {
		return nil
	}

	var result []int
	stack := []*TreeNode{root}

	for len(stack) > 0 {
		node := stack[len(stack)-1]
		stack = stack[:len(stack)-1]

		result = append(result, node.Val)

		// Push right child first so that left child is processed first
		if node.Right != nil {
			stack = append(stack, node.Right)
		}

		// Push left child
		if node.Left != nil {
			stack = append(stack, node.Left)
		}
	}

	return result
}
```

---

## binary-tree-right-side-view

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function rightSideView(root: TreeNode | null): number[] {
  if (!root) {
    return [];
  }

  const result: number[] = [];
  const queue: TreeNode[] = [root];

  while (queue.length > 0) {
    const levelSize = queue.length;

    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift()!;

      if (i === levelSize - 1) {
        result.push(node.val);
      }

      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
  }

  return result;
}
```

---

## binary-tree-tilt

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findTilt = function(root) {
    let totalTilt = 0;

    function calculateTiltAndSum(node) {
        if (node === null) {
            return 0;
        }

        const leftSum = calculateTiltAndSum(node.left);
        const rightSum = calculateTiltAndSum(node.right);

        const tilt = Math.abs(leftSum - rightSum);

        totalTilt += tilt;

        return node.val + leftSum + rightSum;
    }

    calculateTiltAndSum(root);

    return totalTilt;
};
```

---

## binary-tree-zigzag-level-order-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func zigzagLevelOrder(root *TreeNode) [][]int {
    if root == nil {
        return [][]int{}
    }

    var result [][]int
    queue := []*TreeNode{root}
    level := 0

    for len(queue) > 0 {
        levelSize := len(queue)
        levelNodes := make([]int, levelSize)

        for i := 0; i < levelSize; i++ {
            node := queue[i]

            if level%2 == 0 {
                levelNodes[i] = node.Val
            } else {
                levelNodes[levelSize-i-1] = node.Val
            }

            if node.Left != nil {
                queue = append(queue, node.Left)
            }

            if node.Right != nil {
                queue = append(queue, node.Right)
            }
        }

        result = append(result, levelNodes)
        queue = queue[levelSize:]
        level++
    }

    return result
}
```

---

## binary-trees-with-factors

```javascript
/**
 * @param {number[]} arr
 * @return {number}
 */
var numFactoredBinaryTrees = function(arr) {
    const MOD = 1e9 + 7;
    arr.sort((a, b) => a - b); // Sort the array in ascending order
    const n = arr.length;
    const dp = new Array(n).fill(1); // Initialize a DP array with 1 for each element
    
    const index = new Map(); // Create a map for easy access to array indices
    for (let i = 0; i < n; i++) {
        index.set(arr[i], i);
    }

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < i; j++) {
            if (arr[i] % arr[j] === 0) {
                const factor = arr[i] / arr[j];
                if (index.has(factor)) {
                    const k = index.get(factor);
                    dp[i] = (dp[i] + dp[j] * dp[k]) % MOD;
                }
            }
        }
    }

    let total = 0;
    for (let i = 0; i < n; i++) {
        total = (total + dp[i]) % MOD;
    }
    
    return total;
};
```

---

## binary-watch

```golang
func readBinaryWatch(turnedOn int) []string {
	var result []string

	for hour := 0; hour < 12; hour++ {
		for minute := 0; minute < 60; minute++ {
			if countBits(hour)+countBits(minute) == turnedOn {
				timeStr := fmt.Sprintf("%d:%02d", hour, minute)
				result = append(result, timeStr)
			}
		}
	}

	return result
}

func countBits(num int) int {
	count := 0
	for num > 0 {
		if num&1 == 1 {
			count++
		}
		num >>= 1
	}
	return count
}
```

---

## bitwise-and-of-numbers-range

```golang
func rangeBitwiseAnd(left int, right int) int {
	shifts := 0

	// Find the common prefix of the binary representations
	// by counting the number of right shifts required to make
	// left and right equal.
	for left != right {
		left >>= 1
		right >>= 1
		shifts++
	}

	// Shift left back by the number of shifts performed
	// to obtain the bitwise AND result.
	return left << shifts
}
```

---

## broken-calculator

```golang
func brokenCalc(startValue int, target int) int {   
    operations := 0

    for target > startValue {
        if target % 2 == 0 {
            target /= 2
        } else {
            target += 1
        }
        operations++
    }

    return operations + startValue - target
}

/* 
    Allowed operations are "*2" and "-1".

    if startNumber -

*/
```

---

## buddy-strings

```golang
func buddyStrings(s string, goal string) bool {
    if len(s) != len(goal) {
        return false
    }
    
    // Case where s and goal are already equal
    if s == goal {
        // Check if there are duplicate characters in s
        charCount := make(map[byte]int)
        for _, char := range s {
            charCount[byte(char)]++
            if charCount[byte(char)] >= 2 {
                return true
            }
        }
        return false
    }
    
    // Find the indices where s and goal differ
    diffIndices := make([]int, 0)
    for i := 0; i < len(s); i++ {
        if s[i] != goal[i] {
            diffIndices = append(diffIndices, i)
        }
    }
    
    // Check if there are exactly two differing indices
    if len(diffIndices) == 2 && s[diffIndices[0]] == goal[diffIndices[1]] && s[diffIndices[1]] == goal[diffIndices[0]] {
        return true
    }
    
    return false
}

```

---

## build-an-array-with-stack-operations

```golang
func buildArray(target []int, n int) []string {
    result := []string{}
    currentIndex := 0

    for i := 1; i <= n && currentIndex < len(target); i++ {
        result = append(result, "Push")
        if i == target[currentIndex] {
            currentIndex++
        } else {
            result = append(result, "Pop")
        }
    }

    return result
}
```

---

## build-array-where-you-can-find-the-maximum-exactly-k-comparisons

```c
#define MOD 1000000007

int numOfArrays(int n, int m, int k) {
    int dp[n + 1][m + 1][k + 1];
    int prefix[n + 1][m + 1][k + 1];

    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            for (int l = 0; l <= k; l++) {
                dp[i][j][l] = 0;
                prefix[i][j][l] = 0;
            }
        }
    }

    for (int j = 1; j <= m; j++) {
        dp[1][j][1] = 1;
        prefix[1][j][1] = j;
    }

    for (int i = 2; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            for (int l = 1; l <= k; l++) {
                dp[i][j][l] = ((long long)j * dp[i - 1][j][l]) % MOD;

                if (j > 1 && l > 1) {
                    dp[i][j][l] = (dp[i][j][l] + prefix[i - 1][j - 1][l - 1]) % MOD;
                }

                prefix[i][j][l] = (prefix[i][j - 1][l] + dp[i][j][l]) % MOD;
            }
        }
    }

    return prefix[n][m][k];
}
```

---

## bulb-switcher

```golang
func bulbSwitch(n int) int {
    return int(math.Sqrt(float64(n)))
}
```

---

## bus-routes

```golang
func numBusesToDestination(routes [][]int, source int, target int) int {
	if source == target {
		return 0
	}

	stopToRoutes := make(map[int][]int)
	for i, route := range routes {
		for _, stop := range route {
			stopToRoutes[stop] = append(stopToRoutes[stop], i)
		}
	}

	visitedRoutes := make([]bool, len(routes))
	visitedStops := make(map[int]bool)

	queue := list.New()
	queue.PushBack(source)
	steps := 0

	for queue.Len() > 0 {
		size := queue.Len()

		for i := 0; i < size; i++ {
			currentStop := queue.Remove(queue.Front()).(int)

			for _, routeIndex := range stopToRoutes[currentStop] {
				if visitedRoutes[routeIndex] {
					continue
				}

				visitedRoutes[routeIndex] = true

				for _, nextStop := range routes[routeIndex] {
					if nextStop == target {
						return steps + 1
					}

					if !visitedStops[nextStop] {
						visitedStops[nextStop] = true
						queue.PushBack(nextStop)
					}
				}
			}
		}

		steps++
	}

	return -1
}
```

---

## cache-with-time-limit

```javascript
class TimeLimitedCache {
  constructor() {
    this.map = new Map();
  }

  set(key, value, duration) {
    const expirationTime = Date.now() + duration;
    const entry = { value, expirationTime };

    if (this.map.has(key)) {
      const existingEntry = this.map.get(key);
      if (existingEntry.expirationTime > Date.now()) {
        existingEntry.value = value;
        existingEntry.expirationTime = expirationTime;
        return true;
      }
    }

    this.map.set(key, entry);
    return false;
  }

  get(key) {
    const entry = this.map.get(key);
    if (entry && entry.expirationTime > Date.now()) {
      return entry.value;
    }
    return -1;
  }

  count() {
    let count = 0;
    for (const entry of this.map.values()) {
      if (entry.expirationTime > Date.now()) {
        count++;
      }
    }
    return count;
  }
}

```

---

## calculate-digit-sum-of-a-string

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var digitSum = function(s, k) {
    while (s.length > k) {
        let news = "";
        s.match(RegExp(`.{1,${k}}`, "g")).forEach(slice => {

            news += slice
                .split("")
                .map(elem => parseInt(elem))
                .reduce((acc, curr) => acc + curr);
            
        });
        s = news;
    }
    return s;
};
```

---

## calculate-special-bonus

```pythondata
import pandas as pd

def calculate_special_bonus(employees: pd.DataFrame) -> pd.DataFrame:
    # Apply the bonus calculation based on conditions
    employees['bonus'] = employees.apply(lambda row: row['salary'] if row['employee_id'] % 2 == 1 and row['name'][0] != 'M' else 0, axis=1)
    
    # Select and return the 'employee_id' and 'bonus' columns, ordered by 'employee_id'
    result = employees[['employee_id', 'bonus']].sort_values(by='employee_id')
    
    return result

```

---

## calculator-with-method-chaining

```javascript
class Calculator {
  
  ans = 0

  /** 
   * @param {number} value
   */
  constructor(value) {
      this.ans = value;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  add(value){
      this.ans += value;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  subtract(value){
      this.ans -= value;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */  
  multiply(value) {
      this.ans *= value;
  }

  /** 
   * @param {number} value
   * @return {Calculator}
   */
  divide(value) {
      if (value === 0) {
          throw new Error("Division by zero is not allowed");
      }
      this.ans /= value;
  }
  
  /** 
   * @param {number} value
   * @return {Calculator}
   */
  power(value) {
      this.ans **= value;
  }
    
  /** 
   * @return {number}
   */
  getResult() {
      return this.ans;
  }
}
```

---

## can-place-flowers

```golang
func canPlaceFlowers(flowerbed []int, n int) bool {
    count := 0
    length := len(flowerbed)
    for i := 0; i < length && count < n; i++ {
        if flowerbed[i] == 0 && (i == 0 || flowerbed[i-1] == 0) && (i == length-1 || flowerbed[i+1] == 0) {
            flowerbed[i] = 1
            count++
        }
    }
    return count >= n
}
```

---

## candy

```golang
func candy(ratings []int) int {
    n := len(ratings)
    candies := make([]int, n)

    // Initialize candies array with 1 candy for each child
    for i := 0; i < n; i++ {
        candies[i] = 1
    }

    // Traverse from left to right, assign more candies to higher-rated children
    for i := 1; i < n; i++ {
        if ratings[i] > ratings[i-1] {
            candies[i] = candies[i-1] + 1
        }
    }

    // Traverse from right to left, make sure neighbors with higher rating have more candies
    for i := n - 2; i >= 0; i-- {
        if ratings[i] > ratings[i+1] && candies[i] <= candies[i+1] {
            candies[i] = candies[i+1] + 1
        }
    }

    // Calculate the total number of candies needed
    totalCandies := 0
    for _, num := range candies {
        totalCandies += num
    }

    return totalCandies
}

```

---

## car-fleet

```javascript
/**
 * @param {number} target
 * @param {number[]} position
 * @param {number[]} speed
 * @return {number}
 */
var carFleet = function(target, position, speed) {
    const n = position.length;
    const cars = Array(n).fill().map((_, i) => ({ position: position[i], time: (target - position[i]) / speed[i] }));
    cars.sort((a, b) => b.position - a.position);
    let fleets = 0, prevTime = 0;
    for (let i = 0; i < n; i++) {
        if (cars[i].time > prevTime) {
            prevTime = cars[i].time;
            fleets++;
        }
    }
    return fleets;
};
```

---

## chunk-array

```javascript
/**
 * @param {Array} arr
 * @param {number} size
 * @return {Array[]}
 */
var chunk = function(arr, size) {
    let chunks = [];
    while (arr.length) {
        chunks.push([]);
        for (let i = 0; i<size; i++) {
            if (!arr.length) break;
            chunks[chunks.length-1].push(arr.shift());
        };
    };
    return chunks;
};
```

---

## classes-more-than-5-students

```mysql
# Write your MySQL query statement below

select class
from Courses
group by class
having count(student) >= 5;

```

---

## climbing-stairs

```golang
func climbStairs(n int) int {
    if n <= 2 {
        return n
    }
    
    dp := make([]int, n+1)
    dp[1] = 1
    dp[2] = 2
    
    for i := 3; i <= n; i++ {
        dp[i] = dp[i-1] + dp[i-2]
    }
    
    return dp[n]
}

```

---

## clone-graph

```golang
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Neighbors []*Node
 * }
 */


func cloneGraph(node *Node) *Node {
    if node == nil {
        return nil
    }

    visited := make(map[*Node]*Node)
    return clone(node, visited)
}

func clone(node *Node, visited map[*Node]*Node) *Node {
    // If the node has already been visited, return the cloned node
    if visited[node] != nil {
        return visited[node]
    }

    // Create a new cloned node
    cloned := &Node{Val: node.Val, Neighbors: make([]*Node, len(node.Neighbors))}
    visited[node] = cloned

    // Clone the neighbors recursively
    for i, neighbor := range node.Neighbors {
        cloned.Neighbors[i] = clone(neighbor, visited)
    }

    return cloned
}
```

---

## coin-change

```javascript
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function(coins, amount) {
  // Initialize a dp array with a length of amount + 1 and fill it with Infinity
  const dp = new Array(amount + 1).fill(Infinity);
  
  // The minimum number of coins needed to make amount 0 is 0
  dp[0] = 0;

  // Iterate through all amounts from 1 to amount
  for (let i = 1; i <= amount; i++) {
    // For each amount, try using each coin denomination
    for (let j = 0; j < coins.length; j++) {
      if (coins[j] <= i) {
        // If using the current coin leads to a smaller number of coins needed,
        // update the dp array with the new minimum number of coins
        dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
      }
    }
  }

  // If dp[amount] is still Infinity, it means the amount cannot be made up
  return dp[amount] === Infinity ? -1 : dp[amount];
}

```

---

## combination-sum

```golang
func combinationSum(candidates []int, target int) [][]int {
    // Step 1: Sort candidates array
    sort.Ints(candidates)

    // Step 2: Initialize result array
    result := [][]int{}

    // Step 5: Call backtrack function
    backtrack(&result, []int{}, candidates, target, 0)

    // Step 6: Return result array
    return result
}

// Step 3: Define backtrack function
func backtrack(result *[][]int, combination []int, candidates []int, target int, start int) {
    // Step 4a: Check if sum equals target
    if target == 0 {
        // Append a copy of the combination to the result
        temp := make([]int, len(combination))
        copy(temp, combination)
        *result = append(*result, temp)
        return
    }

    // Step 4b: Check if sum exceeds target or index out of bounds
    if target < 0 || start >= len(candidates) {
        return
    }

    // Step 4c: Iterate over candidates
    for i := start; i < len(candidates); i++ {
        candidate := candidates[i]

        // Add candidate to the combination
        combination = append(combination, candidate)

        // Step 4c: Recursively call backtrack with updated combination, sum, and index
        backtrack(result, combination, candidates, target-candidate, i)

        // Remove last candidate from the combination
        combination = combination[:len(combination)-1]
    }
}
```

---

## combination-sum-ii

```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
    const result = [];
    const uniqueCombinations = new Set();

    candidates.sort((a, b) => a - b); // Sort the candidates in ascending order.

    const dfs = (start, current, currentSum) => {
        if (currentSum === target) {
            uniqueCombinations.add([...current]);
            return;
        }

        if (currentSum > target || start === candidates.length) {
            return;
        }

        for (let i = start; i < candidates.length; i++) {
            // Skip duplicates to avoid duplicate combinations.
            if (i > start && candidates[i] === candidates[i - 1]) {
                continue;
            }

            current.push(candidates[i]);
            dfs(i + 1, current, currentSum + candidates[i]);
            current.pop();
        }
    };

    dfs(0, [], 0);

    return Array.from(uniqueCombinations);
};
```

---

## combination-sum-iii

```typescript
function combinationSum3(k: number, n: number): number[][] {
  const combinations: number[][] = [];
  
  function backtrack(start: number, sum: number, combination: number[]): void {
    if (sum === n && combination.length === k) {
      combinations.push([...combination]);
      return;
    }
    
    if (sum > n || combination.length > k) {
      return;
    }
    
    for (let i = start; i <= 9; i++) {
      combination.push(i);
      backtrack(i + 1, sum + i, combination);
      combination.pop();
    }
  }
  
  backtrack(1, 0, []);
  return combinations;
}

```

---

## combinations

```golang
func combine(n int, k int) [][]int {
	result := [][]int{}
	current := []int{}

	backtrack(&result, current, 1, n, k)

	return result
}

func backtrack(result *[][]int, current []int, start, n, k int) {
	if len(current) == k {
		combination := make([]int, k)
		copy(combination, current)
		*result = append(*result, combination)
		return
	}

	for i := start; i <= n; i++ {
		current = append(current, i)
		backtrack(result, current, i+1, n, k)
		current = current[:len(current)-1]
	}
}
```

---

## combine-two-tables

```mysql
# Write your MySQL query statement below
SELECT P.firstName, P.lastName, A.city, A.state
FROM Person P
LEFT JOIN Address A USING (personId)
```

---

## compact-object

```javascript
/**
 * @param {Object} obj
 * @return {Object}
 */
var compactObject = function(obj) {
  if (Array.isArray(obj)) {
    return obj
      .filter(Boolean)
      .map(compactObject);
  }

  if (typeof obj === 'object' && obj !== null) {
    return Object.entries(obj)
      .reduce((acc, [key, value]) => {
        if (Boolean(value)) {
          acc[key] = compactObject(value);
        }
        return acc;
      }, {});
  }

  return obj;
};
```

---

## complement-of-base-10-integer

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var bitwiseComplement = function(n) {
  var mask = (1 << n.toString(2).length) - 1;
  return n ^ mask;
};
```

---

## confirmation-rate

```mysql
# Write your MySQL query statement below

select s.user_id, 
    case when count(c.action) = 0 then 0
        else round(sum(case when c.action = 'confirmed' then 1 else 0 end) / count(c.action), 2)
    end as confirmation_rate
from Signups s
left join Confirmations c on s.user_id = c.user_id
group by s.user_id;

```

---

## consecutive-numbers

```mysql
# Write your MySQL query statement below
select distinct num as ConsecutiveNums
from (
  select num,  row_number() over (order by id) - row_number() over (partition by num order by id) as consecutive_group
  from Logs
) as subquery
group by num, consecutive_group
having count(*) >= 3;
```

---

## constrained-subsequence-sum

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var constrainedSubsetSum = function(nums, k) {
        let dq = [];
        for (let i = 0; i < nums.length; i++) {
            nums[i] += dq.length > 0 ? nums[dq[0]] : 0;

            while (dq.length > 0 && (i - dq[0] >= k || nums[i] >= nums[dq[dq.length - 1]])) {
                if (nums[i] >= nums[dq[dq.length - 1]]) dq.pop();
                else dq.shift();
            }

            if (nums[i] > 0) {
                dq.push(i);
            }
        }
        return Math.max(...nums);
    }
```

---

## construct-binary-tree-from-inorder-and-postorder-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(inorder []int, postorder []int) *TreeNode {
    if len(inorder) == 0 {
        return nil
    }

    // Create a map to store the indices of inorder elements
    indexMap := make(map[int]int)
    for i, val := range inorder {
        indexMap[val] = i
    }

    return buildTreeHelper(inorder, postorder, 0, len(inorder)-1, 0, len(postorder)-1, indexMap)
}

func buildTreeHelper(inorder []int, postorder []int, inStart, inEnd, postStart, postEnd int, indexMap map[int]int) *TreeNode {
    if inStart > inEnd || postStart > postEnd {
        return nil
    }

    // The last element in postorder is the root of the current subtree
    rootVal := postorder[postEnd]
    root := &TreeNode{Val: rootVal}

    // Find the index of the root value in inorder
    rootIndex := indexMap[rootVal]

    // Calculate the number of nodes in the left subtree
    leftSubtreeSize := rootIndex - inStart

    // Recursively build the left and right subtrees
    root.Left = buildTreeHelper(inorder, postorder, inStart, rootIndex-1, postStart, postStart+leftSubtreeSize-1, indexMap)
    root.Right = buildTreeHelper(inorder, postorder, rootIndex+1, inEnd, postStart+leftSubtreeSize, postEnd-1, indexMap)

    return root
}
```

---

## construct-binary-tree-from-preorder-and-inorder-traversal

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func buildTree(preorder []int, inorder []int) *TreeNode {
	if len(preorder) == 0 {
		return nil
	}

	// The first element in the preorder traversal is the root of the tree
	rootVal := preorder[0]
	root := &TreeNode{Val: rootVal}

	// Find the root index in the inorder traversal
	var rootIndex int
	for i, val := range inorder {
		if val == rootVal {
			rootIndex = i
			break
		}
	}

	// Split the inorder traversal into left and right subtrees
	leftInorder := inorder[:rootIndex]
	rightInorder := inorder[rootIndex+1:]

	// Split the preorder traversal into left and right subtrees
	leftPreorder := preorder[1 : len(leftInorder)+1]
	rightPreorder := preorder[len(leftInorder)+1:]

	// Recursively build the left and right subtrees
	root.Left = buildTree(leftPreorder, leftInorder)
	root.Right = buildTree(rightPreorder, rightInorder)

	return root
}
```

---

## construct-quad-tree

```golang

func construct(grid [][]int) *Node {
    n := len(grid)
    return buildQuadTree(grid, 0, 0, n)
}

func buildQuadTree(grid [][]int, x, y, size int) *Node {
    if size == 1 {
        return &Node{
            Val:       grid[x][y] == 1,
            IsLeaf:    true,
            TopLeft:   nil,
            TopRight:  nil,
            BottomLeft: nil,
            BottomRight: nil,
        }
    }
    
    halfSize := size / 2
    topLeft := buildQuadTree(grid, x, y, halfSize)
    topRight := buildQuadTree(grid, x, y+halfSize, halfSize)
    bottomLeft := buildQuadTree(grid, x+halfSize, y, halfSize)
    bottomRight := buildQuadTree(grid, x+halfSize, y+halfSize, halfSize)
    
    if isLeafNode(topLeft) && isLeafNode(topRight) && isLeafNode(bottomLeft) && isLeafNode(bottomRight) &&
        topLeft.Val == topRight.Val && topRight.Val == bottomLeft.Val && bottomLeft.Val == bottomRight.Val {
        return &Node{
            Val:       topLeft.Val,
            IsLeaf:    true,
            TopLeft:   nil,
            TopRight:  nil,
            BottomLeft: nil,
            BottomRight: nil,
        }
    }
    
    return &Node{
        Val:       false,
        IsLeaf:    false,
        TopLeft:   topLeft,
        TopRight:  topRight,
        BottomLeft: bottomLeft,
        BottomRight: bottomRight,
    }
}

func isLeafNode(node *Node) bool {
    return node != nil && node.IsLeaf
}
```

---

## construct-string-from-binary-tree

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */

/**
 * @param {TreeNode} root
 * @return {string}
 */
var tree2str = function(root) {
  if (root === null) {
    return '';
  }
  
  // Recursive function to construct the string
  function constructString(node) {
    let str = node.val.toString();
    
    if (node.left !== null) {
      str += '(' + constructString(node.left) + ')';
    } else if (node.right !== null) {
      str += '()';
    }
    
    if (node.right !== null) {
      str += '(' + constructString(node.right) + ')';
    }
    
    return str;
  }
  
  return constructString(root);
};

```

---

## construct-the-rectangle

```javascript
/**
 * @param {number} area
 * @return {number[]}
 */
var constructRectangle = function(area) {
  var sqrt = Math.floor(Math.sqrt(area));

  for (var i = sqrt; i >= 1; i--) {
    if (area % i === 0) {
      return [area / i, i];
    }
  }
};

```

---

## container-with-most-water

```golang
func maxArea(height []int) int {
    i, j := 0, len(height)-1
    maxArea := 0
    
    for i < j {
        area := min(height[i], height[j]) * (j-i)
        if area > maxArea {
            maxArea = area
        }
        
        if height[i] < height[j] {
            i++
        } else {
            j--
        }
    }
    
    return maxArea
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

---

## contains-duplicate

```golang
func containsDuplicate(nums []int) bool {
    seen := make(map[int]bool)
    
    for _, num := range nums {
        // If the number is already in the set, it's a duplicate
        if seen[num] {
            return true
        }
        // Add the number to the set
        seen[num] = true
    }
    
    return false
}

```

---

## contains-duplicate-ii

```golang
func containsNearbyDuplicate(nums []int, k int) bool {
    numIndex := make(map[int]int) // Map to store the indices of encountered numbers
    
    for i, num := range nums {
        if j, ok := numIndex[num]; ok && i-j <= k {
            return true
        }
        numIndex[num] = i // Update the index of the number
    }
    
    return false
}

```

---

## convert-a-number-to-hexadecimal

```golang
func toHex(num int) string {
	if num == 0 {
		return "0"
	}

	// Define the hexadecimal digits
	digits := "0123456789abcdef"
	result := ""

	// Convert negative numbers to their two's complement form
	if num < 0 {
		num += 1 << 32
	}

	// Convert the number to hexadecimal
	for num > 0 {
		// Extract the last four bits of the number
		digit := num & 0xf

		// Prepend the corresponding hexadecimal digit
		result = string(digits[digit]) + result

		// Right shift the number by four bits
		num >>= 4
	}

	return result
}

/*
In this implementation, the toHex function takes an integer num and converts it into its hexadecimal representation as a string.

We start by checking if num is equal to 0. If it is, we simply return "0" as the hexadecimal representation.

Next, we define a string digits that contains the hexadecimal digits from 0 to f. This string will be used to map the extracted digits to their corresponding hexadecimal characters.

If num is negative, we convert it to its two's complement form by adding 1 << 32 (the length of an integer in bits) to it.

To convert the number to hexadecimal, we repeatedly extract the last four bits of the number using bitwise AND with 0xf. We prepend the corresponding hexadecimal digit to the result string using string indexing.

After extracting the digit, we right shift the number by four bits to move to the next four bits.

Finally, we return the result string as the hexadecimal representation of the given number.
*/
```

---

## convert-object-to-json-string

```javascript
/**
 * @param {any} object
 * @return {string}
 */
var jsonStringify = function(object) {
    if (object === null) return "null";
    if (typeof object === "string") return '"' + object + '"';
    if (typeof object === "number" || typeof object === "boolean") {
        return object.toString();
    }
    if (Array.isArray(object)) {
        var arrResult = [];
        for (var i = 0; i < object.length; i++) {
            arrResult.push(jsonStringify(object[i]))
        }
        return "[" + arrResult.join(",") + "]";
    }
    var objResult = [];
    var keys = Object.keys(object);
    for (var i = 0; i < keys.length; i++) {
        var key = keys[i];
        var val = jsonStringify(object[key]);
        objResult.push('"' + key + '":' + val);
    }
    return "{" + objResult.join(",") + "}";
};
```

---

## convert-sorted-array-to-binary-search-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sortedArrayToBST(nums []int) *TreeNode {
    if len(nums) == 0 {
        return nil
    }
    
    mid := len(nums) / 2
    
    root := &TreeNode{
        Val:   nums[mid],
        Left:  sortedArrayToBST(nums[:mid]),
        Right: sortedArrayToBST(nums[mid+1:]),
    }
    
    return root
}
```

---

## copy-list-with-random-pointer

```typescript
/**
 * Definition for Node.
 * class Node {
 *     val: number
 *     next: Node | null
 *     random: Node | null
 *     constructor(val?: number, next?: Node, random?: Node) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *         this.random = (random===undefined ? null : random)
 *     }
 * }
 */

function copyRandomList(head: Node | null): Node | null {
  if (head === null) {
    return null;
  }

  const map: Map<Node, Node> = new Map();
  let current: Node | null = head;

  // Create new nodes with the same values
  while (current !== null) {
    const newNode = new Node(current.val);
    map.set(current, newNode);
    current = current.next;
  }

  current = head;

  // Set the next and random pointers of the new nodes
  while (current !== null) {
    const newNode = map.get(current)!;
    newNode.next = map.get(current.next) || null;
    newNode.random = map.get(current.random) || null;
    current = current.next;
  }

  return map.get(head)!;
}

```

---

## count-and-say

```javascript
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
    if (n === 1) {
        return "1";
    }
    
    const previous = countAndSay(n - 1);
    let result = "";
    
    let count = 1;
    for (let i = 0; i < previous.length; i++) {
        if (previous[i] === previous[i + 1]) {
            count++;
        } else {
            result += count + previous[i];
            count = 1;
        }
    }
    
    return result;
};
```

---

## count-binary-substrings

```golang
func countBinarySubstrings(s string) int {
    prevCount := 0
    currCount := 1
    count := 0

    for i := 1; i < len(s); i++ {
        if s[i] == s[i-1] {
            currCount++
        } else {
            prevCount = currCount
            currCount = 1
        }

        if prevCount >= currCount {
            count++
        }
    }

    return count
}

```

---

## count-complete-tree-nodes

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func countNodes(root *TreeNode) int {
	if root == nil {
		return 0
	}

	leftHeight := getHeight(root.Left)
	rightHeight := getHeight(root.Right)

	if leftHeight == rightHeight {
		// The left subtree is a full binary tree of height leftHeight.
		// The total number of nodes in the left subtree can be calculated as 2^leftHeight - 1.
		return countNodes(root.Right) + (1 << leftHeight)
	} else {
		// The right subtree is a full binary tree of height rightHeight - 1.
		// The total number of nodes in the right subtree can be calculated as 2^(rightHeight-1) - 1.
		return countNodes(root.Left) + (1 << rightHeight)
	}
}

func getHeight(node *TreeNode) int {
	height := 0
	for node != nil {
		height++
		node = node.Left
	}
	return height
}
```

---

## count-good-nodes-in-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func goodNodes(root *TreeNode) int {
    return countGoodNodes(root, root.Val)
}

func countGoodNodes(node *TreeNode, maxValue int) int {
    if node == nil {
        return 0
    }
    
    count := 0
    if node.Val >= maxValue {
        count = 1
        maxValue = node.Val
    }
    
    count += countGoodNodes(node.Left, maxValue)
    count += countGoodNodes(node.Right, maxValue)
    
    return count
}
```

---

## count-nodes-equal-to-average-of-subtree

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var averageOfSubtree = function(root) {
    // Helper function to calculate the sum and count of nodes in a subtree
    function calculateSubtreeAverage(node) {
        if (!node) {
            return [0, 0]; // [Sum, Count]
        }
        const [leftSum, leftCount] = calculateSubtreeAverage(node.left);
        const [rightSum, rightCount] = calculateSubtreeAverage(node.right);
        
        const subtreeSum = leftSum + rightSum + node.val;
        const subtreeCount = leftCount + rightCount + 1;
        
        if (node.val === Math.floor(subtreeSum / subtreeCount)) {
            result++;
        }
        
        return [subtreeSum, subtreeCount];
    }
    
    let result = 0;
    calculateSubtreeAverage(root);
    return result;
};
```

---

## count-number-of-homogenous-substrings

```golang
func countHomogenous(s string) int {
    const mod int = 1000000007
    result := 0
    count := 1

    for i := 1; i < len(s); i++ {
        if s[i] == s[i-1] {
            count++
        } else {
            result = (result + count*(count+1)/2) % mod
            count = 1
        }
    }

    // Add the count for the last homogenous substring
    result = (result + count*(count+1)/2) % mod

    return result
}

```

---

## count-numbers-with-unique-digits

```golang
func countNumbersWithUniqueDigits(n int) int {
    if n == 0 {
		return 1
	} else if n == 1 {
		return 10
	}

	// Inicializamos el resultado con 10 (números de un solo dígito).
	result := 10
	// El primer dígito tiene 9 opciones (1-9).
	uniqueDigits := 9
	// Inicializamos el número de opciones disponibles para el segundo dígito.
	availableDigits := 9

	for i := 2; i <= n; i++ {
		// Multiplicamos el número de opciones únicas por las opciones disponibles y actualizamos el resultado.
		uniqueDigits *= availableDigits
		result += uniqueDigits
		// Reducimos el número de opciones disponibles para el siguiente dígito.
		availableDigits--
	}

	return result
}
```

---

## count-primes

```rust
impl Solution {
    pub fn count_primes(n: i32) -> i32 {
        let n = n as usize;
        if n <= 2 {return 0;}
        let mut validations: Vec<bool> = vec![true; n];
        validations.splice(0..2, [false;2]);
        for i in 2..=(n as f64).sqrt() as usize {
            if !validations[i] {continue}
            let mut j = i.pow(2);
            while j < n {
                validations[j] = false;
                j += i;
            }
        }
        validations.into_iter().filter(|&a| a).count() as i32
    }
}
```

---

## count-salary-categories

```mysql
# Write your MySQL query statement below

(
  select 'Low Salary' as category, count(*) as accounts_count
  from Accounts
  where income < 20000
)

union

(
  select 'Average Salary' as category, count(*) as accounts_count
  from Accounts
  where income between 20000 and 50000
)

union

(
  select 'High Salary' as category, count(*) as accounts_count
  from Accounts
  where income > 50000
)

```

---

## count-vowels-permutation

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var countVowelPermutation = function(n) {
    const MOD = 1000000007;
    
    // Inicializamos dp para n = 1
    let dp = [1, 1, 1, 1, 1];
    
    for (let i = 2; i <= n; i++) {
        // Creamos un nuevo arreglo para almacenar los valores actualizados
        let newDp = [0, 0, 0, 0, 0];
        
        // Reglas para cada vocal
        newDp[0] = (dp[1] + dp[2] + dp[4]) % MOD; // 'a' puede ser seguido por 'e', 'i' o 'u'
        newDp[1] = (dp[0] + dp[2]) % MOD; // 'e' puede ser seguido por 'a' o 'i'
        newDp[2] = (dp[1] + dp[3]) % MOD; // 'i' puede ser seguido por 'e' o 'o'
        newDp[3] = (dp[2]) % MOD; // 'o' puede ser seguido solo por 'i'
        newDp[4] = (dp[2] + dp[3]) % MOD; // 'u' puede ser seguido por 'i' o 'o'
        
        // Actualizamos dp con los nuevos valores
        dp = newDp;
    }
    
    // Sumamos todos los valores de dp y tomamos el módulo
    return dp.reduce((sum, val) => (sum + val) % MOD, 0);
};

```

---

## counter

```javascript
/**
 * @param {number} n
 * @return {Function} counter
 */
var createCounter = function(n) {
    let count = n;
    return function() {
        const currentCount = count;
        count++;
        return currentCount;
    };
};

/** 
 * const counter = createCounter(10)
 * counter() // 10
 * counter() // 11
 * counter() // 12
 */
```

---

## counter-ii

```typescript
type ReturnObj = {
  increment: () => number;
  decrement: () => number;
  reset: () => number;
};

function createCounter(init: number): ReturnObj {
  let current: number = init;

  return {
    increment: () => {
      current += 1;
      return current;
    },
    decrement: () => {
      current -= 1;
      return current;
    },
    reset: () => {
      current = init;
      return current;
    },
  };
}

/**
 * const counter = createCounter(5)
 * counter.increment(); // 6
 * counter.reset(); // 5
 * counter.decrement(); // 4
 */
```

---

## counting-bits

```typescript
function countBits(n: number): number[] {
    let ans: number[] = new Array(n+1).fill(0);

    for (let i = 0; i <= n; i++) {
        ans[i] = i.toString(2).replace(/0/g, "").length;
    }

    return ans;
};
```

---

## course-schedule

```golang
func canFinish(numCourses int, prerequisites [][]int) bool {
    // Create an adjacency list to represent the graph
    graph := make([][]int, numCourses)
    for _, prerequisite := range prerequisites {
        course, prerequisite := prerequisite[0], prerequisite[1]
        graph[course] = append(graph[course], prerequisite)
    }

    // Create an array to track the visited status of each course
    visited := make([]int, numCourses)

    // Perform depth-first search (DFS) on each course
    for course := 0; course < numCourses; course++ {
        if visited[course] == 0 && !dfs(course, graph, visited) {
            return false
        }
    }

    return true
}

func dfs(course int, graph [][]int, visited []int) bool {
    // If the course has already been visited and marked as being visited again, a cycle exists
    if visited[course] == -1 {
        return false
    }

    // If the course has already been visited and marked as visited, no cycle exists
    if visited[course] == 1 {
        return true
    }

    // Mark the course as being visited
    visited[course] = -1

    // Recursively visit the prerequisites of the course
    for _, prerequisite := range graph[course] {
        if !dfs(prerequisite, graph, visited) {
            return false
        }
    }

    // Mark the course as visited
    visited[course] = 1

    return true
}
```

---

## course-schedule-ii

```javascript
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {number[]}
 */
var findOrder = function(numCourses, prerequisites) {
  const adjacencyList = new Array(numCourses).fill(0).map(() => []);
  const indegree = new Array(numCourses).fill(0);
  const result = [];
  
  // Build the adjacency list and calculate the indegree of each course
  for (let [course, prerequisite] of prerequisites) {
    adjacencyList[prerequisite].push(course);
    indegree[course]++;
  }
  
  const queue = [];
  
  // Add all the courses with indegree 0 to the queue
  for (let i = 0; i < numCourses; i++) {
    if (indegree[i] === 0) {
      queue.push(i);
    }
  }
  
  // Perform topological sorting
  while (queue.length) {
    const prerequisite = queue.shift();
    result.push(prerequisite);
    
    for (let course of adjacencyList[prerequisite]) {
      indegree[course]--;
      
      if (indegree[course] === 0) {
        queue.push(course);
      }
    }
  }
  
  // If there is a cycle, it is impossible to finish all courses
  if (result.length !== numCourses) {
    return [];
  }
  
  return result;
};

```

---

## cousins-in-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isCousins(root *TreeNode, x int, y int) bool {
    if root == nil {
        return false
    }

    queue := []struct {
        node   *TreeNode
        parent *TreeNode
        depth  int
    }{{root, nil, 0}}

    var parentX, parentY *TreeNode
    depthX, depthY := -1, -1

    for len(queue) > 0 {
        nodeInfo := queue[0]
        queue = queue[1:]
        node, parent, depth := nodeInfo.node, nodeInfo.parent, nodeInfo.depth

        if node.Val == x {
            parentX, depthX = parent, depth
        } else if node.Val == y {
            parentY, depthY = parent, depth
        }

        if parentX != nil && parentY != nil {
            break
        }

        if node.Left != nil {
            queue = append(queue, struct {
                node   *TreeNode
                parent *TreeNode
                depth  int
            }{node.Left, node, depth + 1})
        }
        if node.Right != nil {
            queue = append(queue, struct {
                node   *TreeNode
                parent *TreeNode
                depth  int
            }{node.Right, node, depth + 1})
        }
    }

    return depthX == depthY && parentX != parentY
}
```

---

## create-hello-world-function

```javascript
/**
 * @return {Function}
 */
var createHelloWorld = function() {
    return function(...args) {
        return "Hello World"
    }
};

/**
 * const f = createHelloWorld();
 * f(); // "Hello World"
 */
```

---

## customer-placing-the-largest-number-of-orders

```mysql
# Write your MySQL query statement below
SELECT customer_number
FROM Orders
GROUP BY customer_number
HAVING COUNT(*) = (
    SELECT COUNT(*)
    FROM Orders
    GROUP BY customer_number
    ORDER BY COUNT(*) DESC
    LIMIT 1
);

```

---

## customer-who-visited-but-did-not-make-any-transactions

```mysql
# Write your MySQL query statement below

select 
    customer_id, 
    count(visit_id) as count_no_trans
from visits 
where visit_id not in (
    select visit_id 
    from transactions
)
group by 1;
```

---

## customers-who-bought-all-products

```mysql
# Write your MySQL query statement below

select customer_id from Customer
group by customer_id having count(distinct product_key) = (select count(*) from Product)
```

---

## customers-who-never-order

```mysql
# Write your MySQL query statement below

SELECT c.name AS Customers
FROM Customers c
LEFT JOIN Orders o ON c.id = o.customerId
WHERE o.id IS NULL;

```

---

## daily-leads-and-partners

```pythondata
import pandas as pd

def daily_leads_and_partners(daily_sales: pd.DataFrame) -> pd.DataFrame:
    # Group by 'date_id', 'make_name', and calculate the number of distinct lead_ids and partner_ids
    result = daily_sales.groupby(['date_id', 'make_name']).agg(
        unique_leads=pd.NamedAgg(column='lead_id', aggfunc='nunique'),
        unique_partners=pd.NamedAgg(column='partner_id', aggfunc='nunique')
    ).reset_index()
    
    return result

```

---

## daily-temperatures

```golang
func dailyTemperatures(temperatures []int) []int {
    n := len(temperatures)
    result := make([]int, n)
    stack := make([]int, 0)

    for i := 0; i < n; i++ {
        for len(stack) > 0 && temperatures[i] > temperatures[stack[len(stack)-1]] {
            idx := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            result[idx] = i - idx
        }
        stack = append(stack, i)
    }

    return result
}

```

---

## day-of-the-year

```javascript
/**
 * @param {string} date
 * @return {number}
 */
var dayOfYear = function(date) {
    date = date.split("-");
    let 
    year  = parseInt(date[0]),
    month = parseInt(date[1]),
    day   = parseInt(date[2]);

    let days = [
        0,
        31,
        28,
        31,
        30,
        31,
        30,
        31,
        31,
        30,
        31,
        30,
        31
    ]

    if (
        !(year % 4) &&
        !!(year % 100) ||
        !(year % 400)
    ) days[2] = 29;

    let total = 0;
    for (let i = 1; i <= month - 1; i++) {
        total += days[i];
    }

    total += day;

    return total;
};
```

---

## debounce

```javascript
/**
 * @param {Function} fn
 * @param {number} t milliseconds
 * @return {Function}
 */
var debounce = function(fn, t) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer=setTimeout(_=>fn(...args), t);
    }
};

/**
 * const log = debounce(console.log, 100);
 * log('Hello'); // cancelled
 * log('Hello'); // cancelled
 * log('Hello'); // Logged at t=100ms
 */
```

---

## decode-string

```golang
func decodeString(s string) string {
	stack := make([]string, 0)
	numStack := make([]int, 0)
	currentString := ""

	for i := 0; i < len(s); i++ {
		if s[i] >= '0' && s[i] <= '9' {
			// Parse the number
			num := 0
			for ; i < len(s) && s[i] >= '0' && s[i] <= '9'; i++ {
				num = num*10 + int(s[i]-'0')
			}
			i-- // Move the index back by one to reprocess the current character

			numStack = append(numStack, num)
		} else if s[i] == '[' {
			// Push the currentString to the stack
			stack = append(stack, currentString)

			// Reset the currentString
			currentString = ""
		} else if s[i] == ']' {
			// Retrieve the previous string from the stack
			prevString := stack[len(stack)-1]
			stack = stack[:len(stack)-1]

			// Retrieve the previous number from the number stack
			num := numStack[len(numStack)-1]
			numStack = numStack[:len(numStack)-1]

			// Repeat the current string by the previous number
			currentString = prevString + strings.Repeat(currentString, num)
		} else {
			// Append the current character to the currentString
			currentString += string(s[i])
		}
	}

	return currentString
}
```

---

## decode-ways

```golang
func numDecodings(s string) int {
    n := len(s)
    if n == 0 {
        return 0
    }

    // Create a DP array to store the number of ways to decode up to i-th character
    dp := make([]int, n+1)
    dp[0] = 1
    if s[0] != '0' {
        dp[1] = 1
    } else {
        return 0
    }

    for i := 2; i <= n; i++ {
        oneDigit, _ := strconv.Atoi(s[i-1 : i])
        twoDigits, _ := strconv.Atoi(s[i-2 : i])

        if oneDigit >= 1 {
            dp[i] += dp[i-1]
        }
        if twoDigits >= 10 && twoDigits <= 26 {
            dp[i] += dp[i-2]
        }
    }

    return dp[n]
}

```

---

## defanging-an-ip-address

```javascript
/**
 * @param {string} address
 * @return {string}
 */
var defangIPaddr = function(address) {
    return address.replaceAll(".", "[.]");
};
```

---

## degree-of-an-array

```golang
func findShortestSubArray(nums []int) int {
    count := make(map[int][]int)

    for i, num := range nums {
        if _, ok := count[num]; !ok {
            count[num] = []int{1, i, i}
        } else {
            count[num][0]++
            count[num][2] = i
        }
    }

    degree := 0
    minLength := 0

    for _, c := range count {
        if c[0] > degree {
            degree = c[0]
            minLength = c[2] - c[1] + 1
        } else if c[0] == degree {
            minLength = min(minLength, c[2]-c[1]+1)
        }
    }

    return minLength
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## delete-columns-to-make-sorted

```golang
func minDeletionSize(strs []string) int {
    n := len(strs)
    m := len(strs[0])
    deletionCount := 0
    
    for j := 0; j < m; j++ {
        for i := 1; i < n; i++ {
            if strs[i][j] < strs[i-1][j] {
                deletionCount++
                break
            }
        }
    }
    
    return deletionCount
}

```

---

## delete-duplicate-emails

```mysql
# Please write a DELETE statement and DO NOT write a SELECT statement.
# Write your MySQL query statement below

delete from Person
where id NOT IN (
    select id
    from (
        select min(id) AS id
        from Person
        group by email
    ) as t
);
```

---

## delete-node-in-a-bst

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} key
 * @return {TreeNode}
 */
var deleteNode = function(root, key) {

    if (root === null) {
        return null;
    }

    if (key < root.val) {
        root.left = deleteNode(root.left, key);
    } else if (key > root.val) {
        root.right = deleteNode(root.right, key);
    } else {
        // Caso 1: Sin hijos o con un solo hijo
        if (root.left === null) {
            return root.right;
        } else if (root.right === null) {
            return root.left;
        }

        // Caso 2: Dos hijos
        // Encontrar el valor minimo en el subarbol a la derecha
        var minValue = findMinValue(root.right);
        root.val = minValue;

        // Eliminar el minimo nodo en el subarbol a la derecha
        root.right = deleteNode(root.right, minValue);
    }

    return root;
};

var findMinValue = function(root) {
    while (root.left !== null) {
        root = root.left
    }
    return root.val;
}
```

---

## delete-the-middle-node-of-a-linked-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteMiddle(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return nil
    }
    
    slow := head
    fast := head
    var prev *ListNode
    
    for fast != nil && fast.Next != nil {
        prev = slow
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    prev.Next = slow.Next
    
    return head
}
```

---

## department-highest-salary

```pythondata
import pandas as pd

def department_highest_salary(employee: pd.DataFrame, department: pd.DataFrame) -> pd.DataFrame:
    merged = pd.merge(employee, department, left_on='departmentId', right_on='id')
    grouped = merged.groupby('name_y').apply(lambda x: x[x['salary'] == x['salary'].max()])
    result = grouped[['name_y', 'name_x', 'salary']].rename(columns={'name_y': 'Department', 'name_x': 'Employee'})
    return result

```

---

## department-top-three-salaries

```mysql
# Write your MySQL query statement below

select d.name as Department, e.name as Employee, e.salary as Salary
from Employee e
join Department d on e.departmentId = d.id
where (
    select count(distinct salary)
    from Employee
    where departmentId = e.departmentId and salary > e.salary
) < 3
order by d.name, e.salary desc

```

---

## design-add-and-search-words-data-structure

```golang
type TrieNode struct {
	children [26]*TrieNode
	isWord   bool
}

type WordDictionary struct {
	root *TrieNode
}

func Constructor() WordDictionary {
	return WordDictionary{
		root: &TrieNode{},
	}
}

func (this *WordDictionary) AddWord(word string) {
	node := this.root
	for _, ch := range word {
		index := ch - 'a'
		if node.children[index] == nil {
			node.children[index] = &TrieNode{}
		}
		node = node.children[index]
	}
	node.isWord = true
}

func (this *WordDictionary) Search(word string) bool {
	return this.searchHelper(word, 0, this.root)
}

func (this *WordDictionary) searchHelper(word string, index int, node *TrieNode) bool {
	if index == len(word) {
		return node.isWord
	}

	ch := word[index]
	if ch != '.' {
		child := node.children[ch-'a']
		if child != nil && this.searchHelper(word, index+1, child) {
			return true
		}
	} else {
		for _, child := range node.children {
			if child != nil && this.searchHelper(word, index+1, child) {
				return true
			}
		}
	}

	return false
}


/**
 * Your WordDictionary object will be instantiated and called as such:
 * obj := Constructor();
 * obj.AddWord(word);
 * param_2 := obj.Search(word);
 */
```

---

## design-authentication-manager

```golang
type AuthenticationManager struct {
    Hash map[string]int
    timeToLive int
}


func Constructor(timeToLive int) AuthenticationManager {
    var a AuthenticationManager
    a.timeToLive = timeToLive
    a.Hash = make(map[string]int)
    return a
}


func (this *AuthenticationManager) Generate(tokenId string, currentTime int)  {
    this.Hash[tokenId] = currentTime + this.timeToLive
} 


func (this *AuthenticationManager) Renew(tokenId string, currentTime int)  {
    if _, ok := this.Hash[tokenId]; ok && this.Hash[tokenId] > currentTime {
        this.Hash[tokenId] = currentTime + this.timeToLive
    }
}


func (this *AuthenticationManager) CountUnexpiredTokens(currentTime int) int {
    for key, val := range this.Hash {
        if (val <= currentTime) {
            delete(this.Hash, key)
        }
    }
    return len(this.Hash)
}


/**
 * Your AuthenticationManager object will be instantiated and called as such:
 * obj := Constructor(timeToLive);
 * obj.Generate(tokenId,currentTime);
 * obj.Renew(tokenId,currentTime);
 * param_3 := obj.CountUnexpiredTokens(currentTime);
 */
```

---

## design-graph-with-shortest-path-calculator

```golang
type Graph struct {
	nodes  int
	adj    map[int]map[int]int
	edges  [][]int
}

func Constructor(n int, edges [][]int) Graph {
	graph := Graph{
		nodes: n,
		adj:   make(map[int]map[int]int),
		edges: edges,
	}

	for _, edge := range edges {
		from, to, cost := edge[0], edge[1], edge[2]
		if _, ok := graph.adj[from]; !ok {
			graph.adj[from] = make(map[int]int)
		}
		graph.adj[from][to] = cost
	}

	return graph
}

func (g *Graph) AddEdge(edge []int) {
	from, to, cost := edge[0], edge[1], edge[2]
	if _, ok := g.adj[from]; !ok {
		g.adj[from] = make(map[int]int)
	}
	g.adj[from][to] = cost
	g.edges = append(g.edges, edge)
}

func (g *Graph) ShortestPath(node1 int, node2 int) int {
	visited := make(map[int]bool)
	distances := make(map[int]int)

	for i := 0; i < g.nodes; i++ {
		distances[i] = math.MaxInt32
	}
	distances[node1] = 0

	for i := 0; i < g.nodes-1; i++ {
		minNode := -1
		minDistance := math.MaxInt32

		for j := 0; j < g.nodes; j++ {
			if !visited[j] && distances[j] < minDistance {
				minNode = j
				minDistance = distances[j]
			}
		}

		visited[minNode] = true

		for to, cost := range g.adj[minNode] {
			if distances[minNode]+cost < distances[to] {
				distances[to] = distances[minNode] + cost
			}
		}
	}

	if distances[node2] == math.MaxInt32 {
		return -1
	}

	return distances[node2]
}

/**
 * Your Graph object will be instantiated and called as such:
 * obj := Constructor(n, edges);
 * obj.AddEdge(edge);
 * param_2 := obj.ShortestPath(node1,node2);
 */
```

---

## design-hashmap

```golang
type MyHashMap struct {
    data map[int]int
}

func Constructor() MyHashMap {
    return MyHashMap{data: make(map[int]int)}
}

func (this *MyHashMap) Put(key int, value int) {
    this.data[key] = value
}

func (this *MyHashMap) Get(key int) int {
    if val, ok := this.data[key]; ok {
        return val
    }
    return -1
}

func (this *MyHashMap) Remove(key int) {
    delete(this.data, key)
}
```

---

## design-hashset

```golang
type MyHashSet struct {
	buckets []LinkedList
	size    int
}

type LinkedList struct {
	head *Node
}

type Node struct {
	key  int
	next *Node
}

func Constructor() MyHashSet {
	return MyHashSet{
		buckets: make([]LinkedList, 10000),
		size:    10000,
	}
}

func (this *MyHashSet) Add(key int) {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key already exists in the linked list
	current := bucket.head
	for current != nil {
		if current.key == key {
			return
		}
		current = current.next
	}

	// Add the key to the front of the linked list
	newNode := &Node{
		key:  key,
		next: bucket.head,
	}
	bucket.head = newNode
}

func (this *MyHashSet) Remove(key int) {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key exists in the linked list
	if bucket.head == nil {
		return
	}
	if bucket.head.key == key {
		bucket.head = bucket.head.next
		return
	}

	// Find the key and remove it from the linked list
	prev := bucket.head
	current := prev.next
	for current != nil {
		if current.key == key {
			prev.next = current.next
			return
		}
		prev = current
		current = current.next
	}
}

func (this *MyHashSet) Contains(key int) bool {
	hash := key % this.size
	bucket := &this.buckets[hash]

	// Check if the key exists in the linked list
	current := bucket.head
	for current != nil {
		if current.key == key {
			return true
		}
		current = current.next
	}

	return false
}

```

---

## design-parking-system

```javascript
/**
 * @param {number} big
 * @param {number} medium
 * @param {number} small
 */
var ParkingSystem = function(big, medium, small) {
    this[1] = big;
    this[2] = medium;
    this[3] = small;
};

/** 
 * @param {number} carType
 * @return {boolean}
 */
ParkingSystem.prototype.addCar = function(carType) {
    if (this[carType]) {
        this[carType]--;
        return true;
    } else {
        return false;
    }
};

/** 
 * Your ParkingSystem object will be instantiated and called as such:
 * var obj = new ParkingSystem(big, medium, small)
 * var param_1 = obj.addCar(carType)
 */
```

---

## detect-capital

```javascript
/**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function(word) {
  var uppercaseCount = 0;
  var lowercaseCount = 0;

  for (var i = 0; i < word.length; i++) {
    if (word[i] === word[i].toUpperCase()) {
      uppercaseCount++;
    } else {
      lowercaseCount++;
    }
  }

  if (uppercaseCount === word.length || lowercaseCount === word.length) {
    return true;
  }

  if (uppercaseCount === 1 && word[0] === word[0].toUpperCase()) {
    return true;
  }

  return false;
};

```

---

## determine-color-of-a-chessboard-square

```golang
func squareIsWhite(coordinates string) bool {

    if int(rune(coordinates[0]) - 'a' + 1) % 2 == int(rune(coordinates[1])) % 2{
        return false
    }
    return true
}
```

---

## determine-if-a-cell-is-reachable-at-a-given-time

```golang
func isReachableAtTime(sx, sy, fx, fy, t int) bool {
    width := abs(sx - fx)
    height := abs(sy - fy)

    if width == 0 && height == 0 {
        return t != 1 // Handle the case where start and end are the same cell
    }

    min_time := max(width, height)

    return t >= min_time
}

func abs(x int) int {
    if x < 0 {
        return -x
    }
    return x
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## determine-if-two-strings-are-close

```typescript
function closeStrings(word1: string, word2: string): boolean {
  if (word1.length !== word2.length) {
    return false;
  }

  const count1 = new Map<string, number>();
  const count2 = new Map<string, number>();
  const chars1 = new Set<string>();
  const chars2 = new Set<string>();

  for (const char of word1) {
    count1.set(char, (count1.get(char) || 0) + 1);
    chars1.add(char);
  }

  for (const char of word2) {
    count2.set(char, (count2.get(char) || 0) + 1);
    chars2.add(char);
  }

  const counts1 = Array.from(count1.values()).sort((a, b) => a - b);
  const counts2 = Array.from(count2.values()).sort((a, b) => a - b);

  const chars1Array = Array.from(chars1);
  const chars2Array = Array.from(chars2);

  chars1Array.sort();
  chars2Array.sort();

  return arraysEqual(counts1, counts2) && arraysEqual(chars1Array, chars2Array);
}

function arraysEqual<T>(arr1: T[], arr2: T[]): boolean {
  if (arr1.length !== arr2.length) {
    return false;
  }

  for (let i = 0; i < arr1.length; i++) {
    if (arr1[i] !== arr2[i]) {
      return false;
    }
  }

  return true;
}

```

---

## di-string-match

```golang
func diStringMatch(s string) []int {
    n := len(s)
    result := make([]int, n+1)
    low, high := 0, n
    
    for i := 0; i < n; i++ {
        if s[i] == 'I' {
            result[i] = low
            low++
        } else {
            result[i] = high
            high--
        }
    }
    
    result[n] = low  // or high, they will be equal at this point
    return result
}
```

---

## diameter-of-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func diameterOfBinaryTree(root *TreeNode) int {
	if root == nil {
		return 0
	}

	diameter := 0
	calculateDiameter(root, &diameter)
	return diameter
}

func calculateDiameter(node *TreeNode, diameter *int) int {
	if node == nil {
		return 0
	}

	left := calculateDiameter(node.Left, diameter)
	right := calculateDiameter(node.Right, diameter)

	// Update the diameter if the current path is longer
	*diameter = int(math.Max(float64(*diameter), float64(left+right)))

	// Return the longest path from the current node
	return int(math.Max(float64(left), float64(right))) + 1
}
```

---

## distribute-candies

```javascript
/**
 * @param {number[]} candyType
 * @return {number}
 */
var distributeCandies = function(candyType) {
  const uniqueTypes = new Set(candyType);
  const maxEat = candyType.length / 2;
  
  return Math.min(uniqueTypes.size, maxEat);
};
```

---

## distribute-candies-to-people

```golang
func distributeCandies(candies int, num_people int) []int {
    ans := make([]int, num_people)
    turn := 0

    for candies > 0 {
        for i := 0; i < num_people; i++ {
            giveCandies := min(candies, turn*num_people+i+1)
            ans[i] += giveCandies
            candies -= giveCandies

            if candies <= 0 {
                break
            }
        }
        turn++
    }

    return ans
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## distribute-money-to-maximum-children

```golang
func distMoney(money int, children int) int {
    if money < children {
        return -1
    }

    money -= children

    eightChildren := money / 7
    restMoney := money % 7

    if eightChildren > children {
        return children - 1
    }

    if restMoney == 0 {
        return eightChildren
    }

    if restMoney != 3 {
        if eightChildren == children {
            return children - 1
        }
        return eightChildren
    }

    if eightChildren < children - 1 {
        return eightChildren
    }

    return eightChildren-1

}
```

---

## divide-two-integers

```golang
func divide(dividend int, divisor int) int {

    if divisor == 0 || (dividend == math.MinInt32 && divisor == -1) {
        return math.MaxInt32;
    }

    sign := 1;
    if (dividend < 0 && divisor > 0) || (dividend > 0 && divisor < 0) {
        sign = -1;
    }
    a, b := abs(dividend), abs(divisor)
    quotient := 0
    for a >= b {
        temp, multiple := b, 1
        for a >= (temp << 1) {
            temp <<= 1
            multiple <<= 1
        }
        a -= temp
        quotient += multiple
    }
    return sign*quotient
}

func abs(num int) int {
    if num < 0 {
        return -num
    }
    return num
}
```

---

## divisor-game

```golang
func divisorGame(n int) bool {
    dp := make([]bool, n+1)
    
    // Base case
    dp[1] = false
    
    for i := 2; i <= n; i++ {
        for x := 1; x < i; x++ {
            if i % x == 0 && !dp[i-x] {
                dp[i] = true
                break
            }
        }
    }
    
    return dp[n]
}

```

---

## domino-and-tromino-tiling

```typescript
function numTilings(n: number): number {
    const MOD = 1e9+7;
    const dp: number[] = new Array(n+1).fill(0);

    dp[0] = 1;
    dp[1] = 1;
    dp[2] = 2;

    for (let i = 3; i <= n; i++) {
        dp[i] = (2*dp[i-1] + dp[i-3]) % MOD;
    }

    return dp[n];
};
```

---

## dota2-senate

```typescript
function predictPartyVictory(senate: string): string {
  const radiant = [];
  const dire = [];

  for (let i = 0; i < senate.length; i++) {
    if (senate[i] === 'R') {
      radiant.push(i);
    } else {
      dire.push(i);
    }
  }

  while (radiant.length > 0 && dire.length > 0) {
    if (radiant[0] < dire[0]) {
      radiant.push(radiant[0] + senate.length);
    } else {
      dire.push(dire[0] + senate.length);
    }
    radiant.shift();
    dire.shift();
  }

  return radiant.length > 0 ? 'Radiant' : 'Dire';
}

```

---

## duplicate-emails

```mysql
# Write your MySQL query statement below
select email from Person 
group by email having COUNT(*) > 1;
```

---

## duplicate-zeros

```golang
func duplicateZeros(arr []int) {
    length := len(arr)
    
    for i := 0; i < length-1; i++ {
        if arr[i] == 0 {
            // Shift elements to the right starting from the end of the array
            for j := length - 1; j > i+1; j-- {
                arr[j] = arr[j-1]
            }
            // Duplicate the zero
            arr[i+1] = 0
            i++ // Skip the next element since we've already processed it
        }
    }
}

```

---

## edit-distance

```golang
func minDistance(word1 string, word2 string) int {
    m, n := len(word1), len(word2)

    // Create a 2D array to store the minimum operations
    dp := make([][]int, m+1)
    for i := range dp {
        dp[i] = make([]int, n+1)
    }

    // Initialize the first row and column of the dp array
    for i := 0; i <= m; i++ {
        dp[i][0] = i
    }
    for j := 0; j <= n; j++ {
        dp[0][j] = j
    }

    // Fill in the dp array
    for i := 1; i <= m; i++ {
        for j := 1; j <= n; j++ {
            if word1[i-1] == word2[j-1] {
                dp[i][j] = dp[i-1][j-1] // Characters match, no operation needed
            } else {
                dp[i][j] = 1 + min(min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1])
                // 1 + minimum of (insertion, deletion, substitution)
            }
        }
    }

    return dp[m][n]
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

---

## eliminate-maximum-number-of-monsters

```golang
func eliminateMaximum(dist []int, speed []int) int {
    n := len(dist)
    times := make([]float64, n)
    
    for i := 0; i < n; i++ {
        times[i] = float64(dist[i]) / float64(speed[i])
    }
    
    sort.Float64s(times)
    
    for i := 0; i < n; i++ {
        if float64(i) >= times[i] {
            return i
        }
    }
    
    return n
}

```

---

## employee-bonus

```mysql
# Write your MySQL query statement below

select e.name, b.bonus
from Employee e
left join Bonus b on e.empId = b.empId
where b.bonus < 1000 or b.bonus is null;

```

---

## employees-earning-more-than-their-managers

```mysql
# Write your MySQL query statement below

select e1.name as Employee
from Employee e1
join Employee e2 on e1.managerId = e2.id
where e1.salary > e2.salary
```

---

## employees-whose-manager-left-the-company

```mysql
# Write your MySQL query statement below

select employee_id 
from Employees
where salary < 30000
    and manager_id is not null
    and manager_id not in (
        select employee_id 
        from Employees
    )
order by employee_id;
```

---

## equal-row-and-column-pairs

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var equalPairs = function(grid) {
    let count = 0;
    const n = grid.length;

    // Keep track of the frequency of each row.
    const rowCounter = new Map();
    for (const row of grid) {
        const key = JSON.stringify(row);
        rowCounter.set(key, (rowCounter.get(key) || 0) + 1);
    }

    // Add up the frequency of each column in the map.
    for (let c = 0; c < n; c++) {
        const col = [];
        for (let i = 0; i < n; i++) {
            col.push(grid[i][c]);
        }
        const key = JSON.stringify(col);
        count += rowCounter.get(key) || 0;
    }

    return count;
};
```

---

## erect-the-fence

```golang
func outerTrees(trees [][]int) [][]int {
    n := len(trees)
    if n <= 1 {
        return trees
    }
    
    // Sort the trees based on their x-coordinates (and y-coordinates in case of ties).
    sort.Slice(trees, func(i, j int) bool {
        if trees[i][0] == trees[j][0] {
            return trees[i][1] < trees[j][1]
        }
        return trees[i][0] < trees[j][0]
    })
    
    // Initialize two sets to keep track of the upper and lower hulls.
    upperHull, lowerHull := make([][]int, 0), make([][]int, 0)
    
    // Build the upper hull.
    for i := 0; i < n; i++ {
        for len(upperHull) >= 2 && cross(upperHull[len(upperHull)-2], upperHull[len(upperHull)-1], trees[i]) < 0 {
            upperHull = upperHull[:len(upperHull)-1]
        }
        upperHull = append(upperHull, trees[i])
    }
    
    // Build the lower hull.
    for i := n - 1; i >= 0; i-- {
        for len(lowerHull) >= 2 && cross(lowerHull[len(lowerHull)-2], lowerHull[len(lowerHull)-1], trees[i]) < 0 {
            lowerHull = lowerHull[:len(lowerHull)-1]
        }
        lowerHull = append(lowerHull, trees[i])
    }
    
    // Combine the upper and lower hulls to get the final result.
    result := append(upperHull[:len(upperHull)-1], lowerHull[:len(lowerHull)-1]...)
    
    // Remove duplicates from the result.
    uniqueResult := make([][]int, 0)
    uniqueSet := make(map[[2]int]bool)
    for _, point := range result {
        if !uniqueSet[[2]int{point[0], point[1]}] {
            uniqueSet[[2]int{point[0], point[1]}] = true
            uniqueResult = append(uniqueResult, point)
        }
    }
    
    return uniqueResult
}

func cross(p1, p2, p3 []int) int {
    return (p2[0]-p1[0])*(p3[1]-p1[1]) - (p2[1]-p1[1])*(p3[0]-p1[0])
}

```

---

## evaluate-division

```typescript
function calcEquation(
  equations: string[][],
  values: number[],
  queries: string[][]
): number[] {
  const graph = new Map<string, Map<string, number>>();

  // Build the graph with variable pairs and values
  for (let i = 0; i < equations.length; i++) {
    const [a, b] = equations[i];
    const value = values[i];

    if (!graph.has(a)) {
      graph.set(a, new Map<string, number>());
    }
    if (!graph.has(b)) {
      graph.set(b, new Map<string, number>());
    }

    graph.get(a)!.set(b, value);
    graph.get(b)!.set(a, 1 / value);
  }

  // Evaluate queries using DFS
  const results: number[] = [];
  for (const [c, d] of queries) {
    if (!graph.has(c) || !graph.has(d)) {
      results.push(-1.0); // At least one variable is missing
    } else {
      results.push(dfs(c, d, new Set<string>()));
    }
  }

  return results;

  function dfs(a: string, b: string, visited: Set<string>): number {
    if (a === b) {
      return 1.0; // Found the target variable
    }

    visited.add(a);

    for (const [neighbor, value] of graph.get(a)!.entries()) {
      if (!visited.has(neighbor)) {
        const result = dfs(neighbor, b, visited);
        if (result !== -1.0) {
          return value * result;
        }
      }
    }

    return -1.0; // Cannot find a path to the target variable
  }
}

```

---

## evaluate-reverse-polish-notation

```typescript
function evalRPN(tokens: string[]): number {
  const stack: number[] = [];

  for (const token of tokens) {
    if (isOperator(token)) {
      const operand2 = stack.pop()!;
      const operand1 = stack.pop()!;
      const result = evaluateExpression(operand1, operand2, token);
      stack.push(result);
    } else {
      stack.push(parseInt(token));
    }
  }

  return stack.pop()!;
}

function isOperator(token: string): boolean {
  return token === "+" || token === "-" || token === "*" || token === "/";
}

function evaluateExpression(operand1: number, operand2: number, operator: string): number {
  switch (operator) {
    case "+":
      return operand1 + operand2;
    case "-":
      return operand1 - operand2;
    case "*":
      return operand1 * operand2;
    case "/":
      return Math.trunc(operand1 / operand2);
    default:
      throw new Error("Invalid operator");
  }
}

```

---

## event-emitter

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
    this.subscriptionId = 0;
  }

  subscribe(event, cb) {
    if (!this.events[event]) {
      this.events[event] = {};
    }

    const subscriptionId = this.subscriptionId++;
    this.events[event][subscriptionId] = cb;

    return {
      unsubscribe: () => {
        delete this.events[event][subscriptionId];
      },
    };
  }

  emit(event, args = []) {
    if (!this.events[event]) {
      return [];
    }

    const callbacks = Object.values(this.events[event]);
    return callbacks.map(cb => cb(...args));
  }
}


/**
 * const emitter = new EventEmitter();
 *
 * // Subscribe to the onClick event with onClickCallback
 * function onClickCallback() { return 99 }
 * const sub = emitter.subscribe('onClick', onClickCallback);
 *
 * emitter.emit('onClick'); // [99]
 * sub.unsubscribe(); // undefined
 * emitter.emit('onClick'); // []
 */
```

---

## excel-sheet-column-number

```golang
func titleToNumber(columnTitle string) int {
	result := 0

	for _, ch := range columnTitle {
		digit := int(ch - 'A' + 1)
		result = result*26 + digit
	}

	return result
}

```

---

## excel-sheet-column-title

```golang
func convertToTitle(columnNumber int) string {
	var result string

	for columnNumber > 0 {
		columnNumber--  // Adjust columnNumber to be 0-based
		result = string('A'+columnNumber%26) + result
		columnNumber /= 26
	}

	return result
}
```

---

## exchange-seats

```mysql
SELECT  
  IF(id % 2 = 0 , id-1 ,IF(id != ( SELECT MAX(id) FROM SEAT ),id+1,id)) AS id,
  student
FROM SEAT
ORDER BY id;
```

---

## execute-asynchronous-functions-in-parallel

```javascript
/**
 * @param {Array<Function>} functions
 * @return {Promise<any>}
 */
var promiseAll = async function(functions) {
  return new Promise((resolve, reject) => {
    let ans = [];
    let j = functions.length;
    functions.forEach((func, i) => {
      func()
      .then(r => (ans[i] = r, --j == 0 && resolve(ans)))
      .catch(reject)
    })
  })
};



/**
 * const promise = promiseAll([() => new Promise(res => res(42))])
 * promise.then(console.log); // [42]
 */
```

---

## factorial-trailing-zeroes

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var trailingZeroes = function(n) {
  let count = 0;
  
  // Count the number of multiples of 5 in the factorial
  while (n >= 5) {
    count += Math.floor(n / 5);
    n = Math.floor(n / 5);
  }
  
  return count;
};
```

---

## fair-candy-swap

```javascript
/**
 * @param {number[]} aliceSizes
 * @param {number[]} bobSizes
 * @return {number[]}
 */
var fairCandySwap = function(aliceSizes, bobSizes) {
    const sumAlice = aliceSizes.reduce((acc, curr) => acc + curr, 0);
    const sumBob = bobSizes.reduce((acc, curr) => acc + curr, 0);
    const diff = (sumAlice - sumBob) / 2;

    const setBob = new Set(bobSizes);
    for (const candy of aliceSizes) {
        const target = candy - diff;
        if (setBob.has(target)) {
            return [candy, target];
        }
    }
};
```

---

## fibonacci-number

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {
    if(n < 2) return n;

    let next, prev = 0; curr = 1;
    for(let i = 2; i <= n; i++){
        next = prev + curr;
        prev = curr;
        curr = next;
    }
    return next;
};
```

---

## filter-elements-from-array

```javascript
/**
 * @param {number[]} arr
 * @param {Function} fn
 * @return {number[]}
 */
var filter = function(arr, fn) {
    const filtered = [];
    for (let i = 0; i < arr.length; i++) {
        const result = fn(arr[i], i);
        if (result) filtered.push(arr[i]);
    }
    return filtered;
};
```

---

## find-all-anagrams-in-a-string

```typescript
function findAnagrams(s: string, p: string): number[] {
    const result: number[] = [];
    const pMap = new Map<string, number>();
    let windowStart = 0;
    let matched = 0;

    // Create a frequency map of characters in string p
    for (const char of p) {
        pMap.set(char, (pMap.get(char) || 0) + 1);
    }

    // Slide the window over string s
    for (let windowEnd = 0; windowEnd < s.length; windowEnd++) {
        const rightChar = s[windowEnd];

        // Decrement the frequency of the character going out of the window
        if (pMap.has(rightChar)) {
        pMap.set(rightChar, pMap.get(rightChar)! - 1);
        if (pMap.get(rightChar) === 0) {
            matched++;
        }
        }

        // If all characters are matched, add the window start index to the result
        if (matched === pMap.size) {
        result.push(windowStart);
        }

        // Slide the window by one character
        if (windowEnd >= p.length - 1) {
        const leftChar = s[windowStart];
        windowStart++;

        // Increment the frequency of the character going into the window
        if (pMap.has(leftChar)) {
            if (pMap.get(leftChar) === 0) {
            matched--;
            }
            pMap.set(leftChar, pMap.get(leftChar)! + 1);
        }
        }
    }

    return result;
}

```

---

## find-all-numbers-disappeared-in-an-array

```golang
func findDisappearedNumbers(nums []int) []int {
    n := len(nums)
    if n == 0 { return nil }
    res := make([]int, n)
    for _, num := range nums {
        res[num-1] = num
    }
    j := 0
    for i := 0; i < n; i++ {
        if res[i] == 0 {
            res[j] = i + 1
            j++
        }
    }
    return res[:j]
}
```

---

## find-common-characters

```golang
func commonChars(words []string) []string {
    if len(words) == 0 {
        return nil
    }

    // Initialize a hashmap to store character frequencies in the first word
    charCount := make(map[rune]int)
    for _, char := range words[0] {
        charCount[char]++
    }

    // Iterate through the remaining words to update character frequencies
    for i := 1; i < len(words); i++ {
        wordCount := make(map[rune]int)
        for _, char := range words[i] {
            wordCount[char]++
        }

        // Update the character frequencies in charCount to maintain minimum counts
        for char, count := range charCount {
            if wordCount[char] < count {
                charCount[char] = wordCount[char]
            }
        }
    }

    // Create a result slice with the common characters
    var result []string
    for char, count := range charCount {
        for i := 0; i < count; i++ {
            result = append(result, string(char))
        }
    }

    return result
}

```

---

## find-customer-referee

```mysql
# Write your MySQL query statement below

select name from Customer where referee_id is null or referee_id <> 2;
```

---

## find-first-and-last-position-of-element-in-sorted-array

```rust
impl Solution {
    pub fn search_range(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut result = vec![-1, -1];
        if nums.is_empty() {
            return result;
        }

        let first_occurrence = Solution::find_first_occurrence(&nums, target);
        if first_occurrence == -1 {
            return result;
        }

        let last_occurrence = Solution::find_last_occurrence(&nums, target);
        result[0] = first_occurrence;
        result[1] = last_occurrence;
        result
    }

    fn find_first_occurrence(nums: &Vec<i32>, target: i32) -> i32 {
        let mut left = 0;
        let mut right = nums.len() as i32 - 1;
        let mut first_occurrence = -1;

        while left <= right {
            let mid = left + (right - left) / 2;
            if nums[mid as usize] == target {
                first_occurrence = mid;
                right = mid - 1;
            } else if nums[mid as usize] < target {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        first_occurrence
    }

    fn find_last_occurrence(nums: &Vec<i32>, target: i32) -> i32 {
        let mut left = 0;
        let mut right = nums.len() as i32 - 1;
        let mut last_occurrence = -1;

        while left <= right {
            let mid = left + (right - left) / 2;
            if nums[mid as usize] == target {
                last_occurrence = mid;
                left = mid + 1;
            } else if nums[mid as usize] < target {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        last_occurrence
    }
}

```

---

## find-followers-count

```mysql
# Write your MySQL query statement below

select user_id, count(follower_id) as followers_count 
from Followers
group by user_id
order by user_id asc;

```

---

## find-in-mountain-array

```golang
/**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * type MountainArray struct {
 * }
 *
 * func (this *MountainArray) get(index int) int {}
 * func (this *MountainArray) length() int {}
 */

func findInMountainArray(target int, mountainArr *MountainArray) int {
    // Find the peak index using binary search
    n := mountainArr.length()
    left, right := 0, n-1
    peak := -1

    for left < right {
        mid := left + (right-left)/2
        if mountainArr.get(mid) < mountainArr.get(mid+1) {
            left = mid + 1
        } else {
            right = mid
        }
    }
    peak = left

    // Binary search in the increasing part of the mountain array
    left, right = 0, peak
    for left <= right {
        mid := left + (right-left)/2
        midVal := mountainArr.get(mid)
        if midVal == target {
            return mid
        } else if midVal < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    // Binary search in the decreasing part of the mountain array
    left, right = peak, n-1
    for left <= right {
        mid := left + (right-left)/2
        midVal := mountainArr.get(mid)
        if midVal == target {
            return mid
        } else if midVal < target {
            right = mid - 1
        } else {
            left = mid + 1
        }
    }

    return -1
}
```

---

## find-k-closest-elements

```javascript
/**
 * @param {number[]} arr
 * @param {number} k
 * @param {number} x
 * @return {number[]}
 */
var findClosestElements = function(arr, k, x) {
    arr.sort((a, b) => {
        const 
        a1 = Math.abs(a-x),
        b1 = Math.abs(b-x);
        return a1 == b1 ? a-b : a1-b1;
    });
    return arr.splice(0,k).sort((a,b) => a-b);
};
```

---

## find-k-pairs-with-smallest-sums

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[][]}
 */
var kSmallestPairs = function(nums1, nums2, k) {
    
    if (nums1.length === 0 || nums2.length === 0) return []
    
    let arr = [];
    let max = -Infinity;
    
    for (let i = 0; i < nums1.length; i++) {
        for (let j = 0; j < nums2.length; j++) {

            let obj = {
                sum: nums1[i] + nums2[j],
                nums: [nums1[i], nums2[j]]
            }
            
            if (obj.sum >= max && arr.length >= k) {
                break;
            } else if (obj.sum <= max && arr.length < k) {
                arr.push(obj);
            } else if (obj.sum > max && arr.length < k) {
                max = obj.sum; 
                arr.push(obj);
            } else if (obj.sum < max && arr.length >= k) {
                let newMax = -Infinity;
                let replaced = false;
                for (let n = 0; n < arr.length; n++) {
                    if (!replaced && arr[n].sum === max) {
                        arr[n] = obj;
                        replaced = true;
                    }
                    if (arr[n].sum > newMax) newMax = arr[n].sum
                }
                max = newMax;
            } 
        }
    }
    
    return arr.map(obj => obj.nums);
    
};
```

---

## find-largest-value-in-each-tree-row

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
function largestValues(root) {
    if (!root) return [];
    
    const result = [];
    const queue = [root];
    
    while (queue.length) {
        let curr_level_size = queue.length;
        let max_val = Number.MIN_SAFE_INTEGER;
        
        for (let i = 0; i < curr_level_size; i++) {
            const node = queue.shift();
            max_val = Math.max(max_val, node.val);
            
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        
        result.push(max_val);
    }
    
    return result;
}
```

---

## find-median-from-data-stream

```golang
type MaxHeap []int
func (m MaxHeap) Len() int { return len(m) }
func (m MaxHeap) Less(i, j int) bool { return m[i] > m[j] }
func (m MaxHeap) Swap(i, j int) { m[i], m[j] = m[j], m[i] }
func (m *MaxHeap) Pop() interface{} {
    v := (*m)[len(*m)-1]
    *m = (*m)[:len(*m)-1]
    return v
}
func (m *MaxHeap) Push(v interface{}) { *m = append(*m, v.(int)) }
func (m MaxHeap) Top() int { return m[0] }

type MinHeap []int
func (m MinHeap) Len() int { return len(m) }
func (m MinHeap) Less(i, j int) bool { return m[i] < m[j] }
func (m MinHeap) Swap(i, j int) { m[i], m[j] = m[j], m[i] }
func (m *MinHeap) Pop() interface{} {
    v := (*m)[len(*m)-1]
    *m = (*m)[:len(*m)-1]
    return v
}
func (m *MinHeap) Push(v interface{}) { *m = append(*m, v.(int)) }
func (m MinHeap) Top() int { return m[0] }

type MedianFinder struct {
    left MaxHeap
    right MinHeap    
}

func Constructor() MedianFinder {
    return MedianFinder{}    
}

func (mf *MedianFinder) AddNum(num int)  {
    if len(mf.left) + len(mf.right) == 0 {
        heap.Push(&(mf.left), num)
        return
    }
    for {
        if len(mf.left) < len(mf.right) {
            if num <= mf.right.Top() {
                heap.Push(&(mf.left), num)
                return
            } else {
                v := heap.Pop(&(mf.right))
                heap.Push(&(mf.left), v)
            }
        } else {
            if num >= mf.left.Top() {
                heap.Push(&(mf.right), num)
                return
            } else {
                v := heap.Pop(&(mf.left))
                heap.Push(&(mf.right), v)
            }
        }
    }
}

func (mf *MedianFinder) FindMedian() float64 {
    if len(mf.left) == len(mf.right) {
        return float64(mf.left.Top() + mf.right.Top()) / 2.0
    } else if len(mf.left) > len(mf.right) {
        return float64(mf.left.Top())
    } else {
        return float64(mf.right.Top())
    }   
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * obj := Constructor();
 * obj.AddNum(num);
 * param_2 := obj.FindMedian();
 */
```

---

## find-minimum-in-rotated-sorted-array

```golang
func findMin(nums []int) int {
    return backtrack(nums, 0, len(nums)-1)
}

func backtrack(nums []int, left, right int) int {
    // If the array is not rotated, the first element is the minimum
    if nums[left] <= nums[right] {
        return nums[left]
    }

    // Binary search
    mid := left + (right-left)/2

    // Check if the mid element is the minimum
    if mid > left && nums[mid] < nums[mid-1] {
        return nums[mid]
    }

    // Check if the mid+1 element is the minimum
    if mid < right && nums[mid+1] < nums[mid] {
        return nums[mid+1]
    }

    // Recurse on the unsorted side of the array
    if nums[mid] > nums[right] {
        return backtrack(nums, mid+1, right)
    } else {
        return backtrack(nums, left, mid-1)
    }
}
```

---

## find-mode-in-binary-search-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findMode(root *TreeNode) []int {
    var result []int // Un slice para almacenar los modos
    var prev *TreeNode // Un puntero al nodo previo para comparar con el nodo actual
    var currentCount, maxCount int // Contadores para el nodo actual y el nodo maximo
    
    // Funcion para realizar un recorrido in-order del arbol
    var inOrderTraversal func(node *TreeNode)
    inOrderTraversal = func(node *TreeNode) {
        if node == nil {
            return
        }

        // Recorrer el subarbol izquierdo
        inOrderTraversal(node.Left)

        // Comparar el valor del nodo actual con el nodo previo.
        if prev != nil && node.Val == prev.Val {
            currentCount ++
        } else {
            currentCount = 1
        }

        // Actualiza el nodo previo.
        prev = node

        // Comprueba si el conteo actual es mayor o igual al maximo conteo
        if currentCount == maxCount {
            // Agrega el valor actual al nodo
            result = append(result, node.Val)
        } else if currentCount > maxCount {
            // Nuevo valor con un conteo mayor
            result = []int{node.Val}
            maxCount = currentCount
        }

        // Recorre el subarbol derecho
        inOrderTraversal(node.Right)
    }

    // Inicializa la funcion de recorrido in-order desdde el nodo raiz
    inOrderTraversal(root)

    return result

}
```

---

## find-peak-element

```typescript
function findPeakElement(nums: number[]): number {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] > nums[mid + 1]) {
      // The peak is in the left half
      right = mid;
    } else {
      // The peak is in the right half
      left = mid + 1;
    }
  }

  return left;
}
```

---

## find-pivot-index

```typescript
function pivotIndex(nums: number[]): number {
  const totalSum = nums.reduce((sum, num) => sum + num, 0);
  let leftSum = 0;

  for (let i = 0; i < nums.length; i++) {
    const rightSum = totalSum - leftSum - nums[i];
    if (leftSum === rightSum) {
      return i;
    }
    leftSum += nums[i];
  }

  return -1;
}

```

---

## find-smallest-letter-greater-than-target

```golang
func nextGreatestLetter(letters []byte, target byte) byte {
    n := len(letters)
    start := 0
    end := n - 1

    for start <= end {
        mid := start + (end-start)/2
        if letters[mid] <= target {
            start = mid + 1
        } else {
            end = mid - 1
        }
    }

    if start < n {
        return letters[start]
    }
    return letters[0]
}

```

---

## find-the-difference

```golang
func findTheDifference(s string, t string) byte {
	var result byte

	for i := 0; i < len(s); i++ {
		result ^= s[i] ^ t[i]
	}
	result ^= t[len(t)-1]

	return result
}

/*
In this implementation, the findTheDifference function takes two strings s and t and returns the extra letter added to t.

We iterate over the characters of s using a for loop and perform XOR (^) operation between the characters of s and t at each position. This XOR operation cancels out the corresponding bits between the characters, leaving only the extra letter in the result. Finally, we perform XOR between the result and the last character of t to include the extra letter added at the end.
*/
```

---

## find-the-difference-of-two-arrays

```typescript
function findDifference(nums1: number[], nums2: number[]): number[][] {
  const set1 = new Set(nums1);
  const set2 = new Set(nums2);

  const answer: number[][] = [];

  const distinctNums1: number[] = [];
  const distinctNums2: number[] = [];

  for (const num of set1) {
    if (!set2.has(num)) {
      distinctNums1.push(num);
    }
  }

  for (const num of set2) {
    if (!set1.has(num)) {
      distinctNums2.push(num);
    }
  }

  answer.push(distinctNums1);
  answer.push(distinctNums2);

  return answer;
}

```

---

## find-the-duplicate-number

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
 //Floyd's Tortoise
var findDuplicate = function(nums) {
  let slow = nums[0];
  let fast = nums[0];

  // Move slow by 1 step and fast by 2 steps until they meet
  do {
    slow = nums[slow];
    fast = nums[nums[fast]];
  } while (slow !== fast);

  // Move slow back to the start and keep fast at the meeting point
  slow = nums[0];
  while (slow !== fast) {
    slow = nums[slow];
    fast = nums[fast];
  }

  return slow; // Return the repeated number
};
```

---

## find-the-highest-altitude

```typescript
function largestAltitude(gain: number[]): number {
  let maxAltitude = 0; // Maximum altitude
  let currentAltitude = 0; // Current altitude

  for (let i = 0; i < gain.length; i++) {
    currentAltitude += gain[i]; // Update the current altitude
    maxAltitude = Math.max(maxAltitude, currentAltitude); // Update the maximum altitude
  }

  return maxAltitude;
}

```

---

## find-the-index-of-the-first-occurrence-in-a-string

```c
int strStr(char* haystack, char* needle) {
    int haystackLen = strlen(haystack);
    int needleLen = strlen(needle);

    if (needleLen == 0) {
        return 0; // Needle is an empty string, it's always found at index 0.
    }

    if (haystackLen < needleLen) {
        return -1; // Needle is longer than haystack, it can't be found.
    }

    for (int i = 0; i <= haystackLen - needleLen; i++) {
        int j;
        for (j = 0; j < needleLen; j++) {
            if (haystack[i + j] != needle[j]) {
                break; // If characters don't match, break the inner loop.
            }
        }
        if (j == needleLen) {
            return i; // All characters matched, found a match.
        }
    }

    return -1; // No match found.
}

```

---

## find-the-k-or-of-an-array

```golang
func findKOr(nums []int, k int) int {
    maxBit := 32 // Considering integers are 32-bit
	result := 0

	for i := 0; i < maxBit; i++ {
		if countBitsSet(nums, i) >= k {
			result |= 1 << i
		}
	}

	return result
}

func countBitsSet(nums []int, bit int) int {
	count := 0
	for _, num := range nums {
		if num&(1<<bit) != 0 {
			count++
		}
	}
	return count
}
```

---

## find-the-original-array-of-prefix-xor

```golang
func findArray(pref []int) []int {
    result := make([]int, len(pref))
    result[0] = pref[0]
    for i := 1; i < len(pref); i++ {
        result[i] = pref[i] ^ pref[i-1]
    }
    return result
}
```

---

## find-the-town-judge

```golang
func findJudge(n int, trust [][]int) int {
    // Initialize arrays to count trusts given and received
    trustGiven := make([]int, n+1)
    trustReceived := make([]int, n+1)

    for _, relation := range trust {
        a, b := relation[0], relation[1]
        trustGiven[a]++
        trustReceived[b]++
    }

    for i := 1; i <= n; i++ {
        if trustReceived[i] == n-1 && trustGiven[i] == 0 {
            return i
        }
    }

    return -1
}

```

---

## find-the-winner-of-an-array-game

```golang
func getWinner(arr []int, k int) int {
    maxNum := arr[0]
    consecutiveWins := 0

    for i := 1; i < len(arr); i++ {
        if arr[i] > maxNum {
            maxNum = arr[i]
            consecutiveWins = 1
        } else {
            consecutiveWins++
        }

        if consecutiveWins == k {
            return maxNum
        }

        if i == len(arr)-1 {
            i = 0 // Restart the game if no winner in a round
        }
    }

    return maxNum
}

```

---

## find-total-time-spent-by-each-employee

```pythondata
import pandas as pd

def total_time(employees: pd.DataFrame) -> pd.DataFrame:
    # Calculate the total time spent by each employee on each day
    employees['total_time'] = employees['out_time'] - employees['in_time']
    
    # Group by 'event_day' and 'emp_id', then sum the total_time for each group
    result = employees.groupby(['event_day', 'emp_id'])['total_time'].sum().reset_index()
    
    # Rename columns for the output
    result.columns = ['day', 'emp_id', 'total_time']
    
    return result
```

---

## find-users-with-valid-e-mails

```mysql
# Write your MySQL query statement below

select user_id, name, mail 
from users
where mail regexp '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$';
```

---

## first-bad-version

```golang
/** 
 * Forward declaration of isBadVersion API.
 * @param   version   your guess about first bad version
 * @return 	 	      true if current version is bad 
 *			          false if current version is good
 * func isBadVersion(version int) bool;
 */

func firstBadVersion(n int) int {
    left := 1
    right := n

    for left < right {
        mid := left + (right-left)/2
        
        if isBadVersion(mid) {
            right = mid
        } else {
            left = mid + 1
        }
    }

    return left
}
```

---

## first-missing-positive

```golang
func firstMissingPositive(nums []int) int {
    // Step 1: Move all positive integers to their respective indices
    n := len(nums)
    for i := 0; i < n; i++ {
        for nums[i] > 0 && nums[i] <= n && nums[nums[i]-1] != nums[i] {
            nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]
        }
    }

    // Step 2: Find the first missing positive integer
    for i := 0; i < n; i++ {
        if nums[i] != i+1 {
            return i + 1
        }
    }

    return n + 1
}



```

---

## first-unique-character-in-a-string

```golang
func firstUniqChar(s string) int {
    freq := make(map[rune]int)
    
    // Count frequencies of characters in the string
    for _, ch := range s {
        freq[ch]++
    }
    
    // Find the first character with frequency 1
    for i, ch := range s {
        if freq[ch] == 1 {
            return i
        }
    }
    
    return -1
}

```

---

## fix-names-in-a-table

```mysql
# Write your MySQL query statement below

select user_id, concat(upper(substring(name, 1, 1)), lower(substring(name, 2))) AS name
from Users
order by user_id;

```

---

## fizz-buzz

```golang
func fizzBuzz(n int) []string {
    result := make([]string, n)
	for i := 1; i <= n; i++ {
		if i%3 == 0 && i%5 == 0 {
			result[i-1] = "FizzBuzz"
		} else if i%3 == 0 {
			result[i-1] = "Fizz"
		} else if i%5 == 0 {
			result[i-1] = "Buzz"
		} else {
			result[i-1] = strconv.Itoa(i)
		}
	}
	return result
}
```

---

## flatten-binary-tree-to-linked-list

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func flatten(root *TreeNode) {
	if root == nil || (root.Left == nil && root.Right == nil) {
		return
	}

	if root.Left != nil {
		flatten(root.Left)

		temp := root.Right
		root.Right = root.Left
		root.Left = nil

		curr := root.Right
		for curr.Right != nil {
			curr = curr.Right
		}

		curr.Right = temp
	}

	flatten(root.Right)
}
```

---

## flatten-deeply-nested-array

```javascript
/**
 * @param {any[]} arr
 * @param {number} depth
 * @return {any[]}
 */
var flat = function (arr, n) {
  function flattenHelper(arr, depth) {
    const flattened = [];
    for (const elem of arr) {
      if (Array.isArray(elem) && depth < n) {
        flattened.push(...flattenHelper(elem, depth + 1));
      } else {
        flattened.push(elem);
      }
    }
    return flattened;
  }
  
  return flattenHelper(arr, 0);
};

```

---

## flatten-nested-list-iterator

```javascript
class NestedIterator {
    constructor(nestedList) {
        this.flattened = this.flatten(nestedList);
        this.index = 0;
    }

    flatten(nested) {
        let result = [];
        for (let ni of nested) {
            if (ni.isInteger()) {
                result.push(ni.getInteger());
            } else {
                result.push(...this.flatten(ni.getList()));
            }
        }
        return result;
    }

    next() {
        return this.flattened[this.index++];
    }

    hasNext() {
        return this.index < this.flattened.length;
    }
}
```

---

## flipping-an-image

```golang
func flipAndInvertImage(image [][]int) [][]int {
    n := len(image)
    
    // Iterate through each row of the image
    for i := 0; i < n; i++ {
        left := 0
        right := n - 1
        
        // Reverse the row
        for left < right {
            image[i][left], image[i][right] = image[i][right], image[i][left]
            left++
            right--
        }
        
        // Invert the row
        for j := 0; j < n; j++ {
            image[i][j] = 1 - image[i][j]
        }
    }
    
    return image
}

```

---

## flood-fill

```golang
func floodFill(image [][]int, sr int, sc int, newColor int) [][]int {
    if image[sr][sc] == newColor {
        return image
    }
    fill(image, sr, sc, image[sr][sc], newColor)
    return image
}

func fill(image [][]int, sr int, sc int, originalColor int, newColor int) {
    if sr < 0 || sr >= len(image) || sc < 0 || sc >= len(image[0]) || image[sr][sc] != originalColor {
        return
    }
    image[sr][sc] = newColor
    fill(image, sr+1, sc, originalColor, newColor) // Down
    fill(image, sr-1, sc, originalColor, newColor) // Up
    fill(image, sr, sc+1, originalColor, newColor) // Right
    fill(image, sr, sc-1, originalColor, newColor) // Left
}

```

---

## friend-requests-ii-who-has-the-most-friends

```mysql
# Write your MySQL query statement below

select id, count(*) as num
from (
  select requester_id as id
  from RequestAccepted
  union all
  select accepter_id as id
  from RequestAccepted
) as t
group by id
having count(*) = (
  select count(*)
  from (
    select requester_id as id
    from RequestAccepted
    union all
    select accepter_id as id
    from RequestAccepted
  ) as u
  group by id
  order by count(*) desc
  limit 1
);

```

---

## friends-of-appropriate-ages

```golang
func numFriendRequests(ages []int) int {
    count := make([]int, 121)
    for _, age := range ages {
        count[age]++
    }
    
    ans := 0
    for ageA := 1; ageA <= 120; ageA++ {
        countA := count[ageA]
        for ageB := 1; ageB <= 120; ageB++ {
            countB := count[ageB]
            if float64(ageB) <= 0.5*float64(ageA)+float64(7) || ageB > ageA || (ageB > 100 && ageA < 100) {
                continue
            }
            ans += countA * countB
            if ageA == ageB {
                ans -= countA
            }
        }
    }
    return ans
}
```

---

## function-composition

```javascript
/**
 * @param {Function[]} functions
 * @return {Function}
 */
var compose = function(functions) {
    return x => functions.reduceRight((acc,f) => f(acc), x)
};

/**
 * const fn = compose([x => x + 1, x => 2 * x])
 * fn(4) // 9
 */
```

---

## game-of-life

```golang
func gameOfLife(board [][]int) {
	m := len(board)
	n := len(board[0])

	// Helper function to count live neighbors
	countLiveNeighbors := func(row, col int) int {
		count := 0
		for i := row - 1; i <= row+1; i++ {
			for j := col - 1; j <= col+1; j++ {
				if i >= 0 && i < m && j >= 0 && j < n && !(i == row && j == col) {
					count += board[i][j] & 1
				}
			}
		}
		return count
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			liveNeighbors := countLiveNeighbors(i, j)
			if board[i][j] == 1 && (liveNeighbors == 2 || liveNeighbors == 3) {
				// Live cell with 2 or 3 live neighbors survives
				board[i][j] = 3
			}
			if board[i][j] == 0 && liveNeighbors == 3 {
				// Dead cell with 3 live neighbors becomes alive
				board[i][j] = 2
			}
		}
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			// Update the board with the next state
			board[i][j] >>= 1
		}
	}
}

```

---

## game-play-analysis-i

```mysql
# Write your MySQL query statement below

select player_id, min(event_date) as first_login from Activity
group by player_id
```

---

## game-play-analysis-iv

```mysql
# Write your MySQL query statement below

with cte as
(
select *,
  lag(event_date) over(partition by player_id order by event_date) as lag_event_date, 
  min(event_date) over(partition by player_id order by event_date) as min_event_date
from activity
),
cte2 as 
(
  select *, 
  datediff(event_date, min_event_date) as date_difference,
  datediff(event_date, lag_event_date) as date_difference_2
  from cte
),
  total_number_of_players as
(
select count(distinct player_id)
  from cte2
)
select round(count(distinct player_id) / (select * from total_number_of_players),2) as fraction
from cte2
where date_difference  = 1
```

---

## gas-station

```golang
func canCompleteCircuit(gas []int, cost []int) int {
    totalGas := 0
    currentGas := 0
    startIndex := 0

    for i := 0; i < len(gas); i++ {
        totalGas += gas[i] - cost[i]
        currentGas += gas[i] - cost[i]

        if currentGas < 0 {
            // Start from the next station
            startIndex = i + 1
            currentGas = 0
        }
    }

    if totalGas < 0 {
        // Total gas is negative, can't complete the circuit
        return -1
    }

    return startIndex
}
```

---

## generate-a-string-with-characters-that-have-odd-counts

```javascript
/**
 * @param {number} n
 * @return {string}
 */
var generateTheString = function(n) {
    let s = ""
    if (!(n % 2)) {
        s += "a"
        n--;
    }
    s += "b".repeat(n)
    return s;
};

// 4
/*

aaab

*/
```

---

## generate-fibonacci-sequence

```javascript
/**
 * @return {Generator<number>}
 */
var fibGenerator = function*() {
    let prev = 0;
    let curr = 1;

    yield prev;
    yield curr;

    for (let i = 2; i <= 50; i++) {
        const next = prev + curr;
        yield next;
        prev = curr;
        curr = next;
    }
};

/**
 * const gen = fibGenerator();
 * gen.next().value; // 0
 * gen.next().value; // 1
 */
```

---

## generate-parentheses

```golang
func generateParenthesis(n int) []string {
	result := make([]string, 0)
	backtrack(&result, "", 0, 0, n)
	return result
}

func backtrack(result *[]string, current string, open, close, max int) {
	if len(current) == max*2 {
		*result = append(*result, current)
		return
	}

	if open < max {
		backtrack(result, current+"(", open+1, close, max)
	}

	if close < open {
		backtrack(result, current+")", open, close+1, max)
	}
}

```

---

## goat-latin

```golang
func toGoatLatin(sentence string) string {
    words := strings.Fields(sentence) // Split the sentence into words
    vowels := "aeiouAEIOU" // Define the set of vowels
    result := make([]string, 0)

    for i, word := range words {
        if strings.Contains(vowels, string(word[0])) {
            // If the word starts with a vowel, append "ma" and "a" based on the index
            result = append(result, word+"ma"+strings.Repeat("a", i+1))
        } else {
            // If the word starts with a consonant, move the first letter to the end and append "ma" and "a" based on the index
            result = append(result, word[1:]+string(word[0])+"ma"+strings.Repeat("a", i+1))
        }
    }

    return strings.Join(result, " ") // Join the modified words with spaces
}

```

---

## gray-code

```golang
func grayCode(n int) []int {
    result := make([]int, 0, 1<<uint(n))

    for i := 0; i < 1<<uint(n); i++ {
        result = append(result, i^(i>>1))
    }

    return result
}

```

---

## greatest-common-divisor-of-strings

```typescript
function gcdOfStrings(str1: string, str2: string): string {
    if (str1 + str2 !== str2 + str1) {
        // The strings cannot be divided into each other evenly
        return "";
    }

    // Find the greatest common divisor of the lengths
    const gcdLength = gcd(str1.length, str2.length);

    // Extract the substring with length gcdLength from str1
    return str1.substr(0, gcdLength);
    }

    // Helper function to calculate the greatest common divisor using Euclidean algorithm
    function gcd(a: number, b: number): number {
    while (b !== 0) {
        const temp = b;
        b = a % b;
        a = temp;
    }
    return a;
};
```

---

## group-anagrams

```golang
func groupAnagrams(strs []string) [][]string {
    anagramMap := make(map[string][]string)

    for _, str := range strs {
        // Convert the string to a sorted list of characters
        sortedStr := sortString(str)
        
        // Add the string to the corresponding group in the map
        anagramMap[sortedStr] = append(anagramMap[sortedStr], str)
    }

    // Collect the groups of anagrams into a result array
    result := make([][]string, 0, len(anagramMap))
    for _, group := range anagramMap {
        result = append(result, group)
    }

    return result
}

func sortString(str string) string {
    // Convert the string to a list of characters
    chars := strings.Split(str, "")
    
    // Sort the characters in ascending order
    sort.Strings(chars)
    
    // Join the sorted characters to form a string
    return strings.Join(chars, "")
}
```

---

## group-by

```javascript
/**
 * @param {Function} fn
 * @return {Array}
 */
Array.prototype.groupBy = function(fn) {
  return this.reduce(function(result, item) {
    const key = fn(item);
    if (!result[key]) {
      result[key] = [];
    }
    result[key].push(item);
    return result;
  }, {});
};


/**
 * [1,2,3].groupBy(String) // {"1":[1],"2":[2],"3":[3]}
 */
```

---

## group-sold-products-by-the-date

```mysql
# Write your MySQL query statement below

select sell_date, count(distinct product) as num_sold,
group_concat(
  distinct product order by product asc separator ','
) as products
from Activities group by sell_date order by sell_date asc;
```

---

## guess-number-higher-or-lower

```javascript
/** 
 * Forward declaration of guess API.
 * @param {number} num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * var guess = function(num) {}
 */

/**
 * @param {number} n
 * @return {number}
 */
var guessNumber = function(n) {
    let low = 1;
    let high = n;
    while (low <= high) {
        let m = Math.ceil(low + (high - low) / 2);
        let r = guess(m);
        if (r < 0) {
            high = m - 1;
        } else if (r == 0) {
            return m;
        } else {
            low = m + 1;
        }
    }
    return -1;
};
```

---

## h-index

```golang
func hIndex(citations []int) int {
    n := len(citations)
    count := make([]int, n+1)

    // Count the number of papers for each citation
    for _, citation := range citations {
        if citation > n {
            count[n]++
        } else {
            count[citation]++
        }
    }

    // Calculate the h-index
    hIndex := 0
    papers := 0
    for i := n; i >= 0; i-- {
        papers += count[i]
        if papers >= i {
            hIndex = i
            break
        }
    }

    return hIndex
}

```

---

## hamming-distance

```javascript
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var hammingDistance = function(x, y) {
  var xorResult = x ^ y;
  var binaryString = xorResult.toString(2);
  var distance = 0;

  for (var i = 0; i < binaryString.length; i++) {
    if (binaryString[i] === '1') {
      distance++;
    }
  }

  return distance;
};
```

---

## happy-number

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function(n) {
    if (n == 1) return true;
    let seen = [n];
    while (true) {
        n = n
            .toString()
            .split("")
            .map(e => parseInt(e))
            .map(e => e**2)
            .reduce((acc, cur) => acc + cur, 0)
        if (seen.includes(n)) {
            return false;
        }
        seen.push(n);
        if (n == 1) return true;
    }
};
```

---

## height-checker

```golang
func heightChecker(heights []int) int {
    n := len(heights)
    expected := make([]int, n)

    // Copy the given heights into the expected array
    copy(expected, heights)

    // Sort the expected array in non-decreasing order
    sort.Ints(expected)

    // Count the number of differing elements
    count := 0
    for i := 0; i < n; i++ {
        if heights[i] != expected[i] {
            count++
        }
    }

    return count
}

```

---

## house-robber

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function(nums) {
    switch(nums.length) {
        case 0: return 0;
        case 1: return nums[0];
        case 2: return Math.max(nums[0], nums[1]);
    }

    const dp = [];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (let i = 2; i < nums.length; i ++) {
        dp[i] = Math.max(dp[i-2] + nums[i], dp[i-1])
    }

    return dp[dp.length-1]
};
```

---

## image-smoother

```golang
func imageSmoother(img [][]int) [][]int {
    m, n := len(img), len(img[0])
    result := make([][]int, m)
    for i := range result {
        result[i] = make([]int, n)
    }

    directions := []int{-1, 0, 1}

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            sum := 0
            count := 0

            for _, dx := range directions {
                for _, dy := range directions {
                    ni, nj := i+dx, j+dy
                    if ni >= 0 && ni < m && nj >= 0 && nj < n {
                        sum += img[ni][nj]
                        count++
                    }
                }
            }

            result[i][j] = sum / count
        }
    }

    return result
}

```

---

## immediate-food-delivery-i

```pythondata
def food_delivery(delivery: pd.DataFrame) -> pd.DataFrame:
    immediate_orders = delivery[delivery['order_date'] == delivery['customer_pref_delivery_date']]
    total_orders = len(delivery)
    immediate_count = len(immediate_orders)
    immediate_percentage = (immediate_count / total_orders) * 100
    
    result = pd.DataFrame({'immediate_percentage': [round(immediate_percentage, 2)]})
    return result
```

---

## immediate-food-delivery-ii

```mysql
# Write your MySQL query statement below

select round(avg(if(order_date=customer_pref_delivery_date,1,0))*100,2) as  immediate_percentage
from Delivery where (customer_id,order_date) in (
    select customer_id,min(order_date) 
    from Delivery group by customer_id
);
```

---

## implement-queue-using-stacks

```golang
type MyQueue struct {
	stack1 *list.List
	stack2 *list.List
}

func Constructor() MyQueue {
	return MyQueue{
		stack1: list.New(),
		stack2: list.New(),
	}
}

func (q *MyQueue) Push(x int) {
	q.stack1.PushBack(x)
}

func (q *MyQueue) Pop() int {
	if q.stack2.Len() == 0 {
		q.moveStack1ToStack2()
	}

	return q.stack2.Remove(q.stack2.Back()).(int)
}

func (q *MyQueue) Peek() int {
	if q.stack2.Len() == 0 {
		q.moveStack1ToStack2()
	}

	return q.stack2.Back().Value.(int)
}

func (q *MyQueue) Empty() bool {
	return q.stack1.Len() == 0 && q.stack2.Len() == 0
}

func (q *MyQueue) moveStack1ToStack2() {
	for q.stack1.Len() > 0 {
		value := q.stack1.Remove(q.stack1.Back()).(int)
		q.stack2.PushBack(value)
	}
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Peek();
 * param_4 := obj.Empty();
 */

/*
In this implementation, we define a MyQueue struct that contains two stacks (stack1 and stack2) implemented using the container/list package.

The Constructor function initializes the MyQueue struct with the two stacks.

The Push method adds an element to the queue by pushing it onto stack1.

The Pop method removes and returns the element at the front of the queue. If stack2 is empty, it transfers all elements from stack1 to stack2 by calling the moveStack1ToStack2 method. Then, it removes and returns the element from the back of stack2.

The Peek method returns the element at the front of the queue without removing it. If stack2 is empty, it transfers all elements from stack1 to stack2 by calling the moveStack1ToStack2 method. Then, it returns the element at the back of stack2.

The Empty method checks if the queue is empty by examining the lengths of both stack1 and stack2.

The moveStack1ToStack2 method transfers all elements from stack1 to stack2 by removing elements from the back of stack1 and pushing them onto stack2.
*/
```

---

## implement-stack-using-queues

```golang
type MyStack struct {
	queue1 *list.List
	queue2 *list.List
	topVal int
}

func Constructor() MyStack {
	return MyStack{
		queue1: list.New(),
		queue2: list.New(),
		topVal: 0,
	}
}

func (s *MyStack) Push(x int) {
	s.topVal = x
	s.queue1.PushBack(x)
}

func (s *MyStack) Pop() int {
	for s.queue1.Len() > 1 {
		s.topVal = s.queue1.Remove(s.queue1.Front()).(int)
		s.queue2.PushBack(s.topVal)
	}

	value := s.queue1.Remove(s.queue1.Front())
	s.queue1, s.queue2 = s.queue2, s.queue1

	return value.(int)
}

func (s *MyStack) Top() int {
	return s.topVal
}

func (s *MyStack) Empty() bool {
	return s.queue1.Len() == 0
}

/**
 * Your MyStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Empty();
 */

/*
In this implementation, we define a MyStack struct that contains two queues (queue1 and queue2) implemented using the container/list package. We also keep track of the top value of the stack (topVal). The Constructor function initializes the struct with the two queues and the top value set to 0.

The Push method adds an element to the stack by pushing it to queue1 and updating the top value accordingly.

The Pop method removes and returns the element at the top of the stack. It transfers all elements from queue1 to queue2, except for the last element which becomes the new top value. Then, it swaps the queues and returns the last element from the original queue1.

The Top method returns the top value of the stack without removing it.

The Empty method checks if the stack is empty by examining the length of queue1. 
*/
```

---

## implement-trie-prefix-tree

```golang
type TrieNode struct {
	children map[rune]*TrieNode
	isWord   bool
}

type Trie struct {
	root *TrieNode
}

func Constructor() Trie {
	return Trie{
		root: &TrieNode{
			children: make(map[rune]*TrieNode),
			isWord:   false,
		},
	}
}

func (this *Trie) Insert(word string) {
	node := this.root
	for _, ch := range word {
		if _, ok := node.children[ch]; !ok {
			node.children[ch] = &TrieNode{
				children: make(map[rune]*TrieNode),
				isWord:   false,
			}
		}
		node = node.children[ch]
	}
	node.isWord = true
}

func (this *Trie) Search(word string) bool {
	node := this.searchPrefix(word)
	return node != nil && node.isWord
}

func (this *Trie) StartsWith(prefix string) bool {
	node := this.searchPrefix(prefix)
	return node != nil
}

func (this *Trie) searchPrefix(prefix string) *TrieNode {
	node := this.root
	for _, ch := range prefix {
		if _, ok := node.children[ch]; !ok {
			return nil
		}
		node = node.children[ch]
	}
	return node
}


/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
```

---

## increasing-order-search-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
var newRoot, current *TreeNode

func increasingBST(root *TreeNode) *TreeNode {
    newRoot = nil
    current = nil
    inOrderTraversal(root)
    return newRoot
}

func inOrderTraversal(node *TreeNode) {
    if node == nil {
        return
    }
    
    inOrderTraversal(node.Left)
    
    // Create a new node with the same value and set it as the right child
    newNode := &TreeNode{Val: node.Val}
    if newRoot == nil {
        newRoot = newNode
        current = newNode
    } else {
        current.Right = newNode
        current = newNode
    }
    
    inOrderTraversal(node.Right)
}
```

---

## increasing-triplet-subsequence

```typescript
function increasingTriplet(nums: number[]): boolean {
    let smallest = Infinity;
    let secondSmallest = Infinity;

    for (let i = 0; i < nums.length; i++) {
        if (nums[i] <= smallest) {
        smallest = nums[i];
        } else if (nums[i] <= secondSmallest) {
        secondSmallest = nums[i];
        } else {
        // Found a third element greater than both smallest and secondSmallest
        return true;
        }
    }

    return false;
};
```

---

## insert-delete-getrandom-o1

```javascript
var RandomizedSet = function() {
    this.set = [];
    this.map = new Map();
};

RandomizedSet.prototype.insert = function(val) {
    if (this.map.has(val)) {
        return false;
    }
    
    this.set.push(val);
    this.map.set(val, this.set.length - 1);
    return true;
};

RandomizedSet.prototype.remove = function(val) {
    if (!this.map.has(val)) {
        return false;
    }
    
    const index = this.map.get(val);
    const lastElement = this.set[this.set.length - 1];
    
    // Swap the element to be removed with the last element in the set
    this.set[index] = lastElement;
    this.map.set(lastElement, index);
    
    // Remove the last element from the set and the map
    this.set.pop();
    this.map.delete(val);
    
    return true;
};

RandomizedSet.prototype.getRandom = function() {
    const randomIndex = Math.floor(Math.random() * this.set.length);
    return this.set[randomIndex];
};

/** 
 * Your RandomizedSet object will be instantiated and called as such:
 * var obj = new RandomizedSet()
 * var param_1 = obj.insert(val)
 * var param_2 = obj.remove(val)
 * var param_3 = obj.getRandom()
 */
```

---

## insert-interval

```golang
func insert(intervals [][]int, newInterval []int) [][]int {
    merged := make([][]int, 0)
    i := 0

    // Add intervals that end before the new interval starts
    for i < len(intervals) && intervals[i][1] < newInterval[0] {
        merged = append(merged, intervals[i])
        i++
    }

    // Merge overlapping intervals
    for i < len(intervals) && intervals[i][0] <= newInterval[1] {
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i++
    }

    // Add the merged interval
    merged = append(merged, newInterval)

    // Add the remaining intervals
    for i < len(intervals) {
        merged = append(merged, intervals[i])
        i++
    }

    return merged
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## integer-break

```c
int integerBreak(int n) {
    if (n <= 3) {
        return n - 1;
    }

    int dp[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 3;

    for (int i = 4; i <= n; i++) {
        dp[i] = 0;
        for (int j = 1; j <= i / 2; j++) {
            int product = dp[j] * dp[i - j];
            if (product > dp[i]) {
                dp[i] = product;
            }
        }
    }

    return dp[n];
}

```

---

## integer-to-roman

```golang
func intToRoman(num int) string {
    symbols := []string{"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"}
    values := []int{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1}

    roman := ""
    for i := 0; i < len(symbols); i++ {
        for num >= values[i] {
            roman += symbols[i]
            num -= values[i]
        }
    }

    return roman
}
```

---

## interleaving-string

```javascript
/**
 * @param {string} s1
 * @param {string} s2
 * @param {string} s3
 * @return {boolean}
 */
var isInterleave = function(s1, s2, s3) {
  const m = s1.length;
  const n = s2.length;

  if (m + n !== s3.length) {
    return false;
  }

  const dp = new Array(m + 1).fill(false).map(() => new Array(n + 1).fill(false));

  dp[0][0] = true;

  // Check for s1 prefix
  for (let i = 1; i <= m; i++) {
    if (s1[i - 1] === s3[i - 1] && dp[i - 1][0]) {
      dp[i][0] = true;
    }
  }

  // Check for s2 prefix
  for (let j = 1; j <= n; j++) {
    if (s2[j - 1] === s3[j - 1] && dp[0][j - 1]) {
      dp[0][j] = true;
    }
  }

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      const k = i + j - 1;
      if (
        (s1[i - 1] === s3[k] && dp[i - 1][j]) ||
        (s2[j - 1] === s3[k] && dp[i][j - 1])
      ) {
        dp[i][j] = true;
      }
    }
  }

  return dp[m][n];
}
```

---

## intersection-of-two-arrays

```golang
func intersection(nums1 []int, nums2 []int) []int {
    set := make(map[int]bool)
    intersection := []int{}
    
    // Add elements of nums1 to the set
    for _, num := range nums1 {
        set[num] = true
    }
    
    // Find intersection with nums2
    for _, num := range nums2 {
        if set[num] {
            intersection = append(intersection, num)
            set[num] = false // Remove duplicate intersections
        }
    }
    
    return intersection
}

```

---

## intersection-of-two-arrays-ii

```golang
func intersect(nums1 []int, nums2 []int) []int {
    freq := make(map[int]int)
    intersection := []int{}
    
    // Count frequencies of elements in nums1
    for _, num := range nums1 {
        freq[num]++
    }
    
    // Find intersection with nums2 while considering frequencies
    for _, num := range nums2 {
        if freq[num] > 0 {
            intersection = append(intersection, num)
            freq[num]--
        }
    }
    
    return intersection
}

```

---

## intersection-of-two-linked-lists

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
var getIntersectionNode = function(headA, headB) {
  let pA = headA;
  let pB = headB;

  while (pA !== pB) {
    pA = pA ? pA.next : headB; // Move pA to the head of headB if it reaches the end of headA
    pB = pB ? pB.next : headA; // Move pB to the head of headA if it reaches the end of headB
  }

  return pA; // Return the intersected node or null
};
```

---

## interval-cancellation

```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function(fn, args, t) {
    fn(...args);
    let id = setInterval(_ => fn(...args), t);
    return () => clearInterval(id);
};

/**
 *  const result = []
 *
 *  const fn = (x) => x * 2
 *  const args = [4], t = 20, cancelT = 110
 *
 *  const start = performance.now()
 *
 *  const log = (...argsArr) => {
 *		const val = fn(...argsArr)
 *      result.push({"time": Math.floor(performance.now() - start), "returned": fn(...argsArr)})
 *  }
 *       
 *  const cancel = cancellable(log, args, t);
 *           
 *  setTimeout(() => {
 *     cancel()
 *     console.log(result) // [
 *                         //      {"time":0,"returned":8},
 *                         //      {"time":20,"returned":8},
 *                         //      {"time":40,"returned":8},           
 *                         //      {"time":60,"returned":8},
 *                         //      {"time":80,"returned":8},
 *                         //      {"time":100,"returned":8}
 *                         //  ]
 *  }, cancelT)
 */
```

---

## invalid-tweets

```mysql
# Write your MySQL query statement below

select tweet_id from Tweets
where length(content) > 15;
```

---

## invert-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func invertTree(root *TreeNode) *TreeNode {
	if root == nil {
		return nil
	}

	// Invert the left and right subtrees recursively
	root.Left, root.Right = invertTree(root.Right), invertTree(root.Left)

	return root
}
```

---

## investments-in-2016

```mysql
# Write your MySQL query statement below

select round(sum(tiv_2016), 2) as tiv_2016
from Insurance
where tiv_2015 in (
    select tiv_2015
    from Insurance
    group by tiv_2015
    having count(*) > 1
) and (lat, lon) in (
    select lat, lon
    from Insurance
    group by lat, lon
    having count(*) = 1
);
```

---

## ipo

```golang
type project struct {
	capital int
	profit  int
}

type maxHeap []project

func (h maxHeap) Len() int           { return len(h) }
func (h maxHeap) Less(i, j int) bool { return h[i].profit > h[j].profit }
func (h maxHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *maxHeap) Push(x interface{}) {
	*h = append(*h, x.(project))
}

func (h *maxHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[:n-1]
	return x
}

func findMaximizedCapital(k int, w int, profits []int, capital []int) int {
	n := len(profits)
	projects := make([]project, n)
	for i := 0; i < n; i++ {
		projects[i] = project{capital[i], profits[i]}
	}

	sort.Slice(projects, func(i, j int) bool {
		return projects[i].capital < projects[j].capital
	})

	maxHeap := &maxHeap{}
	heap.Init(maxHeap)

	i := 0
	for k > 0 {
		for i < n && projects[i].capital <= w {
			heap.Push(maxHeap, projects[i])
			i++
		}

		if maxHeap.Len() == 0 {
			break
		}

		top := heap.Pop(maxHeap).(project)
		w += top.profit
		k--
	}

	return w
}
```

---

## is-object-empty

```javascript
/**
 * @param {Object | Array} obj
 * @return {boolean}
 */
var isEmpty = function(obj) {
    return ["[]", "{}"].includes(JSON.stringify(obj))
};
```

---

## is-subsequence

```typescript
function isSubsequence(s: string, t: string): boolean {
  let sIndex = 0; // Index for string s
  let tIndex = 0; // Index for string t

  while (sIndex < s.length && tIndex < t.length) {
    if (s[sIndex] === t[tIndex]) {
      // Characters match, move to the next character in s
      sIndex++;
    }
    // Move to the next character in t
    tIndex++;
  }

  // Check if all characters in s have been matched
  return sIndex === s.length;
}

```

---

## island-perimeter

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var islandPerimeter = function(grid) {
  var rows = grid.length;
  var cols = grid[0].length;
  var perimeter = 0;

  for (var i = 0; i < rows; i++) {
    for (var j = 0; j < cols; j++) {
      if (grid[i][j] === 1) {
        perimeter += 4;

        if (i > 0 && grid[i - 1][j] === 1) {
          perimeter -= 2;
        }

        if (j > 0 && grid[i][j - 1] === 1) {
          perimeter -= 2;
        }
      }
    }
  }

  return perimeter;
};
```

---

## isomorphic-strings

```golang
func isIsomorphic(s string, t string) bool {
    if len(s) != len(t) {
        return false
    }
    
    sMap := make(map[byte]byte)
    tMap := make(map[byte]byte)
    
    for i := 0; i < len(s); i++ {
        sChar, sExists := sMap[s[i]]
        tChar, tExists := tMap[t[i]]
        
        if sExists != tExists || (sExists && sChar != t[i]) || (tExists && tChar != s[i]) {
            return false
        }
        
        sMap[s[i]] = t[i]
        tMap[t[i]] = s[i]
    }
    
    return true
}

```

---

## jewels-and-stones

```javascript
/**
 * @param {string} jewels
 * @param {string} stones
 * @return {number}
 */
var numJewelsInStones = function(jewels, stones) {
    let count = 0;
    while (jewels.length) {
        let curr = jewels[0];
        let previus = stones;
        jewels = jewels.replaceAll(curr, "");
        stones = stones.replaceAll(curr, "");
        count += previus.length - stones.length;
    }
    return count;
};
```

---

## join-two-arrays-by-id

```javascript
/**
 * @param {Array} arr1
 * @param {Array} arr2
 * @return {Array}
 */
var join = function(arr1, arr2) {
  var mergedMap = {};

  // Merge objects from arr1
  for (var i = 0; i < arr1.length; i++) {
    var obj = arr1[i];
    var id = obj.id;
    mergedMap[id] = obj;
  }

  // Merge objects from arr2
  for (var j = 0; j < arr2.length; j++) {
    var obj = arr2[j];
    var id = obj.id;
    if (mergedMap[id]) {
      // Merge properties
      for (var prop in obj) {
        mergedMap[id][prop] = obj[prop];
      }
    } else {
      mergedMap[id] = obj;
    }
  }

  // Convert mergedMap values to array
  var joinedArray = Object.values(mergedMap);

  // Sort array by id in ascending order
  joinedArray.sort(function(a, b) {
    return a.id - b.id;
  });

  return joinedArray;
};
```

---

## json-deep-equal

```javascript
/**
 * @param {any} o1
 * @param {any} o2
 * @return {boolean}
 */
var areDeeplyEqual = function(o1, o2) {
    if (Array.isArray(o1) !== Array.isArray(o2)) {
        return false;
    }

    // If the inputs are not objects we can use the strict equality
    if (typeof o1 !== "object" || typeof o2 !== "object" || o1 === null || o2 === null) {
        return o1 === o2;
    }
  
    // Check if both objects have the same keys
    const o1Keys = Object.keys(o1);
    const o2Keys = Object.keys(o2);
    if (o1Keys.length !== o2Keys.length || !o1Keys.every(key => o2.hasOwnProperty(key))) {
        return false; // If the objects dont have the same keys we return false
    }
  
    // Recursively check if the associated values are deeply equal 
    // if all iterations return true the method every return true
    return o1Keys.every(key => areDeeplyEqual(o1[key], o2[key]));
};
```

---

## jump-game

```golang
func canJump(nums []int) bool {
    maxReach := 0 // The maximum index that can be reached so far

    for i := 0; i < len(nums); i++ {
        // If the current index is not reachable, return false
        if i > maxReach {
            return false
        }

        // Update the maximum reach if the current index + jump length is greater
        if i+nums[i] > maxReach {
            maxReach = i + nums[i]
        }

        // If the maximum reach is already the last index, return true
        if maxReach >= len(nums)-1 {
            return true
        }
    }

    return false // The last index is not reachable
}
```

---

## jump-game-ii

```rust
impl Solution {
    pub fn jump(nums: Vec<i32>) -> i32 {
        let mut jumps = 0;
        let mut current_jump_end = 0;
        let mut farthest = 0;

        for i in 0..nums.len() - 1 {
            farthest = farthest.max(i + nums[i] as usize);

            if i == current_jump_end {
                jumps += 1;
                current_jump_end = farthest;
            }
        }

        jumps
    }
}
```

---

## k-th-symbol-in-grammar

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number}
 */
var kthGrammar = function(n, k) {
    if (n === 1) {
        return 0;
    }
    
    // Calculate the mid point of the previous row.
    const mid = Math.pow(2, n - 1) / 2;
    
    // If k is in the first half of the row, it will have the same value as kthGrammar(n - 1, k).
    if (k <= mid) {
        return kthGrammar(n - 1, k);
    }
    // If k is in the second half, it will have the opposite value of k - mid in the previous row.
    return 1 - kthGrammar(n - 1, k - mid);
};
```

---

## keyboard-row

```javascript
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
  var row1 = new Set("qwertyuiop");
  var row2 = new Set("asdfghjkl");
  var row3 = new Set("zxcvbnm");

  var result = [];

  for (var i = 0; i < words.length; i++) {
    var word = words[i].toLowerCase();

    var allInOneRow = true;
    var rowSet = row1;

    if (row2.has(word[0])) {
      rowSet = row2;
    } else if (row3.has(word[0])) {
      rowSet = row3;
    }

    for (var j = 1; j < word.length; j++) {
      if (!rowSet.has(word[j])) {
        allInOneRow = false;
        break;
      }
    }

    if (allInOneRow) {
      result.push(words[i]);
    }
  }

  return result;
};

```

---

## keys-and-rooms

```typescript
function canVisitAllRooms(rooms: number[][]): boolean {
  const n = rooms.length;
  const visited = new Array(n).fill(false);
  visited[0] = true;
  const stack: number[] = [0];

  while (stack.length > 0) {
    const room = stack.pop()!;
    for (const key of rooms[room]) {
      if (!visited[key]) {
        visited[key] = true;
        stack.push(key);
      }
    }
  }

  return visited.every((room) => room);
}

```

---

## kids-with-the-greatest-number-of-candies

```javascript
/**
 * @param {number[]} candies
 * @param {number} extraCandies
 * @return {boolean[]}
 */
var kidsWithCandies = function(candies, extraCandies) {
    const greatest = [];
    candies.forEach((kidcandies, kidcandiesindex) => {
        const sum = kidcandies + extraCandies;
        greatest.push(true);
        candies.forEach((kidcandies2, kidcandiesindex2) => {
            if (kidcandiesindex2 != kidcandiesindex) {
                if (kidcandies2 > sum) {
                    greatest[kidcandiesindex] = false;
                }
            }
        });
    });
    return greatest;
};
```

---

## koko-eating-bananas

```golang
func minEatingSpeed(piles []int, h int) int {
    // Find the maximum pile size
    maxPile := 0
    for _, pile := range piles {
        if pile > maxPile {
            maxPile = pile
        }
    }
    
    // Binary search for the minimum eating speed
    left, right := 1, maxPile
    for left < right {
        mid := left + (right-left)/2
        if canEatAll(piles, h, mid) {
            right = mid
        } else {
            left = mid + 1
        }
    }
    
    return left
}

func canEatAll(piles []int, h, k int) bool {
    hours := 0
    for _, pile := range piles {
        hours += (pile + k - 1) / k
    }
    return hours <= h
}

```

---

## kth-largest-element-in-a-stream

```golang
type KthLargest struct {
	heap *MinHeap
	k    int
}

func Constructor(k int, nums []int) KthLargest {
	h := &MinHeap{}
	heap.Init(h)

	for _, num := range nums {
		if h.Len() < k {
			heap.Push(h, num)
		} else if num > h.Peek() {
			heap.Pop(h)
			heap.Push(h, num)
		}
	}

	return KthLargest{
		heap: h,
		k:    k,
	}
}

func (kl *KthLargest) Add(val int) int {
	if kl.heap.Len() < kl.k {
		heap.Push(kl.heap, val)
	} else if val > kl.heap.Peek() {
		heap.Pop(kl.heap)
		heap.Push(kl.heap, val)
	}

	return kl.heap.Peek()
}

type MinHeap []int

func (h MinHeap) Len() int            { return len(h) }
func (h MinHeap) Less(i, j int) bool  { return h[i] < h[j] }
func (h MinHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }
func (h *MinHeap) Push(x interface{}) { *h = append(*h, x.(int)) }

func (h *MinHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[:n-1]
	return x
}

func (h MinHeap) Peek() int {
	return h[0]
}

```

---

## kth-largest-element-in-an-array

```typescript
function findKthLargest(nums: number[], k: number): number {
  const n = nums.length;
  const targetIndex = n - k; // Index of the kth largest element in the sorted order
  let left = 0;
  let right = n - 1;

  while (left <= right) {
    const pivotIndex = partition(nums, left, right);

    if (pivotIndex === targetIndex) {
      return nums[pivotIndex];
    } else if (pivotIndex < targetIndex) {
      left = pivotIndex + 1;
    } else {
      right = pivotIndex - 1;
    }
  }

  return -1; // Invalid input
}

function partition(nums: number[], left: number, right: number): number {
  const pivot = nums[right];
  let i = left;

  for (let j = left; j < right; j++) {
    if (nums[j] <= pivot) {
      swap(nums, i, j);
      i++;
    }
  }

  swap(nums, i, right);

  return i;
}

function swap(nums: number[], i: number, j: number): void {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

```

---

## kth-largest-sum-in-a-binary-tree

```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthLargestLevelSum(self, root: Optional[TreeNode], k: int) -> int:
        level_sum = defaultdict(int)
        queue = [(root, 0)]

        while queue:
            node, level = queue.pop(0)
            level_sum[level] += node.val
            if node.left:
                queue.append((node.left, level+1))
            if node.right:
                queue.append((node.right, level+1))

        if len(level_sum) < k:
            return -1

        largest_k = nlargest(k, level_sum.values())
        return largest_k[-1]

```

---

## kth-smallest-element-in-a-bst

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function(root, k) {
  let count = 0;
  let result = null;

  function inorder(node) {
    if (node === null) return;

    inorder(node.left);

    count++;
    if (count === k) {
      result = node.val;
      return;
    }

    inorder(node.right);
  }

  inorder(root);
  return result;
};
```

---

## largest-number-at-least-twice-of-others

```golang
func dominantIndex(nums []int) int {
    n := len(nums)
    if n == 1 {
        return 0
    }

    largest := 0
    secondLargest := -1

    for i := 1; i < n; i++ {
        if nums[i] > nums[largest] {
            secondLargest = largest
            largest = i
        } else if secondLargest == -1 || nums[i] > nums[secondLargest] {
            secondLargest = i
        }
    }

    if nums[largest] >= 2*nums[secondLargest] {
        return largest
    }
    return -1
}

```

---

## largest-perimeter-triangle

```golang
func largestPerimeter(nums []int) int {
    sort.Ints(nums)
    n := len(nums)
    maxPerimeter := 0

    for i := n - 1; i >= 2; i-- {
        if nums[i-2]+nums[i-1] > nums[i] {
            // The largest three sides can form a triangle
            maxPerimeter = nums[i-2] + nums[i-1] + nums[i]
            break
        }
    }

    return maxPerimeter
}
```

---

## largest-rectangle-in-histogram

```javascript
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function(heights) {
    const stack = []; // Used to store the indices of the histogram bars
  let maxArea = 0;
  
  // Iterate through each bar in the histogram
  for (let i = 0; i <= heights.length; i++) {
    // Check if the current bar is shorter than the previous bar in the stack
    // Calculate the area of the rectangle formed by the previous bar
    while (stack.length > 0 && (i === heights.length || heights[i] < heights[stack[stack.length - 1]])) {
      const height = heights[stack.pop()]; // Pop the previous bar's index from the stack
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      const area = height * width;
      maxArea = Math.max(maxArea, area);
    }
    
    stack.push(i); // Push the current bar's index into the stack
  }
  
  return maxArea;
};



/**
 * Returns indexes where target appeared
 * @param {number[]} arr
 * @param {number} target
 * @return {number[]} 
*/
const indexesOf = function(arr, target) {
    let indexes = [];
    for (let i = 0; i<arr.length; i++) {
        if (arr[i] == target) {
            indexes.push(i)
        }
    }
    return indexes;
}

/**
 * Returns the biggest number in a number array
 * In this case the tallest height
 * @param {number[]} arr
 * @return {number}
*/
const tallestOf = function(arr) {
    let max = -1;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i]
        }
    }
    return max;
}
```

---

## largest-triangle-area

```golang
func largestTriangleArea(points [][]int) float64 {
    n := len(points)
    maxArea := 0.0

    // Helper function to calculate the area of a triangle given three points
    calcArea := func(p1, p2, p3 []int) float64 {
        return 0.5 * math.Abs(float64(p1[0]*p2[1]+p2[0]*p3[1]+p3[0]*p1[1]-p1[1]*p2[0]-p2[1]*p3[0]-p3[1]*p1[0]))
    }

    // Iterate through all combinations of three points
    for i := 0; i < n-2; i++ {
        for j := i + 1; j < n-1; j++ {
            for k := j + 1; k < n; k++ {
                area := calcArea(points[i], points[j], points[k])
                if area > maxArea {
                    maxArea = area
                }
            }
        }
    }

    return maxArea
}

```

---

## last-moment-before-all-ants-fall-out-of-a-plank

```golang
func getLastMoment(n int, left []int, right []int) int {
    lastMoment := 0

    for _, pos := range left {
        lastMoment = max(lastMoment, pos)
    }

    for _, pos := range right {
        lastMoment = max(lastMoment, n-pos)
    }

    return lastMoment
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## last-person-to-fit-in-the-bus

```mysql
# Write your MySQL query statement below

with cte as (
  select 
    person_id, 
    person_name, 
    sum(weight) over(order by turn) as total_weight 
  from queue
)
select person_name 
from cte
where total_weight <= 1000
order by total_weight desc
limit 1;
```

---

## last-stone-weight

```javascript
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function(stones) {
    while (stones.length > 1) {
        stones.sort((a,b)=>b-a);
        stones[1] = stones[0]-stones[1];
        stones.shift();
    };
    return stones[0];
};
```

---

## leaf-similar-trees

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function leafSimilar(root1: TreeNode | null, root2: TreeNode | null): boolean {
  const leaves1: number[] = [];
  const leaves2: number[] = [];

  getLeaves(root1, leaves1);
  getLeaves(root2, leaves2);

  if (leaves1.length !== leaves2.length) {
    return false;
  }

  for (let i = 0; i < leaves1.length; i++) {
    if (leaves1[i] !== leaves2[i]) {
      return false;
    }
  }

  return true;
}

function getLeaves(node: TreeNode | null, leaves: number[]): void {
  if (node === null) {
    return;
  }

  if (node.left === null && node.right === null) {
    leaves.push(node.val);
  }

  getLeaves(node.left, leaves);
  getLeaves(node.right, leaves);
}
```

---

## lemonade-change

```golang
func lemonadeChange(bills []int) bool {
    // Variables to keep track of the available bills
    fiveBillCount := 0
    tenBillCount := 0
    
    for _, bill := range bills {
        switch bill {
        case 5:
            // Collect a $5 bill
            fiveBillCount++
        case 10:
            // Collect a $10 bill and give back a $5
            if fiveBillCount > 0 {
                fiveBillCount--
                tenBillCount++
            } else {
                return false
            }
        case 20:
            // Collect a $20 bill
            // Give back change of $15 (a $10 bill and a $5 bill)
            if tenBillCount > 0 && fiveBillCount > 0 {
                tenBillCount--
                fiveBillCount--
            } else if fiveBillCount >= 3 {
                fiveBillCount -= 3
            } else {
                return false
            }
        }
    }
    
    return true
}

```

---

## length-of-last-word

```c
int lengthOfLastWord(char* s) {
    int length = 0;
    int i = strlen(s) - 1;

    // Skip trailing spaces
    while (i >= 0 && s[i] == ' ') {
        i--;
    }

    // Count characters of the last word
    while (i >= 0 && s[i] != ' ') {
        length++;
        i--;
    }

    return length;
}

```

---

## letter-combinations-of-a-phone-number

```javascript
/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function(digits) {
    if (!digits) {
        return [];
    }
    const digitMap = {
        '2': ['a', 'b', 'c'],
        '3': ['d', 'e', 'f'],
        '4': ['g', 'h', 'i'],
        '5': ['j', 'k', 'l'],
        '6': ['m', 'n', 'o'],
        '7': ['p', 'q', 'r', 's'],
        '8': ['t', 'u', 'v'],
        '9': ['w', 'x', 'y', 'z'],
    }
    const result = [];
    const generateCombinations = function(combination, digits) {
        if (digits.length === 0) {
            return result.push(combination)
        } else {
            const letters = digitMap[digits.charAt(0)];
            for (let i = 0; i < letters.length; i++) {
                generateCombinations(combination+letters[i], digits.substring(1))
            }
        }
        
    }

    generateCombinations('', digits);

    return result
};
```

---

## license-key-formatting

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var licenseKeyFormatting = function(s, k) {
  // Remove dashes and convert to uppercase
  var formatted = s.replace(/-/g, '').toUpperCase();

  var result = [];
  var count = 0;

  // Iterate over the reversed string
  for (var i = formatted.length - 1; i >= 0; i--) {
    result.push(formatted[i]);
    count++;

    // Insert dashes every k characters
    if (count === k && i > 0) {
      result.push('-');
      count = 0;
    }
  }

  return result.reverse().join('');
};

```

---

## linked-list-cycle

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function hasCycle(head: ListNode | null): boolean {
    if (head === null || head.next === null) {
        return false; // No cycle if there are less than 2 nodes
    }
    
    let tortoise = head;
    let hare = head;
    
    while (hare !== null && hare.next !== null) {
        tortoise = tortoise.next;
        hare = hare.next.next;
        
        if (tortoise === hare) {
            return true; // Cycle detected
        }
    }
    
    return false; // No cycle found
}

```

---

## linked-list-cycle-ii

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
    // Step 1: Check if the list has a cycle
    slow, fast := head, head
    hasCycle := false
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            hasCycle = true
            break
        }
    }
    
    // Step 2: Find the node where the cycle begins
    if hasCycle {
        slow = head
        for slow != fast {
            slow = slow.Next
            fast = fast.Next
        }
        return slow
    }
    
    // Step 3: No cycle found
    return nil
}
```

---

## list-the-products-ordered-in-a-period

```mysql
# Write your MySQL query statement below

select p.product_name, SUM(o.unit) as unit
from Products p
join Orders o on p.product_id = o.product_id
where o.order_date >= '2020-02-01' and o.order_date < '2020-03-01'
group by p.product_name
having unit >= 100;

```

---

## long-pressed-name

```golang
func isLongPressedName(name string, typed string) bool {
    i, j := 0, 0

    for j < len(typed) {
        if i < len(name) && name[i] == typed[j] {
            i++
            j++
        } else if j == 0 || typed[j] != typed[j-1] {
            return false
        } else {
            j++
        }
    }

    return i == len(name)
}
```

---

## longest-common-prefix

```c
char* longestCommonPrefix(char** strs, int strsSize) {
    if (strsSize == 0) {
        return "";
    }

    int minLen = strlen(strs[0]);

    for (int i = 1; i < strsSize; i++) {
        int j = 0;
        while (strs[0][j] && strs[i][j] && strs[0][j] == strs[i][j]) {
            j++;
        }
        if (j < minLen) {
            minLen = j;
        }
    }

    char* result = (char*)malloc((minLen + 1) * sizeof(char));
    strncpy(result, strs[0], minLen);
    result[minLen] = '\0';

    return result;
}
```

---

## longest-common-subsequence

```golang
func longestCommonSubsequence(text1 string, text2 string) int {
    m := len(text1)
    n := len(text2)
    
    // Create a 2D grid to store the lengths of longest common subsequences
    grid := make([][]int, m+1)
    for i := 0; i <= m; i++ {
        grid[i] = make([]int, n+1)
    }
    
    // Calculate the lengths of longest common subsequences
    for i := 1; i <= m; i++ {
        for j := 1; j <= n; j++ {
            if text1[i-1] == text2[j-1] {
                grid[i][j] = grid[i-1][j-1] + 1
            } else {
                grid[i][j] = max(grid[i-1][j], grid[i][j-1])
            }
        }
    }
    
    // Return the length of the longest common subsequence
    return grid[m][n]
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## longest-consecutive-sequence

```golang
func longestConsecutive(nums []int) int {
	if len(nums) == 0 {
		return 0
	}

	numSet := make(map[int]bool)
	for _, num := range nums {
		numSet[num] = true
	}

	longestStreak := 0

	for num := range numSet {
		// Check if the current number is the start of a sequence
		if !numSet[num-1] {
			currentNum := num
			currentStreak := 1

			// Find the length of the consecutive sequence
			for numSet[currentNum+1] {
				currentNum++
				currentStreak++
			}

			// Update the longest streak if necessary
			if currentStreak > longestStreak {
				longestStreak = currentStreak
			}
		}
	}

	return longestStreak
}

```

---

## longest-continuous-increasing-subsequence

```golang
func findLengthOfLCIS(nums []int) int {
    maxLen := 0
    currentLen := 0

    for i := 0; i < len(nums); i++ {
        if i == 0 || nums[i] > nums[i-1] {
            currentLen++
        } else {
            maxLen = max(maxLen, currentLen)
            currentLen = 1
        }
    }

    maxLen = max(maxLen, currentLen)

    return maxLen
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## longest-harmonious-subsequence

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLHS = function(nums) {
  const freqMap = new Map();
  let maxLength = 0;
  
  // Count the frequencies of each number
  for (let num of nums) {
    freqMap.set(num, (freqMap.get(num) || 0) + 1);
  }
  
  // Iterate over the numbers and check for harmonious subsequence
  for (let [num, freq] of freqMap) {
    if (freqMap.has(num + 1)) {
      maxLength = Math.max(maxLength, freq + freqMap.get(num + 1));
    }
    if (freqMap.has(num - 1)) {
      maxLength = Math.max(maxLength, freq + freqMap.get(num - 1));
    }
  }
  
  return maxLength;
};

```

---

## longest-increasing-subsequence

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function(nums) {
    const dp = new Array(nums.length).fill(1); // Initialize dp array with all elements as 1
    let maxLength = 1; // Initialize the maximum length to 1

    for (let i = 1; i < nums.length; i++) {
        for (let j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
        maxLength = Math.max(maxLength, dp[i]);
    }

    return maxLength;
}

```

---

## longest-palindrome

```golang
func longestPalindrome(s string) int {
    freq := make(map[rune]int)
    length := 0
    oddCount := 0
    
    // Count frequencies of characters in the string
    for _, ch := range s {
        freq[ch]++
    }
    
    // Calculate the length of the longest palindrome
    for _, count := range freq {
        length += count / 2 * 2
        if count%2 == 1 {
            oddCount = 1
        }
    }
    
    return length + oddCount
}

```

---

## longest-palindromic-subsequence

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var longestPalindromeSubseq = function(s) {
    const n = s.length;
    const dp = new Array(n).fill(0).map(() => new Array(n).fill(0));
    
    // Initialize diagonal elements to 1
    for (let i = 0; i < n; i++) {
        dp[i][i] = 1;
    }
    
    // Traverse array diagonally and fill in values
    for (let len = 2; len <= n; len++) {
        for (let i = 0; i <= n - len; i++) {
            const j = i + len - 1;
            if (s[i] === s[j]) {
                dp[i][j] = 2 + (len === 2 ? 0 : dp[i+1][j-1]);
            } else {
                dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
            }
        }
    }
    
    return dp[0][n-1];
};
```

---

## longest-palindromic-substring

```golang
func longestPalindrome(s string) string {
    n := len(s)
    dp := make([][]bool, n)
    for i := range dp {
        dp[i] = make([]bool, n)
    }

    var longestPal string
    for l := 0; l < n; l++ {
        for i := 0; i+l < n; i++ {
            j := i + l
            if l == 0 {
                dp[i][j] = true
            } else if l == 1 {
                dp[i][j] = s[i] == s[j]
            } else {
                dp[i][j] = s[i] == s[j] && dp[i+1][j-1]
            }

            if dp[i][j] && l+1 > len(longestPal) {
                longestPal = s[i : j+1]
            }
        }
    }

    return longestPal
}
```

---

## longest-subarray-of-1s-after-deleting-one-element

```typescript
function longestSubarray(nums: number[]): number {
  let maxLength = 0; // Maximum length of subarray
  let left = 0; // Left pointer
  let zerosCount = 0; // Count of zeros

  for (let right = 0; right < nums.length; right++) {
    if (nums[right] === 0) {
      zerosCount++; // Increment the count of zeros

      while (zerosCount > 1) {
        if (nums[left] === 0) {
          zerosCount--; // Decrement the count of zeros
        }
        left++; // Move the left pointer to the right
      }
    }

    maxLength = Math.max(maxLength, right - left);
  }

  return maxLength;
}

```

---

## longest-substring-without-repeating-characters

```golang
func lengthOfLongestSubstring(s string) int {
    charSet := make(map[byte]bool)
    left, right := 0, 0
    maxLength := 0

    for right < len(s) {
        if _, found := charSet[s[right]]; !found {
            charSet[s[right]] = true
            right++
            maxLength = max(maxLength, len(charSet))
        } else {
            delete(charSet, s[left])
            left++
        }
    }

    return maxLength
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## longest-uncommon-subsequence-i

```javascript
/**
 * @param {string} a
 * @param {string} b
 * @return {number}
 */
var findLUSlength = function(a, b) {
   return a !== b ? Math.max(a.length, b.length) : -1; 
};
```

---

## longest-valid-parentheses

```golang
func longestValidParentheses(s string) int {
    stack := []int{-1} // Initialize the stack with -1
    maxLen := 0

    for i, ch := range s {
        if ch == '(' {
            stack = append(stack, i) // Push the index of '(' to the stack
        } else {
            stack = stack[:len(stack)-1] // Pop the top element from the stack

            if len(stack) == 0 {
                stack = append(stack, i) // Push the current index as a potential starting point
            } else {
                currLen := i - stack[len(stack)-1] // Calculate the current valid substring length

                if currLen > maxLen {
                    maxLen = currLen
                }
            }
        }
    }

    return maxLen
}
```

---

## longest-zigzag-path-in-a-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func longestZigZag(root *TreeNode) int {
    if root == nil {
        return 0
    }
    
    maxLen := 0
    dfs(root.Left, 1, 0, &maxLen)
    dfs(root.Right, 1, 1, &maxLen)
    
    return maxLen
}

func dfs(node *TreeNode, length, direction int, maxLen *int) {
    if node == nil {
        return
    }
    
    *maxLen = max(*maxLen, length)
    
    if direction == 0 {
        dfs(node.Left, 1, 0, maxLen)
        dfs(node.Right, length+1, 1, maxLen)
    } else {
        dfs(node.Right, 1, 1, maxLen)
        dfs(node.Left, length+1, 0, maxLen)
    }
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

## lowest-common-ancestor-of-a-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */

func lowestCommonAncestor(root, p, q *TreeNode) *TreeNode {
    // Base case: if the root is nil or matches either of the given nodes, return the root
    if root == nil || root == p || root == q {
        return root
    }

    // Recursively find the lowest common ancestor in the left and right subtrees
    left := lowestCommonAncestor(root.Left, p, q)
    right := lowestCommonAncestor(root.Right, p, q)

    // If both left and right subtrees return a non-nil value, it means p and q are in different subtrees,
    // so the current root is the lowest common ancestor
    if left != nil && right != nil {
        return root
    }

    // If only the left subtree returns a non-nil value, it means both p and q are in the left subtree
    // and the lowest common ancestor is in the left subtree as well
    if left != nil {
        return left
    }

    // If only the right subtree returns a non-nil value, it means both p and q are in the right subtree
    // and the lowest common ancestor is in the right subtree as well
    if right != nil {
        return right
    }

    // If both left and right subtrees return nil, it means p and q are not found in the current subtree
    // Return nil in this case
    return nil
}

```

---

## lru-cache

```golang
type LRUCache struct {
    capacity int
    cache    map[int]*list.Element
    list     *list.List
}

type entry struct {
    key   int
    value int
}

func Constructor(capacity int) LRUCache {
    return LRUCache{
        capacity: capacity,
        cache:    make(map[int]*list.Element),
        list:     list.New(),
    }
}

func (this *LRUCache) Get(key int) int {
    if elem, ok := this.cache[key]; ok {
        this.list.MoveToFront(elem)
        return elem.Value.(*entry).value
    }
    return -1
}

func (this *LRUCache) Put(key int, value int) {
    if elem, ok := this.cache[key]; ok {
        elem.Value.(*entry).value = value
        this.list.MoveToFront(elem)
    } else {
        if this.list.Len() == this.capacity {
            lastElem := this.list.Back()
            delete(this.cache, lastElem.Value.(*entry).key)
            this.list.Remove(lastElem)
        }
        newElem := this.list.PushFront(&entry{key: key, value: value})
        this.cache[key] = newElem
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * obj := Constructor(capacity);
 * param_1 := obj.Get(key);
 * obj.Put(key,value);
 */
```

---

## majority-element

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
  let count = 0;
  let candidate = null;

  for (let num of nums) {
    if (count === 0) {
      candidate = num;
      count = 1;
    } else if (num === candidate) {
      count++;
    } else {
      count--;
    }
  }

  return candidate;
}
```

---

## majority-element-ii

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */

/*
var majorityElement = function(nums) { 
    let hashmap = {};
    let answer = [];
    if (nums.length < 3) {
        return [... new Set(nums)];
    }
    for (let num of nums) {
        if (!hashmap[num]) {
            hashmap[num] = 1;
        } else {
            hashmap[num]++;
            if (hashmap[num] > nums.length/3 && !answer.includes(num)) {
                answer.push(num);
            }
        }
    }
    return answer;
};

*/
var majorityElement = function(nums) {
    let hash = new Map();
    for (const num of nums) {
        hash.set(num, (hash.get(num) || 0) + 1);
    }
    return Array.from(hash.keys()).filter(num => hash.get(num) > nums.length / 3);
}
```

---

## make-array-strictly-increasing

```javascript
/**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @return {number}
 */
var makeArrayIncreasing = function(a, b) {
    // insert -1 as first, insert Infinity as last
    a.unshift(-1), a.push(Infinity)
    
    // ascending
    b = Array.from(new Set(b)).sort((a, b) => a - b)

    // as count
    let n = a.length
    
    // set dp according to count
    let dp = new Array(n).fill(Infinity)
    
    // first 0
    dp[0] = 0
    
    // compare from 1
    for (let i = 1; i < n; i++) {
        let j = search(a[i]);

        for (let k = 1; k <= Math.min(i-1, j); k++) {
            if (a[i-k-1] < b[j - k]) {
                dp[i] = Math.min(dp[i], dp[i-k-1] + k);
            }
        }

        if (a[i-1] < a[i]) {
            dp[i] = Math.min(dp[i], dp[i-1])
        }
    }

    // finite as -1
    return isFinite(dp[n -1]) ? dp[n - 1] : -1

    // find 
    function search(v) {
        // set left and right for compare
        let ans = 0, max = b.length - 1

        // loop
        while(ans <= max) {
            // set middle of
            let m = ans + ((max - ans) >> 1)
            // according to condition
            b[m] < v ? (ans = m + 1) : (max = m - 1)
        }

        // result
        return ans
    }
}
```

---

## managers-with-at-least-5-direct-reports

```mysql
# Write your MySQL query statement below

select e1.name
from Employee e1
join Employee e2 on e1.id = e2.managerId
group by e1.id, e1.name
having count(e2.id) >= 5;

```

---

## matrix-cells-in-distance-order

```golang
import "math"

func allCellsDistOrder(rows int, cols int, rCenter int, cCenter int) [][]int {
    result := make([][]int, rows*cols)
    index := 0

    for r := 0; r < rows; r++ {
        for c := 0; c < cols; c++ {
            result[index] = []int{r, c}
            index++
        }
    }

    // Sort the cells based on their distance from the center cell
    sort.Slice(result, func(i, j int) bool {
        dist1 := int(math.Abs(float64(result[i][0]-rCenter))) + int(math.Abs(float64(result[i][1]-cCenter)))
        dist2 := int(math.Abs(float64(result[j][0]-rCenter))) + int(math.Abs(float64(result[j][1]-cCenter)))
        return dist1 < dist2
    })

    return result
}

```

---

## max-consecutive-ones

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMaxConsecutiveOnes = function(nums) {
  var maxConsecutive = 0;
  var currentConsecutive = 0;

  for (var i = 0; i < nums.length; i++) {
    if (nums[i] === 1) {
      currentConsecutive++;
      maxConsecutive = Math.max(maxConsecutive, currentConsecutive);
    } else {
      currentConsecutive = 0;
    }
  }

  return maxConsecutive;
};

```

---

## max-consecutive-ones-iii

```typescript
function longestOnes(nums: number[], k: number): number {
  let maxConsecutiveOnes = 0; // Maximum consecutive ones
  let left = 0; // Left pointer
  let zerosCount = 0; // Count of zeros

  for (let right = 0; right < nums.length; right++) {
    if (nums[right] === 0) {
      zerosCount++; // Increment the count of zeros
    }

    while (zerosCount > k) {
      if (nums[left] === 0) {
        zerosCount--; // Decrement the count of zeros
      }
      left++; // Move the left pointer to the right
    }

    maxConsecutiveOnes = Math.max(maxConsecutiveOnes, right - left + 1);
  }

  return maxConsecutiveOnes;
}

```

---

## max-dot-product-of-two-subsequences

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
function maxDotProduct(nums1, nums2) {
  const m = nums1.length;
  const n = nums2.length;

  // Create a 2D array dp to store the maximum dot product at each (i, j) position.
  const dp = new Array(m + 1).fill(0).map(() => new Array(n + 1).fill(-Infinity));

  // Initialize the base cases.
  for (let i = 0; i <= m; i++) {
    for (let j = 0; j <= n; j++) {
      if (i === 0 || j === 0) {
        dp[i][j] = -Infinity;
      }
    }
  }

  // Fill in the dp array using dynamic programming.
  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      dp[i][j] = Math.max(
        nums1[i - 1] * nums2[j - 1], // Include the current elements in the product
        dp[i - 1][j - 1] + nums1[i - 1] * nums2[j - 1], // Extend the previous subsequence
        dp[i - 1][j], // Skip the current element in nums2
        dp[i][j - 1] // Skip the current element in nums1
      );
    }
  }

  // The maximum dot product will be at dp[m][n].
  return dp[m][n];
}
```

---

## max-number-of-k-sum-pairs

```typescript
function maxOperations(nums: number[], k: number): number {
  const numCount = new Map<number, number>(); // Map to store the count of each number

  let operations = 0; // Count of operations

  for (const num of nums) {
    const complement = k - num; // Find the complement number to form the sum k

    if (numCount.has(complement) && numCount.get(complement) > 0) {
      // Found a pair that sums up to k
      operations++;
      numCount.set(complement, numCount.get(complement)! - 1); // Decrease the count of the complement number
    } else {
      // Update the count of the current number
      numCount.set(num, (numCount.get(num) || 0) + 1);
    }
  }

  return operations;
}

```

---

## max-points-on-a-line

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var maxPoints = function(points) {
    if (points.length <= 2) {
        return points.length;
    }
    
    let maxCount = 0;
    
    for (let i = 0; i < points.length; i++) {
        const slopes = {};
        let duplicatePoints = 0;
        let currentMax = 0;
        
        for (let j = i + 1; j < points.length; j++) {
            const x1 = points[i][0];
            const y1 = points[i][1];
            const x2 = points[j][0];
            const y2 = points[j][1];
            
            if (x1 === x2 && y1 === y2) {
                duplicatePoints++;
            } else {
                const slope = (x1 - x2) === 0 ? Infinity : (y1 - y2) / (x1 - x2);
                slopes[slope] = (slopes[slope] || 0) + 1;
                currentMax = Math.max(currentMax, slopes[slope]);
            }
        }
        
        maxCount = Math.max(maxCount, currentMax + duplicatePoints + 1);
    }
    
    return maxCount;
};
```

---

## maximal-rectangle

```golang
func maximalRectangle(matrix [][]byte) int {
    if len(matrix) == 0 {
        return 0
    }

    rows, cols := len(matrix), len(matrix[0])
    heights := make([]int, cols)
    maxArea := 0

    for row := 0; row < rows; row++ {
        for col := 0; col < cols; col++ {
            if matrix[row][col] == '1' {
                heights[col]++
            } else {
                heights[col] = 0
            }
        }
        maxArea = max(maxArea, largestRectangleArea(heights))
    }

    return maxArea
}

func largestRectangleArea(heights []int) int {
    stack := make([]int, 0)
    maxArea := 0
    n := len(heights)

    for i := 0; i <= n; {
        h := 0
        if i < n {
            h = heights[i]
        }

        if len(stack) == 0 || h >= heights[stack[len(stack)-1]] {
            stack = append(stack, i)
            i++
        } else {
            tp := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            width := i
            if len(stack) > 0 {
                width = i - stack[len(stack)-1] - 1
            }
            maxArea = max(maxArea, heights[tp]*width)
        }
    }

    return maxArea
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

```

---

## maximal-square

```javascript
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalSquare = function(matrix) {
  const rows = matrix.length;
  const cols = matrix[0].length;
  let maxSquareSize = 0;
  
  // Create a dynamic programming table
  const dp = new Array(rows + 1).fill(0).map(() => new Array(cols + 1).fill(0));
  
  // Iterate through the matrix
  for (let i = 1; i <= rows; i++) {
    for (let j = 1; j <= cols; j++) {
      if (matrix[i - 1][j - 1] === '1') {
        // Calculate the size of the square ending at (i, j)
        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1;
        
        // Update the maximum square size
        maxSquareSize = Math.max(maxSquareSize, dp[i][j]);
      }
    }
  }
  
  // Return the area of the largest square
  return maxSquareSize * maxSquareSize;
}
```

---

## maximize-sum-of-array-after-k-negations

```golang
import "sort"

func largestSumAfterKNegations(nums []int, k int) int {
    // Sort the array in ascending order
    sort.Ints(nums)

    i := 0
    for k > 0 && i < len(nums) && nums[i] < 0 {
        // Negate the current element
        nums[i] = -nums[i]
        i++
        k--
    }

    // If k is still greater than 0 and is odd, negate the smallest element
    if k%2 == 1 {
        // Find the index of the smallest element
        minIdx := 0
        for j := 1; j < len(nums); j++ {
            if nums[j] < nums[minIdx] {
                minIdx = j
            }
        }
        // Negate the smallest element
        nums[minIdx] = -nums[minIdx]
    }

    // Calculate the sum of the modified array
    sum := 0
    for _, num := range nums {
        sum += num
    }

    return sum
}

```

---

## maximum-average-subarray-i

```typescript
function findMaxAverage(nums: number[], k: number): number {
  let sum = 0; // Variable to store the sum of the current subarray
  let maxSum = 0; // Variable to store the maximum sum
  let startIndex = 0; // Start index of the current subarray

  // Calculate the sum of the first k elements
  for (let i = 0; i < k; i++) {
    sum += nums[i];
  }

  maxSum = sum; // Initialize the maximum sum

  // Iterate through the array to find the maximum sum
  for (let i = k; i < nums.length; i++) {
    sum += nums[i] - nums[startIndex]; // Update the sum by adding the current element and subtracting the element at the start index
    maxSum = Math.max(maxSum, sum); // Update the maximum sum if the current sum is greater

    startIndex++; // Move the start index of the subarray forward
  }

  return maxSum / k; // Return the maximum average
}

```

---

## maximum-depth-of-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }
    
    leftDepth := maxDepth(root.Left)
    rightDepth := maxDepth(root.Right)
    
    return max(leftDepth, rightDepth) + 1
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

## maximum-depth-of-n-ary-tree

```javascript
/**
 * // Definition for a Node.
 * function Node(val,children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node|null} root
 * @return {number}
 */
var maxDepth = function(root) {
    if (root === null) {
        return 0;
    }

    let max = 0;
    
    for (let child of root.children) {
        const depth = maxDepth(child);
        if (depth > max) {
            max = depth;
        }
    }

    return max + 1;
};
```

---

## maximum-level-sum-of-a-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxLevelSum(root *TreeNode) int {
	if root == nil {
		return 0
	}

	maxSum := math.MinInt64
	maxLevel := 0
	level := 1

	queue := []*TreeNode{root}

	for len(queue) > 0 {
		sum := 0
		size := len(queue)

		for i := 0; i < size; i++ {
			node := queue[0]
			queue = queue[1:]
			sum += node.Val

			if node.Left != nil {
				queue = append(queue, node.Left)
			}
			if node.Right != nil {
				queue = append(queue, node.Right)
			}
		}

		if sum > maxSum {
			maxSum = sum
			maxLevel = level
		}

		level++
	}

	return maxLevel
}
```

---

## maximum-number-of-non-overlapping-subarrays-with-sum-equals-target

```golang
func maxNonOverlapping(nums []int, target int) int {
    var total int = 0
    var result int = 0
    var seen = make(map[int]bool)
    for _, val := range nums {
        total += val;
        if total == target || seen[total - target] {
            total = 0;
            result++;
            seen = make(map[int]bool)
        } else {
            seen[total] = true
        }
    }
    return result
}
```

---

## maximum-number-of-vowels-in-a-substring-of-given-length

```typescript
function maxVowels(s: string, k: number): number {
  const vowels = new Set(['a', 'e', 'i', 'o', 'u']); // Set of vowel letters
  let maxVowelCount = 0; // Maximum vowel count
  let vowelCount = 0; // Current vowel count

  // Count the vowels in the first window of length k
  for (let i = 0; i < k; i++) {
    if (vowels.has(s[i])) {
      vowelCount++;
    }
  }

  maxVowelCount = vowelCount; // Initialize the maximum vowel count

  // Slide the window through the string
  for (let i = k; i < s.length; i++) {
    if (vowels.has(s[i])) {
      vowelCount++; // Increment the vowel count for the current character
    }

    if (vowels.has(s[i - k])) {
      vowelCount--; // Decrement the vowel count for the character that goes out of the window
    }

    maxVowelCount = Math.max(maxVowelCount, vowelCount); // Update the maximum vowel count
  }

  return maxVowelCount; // Return the maximum vowel count
}

```

---

## maximum-product-of-three-numbers

```golang
func maximumProduct(nums []int) int {
    // Sort the array in ascending order
    sort.Ints(nums)

    // Calculate the two possible products
    product1 := nums[len(nums)-1] * nums[len(nums)-2] * nums[len(nums)-3]
    product2 := nums[0] * nums[1] * nums[len(nums)-1]

    // Return the maximum product
    if product1 > product2 {
        return product1
    } else {
        return product2
    }
}

```

---

## maximum-product-subarray

```typescript
function maxProduct(nums: number[]): number {
  let maxProduct = nums[0];
  let currMax = nums[0];
  let currMin = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (nums[i] < 0) {
      // Swap current maximum and minimum
      [currMax, currMin] = [currMin, currMax];
    }

    currMax = Math.max(nums[i], currMax * nums[i]);
    currMin = Math.min(nums[i], currMin * nums[i]);

    maxProduct = Math.max(maxProduct, currMax);
  }

  return maxProduct;
}
```

---

## maximum-score-of-a-good-subarray

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maximumScore = function(nums, k) {
    const n = nums.length;
    let maxScore = 0;
    const left = Array(n);
    const right = Array(n);

    // Calculate the first smaller element on the left of each element.
    const stack = [];
    for (let i = 0; i < n; i++) {
        while (stack.length > 0 && nums[stack[stack.length - 1]] >= nums[i]) {
            stack.pop();
        }
        left[i] = stack.length === 0 ? -1 : stack[stack.length - 1];
        stack.push(i);
    }

    // Clear the stack and calculate the first smaller element on the right.
    stack.length = 0;
    for (let i = n - 1; i >= 0; i--) {
        while (stack.length > 0 && nums[stack[stack.length - 1]] >= nums[i]) {
            stack.pop();
        }
        right[i] = stack.length === 0 ? n : stack[stack.length - 1];
        stack.push(i);
    }

    // Calculate the maximum score for each possible k.
    for (let i = 0; i < n; i++) {
        if (left[i] < k && right[i] > k) {
            maxScore = Math.max(maxScore, nums[i] * (right[i] - left[i] - 1));
        }
    }

    return maxScore;
};
```

---

## maximum-subarray

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let max = nums[0];
    let curr = 0;
    for (let num of nums) {
        curr = Math.max(num, curr + num);
        if (curr > max) {
            max = curr;
        }
    }
    return max;
};
```

---

## maximum-subsequence-score

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number}
 */
var maxScore = function(nums1, nums2, k) {
	// Sort pair (nums1[i], nums2[i]) by nums2[i] in decreasing order.
	const pairs = nums1.map((num1, index) => [num1, nums2[index]]);
	pairs.sort((a, b) => b[1] - a[1]);

	// Use a min-heap to maintain the top k elements.
	const topKHeap = pairs.slice(0, k).map(([num1]) => num1);
	let topKSum = topKHeap.reduce((sum, num) => sum + num, 0);
	makeHeap(topKHeap);

	// The score of the first k pairs.
	let answer = topKSum * pairs[k - 1][1];

	// Iterate over every nums2[i] as minimum from nums2.
	for (let i = k; i < nums1.length; i++) {
			// Remove the smallest integer from the previous top k elements
			// then add nums1[i] to the top k elements.
			topKSum -= extractMin(topKHeap);
			topKSum += pairs[i][0];
			insertHeap(topKHeap, pairs[i][0]);

			// Update answer as the maximum score.
			answer = Math.max(answer, topKSum * pairs[i][1]);
	}

	return answer;
}

// Helper functions for min-heap operations.
function makeHeap(arr) {
    const n = arr.length;
    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

function heapify(arr, n, i) {
    let smallest = i;
    const left = 2 * i + 1;
    const right = 2 * i + 2;

    if (left < n && arr[left] < arr[smallest]) {
        smallest = left;
    }

    if (right < n && arr[right] < arr[smallest]) {
        smallest = right;
    }

    if (smallest !== i) {
        [arr[i], arr[smallest]] = [arr[smallest], arr[i]];
        heapify(arr, n, smallest);
    }
}

function extractMin(arr) {
    const min = arr[0];
    arr[0] = arr[arr.length - 1];
    arr.pop();
    heapify(arr, arr.length, 0);
    return min;
}

function insertHeap(arr, num) {
    arr.push(num);
    let i = arr.length - 1;
    while (i > 0 && arr[Math.floor((i - 1) / 2)] > arr[i]) {
        [arr[i], arr[Math.floor((i - 1) / 2)]] = [arr[Math.floor((i - 1) / 2)], arr[i]];
        i = Math.floor((i - 1) / 2);
    }
}
```

---

## maximum-sum-circular-subarray

```golang
func maxSubarraySumCircular(nums []int) int {
    // Case 1: Maximum sum subarray is not circular
    maxSum := kadane(nums)
    
    // Case 2: Maximum sum subarray is circular
    // In this case, we subtract the minimum sum subarray from the total sum of the array
    totalSum := 0
    for i := 0; i < len(nums); i++ {
        totalSum += nums[i]
        nums[i] = -nums[i]
    }
    circularSum := totalSum + kadane(nums)
    
    // Return the maximum of the two cases
    if circularSum > maxSum && circularSum != 0 {
        return circularSum
    }
    return maxSum
}

// Kadane's algorithm to find the maximum sum subarray
func kadane(nums []int) int {
    maxSum := nums[0]
    currentSum := nums[0]
    
    for i := 1; i < len(nums); i++ {
        currentSum = max(nums[i], currentSum+nums[i])
        maxSum = max(maxSum, currentSum)
    }
    
    return maxSum
}

// Helper function to find the maximum of two integers
func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

## maximum-twin-sum-of-a-linked-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func pairSum(head *ListNode) int {
    var stack []int = []int{}
    var answer int
    var first int

    // create two pointers
    fast, slow := head, head 

    for nil != fast {
        //while we have fast pointer, add slow pointer value to stack
        stack = append(stack, slow.Val)

        //update slow and fast pointers
        slow = slow.Next
        fast = fast.Next.Next
    }

    for nil != slow {
        // while we have slow pointer, we pop value from stack
        first, stack = stack[len(stack) - 1], stack[:len(stack) - 1]
        // and if our sum of popped value and slow pointer value greater than ans, update ans
        if slow.Val + first > answer {
            answer = slow.Val + first
        }

        // update slow pointer
        slow = slow.Next 
    }

    

    return answer
}

```

---

## maximum-value-of-k-coins-from-piles

```golang
func maxValueOfCoins(piles [][]int, k int) int {
	memo := make([][]int, len(piles)+1)
	for i := range memo {
		memo[i] = make([]int, k+1)
	}

	return dp(piles, memo, 0, k)
}

func dp(piles [][]int, memo [][]int, i int, k int) int {
	if k == 0 || i == len(piles) {
		return 0
	}
	if memo[i][k] != 0 {
		return memo[i][k]
	}

	res := dp(piles, memo, i+1, k)
	cur := 0

	for j := 0; j < min(len(piles[i]), k); j++ {
		cur += piles[i][j]
		res = max(res, cur+dp(piles, memo, i+1, k-j-1))
	}

	memo[i][k] = res
	return res
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

---

## median-of-two-sorted-arrays

```golang
func findMedianSortedArrays(nums1 []int, nums2 []int) float64 {
    totalLength := len(nums1) + len(nums2)
    if totalLength%2 == 1 {
        return float64(findKthElement(nums1, nums2, totalLength/2+1))
    } else {
        return float64(findKthElement(nums1, nums2, totalLength/2)+findKthElement(nums1, nums2, totalLength/2+1)) / 2
    }
}

func findKthElement(nums1 []int, nums2 []int, k int) int {
    index1, index2 := 0, 0
    for {
        if index1 == len(nums1) {
            return nums2[index2+k-1]
        }
        if index2 == len(nums2) {
            return nums1[index1+k-1]
        }
        if k == 1 {
            return min(nums1[index1], nums2[index2])
        }

        half := k / 2
        newIndex1 := min(index1+half, len(nums1)) - 1
        newIndex2 := min(index2+half, len(nums2)) - 1
        pivot1, pivot2 := nums1[newIndex1], nums2[newIndex2]
        if pivot1 <= pivot2 {
            k -= (newIndex1 - index1 + 1)
            index1 = newIndex1 + 1
        } else {
            k -= (newIndex2 - index2 + 1)
            index2 = newIndex2 + 1
        }
    }
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## memoize

```javascript
/**
 * @param {Function} fn
 */
function memoize(fn) {
    const cache = new Map();
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);
        }
        const result = fn(...args);
        cache.set(key, result);
        return result;
    };
}


/** 
 * let callCount = 0;
 * const memoizedFn = memoize(function (a, b) {
 *	 callCount += 1;
 *   return a + b;
 * })
 * memoizedFn(2, 3) // 5
 * memoizedFn(2, 3) // 5
 * console.log(callCount) // 1 
 */
```

---

## memoize-ii

```javascript
/**
 * @param {Function} fn
 */
function memoize(fn) {
    const trie = new Trie();
  return function(...args) {
    let node = trie.root;
    for (let arg of args) {
      if (!node.has(arg)) {
        node.set(arg, new Map());
      }
      node = node.get(arg);
    }
    if (node.has("value")) {
      return node.get("value");
    }
    const result = fn(...args);
    node.set("value", result);
    return result;
  }
}

class Trie {
  constructor() {
    this.root = new Map();
  }

  // Inserts a new value into the trie.
  insert(keys, value) {
    let node = this.root;
    for (let key of keys) {
      if (!node.has(key)) {
        node.set(key, new Map());
      }
      node = node.get(key);
    }
    node.set("value", value);
  }

  // Gets the memoized value for a given set of keys, or undefined if not found.
  lookup(keys) {
    let node = this.root;
    for (let key of keys) {
      if (!node.has(key)) {
        return undefined;
      }
      node = node.get(key);
    }
    return node.get("value");
  }
}


/** 
 * let callCount = 0;
 * const memoizedFn = memoize(function (a, b) {
 *	 callCount += 1;
 *   return a + b;
 * })
 * memoizedFn(2, 3) // 5
 * memoizedFn(2, 3) // 5
 * console.log(callCount) // 1 
 */
```

---

## merge-intervals

```golang
func merge(intervals [][]int) [][]int {
	if len(intervals) <= 1 {
		return intervals
	}

	// Sort intervals based on the start time
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][0] < intervals[j][0]
	})

	result := make([][]int, 0)
	currentInterval := intervals[0]

	for i := 1; i < len(intervals); i++ {
		if intervals[i][0] <= currentInterval[1] {
			// Merge the overlapping intervals
			currentInterval[1] = max(currentInterval[1], intervals[i][1])
		} else {
			// Add the non-overlapping interval to the result
			result = append(result, currentInterval)
			currentInterval = intervals[i]
		}
	}

	// Add the last interval to the result
	result = append(result, currentInterval)

	return result
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

---

## merge-k-sorted-lists

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
// ListNodeHeap implements the heap.Interface for ListNode slice
type ListNodeHeap []*ListNode

func (h ListNodeHeap) Len() int            { return len(h) }
func (h ListNodeHeap) Less(i, j int) bool  { return h[i].Val < h[j].Val }
func (h ListNodeHeap) Swap(i, j int)       { h[i], h[j] = h[j], h[i] }
func (h *ListNodeHeap) Push(x interface{}) { *h = append(*h, x.(*ListNode)) }
func (h *ListNodeHeap) Pop() interface{} {
	old := *h
	n := len(old)
	item := old[n-1]
	*h = old[0 : n-1]
	return item
}

func mergeKLists(lists []*ListNode) *ListNode {
	// Create a min-heap and initialize it with the heads of each linked list
	h := &ListNodeHeap{}
	heap.Init(h)

	for _, node := range lists {
		if node != nil {
			heap.Push(h, node)
		}
	}

	// Create a dummy node to build the merged list
	dummy := &ListNode{}
	curr := dummy

	// Continue merging until all lists are exhausted
	for h.Len() > 0 {
		minNode := heap.Pop(h).(*ListNode)
		curr.Next = minNode
		curr = curr.Next

		if minNode.Next != nil {
			heap.Push(h, minNode.Next)
		}
	}

	return dummy.Next
}
```

---

## merge-sorted-array

```golang
func merge(nums1 []int, m int, nums2 []int, n int) {
    // Start merging from the end of the merged array
    i := m - 1
    j := n - 1
    k := m + n - 1

    // Merge nums1 and nums2 from the end
    for i >= 0 && j >= 0 {
        if nums1[i] > nums2[j] {
            nums1[k] = nums1[i]
            i--
        } else {
            nums1[k] = nums2[j]
            j--
        }
        k--
    }

    // Copy remaining elements from nums2 to nums1
    for j >= 0 {
        nums1[k] = nums2[j]
        j--
        k--
    }
}

```

---

## merge-strings-alternately

```typescript
function mergeAlternately(word1: string, word2: string): string {
    let merged = '';
    const length = Math.max(word1.length, word2.length);

    for (let i = 0; i < length; i++) {
        if (i < word1.length) {
        merged += word1[i];
        }
        if (i < word2.length) {
        merged += word2[i];
        }
    }

    return merged;
};
```

---

## merge-two-binary-trees

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func mergeTrees(root1 *TreeNode, root2 *TreeNode) *TreeNode {
    // Base cases
    if root1 == nil {
        return root2
    }
    if root2 == nil {
        return root1
    }

    // Merge the current nodes
    merged := &TreeNode{
        Val:   root1.Val + root2.Val,
        Left:  mergeTrees(root1.Left, root2.Left),
        Right: mergeTrees(root1.Right, root2.Right),
    }

    return merged
}

```

---

## merge-two-sorted-lists

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
// Function to create a new node with a given value
struct ListNode* createNode(int val) {
    struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    newNode->val = val;
    newNode->next = NULL;
    return newNode;
}

// Function to merge two sorted linked lists
struct ListNode* mergeTwoLists(struct ListNode* list1, struct ListNode* list2) {
    struct ListNode dummy; // Dummy node to simplify the code
    struct ListNode* current = &dummy;

    while (list1 != NULL && list2 != NULL) {
        if (list1->val < list2->val) {
            current->next = list1;
            list1 = list1->next;
        } else {
            current->next = list2;
            list2 = list2->next;
        }
        current = current->next;
    }

    // If one of the lists is not empty, append the remaining elements
    if (list1 != NULL) {
        current->next = list1;
    } else {
        current->next = list2;
    }

    return dummy.next;
}

// Function to print the linked list
void printList(struct ListNode* head) {
    struct ListNode* current = head;
    while (current != NULL) {
        printf("%d -> ", current->val);
        current = current->next;
    }
    printf("NULL\n");
}
```

---

## middle-of-the-linked-list

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var middleNode = function(head) {
    let slow = head;
    let fast = head;
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
};
```

---

## min-cost-climbing-stairs

```javascript
/**
 * @param {number[]} cost
 * @return {number}
 */
var minCostClimbingStairs = function(cost) {
    let n = cost.length;
    let dp = new Array(n);

    dp[0] = cost[0];
    dp[1] = cost[1];

    for (let i = 2; i < n; i++) {
        dp[i] = cost[i] + Math.min(
            dp[i-1],
            dp[i-2]
        );
    }

    return Math.min(dp[n-1], dp[n-2]);
};
```

---

## min-stack

```golang
type MinStack struct {
    stack    []int
    minStack []int
}

func Constructor() MinStack {
    return MinStack{}
}

func (this *MinStack) Push(val int) {
    this.stack = append(this.stack, val)

    if len(this.minStack) == 0 || val <= this.minStack[len(this.minStack)-1] {
        this.minStack = append(this.minStack, val)
    }
}

func (this *MinStack) Pop() {
    if this.stack[len(this.stack)-1] == this.minStack[len(this.minStack)-1] {
        this.minStack = this.minStack[:len(this.minStack)-1]
    }
    this.stack = this.stack[:len(this.stack)-1]
}

func (this *MinStack) Top() int {
    return this.stack[len(this.stack)-1]
}

func (this *MinStack) GetMin() int {
    return this.minStack[len(this.minStack)-1]
}



/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(val);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.GetMin();
 */
```

---

## minimum-absolute-difference-in-bst

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val === undefined ? 0 : val);
 *     this.left = (left === undefined ? null : left);
 *     this.right = (right === undefined ? null : right);
 * }
 */

/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function(root) {
  // Initialize variables
  var prev = null; // Previous node's value during traversal
  var minDiff = Infinity; // Minimum difference found
  
  // In-order traversal function
  function inorder(node) {
    if (node === null) return;
    
    // Traverse left subtree
    inorder(node.left);
    
    // Check difference with previous value
    if (prev !== null) {
      minDiff = Math.min(minDiff, node.val - prev);
    }
    
    // Update previous value
    prev = node.val;
    
    // Traverse right subtree
    inorder(node.right);
  }
  
  // Start traversal from the root
  inorder(root);
  
  // Return the minimum difference found
  return minDiff;
};

```

---

## minimum-common-value

```golang
// enfoque meh
/*
func getCommon(nums1 []int, nums2 []int) int {
    for _, i := range nums1 {
        for _, j := range nums2 {
            if i == j {
                return i
            }
        }
    }
    return -1
}
*/

// enfoque de dos punteros
/*
func getCommon(nums1 []int, nums2 []int) int {
    i, j := 0, 0
    for i < len(nums1) && j < len(nums2) {
        switch {
        case nums1[i] == nums2[j]:
            return nums1[i]
        case nums1[i] < nums2[j]:
            i++
        default:
            j++
        }
    }
    return -1
}
*/

func getCommon(nums1 []int, nums2 []int) int {
    hash := make(map[int]int, len(nums2))

    for i, num := range nums2 {
        hash[num] = i
    }

    for _, num := range nums1 {
        _, ok := hash[num]
        if ok {
            return num
        }
    }

    return -1
}
```

---

## minimum-depth-of-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func minDepth(root *TreeNode) int {
	if root == nil {
		return 0
	}

	if root.Left == nil && root.Right == nil {
		return 1
	}

	min := math.MaxInt32

	if root.Left != nil {
		min = getMin(min, minDepth(root.Left))
	}

	if root.Right != nil {
		min = getMin(min, minDepth(root.Right))
	}

	return min + 1
}

func getMin(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```

---

## minimum-distance-between-bst-nodes

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDiffInBST = function(root) {
      // Initialize variables
  var prev = null; // Previous node's value during traversal
  var minDiff = Infinity; // Minimum difference found
  
  // In-order traversal function
  function inorder(node) {
    if (node === null) return;
    
    // Traverse left subtree
    inorder(node.left);
    
    // Check difference with previous value
    if (prev !== null) {
      minDiff = Math.min(minDiff, node.val - prev);
    }
    
    // Update previous value
    prev = node.val;
    
    // Traverse right subtree
    inorder(node.right);
  }
  
  // Start traversal from the root
  inorder(root);
  
  // Return the minimum difference found
  return minDiff;
};
```

---

## minimum-flips-to-make-a-or-b-equal-to-c

```golang
func minFlips(a int, b int, c int) int {
    flips := 0
    for i := 0; i < 32; i++ {
        bitA := (a >> i) & 1
        bitB := (b >> i) & 1
        bitC := (c >> i) & 1
        
        if bitC == 0 {
            if bitA == 1 {
                flips++
            }
            if bitB == 1 {
                flips++
            }
        } else {
            if bitA == 0 && bitB == 0 {
                flips++
            }
        }
    }
    return flips
}
```

---

## minimum-genetic-mutation

```javascript
/**
 * @param {string} startGene
 * @param {string} endGene
 * @param {string[]} bank
 * @return {number}
 */
var minMutation = function(startGene, endGene, bank) {
  // Check if the endGene is not in the bank
  if (!bank.includes(endGene)) {
    return -1;
  }
  
  // Create a set to keep track of visited genes
  const visited = new Set();
  
  // Create a queue for BFS
  const queue = [];
  
  // Enqueue the startGene with 0 mutations
  queue.push([startGene, 0]);
  
  while (queue.length > 0) {
    const [gene, mutations] = queue.shift();
    
    // Check if we have reached the endGene
    if (gene === endGene) {
      return mutations;
    }
    
    // Explore all possible mutations
    for (const nextGene of bank) {
      if (!visited.has(nextGene) && isMutation(gene, nextGene)) {
        visited.add(nextGene);
        queue.push([nextGene, mutations + 1]);
      }
    }
  }
  
  // If we reach here, it means there is no valid mutation
  return -1;
};

// Helper function to check if two genes are a valid mutation
function isMutation(gene1, gene2) {
  let diff = 0;
  
  for (let i = 0; i < gene1.length; i++) {
    if (gene1[i] !== gene2[i]) {
      diff++;
    }
  }
  
  return diff === 1;
}
```

---

## minimum-index-sum-of-two-lists

```javascript
/**
 * @param {string[]} list1
 * @param {string[]} list2
 * @return {string[]}
 */
var findRestaurant = function(list1, list2) {
  const map = new Map();
  let minIndexSum = Infinity;
  const result = [];
  
  // Store the index of each string in list1
  for (let i = 0; i < list1.length; i++) {
    map.set(list1[i], i);
  }
  
  // Check for common strings and update the minimum index sum
  for (let j = 0; j < list2.length; j++) {
    if (map.has(list2[j])) {
      const indexSum = j + map.get(list2[j]);
      if (indexSum < minIndexSum) {
        minIndexSum = indexSum;
        result.length = 0; // Clear the previous result
        result.push(list2[j]);
      } else if (indexSum === minIndexSum) {
        result.push(list2[j]);
      }
    }
  }
  
  return result;
};

```

---

## minimum-number-of-arrows-to-burst-balloons

```golang
func findMinArrowShots(points [][]int) int {
	// Sort the balloons based on their end coordinates
	sort.Slice(points, func(i, j int) bool {
		return points[i][1] < points[j][1]
	})

	// Initialize the number of arrows and the end coordinate of the current arrow
	arrows := 0
	end := points[0][1]

	// Iterate through the sorted balloons
	for i := 1; i < len(points); i++ {
		// If the balloon's start coordinate is greater than the current arrow's end coordinate,
		// it means we need an additional arrow since the previous arrow cannot burst this balloon.
		if points[i][0] > end {
			arrows++
			end = points[i][1]
		}
	}

	// Return the minimum number of arrows needed
	return arrows + 1
}

```

---

## minimum-number-of-operations-to-make-array-continuous

```rust
impl Solution {
    pub fn min_operations(nums: Vec<i32>) -> i32 {
        let mut nums = nums;
        let n = nums.len();
        let mut ans = n as i32;
        nums.sort_unstable();
        nums.dedup();
        let m = nums.len();
        let mut j = 0;
        for i in 0..m {
            while j < m && nums[j] < nums[i] + n as i32 {
                j += 1;
            }
            ans = ans.min(n as i32 - j as i32 + i as i32);
        }
        ans
    }
}
```

---

## minimum-path-sum

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
  const m = grid.length;
  const n = grid[0].length;

  // Create a 2D array to store the minimum path sum
  const dp = new Array(m);
  for (let i = 0; i < m; i++) {
    dp[i] = new Array(n);
  }

  // Initialize the first cell
  dp[0][0] = grid[0][0];

  // Initialize the first column
  for (let i = 1; i < m; i++) {
    dp[i][0] = dp[i - 1][0] + grid[i][0];
  }

  // Initialize the first row
  for (let j = 1; j < n; j++) {
    dp[0][j] = dp[0][j - 1] + grid[0][j];
  }

  // Calculate the minimum path sum for each cell
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
    }
  }

  // Return the minimum path sum for the bottom-right cell
  return dp[m - 1][n - 1];
}
```

---

## minimum-size-subarray-sum

```javascript
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
function minSubArrayLen(target, nums) {
  let minLength = Infinity;
  const prefixSum = [0];

  for (let i = 1; i <= nums.length; i++) {
    prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
  }

  for (let i = 0; i < prefixSum.length; i++) {
    const end = binarySearch(prefixSum, i + 1, prefixSum.length - 1, prefixSum[i] + target);
    if (end !== -1) {
      minLength = Math.min(minLength, end - i);
    }
  }

  return minLength !== Infinity ? minLength : 0;
}

function binarySearch(nums, left, right, target) {
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return left >= nums.length ? -1 : left;
}
```

---

## minimum-window-substring

```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
function minWindow(s, t) {
  // Create a character map for string t
  const tMap = {};
  for (let char of t) {
    tMap[char] = (tMap[char] || 0) + 1;
  }

  let left = 0;
  let count = Object.keys(tMap).length;
  let minLength = Infinity;
  let minWindowStart = 0;

  for (let right = 0; right < s.length; right++) {
    const char = s[right];

    if (char in tMap) {
      tMap[char]--;
      if (tMap[char] === 0) count--;
    }

    while (count === 0) {
      if (right - left + 1 < minLength) {
        minLength = right - left + 1;
        minWindowStart = left;
      }

      const leftChar = s[left];
      if (leftChar in tMap) {
        tMap[leftChar]++;
        if (tMap[leftChar] > 0) count++;
      }

      left++;
    }
  }

  if (minLength === Infinity) return "";
  return s.substr(minWindowStart, minLength);
}

```

---

## missing-number

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    nums.sort((a,b)=>a-b);
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] != i) {
            return i;
        }
    }
    return nums[nums.length-1] + 1;
};
```

---

## monotonic-array

```golang
func isMonotonic(nums []int) bool {
    increasing, decreasing := true, true

    for i := 1; i < len(nums); i++ {
        if nums[i-1] > nums[i] {
            increasing = false
        }
        if nums[i-1] < nums[i] {
            decreasing = false
        }
    }

    return increasing || decreasing
}
```

---

## monthly-transactions-i

```mysql
# Write your MySQL query statement below

select date_format(trans_date, '%Y-%m') as month,
       country,
       COUNT(*) as trans_count,
       sum(case when state = 'approved' then 1 else 0 end) as approved_count,
       sum(amount) as trans_total_amount,
       sum(case when state = 'approved' then amount else 0 end) as approved_total_amount
from Transactions
group by month, country;

```

---

## most-common-word

```golang
func mostCommonWord(paragraph string, banned []string) string {
    // Preprocess the paragraph: lowercase and split into words
    paragraph = strings.ToLower(paragraph)
    words := make([]string, 0)
    wordStart := -1

    for i, char := range paragraph {
        if isLetter(char) {
            if wordStart == -1 {
                wordStart = i
            }
        } else {
            if wordStart != -1 {
                words = append(words, paragraph[wordStart:i])
                wordStart = -1
            }
        }
    }

    if wordStart != -1 {
        words = append(words, paragraph[wordStart:])
    }

    // Create a map to store word frequency counts
    wordCount := make(map[string]int)

    // Create a set of banned words for faster lookup
    bannedSet := make(map[string]bool)
    for _, word := range banned {
        bannedSet[word] = true
    }

    // Iterate through words and count frequencies
    mostCommon := ""
    maxCount := 0

    for _, word := range words {
        if !bannedSet[word] {
            wordCount[word]++
            if wordCount[word] > maxCount {
                maxCount = wordCount[word]
                mostCommon = word
            }
        }
    }

    return mostCommon
}

func isLetter(char rune) bool {
    return (char >= 'a' && char <= 'z') || (char >= 'A' && char <= 'Z')
}

```

---

## move-zeroes

```golang
func moveZeroes(nums []int)  {
    // Initialize a pointer to the first zero
    zeroPtr := 0

    // Iterate through the array
    for i := 0; i < len(nums); i++ {
        // If the current element is non-zero
        if nums[i] != 0 {
            // Swap the current element with the element at the first zero pointer
            nums[i], nums[zeroPtr] = nums[zeroPtr], nums[i]
            // Move the zero pointer one position to the right
            zeroPtr++
        }
    }
}
```

---

## movie-rating

```oraclesql
/* Write your PL/SQL query statement below */

select name results
from (
select u.user_id, u.name, count(distinct movie_id) mv_cnt
from MovieRating m
inner join Users u
on u.user_id = m.user_id
group by u.user_id, u.name
order by mv_cnt desc, u.name
    )
where rowNum = 1

union all

select title results
from(
    select m2.movie_id, m2.title, avg(m1.rating) avg_rt
    from MovieRating m1
    inner join Movies m2
    on m1.movie_id = m2.movie_id
    where to_char(m1.created_at, 'YYYY-MM') = '2020-02'
    group by m2.movie_id, m2.title
    order by avg_rt desc, m2.title
    )
where rowNum = 1
```

---

## multiply-strings

```javascript
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var multiply = function(num1, num2) {
    const m = num1.length, n = num2.length;
    const res = Array(m + n).fill(0);
    for (let i = n - 1; i >= 0; i--) {
        let carry = 0;
        for (let j = m - 1; j >= 0; j--) {
            let prod = carry + parseInt(num2.charAt(i)) * parseInt(num1.charAt(j));
            carry = Math.floor(prod / 10);
            res[i + j + 1] += prod % 10;
            res[i + j] += Math.floor(res[i + j + 1] / 10);
            res[i + j + 1] %= 10;
        }
        res[i] += carry;
    }
    let i = 0;
    while (i < m + n && res[i] === 0) {
        i++;
    }
    return i === m + n ? "0" : res.slice(i).join("");
};

```

---

## n-ary-tree-postorder-traversal

```javascript
/**
 * // Definition for a Node.
 * function Node(val,children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node|null} root
 * @return {number[]}
 */
var postorder = function(root) {
    if (root === null) {
      return [];
    }

    const stack = [root];
    const result = [];

    while (stack.length > 0) {
      const node = stack.pop();
      result.unshift(node.val);
      for (let child of node.children) {
        stack.push(child);
      }
    }

    return result;
};
```

---

## n-ary-tree-preorder-traversal

```javascript
/**
 * // Definition for a Node.
 * function Node(val, children) {
 *    this.val = val;
 *    this.children = children;
 * };
 */

/**
 * @param {Node|null} root
 * @return {number[]}
 */
var preorder = function(root) {
  const result = [];
  
  // Recursive function to perform preorder traversal
  function traverse(node) {
    if (node === null) {
      return;
    }
    
    // Visit the current node
    result.push(node.val);
    
    // Traverse the children nodes recursively
    for (let child of node.children) {
      traverse(child);
    }
  }
  
  // Call the recursive function on the root node
  traverse(root);
  
  return result;
};

```

---

## n-queens

```golang
func solveNQueens(n int) [][]string {
    res := [][]string{}
    cols, diags1, diags2 := make(map[int]bool), make(map[int]bool), make(map[int]bool)
    board := make([]string, n)
    for i := range board {
        board[i] = strings.Repeat(".", n)
    }
    backtrack(0, board, &res, cols, diags1, diags2, n)
    return res
}

func backtrack(row int, board []string, res *[][]string, cols, diags1, diags2 map[int]bool, n int) {
    if row == n {
        tmp := make([]string, n)
        copy(tmp, board)
        *res = append(*res, tmp)
        return
    }
    for col := 0; col < n; col++ {
        if !cols[col] && !diags1[row-col] && !diags2[row+col] {
            cols[col], diags1[row-col], diags2[row+col] = true, true, true
            board[row] = board[row][:col] + "Q" + board[row][col+1:]
            backtrack(row+1, board, res, cols, diags1, diags2, n)
            cols[col], diags1[row-col], diags2[row+col] = false, false, false
            board[row] = board[row][:col] + "." + board[row][col+1:]
        }
    }
}

```

---

## n-queens-ii

```golang
func totalNQueens(n int) int {
	count := 0
	columns := make([]bool, n)
	diagonal1 := make([]bool, 2*n-1)
	diagonal2 := make([]bool, 2*n-1)
	backtrack(0, n, &count, &columns, &diagonal1, &diagonal2)
	return count
}

func backtrack(row, n int, count *int, columns, diagonal1, diagonal2 *[]bool) {
	if row == n {
		*count++
		return
	}

	for col := 0; col < n; col++ {
		d1 := row - col + n - 1
		d2 := row + col

		if (*columns)[col] || (*diagonal1)[d1] || (*diagonal2)[d2] {
			continue
		}

		(*columns)[col] = true
		(*diagonal1)[d1] = true
		(*diagonal2)[d2] = true

		backtrack(row+1, n, count, columns, diagonal1, diagonal2)

		(*columns)[col] = false
		(*diagonal1)[d1] = false
		(*diagonal2)[d2] = false
	}
}
```

---

## n-repeated-element-in-size-2n-array

```golang
func repeatedNTimes(nums []int) int {
    freqMap := make(map[int]int)

    for _, num := range nums {
        freqMap[num]++
        if freqMap[num] == len(nums)/2 {
            return num
        }
    }

    return 0 // Return 0 if no repeated element is found (which shouldn't happen based on the problem constraints).
}

```

---

## n-th-tribonacci-number

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var tribonacci = function(n) {
    let dp = new Array(n+1).fill(0);
    dp[1] = 1;
    dp[2] = 1;
    for (let i = 3; i<=n; i++) {
        dp[i] = dp[i-1] + dp[i-2] + dp[i-3];
    }
    return dp[n]
};
```

---

## nearest-exit-from-entrance-in-maze

```typescript
function nearestExit(maze: string[][], entrance: number[]): number {
  const rows = maze.length;
  const cols = maze[0].length;
  const directions = [[-1, 0], [1, 0], [0, -1], [0, 1]];
  const queue: number[][] = [entrance];
  const visited: boolean[][] = [];

  for (let i = 0; i < rows; i++) {
    visited[i] = [];
    for (let j = 0; j < cols; j++) {
      visited[i][j] = false;
    }
  }

  visited[entrance[0]][entrance[1]] = true;
  let steps = 0;

  while (queue.length > 0) {
    const size = queue.length;

    for (let i = 0; i < size; i++) {
      const [x, y] = queue.shift()!;

      if (isExit(x, y, rows, cols)) {
        if (!(x === entrance[0] && y === entrance[1])) {
          return steps;
        }
      }

      for (const [dx, dy] of directions) {
        const nx = x + dx;
        const ny = y + dy;

        if (isValid(nx, ny, rows, cols, maze, visited)) {
          queue.push([nx, ny]);
          visited[nx][ny] = true;
        }
      }
    }

    steps++;
  }

  return -1;
}

function isValid(
  x: number,
  y: number,
  rows: number,
  cols: number,
  maze: string[][],
  visited: boolean[][]
): boolean {
  return (
    x >= 0 &&
    x < rows &&
    y >= 0 &&
    y < cols &&
    maze[x][y] === "." &&
    !visited[x][y]
  );
}

function isExit(x: number, y: number, rows: number, cols: number): boolean {
  return (
    x === 0 || x === rows - 1 || y === 0 || y === cols - 1
  );
}

```

---

## nested-array-generator

```javascript
/**
 * @param {Array} arr
 * @return {Generator}
 */
var inorderTraversal = function*(arr) {
    for (let i = 0; i < arr.length; i++) {
        if (Array.isArray(arr[i])) {
            yield* inorderTraversal(arr[i]);
        } else {
            yield arr[i];
        }
    }
};

/**
 * const gen = inorderTraversal([1, [2, 3]]);
 * gen.next().value; // 1
 * gen.next().value; // 2
 * gen.next().value; // 3
 */
```

---

## next-greater-element-i

```golang
func nextGreaterElement(nums1 []int, nums2 []int) []int {
    nextGreater := make(map[int]int)
    stack := []int{}
    
    // Find the next greater element for each element in nums2
    for _, num := range nums2 {
        for len(stack) > 0 && stack[len(stack)-1] < num {
            top := stack[len(stack)-1]
            stack = stack[:len(stack)-1]
            nextGreater[top] = num
        }
        stack = append(stack, num)
    }
    
    // Find the next greater element for each element in nums1
    result := make([]int, len(nums1))
    for i, num := range nums1 {
        if val, found := nextGreater[num]; found {
            result[i] = val
        } else {
            result[i] = -1
        }
    }
    
    return result
}

```

---

## next-permutation

```golang
func nextPermutation(nums []int) {
    // Find the first decreasing element from the right
    i := len(nums) - 2
    for i >= 0 && nums[i] >= nums[i+1] {
        i--
    }

    // If such element exists, find the next greater element to its right
    if i >= 0 {
        j := len(nums) - 1
        for j > i && nums[j] <= nums[i] {
            j--
        }
        // Swap the two elements
        nums[i], nums[j] = nums[j], nums[i]
    }

    // Reverse the subarray to the right of i
    reverse(nums, i+1, len(nums)-1)
}

// Helper function to reverse a subarray in place
func reverse(nums []int, start, end int) {
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
}

```

---

## nim-game

```golang
func canWinNim(n int) bool {
	return n%4 != 0
}
```

---

## non-decreasing-subsequences

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var findSubsequences = function(nums) {
    const result = [];
    function backtrack(current, start) {
        if (current.length >= 2) {
            result.push([...current]);
        }

        const used = new Set();
        for (let i = start; i < nums.length; i++) {
            if (used.has(nums[i]) || (current.length > 0 && nums[i] < current[current.length-1])) {
                continue;
            }
            used.add(nums[i]);
            current.push(nums[i]);
            backtrack(current, i + 1);
            current.pop();
        }
    }
    backtrack([], 0);
    return result;
};


```

---

## non-overlapping-intervals

```golang
func eraseOverlapIntervals(intervals [][]int) int {
	if len(intervals) == 0 {
		return 0
	}

	// Sort intervals based on their end coordinates
	sort.Slice(intervals, func(i, j int) bool {
		return intervals[i][1] < intervals[j][1]
	})

	// Initialize variables
	end := intervals[0][1]
	removals := 0

	// Iterate through intervals
	for i := 1; i < len(intervals); i++ {
		// If the start of the current interval is less than the end of the previous interval,
		// it means there is an overlap and we need to remove one interval.
		if intervals[i][0] < end {
			removals++
		} else {
			end = intervals[i][1]
		}
	}

	return removals
}

```

---

## not-boring-movies

```mysql
# Write your MySQL query statement below

select id, movie, description, rating
from Cinema
where id % 2 = 1 and description <> 'boring'
order by rating desc;
```

---

## nth-highest-salary

```pythondata
import pandas as pd

def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:

    # Drop any duplicate salary values to avoid counting duplicates as separate salary ranks
    unique_salaries = employee['salary'].drop_duplicates()

    # Sort the unique salaries in descending order and get the Nth highest salary
    sorted_salaries = unique_salaries.sort_values(ascending=False)

    # If N exceeds the number of unique salaries, return None
    if N > len(sorted_salaries):
        return pd.DataFrame({'Nth Highest Salary': [None]})
    
    # Get the Nth highest salary from the sorted salaries
    nth_highest = sorted_salaries.iloc[N - 1]
    
    return pd.DataFrame({'Nth Highest Salary': [nth_highest]})
```

---

## number-complement

```javascript
/**
 * @param {number} num
 * @return {number}
 */
var findComplement = function(num) {
  var mask = (1 << num.toString(2).length) - 1;
  return num ^ mask;
};
```

---

## number-of-1-bits

```javascript
/**
 * @param {number} n - a positive integer
 * @return {number}
 */
var hammingWeight = function(n) {
    return Number(n).toString(2).replaceAll("0", "").length
};
```

---

## number-of-days-between-two-dates

```javascript
/**
 * @param {string} date1
 * @param {string} date2
 * @return {number}
 */
var daysBetweenDates = function(date1, date2) {
    let startDate = new Date(date1);
    let endDate = new Date(date2);
    
    const diff = endDate - startDate;
    const days = Math.floor(diff / (1000*60*60*24));

    return Math.abs(days);
};
```

---

## number-of-digit-one

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var countDigitOne = function(n) {
    let count = 0;
    for (let i = 1; i <= n; i *= 10) {
        const div = i * 10;
        count += Math.floor(n/div) * i + Math.min(Math.max(n % div - i + 1, 0), i)
    }
    return count
};
```

---

## number-of-equivalent-domino-pairs

```golang
func numEquivDominoPairs(dominoes [][]int) int {
    total := 0
    for i := 0; i < len(dominoes); i++ {
        for j := i+1; j < len(dominoes); j++ {
            if dominoes[i][0] == dominoes[j][0] && dominoes[i][1] == dominoes[j][1] || 
dominoes[i][0] == dominoes[j][1] && dominoes[i][1] == dominoes[j][0] {
                total += 1
            }
        }
    }
    return total
}
```

---

## number-of-flowers-in-full-bloom

```typescript
function fullBloomFlowers(flowers: number[][], people: number[]): number[] {
    const search = (arr: Uint32Array, target: number): number => {
        let low = 0;
        let high = arr.length;
        while (low < high) {
            const mid = ~~((low + high) / 2);
            if (arr[mid] > target) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    };

    const starts = new Uint32Array(flowers.length);
    const ends = new Uint32Array(flowers.length);
    for (let i = 0; i < flowers.length; i++) {
        starts[i] = flowers[i][0];
        ends[i] = flowers[i][1] + 1;
    }
    starts.sort();
    ends.sort();
    return people.map(t => search(starts, t) - search(ends, t));
}

```

---

## number-of-good-pairs

```golang
func numIdenticalPairs(nums []int) int {
    // Create a map to count the occurrences of each number
    numCounts := make(map[int]int)
    
    // Initialize the result variable to keep track of good pairs
    goodPairs := 0
    
    // Iterate through the nums array and update the counts in the map
    for _, num := range nums {
        numCounts[num]++
    }
    
    // Iterate through the map and calculate the number of good pairs
    for _, count := range numCounts {
        goodPairs += (count * (count - 1)) / 2
    }
    
    return goodPairs
}
```

---

## number-of-increasing-paths-in-a-grid

```golang
func countPaths(grid [][]int) int {
	m, n := len(grid), len(grid[0])
	ans, mod := 0, 1000000007
	dp := make([][]int, m)
	for i := 0; i < m; i++ {
		dp[i] = make([]int, n)
		for j := 0; j < n; j++ {
			dp[i][j] = -1
		}
	}

	var dfs func(int, int) int
	dfs = func(r, c int) int {
		if dp[r][c] != -1 {
			return dp[r][c]
		}
		cellValue := 1
		direction := [4][2]int{{r - 1, c}, {r, c + 1}, {r + 1, c}, {r, c - 1}}
		for _, d := range direction {
			nr, nc := d[0], d[1]
			if 0 <= nr && nr < m && 0 <= nc && nc < n && grid[nr][nc] > grid[r][c] {
				cellValue = (cellValue%mod + dfs(nr, nc)%mod) % mod
			}
		}
		dp[r][c] = cellValue
		return dp[r][c]
	}

	for i := 0; i < m; i++ {
		for j := 0; j < n; j++ {
			ans = (ans%mod + dfs(i, j)%mod) % mod
		}
	}
	return ans
}
```

---

## number-of-islands

```golang
func numIslands(grid [][]byte) int {
	if len(grid) == 0 || len(grid[0]) == 0 {
		return 0
	}

	numRows, numCols := len(grid), len(grid[0])
	count := 0

	var stack [][]int

	for i := 0; i < numRows; i++ {
		for j := 0; j < numCols; j++ {
			if grid[i][j] == '1' {
				count++
				stack = append(stack, []int{i, j})

				for len(stack) > 0 {
					curr := stack[len(stack)-1]
					stack = stack[:len(stack)-1]
					row, col := curr[0], curr[1]

					if row < 0 || row >= numRows || col < 0 || col >= numCols || grid[row][col] != '1' {
						continue
					}

					grid[row][col] = '0'

					stack = append(stack, []int{row - 1, col})
					stack = append(stack, []int{row + 1, col})
					stack = append(stack, []int{row, col - 1})
					stack = append(stack, []int{row, col + 1})
				}
			}
		}
	}

	return count
}
```

---

## number-of-lines-to-write-string

```golang
func numberOfLines(widths []int, s string) []int {
    lineCount := 1
    lineWidth := 0
    
    for _, char := range s {
        charWidth := widths[char-'a']
        if lineWidth+charWidth > 100 {
            lineCount++
            lineWidth = charWidth
        } else {
            lineWidth += charWidth
        }
    }
    
    return []int{lineCount, lineWidth}
}

```

---

## number-of-longest-increasing-subsequence

```golang
/*
To solve this problem, we can use dynamic programming. We will maintain two arrays, lengths and counts, where lengths[i] represents the length of the longest increasing subsequence ending at index i, and counts[i] represents the number of longest increasing subsequences ending at index i.

We will initialize lengths and counts arrays with 1, as every individual element is an increasing subsequence of length 1, and the count of such subsequences is also 1.

Then, for each index i from 1 to len(nums), we will check the previous elements j from 0 to i-1 and update lengths[i] and counts[i] based on the following conditions:

If nums[i] is greater than nums[j], it means we can extend the increasing subsequence, so we check if lengths[j] + 1 is greater than the current lengths[i]. If it is, we update lengths[i] to lengths[j] + 1 and set counts[i] to counts[j].

If nums[i] is equal to nums[j], it means we can't extend the increasing subsequence, so we check if lengths[j] + 1 is equal to the current lengths[i]. If it is, it means we have found an equal length increasing subsequence, so we add counts[j] to counts[i].

Finally, we find the maximum length from the lengths array and count all occurrences of the maximum length in the counts array to get the total number of longest increasing subsequences.
*/

func findNumberOfLIS(nums []int) int {
    n := len(nums)
    lengths := make([]int, n)
    counts := make([]int, n)

    for i := 0; i < n; i++ {
        lengths[i] = 1
        counts[i] = 1
        for j := 0; j < i; j++ {
            if nums[i] > nums[j] {
                if lengths[j]+1 > lengths[i] {
                    lengths[i] = lengths[j] + 1
                    counts[i] = counts[j]
                } else if lengths[j]+1 == lengths[i] {
                    counts[i] += counts[j]
                }
            }
        }
    }

    maxLength := 0
    maxCount := 0
    for i := 0; i < n; i++ {
        if lengths[i] > maxLength {
            maxLength = lengths[i]
            maxCount = counts[i]
        } else if lengths[i] == maxLength {
            maxCount += counts[i]
        }
    }

    return maxCount
}

```

---

## number-of-provinces

```typescript
function findCircleNum(isConnected: number[][]): number {
  const n = isConnected.length;
  const visited = new Array(n).fill(false);
  let provinces = 0;

  for (let i = 0; i < n; i++) {
    if (!visited[i]) {
      dfs(i);
      provinces++;
    }
  }

  function dfs(city: number): void {
    visited[city] = true;

    for (let j = 0; j < n; j++) {
      if (isConnected[city][j] === 1 && !visited[j]) {
        dfs(j);
      }
    }
  }

  return provinces;
}

```

---

## number-of-recent-calls

```typescript
class RecentCounter {
  requests: number[];

  constructor() {
    this.requests = [];
  }

  ping(t: number): number {
    this.requests.push(t);
    const lowerBound = t - 3000;

    while (this.requests[0] < lowerBound) {
      this.requests.shift();
    }

    return this.requests.length;
  }
}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```

---

## number-of-segments-in-a-string

```golang
func countSegments(s string) int {
    count := 0
    inSegment := false

    for _, char := range s {
        if char != ' ' {
            if !inSegment {
                count++
            }
            inSegment = true
        } else {
            inSegment = false
        }
    }

    return count
}
```

---

## number-of-unique-subjects-taught-by-each-teacher

```mysql
# Write your MySQL query statement below

select teacher_id, count(distinct subject_id) as cnt
from Teacher
group by teacher_id;

```

---

## number-of-ways-to-earn-points

```golang
func waysToReachTarget(target int, types [][]int) int {
    const mod = 1e9 + 7
    n := len(types)
    dp := make([]int, target+1)
    dp[0] = 1
    for i := 0; i < n; i++ {
        count, marks := types[i][0], types[i][1]
        for j := target; j >= marks; j-- {
            for k := 1; k <= count && j-k*marks >= 0; k++ {
                dp[j] = (dp[j] + dp[j-k*marks]) % mod
            }
        }
    }
    return dp[target]
}

```

---

## number-of-ways-to-reorder-array-to-get-same-bst

```golang
const mod = int(1e9) + 7

func numOfWays(nums []int) int {
	memo := make(map[string]int)
	return (countWays(nums, memo) - 1 + mod) % mod
}

func countWays(nums []int, memo map[string]int) int {
	if len(nums) <= 2 {
		return 1
	}

	key := toString(nums)
	if val, ok := memo[key]; ok {
		return val
	}

	left := make([]int, 0)
	right := make([]int, 0)

	root := nums[0]
	for i := 1; i < len(nums); i++ {
		if nums[i] < root {
			left = append(left, nums[i])
		} else {
			right = append(right, nums[i])
		}
	}

	leftCount := countWays(left, memo)
	rightCount := countWays(right, memo)

	result := comb(len(nums)-1, len(left))
	result = (result * leftCount) % mod
	result = (result * rightCount) % mod

	memo[key] = result
	return result
}

func comb(n, k int) int {
	if k > n/2 {
		k = n - k
	}
	res := 1
	for i := 1; i <= k; i++ {
		res = (res * (n - i + 1)) % mod
		res = (res * modInverse(i)) % mod
	}
	return res
}

func modInverse(a int) int {
	res := 1
	exp := mod - 2
	for exp > 0 {
		if exp%2 == 1 {
			res = (res * a) % mod
		}
		a = (a * a) % mod
		exp >>= 1
	}
	return res
}

func toString(nums []int) string {
	str := ""
	for _, num := range nums {
		str += strconv.Itoa(num)
	}
	return str
}

```

---

## number-of-ways-to-stay-in-the-same-place-after-some-steps

```javascript
/**
 * @param {number} steps
 * @param {number} arrLen
 * @return {number}
 */
var numWays = function(steps, arrLen) {
    // Define a modulus value for taking the modulo operation to avoid overflow.
    const mod = 1000000007;

    // Calculate the maximum position the pointer can reach, which is the minimum of steps/2 and arrLen - 1.
    const maxPosition = Math.min(Math.floor(steps / 2), arrLen - 1);

    // Create a 2D array dp to store the number of ways to reach a specific position at each step.
    const dp = new Array(steps + 1).fill().map(() => new Array(maxPosition + 1).fill(0));

    // Initialize the number of ways to stay at position 0 after 0 steps to 1.
    dp[0][0] = 1;

    // Loop through the number of steps.
    for (let i = 1; i <= steps; i++) {
        for (let j = 0; j <= maxPosition; j++) {
            // Initialize the number of ways to stay at the current position with the number of ways to stay at the same position in the previous step.
            dp[i][j] = dp[i - 1][j];

            // If the current position is greater than 0, add the number of ways to reach it by moving left.
            if (j > 0) {
                dp[i][j] = (dp[i][j] + dp[i - 1][j - 1]) % mod;
            }

            // If the current position is less than the maximum position, add the number of ways to reach it by moving right.
            if (j < maxPosition) {
                dp[i][j] = (dp[i][j] + dp[i - 1][j + 1]) % mod;
            }
        }
    }

    // The final result is stored in dp[steps][0], representing the number of ways to reach the initial position after taking 'steps' steps.
    return dp[steps][0];
};
```

---

## occurrences-after-bigram

```golang
func findOcurrences(text string, first string, second string) []string {
	words := strings.Fields(text)
	result := make([]string, 0)

	for i := 0; i < len(words)-2; i++ {
		if words[i] == first && words[i+1] == second {
			result = append(result, words[i+2])
		}
	}

	return result
}
```

---

## odd-even-linked-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func oddEvenList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    
    oddHead := head
    evenHead := head.Next
    odd := oddHead
    even := evenHead
    
    for even != nil && even.Next != nil {
        odd.Next = even.Next
        odd = odd.Next
        even.Next = odd.Next
        even = even.Next
    }
    
    odd.Next = evenHead
    
    return oddHead

}
```

---

## online-stock-span

```golang
type StockSpanner struct {
    prices []int
    spans  []int
}

func Constructor() StockSpanner {
    return StockSpanner{
        prices: make([]int, 0),
        spans:  make([]int, 0),
    }
}

func (this *StockSpanner) Next(price int) int {
    span := 1
    for len(this.prices) > 0 && price >= this.prices[len(this.prices)-1] {
        this.prices = this.prices[:len(this.prices)-1]
        span += this.spans[len(this.spans)-1]
        this.spans = this.spans[:len(this.spans)-1]
    }
    this.prices = append(this.prices, price)
    this.spans = append(this.spans, span)
    return span
}

/**
 * Your StockSpanner object will be instantiated and called as such:
 * obj := Constructor();
 * param_1 := obj.Next(price);
 */
```

---

## painting-the-walls

```javascript
/**
 * @param {number[]} cost
 * @param {number[]} time
 * @return {number}
 */
var paintWalls = function(cost, time) {
    const n = cost.length; // Get the number of walls
    const dp = new Array(n + 1).fill(Number.MAX_SAFE_INTEGER); // Create a dynamic programming array to store the minimum cost
    dp[0] = 0; // The minimum cost to paint 0 walls is 0 (base case)

    // Loop through each wall
    for (let i = 0; i < n; ++i) {
        // Loop through the dynamic programming array in reverse order
        for (let j = n; j > 0; --j) {
            // Calculate the minimum cost to paint 'j' walls using the current wall 'i'
            // The minimum cost at 'j' is the minimum of:
            //   - The cost of painting the current wall 'i' + the cost of painting the previous walls (dp[j - time[i] - 1])
            //   - The cost of painting the previous walls without using the current wall 'i' (dp[j])
            dp[j] = Math.min(dp[j], dp[Math.max(j - time[i] - 1, 0)] + cost[i]);
        }
    }
    return dp[n]; // The minimum cost to paint all 'n' walls is stored in dp[n]
}
```

---

## palindrome-linked-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func isPalindrome(head *ListNode) bool {
    // Check if the list is empty or contains only one element
    if head == nil || head.Next == nil {
        return true
    }
    
    // Find the middle of the list
    slow, fast := head, head
    for fast != nil && fast.Next != nil {
        slow = slow.Next
        fast = fast.Next.Next
    }
    
    // Reverse the second half of the list
    prev := (*ListNode)(nil)
    curr := slow
    for curr != nil {
        next := curr.Next
        curr.Next = prev
        prev = curr
        curr = next
    }
    
    // Compare the first half with the reversed second half
    p1, p2 := head, prev
    for p2 != nil {
        if p1.Val != p2.Val {
            return false
        }
        p1 = p1.Next
        p2 = p2.Next
    }
    
    return true
}
```

---

## palindrome-number

```c
bool isPalindrome(int x) {
    // Negative numbers are not palindromes
    if (x < 0) {
        return false;
    }

    int original = x;
    long long reversed = 0; // Use long long to prevent overflow

    // Reverse the number
    while (x > 0) {
        int digit = x % 10;
        reversed = reversed * 10 + digit;
        x /= 10;
    }

    // Check if the reversed number is the same as the original
    return original == reversed;
}
```

---

## palindrome-partitioning

```golang
func partition(s string) [][]string {
    var result [][]string
    var current []string
    backtrack(&result, &current, s, 0)
    return result
}

func backtrack(
    result *[][]string, 
    current *[]string, 
    s string, 
    start int) {

    if start >= len(s) {
        temp := make([]string, len(*current))
        copy(temp, *current)
        *result = append(*result, temp)
    }

    for end := start; end < len(s); end++ {
        if isPalindrome(s, start, end) {
            *current = append(*current, s[start:end+1])
            backtrack(result, current, s, end+1)
            *current = (*current)[:len(*current)-1]
        }
    }

}

func isPalindrome(s string, start int, end int) bool {
    for start < end {
        if s[start] != s[end] {
            return false
        }
        start++
        end--
    }
    return true
}


```

---

## parallel-courses-iii

```cpp
class Solution {
public:
    int minimumTime(int n, vector<vector<int>>& A, vector<int>& time) {
        vector<vector<int>>adj(n);
        vector<int>indegree(n, 0);
        for(int i=0; i<A.size(); i++){
            adj[A[i][0]-1].push_back(A[i][1]-1);
            indegree[A[i][1]-1]++;
        }
        queue<int> q;
        vector<int> maxTime(n, 0);
        for(int i=0; i<n; i++){
            if(indegree[i]==0){
                q.push(i);
                maxTime[i]=time[i];
            }
        }
        while(!q.empty()){
            int node=q.front();
            q.pop();
            for(auto it: adj[node]){
                maxTime[it]=max(maxTime[it], maxTime[node]+time[it]);
                indegree[it]--;
                if(indegree[it]==0) q.push(it);
            }
        }
        int ans=0;
        for(int i=0; i<n; i++){
            ans=max(ans, maxTime[i]);
        }
        return ans;
    }
}; 
```

---

## partition-array-into-three-parts-with-equal-sum

```javascript
/**
 * @param {number[]} arr
 * @return {boolean}
 */
var canThreePartsEqualSum = function(arr) {
    const sum = arr.reduce((a,b) => a+b); // Suma de todo
    if (sum % 3) return false; // Si la suman de todo no es divisible entre 3 retorna false

    const target = sum / 3; // Cuanto debe sumar cada parte
    let partSum = 0, count = 0;

    for  (let i = 0; i < arr.length; i++) {
        partSum += arr[i]
        if (partSum === target) {
            count++;
            partSum = 0;
        }
    }

    return count >= 3;
};
```

---

## partition-equal-subset-sum

```golang
func canPartition(nums []int) bool {
    totalSum := 0
    for _, num := range nums {
        totalSum += num
    }
    
    if totalSum%2 != 0 {
        return false
    }
    
    targetSum := totalSum / 2
    dp := make([]bool, targetSum+1)
    dp[0] = true
    
    for _, num := range nums {
        for j := targetSum; j >= num; j-- {
            dp[j] = dp[j] || dp[j-num]
        }
    }
    
    return dp[targetSum]
}
```

---

## partition-labels

```golang
func partitionLabels(s string) []int {
	// Store the last occurrence index of each character
	lastIndex := make(map[byte]int)
	for i := 0; i < len(s); i++ {
		lastIndex[s[i]] = i
	}

	partitionSizes := make([]int, 0)
	start := 0
	end := 0

	for i := 0; i < len(s); i++ {
		// Update the end index to the maximum of current end and the last occurrence index of the current character
		end = max(end, lastIndex[s[i]])

		// If the current index reaches the end index, we have found a partition
		if i == end {
			partitionSizes = append(partitionSizes, end-start+1)
			start = end + 1
		}
	}

	return partitionSizes
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

---

## partition-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func partition(head *ListNode, x int) *ListNode {
	// Create two dummy nodes for the two partitions
	dummy1 := &ListNode{}
	dummy2 := &ListNode{}

	// Create two pointers for the current nodes in each partition
	curr1 := dummy1
	curr2 := dummy2

	// Traverse the original list
	for head != nil {
		// If the current node's value is less than x, add it to the first partition
		if head.Val < x {
			curr1.Next = head
			curr1 = curr1.Next
		} else { // If the current node's value is greater than or equal to x, add it to the second partition
			curr2.Next = head
			curr2 = curr2.Next
		}

		// Move to the next node in the original list
		head = head.Next
	}

	// Connect the two partitions
	curr1.Next = dummy2.Next
	curr2.Next = nil

	// Return the head of the first partition
	return dummy1.Next
}
```

---

## pascals-triangle

```javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    let pascalTriangle = [];
    for (let i = 0; i < numRows; i++) {
        if (i == 0) pascalTriangle.push([1]);
        if (i == 1) pascalTriangle.push([1, 1]);
        if (i >= 2) {
            let row = [1];
            for (let j = 0; j < pascalTriangle[i-1].length-1; j++) {
                let r = pascalTriangle[i-1][j] + pascalTriangle[i-1][j+1];
                row.push(r);
            }
            row.push(1);
            pascalTriangle.push(row);
        }
    }
    return pascalTriangle;
};
```

---

## pascals-triangle-ii

```javascript
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    if (rowIndex < 0) {
        return [];
    }
    
    // Initialize the first row with a single element 1.
    let row = [1];
    
    for (let i = 1; i <= rowIndex; i++) {
        const newRow = [1]; // The first element of each row is always 1.
        for (let j = 1; j < row.length; j++) {
            newRow.push(row[j - 1] + row[j]);
        }
        newRow.push(1); // The last element of each row is always 1.
        
        row = newRow; // Update the current row.
    }
    
    return row;
};

```

---

## path-sum

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */

/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function(root, targetSum) {
  if (!root) {
    // If the root is null, there are no root-to-leaf paths
    return false;
  }

  if (!root.left && !root.right) {
    // If the current node is a leaf, check if its value equals the remaining target sum
    return root.val === targetSum;
  }

  // Recursively check if there is a path in the left or right subtree
  const remainingSum = targetSum - root.val;
  return (
    hasPathSum(root.left, remainingSum) ||
    hasPathSum(root.right, remainingSum)
  );
};

```

---

## path-sum-iii

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, targetSum int) int {
    if root == nil {
        return 0
    }
    
    return countPaths(root, targetSum) + pathSum(root.Left, targetSum) + pathSum(root.Right, targetSum)
}

func countPaths(node *TreeNode, targetSum int) int {
    if node == nil {
        return 0
    }
    
    count := 0
    if node.Val == targetSum {
        count++
    }
    
    count += countPaths(node.Left, targetSum-node.Val)
    count += countPaths(node.Right, targetSum-node.Val)
    
    return count
}
```

---

## patients-with-a-condition

```mysql
# Write your MySQL query statement below

select patient_id, patient_name, conditions
from Patients
where conditions like '% DIAB1%'
or conditions like 'DIAB1%'
```

---

## percentage-of-users-attended-a-contest

```mysql
# Write your MySQL query statement below

select r.contest_id, round(count(r.user_id)*100.0 / u.total_users, 2) as percentage
from Register r
inner join Users u on r.user_id = u.user_id
cross join (
    select count(*) as total_users from Users
) u
group by r.contest_id
order by percentage desc, r.contest_id asc;
```

---

## perfect-number

```javascript
/**
 * @param {number} num
 * @return {boolean}
 */
var checkPerfectNumber = function(num) {
  if (num <= 1) {
    return false;
  }

  var sum = 1;
  var sqrt = Math.floor(Math.sqrt(num));

  for (var i = 2; i <= sqrt; i++) {
    if (num % i === 0) {
      sum += i;

      var complement = num / i;
      if (complement !== i) {
        sum += complement;
      }
    }
  }

  return sum === num;
};

```

---

## perfect-squares

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var numSquares = function(n) {
    // Create an array to store the minimum number of perfect squares for each value from 0 to n
    const dp = new Array(n + 1).fill(Number.MAX_SAFE_INTEGER);
  
    // Initialize the base case: 0 requires 0 perfect squares
    dp[0] = 0;
  
    // Iterate from 1 to n
    for (let i = 1; i <= n; i++) {
    // Iterate over all possible perfect squares less than or equal to i
        for (let j = 1; j * j <= i; j++) {
            // Calculate the minimum number of perfect squares for i
            dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
        }
    }
  
  // Return the result for n
  return dp[n];
};
```

---

## permutation-sequence

```golang
func getPermutation(n int, k int) string {
    fact := make([]int, n)
    numbers := make([]int, n)
    
    fact[0] = 1
    for i := 1; i < n; i++ {
        fact[i] = fact[i-1] * i
    }
    
    for i := 1; i <= n; i++ {
        numbers[i-1] = i
    }
    
    k-- // Convert to 0-based index
    
    var result strings.Builder
    for i := n; i >= 1; i-- {
        index := k / fact[i-1]
        k %= fact[i-1]
        
        result.WriteString(strconv.Itoa(numbers[index]))
        numbers = append(numbers[:index], numbers[index+1:]...)
    }
    
    return result.String()
}

```

---

## permutations

```golang
func permute(nums []int) [][]int {
    permutations := [][]int{}

    backtrack(nums, &permutations, 0)

    return permutations
}

func backtrack(nums []int, permutations *[][]int, start int) {
    if start == len(nums) {
        currentPermutation := make([]int, len(nums))
        copy(currentPermutation, nums)
        *permutations = append(*permutations, currentPermutation)
        return
    }

    for i := start; i < len(nums); i++ {
        nums[start], nums[i] = nums[i], nums[start]

        backtrack(nums, permutations, start+1)

        nums[start], nums[i] = nums[i], nums[start]
    }

}
```

---

## permutations-ii

```golang
func permuteUnique(nums []int) [][]int {
    var result [][]int
    var current []int
    used := make([]bool, len(nums))
    sort.Ints(nums) // Sort the input to handle duplicates easily
    backtrack(nums, used, current, &result)
    return result
}

func backtrack(nums []int, used []bool, current []int, result *[][]int) {
    if len(current) == len(nums) {
        // Create a copy of the current permutation to avoid modifying it later
        temp := make([]int, len(current))
        copy(temp, current)
        *result = append(*result, temp)
        return
    }

    for i := 0; i < len(nums); i++ {
        if used[i] || (i > 0 && nums[i] == nums[i-1] && !used[i-1]) {
            // Skip duplicates and already used numbers
            continue
        }
        used[i] = true
        current = append(current, nums[i])
        backtrack(nums, used, current, result)
        used[i] = false
        current = current[:len(current)-1]
    }
}
```

---

## plus-one

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* plusOne(int* digits, int digitsSize, int* returnSize) {
    // Add one to the least significant digit
    digits[digitsSize - 1] += 1;

    // Initialize carry
    int carry = 0;

    // Iterate from right to left
    for (int i = digitsSize - 1; i >= 0; i--) {
        digits[i] += carry;

        // Update carry for the next iteration
        carry = digits[i] / 10;
        digits[i] %= 10;
    }

    // If there's still a carry, we need to add an additional digit
    if (carry > 0) {
        (*returnSize) = digitsSize + 1;
        int* result = (int*)malloc((*returnSize) * sizeof(int));
        result[0] = carry;

        // Copy the original digits to the result array
        for (int i = 0; i < digitsSize; i++) {
            result[i + 1] = digits[i];
        }

        return result;
    } else {
        (*returnSize) = digitsSize;
        return digits;
    }
}
```

---

## poor-pigs

```golang
func poorPigs(buckets int, minutesToDie int, minutesToTest int) int {
    // Calculate the number of tests we can perform
    tests := minutesToTest/minutesToDie + 1

    // Calculate the number of pigs needed
    pigs := 0
    for pow := 1; pow < buckets; pow *= tests {
        pigs++
    }

    return pigs
}
```

---

## populating-next-right-pointers-in-each-node-ii

```golang
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Left *Node
 *     Right *Node
 *     Next *Node
 * }
 */

func connect(root *Node) *Node {
	if root == nil {
		return nil
	}
	
	queue := []*Node{root}
	
	for len(queue) > 0 {
		levelSize := len(queue)
		
		for i := 0; i < levelSize; i++ {
			node := queue[0]
			queue = queue[1:]
			
			if i < levelSize-1 {
				node.Next = queue[0]
			}
			
			if node.Left != nil {
				queue = append(queue, node.Left)
			}
			
			if node.Right != nil {
				queue = append(queue, node.Right)
			}
		}
	}
	
	return root
}
```

---

## positions-of-large-groups

```golang
func largeGroupPositions(s string) [][]int {
    result := make([][]int, 0)
    n := len(s)
    
    for i := 0; i < n; {
        char := s[i]
        start := i
        count := 0
        
        // Count consecutive characters
        for i < n && s[i] == char {
            count++
            i++
        }
        
        // Check if the group is large (count >= 3)
        if count >= 3 {
            result = append(result, []int{start, i - 1})
        }
    }
    
    return result
}

```

---

## power-of-four

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isPowerOfFour = function(n) {
    if (n <= 0) {
        return false;
    }
    return Number.isInteger(Math.log(n) / Math.log(4));    
};
```

---

## power-of-three

```golang
func isPowerOfThree(n int) bool {
	return n > 0 && 1162261467%n == 0
}
```

---

## power-of-two

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isPowerOfTwo = n => ~~Math.log2(n) == Math.log2(n);
```

---

## powx-n

```golang
func myPow(x float64, n int) float64 {
    // Any number to the power 0 is equal to 1
    if n == 0 {
        return 1
    }
    // If the power is a negative number we invert the value of x and change make n positive.
    if n < 0 {
        x = 1 / x
        n = -n
    }
    res := 1.0
    for n > 0 {
        if n%2 == 1 {
            res *= x
        }
        x *= x
        n /= 2
    }
    return res
}
```

---

## primary-department-for-each-employee

```mysql
# Write your MySQL query statement below

select employee_id, department_id
from Employee
where primary_flag = 'Y'
union
select employee_id, department_id
from Employee
where employee_id NOT IN (
    select employee_id
    from Employee
    where primary_flag = 'Y'
)

```

---

## prime-number-of-set-bits-in-binary-representation

```golang
func countPrimeSetBits(left int, right int) int {
	count := 0

	for num := left; num <= right; num++ {
		bitCount := countSetBits(num)
		if isPrime(bitCount) {
			count++
		}
	}

	return count
}

func countSetBits(num int) int {
	count := 0

	for num > 0 {
		if num&1 == 1 {
			count++
		}
		num >>= 1
	}

	return count
}

func isPrime(num int) bool {
	if num <= 1 {
		return false
	}

	for i := 2; i*i <= num; i++ {
		if num%i == 0 {
			return false
		}
	}

	return true
}

```

---

## product-of-array-except-self

```typescript
function productExceptSelf(nums: number[]): number[] {
    const n = nums.length;
    const output: number[] = new Array(n);
    
    // Calculate the product of all elements to the left of each element
    let leftProduct = 1;
    for (let i = 0; i < n; i++) {
        output[i] = leftProduct;
        leftProduct *= nums[i];
    }
    
    // Calculate the product of all elements to the right of each element
    let rightProduct = 1;
    for (let i = n - 1; i >= 0; i--) {
        output[i] *= rightProduct;
        rightProduct *= nums[i];
    }
    
    return output;
};
```

---

## product-price-at-a-given-date

```mysql
# Write your MySQL query statement below

select distinct product_id, 10 as price
from Products
group by product_id
having (min(change_date) > "2019-08-16")

union

select p2.product_id, new_price
from Products p2
where (p2.product_id, p2.change_date) in (
    select product_id, max(change_date) as recent_date
    from Products
    where change_date <= "2019-08-16"
    group by product_id
)
```

---

## product-sales-analysis-i

```mysql
# Write your MySQL query statement below

select p.product_name, s.year, s.price 
from Sales s
join Product p on s.product_id = p.product_id
```

---

## product-sales-analysis-iii

```mysql
# Write your MySQL query statement below

select s.product_id, s.year as first_year, s.quantity, s.price
from Sales s
inner join (
    select product_id, min(year) as min_year
    from Sales
    group by product_id
) t on s.product_id = t.product_id and s.year = t.min_year

```

---

## project-employees-i

```mysql
# Write your MySQL query statement below

select project_id, round(avg(experience_years), 2) as average_years
from Project
join Employee on Project.employee_id = Employee.employee_id
group by project_id;

```

---

## projection-area-of-3d-shapes

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var projectionArea = function(grid) {
    let n = grid.length;
    let xyProjection = 0;
    let xzProjection = 0;
    let yzProjection = 0;

    for (let i = 0; i < n; i++) {
        let maxRow = 0;
        let maxCol = 0;

        for (let j = 0; j < n; j++) {
            if (grid[i][j] > 0) {
                xyProjection++;
            }
            maxRow = Math.max(maxRow, grid[i][j]);
            maxCol = Math.max(maxCol, grid[j][i]);
        }

        xzProjection += maxRow;
        yzProjection += maxCol;
    }

    const totalArea = xyProjection + xzProjection + yzProjection;

    return totalArea;
};
```

---

## promise-time-limit

```javascript
/**
 * @param {Function} fn
 * @param {number} t
 * @return {Function}
 */
var timeLimit = function(fn, t) {
	return async function(...args) {
        const promise = fn(...args);
        const timeout = new Promise((resolve, reject) => {
            setTimeout(() => reject(`Time Limit Exceeded`), t);
        });
        return Promise.race([promise, timeout]);
    }
};

/**
 * const limited = timeLimit((t) => new Promise(res => setTimeout(res, t)), 100);
 * limited(150).catch(console.log) // "Time Limit Exceeded" at t=100ms
 */
```

---

## queries-quality-and-percentage

```mysql
# Write your MySQL query statement below

select
  query_name,
  round(avg(cast(rating as DECIMAL) / position), 2) as quality,
  round((count(case when rating < 3 then 1 end) / count(*) * 100), 2) as poor_query_percentage
from
  Queries
group by
  query_name;

```

---

## range-addition-ii

```javascript
/**
 * @param {number} m
 * @param {number} n
 * @param {number[][]} ops
 * @return {number}
 */
var maxCount = function(m, n, ops) {
  let minRow = m;
  let minCol = n;
  
  for (let [row, col] of ops) {
    minRow = Math.min(minRow, row);
    minCol = Math.min(minCol, col);
  }
  
  return minRow * minCol;
};

```

---

## range-sum-of-bst

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} low
 * @param {number} high
 * @return {number}
 */
var rangeSumBST = function(root, low, high) {
    if (!root) {
        return 0;
    }
    
    let sum = 0;
    
    if (root.val >= low && root.val <= high) {
        sum += root.val;
    }

    sum += rangeSumBST(root.left, low, high);
    sum += rangeSumBST(root.right, low, high);
    
    return sum;
};
```

---

## range-sum-query-immutable

```golang
type NumArray struct {
	prefixSum []int
}

func Constructor(nums []int) NumArray {
	n := len(nums)
	prefixSum := make([]int, n+1)

	for i := 1; i <= n; i++ {
		prefixSum[i] = prefixSum[i-1] + nums[i-1]
	}

	return NumArray{
		prefixSum: prefixSum,
	}
}

func (this *NumArray) SumRange(left int, right int) int {
	return this.prefixSum[right+1] - this.prefixSum[left]
}



/**
 * Your NumArray object will be instantiated and called as such:
 * obj := Constructor(nums);
 * param_1 := obj.SumRange(left,right);
 */
```

---

## rank-scores

```pythondata
import pandas as pd

def order_scores(scores: pd.DataFrame) -> pd.DataFrame:
    # Use the rank method to assign ranks to the scores in descending order with no gaps
    scores['rank'] = scores['score'].rank(method='dense', ascending=False)
    
    # Drop id column & Sort the DataFrame by score in descending order
    result_df = scores.drop('id',axis=1).sort_values(by='score', ascending=False)
    
    return result_df
```

---

## ransom-note

```golang
func canConstruct(ransomNote string, magazine string) bool {
    // Create a frequency map for characters in the magazine
    magazineMap := make(map[rune]int)
    for _, ch := range magazine {
        magazineMap[ch]++
    }
    
    // Check if the ransom note can be constructed
    for _, ch := range ransomNote {
        count, exists := magazineMap[ch]
        if !exists || count == 0 {
            return false
        }
        magazineMap[ch]--
    }
    
    return true
}

```

---

## rearrange-products-table

```pythondata
import pandas as pd

def rearrange_products_table(products: pd.DataFrame) -> pd.DataFrame:
    store_columns = products.columns[1:]  # Get the store columns
    rows = []
    
    for index, row in products.iterrows():
        for store_col in store_columns:
            if pd.notna(row[store_col]):
                rows.append([row['product_id'], store_col, row[store_col]])
    
    result = pd.DataFrame(rows, columns=['product_id', 'store', 'price'])
    return result
```

---

## rearrange-spaces-between-words

```javascript
/**
 * @param {string} text
 * @return {string}
 */
var reorderSpaces = function(text) {
    let spaces = text.replaceAll(/[^ ]/g, "").length; // 2nd way: Array.from(text.matchAll(/[ ]/g))
    let words = text.trim().split(/ +/);

    let remainder = spaces % (words.length - 1);
    let separator = " ".repeat((spaces-remainder)/(words.length - 1));

    if (words.length == 1) return words.join("") + " ".repeat(spaces);

    return words.join(separator) + " ".repeat(remainder);
};
```

---

## rectangle-overlap

```golang
func isRectangleOverlap(rec1 []int, rec2 []int) bool {
    return !(rec1[2] <= rec2[0] ||   // rec1 is to the left of rec2
             rec1[0] >= rec2[2] ||   // rec1 is to the right of rec2
             rec1[1] >= rec2[3] ||   // rec1 is above rec2
             rec1[3] <= rec2[1])     // rec1 is below rec2
}

```

---

## recyclable-and-low-fat-products

```mysql
# Write your MySQL query statement below

select product_id from Products where low_fats = "Y" and recyclable = "Y";
```

---

## regular-expression-matching

```golang
func isMatch(s string, p string) bool {
    n, m := len(s), len(p)
    
    // Crear una matriz dp de (n+1) x (m+1) para almacenar los resultados de subproblemas
    dp := make([][]bool, n+1)
    for i := range dp {
        dp[i] = make([]bool, m+1)
    }

    // El patrón vacío solo puede emparejar una cadena vacía
    dp[0][0] = true
    
    // Si el patrón tiene un '*', el caracter anterior debe ser ignorado
    for j := 2; j <= m; j++ {
        if p[j-1] == '*' {
            dp[0][j] = dp[0][j-2]
        }
    }
    
    // Llenar la matriz dp utilizando la relación de recurrencia
    for i := 1; i <= n; i++ {
        for j := 1; j <= m; j++ {
            // Si los caracteres coinciden o el patrón tiene un punto, 
            // los resultados anteriores son relevantes
            if s[i-1] == p[j-1] || p[j-1] == '.' {
                dp[i][j] = dp[i-1][j-1]
            } else if p[j-1] == '*' {
                // Si el patrón tiene un '*', hay dos posibilidades:
                if s[i-1] == p[j-2] || p[j-2] == '.' {
                    // 1. Ignorar el '*' y el caracter anterior
                    // y comprobar si los subproblemas anteriores se resolvieron con éxito
                    dp[i][j] = dp[i][j-2] || 
                        // 2. O emparejar el caracter actual 
                        // y comprobar si el subproblema anterior se resolvió con éxito
                        dp[i-1][j]
                } else {
                    // El caracter anterior y el '*' no coinciden con el caracter actual, 
                    // por lo que solo podemos ignorarlos
                    dp[i][j] = dp[i][j-2]
                }
            }
        }
    }
    
    // El resultado final se encuentra en dp[n][m]
    return dp[n][m]
}


```

---

## relative-ranks

```javascript
/**
 * @param {number[]} score
 * @return {string[]}
 */
var findRelativeRanks = function(score) {
  var sortedScore = [...score].sort((a, b) => b - a);
  var rankMap = new Map();

  for (var i = 0; i < sortedScore.length; i++) {
    if (i === 0) {
      rankMap.set(sortedScore[i], "Gold Medal");
    } else if (i === 1) {
      rankMap.set(sortedScore[i], "Silver Medal");
    } else if (i === 2) {
      rankMap.set(sortedScore[i], "Bronze Medal");
    } else {
      rankMap.set(sortedScore[i], (i + 1).toString());
    }
  }

  var result = [];
  for (var j = 0; j < score.length; j++) {
    result.push(rankMap.get(score[j]));
  }

  return result;
};

```

---

## remove-all-adjacent-duplicates-in-string

```golang
func removeDuplicates(s string) string {
    stack := []rune{} // Use a stack of runes to handle non-ASCII characters

    for _, char := range s {
        if len(stack) > 0 && stack[len(stack)-1] == char {
            // Pop the top character if it's equal to the current character
            stack = stack[:len(stack)-1]
        } else {
            // Push the current character onto the stack
            stack = append(stack, char)
        }
    }

    return string(stack)
}

```

---

## remove-colored-pieces-if-both-neighbors-are-the-same-color

```golang
func winnerOfGame(colors string) bool {
    countA := 0
    countB := 0

    for i := 0; i < len(colors); i++ {
        x := colors[i]
        count := 0

        for i < len(colors) && colors[i] == x {
            i++
            count++
        }

        if x == 'A' {
            countA += max(count-2, 0)
        } else if x == 'B' {
            countB += max(count-2, 0)
        }

        i--
    }

    return countA > countB
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}
```

---

## remove-duplicates-from-sorted-array

```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0;
    }

    int uniqueCount = 1; // Initialize with 1 for the first element
    int i;

    for (i = 1; i < numsSize; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[uniqueCount] = nums[i];
            uniqueCount++;
        }
    }

    return uniqueCount;
}
```

---

## remove-duplicates-from-sorted-array-ii

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let count = 1; // Count for the current element
  let j = 1; // Position to overwrite duplicates

  for (let i = 1; i < nums.length; i++) {
    // If the current element is the same as the previous one
    if (nums[i] === nums[i - 1]) {
      count++; // Increment the count

      // If the count is less than or equal to 2, keep the element
      if (count <= 2) {
        nums[j] = nums[i]; // Overwrite duplicates
        j++; // Move to the next position to overwrite
      }
    } else {
      // Reset the count for a new element
      count = 1;
      nums[j] = nums[i]; // Overwrite non-duplicates
      j++; // Move to the next position to overwrite
    }
  }

  return j; // Return the new length of the array
}

```

---

## remove-duplicates-from-sorted-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteDuplicates(head *ListNode) *ListNode {
    current := head

    for current != nil && current.Next != nil {
        if current.Val == current.Next.Val {
            current.Next = current.Next.Next
        } else {
            current = current.Next
        }
    }

    return head
}
```

---

## remove-duplicates-from-sorted-list-ii

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteDuplicates(head *ListNode) *ListNode {
	// Create a dummy node as the previous node of the head
	dummy := &ListNode{Next: head}
	prev := dummy
	current := head

	for current != nil {
		// Skip all duplicate nodes
		for current.Next != nil && current.Val == current.Next.Val {
			current = current.Next
		}

		// If no duplicates, update the prev and current pointers
		if prev.Next == current {
			prev = prev.Next
		} else {
			prev.Next = current.Next
		}

		current = current.Next
	}

	return dummy.Next
}

func createLinkedList(arr []int) *ListNode {
	if len(arr) == 0 {
		return nil
	}

	head := &ListNode{
		Val: arr[0],
	}

	current := head
	for i := 1; i < len(arr); i++ {
		node := &ListNode{
			Val: arr[i],
		}
		current.Next = node
		current = current.Next
	}

	return head
}

func printLinkedList(head *ListNode) {
	current := head
	for current != nil {
		fmt.Print(current.Val, " ")
		current = current.Next
	}
	fmt.Println()
}

```

---

## remove-element

```c
int removeElement(int* nums, int numsSize, int val) {
    int nonValCount = 0; // Count of elements not equal to val

    for (int i = 0; i < numsSize; i++) {
        if (nums[i] != val) {
            nums[nonValCount] = nums[i];
            nonValCount++;
        }
    }

    return nonValCount;
}
```

---

## remove-linked-list-elements

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeElements(head *ListNode, val int) *ListNode {
	dummy := &ListNode{Next: head}
	prev := dummy
	current := head

	for current != nil {
		if current.Val == val {
			prev.Next = current.Next
		} else {
			prev = current
		}
		current = current.Next
	}

	return dummy.Next
}

// Helper function to create a linked list from an array
func createLinkedList(arr []int) *ListNode {
	dummy := &ListNode{}
	current := dummy

	for _, val := range arr {
		current.Next = &ListNode{Val: val}
		current = current.Next
	}

	return dummy.Next
}

// Helper function to convert a linked list to a string
func linkedListToString(head *ListNode) string {
	result := ""
	current := head

	for current != nil {
		result += fmt.Sprintf("%d -> ", current.Val)
		current = current.Next
	}

	result += "nil"

	return result
}

/*
In this implementation, the removeElements function takes a pointer to the head of the linked list and an integer val to remove. It uses a dummy node and two pointers (prev and current) to iterate through the linked list. If the current node has a value equal to val, it bypasses the current node by updating the Next pointer of the previous node. Otherwise, it updates the prev pointer to the current node. Finally, it returns the Next pointer of the dummy node, which points to the modified head of the linked list.

The createLinkedList function is a helper function that takes an array of integers and creates a linked list. The linkedListToString function converts a linked list to a string representation for printing purposes.
*/
```

---

## remove-nth-node-from-end-of-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func removeNthFromEnd(head *ListNode, n int) *ListNode {
	// Create a dummy node as the previous node of the head
	dummy := &ListNode{Next: head}
	slow := dummy
	fast := dummy

	// Move the fast pointer n steps ahead
	for i := 0; i <= n; i++ {
		fast = fast.Next
	}

	// Move the slow and fast pointers simultaneously until the fast pointer reaches the end
	for fast != nil {
		slow = slow.Next
		fast = fast.Next
	}

	// Remove the nth node from the end by adjusting the pointers
	slow.Next = slow.Next.Next

	return dummy.Next
}

func createLinkedList(arr []int) *ListNode {
	if len(arr) == 0 {
		return nil
	}

	head := &ListNode{
		Val: arr[0],
	}

	current := head
	for i := 1; i < len(arr); i++ {
		node := &ListNode{
			Val: arr[i],
		}
		current.Next = node
		current = current.Next
	}

	return head
}

func printLinkedList(head *ListNode) {
	current := head
	for current != nil {
		fmt.Print(current.Val, " ")
		current = current.Next
	}
	fmt.Println()
}
```

---

## remove-outermost-parentheses

```golang
func removeOuterParentheses(s string) string {
    result := ""
    balance := 0

    for _, char := range s {
        if char == '(' {
            if balance > 0 {
                result += string(char)
            }
            balance++
        } else if char == ')' {
            balance--
            if balance > 0 {
                result += string(char)
            }
        }
    }

    return result
}

```

---

## removing-stars-from-a-string

```golang
func removeStars(s string) string {
    // Convert the string to a slice of runes for easier manipulation.
    chars := []rune(s)
    // Use two pointers: i for iterating through the string, and j for keeping track of the valid characters.
    j := 0
    for i := 0; i < len(chars); i++ {
        if chars[i] != '*' {
            chars[j] = chars[i]
            j++
        } else {
            j--
        }
    }
    // Convert the slice of runes back to a string and return it.
    return string(chars[:j])
}

```

---

## reorder-routes-to-make-all-paths-lead-to-the-city-zero

```typescript
function minReorder(n: number, connections: number[][]): number {
  const graph = new Map<number, number[]>();
  const visited = new Set<number>();
  let changes = 0;

  for (const [from, to] of connections) {
    if (!graph.has(from)) {
      graph.set(from, []);
    }
    if (!graph.has(to)) {
      graph.set(to, []);
    }

    graph.get(from)!.push(to);
    graph.get(to)!.push(-from); // Mark reverse connections with negative sign
  }

  dfs(0); // Start DFS from city 0

  function dfs(city: number): void {
    visited.add(city);

    for (const neighbor of graph.get(city)!) {
      if (!visited.has(Math.abs(neighbor))) {
        changes += neighbor > 0 ? 1 : 0; // Increase changes count if the connection is reversed
        dfs(Math.abs(neighbor));
      }
    }
  }

  return changes;
}

```

---

## repeated-substring-pattern

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var repeatedSubstringPattern = function(s) {
  var n = s.length;
  
  // Try all possible substrings
  for (var i = 1; i <= Math.floor(n / 2); i++) {
    if (n % i === 0) {
      var substring = s.slice(0, i);
      var repeatedSubstring = substring.repeat(n / i);
      
      if (repeatedSubstring === s) {
        return true;
      }
    }
  }
  
  return false;
};
```

---

## replace-employee-id-with-the-unique-identifier

```mysql
# Write your MySQL query statement below

select EmployeeUNI.unique_id, Employees.name
from Employees
left join EmployeeUNI on Employees.id = EmployeeUNI.id
order by Employees.id;
```

---

## reshape-the-matrix

```javascript
/**
 * @param {number[][]} mat
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(mat, r, c) {
  const m = mat.length; // Number of rows in the original matrix
  const n = mat[0].length; // Number of columns in the original matrix

  // Check if the reshape operation is possible
  if (m * n !== r * c) {
    return mat; // Reshape is not possible, return the original matrix
  }

  // Flatten the original matrix into a 1D array
  const flattened = mat.flat();

  // Create the reshaped matrix
  const reshaped = [];
  let index = 0;

  // Fill the reshaped matrix with the elements from the flattened array
  for (let i = 0; i < r; i++) {
    const row = [];
    for (let j = 0; j < c; j++) {
      row.push(flattened[index]);
      index++;
    }
    reshaped.push(row);
  }

  return reshaped;
};
```

---

## restaurant-growth

```mysql
# Write your MySQL query statement below

with helpDATE as (
    select date_add(visited_on, interval 6 day) as seven_day
    from Customer
), moving_amount as (
    select visited_on, sum(sum(amount)) over window_frame as amount,
    round(avg(sum(amount)) over window_frame, 2) as average_amount
    from Customer
    group by visited_on window window_frame as (
        order by visited_on rows between 6 preceding and current row 
    )
)

select visited_on, amount, average_amount
from moving_amount
where visited_on in (select * from helpDATE)
```

---

## restore-ip-addresses

```golang
func restoreIpAddresses(s string) []string {
    var result []string
    var currentIP []string
    backtrack(0, s, &currentIP, &result)
    return result
}

func backtrack(start int, s string, currentIP *[]string, result *[]string) {
    if start == len(s) && len(*currentIP) == 4 {
        *result = append(*result, strings.Join(*currentIP, "."))
        return
    }

    if len(*currentIP) == 4 || len(s)-start > (4-len(*currentIP))*3 {
        return
    }

    for i := 1; i <= 3 && start+i <= len(s); i++ {
        substring := s[start : start+i]
        num, _ := strconv.Atoi(substring)

        if num <= 255 {
            *currentIP = append(*currentIP, substring)
            backtrack(start+i, s, currentIP, result)
            *currentIP = (*currentIP)[:len(*currentIP)-1]
        }

        if s[start] == '0' {
            break
        }
    }
}

```

---

## restore-the-array-from-adjacent-pairs

```golang
func restoreArray(adjacentPairs [][]int) []int {
    // Create a hashmap to store adjacent pairs
    adjacentMap := make(map[int][]int)

    // Fill the hashmap with adjacent pairs
    for _, pair := range adjacentPairs {
        u, v := pair[0], pair[1]
        adjacentMap[u] = append(adjacentMap[u], v)
        adjacentMap[v] = append(adjacentMap[v], u)
    }

    // Find the starting element (the one with only one adjacent pair)
    var start int
    for num, adjacents := range adjacentMap {
        if len(adjacents) == 1 {
            start = num
            break
        }
    }

    // Reconstruct the array using the adjacent pairs
    n := len(adjacentPairs) + 1
    result := make([]int, n)
    result[0] = start

    for i := 1; i < n; i++ {
        prev := result[i-1]
        next := adjacentMap[prev][0]
        result[i] = next

        // Remove the used adjacent pair to avoid revisiting it
        delete(adjacentMap, prev)
        adjacentMap[next] = removeValue(adjacentMap[next], prev)
    }

    return result
}

func removeValue(arr []int, val int) []int {
    for i, num := range arr {
        if num == val {
            return append(arr[:i], arr[i+1:]...)
        }
    }
    return arr
}

```

---

## return-length-of-arguments-passed

```javascript
/**
 * @return {number}
 */
var argumentsLength = function(...args) {
    return args.length;
};

/**
 * argumentsLength(1, 2, 3); // 3
 */
```

---

## reverse-bits

```javascript
/**
 * @param {number} n - a positive integer
 * @return {number} - a positive integer
 */
var reverseBits = function(n) {
  let result = 0;
  for (let i = 0; i < 32; i++) {
    result <<= 1; // Left shift result by 1 bit
    result |= n & 1; // Set the least significant bit of result to the least significant bit of n
    n >>= 1; // Right shift n by 1 bit
  }
  return result >>> 0; // Convert result to unsigned integer
};
```

---

## reverse-integer

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let isnegative = x < 0;
    x = x.toString().replace("-", "");
    x = x.split("").reverse().join("").replace("^0+");
    x = parseInt(x) * (isnegative ? -1: 1);
    if (x > 2 ** 31 - 1 || x < -(2 ** 31)) return 0;
    return x;
};
```

---

## reverse-linked-list

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
    return reverseListRecursive(head)
};

function reverseListIterative(head: ListNode | null): ListNode | null {
  let prev: ListNode | null = null;
  let current: ListNode | null = head;

  while (current !== null) {
    const nextNode: ListNode | null = current.next;
    current.next = prev;
    prev = current;
    current = nextNode;
  }

  return prev;
}

function reverseListRecursive(head: ListNode | null): ListNode | null {
  if (head === null || head.next === null) {
    return head;
  }

  const reversedHead: ListNode | null = reverseListRecursive(head.next);
  head.next.next = head;
  head.next = null;

  return reversedHead;
}
```

---

## reverse-linked-list-ii

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseBetween(head: ListNode | null, left: number, right: number): ListNode | null {
    if (!head || left === right) {
        return head;
    }
    
    // Create a dummy node to handle cases where left = 1
    const dummy = new ListNode(0);
    dummy.next = head;
    
    // Find the node at position (left - 1)
    let preLeft: ListNode | null = dummy;
    for (let i = 1; i < left; i++) {
        preLeft = preLeft!.next;
    }
    
    // Reverse the sublist from left to right
    let prev: ListNode | null = null;
    let curr: ListNode | null = preLeft!.next;
    for (let i = left; i <= right; i++) {
        const next = curr!.next;
        curr!.next = prev;
        prev = curr;
        curr = next;
    }
    
    // Connect the reversed sublist back to the original list
    preLeft!.next.next = curr;
    preLeft!.next = prev;
    
    return dummy.next;
}

```

---

## reverse-nodes-in-k-group

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseKGroup(head *ListNode, k int) *ListNode {
	count := 0
	current := head

	// Count the number of nodes in the list
	for count < k && current != nil {
		current = current.Next
		count++
	}

	// If there are at least k nodes, reverse them
	if count == k {
		nextGroupHead := reverseKGroup(current, k) // Reverse the remaining groups recursively

		// Reverse the current group
		for count > 0 {
			next := head.Next
			head.Next = nextGroupHead
			nextGroupHead = head
			head = next
			count--
		}

		head = nextGroupHead
	}

	return head
}

func createLinkedList(arr []int) *ListNode {
	if len(arr) == 0 {
		return nil
	}

	head := &ListNode{
		Val: arr[0],
	}

	current := head
	for i := 1; i < len(arr); i++ {
		node := &ListNode{
			Val: arr[i],
		}
		current.Next = node
		current = current.Next
	}

	return head
}

func printLinkedList(head *ListNode) {
	current := head
	for current != nil {
		fmt.Print(current.Val, " ")
		current = current.Next
	}
	fmt.Println()
}
```

---

## reverse-only-letters

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseOnlyLetters = function(s) {
    s = s.split("");

    let left = 0;
    let right = s.length - 1;

    while (left < right) {
        while (left < right && !isLetter(s[left])) left++;
        while (left < right &&!isLetter(s[right])) right--;
        [s[left], s[right]] = [s[right], s[left]];
        left++;
        right--;
    }

    return s.join("");
};

var isLetter = function(char) {
    return /[a-zA-Z]/.test(char);
}
```

---

## reverse-string

```golang
func reverseString(s []byte) {
	left := 0
	right := len(s) - 1

	for left < right {
		s[left], s[right] = s[right], s[left]
		left++
		right--
	}
}

/*
In this implementation, the reverseString function takes an array of characters s and reverses it in-place. It initializes left and right pointers to the beginning and end of the array, respectively. It then iterates while left is less than right. In each iteration, it swaps the characters at the left and right positions using the tuple assignment s[left], s[right] = s[right], s[left], and increments left and decrements right. This process continues until the pointers meet or cross each other, resulting in the reversed array.
*/
```

---

## reverse-string-ii

```javascript
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function(s, k) {
  var chars = s.split('');

  for (var i = 0; i < chars.length; i += 2 * k) {
    var left = i;
    var right = Math.min(i + k - 1, chars.length - 1);

    while (left < right) {
      var temp = chars[left];
      chars[left] = chars[right];
      chars[right] = temp;

      left++;
      right--;
    }
  }

  return chars.join('');
};

```

---

## reverse-vowels-of-a-string

```typescript
function reverseVowels(s: string): string {
    const vowels = ['a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'];
    const arr = s.split('');
    let start = 0;
    let end = s.length - 1;

    while (start < end) {
        while (start < end && !vowels.includes(arr[start])) {
        start++;
        }

        while (start < end && !vowels.includes(arr[end])) {
        end--;
        }

        if (start < end) {
        const temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
        }
    }

    return arr.join('');
};
```

---

## reverse-words-in-a-string

```typescript
function reverseWords(s: string): string {
    // Trim leading and trailing spaces
    s = s.trim();

    // Split the string into an array of words
    const words = s.split(/\s+/);

    // Reverse the array of words
    const reversedWords = words.reverse();

    // Join the reversed words with a single space
    const reversedString = reversedWords.join(' ');

    return reversedString;
};
```

---

## reverse-words-in-a-string-iii

```golang
func reverseWords(s string) string {
    words := strings.Split(s, " ")
    for i, word := range words {
        words[i] = reverseString(word)
    }
    return strings.Join(words, " ")
}

func reverseString(s string) string {
    runes := []rune(s)
    left, right := 0, len(runes)-1
    for left < right {
        runes[left], runes[right] = runes[right], runes[left]
        left++
        right--
    }
    return string(runes)
}

```

---

## rising-temperature

```mysql
# Write your MySQL query statement below

select w1.id
from Weather w1
join Weather w2 on w1.recordDate = date_add(w2.recordDate, interval 1 day)
where w1.temperature > w2.temperature;
```

---

## robot-return-to-origin

```golang
func judgeCircle(moves string) bool {
    x, y := 0, 0
    for _, move := range moves {
        switch move {
            case 'U':
                y++
            case 'D':
                y--
            case 'L':
                x--
            case 'R':
                x++
        }
    }
    return x == 0 && y == 0
}
```

---

## roman-to-integer

```c
int romanToInt(char *s) {
    int romanValue = 0;
    int prevValue = 0;

    for (int i = 0; s[i] != '\0'; i++) {
        int currentValue = 0;

        switch (s[i]) {
            case 'I':
                currentValue = 1;
                break;
            case 'V':
                currentValue = 5;
                break;
            case 'X':
                currentValue = 10;
                break;
            case 'L':
                currentValue = 50;
                break;
            case 'C':
                currentValue = 100;
                break;
            case 'D':
                currentValue = 500;
                break;
            case 'M':
                currentValue = 1000;
                break;
        }

        romanValue += currentValue;

        if (currentValue > prevValue) {
            romanValue -= 2 * prevValue;
        }

        prevValue = currentValue;
    }

    return romanValue;
}

```

---

## rotate-array

```golang
func rotate(nums []int, k int)  {
    k %= len(nums)
    start, end := 0, len(nums)-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
    start, end = 0, k-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
    start, end = k, len(nums)-1
    for start < end {
        nums[start], nums[end] = nums[end], nums[start]
        start++
        end--
    }
}
```

---

## rotate-image

```golang
func rotate(matrix [][]int) {
    n := len(matrix)
    
    // Transpose the matrix
    for i := 0; i < n; i++ {
        for j := i; j < n; j++ {
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        }
    }
    
    // Reverse each row
    for i := 0; i < n; i++ {
        for j := 0; j < n/2; j++ {
            matrix[i][j], matrix[i][n-j-1] = matrix[i][n-j-1], matrix[i][j]
        }
    }
}

```

---

## rotate-list

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func rotateRight(head *ListNode, k int) *ListNode {
	// Check for empty list or k = 0
	if head == nil || k == 0 {
		return head
	}

	// Calculate the length of the list
	length := 1
	tail := head
	for tail.Next != nil {
		tail = tail.Next
		length++
	}

	// Calculate the actual rotation steps needed
	k = k % length
	if k == 0 {
		return head
	}

	// Find the new tail and new head
	newTail := head
	for i := 1; i < length-k; i++ {
		newTail = newTail.Next
	}
	newHead := newTail.Next

	// Perform the rotation
	newTail.Next = nil
	tail.Next = head

	return newHead
}
```

---

## rotate-string

```javascript
/**
 * @param {string} s
 * @param {string} goal
 * @return {boolean}
 */
var rotateString = function(s, goal) {
    
    for (let i = 0; i < s.length; i++) {
        s = s.split("");
        s.push(s.shift());
        s = s.join("");
        
        if (s == goal) return true;
    }

    return false;
};
```

---

## rotting-oranges

```golang
func orangesRotting(grid [][]int) int {
    // Define the directions for 4-directional adjacency
    directions := [4][2]int{{-1, 0}, {0, 1}, {1, 0}, {0, -1}}

    // Initialize a queue to store the coordinates of rotten oranges
    queue := make([][2]int, 0)

    // Initialize variables to keep track of fresh oranges and the number of minutes elapsed
    freshOranges := 0
    minutesElapsed := 0

    // Step 1: Count the number of fresh oranges and enqueue the coordinates of rotten oranges
    rows := len(grid)
    cols := len(grid[0])
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if grid[i][j] == 1 {
                freshOranges++
            } else if grid[i][j] == 2 {
                queue = append(queue, [2]int{i, j})
            }
        }
    }

    // Step 2: Simulate the rotting process using BFS
    for len(queue) > 0 && freshOranges > 0 {
        // Keep track of the size of the current level/minute
        levelSize := len(queue)

        for i := 0; i < levelSize; i++ {
            orange := queue[0]
            queue = queue[1:]

            row := orange[0]
            col := orange[1]

            // Check the 4-directionally adjacent cells
            for _, dir := range directions {
                newRow := row + dir[0]
                newCol := col + dir[1]

                // Skip if the adjacent cell is out of bounds or contains a rotten or empty orange
                if newRow < 0 || newRow >= rows || newCol < 0 || newCol >= cols || grid[newRow][newCol] != 1 {
                    continue
                }

                // Mark the adjacent fresh orange as rotten and enqueue its coordinates
                grid[newRow][newCol] = 2
                queue = append(queue, [2]int{newRow, newCol})
                freshOranges--
            }
        }

        // Increment the number of minutes elapsed
        if len(queue) > 0 {
            minutesElapsed++
        }
    }

    // Step 3: Return the result based on the remaining fresh oranges
    if freshOranges == 0 {
        return minutesElapsed
    }

    return -1
}

```

---

## sales-analysis-iii

```mysql
# Write your MySQL query statement below
SELECT s.product_id, product_name
FROM Sales s
LEFT JOIN Product p
ON s.product_id = p.product_id
GROUP BY s.product_id
HAVING MIN(sale_date) >= CAST('2019-01-01' AS DATE) AND
       MAX(sale_date) <= CAST('2019-03-31' AS DATE)
```

---

## sales-person

```pythondata
import pandas as pd

def sales_person(sales_person: pd.DataFrame, company: pd.DataFrame, orders: pd.DataFrame) -> pd.DataFrame:
    # Merge the SalesPerson and Orders tables on 'sales_id'
    merged = sales_person.merge(orders, on='sales_id', how='left')
    
    # Merge the merged DataFrame with the Company table on 'com_id'
    merged = merged.merge(company, on='com_id', how='left')
    
    # Filter the DataFrame to include only rows where company name is 'RED'
    red_orders = merged[merged['name_y'] == 'RED']
    
    # Find the salespersons who have orders related to company 'RED'
    salespersons_with_red_orders = red_orders['sales_id'].unique()
    
    # Filter the original SalesPerson DataFrame to exclude those with red orders
    result = sales_person[~sales_person['sales_id'].isin(salespersons_with_red_orders)]
    
    # Select and return only the 'name' column
    result = result[['name']]
    
    return result
```

---

## same-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSameTree(p *TreeNode, q *TreeNode) bool {
    // If both trees are empty, they are considered the same
    if p == nil && q == nil {
        return true
    }
    
    // If one tree is empty and the other is not, they are not the same
    if p == nil || q == nil {
        return false
    }
    
    // If the values of the current nodes are different, they are not the same
    if p.Val != q.Val {
        return false
    }
    
    // Recursively check if the left and right subtrees are the same
    return isSameTree(p.Left, q.Left) && isSameTree(p.Right, q.Right)
}
```

---

## scramble-string

```golang
func isScramble(s1 string, s2 string) bool {
    n := len(s1)
    if n != len(s2) {
        return false
    }

    // Initialize a 3D DP array to store the results
    dp := make([][][]bool, n)
    for i := range dp {
        dp[i] = make([][]bool, n)
        for j := range dp[i] {
            dp[i][j] = make([]bool, n+1)
        }
    }

    // Base case: strings of length 1
    for i := 0; i < n; i++ {
        for j := 0; j < n; j++ {
            if s1[i] == s2[j] {
                dp[i][j][1] = true
            }
        }
    }

    // Length of the substring to check
    for len := 2; len <= n; len++ {
        for i := 0; i <= n-len; i++ {
            for j := 0; j <= n-len; j++ {
                for k := 1; k < len; k++ {
                    // Check for unswapped and swapped substrings
                    if (dp[i][j][k] && dp[i+k][j+k][len-k]) || (dp[i][j+len-k][k] && dp[i+k][j][len-k]) {
                        dp[i][j][len] = true
                        break
                    }
                }
            }
        }
    }

    return dp[0][0][n]
}

```

---

## search-a-2d-matrix

```javascript
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
  if (matrix.length === 0 || matrix[0].length === 0) {
    return false;
  }
  
  const rows = matrix.length;
  const columns = matrix[0].length;
  let left = 0;
  let right = rows * columns - 1;
  
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    const midValue = matrix[Math.floor(mid / columns)][mid % columns];
    
    if (midValue === target) {
      return true;
    } else if (midValue < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  
  return false;
};
```

---

## search-a-2d-matrix-ii

```golang
func searchMatrix(matrix [][]int, target int) bool {
    if len(matrix) == 0 || len(matrix[0]) == 0 {
        return false
    }

    m, n := len(matrix), len(matrix[0])
    row, col := 0, n-1

    for row < m && col >= 0 {
        if matrix[row][col] == target {
            return true
        } else if matrix[row][col] > target {
            col--
        } else {
            row++
        }
    }

    return false
}
```

---

## search-in-a-binary-search-tree

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */
var searchBST = function(root, val) {
    if (root === null ||  root.val === val) {
        return root;
    }
    if (val < root.val)  {
        return searchBST(root.left, val);
    } else {
        return searchBST(root.right, val);
    }
};
```

---

## search-in-rotated-sorted-array

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (nums[mid] === target) {
      return mid;
    }

    if (nums[left] <= nums[mid]) {
      // Left side is sorted in ascending order
      if (nums[left] <= target && target < nums[mid]) {
        // Target is within the sorted left side
        right = mid - 1;
      } else {
        // Target is on the right side
        left = mid + 1;
      }
    } else {
      // Right side is sorted in ascending order
      if (nums[mid] < target && target <= nums[right]) {
        // Target is within the sorted right side
        left = mid + 1;
      } else {
        // Target is on the left side
        right = mid - 1;
      }
    }
  }

  // Target element not found
  return -1;
};
```

---

## search-in-rotated-sorted-array-ii

```golang
func search(nums []int, target int) bool {
    left, right := 0, len(nums)-1

    for left <= right {
        mid := left + (right-left)/2

        if nums[mid] == target {
            return true
        }

        // Handle duplicates by moving the left or right pointer
        for left < mid && nums[left] == nums[mid] {
            left++
        }

        for mid < right && nums[mid] == nums[right] {
            right--
        }

        if nums[left] <= nums[mid] {
            // Left half is sorted
            if nums[left] <= target && target < nums[mid] {
                right = mid - 1
            } else {
                left = mid + 1
            }
        } else {
            // Right half is sorted
            if nums[mid] < target && target <= nums[right] {
                left = mid + 1
            } else {
                right = mid - 1
            }
        }
    }

    return false
}

```

---

## search-insert-position

```c
int searchInsert(int* nums, int numsSize, int target) {
    int left = 0;
    int right = numsSize - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return left; // If the loop exits, the target was not found, so return the left index.
}
```

---

## search-suggestions-system

```golang
func suggestedProducts(products []string, searchWord string) [][]string {
	// Sort the products lexicographically
	sort.Strings(products)
	
	result := make([][]string, len(searchWord))
	prefix := ""

	for i, char := range searchWord {
		prefix += string(char)

		// Binary search for the index of the first product with a prefix >= prefix
		index := sort.SearchStrings(products, prefix)

		// Collect up to three suggested products with the common prefix
		for j := index; j < len(products) && j < index+3; j++ {
			if !startsWith(products[j], prefix) {
				break
			}
			result[i] = append(result[i], products[j])
		}
	}

	return result
}

// Helper function to check if a string starts with a given prefix
func startsWith(s, prefix string) bool {
	if len(s) < len(prefix) {
		return false
	}
	for i := 0; i < len(prefix); i++ {
		if s[i] != prefix[i] {
			return false
		}
	}
	return true
}
```

---

## seat-reservation-manager

```golang
type SeatManager struct {
    availableSeats *PriorityQueue
}

func Constructor(n int) SeatManager {
    pq := &PriorityQueue{}
    heap.Init(pq)

    for i := 1; i <= n; i++ {
        heap.Push(pq, i)
    }

    return SeatManager{pq}
}

func (this *SeatManager) Reserve() int {
    if this.availableSeats.Len() > 0 {
        return heap.Pop(this.availableSeats).(int)
    }
    return -1 // Or handle the case when all seats are reserved
}

func (this *SeatManager) Unreserve(seatNumber int) {
    heap.Push(this.availableSeats, seatNumber)
}

// PriorityQueue for managing available seats
type PriorityQueue []int

func (pq PriorityQueue) Len() int { return len(pq) }

func (pq PriorityQueue) Less(i, j int) bool { return pq[i] < pq[j] }

func (pq PriorityQueue) Swap(i, j int) { pq[i], pq[j] = pq[j], pq[i] }

func (pq *PriorityQueue) Push(x interface{}) {
    item := x.(int)
    *pq = append(*pq, item)
}

func (pq *PriorityQueue) Pop() interface{} {
    old := *pq
    n := len(old)
    item := old[n-1]
    *pq = old[0 : n-1]
    return item
}

/**
 * Your SeatManager object will be instantiated and called as such:
 * obj := Constructor(n);
 * param_1 := obj.Reserve();
 * obj.Unreserve(seatNumber);
 */
```

---

## second-highest-salary

```mysql
# Write your MySQL query statement below

SELECT
    MAX(salary) AS SecondHighestSalary
FROM
    Employee
WHERE
    salary < (SELECT MAX(salary) FROM Employee)
```

---

## second-minimum-node-in-a-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findSecondMinimumValue(root *TreeNode) int {
    min1 := root.Val
    min2 := math.MaxInt64

    dfs(root, min1, &min2)

    if min2 == math.MaxInt64 {
        return -1
    }

    return min2
}

func dfs(node *TreeNode, min1 int, min2 *int) {
    if node == nil {
        return
    }

    if node.Val > min1 && node.Val <= *min2 {
        *min2 = node.Val
    }

    dfs(node.Left, min1, min2)
    dfs(node.Right, min1, min2)
}

```

---

## self-dividing-numbers

```golang
func selfDividingNumbers(left int, right int) []int {
    var result []int
    for num := left; num <= right; num++ {
        if isSelfDividing(num) {
            result = append(result, num)
        }
    }
    return result
}

func isSelfDividing(num int) bool {
    n := num
    for n > 0 {
        digit := n % 10
        if digit == 0 || num%digit != 0 {
            return false
        }
        n /= 10
    }
    return true
}

```

---

## set-matrix-zeroes

```golang
func setZeroes(matrix [][]int) {
    m := len(matrix)
    n := len(matrix[0])

    firstRowZero := false
    firstColZero := false

    // Check if first row contains zero
    for j := 0; j < n; j++ {
        if matrix[0][j] == 0 {
            firstRowZero = true
            break
        }
    }

    // Check if first column contains zero
    for i := 0; i < m; i++ {
        if matrix[i][0] == 0 {
            firstColZero = true
            break
        }
    }

    // Mark zeros in the rest of the matrix
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            if matrix[i][j] == 0 {
                matrix[0][j] = 0
                matrix[i][0] = 0
            }
        }
    }

    // Set zeros based on marked rows and columns
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            if matrix[0][j] == 0 || matrix[i][0] == 0 {
                matrix[i][j] = 0
            }
        }
    }

    // Set zeros in the first row if necessary
    if firstRowZero {
        for j := 0; j < n; j++ {
            matrix[0][j] = 0
        }
    }

    // Set zeros in the first column if necessary
    if firstColZero {
        for i := 0; i < m; i++ {
            matrix[i][0] = 0
        }
    }
}

```

---

## set-mismatch

```golang
func findErrorNums(nums []int) []int {
    n := len(nums)
    numSet := make(map[int]bool)

    duplicate := -1
    for _, num := range nums {
        if numSet[num] {
            duplicate = num
        }
        numSet[num] = true
    }

    missing := -1
    for i := 1; i <= n; i++ {
        if !numSet[i] {
            missing = i
            break
        }
    }

    return []int{duplicate, missing}
}

```

---

## shift-2d-grid

```javascript
/**
 * @param {number[][]} grid
 * @param {number} k
 * @return {number[][]}
 */
var shiftGrid = function(grid, k) {
    let m = grid[0].length;
    grid = grid.join().split(",");
    for (let i = 0; i < k; i++) {
        grid.unshift(grid.pop());
    }
    for (let i = 0; i < grid.length; i += m) {
        grid[i] = grid.slice(i, i+m);
    }
    return grid.filter(e => Array.isArray(e));
};
```

---

## shortest-completing-word

```golang
func shortestCompletingWord(licensePlate string, words []string) string {
	licensePlate = normalizeLicensePlate(licensePlate)
	letterFreq := getLetterFrequency(licensePlate)

	shortestWord := ""
	for _, word := range words {
		if isCompletingWord(word, letterFreq) {
			if shortestWord == "" || len(word) < len(shortestWord) {
				shortestWord = word
			}
		}
	}

	return shortestWord
}

func normalizeLicensePlate(licensePlate string) string {
	licensePlate = strings.ToLower(licensePlate)
	normalized := ""
	for _, ch := range licensePlate {
		if ch >= 'a' && ch <= 'z' {
			normalized += string(ch)
		}
	}
	return normalized
}

func getLetterFrequency(str string) map[rune]int {
	freq := make(map[rune]int)
	for _, ch := range str {
		freq[ch]++
	}
	return freq
}

func isCompletingWord(word string, letterFreq map[rune]int) bool {
	wordFreq := getLetterFrequency(word)

	for ch, count := range letterFreq {
		if wordFreq[ch] < count {
			return false
		}
	}

	return true
}

```

---

## shortest-distance-to-a-character

```golang
func shortestToChar(s string, c byte) []int {
    n := len(s)
    
    // Initialize an array to store the distances
    distances := make([]int, n)
    
    // Initialize variables to keep track of the leftmost and rightmost occurrences of 'c'
    leftmost := -n
    rightmost := 2 * n
    
    // Iterate through the string from left to right
    for i := 0; i < n; i++ {
        if s[i] == c {
            leftmost = i
        }
        distances[i] = i - leftmost
    }
    
    // Iterate through the string from right to left
    for i := n - 1; i >= 0; i-- {
        if s[i] == c {
            rightmost = i
        }
        distances[i] = min(distances[i], rightmost - i)
    }
    
    return distances
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## shortest-palindrome

```golang
func shortestPalindrome(s string) string {
    n := len(s)
    
    // Helper function to check if a string is a palindrome.
    isPalindrome := func(str string) bool {
        i, j := 0, len(str)-1
        for i < j {
            if str[i] != str[j] {
                return false
            }
            i++
            j--
        }
        return true
    }
    
    // Find the longest palindrome prefix.
    i := n - 1
    for i >= 0 && !isPalindrome(s[:i+1]) {
        i--
    }
    
    // Reverse the suffix and concatenate it to the original string.
    suffix := ""
    for j := n - 1; j > i; j-- {
        suffix += string(s[j])
    }
    
    return suffix + s
}

```

---

## simplify-path

```golang
func simplifyPath(path string) string {
    dirs := strings.Split(path, "/")
    stack := make([]string, 0, len(dirs))
    
    for _, dir := range dirs {
        if dir == "." || dir == "" {
            continue
        }
        if dir == ".." {
            if len(stack) > 0 {
                stack = stack[:len(stack)-1]
            }
        } else {
            stack = append(stack, dir)
        }
    }
    
    if len(stack) == 0 {
        return "/"
    }
    
    return "/" + strings.Join(stack, "/")
}
```

---

## single-number

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = (nums) => nums.reduce((acc, e) => acc ^ e);
```

---

## single-number-ii

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    //return nums.reduce((acc, curr) => acc ^= curr)
    nums.sort((a,b) => b-a);

    for (let i = 0; i < nums.length; i+=3) {
        if (nums[i] == nums[i+1]) {
            continue;
        } else {
            return nums[i]
        }
    }
    
};

/*
nums = 0,100,0,99,100,0,100
nums.sort(); // nums = 0,0,0,99,100,100,100

nums[i] == nums[i+1] {
    continue;
} else {
    return nums[i]
}


*/
```

---

## sleep

```javascript
/**
 * @param {number} millis
 */
async function sleep(millis) {
    return new Promise(resolve => {
        setTimeout(resolve, millis)
    })
}

/** 
 * let t = Date.now()
 * sleep(100).then(() => console.log(Date.now() - t)) // 100
 */
```

---

## sliding-window-maximum

```typescript
function maxSlidingWindow(nums: number[], k: number): number[] {
    const result: number[] = [];
    const deque: number[] = [];

    for (let i = 0; i < nums.length; i++) {
        // Remove elements from the front of the deque that are outside the current window
        if (deque.length > 0 && deque[0] <= i - k) {
        deque.shift();
        }

        // Remove elements from the back of the deque that are smaller than the current element
        while (deque.length > 0 && nums[deque[deque.length - 1]] < nums[i]) {
        deque.pop();
        }

        deque.push(i);

        // Add the maximum element to the result when the window size is reached
        if (i >= k - 1) {
        result.push(nums[deque[0]]);
        }
    }

    return result;
}

```

---

## smallest-number-in-infinite-set

```javascript
var SmallestInfiniteSet = function() {
    this.heap = [];
    this.min = 1;
};

/**
 * @return {number}
 */
SmallestInfiniteSet.prototype.popSmallest = function() {
    if (this.heap.length > 0) {
        return this.heap.shift();
    }
    this.min++;
    return this.min - 1;
};

/** 
 * @param {number} num
 * @return {void}
 */
SmallestInfiniteSet.prototype.addBack = function(num) {
    if (
        this.min > num &&
        this.heap.indexOf(num) === - 1
    ) {
        this.heap.push(num);
        this.heap.sort((a,b) => a-b);
    }
};

/** 
 * Your SmallestInfiniteSet object will be instantiated and called as such:
 * var obj = new SmallestInfiniteSet()
 * var param_1 = obj.popSmallest()
 * obj.addBack(num)
 */
```

---

## smallest-range-i

```golang
func smallestRangeI(nums []int, k int) int {
    minVal := min(nums...)
    maxVal := max(nums...)
    
    // Calculate the minimum possible score by adjusting the min and max values
    minScore := maxVal - k - (minVal + k)
    
    // Ensure the score is non-negative
    if minScore < 0 {
        return 0
    }
    
    return minScore
}

func min(nums ...int) int {
    minVal := nums[0]
    for _, num := range nums {
        if num < minVal {
            minVal = num
        }
    }
    return minVal
}

func max(nums ...int) int {
    maxVal := nums[0]
    for _, num := range nums {
        if num > maxVal {
            maxVal = num
        }
    }
    return maxVal
}

```

---

## smallest-sufficient-team

```javascript
/**
 * @param {string[]} req_skills
 * @param {string[][]} people
 * @return {number[]}
 */
var smallestSufficientTeam = function(req_skills, people) {
  const n = req_skills.length;
  const skillMap = new Map();
  
  // Map skills to their corresponding bitmask value
  for (let i = 0; i < n; i++) {
    skillMap.set(req_skills[i], i);
  }
  
  const dp = new Array(1 << n).fill(Infinity); // Minimum team size for each bitmask
  dp[0] = 0; // Base case: no skills required
  
  const team = new Array(1 << n).fill([]);
  
  // Iterate over each person and update the dp array
  for (let i = 0; i < people.length; i++) {
    const personSkills = people[i];
    let bitmask = 0; // Bitmask representing skills possessed by the person
    
    // Calculate the bitmask for the person's skills
    for (let j = 0; j < personSkills.length; j++) {
      const skill = personSkills[j];
      if (skillMap.has(skill)) {
        const skillIndex = skillMap.get(skill);
        bitmask |= (1 << skillIndex); // Set the bit representing the skill
      }
    }
    
    // Update the dp array based on the current person
    for (let prevBitmask = 0; prevBitmask < (1 << n); prevBitmask++) {
      if (dp[prevBitmask] + 1 < dp[prevBitmask | bitmask]) {
        dp[prevBitmask | bitmask] = dp[prevBitmask] + 1;
        team[prevBitmask | bitmask] = [...team[prevBitmask], i];
      }
    }
  }
  
  return team[(1 << n) - 1]; // Return the team for the bitmask representing all required skills
};

```

---

## snakes-and-ladders

```javascript
/**
 * @param {number[][]} board
 * @return {number}
 */
var snakesAndLadders = function(board) {
  const n = board.length;
  const target = n * n;
  const visited = new Array(n * n + 1).fill(false); // Mark cells as visited
  
  // Create a queue for BFS
  const queue = [];
  queue.push(1); // Start at square 1
  visited[1] = true; // Mark square 1 as visited
  
  let moves = 0;
  
  // Perform BFS
  while (queue.length > 0) {
    const size = queue.length;
    
    // Process all cells at the current level
    for (let i = 0; i < size; i++) {
      const curr = queue.shift();
      
      // Check if we have reached the target square
      if (curr === target) {
        return moves;
      }
      
      // Roll the die and explore all possible destinations
      for (let j = 1; j <= 6 && curr + j <= target; j++) {
        const next = curr + j;
        const [row, col] = getCoordinates(next, n);
        
        // Check if the next square has a snake or ladder
        const dest = board[row][col] === -1 ? next : board[row][col];
        
        // If the destination has not been visited, add it to the queue
        if (!visited[dest]) {
          visited[dest] = true;
          queue.push(dest);
        }
      }
    }
    
    moves++; // Increment the number of moves after processing all cells at the current level
  }
  
  return -1; // Target square cannot be reached
};

// Helper function to convert a square number to coordinates
function getCoordinates(square, n) {
  const row = Math.floor((square - 1) / n);
  const col = (square - 1) % n;
  
  // Adjust coordinates for Boustrophedon style
  if (row % 2 === 1) {
    return [n - 1 - row, n - 1 - col];
  }
  
  return [n - 1 - row, col];
}
```

---

## sort-array-by-parity

```golang
func sortArrayByParity(nums []int) []int {
    left, right := 0, len(nums) - 1

    for left < right {
        if nums[left]%2 == 1 && nums[right]%2 == 0 {
            nums[left], nums[right] = nums[right], nums[left]
        }

        if nums[left]%2 == 0 {
            left++
        }

        if nums[right]%2 == 1 {
            right--
        }
    }

    return nums
}
```

---

## sort-array-by-parity-ii

```golang
func sortArrayByParityII(nums []int) []int {
    evenIdx := 0
    oddIdx := 1
    result := make([]int, len(nums))
    for _, num := range nums {
        if num%2 == 0 {
            result[evenIdx] = num
            evenIdx += 2
        } else {
            result[oddIdx] = num
            oddIdx += 2
        }
    }
    return result
}
```

---

## sort-by

```javascript
/**
 * @param {Array} arr
 * @param {Function} fn
 * @return {Array}
 */
var sortBy = function(arr, fn) {
    if (arr.length <= 1) {
        return arr;
    }

    var mid = Math.floor(arr.length / 2);
    var left = arr.slice(0, mid);
    var right = arr.slice(mid);

    return merge(sortBy(left, fn), sortBy(right, fn), fn);
    };

function merge(left, right, fn) {
    var sorted = [];
    var leftIndex = 0;
    var rightIndex = 0;

    while (leftIndex < left.length && rightIndex < right.length) {
        if (fn(left[leftIndex]) <= fn(right[rightIndex])) {
        sorted.push(left[leftIndex]);
        leftIndex++;
        } else {
        sorted.push(right[rightIndex]);
        rightIndex++;
        }
    }

    while (leftIndex < left.length) {
        sorted.push(left[leftIndex]);
        leftIndex++;
    }

    while (rightIndex < right.length) {
        sorted.push(right[rightIndex]);
        rightIndex++;
    }

    return sorted;
};
```

---

## sort-colors

```javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let low = 0;          // pointer for 0
    let mid = 0;          // pointer for 1
    let high = nums.length - 1;  // pointer for 2

    while (mid <= high) {
        if (nums[mid] === 0) {
        // Swap the current element with the element at the low pointer
        [nums[mid], nums[low]] = [nums[low], nums[mid]];
        low++;
        mid++;
        } else if (nums[mid] === 1) {
        // Move to the next element
        mid++;
        } else if (nums[mid] === 2) {
        // Swap the current element with the element at the high pointer
        [nums[mid], nums[high]] = [nums[high], nums[mid]];
        high--;
        }
    }
};
```

---

## sort-integers-by-the-number-of-1-bits

```javascript
/**
 * @param {number[]} arr
 * @return {number[]}
 */
var sortByBits = function(arr) {
    return arr.sort((a,b) => a-b).sort((a, b) => a.toString(2).replaceAll("0", "").length - b.toString(2).replaceAll("0", "").length)
};
```

---

## sort-list

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
function mergeSort(head) {
  // Base case: empty list or single node
  if (!head || !head.next) {
    return head;
  }

  // Split the list into two halves
  let mid = findMiddle(head);
  let left = head;
  let right = mid.next;
  mid.next = null;

  // Recursively sort the two halves
  let sortedLeft = mergeSort(left);
  let sortedRight = mergeSort(right);

  // Merge the sorted halves
  return merge(sortedLeft, sortedRight);
}

function findMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow;
}

function merge(left, right) {
  let dummy = new ListNode(0);
  let curr = dummy;

  while (left && right) {
    if (left.val < right.val) {
      curr.next = left;
      left = left.next;
    } else {
      curr.next = right;
      right = right.next;
    }
    curr = curr.next;
  }

  if (left) {
    curr.next = left;
  } else if (right) {
    curr.next = right;
  }

  return dummy.next;
}

var sortList = function(head) {
  return mergeSort(head);
};
```

---

## sort-the-people

```javascript
/**
 * @param {string[]} names
 * @param {number[]} heights
 * @return {string[]}
 */
var sortPeople = function(names, heights) {
    let heightEntries = {};
    heights.forEach((value, index) => {
        heightEntries[value] = index;
    })
    let sortedHeights = heights.sort((a,b)=>b-a)
    let sortedPeople = [];

    sortedHeights.forEach((val) => {
        sortedPeople.push(names[heightEntries[val]])
    })

    return sortedPeople
};
```

---

## sort-vowels-in-a-string

```golang
func isVowel(c byte) bool {
	vowels := "aeiouAEIOU"
	return strings.ContainsRune(vowels, rune(c))
}

func sortVowels(s string) string {
	vowelIndices := make([]int, 0)
	vowels := make([]byte, 0)

	// Find vowel indices and collect vowels
	for i := 0; i < len(s); i++ {
		if isVowel(s[i]) {
			vowelIndices = append(vowelIndices, i)
			vowels = append(vowels, s[i])
		}
	}

	// Sort vowels
	sort.Slice(vowels, func(i, j int) bool {
		return vowels[i] < vowels[j]
	})

	// Reconstruct the final string
	result := make([]byte, len(s))
	copy(result, []byte(s))

	for i := 0; i < len(vowels); i++ {
		result[vowelIndices[i]] = vowels[i]
	}

	return string(result)
}

```

---

## spiral-matrix

```golang
func spiralOrder(matrix [][]int) []int {
    if len(matrix) == 0 {
        return []int{}
    }
    
    var result []int
    rowStart, rowEnd := 0, len(matrix)-1
    colStart, colEnd := 0, len(matrix[0])-1
    
    for rowStart <= rowEnd && colStart <= colEnd {
        // Traverse right
        for j := colStart; j <= colEnd; j++ {
            result = append(result, matrix[rowStart][j])
        }
        rowStart++
        
        // Traverse down
        for i := rowStart; i <= rowEnd; i++ {
            result = append(result, matrix[i][colEnd])
        }
        colEnd--
        
        // Traverse left
        if rowStart <= rowEnd {
            for j := colEnd; j >= colStart; j-- {
                result = append(result, matrix[rowEnd][j])
            }
            rowEnd--
        }
        
        // Traverse up
        if colStart <= colEnd {
            for i := rowEnd; i >= rowStart; i-- {
                result = append(result, matrix[i][colStart])
            }
            colStart++
        }
    }
    
    return result
}

```

---

## spiral-matrix-ii

```golang
func generateMatrix(n int) [][]int {
    // Initialize the result matrix with all zeros.
    matrix := make([][]int, n)
    for i := 0; i < n; i++ {
        matrix[i] = make([]int, n)
    }

    num := 1
    top, bottom, left, right := 0, n-1, 0, n-1

    for num <= n*n {
        // Fill the top row.
        for i := left; i <= right; i++ {
            matrix[top][i] = num
            num++
        }
        top++

        // Fill the rightmost column.
        for i := top; i <= bottom; i++ {
            matrix[i][right] = num
            num++
        }
        right--

        // Fill the bottom row.
        for i := right; i >= left; i-- {
            matrix[bottom][i] = num
            num++
        }
        bottom--

        // Fill the leftmost column.
        for i := bottom; i >= top; i-- {
            matrix[i][left] = num
            num++
        }
        left++
    }

    return matrix
}

```

---

## sqrtx

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    if (x < 2) return x;

    let left = 1;
    let right = x;

    while (left <= right) {
        const mid = (left + right) >>> 1;
        if (mid * mid === x) return mid;
        else if (mid * mid < x) left = mid + 1;
        else right = mid - 1;
    }

    return ~~right;
};
```

---

## squares-of-a-sorted-array

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortedSquares = function(nums) {
    for (let i = 0; i < nums.length; i++) {
        nums[i] = nums[i] ** 2
    }
    return nums.sort((a, b) => a-b)
};
```

---

## strictly-palindromic-number

```javascript
/**
 * @param {number} n
 * @return {boolean}
 */
var isStrictlyPalindromic = function(n) {
    return false
};
```

---

## string-compression

```typescript
function compress(chars: string[]): number {
  let writeIdx = 0; // Index to write compressed characters
  let count = 1; // Count of consecutive repeating characters

  for (let i = 0; i < chars.length; i++) {
    if (i + 1 === chars.length || chars[i] !== chars[i + 1]) {
      // Current character is different from the next one or it's the last character
      chars[writeIdx] = chars[i]; // Write the character at the current write index

      if (count > 1) {
        // There is a group of repeating characters
        const countChars = count.toString().split(''); // Split the count into individual digits

        for (const char of countChars) {
          chars[++writeIdx] = char; // Write each digit of the count
        }
      }

      writeIdx++; // Move the write index forward
      count = 1; // Reset the count for the next group
    } else {
      // Current character is the same as the next one
      count++; // Increment the count
    }
  }

  return writeIdx;
}

```

---

## string-to-integer-atoi

```golang
func myAtoi(s string) int {
    // Step 1: Ignore leading whitespace
    i := 0
    for i < len(s) && s[i] == ' ' {
        i++
    }
    
    // Step 2: Check if the number is negative or positive
    sign := 1
    if i < len(s) && (s[i] == '-' || s[i] == '+') {
        if s[i] == '-' {
            sign = -1
        }
        i++
    }
    
    // Step 3: Read in the digits
    num := 0
    for i < len(s) && isDigit(s[i]) {
        digit := int(s[i] - '0')
        // Check for overflow
        if num > (math.MaxInt32-digit)/10 {
            if sign == 1 {
                return math.MaxInt32
            } else {
                return math.MinInt32
            }
        }
        num = num*10 + digit
        i++
    }
    
    // Step 4: Apply the sign
    return num * sign
}

func isDigit(c byte) bool {
    return c >= '0' && c <= '9'
}
```

---

## student-attendance-record-i

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var checkRecord = function(s) {
  var absentCount = 0;
  var lateCount = 0;

  for (var i = 0; i < s.length; i++) {
    if (s[i] === 'A') {
      absentCount++;
      if (absentCount >= 2) {
        return false;
      }
    }

    if (s[i] === 'L') {
      lateCount++;
      if (lateCount >= 3) {
        return false;
      }
    } else {
      lateCount = 0;
    }
  }

  return true;
};

```

---

## students-and-examinations

```mysql
# Write your MySQL query statement below

select s.student_id, s.student_name, sub.subject_name, count(e.subject_name) as attended_exams
from Students s
cross join Subjects sub
left join Examinations e on s.student_id = e.student_id and sub.subject_name = e.subject_name
group by s.student_id, s.student_name, sub.subject_name
order by s.student_id, sub.subject_name;

```

---

## subarray-sum-equals-k

```typescript
function subarraySum(nums: number[], k: number): number {
    let count = 0;
    let sum = 0;
    const map = new Map<number, number>();
    map.set(0, 1);

    for (let i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (map.has(sum - k)) {
        count += map.get(sum - k)!;
        }
        if (map.has(sum)) {
        map.set(sum, map.get(sum)! + 1);
        } else {
        map.set(sum, 1);
        }
    }

    return count;
}

```

---

## subsets

```typescript
function subsets(nums: number[]): number[][] {
    const subsets: number[][] = [];
    
    backtrack([], 0);

    function backtrack(currentSubset: number[], start: number) {
        subsets.push([... currentSubset]);
        for (let i = start; i < nums.length; i++) {
            currentSubset.push(nums[i]);
            backtrack(currentSubset, i+1);
            currentSubset.pop()
        }
    }

    return subsets;
};


```

---

## subsets-ii

```golang
func subsetsWithDup(nums []int) [][]int {
    // Sort the input array to handle duplicates
    sort.Ints(nums)

    subsets := make([][]int, 0)
    subset := make([]int, 0)

    var backtrack func(start int)
    backtrack = func(start int) {
        subsetCopy := make([]int, len(subset))
        copy(subsetCopy, subset)
        subsets = append(subsets, subsetCopy)

        for i := start; i < len(nums); i++ {
            // Skip duplicates
            if i > start && nums[i] == nums[i-1] {
                continue
            }

            subset = append(subset, nums[i])
            backtrack(i + 1)
            subset = subset[:len(subset)-1]
        }
    }

    backtrack(0)
    return subsets
}

```

---

## substring-with-concatenation-of-all-words

```javascript
/**
 * @param {string} s
 * @param {string[]} words
 * @return {number[]}
 */
function findSubstring(s, words) {
  const result = [];
  if (s.length === 0 || words.length === 0) {
    return result;
  }
  
  const wordLength = words[0].length;
  const wordCount = words.length;
  const totalLength = wordLength * wordCount;
  
  const wordMap = {};
  for (const word of words) {
    if (wordMap[word]) {
      wordMap[word]++;
    } else {
      wordMap[word] = 1;
    }
  }
  
  for (let i = 0; i <= s.length - totalLength; i++) {
    const substring = s.substr(i, totalLength);
    const substringMap = {};
    
    for (let j = 0; j < totalLength; j += wordLength) {
      const word = substring.substr(j, wordLength);
      if (wordMap[word]) {
        if (substringMap[word]) {
          substringMap[word]++;
        } else {
          substringMap[word] = 1;
        }
        
        if (substringMap[word] > wordMap[word]) {
          break;
        }
      } else {
        break;
      }
    }
    
    if (compareMaps(wordMap, substringMap)) {
      result.push(i);
    }
  }
  
  return result;
}

function compareMaps(map1, map2) {
  for (const key in map1) {
    if (map1[key] !== map2[key]) {
      return false;
    }
  }
  
  return true;
}

```

---

## subtree-of-another-tree

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} subRoot
 * @return {boolean}
 */
var isSubtree = function(s, t) {
  // Helper function to check if two trees are identical
  function isIdentical(tree1, tree2) {
    if (tree1 === null && tree2 === null) {
      return true;
    }
    if (tree1 === null || tree2 === null) {
      return false;
    }
    return (
      tree1.val === tree2.val &&
      isIdentical(tree1.left, tree2.left) &&
      isIdentical(tree1.right, tree2.right)
    );
  }

  // Base case: If the main tree is null, return false
  if (s === null) {
    return false;
  }

  // Check if the current subtree is identical to the given subtree
  if (isIdentical(s, t)) {
    return true;
  }

  // Recursively check if the subtree exists in the left or right child of the main tree
  return isSubtree(s.left, t) || isSubtree(s.right, t);
};
```

---

## successful-pairs-of-spells-and-potions

```golang
func successfulPairs(spells []int, potions []int, success int64) []int {
	sort.Ints(potions)
	answer := make([]int, 0)
	m := len(potions)
	maxPotion := potions[m-1]

	for _, spell := range spells {
		minPotion := int(math.Ceil(float64(success) / float64(spell)))
		if minPotion > maxPotion {
			answer = append(answer, 0)
			continue
		}
		index := lowerBound(potions, minPotion)
		answer = append(answer, m-index)
	}

	return answer
}

func lowerBound(arr []int, key int) int {
	low := 0
	high := len(arr)
	for low < high {
		mid := (low + high) / 2
		if arr[mid] < key {
			low = mid + 1
		} else {
			high = mid
		}
	}
	return low
}
```

---

## sudoku-solver

```golang
func solveSudoku(board [][]byte) {
    solve(board, 0, 0)
}

func solve(board [][]byte, row, col int) bool {
    if row == 9 {
        return true
    }
    if col == 9 {
        return solve(board, row+1, 0)
    }
    if board[row][col] != '.' {
        return solve(board, row, col+1)
    }
    for num := '1'; num <= '9'; num++ {
        if isValid(board, row, col, byte(num)) {
            board[row][col] = byte(num)
            if solve(board, row, col+1) {
                return true
            }
            board[row][col] = '.'
        }
    }
    return false
}

func isValid(board [][]byte, row, col int, c byte) bool {
    for i := 0; i < 9; i++ {
        if board[row][i] == c || board[i][col] == c || board[3*(row/3)+i/3][3*(col/3)+i%3] == c {
            return false
        }
    }
    return true
}
```

---

## sum-of-left-leaves

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumOfLeftLeaves(root *TreeNode) int {
	if root == nil {
		return 0
	}

	sum := 0

	// Check if the left child is a left leaf
	if root.Left != nil && root.Left.Left == nil && root.Left.Right == nil {
		sum += root.Left.Val
	}

	// Recursively calculate the sum of left leaves in the left and right subtrees
	sum += sumOfLeftLeaves(root.Left)
	sum += sumOfLeftLeaves(root.Right)

	return sum
}

/*
In this implementation, the sumOfLeftLeaves function takes the root of a binary tree and calculates the sum of all left leaves in the tree.

We start with a base case where if the root is nil, we return 0. Then, we initialize a variable sum to 0.

To calculate the sum of left leaves, we check if the left child of the current node is a left leaf. We can determine this by checking if the left child exists (root.Left != nil) and if it has no children (root.Left.Left == nil && root.Left.Right == nil). If it satisfies both conditions, we add the value of the left child to the sum.

Next, we recursively call sumOfLeftLeaves on the left and right subtrees to calculate the sum of left leaves in those subtrees. We add the returned values to the sum.

Finally, we return the sum as the result.
*/
```

---

## sum-of-root-to-leaf-binary-numbers

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumRootToLeaf(root *TreeNode) int {
    return sumRootToLeafHelper(root, 0)
}

func sumRootToLeafHelper(node *TreeNode, currentSum int) int {
    if node == nil {
        return 0
    }

    // Update the current binary number by left-shifting and adding the current node's value.
    currentSum = (currentSum << 1) + node.Val

    // If it's a leaf node, return the binary number.
    if node.Left == nil && node.Right == nil {
        return currentSum
    }

    // Recursively compute the sum for left and right subtrees.
    leftSum := sumRootToLeafHelper(node.Left, currentSum)
    rightSum := sumRootToLeafHelper(node.Right, currentSum)

    return leftSum + rightSum
}
```

---

## sum-root-to-leaf-numbers

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sumNumbers(root *TreeNode) int {
	if root == nil {
		return 0
	}
	return calculatePathSum(root, 0)
}

func calculatePathSum(node *TreeNode, currentSum int) int {
	if node == nil {
		return 0
	}

	currentSum = currentSum*10 + node.Val

	if node.Left == nil && node.Right == nil {
		return currentSum
	}

	return calculatePathSum(node.Left, currentSum) + calculatePathSum(node.Right, currentSum)
}
```

---

## summary-ranges

```golang
func summaryRanges(nums []int) []string {
	result := []string{}
	n := len(nums)
	if n == 0 {
		return result
	}

	start := nums[0]
	for i := 0; i < n; i++ {
		if i+1 < n && nums[i+1]-nums[i] == 1 {
			continue
		}

		if start == nums[i] {
			result = append(result, strconv.Itoa(start))
		} else {
			result = append(result, fmt.Sprintf("%d->%d", start, nums[i]))
		}

		if i+1 < n {
			start = nums[i+1]
		}
	}

	return result
}
```

---

## surface-area-of-3d-shapes

```golang
func surfaceArea(grid [][]int) int {
    n := len(grid)
    surface := 0

    for i := 0; i < n; i++ {
        for j := 0; j < n; j++ {
            if grid[i][j] > 0 {
                surface += (grid[i][j] * 4) + 2
                if i > 0 {
                    surface -= min(grid[i][j], grid[i - 1][j]) * 2;
                }
                if j > 0 {
                    surface -= min(grid[i][j], grid[i][j - 1]) * 2;
                }
            }
        }
    }

    return surface
}

func min(a int, b int) int {
    if a < b {
        return a
    }
    return b
}
```

---

## surrounded-regions

```golang
func solve(board [][]byte) {
    if len(board) == 0 {
        return
    }

    rows, cols := len(board), len(board[0])

    // Helper function to mark safe cells
    var markSafe func(row, col int)
    markSafe = func(row, col int) {
        if row < 0 || row >= rows || col < 0 || col >= cols || board[row][col] != 'O' {
            return
        }
        board[row][col] = 'S'
        markSafe(row-1, col) // Up
        markSafe(row+1, col) // Down
        markSafe(row, col-1) // Left
        markSafe(row, col+1) // Right
    }

    // Mark safe cells starting from the border
    for row := 0; row < rows; row++ {
        markSafe(row, 0)         // Left border
        markSafe(row, cols-1)    // Right border
    }
    for col := 1; col < cols-1; col++ {
        markSafe(0, col)         // Top border
        markSafe(rows-1, col)    // Bottom border
    }

    // Flip 'O' to 'X' and restore 'S' to 'O'
    for row := 0; row < rows; row++ {
        for col := 0; col < cols; col++ {
            if board[row][col] == 'O' {
                board[row][col] = 'X'
            } else if board[row][col] == 'S' {
                board[row][col] = 'O'
            }
        }
    }
}
```

---

## swap-nodes-in-pairs

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func swapPairs(head *ListNode) *ListNode {
	// If the list has fewer than two nodes or is empty, return the head
	if head == nil || head.Next == nil {
		return head
	}

	// Create a dummy node to serve as the new head
	dummy := &ListNode{Val: 0, Next: head.Next}
	prev := dummy

	// Swap nodes in pairs
	for head != nil && head.Next != nil {
		// Nodes to be swapped
		node1 := head
		node2 := head.Next

		// Swap nodes
		prev.Next = node2
		node1.Next = node2.Next
		node2.Next = node1

		// Move pointers forward
		prev = node1
		head = node1.Next
	}

	return dummy.Next
}
```

---

## swap-salary

```mysql
# Write your MySQL query statement below
UPDATE Salary
SET sex = CASE
    WHEN sex = 'm' THEN 'f'
    WHEN sex = 'f' THEN 'm'
END;
```

---

## symmetric-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSymmetric(root *TreeNode) bool {
    // Recursive approach
    return isMirror(root, root)
    
    // Iterative approach
    // if root == nil {
    //     return true
    // }
    // queue := []*TreeNode{root.Left, root.Right}
    // for len(queue) > 0 {
    //     left := queue[0]
    //     right := queue[1]
    //     queue = queue[2:]
    //     if left == nil && right == nil {
    //         continue
    //     }
    //     if left == nil || right == nil || left.Val != right.Val {
    //         return false
    //     }
    //     queue = append(queue, left.Left, right.Right, left.Right, right.Left)
    // }
    // return true
}

func isMirror(left *TreeNode, right *TreeNode) bool {
    if left == nil && right == nil {
        return true
    }
    if left == nil || right == nil || left.Val != right.Val {
        return false
    }
    return isMirror(left.Left, right.Right) && isMirror(left.Right, right.Left)
}
```

---

## teemo-attacking

```javascript
/**
 * @param {number[]} timeSeries
 * @param {number} duration
 * @return {number}
 */
var findPoisonedDuration = function(timeSeries, duration) {
  var totalDuration = 0;
  var n = timeSeries.length;

  for (var i = 0; i < n; i++) {
    if (i > 0 && timeSeries[i] < timeSeries[i - 1] + duration) {
      totalDuration += timeSeries[i] - timeSeries[i - 1];
    } else {
      totalDuration += duration;
    }
  }

  return totalDuration;
};

```

---

## tenth-line

```bash
# Read from the file file.txt and output the tenth line to stdout.

filename="file.txt"
line_number=10

# Check if the file has at least 10 lines
if [ $(wc -l < "$filename") -ge $line_number ]; then
    # Print the 10th line using head and tail commands
    head -n $line_number "$filename" | tail -n 1
fi
```

---

## text-justification

```javascript
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
function fullJustify(words, maxWidth) {
    const result = [];
    let currentLine = [];
    let currentWidth = 0;

    for (let i = 0; i < words.length; i++) {
        const word = words[i];

        if (currentWidth + currentLine.length + word.length <= maxWidth) {
            // Add word to current line
            currentLine.push(word);
            currentWidth += word.length;
        } else {
            // Create a new line
            result.push(justifyLine(currentLine, maxWidth, false));
            currentLine = [word];
            currentWidth = word.length;
        }
    }

    // Justify the last line
    result.push(justifyLine(currentLine, maxWidth, true));

    return result;
}

function justifyLine(line, maxWidth, isLastLine) {
    const numWords = line.length;
    const totalWidth = line.reduce((acc, word) => acc + word.length, 0);
    const totalSpaces = maxWidth - totalWidth;

    if (numWords === 1 || isLastLine) {
        // Left-justify the line if it's the last line or has only one word
        return line.join(' ') + ' '.repeat(maxWidth - totalWidth - (numWords - 1));
    } else {
        const numGaps = numWords - 1;
        const spacesPerGap = Math.floor(totalSpaces / numGaps);
        const extraSpaces = totalSpaces % numGaps;

        let justifiedLine = '';
        for (let i = 0; i < line.length; i++) {
            justifiedLine += line[i];
            if (i < numGaps) {
                justifiedLine += ' '.repeat(spacesPerGap + (i < extraSpaces ? 1 : 0));
            }
        }

        return justifiedLine;
    }
}


```

---

## the-number-of-employees-which-report-to-each-employee

```mysql
# Write your MySQL query statement below

select e.employee_id, e.name, count(r.employee_id) as reports_count, round(avg(r.age)) as average_age from Employees e left join Employees r on e.employee_id = r.reports_to
where e.employee_id in (
    select distinct reports_to from Employees
)
group by e.employee_id, e.name
order by e.employee_id
```

---

## the-number-of-rich-customers

```pythondata
import pandas as pd

def count_rich_customers(store: pd.DataFrame) -> pd.DataFrame:
    rich_count = len(store[store['amount'] > 500]['customer_id'].unique())
    result = pd.DataFrame({'rich_count': [rich_count]})
    return result
```

---

## third-maximum-number

```golang

func thirdMax(nums []int) int {
	first := math.MinInt64
	second := math.MinInt64
	third := math.MinInt64

	for _, num := range nums {
		if num == first || num == second || num == third {
			continue
		}

		if num > first {
			third = second
			second = first
			first = num
		} else if num > second {
			third = second
			second = num
		} else if num > third {
			third = num
		}
	}

	if third == math.MinInt64 {
		return first
	}

	return third
}
```

---

## time-needed-to-rearrange-a-binary-string

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var secondsToRemoveOccurrences = function(s) {
    let seconds = 0;

    while (s.includes("01")) {
        s = s.replace(/01/g, "10");
        seconds++;
    }

    return seconds;
};
```

---

## timeout-cancellation

```javascript
/**
 * @param {Function} fn
 * @param {Array} args
 * @param {number} t
 * @return {Function}
 */
var cancellable = function(fn, args, t) {
    const id = setTimeout(_=>fn(...args), t);
    return _ => clearTimeout(id);
};

/**
 *  const result = []
 *
 *  const fn = (x) => x * 5
 *  const args = [2], t = 20, cancelT = 50
 *
 *  const log = (...argsArr) => {
 *      result.push(fn(...argsArr))
 *  }
 *       
 *  const cancel = cancellable(fn, args, t);
 *           
 *  setTimeout(() => {
 *     cancel()
 *     console.log(result) // [{"time":20,"returned":10}]
 *  }, cancelT)
 */
```

---

## to-be-or-not-to-be

```typescript
type ToBeOrNotToBe = {
    toBe: (val: any) => boolean;
    notToBe: (val: any) => boolean;
};

function expect(val: any): ToBeOrNotToBe {
    return {
        toBe: (expected: any) => {
        if (val !== expected) {
            throw new Error("Not Equal");
        }
        return true;
        },
        notToBe: (unexpected: any) => {
        if (val === unexpected) {
            throw new Error("Equal");
        }
        return true;
        }
    };
}

/**
 * expect(5).toBe(5); // true
 * expect(5).notToBe(5); // throws "Equal"
 */
```

---

## to-lower-case

```golang
func toLowerCase(s string) string {
    return strings.ToLower(s)
}
```

---

## toeplitz-matrix

```golang
func isToeplitzMatrix(matrix [][]int) bool {
	m := len(matrix)
	n := len(matrix[0])

	for i := 1; i < m; i++ {
		for j := 1; j < n; j++ {
			if matrix[i][j] != matrix[i-1][j-1] {
				return false
			}
		}
	}

	return true
}

```

---

## top-k-frequent-elements

```golang
type Item struct {
	value    int
	frequency int
}

type MinHeap []*Item

func (h MinHeap) Len() int           { return len(h) }
func (h MinHeap) Less(i, j int) bool { return h[i].frequency < h[j].frequency }
func (h MinHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MinHeap) Push(x interface{}) {
	*h = append(*h, x.(*Item))
}

func (h *MinHeap) Pop() interface{} {
	old := *h
	n := len(old)
	item := old[n-1]
	*h = old[0 : n-1]
	return item
}

func topKFrequent(nums []int, k int) []int {
	frequencyMap := make(map[int]int)

	// Build frequency map
	for _, num := range nums {
		frequencyMap[num]++
	}

	// Create a min-heap
	h := &MinHeap{}

	// Insert elements into the heap
	for value, frequency := range frequencyMap {
		item := &Item{
			value:    value,
			frequency: frequency,
		}
		heap.Push(h, item)
		if h.Len() > k {
			heap.Pop(h)
		}
	}

	// Extract the top k frequent elements from the heap
	result := make([]int, k)
	for i := k - 1; i >= 0; i-- {
		result[i] = heap.Pop(h).(*Item).value
	}

	return result
}
```

---

## total-cost-to-hire-k-workers

```javascript
var totalCost = function(costs, k, candidates) {
  let result = 0;

  const mincomp = (a, b) => (a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
  const left = new MinPriorityQueue({ compare: mincomp });
  const right = new MinPriorityQueue({ compare: mincomp });

  let l = 0;
  while (l < candidates && l < costs.length) {
    left.enqueue([costs[l], l]);
    ++l;
  }
  
  let r = costs.length - 1;
  while (l <= r && costs.length - candidates <= r) {
    right.enqueue([costs[r], r]);
    --r;
  }

  while (0 < k) {
    const lf = left.front();
    const rf = right.front();
    if (rf == null || (lf != null && lf[0] <= rf[0])) {
      result += lf[0];
      left.dequeue();
      if (l <= r) {
        left.enqueue([costs[l], l]);
        ++l;
      }
    } else {
      result += rf[0];
      right.dequeue();
      if (l <= r) {
        right.enqueue([costs[r], r]);
        --r;
      }
    }
    --k;
  }
  return result;
};
```

---

## transpose-file

```bash
# Read from the file file.txt and print its transposed content to stdout.

transpose=$(awk '{ for(i=1; i<=NF; i++) { a[i,NR]=$i } } END { for(i=1; i<=NF; i++) { for(j=1; j<=NR; j++) { printf "%s%s", a[i,j], (j==NR ? RS : FS) } } }' file.txt)

echo "$transpose"
```

---

## transpose-matrix

```javascript
/**
 * @param {number[][]} matrix
 * @return {number[][]}
 */
var transpose = function(matrix) {
    let m = matrix.length
    let n = matrix[0].length

    let transposed = new Array(n).fill(0).map(() => new Array(m).fill(0));

    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            transposed[j][i] = matrix[i][j];
        }
    }

    return transposed;

};
```

---

## trapping-rain-water

```golang
func trap(height []int) int {
    if len(height) <= 2 {
        return 0
    }

    leftMax := make([]int, len(height))
    rightMax := make([]int, len(height))

    leftMax[0] = height[0]
    for i := 1; i < len(height); i++ {
        leftMax[i] = max(leftMax[i-1], height[i])
    }

    rightMax[len(height)-1] = height[len(height)-1]
    for i := len(height) - 2; i >= 0; i-- {
        rightMax[i] = max(rightMax[i+1], height[i])
    }

    totalWater := 0
    for i := 0; i < len(height); i++ {
        minHeight := min(leftMax[i], rightMax[i])
        if minHeight > height[i] {
            totalWater += minHeight - height[i]
        }
    }

    return totalWater
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

```

---

## triangle

```javascript
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
  const n = triangle.length;
  const dp = triangle[n - 1];

  for (let row = n - 2; row >= 0; row--) {
    for (let col = 0; col <= row; col++) {
      dp[col] = triangle[row][col] + Math.min(dp[col], dp[col + 1]);
    }
  }

  return dp[0];
}

```

---

## triangle-judgement

```mysql
# Write your MySQL query statement below

select x, y, z, 
  case
    when x + y > z and y + z > x and x + z > y then 'Yes'
    else 'No'
  end as triangle
from Triangle;

```

---

## two-out-of-three

```golang
func twoOutOfThree(nums1 []int, nums2 []int, nums3 []int) []int {
    hash := make(map[int]int)
    result := []int{}

    addToMap := func(nums []int) {
        unique := make(map[int]bool)
        for _, num := range nums {
            unique[num] = true
        }

        for num := range unique {
            hash[num]++
        }
    }

    addToMap(nums1)
    addToMap(nums2)
    addToMap(nums3)

    for num, count := range hash {
        if (count >= 2) {
            result = append(result, num)
        }
    }

    return result
}
```

---

## two-sum

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
typedef struct HashNode {
    int key;
    int value;
    struct HashNode* next;
} HashNode;

typedef struct HashMap {
    HashNode** buckets;
    int size;
} HashMap;

HashMap* createHashMap(int size) {
    HashMap* map = (HashMap*)malloc(sizeof(HashMap));
    map->size = size;
    map->buckets = (HashNode**)malloc(sizeof(HashNode*) * size);
    for (int i = 0; i < size; i++) {
        map->buckets[i] = NULL;
    }
    return map;
}

int hashCode(int key, int size) {
    return abs(key) % size;
}

void insert(HashMap* map, int key, int value) {
    int index = hashCode(key, map->size);
    HashNode* newNode = (HashNode*)malloc(sizeof(HashNode));
    newNode->key = key;
    newNode->value = value;
    newNode->next = map->buckets[index];
    map->buckets[index] = newNode;
}

int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    HashMap* map = createHashMap(numsSize);
    for (int i = 0; i < numsSize; i++) {
        int complement = target - nums[i];
        int index = hashCode(complement, numsSize);
        HashNode* current = map->buckets[index];
        while (current != NULL) {
            if (current->key == complement) {
                int* result = (int*)malloc(sizeof(int) * 2);
                result[0] = current->value;
                result[1] = i;
                *returnSize = 2;
                return result;
            }
            current = current->next;
        }
        insert(map, nums[i], i);
    }
    *returnSize = 0; // No solution found
    return NULL;
}

```

---

## two-sum-ii-input-array-is-sorted

```golang
func twoSum(numbers []int, target int) []int {
    left, right := 0, len(numbers)-1
    for left < right {
        sum := numbers[left] + numbers[right]
        if sum == target {
            return []int{left+1, right+1}
        } else if sum < target {
            left++
        } else {
            right--
        }
    }
    return []int{}
}
```

---

## two-sum-iv-input-is-a-bst

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func findTarget(root *TreeNode, k int) bool {
    // Create an empty hash set
    numSet := make(map[int]bool)
    return dfs(root, k, numSet)
}

func dfs(node *TreeNode, k int, numSet map[int]bool) bool {
    if node == nil {
        return false
    }

    // Check if the complement exists in the hash set
    if numSet[k-node.Val] {
        return true
    }

    // Add the current node's value to the hash set
    numSet[node.Val] = true

    // Recursively search the left and right subtrees
    return dfs(node.Left, k, numSet) || dfs(node.Right, k, numSet)
}
```

---

## ugly-number

```golang
func isUgly(n int) bool {
	if n <= 0 {
		return false
	}

	for n%2 == 0 {
		n /= 2
	}

	for n%3 == 0 {
		n /= 3
	}

	for n%5 == 0 {
		n /= 5
	}

	return n == 1
}
```

---

## uncommon-words-from-two-sentences

```golang
func uncommonFromSentences(s1 string, s2 string) []string {
    words1 := strings.Fields(s1)
    words2 := strings.Fields(s2)

    wordCount := make(map[string]int)

    for _, word := range words1 {
        wordCount[word]++
    }

    for _, word := range words2 {
        wordCount[word]++
    }

    uncommonWords := []string{}

    for word, count := range wordCount {
        if count == 1 {
            uncommonWords = append(uncommonWords, word)
        }
    }

    return uncommonWords
}
```

---

## uncrossed-lines

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var maxUncrossedLines = function(nums1, nums2) {
    const m = nums1.length, n = nums2.length;
    const dp = Array.from({length: m+1}, () => new Array(n+1).fill(0));
    for (let i=1; i<=m; i++) {
        for (let j=1; j<=n; j++) {
            if (nums1[i-1] === nums2[j-1]) {
                dp[i][j] = 1 + dp[i-1][j-1]
            } else {
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1])
            }
        }
    }
    return dp[m][n];
};
```

---

## unique-email-addresses

```golang
func numUniqueEmails(emails []string) int {
    uniqueEmails := make(map[string]bool)

    for _, email := range emails {
        normalizedEmail := normalizeEmail(email)
        uniqueEmails[normalizedEmail] = true
    }

    return len(uniqueEmails)
}

func normalizeEmail(email string) string {
    parts := strings.Split(email, "@")
    localName := parts[0]
    domainName := parts[1]

    localName = strings.Split(localName, "+")[0] // Remove everything after '+'
    localName = strings.ReplaceAll(localName, ".", "") // Remove all '.' characters

    return localName + "@" + domainName
}

```

---

## unique-length-3-palindromic-subsequences

```golang
func countPalindromicSubsequence(s string) int {
    count := 0
    for i := 'a'; i <= 'z'; i++ {
        first, last := -1, -1
        for j := 0; j < len(s); j++ {
            if rune(s[j]) == i {
                if first == -1 {
                    first = j
                }
                last = j
            }
        }
        if first != -1 && last != -1 && last-first > 1 {
            count += len(uniqueSubsequences(s[first+1:last]))
        }
    }
    return count
}

func uniqueSubsequences(s string) map[rune]bool {
    result := make(map[rune]bool)
    for _, char := range s {
        result[char] = true
    }
    return result
}

```

---

## unique-morse-code-words

```golang
func uniqueMorseRepresentations(words []string) int {
    morseCodes := []string{
        ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--",
        "-.", "---", ".--.", "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--..",
    }

    uniqueTransformations := make(map[string]bool)

    for _, word := range words {
        transformation := ""
        for _, letter := range word {
            transformation += morseCodes[letter-'a']
        }
        uniqueTransformations[transformation] = true
    }

    return len(uniqueTransformations)
}

```

---

## unique-number-of-occurrences

```typescript
function uniqueOccurrences(arr: number[]): boolean {
  const occurrenceCount = new Map<number, number>();

  for (const num of arr) {
    if (occurrenceCount.has(num)) {
      occurrenceCount.set(num, occurrenceCount.get(num)! + 1);
    } else {
      occurrenceCount.set(num, 1);
    }
  }

  const occurrenceSet = new Set(occurrenceCount.values());

  return occurrenceSet.size === occurrenceCount.size;
}

```

---

## unique-paths

```golang
func uniquePaths(m int, n int) int {
    // Create a 2D grid to store the number of paths for each cell
    grid := make([][]int, m)
    for i := 0; i < m; i++ {
        grid[i] = make([]int, n)
    }
    
    // Set the number of paths for the first row and first column to 1
    for i := 0; i < m; i++ {
        grid[i][0] = 1
    }
    for j := 0; j < n; j++ {
        grid[0][j] = 1
    }
    
    // Calculate the number of paths for each cell based on the previous cells
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            grid[i][j] = grid[i-1][j] + grid[i][j-1]
        }
    }
    
    // Return the number of paths for the bottom-right cell
    return grid[m-1][n-1]
}

```

---

## unique-paths-ii

```javascript
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    const m = obstacleGrid.length;
    const n = obstacleGrid[0].length;

    if (obstacleGrid[0][0] === 1 || obstacleGrid[m - 1][n - 1] === 1) {
        return 0; // If the starting or ending position is an obstacle, there is no path
    }

    const dp = Array(m).fill(0).map(() => Array(n).fill(0));
    dp[0][0] = 1; // Set the starting position as reachable

    // Initialize the first column
    for (let i = 1; i < m; i++) {
        if (obstacleGrid[i][0] === 0) {
            dp[i][0] = dp[i - 1][0];
        }
    }

    // Initialize the first row
    for (let j = 1; j < n; j++) {
        if (obstacleGrid[0][j] === 0) {
            dp[0][j] = dp[0][j - 1];
        }
    }

    // Calculate the number of paths for each cell
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 0) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
    }

    return dp[m - 1][n - 1]; // Return the number of paths for the bottom-right cell
}
```

---

## univalued-binary-tree

```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isUnivalTree(root *TreeNode) bool {
    return isUnivalTreeHelper(root, root.Val)
}

func isUnivalTreeHelper(node *TreeNode, val int) bool {
    if node == nil {
        return true
    }

    if node.Val != val {
        return false
    }

    return isUnivalTreeHelper(node.Left, val) && isUnivalTreeHelper(node.Right, val)
}
```

---

## user-activity-for-the-past-30-days-i

```mysql
# Write your MySQL query statement below

select activity_date as day, count(distinct user_id) as active_users
from Activity
where activity_date between date_sub('2019-07-27', interval 29 day) and '2019-07-27'
group by activity_date;

```

---

## valid-anagram

```ruby
# @param {String} s
# @param {String} t
# @return {Boolean}
def is_anagram(s, t)
    return false if s.length != t.length
    
    s_count = Hash.new(0)
    t_count = Hash.new(0)

    s.each_char { |char| s_count[char] += 1}
    t.each_char { |char| t_count[char] += 1}

    return s_count == t_count
end
```

---

## valid-boomerang

```golang
func isBoomerang(points [][]int) bool {
    // Check if the points are distinct
    if points[0][0] == points[1][0] && points[0][1] == points[1][1] ||
        points[0][0] == points[2][0] && points[0][1] == points[2][1] ||
        points[1][0] == points[2][0] && points[1][1] == points[2][1] {
        return false
    }

    // Check if the slopes of two lines are not equal
    return (points[0][1]-points[1][1])*(points[0][0]-points[2][0]) != (points[0][1]-points[2][1])*(points[0][0]-points[1][0])
}

```

---

## valid-mountain-array

```golang
func validMountainArray(arr []int) bool {
    n := len(arr)
    if n < 3 {
        return false
    }
    
    // Find the peak of the mountain
    peak := 0
    for peak < n-1 && arr[peak] < arr[peak+1] {
        peak++
    }
    
    // Check if the peak is not at the beginning or end
    if peak == 0 || peak == n-1 {
        return false
    }
    
    // Check if the right side of the peak is decreasing
    for i := peak; i < n-1; i++ {
        if arr[i] <= arr[i+1] {
            return false
        }
    }
    
    return true   
}
```

---

## valid-number

```golang
func isNumber(s string) bool {
    // Define a regular expression pattern for a valid number
    pattern := `^[\+\-]?(\d+(\.\d*)?|\.\d+)([eE][\+\-]?\d+)?$`

    // Compile the regular expression
    re := regexp.MustCompile(pattern)

    // Use the MatchString function to check if the string matches the pattern
    return re.MatchString(s)
}

```

---

## valid-palindrome

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    s = s.toLowerCase().replace(/[^a-z0-9]/g,"");
    return s == s.split("").reverse().join("");
};
```

---

## valid-palindrome-ii

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var validPalindrome = function(s) {
    let left = 0;
    let right = s.length-1;
    while (left < right) {
        if (s[left] !== s[right]) {
            return (
                isPalindrome(s, left + 1, right) ||
                isPalindrome(s, left, right - 1)
            )
        }
        left++;
        right--;
    }
    return true;
};

var isPalindrome = function(s, left, right) {
    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

---

## valid-parentheses

```c
// Define a structure for the stack
typedef struct {
    char data[10000];
    int top;
} Stack;

// Initialize the stack
void initialize(Stack* stack) {
    stack->top = -1;
}

// Push an element onto the stack
void push(Stack* stack, char element) {
    stack->data[++stack->top] = element;
}

// Pop an element from the stack
char pop(Stack* stack) {
    return stack->data[stack->top--];
}

// Check if the stack is empty
bool isEmpty(Stack* stack) {
    return stack->top == -1;
}

// Function to check if the input string is valid
bool isValid(char* s) {
    int len = strlen(s);
    Stack stack;
    initialize(&stack);

    for (int i = 0; i < len; i++) {
        char current = s[i];

        if (current == '(' || current == '[' || current == '{') {
            push(&stack, current);
        } else {
            if (isEmpty(&stack)) {
                return false;
            }

            char top = pop(&stack);

            if ((current == ')' && top != '(') ||
                (current == ']' && top != '[') ||
                (current == '}' && top != '{')) {
                return false;
            }
        }
    }

    return isEmpty(&stack);
}
```

---

## valid-perfect-square

```golang
func isPerfectSquare(num int) bool {
	if num < 1 {
		return false
	}

	left, right := 1, num

	for left <= right {
		mid := left + (right-left)/2
		square := mid * mid

		if square == num {
			return true
		} else if square < num {
			left = mid + 1
		} else {
			right = mid - 1
		}
	}

	return false
}

/*
In this implementation, the isPerfectSquare function takes a positive integer num and determines if it is a perfect square. It returns false if num is less than 1 since perfect squares are always positive integers.

We initialize left as 1 and right as num for the binary search. We continue the search until left is less than or equal to right. In each iteration, we calculate the square of the middle element (mid) using mid * mid. We then compare the calculated square with num. If they are equal, num is a perfect square, and we return true. If the calculated square is less than num, we update left to mid + 1 to search the upper half of the remaining range. Otherwise, if the calculated square is greater than num, we update right to mid - 1 to search the lower half of the remaining range.

If the search completes without finding a perfect square, the function returns false.
*/
```

---

## valid-phone-numbers

```bash
# Read from the file file.txt and output all valid phone numbers to stdout.
grep -E '^(\([0-9]{3}\) |[0-9]{3}-)[0-9]{3}-[0-9]{4}$' file.txt

```

---

## valid-sudoku

```golang
func isValidSudoku(board [][]byte) bool {
    // Create sets to track digits in each row, column, and sub-grid
	rows := make([]map[byte]bool, 9)
	cols := make([]map[byte]bool, 9)
	grids := make([]map[byte]bool, 9)

	for i := 0; i < 9; i++ {
		rows[i] = make(map[byte]bool)
		cols[i] = make(map[byte]bool)
		grids[i] = make(map[byte]bool)
	}

	for i := 0; i < 9; i++ {
		for j := 0; j < 9; j++ {
			digit := board[i][j]

			if digit == '.' {
				continue // Skip empty cells
			}

			// Check row
			if rows[i][digit] {
				return false
			}
			rows[i][digit] = true

			// Check column
			if cols[j][digit] {
				return false
			}
			cols[j][digit] = true

			// Check sub-grid
			gridIdx := (i/3)*3 + j/3
			if grids[gridIdx][digit] {
				return false
			}
			grids[gridIdx][digit] = true
		}
	}

	return true
}
```

---

## validate-binary-search-tree

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */
 
function isValidBST(root: TreeNode | null): boolean {
  return validateNode(root, null, null);
}

function validateNode(node: TreeNode | null, min: number | null, max: number | null): boolean {
  if (node === null) {
    return true;
  }

  if ((min !== null && node.val <= min) || (max !== null && node.val >= max)) {
    return false;
  }

  return (
    validateNode(node.left, min, node.val) && 
    validateNode(node.right, node.val, max)
  );
}
```

---

## validate-binary-tree-nodes

```typescript
function validateBinaryTreeNodes(n: number, leftChild: number[], rightChild: number[]): boolean {
    const childrenSet = new Set([...leftChild, ...rightChild]);
    let rootNode: number = null;
    for (let i = 0; i < n; i++) {
        if (! childrenSet.has(i)) {
            rootNode = i;
            break;
        }
    }

    // The binary tree have a root (root has no parent)
    if (rootNode === null) {
        return false;
    }

    const visited = new Set([rootNode]);
    const stack = [rootNode];

    while (stack.length > 0) {
        const node = stack.pop();
        for (const child of [leftChild[node], rightChild[node]]) {
            if (child == -1) continue;

            // Every node have 1 parent + There are no cycle
            if (visited.has(child)) {
                return false;
            }

            stack.push(child);
            visited.add(child);
        }
    }

    // Every node must be connected
    return visited.size == n;

};
```

---

## validate-stack-sequences

```golang
func validateStackSequences(pushed []int, popped []int) bool {
    stack := make([]int, 0)
    i := 0
    for _, x := range pushed {
        stack = append(stack, x)
        for len(stack) > 0 && stack[len(stack)-1] == popped[i] {
            stack = stack[:len(stack)-1]
            i++
        }
    }
    return i == len(popped)
}
```

---

## verifying-an-alien-dictionary

```golang
func isAlienSorted(words []string, order string) bool {
    alienOrder := make(map[byte]int)
    for i, char := range order {
        alienOrder[byte(char)] = i
    }

    for i := 1; i < len(words); i++ {
        if !isLexicographicallySorted(words[i-1], words[i], alienOrder) {
            return false
        }
    }

    return true
}

func isLexicographicallySorted(word1, word2 string, alienOrder map[byte]int) bool {
    i, j := 0, 0
    for i < len(word1) && j < len(word2) {
        if alienOrder[word1[i]] < alienOrder[word2[j]] {
            return true
        } else if alienOrder[word1[i]] > alienOrder[word2[j]] {
            return false
        }
        i++
        j++
    }

    return i == len(word1) || j < len(word2)
}

```

---

## wildcard-matching

```golang
func isMatch(s string, p string) bool {
    // Create a two-dimensional boolean array to store the matching results
    dp := make([][]bool, len(s)+1)
    for i := 0; i <= len(s); i++ {
        dp[i] = make([]bool, len(p)+1)
    }
    
    // An empty pattern matches an empty string
    dp[0][0] = true
    
    // Handling cases where '*' matches an empty sequence
    for j := 1; j <= len(p); j++ {
        if p[j-1] == '*' {
            dp[0][j] = dp[0][j-1]
        }
    }
    
    // Fill the dynamic programming table
    for i := 1; i <= len(s); i++ {
        for j := 1; j <= len(p); j++ {
            if p[j-1] == '*' {
                // Either '*' matches an empty sequence (dp[i][j-1]),
                // or '*' matches the current character in the string (dp[i-1][j]).
                dp[i][j] = dp[i][j-1] || dp[i-1][j]
            } else if p[j-1] == '?' || p[j-1] == s[i-1] {
                // If the current characters match or the pattern has a '?',
                // then the result depends on the previous characters' matching result.
                dp[i][j] = dp[i-1][j-1]
            }
        }
    }
    
    // The last cell of the table represents the matching result for the entire string and pattern
    return dp[len(s)][len(p)]
}

```

---

## word-break

```javascript
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {
  const n = s.length;
  const dp = new Array(n + 1).fill(false);
  dp[0] = true;

  for (let i = 1; i <= n; i++) {
    for (let j = 0; j < i; j++) {
      if (dp[j] && wordDict.includes(s.substring(j, i))) {
        dp[i] = true;
        break;
      }
    }
  }

  return dp[n];
}

```

---

## word-frequency

```bash
# Read from the file words.txt and output the word frequency list to stdout.
cat words.txt | tr -s ' ' '\n' | sort | uniq -c | sort -nr | awk '{print $2, $1}'
```

---

## word-ladder

```golang
func ladderLength(beginWord string, endWord string, wordList []string) int {
	// Convert wordList to a set for efficient word lookup
	wordSet := make(map[string]bool)
	for _, word := range wordList {
		wordSet[word] = true
	}

	// If endWord is not in the wordList, there is no valid transformation sequence
	if !wordSet[endWord] {
		return 0
	}

	// Perform BFS starting from the beginWord
	queue := []string{beginWord}
	visited := make(map[string]bool)
	visited[beginWord] = true
	level := 1

	for len(queue) > 0 {
		size := len(queue)

		// Process all words at the current level
		for i := 0; i < size; i++ {
			word := queue[0]
			queue = queue[1:]

			// Generate all possible transformations of the word
			for j := 0; j < len(word); j++ {
				for ch := 'a'; ch <= 'z'; ch++ {
					newWord := word[:j] + string(ch) + word[j+1:]

					// If the newWord is in the wordSet and not visited yet, enqueue it
					if wordSet[newWord] && !visited[newWord] {
						if newWord == endWord {
							return level + 1 // Found the endWord
						}
						queue = append(queue, newWord)
						visited[newWord] = true
					}
				}
			}
		}

		level++
	}

	return 0 // No transformation sequence found
}
```

---

## word-pattern

```javascript
/**
 * @param {string} pattern
 * @param {string} s
 * @return {boolean}
 */
var wordPattern = function(pattern, s) {
  const words = s.split(' ');

  if (pattern.length !== words.length) {
    return false;
  }

  const patternToWord = new Map();
  const wordToPattern = new Map();

  for (let i = 0; i < pattern.length; i++) {
    const char = pattern[i];
    const word = words[i];

    if (!patternToWord.has(char) && !wordToPattern.has(word)) {
      patternToWord.set(char, word);
      wordToPattern.set(word, char);
    } else if (patternToWord.get(char) !== word || wordToPattern.get(word) !== char) {
      return false;
    }
  }

  return true;
}
```

---

## word-search

```golang
func exist(board [][]byte, word string) bool {
    rows := len(board)
    cols := len(board[0])
    
    // Create a visited array to keep track of visited cells
    visited := make([][]bool, rows)
    for i := 0; i < rows; i++ {
        visited[i] = make([]bool, cols)
    }
    
    // Iterate through each cell and check if the word exists
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if board[i][j] == word[0] && backtrack(board, word, visited, i, j, 0) {
                return true
            }
        }
    }
    
    return false
}

func backtrack(board [][]byte, word string, visited [][]bool, row, col, index int) bool {
    // Check if all characters in the word have been found
    if index == len(word) {
        return true
    }
    
    // Check if the current cell is out of bounds or has been visited
    if row < 0 || row >= len(board) || col < 0 || col >= len(board[0]) || visited[row][col] {
        return false
    }
    
    // Check if the current cell matches the character in the word
    if board[row][col] != word[index] {
        return false
    }
    
    // Mark the current cell as visited
    visited[row][col] = true
    
    // Explore the neighboring cells in a recursive manner
    found := backtrack(board, word, visited, row-1, col, index+1) ||
        backtrack(board, word, visited, row+1, col, index+1) ||
        backtrack(board, word, visited, row, col-1, index+1) ||
        backtrack(board, word, visited, row, col+1, index+1)
    
    // Mark the current cell as unvisited for future backtracking
    visited[row][col] = false
    
    return found
}

```

---

## word-search-ii

```golang
type TrieNode struct {
	children [26]*TrieNode
	word     string
}

func buildTrie(words []string) *TrieNode {
	root := &TrieNode{}

	for _, word := range words {
		node := root
		for _, ch := range word {
			index := ch - 'a'
			if node.children[index] == nil {
				node.children[index] = &TrieNode{}
			}
			node = node.children[index]
		}
		node.word = word
	}

	return root
}

func findWords(board [][]byte, words []string) []string {
	// Build the trie from the given words
	trie := buildTrie(words)

	// Perform backtracking for each cell in the board
	result := make([]string, 0)
	for i := 0; i < len(board); i++ {
		for j := 0; j < len(board[0]); j++ {
			backtrack(board, i, j, trie, &result)
		}
	}

	return result
}

func backtrack(board [][]byte, row, col int, trie *TrieNode, result *[]string) {
	ch := board[row][col]
	if ch == '#' || trie.children[ch-'a'] == nil {
		return
	}

	trie = trie.children[ch-'a']
	if trie.word != "" {
		*result = append(*result, trie.word)
		trie.word = ""
	}

	board[row][col] = '#'
	if row > 0 {
		backtrack(board, row-1, col, trie, result)
	}
	if col > 0 {
		backtrack(board, row, col-1, trie, result)
	}
	if row < len(board)-1 {
		backtrack(board, row+1, col, trie, result)
	}
	if col < len(board[0])-1 {
		backtrack(board, row, col+1, trie, result)
	}
	board[row][col] = ch
}

```

---

## x-of-a-kind-in-a-deck-of-cards

```javascript
/**
 * @param {number[]} deck
 * @return {boolean}
 */
var hasGroupsSizeX = function(deck) {
    const counts = new Map();
    for (const card of deck) {
        if (counts.has(card)) {
            counts.set(card, counts.get(card) + 1);
        } else {
            counts.set(card, 1);
        }
    }

    const values = Array.from(counts.values());
    let gcd = values[0];
    for (let i = 1; i < values.length; i++) {
        gcd = GCD(gcd, values[i]);
    }

    return gcd >= 2;
};

function GCD(a, b) {
    if (b === 0) return a;
    return GCD(b, a % b);
}
```

---

## zigzag-conversion

```typescript
function convert(s: string, numRows: number): string {
    if (numRows === 1 || s.length <= numRows) {
        return s;
    }

    const resultRows: string[] = new Array(numRows).fill('');
    let currentRow = 0;
    let direction = -1;

    for (let i = 0; i < s.length; i++) {
        resultRows[currentRow] += s[i];

        if (currentRow === 0 || currentRow === numRows - 1) {
            direction *= -1;
        }

        currentRow += direction;
    }

    return resultRows.join('');
};
```

---

