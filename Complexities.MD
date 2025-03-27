1️⃣ Constant Time - O(1)
👉 The algorithm takes the same time regardless of input size.

javascript
Copy
Edit
function getFirstElement(arr) {
    return arr[0]; // Always takes constant time
}

console.log(getFirstElement([10, 20, 30])); // Output: 10
✅ Why O(1)?

Only one operation is performed, no matter how large arr is.

2️⃣ Logarithmic Time - O(log n)
👉 The problem size shrinks exponentially.

javascript
Copy
Edit
function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;

    while (left <= right) {
        let mid = Math.floor((left + right) / 2);

        if (arr[mid] === target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }

    return -1;
}

console.log(binarySearch([1, 3, 5, 7, 9], 7)); // Output: 3
✅ Why O(log n)?

Each step cuts the array in half (dividing work by 2 each time).

3️⃣ Linear Time - O(n)
👉 The runtime grows proportionally to the input size.

javascript
Copy
Edit
function sumArray(arr) {
    let sum = 0;
    for (let num of arr) {
        sum += num;
    }
    return sum;
}

console.log(sumArray([1, 2, 3, 4, 5])); // Output: 15
✅ Why O(n)?

Each element is visited once.

4️⃣ Linearithmic Time - O(n log n)
👉 Common in efficient sorting algorithms.

javascript
Copy
Edit
function mergeSort(arr) {
    if (arr.length <= 1) return arr;

    let mid = Math.floor(arr.length / 2);
    let left = mergeSort(arr.slice(0, mid));
    let right = mergeSort(arr.slice(mid));

    return merge(left, right);
}

function merge(left, right) {
    let result = [], i = 0, j = 0;

    while (i < left.length && j < right.length) {
        if (left[i] < right[j]) result.push(left[i++]);
        else result.push(right[j++]);
    }

    return result.concat(left.slice(i)).concat(right.slice(j));
}

console.log(mergeSort([5, 3, 8, 4, 2])); // Output: [2, 3, 4, 5, 8]
✅ Why O(n log n)?

mergeSort divides the array (log n) and merges (n).

5️⃣ Quadratic Time - O(n²)
👉 Nested loops make this inefficient for large inputs.

javascript
Copy
Edit
function bubbleSort(arr) {
    let n = arr.length;
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // Swap
            }
        }
    }
    return arr;
}

console.log(bubbleSort([5, 3, 8, 4, 2])); // Output: [2, 3, 4, 5, 8]
✅ Why O(n²)?

Two nested loops → n * n operations.

6️⃣ Cubic Time - O(n³)
👉 Triple-nested loops (even worse than O(n²)).

javascript
Copy
Edit
function tripletSum(arr) {
    let count = 0;
    for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < arr.length; j++) {
            for (let k = 0; k < arr.length; k++) {
                count++;
            }
        }
    }
    return count;
}

console.log(tripletSum([1, 2, 3])); // Output: 27
✅ Why O(n³)?

Three nested loops → n * n * n.

7️⃣ Exponential Time - O(2ⁿ)
👉 Often seen in brute-force recursive algorithms.

javascript
Copy
Edit
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(5)); // Output: 5
✅ Why O(2ⁿ)?

Each call spawns two more recursive calls, leading to an exponential explosion.

8️⃣ Factorial Time - O(n!)
👉 Seen in problems like traveling salesperson problem (TSP).

javascript
Copy
Edit
function permutations(str, prefix = "") {
    if (str.length === 0) console.log(prefix);
    for (let i = 0; i < str.length; i++) {
        let rem = str.slice(0, i) + str.slice(i + 1);
        permutations(rem, prefix + str[i]);
    }
}

permutations("ABC"); 
// Output: ABC, ACB, BAC, BCA, CAB, CBA
✅ Why O(n!)?

Each character can be placed in n! ways.

🚀 Complexity Summary Table
Complexity	Example	Efficient?
O(1)	Accessing array element	✅ Best
O(log n)	Binary search	✅ Great
O(n)	Linear search, summing an array	✅ Good
O(n log n)	Merge sort, QuickSort (avg)	✅ Efficient
O(n²)	Bubble sort, Selection sort	❌ Slow
O(n³)	Triple nested loops	❌ Very slow
O(2ⁿ)	Fibonacci recursion	❌ Horrible
O(n!)	Permutations, TSP	❌ Worst
🔥 Key Takeaways
Avoid O(n²) or worse in large datasets.

Use O(n log n) sorting instead of O(n²).

Logarithmic (O(log n)) and linear (O(n)) are efficient for searching.

Exponential & factorial algorithms should be replaced with dynamic programming or greedy techniques.