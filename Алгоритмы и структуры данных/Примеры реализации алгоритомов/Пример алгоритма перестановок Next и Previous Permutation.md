
```python
def next_smaller(n):
    n = list(str(n))
    pivot_idx = -1

    # 1. Найти pivot (где порядок нарушается)
    for i in range(len(n)-2, -1, -1):
        if int(n[i]) > int(n[i+1]):
            pivot_idx = i
            break

    if pivot_idx == -1:
        return -1

    # 2. Найти справа наибольшую цифру, которая меньше pivot
    max_smaller_idx = -1
    for j in range(len(n)-1, pivot_idx, -1):
        if int(n[j]) < int(n[pivot_idx]):
            if max_smaller_idx == -1 or int(n[j]) > int(n[max_smaller_idx]):
                max_smaller_idx = j

    # 3. Swap
    n[pivot_idx], n[max_smaller_idx] = n[max_smaller_idx], n[pivot_idx]

    # 4. Хвост по убыванию
    right_side = sorted(n[pivot_idx+1:], reverse=True)
    left_side = n[:pivot_idx+1]

    if left_side[0] == "0":  # ведущий ноль
        return -1

    return int("".join(left_side + right_side))

```

```python
def next_permutation(arr):
    arr = list(arr)
    pivot = -1

    # 1. Найти pivot
    for i in range(len(arr)-2, -1, -1):
        if arr[i] < arr[i+1]:
            pivot = i
            break
    if pivot == -1:
        return None  # последняя перестановка

    # 2. Найти кандидата
    candidate = -1
    for j in range(len(arr)-1, pivot, -1):
        if arr[j] > arr[pivot]:
            candidate = j
            break

    # 3. Swap
    arr[pivot], arr[candidate] = arr[candidate], arr[pivot]

    # 4. Хвост по возрастанию
    arr[pivot+1:] = reversed(arr[pivot+1:])
    return arr

```

Причина в том, что мы хотим получить **ближайшее** число:

- 🔹 **Next (большее)**:  
    после обмена pivot и кандидата хвост нужно сделать **минимальным**, чтобы число стало **как можно меньше, но всё равно больше исходного** → поэтому **сортируем хвост по возрастанию**.
    
- 🔹 **Previous (меньшее)**:  
    после обмена pivot и кандидата хвост нужно сделать **максимальным**, чтобы число стало **как можно больше, но всё равно меньше исходного** → поэтому **сортируем хвост по убыванию**.