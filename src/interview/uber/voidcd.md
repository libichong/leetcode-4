1.电面是一个美国小哥，开始聊了聊简历之后给了一道系统设计题，设计一个Service可以输入用户location查询附近的公交站台和所有即将到这些站台的公交车。我随便和他扯了一些系统设计的还有优化算法之类的东西，后来让我写一个控制访问API频率（Ratelimit）的function， 用了一个Queue写完就结束了。 
solution 
google实现的guava rate limiter 
附近的位置可以用Geohash，车维持一个circular linkedlist，因为新发一辆车、超车会导致insertion，事故导致deletion 
ratelimit function: blockingqueue + synchronized + sleep 
比如控制10次每秒，request存在blockingqueue里，然后维持一个count (多个server就要synchronized)，然后count等于10 sleep一秒

Onsite： 到公司recruiter带我到了uber拐角的一个小会议室就开始面试了，Uber公司看起来还是很不错的。四轮面试： 
第一个人 ： 让我设计一个 Netflix， follow up 很多 比如如何限制同一个用户多处登录不能同时看一个资源，如何实现根据用户的网速调整清晰度，怎么热门推荐等等。 
第二个人 ： 进来直接不闲聊直接让我打开自己电脑开始写一些代码，设计一个 Excel ， 每个cell里面是一个String。 一开始想当然说可以直接用二维矩阵存，后来改成list of lists， 最后改成了HashMap。后续还有evaluate一个string相关的问题（给了黑盒evaluate函数，对每个cell实现evaluate和支持修改）。 
第三个人 ： 纯聊简历，干聊project，面试官没有准备一道题，到最后我就已经是在找话说了。 
第四个人 ： 好像是个小领导，先问了问我有没有问题，后来问了一些知识点问题，python有哪些语言特性等等之类的。 
最后recruiter总结问我觉得怎么样，我说觉得很好我很喜欢uber，问我如果给我offer我能不能很快接受，I said yes。

2.两个面试官都是国人大哥 
mirror tree， uber电面是要compile的，不像其他的，写写算法就行，之前没意识到, 
solution 
TreeNode mirror(root) 
node=copy(root); 
node.left=mirror(root.right); 
node.right=mirror(root.left); 
return node;

design，shortened url

3.电面通过Skype进行，面试官是一个Dev manager。 
如何实现Asynchronous service call？如何retry？讨论了一下Service oriented architecture的好处和弊端。 
solution: callback+multithread, retry 就再加一个thread

第一轮：系统设计问题 How to design netflix?

这个其实小编也不太了解，就尽量根据自己之前看过的资料开始一步一步给出自己的Solution，然后进行优化。架构上：基本上就是数据层，Service层，前端。因为小编知道Netflix是AWS的忠实用户，所以基本就以AWS为例：数据存储使用s3，配合Relational db / Non sql database；然后是Service layer，功能包括：User authentication，session management，data streaming and other business logic；前台则主要是用户界面。优化包括：如何Cache，如何利用CDN network replicate data close to the users. 因为Netflix的数据大部分是静态数据，很少更新，电影电视剧的内容完全可以Replicate很多份放到Internet的Edge server上。

第二轮：Deep dive personal project.

聊过去的项目，这种类型的面试真的是因人而异，以下是小编对它的理解：Project在技术上要Impressive，如果你能让面试官认可Project的架构设计甚至从你的Project里学到东西，他肯定会希望和你成为同事，这是面试中很重要的一个标准。在日常工作中，每个人都要和组员或者公司其他员工交流沟通很多，如果面试官发现很难和你交流、或者很难理解你的话，过关的几率会大大下降。所以这轮面试的重点就是测试面试者是否有能力进行有效的交流沟通，从面试官的角度，以后愿不愿意Work on something together。

Baozi Tip

因为这类面试通常是自己准备话题，所以可以提前找好朋友多Mock interview几次，这样子可以确保真正面试的时候可以说的有条理，有主有细。

第三轮：Behavior question / Cultural fit面试。

这一轮面试基本和HR Recruiter的那轮差不多，区别就是这次时间更长，想象一下45分钟全是Behavior question，面对面。小编个人觉得这一轮真的就是看前期的准备工作是不是到位：最起码要使用几次面试公司的产品，最好发现一些需要改进的地方，能说清楚产品的优点，大体了解公司的愿景，潜在的客户群体。然后尽量多关注关于公司的报道，记得当时Uber刚刚在纽约Launch delivery service，所以当小编跟面试官提到的时候，可以明显感觉到她是很高兴的。

第四轮：Coding + OO design (Design windows excel)

这个主要是看OO design的功底，其实不难。Follow-up question: In excel, one cell can refer to other cells, if I update one cell, how do you update all the dependent cells？这个问题可以被转化成经典的Topological sort，所以这里就不详细展开啦，如果不知道可以看看算法书，或者关注包子博客之后的总结

4.只有一道，电话combination那道，算法很熟悉了，dfs，不过好长时间没做，边think aloud 边码，还算顺利. 
让自己弄几个test case 跑跑，但没有一次bug free，忘了考虑0，1的case ＝＝还有关于unsigned int 的warning 
接着聊了聊怎么 code review，加一些comments啊什么的

5.计算表达式 1+2*3+4 = 11 
这里一般都会用空格来当delimiter 
solution 
use two arrays to store numbers and signs. 
nums = [1,2,3,4] 
signs = [+, *, +]. visit 1point3acres.com for more.

scan signs, when we meet * or /, and change * or / into +, corresponding nums changed to [0, a*b or [0, a/b]. for the example:

nums = [1,0,6,4]. 
signs = [+,+,+] 
then do (zigzag) sum.

6. 
1). 给定一个string，判断能否用这个string来组成一个palindrome。e.g. ‘uber’ –> False, ‘aab’ –> True, ‘carecra’ –> True. 
Follow up: 给出所有能够组成的palindrome，因为时间原因可以不用担心duplicates。（potential follow up就是去重了） 
solution 
odd的char最多一个. follow up可以选出一半做permutation,然后加上落单的(if exists)和reverse, 
2).白人小哥很nice，第二题就是permutation

7.刚刚面完二面，发面经攒人品 
一面 
烙印面的，同Word Ladder ii 
由于一直没写过，看到我就疯了，磕磕碰碰写了个大概，烙印估计也看出来我没写过，但是思路对，就加面了一次 
二面. 
1 Anagram 需要自己写很多test case 
2 实现google搜索的自动补全，以及备选短语的ranking，我用trie做的

8. 
1)给一个String array，找出每个元素的Anagram，按照相同的anagram分为一组，最后输出每一组元素。 
我用了HashMap<String, ArrayList<String>>来做的，在计算key的时候，需要按字母顺序sort String作为key， 
于是follow up就是怎么不用sort，于是我就说可以把每一个string统计一下a,b,c。。。的频率，然后输出一个pattern a1b3c4。 
把这个pattern作为map的key。 
2)问当你用browser打开www.uber.com的时候，发生了生么。 
Solution dns查找ip，然后发送http request到这个ip，server收到request并return html，browser rendering the page

9. 
1)问了什么是RPC, 怎么实现的. 
solution 
remote procedure call 流程, client/server mode

client: local call->pack args->transmit call packet to server
server: receive packet->unpack-> call,work, return -> pack result->transmit packet to client
client: receive packet->unpack->local return
2)Linux的file system的结构, 最后让我自己设计一个结构可以存很大的file 
solution 
linux把硬盘分成3个区: 目录项(英文dentry, 包含文件名和inode号)， inode table(w/r属性，data block指针)，data block 
3)接下来是算法题: 有一个很长的list<pair<int, int> >第一个int 的这个node的序号，第二个int 是这个node 的weight。 写一个函数返回node的序号， 比如： 
(2, 3)->(3, 5)->(1, 7). 那么返回2的概率是（3／15）， 3的概率是：（5／15），1 的概率 
solution binary search? brute force?

10.问题是统计backtraces。 
给一个1000行的文件。每一行是一个String数组，表示一个backtrace，例如 
[“main”, “fun1”, “fun2”]. 
[“main”,” “fun1”, “fun3”,”fun4”] 
[“main”,”fun5”] 
[“main”] 
[“main”,”fun5”,”fun6”]. more info on 1point3acres.com 
第一行表示一个函数调用关系main->fun1->fun2，其他类似。显然每一行的第0个元素必然是main。最后统计出每一个function的调用次数和调用关系，例如这个例子的输出是： 
main 5 
fun1 2 
fun2 1 
fun3 1 
fun4 1 
fun5 2 
fun6 1 
调用关系用indent表示出来，每多调用一层就多一个tab。 
实现就是写一个树的节点类，每一个点表示一个函数，储存它的函数名和调用次数的count，孩子存在一个HashMap里，Key是孩子的函数名

public Class Node{
    public Stirng name;
    public int count;

}
public HashMap<String, Node> children;
最后打印的部分没时间写了，就口头讲了一下打印的顺序，从main开始，每多一层递归就多打一个tab，讲着讲着发现其实就是dfs，面试官说OK，dfs能work。因为没写完也没跑test case。 
solution看题意应该同一个func不能出现在2个不同的层

11.一个已经实现好了的API，只要输入一个站名，就可以输出来此站的所有公交线路的信息。问你设计一个interface，输出最近要来的公交车的下一站。 
然后慢慢问问题，逐渐把问题缩小成为找离现在时间点最近的下一个公交到站时间点。 
继续问问题，把API的输出理解为已经按时间点排好序，OK，典型的find element in sorted array。提供两种解法，duang duang duang写出来~

12.电面 
给一串direction, 比如A N C 意味着A在C的北边。写一个function验证这些direction 
是否valid 
Note：A N C, A NE C同时出现是合法的 
例子：下面这个不合法，因为A N C, C NE D所以不可能A S D 
A N C 
B NE C 
C NE D 
A S D 
B W A 
solution x,y 分别建有向图，判断是否有环

设计实现 excel,最基本的就是数据结构和实现Put和Get. 先解释清楚, 最后code. 
Follow up 就是涉及到一个cell可能包含其他cell的pointer的时候, 如何获取这个cell的值. 紧接着更新一个cell如何保证所有指向它的cell也能更新. 
solution 
实现 GET, SET，不用map<Position, Cell> 用hashmap<Integer, hashmap<Integer, Cell>,方便按行列遍历。 follow up 用有向图就可以