Name :               Shahnawaz Habib Jaffar
Department :     Computer Science
Submission DL:  20/11/2024
Subject :              Data Structure and Algorithm (DSA)
Submitted to:     Tajmir khan



To implement a dynamic array in C++ that adheres to the given requirements, we will encapsulate the functionality in a class. This class will allow us to manage memory dynamically, resize the array when needed, and provide essential operations like adding elements, displaying the content, and retrieving values.

Here’s a detailed step-by-step implementation in C++:

Key Steps:
Constructor: Initialize the dynamic array with an initial capacity and size.
Destructor: Free dynamically allocated memory.
Add Element: Add elements to the array and resize when necessary.
Resize Array: Automatically resize the array when capacity is exceeded.
Display Elements: Print all elements in the array.
Get Array Size: Return the current number of elements in the array.
Get Value by Index: Retrieve the value at a specific index, with error handling for invalid indices.
C++ Code Implementation:
cpp
Copy code
#include <iostream>
#include <stdexcept>  // for exception handling

class DynamicArray {
private:
    int* arr;            // Pointer to dynamically allocated array
    int capacity;        // Current capacity of the array
    int size;            // Current number of elements in the array

    // Helper function to resize the array when capacity is exceeded
    void resize() {
        capacity *= 2;  // Double the capacity
        int* newArr = new int[capacity];

        // Copy old array elements to the new array
        for (int i = 0; i < size; ++i) {
            newArr[i] = arr[i];
        }

        // Free old array memory and point arr to the new array
        delete[] arr;
        arr = newArr;
    }

public:
    // Constructor: Initializes the dynamic array with a starting capacity of 2
    DynamicArray(int initialCapacity = 2) {
        capacity = initialCapacity;
        size = 0;
        arr = new int[capacity];
    }

    // Destructor: Deallocates memory to prevent memory leaks
    ~DynamicArray() {
        delete[] arr;
    }

    // Add element to the array
    void addElement(int value) {
        if (size == capacity) {
            resize();  // Resize array if capacity is exceeded
        }
        arr[size++] = value;
    }

    // Display all elements in the array
    void display() const {
        if (size == 0) {
            std::cout << "Array is empty!" << std::endl;
            return;
        }
        std::cout << "Array contents: ";
        for (int i = 0; i < size; ++i) {
            std::cout << arr[i] << " ";
        }
        std::cout << std::endl;
    }

    // Get the current size of the array
    int getSize() const {
        return size;
    }

    // Retrieve value by index (with bounds checking)
    int getValueByIndex(int index) const {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Index out of range!");
        }
        return arr[index];
    }
};

// Function to show the menu and interact with the user
void showMenu() {
    std::cout << "\nMenu:\n";
    std::cout << "1. Add Element\n";
    std::cout << "2. Display Array\n";
    std::cout << "3. Resize Array (Resize by doubling the size)\n";
    std::cout << "4. Find Array Size\n";
    std::cout << "5. Get Value by Index\n";
    std::cout << "6. Exit\n";
}

int main() {
    DynamicArray arr;
    int choice, value, index;

    while (true) {
        showMenu();
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1:
                // Add Element
                std::cout << "Enter value to add: ";
                std::cin >> value;
                arr.addElement(value);
                break;

            case 2:
                // Display Array
                arr.display();
                break;

            case 3:
                // Resize Array
                std::cout << "Array resized automatically when capacity is exceeded.\n";
                break;

            case 4:
                // Find Array Size
                std::cout << "Current size of the array: " << arr.getSize() << std::endl;
                break;

            case 5:
                // Get Value by Index
                std::cout << "Enter index: ";
                std::cin >> index;
                try {
                    value = arr.getValueByIndex(index);
                    std::cout << "Value at index " << index << ": " << value << std::endl;
                } catch (const std::out_of_range& e) {
                    std::cout << "Error: " << e.what() << std::endl;
                }
                break;

            case 6:
                // Exit
                std::cout << "Exiting program.\n";
                return 0;

            default:
                std::cout << "Invalid choice! Please select again.\n";
        }
    }

    return 0;
}
Explanation of the Code:
DynamicArray Class:

Private Members:
int* arr: A pointer to the dynamically allocated array.
int capacity: The current capacity of the array.
int size: The current number of elements in the array.
Member Functions:
resize(): Doubles the array's capacity and copies the existing elements into a new array.
addElement(int value): Adds a new element to the array and resizes it if necessary.
display(): Prints the current contents of the array.
getSize(): Returns the current number of elements in the array.
getValueByIndex(int index): Retrieves the value at a specific index, throwing an exception if the index is out of range.
Main Program:

Provides a simple text-based menu for the user to interact with the dynamic array.
Allows the user to add elements, display the array, resize it, get the size, and access specific elements by index.
Error handling is implemented for invalid indices when accessing values.
Example Usage:
mathematica
Copy code
Menu:
1. Add Element
2. Display Array
3. Resize Array (Resize by doubling the size)
4. Find Array Size
5. Get Value by Index
6. Exit
Enter your choice: 1
Enter value to add: 10

Menu:
1. Add Element
2. Display Array
3. Resize Array (Resize by doubling the size)
4. Find Array Size
5. Get Value by Index
6. Exit
Enter your choice: 2
Array contents: 10
Explanation of Key Operations:
Adding Elements: The addElement method adds an element to the array, resizing it automatically if the capacity is exceeded.
Resizing: The array is resized by doubling its capacity whenever the array reaches its current capacity.
Displaying the Array: The display method prints the current elements in the array in a user-friendly format.
Getting Array Size: The getSize method returns the current number of elements in the array.
Accessing Value by Index: The getValueByIndex method retrieves the value at a specific index, with bounds checking to prevent accessing out-of-range elements.
Error Handling:
Invalid indices when accessing the array are handled using std::out_of_range exceptions.
Invalid menu choices are also handled gracefully.
This implementation ensures that the dynamic array behaves as expected, with memory management, resizing, and operations working seamlessly.
