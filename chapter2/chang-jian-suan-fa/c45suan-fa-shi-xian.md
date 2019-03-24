# C4.5算法实现

基于ID3算法，

```python
def chooseBestFeatureToSplit(dataSet):
        numFeatures = len(dataSet[0]) - 1 
        baseEntropy = calcShannonEnt(dataSet)
        bestInfoGainRate = 0.0
        bestFeature = -1
        for i in range(numFeatures):
                featList = [example[i] for example in dataSet]
                uniqueVals = set(featList)
                newEntropy = 0.0
              
                for value in uniqueVals:
                        subDataSet = splitDataSet(dataSet, i, value)
                        prob = len(subDataSet) / float(len(dataSet))
                        newEntropy += prob *calcShannonEnt(subDataSet) 
                
                infoGain = baseEntropy - newEntropy
                iv = calcShannonEnt(dataSet)
                if(iv == 0): 
                        continue
                infoGainRate = infoGain / iv
                print(infoGain)
                if infoGainRate > bestInfoGainRate:
                        bestInfoGainRate = infoGainRate
                        bestFeature = i
       
        return bestFeature
```

