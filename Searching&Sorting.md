# Searching

-   **Sequential** Search locates the target value in an array/list by examining each element from start to finish
-   **Binary** Search locates the target value in a sorted array/list by

# Methods from the Arrays classes that are useful

-   Syntax: `Arrays.methodName(parameters)`
-   `Arrays.binarySearch(array, value)` - returns the index of a given value in a sorted array, or < 0 if not found
-   `Arrays.binarySearch(array, minIndex, maxIndex, value)` - returns index of given value in a sorted array between indexes min and max - 1 (< 0 if not found)
-   `copyOf(array, length)` - returns a new resized copy of an array
-   `equals(array1, array2)` - returns true if the two arrays contain same elements in the same order
-   `fill(array, value)` - sets every element to the given value
-   `sort(array)` - arranges the elements into sorted order
-   `toString(array)` - returns a string representing the array, such as “[10, 30, -25, 17]”

```
// searches an entire sorted array for a given value
// returns its index if found;  a negative number if not found
// Precondition: array is sorted
Arrays.binarySearch(array, value)

// searches given portion of a sorted array for a given value
// examines minIndex (inclusive) through maxIndex (exclusive)
// returns its index if found;  a negative number if not found
// Precondition: array is sorted
Arrays.binarySearch(array, minIndex, maxIndex, value)
```

-   The `binarySearch` method in the `Arrays` class searches an array very efficiently if the array is sorted
-   You can search the entire array, or juts a range of indexes
-   If the array is not sorted, you may need to sort it first

```
// index    0  1  2  3   4   5   6   7   8   9  10  11  12  13  14  15
int[] a = {-4, 2, 7, 9, 15, 19, 25, 28, 30, 36, 42, 50, 56, 68, 85, 92};

int index  = Arrays.binarySearch(a, 0, 16, 42);   // index1 is 10
int index2 = Arrays.binarySearch(a, 0, 16, 21);   // index2 is -7
```

-   if the value is not found, `binarySearch` returns
-   `-(insertionPoint - 1)`
-   insertionPoint is the index where the element would have beein, if it has been in the sorted array
-   To insert the velue into the array, negate insertionPoint + 1
-   `int indexToInsert21 = -(index2 + 1); //6`

```
// Returns the index of an occurrence of target in a,
// or a negative number if the target is not found.
// Precondition: elements of a are in sorted order
public static int binarySearch(int[] a, int target) {
    int min = 0;
    int max = a.length - 1;

    while (min <= max) {
        int mid = (min + max) / 2;
        if (a[mid] < target) {
            min = mid + 1;
        } else if (a[mid] > target) {
            max = mid - 1;
        } else {
            return mid;   // target found
        }
    }

    return -(min + 1);    // target not found
}
```

-   natural ordering: rules governing the relative placement of all values of a given type
-   Comparison fuction: code that, when given two values A and B of a given type, decides their relative ordering
-   The standard way for a java class to define a comparison function for its objects is to define a `compareTo` method
-   A call of `A.compareTo(B)` will return a value:
-   < 0 if A comes before B in the ordering
-   0 if A and B are considered equal in the ordering
-   efficiency - A measure of the use of computing resources by code
-   Can be relative to speed (time), memory (space), etc
-   most commonly refers to run time

## Assume the following

-   Any single java statement takes the same amount fo time to run
-   A method call’s runtime is measured by the total of the statements inside the method’s body
-   A loop’s runtime, if the loop repeats N times, is N times the runtime of the statements in its body
-   We measure runtime in proportion to the input data size, N
-   growth rate: change in runtime as N changes
-   we ignore constants because they are tiny next to N
-   the highest order term (N^3) dominates the overall runtime
-   we say that this algorithm runs “on the order of” N^3
-   or O(N^3) for short (“Big Oh of N cubed”)
-   Complexity class: a category of algorithm efficiency based upon the algorithm’s relationship to the number of inputs, N
- ![[NType.png]]
- **Binary Search**: successively eliminates half of the elements
	- Algorithm: examine the middle element of the array
		- If it is too big, eliminate the right half of the array and repeat
		- If it is too small, eliminate the left half of the array and repeat
		- Else it is the value that we are searching for, so stop
	- For an array of size N, it eliminates 1/2 until 1 element remains
	- Think of it from the other direction:
		- How many times do I have to multiply by 2 to reach N?
			- Call this number of multiplications "x"
	- Binary search is in the logarithmic complexity class
	- ![[BIGOComplexityChart.png]]
	- Range Algorithm
		- ```
```
// returns the range of values in the given array;

// the difference between elements furthest apart

// example: range({17, 29, 11, 4, 20, 8}) is 25

public static int range(int[] numbers) {

    int maxDiff = 0;     // look at each pair of values

    for (int i = 0; i < numbers.length; i++) {

        for (int j = 0; j < numbers.length; j++) {

            int diff = Math.abs(numbers[j] – numbers[i]);

            if (diff > maxDiff) {

                maxDiff = diff;

            }

        }

    }

    return diff;

}
```
Range Algorithm 2
The algortithm is O(N^2)
```
// returns the range of values in the given array;

// the difference between elements furthest apart

// example: range({17, 29, 11, 4, 20, 8}) is 25

public static int range(int[] numbers) {

    int maxDiff = 0;     // look at each pair of values

    for (int i = 0; i < numbers.length; i++) {

        for (int j = i + 1; j < numbers.length; j++) {

            int diff = Math.abs(numbers[j] – numbers[i]);

            if (diff > maxDiff) {

                maxDiff = diff;

            }

        }

    }

    return diff;

}
```
This final version is O(N). It runs much faster
```
// returns the range of values in the given array;

// example: range({17, 29, 11, 4, 20, 8}) is 25

public static int range(int[] numbers) {

    int max = numbers[0];     // find max/min values

    int min = max;

    for (int i = 1; i < numbers.length; i++) {

        if (numbers[i] < min) {

            min = numbers[i];

        }

        if (numbers[i] > max) {

            max = numbers[i];

        }

    }

    return max - min;

}
```
Complexity Cheat Sheet:
![[ComplexityCheatSheet.png]]
