1️⃣ Avoid Unnecessary Data Structures
🔹 Problem: Using Map, Set, or extra arrays when they aren't necessary increases space complexity.
✅ Solution: Modify the existing array in-place instead of creating copies.
Example: Removing duplicates efficiently

javascript
Copy
Edit
// Less efficient (uses extra Set)
var removeDuplicates = function(nums) {
    let unique = new Set(nums); // O(n) space
    return [...unique]; // Creates a new array
};

// More efficient (modifies in-place)
var removeDuplicates = function(nums) {
    let j = 0;
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] !== nums[j]) {
            j++;
            nums[j] = nums[i]; // Modify in place
        }
    }
    nums.length = j + 1; // Trim unused elements
    return j + 1;
};
✔ Memory Usage: O(1) instead of O(n)

2️⃣ Use Two Pointers Instead of Extra Arrays
Instead of creating a new array for filtering or processing, use two pointers (slow and fast) to overwrite the existing array.

Example: Moving Zeros Efficiently

javascript
Copy
Edit
// Inefficient (creates a new array)
var moveZeroes = function(nums) {
    let nonZero = nums.filter(num => num !== 0); // O(n) space
    let zeros = Array(nums.length - nonZero.length).fill(0);
    return [...nonZero, ...zeros];
};

// More Efficient (modifies in-place)
var moveZeroes = function(nums) {
    let j = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== 0) {
            [nums[j], nums[i]] = [nums[i], nums[j]]; // Swap non-zero forward
            j++;
        }
    }
};
✔ Memory Usage: O(1) instead of O(n)

3️⃣ Use Primitive Data Types When Possible
Objects and arrays take up more memory than primitive types (number, boolean, string).

Example: Instead of an object, use a simple counter or bit manipulation.

Example: Checking if all numbers are unique

javascript
Copy
Edit
// Uses extra space (O(n))
var allUnique = function(nums) {
    let seen = new Set(nums);
    return seen.size === nums.length;
};

// More efficient (O(1) space with bitwise operations)
var allUnique = function(nums) {
    let checker = 0;
    for (let num of nums) {
        let bit = 1 << num;
        if (checker & bit) return false;
        checker |= bit;
    }
    return true;
};
✔ Memory Usage: O(1) instead of O(n)

4️⃣ Modify Input Instead of Returning New Data
If you don’t need to keep the original data, modify it in-place instead of creating a new copy.

Example: Reversing an array

javascript
Copy
Edit
// Less efficient (creates new array)
var reverseArray = function(arr) {
    return arr.slice().reverse();
};

// More efficient (modifies in-place)
var reverseArray = function(arr) {
    let left = 0, right = arr.length - 1;
    while (left < right) {
        [arr[left], arr[right]] = [arr[right], arr[left]]; // Swap in place
        left++;
        right--;
    }
};
✔ Memory Usage: O(1) instead of O(n)

5️⃣ Use Generators for Large Data Processing
If you're dealing with large datasets, generators (yield) help avoid loading everything into memory at once.

Example: Processing large logs efficiently

javascript
Copy
Edit
// Inefficient (loads everything into memory)
function readLinesSync(filePath) {
    const fs = require('fs');
    return fs.readFileSync(filePath, 'utf8').split('\n'); // O(n) space
}

// Efficient (uses a generator)
function* readLines(filePath) {
    const fs = require('fs');
    const readline = require('readline');
    const stream = fs.createReadStream(filePath);
    const rl = readline.createInterface({ input: stream });

    for await (const line of rl) {
        yield line; // Only keeps one line in memory at a time
    }
}
✔ Memory Usage: O(1) instead of O(n)

6️⃣ Use Efficient Data Structures
Choosing the right data structure can reduce memory consumption.

Task	Inefficient	Efficient
Checking duplicates	array.includes(num) (O(n))	Set.has(num) (O(1))
Counting frequency	Object { key: count } (O(n) space)	Use bitwise operations if numbers are small
Large lists	Array (O(n))	Linked List if frequent insertions/removals
7️⃣ Avoid Memory Leaks
Common causes of memory leaks in JavaScript:

Global variables that persist (window.variable)

Uncleared event listeners

Closures holding unnecessary references

Forgetting to null out large objects after use

Example: Preventing a memory leak in event listeners

javascript
Copy
Edit
// Bad: Event listener stays in memory forever
document.getElementById('btn').addEventListener('click', function() {
    console.log('Clicked!');
});

// Good: Remove event listener when not needed
const handler = function() {
    console.log('Clicked!');
    document.getElementById('btn').removeEventListener('click', handler);
};
document.getElementById('btn').addEventListener('click', handler);
✔ Memory Usage: Prevents unnecessary retention of objects.

8️⃣ Use WeakMap & WeakSet for Temporary Data
Map and Set keep keys alive in memory even if they’re no longer used.

WeakMap and WeakSet allow garbage collection when objects are no longer referenced.

Example: Using WeakMap for caching

javascript
Copy
Edit
let cache = new WeakMap();

function getUserData(user) {
    if (!cache.has(user)) {
        cache.set(user, fetchData(user.id)); // Only stores while `user` exists
    }
    return cache.get(user);
}
✔ Memory Usage: No risk of memory leaks.

Conclusion
🚀 Key takeaways for memory-efficient JavaScript: ✅ Modify arrays in-place instead of creating copies.
✅ Use two pointers instead of extra arrays.
✅ Prefer primitive types over objects when possible.
✅ Avoid unnecessary data structures like Map unless needed.
✅ Use generators (yield) for large datasets.
✅ Be careful with event listeners & closures to prevent memory leaks.
✅ Use WeakMap & WeakSet for temporary data storage.

Would you like a memory profiling example using console.memory or Performance API? 🚀