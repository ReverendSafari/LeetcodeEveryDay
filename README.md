# Leetcode Every Day
My interview prep journey! I am currently a rising senior at the new college of florida and I need to start applying to SE jobs this summer. I really want to be prepared if I can get any interviews so I am starting this repo to try and motivate myself to practice as much as possible.

My goal by the end of summer is to comfortably solve atleast HALF of the neetcode 150.

Wish me luck and follow below for my progress, solutions, struggles, and thoughts/strategies.

## 5/24/24 

Today I tried problem 66 - Plus One
I had made an attempt the other day in java but couldn't quite get it working for the third test case. However I want to focus more on python anyway so I tried again in python this morning and got a working solution in maybe about 30-40 minutes. I am pretty happy with this being my first real problem I have done without looking at a solution.

I think what I learned from this guy is that I am REALLY behind on my basic syntax in python, and am excited to get more solid with my fundamentals this summer. I am going to be solving all the problems from this point in python as well, no more switching around.

I will be posting the solution below

##### 66 - Plus One (Solution)

```
class Solution(object):

    def plusOne(self, digits):

        """

        :type digits: List[int]

        :rtype: List[int]

        """

        for index in range(len(digits) - 1, -1, -1):

            if (digits[index] < 9):

                digits[index]+= 1

                break

            else:

                digits[index] = 0

        if(digits[0] == 0):

            digits.insert(0, 1)

            return digits

        return digits
```

It runs in O(n) which I think is pretty good for this problem, Idk if one can get lower then that. I am gonna try two sum after this now that my array knowledge is coming back to me a little bit.

I ran into a TON of syntax errors along the way btw, my python has really gotten bad this past semester 

Link to solution -> https://leetcode.com/problems/plus-one/submissions/1266909934


##### Problem 1 - Two Sum

This is a problem near and dear to my heart, it was the first ever leetcode problem I ever attempted this fall. I think I was eventually able to get the O(n^2) nested for loop solution but I think I had to look at a solution to get the syntax right. So I hadn't really even solved it in the slow way in my head. I knew off the rip that there was some O(n) solution somehow using dictionaries but I wasn't quite sure how. Probably took me 20-30 minutes just to think of how I could possibly speed the solution up with hash maps and then another 20-25 to actually solve it. I was originally trying to use a dictionary conventionally and then realized it would make more sense to store the indexes as values instead of keys. (I think its the same time complexity either way but definitely more complex) 

Up at the top of the solution are just random thoughts I was writing down while trying to think through a possible solution

```
#Loop thru array and add all the numbers to dict
#Index is key value is value
#Dict get and inserts are constant
#Regular way is nested loops, how can hash map improve this?
#Loop one builds dictionary
#Loop two takes target - currentval and checks if that value exists in array
#and IS NOT the same index, and then if true returns both indexes

class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        valueDict = {}
        for index, item in enumerate(nums):
            valueDict[item] = index
        for index, item in enumerate(nums):
            searchFor = target - item
            if(searchFor in valueDict and valueDict[searchFor] != index):
                return [index, valueDict[searchFor]]
```

Link to solution -> https://leetcode.com/problems/two-sum/submissions/1266955763

I am going to try to work through the traditional neetcode path in a bfs kind of way and really take my time with each data structure.

##### Problem 242 - Valid Anagram

This one was def the easiest of the three today, total time to solve (had to google how to check if dict's were equal lol) was no more then 15 minutes, I would like to say maybe 10 with googling and everything

```
#Loop thru s, add letters to hashmap

#Loop thru t, add letters to hashmap

#Check if items and keys are equal??

class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        sDict = {}
        tDict = {}
        for letter in s:
            if (letter not in sDict):
                sDict[letter] = 1
            else:
                sDict[letter]+= 1

        for letter in t:
            if (letter not in tDict):
                tDict[letter] = 1
            else:
                tDict[letter]+= 1

        if (sDict == tDict):
            return True
        else:
            return False
```

This solution is O(n) which I think is probably the best time complexity although I could be wrong. I liked this one because it was easy :)

Link to solution -> https://leetcode.com/problems/valid-anagram/submissions/1266972132



## 5/26/24

##### Problem 217 - Contains Duplicate

I just started problem 217 - Contains Duplicate the other day and didn't get to finish it, my original idea below was just sorting it and then using two pointers (I think we may have talked about this problem in class for a minute in the past two years) I will put this solution below 

```
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        nums.sort()
        p1 = 0
        p2 = 1

        if (len(nums) < 2):
            return False
        else:
            while (p2 < len(nums)):
                if (nums[p1] == nums[p2]):
                    return True
                p1+=1
                p2+=1
```

This comes to a time complexity of O(nlogn) because its being capped by the sorting algorithm. However I realized after I could get a faster time just by using a hashmap. I think thats more ideal so I am putting that below.

```
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        countTable = {}
        for num in nums:
            if num in countTable:
                countTable[num]+=1
            else:
                countTable[num] = 0
        
        for values in countTable:
            if countTable[values] > 0:
                return True
        return False
```

I think this O(n) solution is probably the best. I am getting a little more used to these problems and my python skills are starting to come back to me a little bit. I am now done with all the EASY array problems in the first node of the neetcode branch. On to the MEDIUMS (Hope these wont kill me) but approaching mediums I am going to start looking at solutions if I am taking more then like 30 - 45 minutes to actually think of a solution (not necessarily solve it)

###### Note - Prefix Sum

I didn't learn about this school, but seems like a cool array algo 
Takes an array and creates a new array that contains the sum of the sequence of values that come before it

ie -
someArr = [1,3,2,2,4]
prefixSumArr = [1,4,6,8,12]


###### Problem 49 - Group Anagrams

My first EVER medium!!! I actually did better then I thought, Maybe took me 20-25 minutes to figure out the logic and then another 10 to actually program it (Rough estimates I was about an about while solving). Less scary then I originally thought although def took more thought then the other easy's. I originally wanted to put each string into a hash map to compare them like my regular anagram solution however, I halfway into coding it that this probably wouldn't be super efficient so I switched to sorting the anagrams instead. Def could have saved some space complexity but sweating it. 

```
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        #Sort anagrams
        sortedAnagrams = [''.join(sorted(string)) for string in strs]
        groupDict = {}
        outputArr = []

        for index, sortedString in enumerate(sortedAnagrams):
            if sortedString not in groupDict:
                groupDict[sortedString] = [strs[index]]
            else: 
                groupDict[sortedString].append(strs[index]) 
        
        for value in groupDict.values():
            outputArr.append(value)

        return outputArr
        
```

Solution -> https://leetcode.com/problems/group-anagrams/solutions/3687735/beats-100-c-java-python-beginner-friendly

Overall happy with my progress so far, with enough time I have been able to work through all the problems I have dealt with.

##### Problem 347 - Top K Frequent Elements +++

I solved this one in about 20ish minutes but DID NOT come up with best time complexity solution ! ! ! ! ! I think I needed to use a min heap or something but honestly lol I totally forgot how heaps even work so I would have never even gotten to that solution lol. Posting my current solution below but will revisit in the next few days to try and understand the better solution

```
# Just guessing but add all items to a hashmap
# Iterate through hashmap k times
# Each iteration pop the most frequent dict item and add it to return list
#

class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        frequencyDict = {}
        returnList = []

        for item in nums:
            if item not in frequencyDict:
                frequencyDict[item] = 1
            else:
                frequencyDict[item]+= 1
        
        while k > 0:
            maxValue = 0
            maxKey = 0
            for key, value in frequencyDict.items():
                if value > maxValue:
                    maxKey = key
                    maxValue = value
            returnList.append(maxKey)
            frequencyDict.pop(maxKey)
            maxValue = 0
            maxKey = 0
            k-= 1
        
        return returnList
                
```



## 8/5/24 MY BIG RETURN

It has been a minute since I have solved any problems! It has been very hectic this summer trying to balance my internship - responsibilities - and leetcode but I am locking back in for the end of summer and fall!

###### 128. Longest Consecutive Sequence

This one I had to use some help from neetcode but once I understood the concept I wrote the solution pretty quick, it was cool learning about a new data structure I hadn't used before.

```
#Create set
#Loop thru nums in array
#Check if the num is start of a sequence
#If it is, loop thru until you find the end, updating length and longest (if applicable)
# ** Hadn't used sets before, apparently it's like a tuple but can't have repeating values **
# ** Cool because it stops us from looking at repeating values, and has linear looksups because it uses a hashmap **

class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numsSet = set(nums)
        longestSeq = 0
        
        for num in nums:
            #check if it starts a sequence
            if (num - 1) not in numsSet:
                length = 1
                while (num + length) in numsSet:
                    length += 1
                if length > longestSeq:
                    longestSeq = length
        return longestSeq
```

Link -> https://leetcode.com/problems/longest-consecutive-sequence/submissions/1345877503

I think another reason I have been slacking is not wanting to use help when I am stuck, but honestly at this point if I waste less time when I am hardstuck and look at a tip or solution I will probably learn quicker in the long run


###### 238. Product of Array Except Self

This one was really tough for me, took some help to figure out the idea behind the solution and a long time to actually get the arrays and everything working. Really need to drill python fundamentals for sure

Once I complete the array section I am gonna try and resolve them all so hoping the next time around it all comes a bit easier.

```
#Okay so we could do it all with poor space complexity by calculating a prefix and postfix array
#And then multiplying those values to create the final array, but I guess if we want constant space 
#Then we calculate suffix's and shuv them in final array, and then calculate suffixes and multiply values
#Already in array to get final answer

class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        finalArray = [1] * len(nums)
        prefix = 1
        suffix = 1

        #Generate All the prefixes
        for index in range(len(nums)):
            finalArray[index] *= prefix
            prefix = prefix * nums[index]

        #Generate the suffixes & multiply against prefixes 
        for index in range(len(nums)-1,-1,-1):
            finalArray[index] *= suffix 
            suffix *= nums[index]

        return finalArray
```

Tough problem! But only two array problems left and then a resolve of K frequent elements and we are MOVING ON!!!!!! Lets go. I think goal wise I am really just trying to have the first half of the neetcode tree LOCKED DOWN, and beyond that is a bonus. I remember him saying in a video that the top of half of the tree makes up a BIG majority of questions asked.

##### 36. Valid Sudoku

This one has been on my mind for a while, because it is different from the other array problems. Of the bat given the finite array size, with this problem you aren't so concerned about time complexity. So it really all comes down to you being able to conceptualize it, and produce a solution.

I will say of the get go, that if there is one thing I am back at it's indexing arrays in loops properly. Always hard to do so, and I think I need to draw things out more so I can get a better mental image or something. Either way also solved with some assistance from Mr.Neetcode. But slay la vie, third problem of the day. I am happy and logging off leetcode to relax and play chess after this.

```
#Create empty 2d arrays for rows/cols/boxes
#Loop thru every index in the board
#Check if that cell value is repeating in any of the collections

class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """

        #Create empty list of sets
        rows = collections.defaultdict(set)
        columns = collections.defaultdict(set)
        boxes = collections.defaultdict(set)

        #Loop through cells
        for x in range(9):
            for y in range(9):
                cell = board[x][y]
                if cell == ".":
                    continue
                if cell in rows[x] or cell in columns[y] or cell in boxes[(x//3,y//3)]:
                    return False
                rows[x].add(cell)
                columns[y].add(cell)
                boxes[(x//3,y//3)].add(cell)
        return True
```

Link to solution -> https://leetcode.com/problems/valid-sudoku/submissions/1345939199

## 8/6 WE ARE SO BACK

Starting the day fresh by jumping into a TWO pointer problem, except my first solution didn't actually utilize two pointers lol

###### 125. Valid Palindrome

```
#Clean String
#Reverse
#Compare 

class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        cleanString = ""
        pointer = 0

        for char in s:
            if char.isalnum():
                cleanString += char
        
        cleanString = cleanString.lower()
        reverse = cleanString[::-1]

        if cleanString == reverse:
            return True
        return False
```

## 8/12/24 Back in florida!

Starting the day of strong with a STACK problem!

###### 20. Valid Parentheses

I had solved this in java a while ago but it took me a while to get back to the optimal solution in python I'm ngl. Feeling good though starting off a new problem category! Lol didn't realize a stack is just a list in python

Anywho's here my not super elegant python solution

```
#Loop through string, add any open brackets to a stack
#If we encounter a closed bracket then pop off stack and check for match
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        open = []

        if(len(s) % 2 != 0):
            return False

        for bracket in s:
            if (bracket == "{" or bracket == "[" or bracket == "("):
                open.append(bracket)
            else:
                if bracket == "]":
                    if len(open) == 0 or open.pop() != "[":
                        return False
                if bracket == "}":
                    if len(open) == 0 or open.pop() != "{":
                        return False
                if bracket == ")":
                    if len(open) == 0 or open.pop() != "(":
                        return False
            
        return (len(open) == 0)

```

Link to solution -> https://leetcode.com/problems/valid-parentheses/submissions/1353526765

## 8/13/2024

Finally forcing myself through these problems like I should be, I feel like when I get hung up on a problem I just wanna abandon it instead of seeing it through, but even if I rly don't wanna problem solve I think I need to start looking at help sooner. After all this is a memory plus problem solving deal not just problem solving.

###### 125. Valid Palindrome

This one was easy in concept with python, but I decided to avoid so many nice easy built in functions like isalnum to plan for the worst, after all it would suck to be an interview and have them tell me I NEED to figure it out instead of using built in's and getting totally lost.

Anywho's I present HER 

```
#Make two pointers
#Set them at left and right indexes
#Loop thru WHILE left is < right 
#Check that characters are equal (And skipping if it's a space)

class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        left = 0
        right = (len(s) - 1)


        while(left < right):
            while left < right and not self.isAlpha(s[left]):
                left += 1
            while left < right and not self.isAlpha(s[right]):
                right -= 1

            if s[left].lower() != s[right].lower():
                return False
            left += 1
            right -= 1

        return True
        
    def isAlpha(self, c):
        if (ord('0') <= ord(c) <= ord('9') or ord('A') <= ord(c) <= ord('Z') or ord('a') <= ord(c) <= ord('z')):
            return True
        return False
```


Link to solution -> https://leetcode.com/problems/valid-palindrome/submissions/1354372538

###### 167. Two Sum II

God leetcode frustration setting in on this one lol, super close to answer within 15 minutes but got stuck for a while and checked answer and my loop conditions were just out of order UGHHHHH, but lesson learned

```
#Two sum but we are returning an array with the indexes 
#Constant space so no extra dict, this FORCES us to use two pointers
#Left pointer right pointer, keep inc'ing right pointer until sum exceeds target THEN move left pointer


class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        l = 0
        r = len(numbers) - 1 
        
        while r < len(numbers):
            if numbers[l] + numbers[r] > target:
                r -= 1
            elif numbers[l] + numbers[r] < target:
                l += 1
            else: 
                return [l+1,r+1]
    
```

Link to solution -> https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/submissions/1354423634

###### 15. 3Sum

Ngl was feeling decent about this problem going in using some kind of psudo 2sum dict + a loop approach however could NOT get it working after a while and unlike the other problems after watching the neetcode video I still didn't have a full grasp on the solution. Def gotta come back to this soon and try again. My solution is basically neetcodes with one extra conditional

```

class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        triplets = []
        nums.sort()

        for index, num in enumerate(nums):
            if index > 0 and num == nums[index-1]:
                continue
            
            l,r = index + 1, len(nums) - 1
            while l < r:
                tresSum = num + nums[l] + nums[r]
                if tresSum > 0:
                    r -= 1
                elif tresSum < 0:
                    l += 1
                else:
                    someTriplet = [num, nums[l], nums[r]]
                    if someTriplet not in triplets:
                        triplets.append(someTriplet)
                    l += 1
                    while l == nums[l-1] and l != r:
                        l += 1

        return triplets

```

