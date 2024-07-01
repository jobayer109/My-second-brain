### What is a Pointer?
- **Definition**: A pointer is a variable that stores the memory address of another variable.
- **Syntax**: `type *pointerName;`

### Declaration and Initialization
```cpp
int *ptr;  // declares a pointer to an integer
```
```cpp
int x = 10;
int *ptr = &x;  // ptr now holds the address of x
```

### Dereferencing
- **Dereferencing**: Accessing the value stored at the memory address held by the pointer.
```cpp
int y = *ptr;  // y now holds the value of x, which is 10
```

### Pointer Arithmetic
- **Incrementing/Decrementing**: Traversing through an array.
```cpp
int arr[] = {1, 2, 3, 4, 5};
int *ptr = arr;  // ptr points to the first element of arr

ptr++;  // ptr now points to the second element of arr
```

### Null Pointers
- **Null Pointer**: A pointer that is not assigned any memory address.
```cpp
int *ptr = nullptr;
```

### Pointers and Functions
- **Passing Pointers to Functions**: Allows modification of the original variable.
```cpp
void increment(int *p) {
    (*p)++;
}

int main() {
    int x = 5;
    increment(&x);  // x is now 6
    return 0;
}
```

### Dynamic Memory Allocation
- **Using `new` and `delete`**: Allocating and freeing memory dynamically.
```cpp
int *ptr = new int;  // dynamically allocate memory for an integer
*ptr = 7;

delete ptr;  // free the allocated memory
```

### Example: Swapping Values Using Pointers
```cpp
#include <iostream>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 10;
    int y = 20;
    
    std::cout << "Before swap: x = " << x << ", y = " << y << std::endl;
    swap(&x, &y);
    std::cout << "After swap: x = " << x << ", y = " << y << std::endl;

    return 0;
}
```

### Best Practices
- **Initialize Pointers**: Always initialize pointers to `nullptr` if not immediately assigned a valid address.
- **Memory Management**: Ensure dynamically allocated memory is properly freed using `delete`.
- **Avoid Dangling Pointers**: Do not use pointers to memory that has been freed or is out of scope.
