# Best Time to Buy and Sell Stock

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.


## Brute force :

run two loops and find the profit for each element from all the element and return the maxprofit 

### code :

```java
class Solution {
    public int maxProfit(int[] prices) {

        int maxprofit = 0;

        for(int i=0;i<prices.length;i++){
            for(int j=i+1;j<prices.length;j++){
                maxprofit = Math.max(maxprofit,prices[j]-prices[i]);
            }
        }

        return maxprofit;
        
    }
}
```

### Complexity :

* time complexity = O(n^2)
* space complexity :  o(1)


## Optimal approach :

keep tarck of the min element seen so far and find the profit betwwen the current element and minprice and return the maxprofit

### code :

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minprice = Integer.MAX_VALUE;

        int maxprofit = 0;

        for(int i=0;i<prices.length;i++){

            if(prices[i] < minprice){
                minprice = prices[i];
            }
            else{
                maxprofit = Math.max(maxprofit,prices[i]-minprice);
            }


        }

        return maxprofit;
    }
}

```

### complexity :

* time complexity : o(n)
* space complexity : o(1)
