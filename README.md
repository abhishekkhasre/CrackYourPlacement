# CrackYourPlacement
# 1 
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

# 9
 def subarraysDivByK(self, nums, k):
        c=0
        curr_sum=0
        dict={0:1}
        for i in range(len(nums)):
            curr_sum+=nums[i]
            r=((curr_sum%k)+k)%k
            c+=dict.get(r,0)
            dict[r]=dict.get(r,0)+1
         
        return c
# 10
def maxArea(self, height):
        l=0
        r=len(height)-1
        maxarea=0
        while l<r:
            width=r-l
            maxarea=max(maxarea,(width)*min(height[l],height[r]))
            
            if height[l]<height[r]:
                l+=1
            else:
                r=r-1
        return maxarea
# 11
def threeSum(self, nums):
        nums.sort()
        n=len(nums)
        ans=[]
        checkset=set()
        for i in range(n):
            x=nums[i]
            s=i+1
            e=n-1
            t=0-x
            while s<e:
                st=nums[s]+nums[e]
                if st>t:
                    e=e-1
                elif st<t:
                    s+=1
                else:
                    d=str(x)+str(nums[s])+str(nums[e])
                    if d in checkset:
                        s+=1
                        e-=1
                        
                    else:
                        checkset.add(d)
                    
                        ans.append([x,nums[s],nums[e]])
                        s+=1
                        e-=1
                    
        return ans
                
               
# 12
def fourSum(self, nums, target):
        nums.sort()
        n=len(nums)
        checkset=set()
        ans=[]
        for j in range(n-3):
            
            for i in range(j+1,n-2):
                x=nums[j]+nums[i]
                s=i+1
                e=n-1
                t=target-x
                while s<e:
                    ss=nums[e]+nums[s]
                    if ss>t:
                        e=e-1
                    elif ss<t:
                        s+=1
                    else:
                        c_set=str(nums[j])+str(nums[i])+str(nums[s])+str(nums[e])
                        if c_set in checkset:
                            s+=1
                            e=e-1
                        else:
                            ans.append([nums[j],nums[i],nums[s],nums[e]])
                            checkset.add(c_set)
                            s+=1
                            e=e-1
        return ans
                      
# 13
def maxScore(self, cardPoints, k):
        rest=sum(cardPoints[:k])
        total=rest
        for i in range(k-1,-1,-1):
            rest=rest-cardPoints[i]+cardPoints[i-k]
            total=max(total,rest)
        return total
# 14
def subarraySum(self, nums, k):
        c=0
        s={}
        curr=0
        for i in range(len(nums)):
            curr+=nums[i]
            if curr==k:
                c+=1
            if curr-k in s:
                c+=s.get(curr-k)
            s[curr]=s.get(curr,0)+1
        return c

# 15
 def isValid(self, s):
        stack=[]
        for i in range(len(s)):
            x=s[i]
            if x=="(" or x=="{" or x=="[":
                stack.append(x)
            else:
                if len(stack)<1:
                    return False
                if x==")":
                    d=stack.pop()
                    if d=="(":
                        continue
                    else:
                        return False
                elif x=="]":
                    d=stack.pop()
                    if d=="[":
                        continue
                    else:
                        return False
                else:
                    d=stack.pop()
                    if d=="{":
                        continue
                    else:
                        return False
        if len(stack)>=1:
            return False
        return True 

# 16
def canJump(self, nums):
        max_index=0
        for i in range(len(nums)):
            if i>max_index:
                return False
            else:
                max_index=max(max_index,i+nums[i])
        return True
              

# 17
def merge(self, nums1, m, nums2, n):
        f=m+n-1
        e1=m-1
        e2=n-1
        if n==0:
            return
        elif m==0:
            while nums1:
                nums1.pop()
            nums1.extend(nums2)
            return
        while f>=0 and e1>=0 and e2>=0:
            if nums1[e1]>nums2[e2]:
                nums1[f]=nums1[e1]
                e1-=1
            else:
                nums1[f]=nums2[e2]
                e2-=1
            f=f-1
        while f>=0 and e2>=0:
            nums1[f]=nums2[e2]
            e2-=1
            f=f-1

# 18
def reversePairs(self, nums):
        c=0
        for i in range(len(nums)):
            x=nums[i]
            for j in range(i+1,len(nums)):
                if nums[i]>2*nums[j]:
                    c+=1
        return c
# 19
def strStr(self, haystack, needle):
        n=len(needle)
        h=len(haystack)
        
        for i in range(h):
            if haystack[i:n+i]==needle:
                return i
        return -1

# 20
def longestCommonPrefix(self, strs):
        m=1000000000
        a=""
        
        for ele in strs:
            if len(ele)<m:
                a=ele
                m=len(ele)
        ans=""
        for i in range(len(a)):
            for j in range(len(strs)):
                if strs[j][i]==a[i]:
                    continue
                else:
                    return ans
                    break
            
            ans+=a[i]
        return ans

# 21
 def validPalindrome(self, s):
        i=0
        j=len(s)-1
        while i<j:
            if i==len(s)-1:
                x=s[:i]
                if x==x[::-1]:
                    return True
            else:
                x=s[:i]+s[i+1:]
                if x==x[::-1]:
                    return True
        return False
# 22
 def intToRoman(self, num):
        ans=""
        d={1:"I",5:"V",10:"X",50:"L",100:"C",500:"D",1000:"M"}
        for i in range(len(str(num))-1,-1,-1):
            n=num//(10**i)
            if 1<=n<4:
                ans+=str(d[(10**i)]*n)
            elif n==4 or n==9:
                ans+=str(d[10**i])+str(d[(n+1)*(10**i)])
            elif n>=5:
                ans+=str(d[5*(10**i)])+(d[10**i]*(n-5))
            
            num=num%(10**i)
        return ans
# 23
 def generateParenthesis(self, n):
        ans=[]
         
        def backtrack(s=[],l=0,r=0):
            if len(s)==2*n:
                ans.append("".join(s))
                return
            if l<n:
                s.append("(")
                backtrack(s,l+1,r)
                s.pop()
            
            if r<l:
                s.append(")")
                backtrack(s,l,r+1)
                s.pop()
        backtrack()
        return ans
# 24
def simplifyPath(self, path):
        ans=[]
        res=""
        for i in range(1,len(path)):
            if path[i]=="/":
                if res==".":
                    res=""
                    continue
                elif res=="..":
                    if len(ans)!=0:
                        print(ans)
                        ans.pop()
                    res=""
                else:
                    if res!="":
                        ans.append(res)
                    res=""
            else:
                res+=path[i]
        a="/"
        if res==".." and len(ans)!=0:
            ans.pop()
        else:
            if res!="." and res!="" and res!="..":
                ans.append(res)
                
                
        for i in range(len(ans)):
            if i==0:
                a+=ans[i]
            else:
                a+="/"+ans[i]
        return a
                
# 25
def reverseWords(self, s):
        ans=list(s.split(" "))
        print(ans)
        a=""
        for i in range(len(ans)-1,-1,-1):
            if ans[i]==" " or ans[i]=="":
                continue
            else:
                if len(a)==0:
                    a+=ans[i]
                else:
                    a=a+" "+ans[i]
        return a

# 26                   
def groupAnagrams(self, strs):
        ans=[]
        for ele in strs:
            x="".join(sorted(ele))
            
            for i in ans:
                if i[len(i)-1]==x:
                    s=i.pop()
                    i.append(ele)
                    i.append(s)
                    break
            else:
                mini=[]
                mini.append(ele)
                mini.append(x)
                ans.append(mini)
        for i in ans:
            i.pop()
        return ans
# 27


# 28

# 29

# 30

# 31

# 32

# 33

# 34

# 35

# 36

# 37 

# 38

# 39

# 40
        
