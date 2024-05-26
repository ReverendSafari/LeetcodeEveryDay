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

