# CrackYourPlacement
# 1 def findDuplicate(self, nums):
def findDuplicate(self, nums):
        for ele in nums:
            x=abs(ele)
            if nums[x]<0:
                ans = x
                break
            nums[x]=-nums[x]
        
        for i in range(len(nums)):
            nums[i]=abs(nums[i])
        return ans

# 2
def sortColors(self, nums):
        si=0
        mid=0
        li=len(nums)-1
        while mid<=li:
            if nums[mid]==0:
                nums[mid],nums[si]=nums[si],nums[mid]
                mid+=1
                si+=1
            elif nums[mid]==1:
                mid+=1
            else:
                nums[mid],nums[li]=nums[li],nums[mid]
                
                li-=1
        return nums

# 3
 def removeDuplicates(self, nums):
        prev=0
        i=1
        while i<len(nums):
            if nums[i]!=nums[prev]:
                nums[i],nums[prev+1]=nums[prev+1],nums[i]
                prev+=1
            i+=1
        return prev+1

# 4
def moveZeroes(self, nums):
        count=0
        for ele in nums:
            if ele==0:
                count+=1
        s=0
        for i in range(len(nums)):
            if nums[i]!=0:
                nums[s]=nums[i]
                s+=1
        while count>0:
            nums[-count]=0
            count-=1
        return nums
       
# 5
def maxProfit(self, prices):
        m=prices[0]
        profit=-1
        for i in range(1,len(prices)):
            if (prices[i]-m)>0:
                profit=max(profit,prices[i]-m)
            m=min(m,prices[i])
        if profit<0:
            return 0
        return profit
        
# 6
min difference
sort the given array and find difference between small sized and large sized packet and return the minimun difference as answer
        
# 7
def twoSum(self, nums, target):
        sum_dict={}
        ans=[]
        for i in range(len(nums)):
            x = nums[i]
            if x in sum_dict:
                ans.append(sum_dict[x])
                ans.append(i)
                return ans
            sum_dict[target-nums[i]]=i

# 8
 def maxProfit(self, prices):
        buy=prices[0]
        sell=0
        profit=0
        for i in range(1,len(prices)):
            if prices[i] - prices[i-1]>0:
                profit+=prices[i] - prices[i-1]
        return profit
