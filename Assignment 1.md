# Assignment 1



## 1. Flowchart
```python
import random

def Get_value(x, y, z):
    print("We get the value = {}.".format(x+y-10*z))
def Print_values(a, b, c):
    print("a={} b={} c={}".format(a,b,c))
    if (a > b):
        if(b > c):
            Get_value(a, b, c)
        else:
            if (a > c):
                Get_value(a, c, b)
            else:
                Get_value(c, a, b)
    else:
        if (b > c):
            if (a > c):
                Get_value(b, a, c)
            else:
                Get_value(b, c, a)
        else:
            Get_value(c, b, a)

def main():
    a = round(random.random()*10)
    b = round(random.random()*10)
    c = round(random.random()*10)
    Print_values(a, b, c)
    a,b,c = 10,5,1
    Print_values(a, b, c)
    
    
if __name__ == '__main__':
    main()
```

### Output :

![image-20221001221758986](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001221758986.png)


## 2. Continuous celing function
```python
from math import ceil

def Get_fx(x):
    if(x != 1):
        return(Get_fx(ceil(x/3)) + 2*x)
    else:
        return 1
    
def main():
    n = eval(input("Please input your list number(>0):"))
    i = 0
    x_lst = []
    answer_lst = []
    while(i < n):
        x = eval(input("Please input you number:"))
        x_lst.append(x)
        i = i + 1
    
    print("Your number list is :")
    for i in x_lst:
        answer = Get_fx(i)
        answer_lst.append(answer)
        print(i, end = " ")
    print() # get a blank line
    print("Your answer list is :")
    for i in answer_lst:
        print(i, end = " ")
    

if __name__ == '__main__':
    main()
```
### Output :

![image-20221001221901763](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001221901763.png)

First we define a function get the $f(x) = f(ceil(x/3)) + 2x,(f(1) = 1)$, then we get input list(let user input the list size and number). When we input a list [1, 6， 88, 22, 16, 3, 5, 77, 49], we get the answer list [1, 17, 269, 67, 49, 7,15, 231, 205 ]



## 3. Dice rollint

### 3.1

```python
import random

def go_or_not(x,face_sum,count):
    remain_sum = x - face_sum
    remain_count = 10 - count
    if (remain_count * 6 < remain_sum):
        return False
    elif (remain_count > remain_sum):
        return False
    else:
        return True

def Find_number_of_ways(x):
    
    Face = [1,2,3,4,5,6]
    face_sum = 0
    count = 0
    ways = 0
    for dice1 in range(1, 7):
        face_sum = dice1
        count = 1
        if(not go_or_not(x,face_sum,count)):
            face_sum -= dice1
            count -= 1
            continue
        for dice2 in range(1,7):
            face_sum = dice2 + dice1
            count = 2
            if(not go_or_not(x,face_sum,count)):
                face_sum -= dice2
                count -= 1
                continue
            for dice3 in range(1,7):
                face_sum = dice3 + dice2 + dice1
                count = 3
                if(not go_or_not(x,face_sum,count)):
                    face_sum -= dice3
                    count -= 1
                    continue
                for dice4 in range(1,7):
                    face_sum = dice4 + dice3 + dice2 + dice1
                    count = 4
                    if(not go_or_not(x,face_sum,count)):
                        face_sum -= dice4
                        count -= 1
                        continue
                    for dice5 in range(1,7):
                        face_sum = dice5 + dice4 + dice3 + dice2 + dice1
                        count = 5
                        if(not go_or_not(x,face_sum,count)):
                            face_sum -= dice5
                            count -= 1
                            continue
                        for dice6 in range(1,7):
                            face_sum = dice6 + dice5 + dice4 + dice3 + dice2 + dice1
                            count = 6
                            if(not go_or_not(x,face_sum,count)):
                                face_sum -= dice6
                                count -= 1
                                continue
                            for dice7 in range(1,7):
                                face_sum = dice7 + dice6 + dice5 + dice4 + dice3 + dice2 + dice1
                                count = 7
                                if(not go_or_not(x,face_sum,count)):
                                    continue
                                for dice8 in range(1,7):
                                    face_sum = dice8 + dice7 + dice6 + dice5 + dice4 + dice3 + dice2 + dice1
                                    count = 8
                                    if(not go_or_not(x,face_sum,count)):
                                        continue
                                    for dice9 in range(1,7):
                                        face_sum = dice9 + dice8 + dice7 + dice6 + dice5 + dice4 + dice3 + dice2 + dice1 
                                        count = 9
                                        if(not go_or_not(x,face_sum,count)):
                                            continue
                                        for dice10 in range(1,7):
                                            face_sum = dice10 + dice9 +dice8 + dice7 + dice6 + dice5 + dice4 + dice3 + dice2 + dice1
                                            if(face_sum == x):
                                                face_sum = 0
                                                count = 0
                                                ways += 1
                                                break
                                            else:
                                                face_sum -= dice10
                                                count -= 1
                                                
    return ways
```

We use the traversal method to obtain possible results, but we have 6^10^ possibilities, it's too big to computer all possibilities. So we define a function ==go_or_not== to judge whether to continue.

### 3.2 

Then we add some code to get ==Number_of_ways== 

```python
def main():
    Number_of_ways = []
    for number in range(10,61):
        ways = Find_number_of_ways(number)
        Number_of_ways.append(ways)
    print(Number_of_ways)
    max_value = 0
    max_num = 0
    for i in range(len(Number_of_ways)):
        if(Number_of_ways[i] > max_value):
            max_value = Number_of_ways[i]
            max_num = i
    x = 10 + max_num
    print("x = {}".format(x))
    
if __name__ == '__main__':
    main()
```

### Output :

![image-20221001211504129](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001211504129.png)



## 4. Dynamic programmint

### 4.1

```python
import random

def Random_integer(N):
    lst = []
    for i in range(N):
        lst.append(round(random.random()*10))
    return lst
```

### 4.2

```python
def Get_average(lst):
    lst_sum = 0
    lst_count = len(lst)
    for i in lst:
        lst_sum += i
    return lst_sum/lst_count

def Sum_averages(lst):
    lst_len = len(lst)
    i = 1
    sum_average = []
    while (i <= lst_len):
        #print("get {} element(s) list: ".format(i))
        index = 0
        while(index + i <= lst_len):
            #print(lst[index:index+i], end = " ")
            average = Get_average(lst[index:index+i])
            sum_average.append(average)
            #print("average = {}".format(average), end = " ")
            index += 1
        #print()
        i += 1
    return sum(sum_average)
```

We define a function ==Get_average== to get average of list.

### 4.3

We add some codes to get a list called  ==Total_sum_averages== and plot ==Total_sum_averages==.

```python
import matplotlib.pyplot as plt
%matplotlib inline

def main():
#     lst1 = Random_integer(10)
#     print("Your list is :")
#     print(lst1)
#     Sum_averages(lst1)
    N_lst = []
    Total_sum_averages = []
    for i in range(1, 101):
        N_lst.append(i)
        Total_sum_averages.append(Sum_averages(Random_integer(i)))
    print(N_lst)
    print(Total_sum_averages)
    fig = plt.figure(figsize = (12,8),
                    )
    ax = fig.add_subplot(111)
    ax = fig.add_axes([0,0,1,1])
    ax.plot(N_lst, Total_sum_averages)
    ax.set_title("Assignment_01 number4")
    ax.set_xlabel("x")
    ax.set_ylabel("sum_averages")
        
    
if __name__ == '__main__':
    main()
```

### Output :

![image-20221001222533266](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001222533266.png)

![image-20221001222552228](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001222552228.png)

We can see that the sum of the average values of all subsets increase with the increase of the array capacity.

## 5. Path counting

### 5.1

```python
import numpy as np

def Get_matrix(N, M):
    a = np.random.choice(a = [0,1], size = [N,M])
    a[0][0] = 1
    a[-1][-1] = 1
    return a
```

### 5.2

```python
import numpy as np

def Get_matrix(N, M):
    a = np.random.choice(a = [0,1], size = [N,M])
    a[0][0] = 1
    a[-1][-1] = 1
    return a

path = 0
okay = 0
def Count_path(Matrix,x,y,endx,endy):
    global path
    global okay
    
    if (okay == 1):
        return path
    
    if(x == endx and y == endy):
        okay = 1
        print("find ways")
        print("path = {}".format(path))
        return path
    
    if(y != endy and Matrix[x][y+1] != 0 and okay!=1):
        print("right")
        path += 1
        Move(Matrix,x,y+1,endx,endy)
    if (okay == 1):
        return path
    
    if(x != endx and Matrix[x+1][y] != 0 and okay!=1):
        print("down")
        path += 1
        Move(Matrix,x+1 ,y,endx,endy)
    if (okay == 1):
        return path 
    
    if (okay == 0):
        print("no way")
        path -= 1
        return 0
    
    
a = Get_matrix(3,3)
print(a)
Count_path(a,0,0,2,2)
if(not okay):
    print("path = 0");
```

#### 5.2 Output :

situation01 :

![image-20221001212355632](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001212355632.png)

situation02 :

![image-20221001212622835](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001212622835.png)

### 5.3

```python
import numpy as np

def Get_matrix(N, M):
    a = np.random.choice(a = [0,1], size = [N,M])
    a[0][0] = 1
    a[-1][-1] = 1
    return a

path = 0
okay = 0
def Count_path(Matrix,x,y,endx,endy):
    global path
    global okay

    if (okay == 1):
        return path

    if(x == endx and y == endy):
        okay = 1
        print("find ways")
        print("path = {}".format(path))
        return path

    if(y != endy and Matrix[x][y+1] != 0 and okay!=1):
        #print("right")
        path += 1
        Count_path(Matrix,x,y+1,endx,endy)
    if (okay == 1):
        return path

    if(x != endx and Matrix[x+1][y] != 0 and okay!=1):
        #print("down")
        path += 1
        Count_path(Matrix,x+1 ,y,endx,endy)
    if (okay == 1):
        return path 

    if (okay == 0):
        #print("no way")
        path -= 1
        return 0

def main():
    global path
    global okay
    N = 10
    M = 8
    path_lst = []
    for i in range(1000):
        a = Get_matrix(N,M)
        path_ans = Count_path(a,0,0,N-1,M-1)
        path_lst.append(path_ans);
        if(okay):
            print(a)
        path = 0
        okay = 0
    print(path_lst)
    total_num = sum(path_lst)
    print(total_num)
        


if __name__ == '__main__':
    main()
```



### Output :

![image-20221001222738863](C:\Users\ljn\AppData\Roaming\Typora\typora-user-images\image-20221001222738863.png)



