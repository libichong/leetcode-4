Question:Implement a regular expression matching. There are three special characters.

* means zero or more of previous characters
. means any single character
+ means one or more of previous characters


Sort a list of numbers in which each number is at a distance k from its actual position.



Rectangle: You have a plain with lots of rectangles on it, find out how many of them intersect.



Question:
Given a list of word and a target word, output all the words for each the edit distance with the target no greater than k.

e.g. [abc, abd, abcd, adc], target "ac", k = 1,

output = [abc, adc]

Naive Solution:
A naive solution would be, for each word in the list, calculate the edit distance with the target word. If it is equal or less than k, output to the result list. 

If we assume that the average length of the words is m, and the total number of words in the list is n, the total time complexity is O(n * m^2). 

A better solution with a trie:
The problem with the previous solution is if the given list of the words is like ab, abc, abcd, each time we need to repeatedly calculate the edit distance with the target word. If we can combine the prefix of all words together, we can save lots of time. 



实现一个mini parser, 输入是以下格式的string:"324" or"[123,456,[788,799,833],[[]],10,[]]"
要求输出:324 or [123,456,[788,799,833],[[]],10,[]].
也就是将字符串转换成对应的格式的数据.
输入一个数组的字符串, 要返回一个数组, 里面每一个元素是要么一个整数, 要么是一个数组.
但是注意数组可以多层嵌套. 


Airbnb: Decode string
Often, we want to encode raw IDs in our database by hiding them behind some
2-way decodeable hash. So, a URL which would have at one time been:
https://www.airbnb.com/rooms/848662
becomes
https://www.airbnb.com/rooms/kljJJ324hjkS_
We decode the ID kljJJ324hjkS_ to 848662 on our backend and serve the
relevant content. at some point, we start getting 404 errors from clients
requesting a certain URL of the form
https://www.airbnb.com/rooms/kljjj324hjks_
This can happen if certain clients, email services, or url shorteners "
sanitize" the url. Unfortunately, this change breaks decoding and the
resource cannot be found.
To assess how big of a deal this is, we may want to recover the IDs of the
targets that were 404ing.
Your task:
Given a method decode(testEncStr) which will return the decoded int id if
testEncStr is decodeable or will throw an exception or return null (
depending on the language) if not, implement a new method decodeFind(String
badEncStr) which takes a string and returns the decoded int id.


Airbnb: CSV Parser
/*
John,Smith,john.smith@gmail.com,Los Angeles,1
Jane,Roberts,janer@msn.com,"San Francisco, CA",0
"Alexandra ""Alex""",Menendez,alex.menendez@gmail.com,Miami,1
"""Alexandra Alex"""
John|Smith|john.smith@gmail.com|Los Angeles|1
Jane|Roberts|janer@msn.com|San Francisco, CA|0
Alexandra "Alex"|Menendez|alex.menendez@gmail.com|Miami|1
"Alexandra Alex"
*/
Understand the problem:
For this problem, there are several cases need to consider:
1. For comma, transform to |
2. If comma is inside a quote, don't treat the comma as separated. Remove the comma and print the entire token. e.g. "San Francisco, CA" => San Francisco, CA
3. If there are double quotes, remove one. e.g. "Alexandra ""Alex""" => Alexandra "Alex". 
Note that """Alexandra Alex""" becomes "Alexandra Alex" because we first remove the outer-most quote, and then remove one quote of the double quote.




Airbnb: Palindromic pair of a list of strings
Given a list of strings, find all the palindromic pairs of the string and output the concatenated palindrome.

e.g. [abc, cba], output is abccba, cbaabc.
e.g. [aabc, cb], output is cbaabc



Understand the problem:
The brute-force solution to this problem is very simple. For each word, we search all the others and see if it can form a palindrome. Assume that the ave. length of each word is m and there are totally n words in the list, the time complexity would be O(n^2 * m). 

Solution:
1. Put all the reversed order of the input string into a Map. The key is the reversed order of the string, and the value is the indices of the word
2. For each word, get all its prefixes, If the prefix is in the map AND the rest of the string is a palindrome, then we can find a pair where the first half is the current word, and the second half is the reversed order of prefix.
3. For each word, get all its postfixes. If the postfix is in the map AND the first half of the string is palindrome, then we can find a pair where the reversed order of the postfix is the first part, and the word is the second part of the pair. 

The reason why we need to track the position of each word is to avoid the situation like ["c"], i.e. the word itself is a palindrome. Then we may mistakely concatenate a "cc" as a palindrome. So we can concatenate two words IFF
1. The key in the map is different from the current word
2. If they are the same, they must have different indices. 



Airbnb: Maximum Room Days
给一个数组代表reservation request，suppose start date, end date back to back.
比如[5,1,1,5]代表如下预定：
Jul 1-Jul6
Jul6-Jul7
Jul7-Jul8
jul8-Jul13
当然最开始那个Jul 1是随便选就好的啦。
现在input的意义搞清楚了。还有一个限制，就是退房跟开始不能是同一天，比如如果接了Jul 1-Jul6，Jul6-Jul7就不能接了。那问题就是给你个数组，算算最多能把房子租出去多少天。这个例子的话就是10天。. 1point3acres.com/bbs
[4,9,6]=10. visit 1point3acres.com for more.

[4,10,3,1,5]=1

Understand the problem:
This problem is similar to the Leetcode House Robbery
http://buttercola.blogspot.com/2015/08/leetcode-house-robber.html





Implement a 2D iterator, with method next(), hasNext() and remove().


Understand the problem:
The question is close to the Leetcode Flatten 2D iterator. The only thing needs to take care is the remove() method. 

According to the definition of the remove(), 
Removes from the underlying collection the last element returned by this iterator (optional operation). This method can be called only once per call to next(). The behavior of an iterator is unspecified if the underlying collection is modified while the iteration is in progress in any way other than by calling this method.

So the remove() method actually removes the element returned from the next(). 
To safely remove from a collection while iterating over it you should use an Iterator.



