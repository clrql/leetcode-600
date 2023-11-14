
  # find-in-mountain-array

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
  