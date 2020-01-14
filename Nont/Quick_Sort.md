优秀文章:   
- [选择排序-冒泡-插入-快排](https://github.com/JiongXing/JXSort)  

快速排序算法:  
```Python
def Crate_Shuffle_List(max_num):
    from random import shuffle
    q_list = list()
    for i in range(max_num):
        q_list.append(i)
    shuffle(q_list)
    return q_list


def quick_sort(q_list):
    q_sort(q_list, 0, len(q_list) - 1)


def q_sort(q_list, first, last):
    if first < last:
        split = partition(q_list, first, last)
        q_sort(q_list, first, split - 1)
        q_sort(q_list, split + 1, last)


def partition(q_list, first, last):
    PIVOT = q_list[first]
    left_mark = first + 1
    right_mark = last
    while True:
        while q_list[left_mark] <= PIVOT:
            if left_mark == right_mark:
                break
            left_mark += 1
        while q_list[right_mark] > PIVOT:
            right_mark -= 1
		
            if left_mark < right_mark:
                q_list[left_mark], q_list[right_mark] = q_list[right_mark], q_list[left_mark]
            else:
                break
    q_list[first], q_list[right_mark] = q_list[right_mark], q_list[first]
    return right_mark


if __name__ == "__main__":
    q = Crate_Shuffle_List(30)
    print(q)

    quick_sort(q)
    print(q)
```

#  另外一种更高效的递归
```Python
import time
start = time.time()

def quicksort(arr):
    if len(arr) <= 1:
        return arr
    PIVOT  = arr[len(arr) // 2]
    left   = [x for x in arr if x < PIVOT]
    middle = [x for x in arr if x == PIVOT]
    right  = [x for x in arr if x > PIVOT]
    return quicksort(left) + middle + quicksort(right)
    
def Crate_Shuffle_List(max_num):
    from random import shuffle
    q_list = list()
    for i in range(max_num):
        q_list.append(i)
    shuffle(q_list)
    return q_list

#q = [3, 5, 8, 1, 2, 9, 4, 7, 6]
q = Crate_Shuffle_List(10)
print(quicksort(q))

end = time.time()
print('程序运行时间: ', end-start)
```


