
  # number-of-longest-increasing-subsequence

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
  