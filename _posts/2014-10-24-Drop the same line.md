---
title: python去掉相同内容的行
date: 2014-10-24 17:47
status: public
thread: 0
categories: 日志
tags: python
---

同一文件中存在相同行的内容，而又不想出现相同行时的处理方式：
```python:n
lines_seen = set() 
outfile = open("4.txt", "w")
n=0
for line in open("3.txt", "r"):
    if line not in lines_seen: 
        outfile.write(line)
        lines_seen.add(line)
        n=n+1
outfile.close()
print n-1
```
另一种方法：
``` python:n
#--conding:utf-8--
a=[] #初始化要用到的列表a，用于记录原始行信息
b=[] #初始化要用到的列表b，用于记录结果数据，由两项构成。前一项为行信息如“小明：90”，后一项为该行对应的出现次数如2
f1=file("3.txt", "r") #打开1.txt文件
for line in f1:
    a.append(line) #将1.txt文件每一行作为一个元素，存入列表a
f1.close
 
for n in a: #遍历a中每一项（记为n），即1.txt中每一行
    flag=1
    for i in range(0,len(b)):
        if n == b[i][0]: #n与列表b中的每一项对比，如果有相等的：
            b[i][1]=b[i][1]+1 #那么对应的出现计数加1
            flag=0
            break
    if flag==1: #如果前面的比对没有一个相等的，即该行是第一次出现：
        b.append([n,1]) #那么在列表b中添加改行为新的一项
 
f2=file("5.txt", "w") #打开2.txt文件，用于输出
for n in b: #输出格式为：行信息 （tab） 出现次数 （回车）
    #f2.write(str(n[0][0:-1]) + "\t")
    f2.write(str(n[0][0:-1]) + "\n")
    #f2.write(str(n[1]) + "\n") 
f2.close
print "Finished" #完成
```