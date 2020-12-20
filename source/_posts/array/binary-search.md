---
title: Binary Search (Dễ)
date: 2020-12-20 12:57:15
tags:
categories:
  - [Thuật toán, Mảng]
---

### Đề bài

Viết thuật toán tìm một phần tử trong mảng đã được sắp xếp

**Input**:
Một mảng arrA đã được sắp xếp và một key

**Output**: Trả về true nếu tìm thấy, false nếu không tìm thấy

**Phương pháp**: Ý tưởng ở đây là so sánh các phần tử ở giữa mảng với key được cho. Nếu key bằng với một phần tử ở giữa thì ta tìm thấy, trả về true. Nếu key lớn hơn phần tử ở giữa mảng, cắt nửa đầu của mảng, khi bạn không tìm thấy phần tử ở nữa trước của mảng thì thực hiện đệ quy tìm ở phần còn lại và ngược lại.

```
if key == mid_element:
   return True
elif (mid_element > key):
   # Thực hiện đệ quy tìm kiếm nửa bên trái của mảng
else:
   # Thực hiện đệ quy tìm kiếm nửa bên phải
```

![Mô phỏng đệ Binary Search](https://i1.wp.com/algorithms.tutorialhorizon.com/files/2014/07/Binary-Search1.png?w=717&ssl=1)

Code mẫu

```python
def search(arrA, start, end, key):
    if start > end:
        return False

    mid = start + int(((end - start) / 2))
    print(mid)
    if arrA[mid] == key:
        return True
    elif arrA[mid] > key:
        return search(arrA, start, mid -1 , key)
    else:
        return search(arrA, mid + 1, end, key)


def main():
    a = [2, 5, 8, 10, 14, 44, 77, 78, 99]
    number = 99
    print(search(a, 0, len(a) - 1, number))

    number = 76
    print(search(a, 0, len(a) - 1, number))

main()
```
