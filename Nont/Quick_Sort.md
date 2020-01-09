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
    q_sort(q_list, 0, len(q_list)-1)


def q_sort(q_list, first, last):
    if first < last:
        split = partition(q_list, first, last)
        q_sort(q_list, first, split-1)
        q_sort(q_list, first+1, split)


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


q = Crate_Shuffle_List(30000)
print(q)

quick_sort(q)
print(q)
```
