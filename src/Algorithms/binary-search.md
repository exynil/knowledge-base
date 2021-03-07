# Бинарный поиск

~~~~
def binary_search(array, element):
    mid = 0
    start = 0
    end = len(array)

    while (start <= end):
        mid = (start + end) // 2

        if element == array[mid]:
            return mid

        if element < array[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return -1

my_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(binary_search(my_list, 3))
~~~~

### Хештеги: #бинарный_поиск #алгоритм