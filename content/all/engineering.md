---
tags:
  - programming
  - engineering
  - gotcha
  - pitfall
---
# Python

|        | PIL/scipy.misc              | cv2   | skimage |
| ------ | --------------------------- | ----- | ------- |
| Mode   | RGB                         | _BGR_ | RGB     |
| Resize | WxH                         | WxH   | _HxW_   |
| Size   | _WxH but HxWxC if np.array_ | HxWxC | HxWxC   |
## numpy
1. `flatten` returns a new copy while `ravel` returns a view. (pytorch is
   different)
# C
1. `volatile` can be used to modify functions to inform gcc that this function will
   not return.
# CPP
1. This snippet will not print out all the content in the priority_queue because
seat.size() is evaluated every iteration.
```cpp
priority_queue<int> seat;
// ...
for (int i = 0; i < seat.size(); i++) {
  cout << seat.top().first << endl;
  seat.pop();
}
```
2. gcc and clang will not report a warning for narrowing conversion unless you
specify `-Wconversion`