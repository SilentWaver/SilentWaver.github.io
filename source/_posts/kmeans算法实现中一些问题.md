---
title: kmeans算法实现中一些问题
date: 2020-11-22
---

本来，是没打算写一篇文的

然后发现自己写的代码计算出的平均准确度是错误的

然后我就疯了

<!-- more -->

我本计划通过比较保留数据集自带的标签与划分后的标签来判断精度，但是程序划分出的标签完全乱套了，无法确定哪个簇是哪个簇。

硬改应该也能改出来，但只能适用于单个数据集，如何改成具有泛用性的代码，莫得头绪。  
以下是我的源码，没什么必要看，我也放上了

```python
 # coding=utf-8
from numpy import *
import time
import xlwt
from xlrd import open_workbook
from xlutils.copy import copy
import math

listA = [] 
        
def distE(vecA,vecB):
    return sqrt(sum(power(vecA-vecB,2)))

def loadData(filename,n):
    dataMat = []
    fr = open(filename)
    for line in fr.readlines():
        curLine = line.strip('\n').split(',')
        temp=curLine[0]
        del curLine[0]
        listA.append(temp)
        #listA.append(curLine)
        fltLine = list(map(float,curLine))
        dataMat.append(fltLine)
    return dataMat

def randCent(dataSet, k):
    n = shape(dataSet)[1]
    centroids = mat(zeros((k,n)))   
    for j in range(n):
        minJ = min(dataSet[:,j]) 
        maxJ = max(dataSet[:,j])
        rangeJ = float(maxJ - minJ)
        centroids[:,j] = minJ + rangeJ * random.rand(k, 1)
    return centroids

def kMeans(dataSet, k, distMeans =distE, createCent = randCent):
    m = shape(dataSet)[0]
    clusterAssment = mat(zeros((m,2)))    
    centroids = createCent(dataSet, k)
    clusterChanged = True   
    while clusterChanged:
        clusterChanged = False;
        for i in range(m):  
            minDist = inf; minIndex = -1;
            for j in range(k):
                distJI = distMeans(centroids[j,:], dataSet[i,:])
                if distJI < minDist:
                    minDist = distJI; minIndex = j  
            if clusterAssment[i,0] != minIndex: clusterChanged = True; 
            clusterAssment[i,:] = minIndex,minDist**2   
        #print(centroids)
        for cent in range(k):   
            ptsInClust = dataSet[nonzero(clusterAssment[:,0].A == cent)[0]]   
            centroids[cent,:] = mean(ptsInClust, axis = 0) 
    return centroids, clusterAssment
 
def accCalu(clus):
    global listA
    mable=[]
    acc = 0
    n=0
    total = len(listA)
    listA=list(map(int,listA))
    for i in clus:
        if isinstance(i, list):
            mable.append(int(i[0])+1)  
    for j in mable:
        if j == listA[n]:
            acc=acc+1
        n=n+1
    #print('准确度: {:.2f}%'.format((acc/total)*100))
    print(mable)
    print(clus)
    return (acc/total)*100       



datMat = mat(loadData('Ecoli.txt',8))
cnt_times=1
TStime = time.time()
TaccA = 0  
while (1): 
    starttime = time.time()   
    myCentroids,clustAssing = kMeans(datMat,8)
    endtime = time.time()
    dtime = endtime - starttime
    accA = accCalu(clustAssing.tolist())
    listR=[]
    listR.append([accA,dtime])
    TaccA += accA
    
    
    
    cnt_times+=1
    if(cnt_times>1):
        break
    
    
TEtime = time.time()
TDtime = TEtime - TStime
print('平均准确度: {:.2f}%'  .format(TaccA/100))
print("总训练时间：%.8s s" % TDtime)


```

