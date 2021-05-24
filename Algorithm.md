# Heap_sort
class Solution(object):
    def heap_sort(self, nums):
        n =len(nums)
        self.nums = nums
        # 构造大顶堆，从非叶子节点开始倒序遍历，因此是l//2 -1 就是最后一个非叶子节点
        for i in range(n // 2 -1 , -1, -1):
            self.build_heap(i, n - 1)
        # 上面的循环完成了大顶堆的构造，那么就开始把根节点跟末尾节点交换，然后重新调整大顶堆
        for j in range(n -1, 0, -1):
            nums[0], nums[j] = nums[j], nums[0]
            self.build_heap(0, j - 1)

        return nums

    def build_heap(self, i, n):
        """构建大顶堆"""
        nums = self.nums
        left, right = 2 * i + 1, 2 * i + 2  ## 左右子节点的下标
        large_index = i
        if left < n and nums[i] < nums[left]:
            large_index = left

        if right < n and nums[large_index] < nums[right]:
            large_index = right

        # 通过上面跟左右节点比较后，得出三个元素之间较大的下标，如果较大下表不是父节点的下标，说明交换后需要重新调整大顶堆
        if large_index != i:
            nums[i], nums[large_index] = nums[large_index], nums[i]
            self.build_heap(large_index, n)

# test
nums = [12,11,15,13,4,5,6,7,20]
solution = Solution()
print(solution.heap_sort(nums))
