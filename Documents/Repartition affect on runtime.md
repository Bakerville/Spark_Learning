![[images/2 partitions.png]]
The time when using 2 partitions in join transformation


![alt text](images/3%20Partition.png)
The time when using 3 partitions

![alt text](images/4%20Partition.png)
The time when using 4 partitions

![alt text](images/5%20Partition.png)
The time when using 4 partitions

![alt text](images/Time%20for%20each%20number%20partition.png)

```
The time for each number partition. As you see, The time down at 2 and 5. But it is not enough to claim that increasing number partions can decreased the time
```


![[Partition by CustomerKey.png]]

```
I ran the join transformation many times. I see the time of 1-5th run of using partitioning by CustomerKey is faster than not using repartion. But when run more times, these two measures are approximate.
```