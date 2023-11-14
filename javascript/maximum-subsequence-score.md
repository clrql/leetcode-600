
  # maximum-subsequence-score

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
  