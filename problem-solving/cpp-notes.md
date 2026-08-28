# C++ notes to check

<details>
<summary>1. Use Class (Initialization, Public/Private Scopes)</summary>

### Explanation
In C++, a `class` is used to define custom data types. 
- **Private:** Members are accessible only from within other member functions of the same class. This is the default scope if none is specified.
- **Public:** Members are accessible from outside the class.
- **Initialization:** You can initialize members using a constructor. The member initializer list is the preferred way to initialize class variables.

### Example Code
```cpp
#include <iostream>
#include <string>

using namespace std;

class Solution {
private:
    string name;
    int value;

    // Private method
    void updateValue(int val) {
        value = val;
    }

public:
    // Constructor with initializer list
    Solution(string n, int v) : name(n), value(v) {}

    void print() {
        cout << "Name: " << name << ", Value: " << value << endl;
    }

    void process(int multiplier) {
        updateValue(value * multiplier);
    }
};

int main() {
    // Initialization
    Solution sol("Interview", 10);
    sol.print(); // Output: Name: Interview, Value: 10
    
    sol.process(5);
    sol.print(); // Output: Name: Interview, Value: 50
    return 0;
}
```
</details>

<details>
<summary>2. Return Exception</summary>

### Explanation
Exceptions provide a way to react to exceptional circumstances (like runtime errors) in programs by transferring control to special functions called handlers.
- `throw`: Used to signal an exception.
- `try`: Identifies a block of code for which particular exceptions will be activated.
- `catch`: Catches the exception with an exception handler.

### Example Code
```cpp
#include <iostream>
#include <stdexcept>

using namespace std;

int divide(int a, int b) {
    if (b == 0) {
        // Throwing a standard runtime exception
        throw runtime_error("Division by zero exception!");
    }
    return a / b;
}

int main() {
    try {
        cout << divide(10, 2) << endl; // Output: 5
        cout << divide(10, 0) << endl; // Throws exception
    } catch (const exception& e) {
        // Catching the exception and printing the error message
        cerr << "Caught exception: " << e.what() << endl;
    }
    return 0;
}
```
</details>

<details>
<summary>3. File Input/Output with 'freopen'</summary>

### Explanation
`freopen` is heavily used in competitive programming and technical interviews to redirect standard input (`stdin`) and standard output (`stdout`) to read from and write to text files instead of the console. This makes it easier to run test cases locally.

### Example Code
```cpp
#include <iostream>

using namespace std;

int main() {
    // Redirect stdin to read from "input.txt"
    // Redirect stdout to write to "output.txt"
    #ifndef ONLINE_JUDGE
    freopen("input.txt", "r", stdin);
    freopen("output.txt", "w", stdout);
    #endif

    int a, b;
    // Reads from input.txt instead of the console
    if (cin >> a >> b) {
        // Writes to output.txt instead of the console
        cout << "Sum: " << (a + b) << endl; 
    }
    
    return 0;
}
```
</details>

<details>
<summary>4. Command Line Input</summary>

### Explanation
Command line arguments are passed to the `main` function. 
- `argc` (Argument Count): The number of command line arguments passed.
- `argv` (Argument Vector): An array of character pointers (C-strings) containing the arguments. `argv[0]` is typically the name of the program itself.

### Example Code
```cpp
#include <iostream>

using namespace std;

int main(int argc, char* argv[]) {
    cout << "Total arguments provided: " << argc << endl;
    
    // Loop through all provided arguments
    for (int i = 0; i < argc; i++) {
        cout << "Argument " << i << ": " << argv[i] << endl;
    }
    
    // Example usage: converting argument string to integer
    if (argc > 1) {
        int firstArgAsInt = stoi(argv[1]);
        cout << "First argument as int + 5: " << firstArgAsInt + 5 << endl;
    }

    return 0;
}
```
</details>

<details>
<summary>5. Split Strings using 'stringstream'</summary>

### Explanation
`stringstream` acts like a stream (like `cin`), but instead of reading from the console, it reads from a string. When combined with `getline` and a custom delimiter, it's the standard and most efficient way to split a string in C++.

### Example Code
```cpp
#include <iostream>
#include <sstream>
#include <vector>
#include <string>

using namespace std;

vector<string> splitString(const string& log, char delimiter) {
    stringstream ss(log);
    string token;
    vector<string> tokens;
    
    // Read from stringstream 'ss' into 'token' until 'delimiter' is found
    while (getline(ss, token, delimiter)) {
        tokens.push_back(token);
    }
    
    return tokens;
}

int main() {
    string logEntry = "grpcs 2025-04-22T23:57:52Z 10.169.30.214 200";
    
    vector<string> result = splitString(logEntry, ' ');
    
    cout << "Tokens:" << endl;
    for (int i = 0; i < result.size(); i++) {
        cout << i << ": " << result[i] << endl;
    }
    // Output:
    // 0: grpcs
    // 1: 2025-04-22T23:57:52Z
    // 2: 10.169.30.214
    // 3: 200

    return 0;
}
```
</details>

<details>
<summary>6. Sorting with Custom Comparator (Lambda)</summary>

### Explanation
A very common interview requirement is sorting a container (like a vector of pairs or custom objects) based on a specific logic. Using inline lambda functions inside `std::sort` makes this clean and straightforward.

### Example Code
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    vector<pair<int, int>> intervals = {{1, 3}, {2, 6}, {8, 10}, {15, 18}};

    // Sort intervals by the second element in descending order
    sort(intervals.begin(), intervals.end(), [](const pair<int, int>& a, const pair<int, int>& b) {
        return a.second > b.second; 
    });

    for (auto it : intervals) {
        cout << "[" << it.first << ", " << it.second << "] ";
    }
    // Output: [15, 18] [8, 10] [2, 6] [1, 3]
    cout << endl;
    return 0;
}
```
</details>
