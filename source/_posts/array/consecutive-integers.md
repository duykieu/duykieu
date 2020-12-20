---
title: Kiểm tra mảng là các số nguyên liên tiếp (Dễ)
date: 2020-12-20 17:57:15
tags:
categories:
  - [Thuật toán, Mảng]
---

## Đề bài

Cho một mảng các số nguyên chưa sắp xếp, kiểm tra xem mảng trên có phải là mảng số nguyên liên tiếp hay không

## Ví dụ

```
arrA = [21, 24, 22, 26, 23, 25] => True
(Các số nguyên liên tiếp từ 21 - 26)

arrB = [11, 10, 12, 14, 13] => True
(Các số nguyên liên tiếp từ 10 - 14)

arrC = [11, 10, 14, 13] => False
(Không phải vì thiếu 12)
```

## Phương pháp

- **_Cách thông thường_**: Sắp xếp mảng => Time complexity bằng O<sub>(log<sub>n</sub>)</sub>

- **_Cách tốt hơn_**: Time complexity O<sub>(n)</sub>

### Các bước thực hiện

1.  Tìm số lớn nhất và nhỏ nhất của mảng
2.  Kiểm tra nếu chiều dài mảng có bằng `max - min + 1`
3.  Trừ tất cả các phần tử của mảng cho `min`
4.  Kiểm tra xem mảng có bị đúp phần tử hay không

Ta sẽ focus vào bước số 4 như sau

---

### Nếu mảng chứa phần tử âm

- Tạo một mảng phụ và đặt 0 vào tất cả phần tử
- Di chuyển trên mảng chính và cập nhật mảng phụ `aux[arrA[i]] = 1`
- Trong toàn bộ bước số 2, nếu bạn thấy bất kỳ vị trí nào có giá trị 1 thì mảng đã bị đúp và chúng ta trả về False
- Thao tác này sẽ tốn time complexity và space complexity đều bằng O<sub>(n)</sub>

### Nếu mảng không chứa phần tử âm

- Di chuyển qua mảng
- Cập nhật giá trị cho mảng tại vị trí i bằng `arrA[arrA[i]] = arrA[arrA[i]] * -1` (Nếu nó không âm)
- Nếu âm dẫn đến đúp, trả về False
- Thao tác này thì time complexity O<sub>(n)</sub> và space complexity O<sub>(1)</sub>

### Code mẫu

```python
def find_max(arr):
    _max = arr[0]
    for i in range(1, len(arr)):
        if _max < arr[i]:
            _max = arr[i]
    return _max

def find_min(arr):
    _min = arr[0]
    for i in range(1, len(arr)):
        if _min > arr[i]:
            _min = arr[i]
    return _min



def without_aux_arr(arr):
    """Cách này sẽ đúng nếu như mảng không âm"""

    # Bước 1
    _max = find_max(arr)
    _min = find_min(arr)

    # Bước 2
    if len(arr) != _max - _min + 1:
        return False

    # Bước 3
    for i in range(0, len(arr)):
        arr[i] = arr[i] - _min + 1

    # Bước 4
    for i in range(0, len(arr)):
        x = abs(arr[i])
        if arr[x - 1] > 0:
            arr[x - 1] = arr[x - 1] * -1
        else:
            return False
    return True

    print(arr)


def with_aux_arr(arr):
    """Phương pháp này đúng với cả mảng chứa số âm"""

    # Bước 1
    aux_arr = []
    _max = find_max(arr)
    _min = find_min(arr)

    # Bước 2
    if len(arr) != _max - _min + 1:
        return False

    # Bước 3
    for i in range(0, len(arr)):
        arr[i] = arr[i] - _min
        aux_arr.append(0)

    #Bước 4
    for i in range(0, len(arr)):
        if aux_arr[arr[i]] == 0:
            aux_arr[arr[i]] = 1
        else:
            return False

    # Nếu code chạy đến đây thì ta đã đạt đủ điều kiện
    return True


def main():
    arrA = [21, 24, 22, 26, 29, 25]
    print(with_aux_arr(arrA))

    arrA = [-1, 0, 1, 2,3]
    print(without_aux_arr(arrA))

main()
```
