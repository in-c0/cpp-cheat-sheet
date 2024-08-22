# CPP Cheatsheet

For exam / hackathon / coding contest. Also see [CPP Utilities](cpp-utility-functions.md)


# Input Processing

### File read - try catch

```cpp
#include <iostream>
#include <fstream>

class FileRAII {
public:
    FileRAII(const std::string& filename) : file(filename) {
        if (!file.is_open()) {
            throw std::runtime_error("Failed to open file");
        }
    }

    ~FileRAII() {
        if (file.is_open()) {
            file.close();
        }
    }

private:
    std::ofstream file;
};

int main() {
    try {
        FileRAII file("example.txt");
        // file operations...
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
    }
    return 0;
}
```

### File Input/Output - Store in a string vector

```cpp
#include <fstream>
#include <sstream>
#include <string>
#include <vector>

auto main() -> int {
    
    std::ifstream inputFile("input.txt"); 
    std::ofstream outputFile("output.txt");
    // If you want to append to output.txt instead of overwriting it, 
    // open the file in append mode by
    // std::ofstream outputFile("output.txt", std::ios_base::app);
    
    std::vector<string> tokens;
    std::string line;

    while (std::getline(inputFile, line)) {
        std::stringstream ss(line);
        std::string token;
        while (ss >> token) {
            tokens.push_back(token);
        }
    }

    inputFile.close();

		// print output
    for (const auto& tok : tokens) { // const to make it read-only, & for performance
        std::cout << tok << std::endl;
    }
    
    // write to output file
    for (const auto& tok : tokens) {
        outputFile << tok << std::endl; 
        // writes each token to the file, each on a new line
    }

    outputFile.close();

    return 0;
}
```

Caveat - using `std::stringstream` seems to somehow make floats lose the floating point precision. We gotta set them manually if we wanna print as float:

```cpp
#include <iomanip>

std::stringstream output_ss;
output_ss << std::fixed << std::setprecision(3);
```

### String Vector - Concatenate with a comma and a space

```cpp
#include <vector>
#include <numeric>  // For std::accumulate
#include <iostream>
#include <string>

int main() {
    std::vector<std::string> vec{"Hello", "World", "This", "is", "C++"};

    std::string result = std::accumulate(vec.begin(), vec.end(), std::string(""),
        [](const std::string& a, const std::string& b) {
            return a + (a.empty() ? "" : ", ") + b;
        });

    std::cout << result;
    return 0;
} 

// Hello, World, This, is, C++
```

### String Vector - Split a line by spaces or newlines

```cpp
#include <sstream>
#include <string>
#include <vector>

auto splitString(const std::string &str) -> std::vector<std::string> {
    std::vector<std::string> tokens;
    std::stringstream ss(str);
    std::string token;
    
    while (ss >> token) {
        tokens.push_back(token);
    }
    
    return tokens;
}

// Example:

// auto tokens = splitString("10 20 sub");
// tokens is now {"10", "20", "sub"}

```

### Vector - Print Output Line by Line

```cpp
#include <vector>
#include <string>

vector<string> svec;
for (auto const& line : svec) { // const to make it read-only, & for performance
    cout << line << endl;
}
```

or using std::for_each( start , end ,  void function pointer )…

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

void printElement(int n) {
    std::cout << n << " ";
}

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    std::for_each(numbers.begin(), numbers.end(), printElement);
    // Output: 1 2 3 4 5

    return 0;
}

```

or using Lambda (pass as reference into the function if you’re modifying the element, otherwise, modify the copied value and mark the lambda as mutable):

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};

    std::for_each(numbers.begin(), numbers.end(), [](int &n) {
        n *= 2;
    });

    for (int n : numbers) {
        std::cout << n << " ";  // Output: 2 4 6 8 10
    }
    return 0;
}
```

or using Lambda, and modifying values captured from outside of the loop … e.g. [&count]

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    int count = 0;

    std::for_each(numbers.begin(), numbers.end(), [&count](int n) {
        if (n > 2) count++;
    });

    std::cout << "Count of elements > 2: " << count << std::endl;  // Output: 3
    return 0;
}
```

### Convert string to a “number” (e.g. ”42.6”, “3”) into double or int

```cpp
bool isInteger(const std::string& str) {
    if (str.empty()) return false;
    if (str == "-") return false;
    size_t start = 0;    
    for (size_t i = start; i < str.length(); ++i) {
        if (!std::isdigit(str[i])) return false;
    }

    return true;
}
```

```cpp
bool isDouble(const std::string& str) {
    if (str.empty()) return false;

    bool decimalPointSeen = false;
    size_t start = (str[0] == '-') ? 1 : 0;
    bool digitsSeen = false;

    for (size_t i = start; i < str.length(); ++i) {
        if (str[i] == '.') {
            if (decimalPointSeen) return false;  // two decimal points
            decimalPointSeen = true;
        } else if (std::isdigit(str[i])) {
            digitsSeen = true;
        } else {
            return false;
        }
    }

    // if there's at least one digit and exactly one decimal point
    return decimalPointSeen && digitsSeen;
}

```

```cpp
#include <iostream>
#include <string>

int main() {
    std::string input;
    std::cout << "Enter a string: ";
    std::cin >> input;

    if (isNumber(input)) {
        if (isInteger(input)) {
            std::cout << input << " is an integer." << std::endl;
        } else if (isDouble(input)) {
            std::cout << input << " is a double." << std::endl;
        } else {
            std::cout << input << " is a number, but neither an integer nor a double." << std::endl;
        }
    } else {
        std::cout << input << " is not a valid number." << std::endl;
    }

    return 0;
}
```

or use std::from_chars

```cpp
#include <iostream>
#include <charconv>
#include <string>

int main() {
    std::string str = "161718";
    int num;
    auto [ptr, ec] = std::from_chars(str.data(), str.data() + str.size(), num);
    if (ec == std::errc()) {
        std::cout << "Converted number: " << num << std::endl;  // Output: 161718
    } else {
        std::cerr << "Conversion failed" << std::endl;
    }
    return 0;
}

```

### Convert string to uppercase in place - std::transform

```cpp
#include <algorithm>
#include <cctype>
#include <iomanip>
#include <iostream>
#include <string>
#include <utility>
#include <vector>
 
void print_ordinals(const std::vector<unsigned>& ordinals)
{
    std::cout << "ordinals: ";
    for (unsigned ord : ordinals)
        std::cout << std::setw(3) << ord << ' ';
    std::cout << '\n';
}
 
char to_uppercase(unsigned char c)
{
    return std::toupper(c);
}
 
void to_uppercase_inplace(char& c)
{
    c = to_uppercase(c);
}
 
void unary_transform_example(std::string& hello, std::string world)
{
    // Transform string to uppercase in-place
    std::transform(hello.cbegin(), hello.cend(), hello.begin(), to_uppercase);
    std::cout << "hello = " << std::quoted(hello) << '\n';
 
    // std::transform does not guarantee in-order application of unary_op or binary_op.
    // To apply a function to a sequence in-order or to apply a function that modifies 
    // the elements of a sequence, use std::for_each

    // for_each version
    std::for_each(world.begin(), world.end(), to_uppercase_inplace);
    std::cout << "world = " << std::quoted(world) << '\n';
}
 
void binary_transform_example(std::vector<unsigned> ordinals)
{
    // Transform numbers to doubled values
 
    print_ordinals(ordinals);
 
    std::transform(ordinals.cbegin(), ordinals.cend(), ordinals.cbegin(),
                   ordinals.begin(), std::plus<>{});
 
    print_ordinals(ordinals);
}
 
int main()
{
    std::string hello("hello");
    unary_transform_example(hello, "world");
 
    std::vector<unsigned> ordinals;
    std::copy(hello.cbegin(), hello.cend(), std::back_inserter(ordinals));
    binary_transform_example(std::move(ordinals));

//    Output:
// hello = "HELLO"
// world = "WORLD"
// ordinals:  72  69  76  76  79 
// ordinals: 144 138 152 152 158
}
```

### Find string / Cut string / Convert to Bit - std::string::npos

```cpp
#include <bitset>
#include <iostream>
#include <string>
 
int main()
{
    // find() returns std::npos (-1) if nothing is found
    std::string s = "test string";
    if (s.find('a') == s.npos)
        std::cout << "no 'a' in 'test'\n";
 
    // from index 2 of s, go to the end of the string
    std::string s2(s, 2, std::string::npos);
    std::cout << s2 << '\n'; // s2 = "st string"

    // "aaabbBc" to 0001100 
    std::bitset<5> b("aaabbBc", std::string::npos, 'a', 'b');
    std::cout << b << '\n';
}
```

C#: String.Contains(’.’)

C++: token.find('.') == std::string::npos

### Floating point (precision)

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double pi = 3.141592653589793;

		// use both std::fixed and std::setprecision
    std::cout << std::fixed << std::setprecision(2) << pi << std::endl;  // 3.14
    std::cout << std::fixed << std::setprecision(5) << pi << std::endl;  // 3.14159
    return 0;
}
```

# TYPE CHECKING

### Runtime type checking - typeid

```cpp
#include <typeinfo>
#include <iostream>

int main() {
    int a = 5;
    double b = 3.14;

    std::cout << "Type of a: " << typeid(a).name() << std::endl;
    std::cout << "Type of b: " << typeid(b).name() << std::endl;

    if (typeid(a) == typeid(int)) {
        std::cout << "a is an int." << std::endl;
    }
    
    if (typeid(b) == typeid(double)) {
        std::cout << "b is a double." << std::endl;
    }

    return 0;
}
```

typeid(word).name(); if you want the string .. doesnt work on CLANG :(

### Compile-time Type Checking - decltype()

```cpp
int a = 10;
decltype(a) b;  // int b; 

int a = 10;
double b = 3.14;
decltype(a + b) c;  // double c;  .. adding an int to a double results in a double
```

```cpp
template<typename T1, typename T2>
auto add(T1 a, T2 b) -> decltype(a + b) { // auto add() -> double or int
    return a + b;
}
```

### Downcasting / Inheritance type checking - dynamic_cast

```cpp
class Base {
    virtual void dummy() {}
};

class Derived : public Base {};

int main() {
    Base* b = new Derived();
    Derived* d = dynamic_cast<Derived*>(b);

    if (d != nullptr) {
        std::cout << "b is actually a Derived." << std::endl;
    } else {
        std::cout << "b is not a Derived." << std::endl;
    }

    return 0;
}
```

### Compile time type checking - is_same<T1, T2>

```cpp
#include <type_traits>
#include <iostream>

int main() {
    int a = 5;
    double b = 3.14;

    if (std::is_same<decltype(a), int>::value) {
        std::cout << "a is an int." << std::endl;
    }

    if (std::is_same<decltype(b), double>::value) {
        std::cout << "b is a double." << std::endl;
    }

    return 0;
}
```

But be careful dividing an int by a float, because it results in a double:

```cpp
template <typename T>
T exampleFunc(T a) {
    if (is_same_v<T, int>) {
        return a + 1;  // Valid for both int and double
    } else {
        return a / 1.0;  // !! This would cause a compile-time error for int !!             
    }
}

// This is because the function expects an int return type from the else { } block
// but the division by a float is attempting to return a double
```

So remember to use `constexpr` to branch so that only the relevant branch for the type is compiled (in this case, we separate int division and float division)

```cpp
template <typename T>
T div(T a, T b) {
    if constexpr (is_same_v<T, int>) {
        return a / b;  // Integer division
    } else {
        return a / b;  // Floating-point division
    }
}
```

Other caveats:

- dividing a double by `0.0` results in `+inf`, `inf`, or `NaN` at runtime.
    
    e.g. `1.0 / 0.0 = +inf`, `-1.0 / 0.0 = -inf`.
    
- dividing an int by zero causes **undefined behavior** at runtime

# DATA STRUCTURES

STL Header:

```cpp
#include <bits/stdc++.h>
```

or

```cpp
#include <iostream>
#include <algorithm>
#include <list>
#include <map>
#include <queue> 
#include <stack>
#include <string>
#include <vector>
```

```cpp
using namespace std;

struct Person {
	string name;
	int age;
} p1, p2, p3;

struct is_older {
	bool operator()(struct Person p1, struct Person p2) {
    	return p1.age > p2.age;
    }
};

bool compare_names(struct Person p1, struct Person p2) {
    	return p1.name < p2.name;
}

bool way_to_sort(int i, int j) { return i > j; }

int main() {

	/*
	========
	 STACK
	========
	*/

	stack <string> distros; //Create a stack of strings.

	distros.push("Ubuntu");  //Pushing elements into the stack.
	distros.push("Mint");

	cout << "Number of distros in the stack are " << distros.size() << endl;
	cout << "Distro on the top is " << distros.top() << endl;

	distros.pop();
	cout << "The top of the stack is now " << distros.top() << endl;

	/*
	========
	 VECTOR
	========
	*/

	vector <int> numbers;

	if (numbers.empty()){ //check if the vector is empty?
		cout << "The vector is empty :(" << endl;
	}

	for(int i=0; i<100; i+=10){ //Add some values to the vector
		numbers.push_back(i);
	}

	cout << "Size of the vector is " << numbers.size() << endl;

	// iterating over the vector, declaring the iterator
	vector <int>::iterator it;

	cout << "The vector contains: ";
	for (it=numbers.begin(); it!=numbers.end(); it++) {
		cout << "  " << *it;
	}

	// getting value at particular position
	int position = 5;
	cout<<"\nVector at position "<<position<<" contains "<<numbers.at(position)<<endl;

	// deleting an element at position
	numbers.erase(numbers.begin() + position);
	cout<<"Vector at position "<<position<<" contains "<<numbers.at(position)<<endl;

	// deleting a range of elements, first two elements
	// NOTE: You may expect elements at 0, 1 and 2 to be deleted
	// but index 2 is not inclusive.
	numbers.erase(numbers.begin(), numbers.begin()+2);
	cout << "The vector contains: ";
	for (it=numbers.begin(); it!=numbers.end(); it++) {
		cout << "  " << *it;
	}

	// Clearing the vector
	numbers.clear();
	if (numbers.empty()){
		cout << "\nThe vector is now empty again :(";
	}

	/*
	=========
	 HASHMAP
	=========
	*/

	// Declaration <key type, value type>
	map <string, string> companies;

	companies["Google"] = "Larry Page";
	companies["Facebook"] = "Mark Zuckerberg";

	// insertion can also be done as
	companies.insert(pair<string, string> ("Xarvis Tech", "xarvis"));
	// or
	companies.insert(map<string,string>::value_type("Quora", "Adam D'Angelo"));
	// or even
	companies.insert(make_pair(string("Uber"), string("Travis Kalanick")));

	// Iterating the map
	map<string, string>::iterator itz;
	cout << "\n\nCompanies and founders" << endl;
	for (itz=companies.begin(); itz!=companies.end(); itz++){
		cout << "Company: " << (*itz).first << "\t Founder: " << itz->second <<endl;
	}

	itz = companies.find("Google");
	cout << itz->second;
        
        /* Check if key exists!
        if ( m.find("f") == m.end() ) {
              // not found
        } else {
             // found
        }
        */

    /*
    ==============
    LINKED LISTS
    ==============
    */
    list<int> mylist;
    list<int>::iterator it1,it2,itx;

    // set some values:
    for (int i=1; i<10; ++i) mylist.push_back(10*i);

                                // 10 20 30 40 50 60 70 80 90
    it1 = it2 = mylist.begin(); // ^^
    advance (it2,6);            // ^                 ^
    ++it1;                      //    ^              ^

    it1 = mylist.erase (it1);   // 10 30 40 50 60 70 80 90
                                //    ^           ^
		
    it2 = mylist.erase (it2);   // 10 30 40 50 60 80 90
                                //    ^           ^

    ++it1;                      //       ^        ^
    --it2;                      //       ^     ^

    mylist.erase (it1,it2);     // 10 30 60 80 90

    cout << "\nmylist contains:";
    for (itx=mylist.begin(); itx!=mylist.end(); ++itx)
        cout << ' ' << *itx;
    cout << '\n';

    // NOTE: it1 still points to 40, and 60 is not deleted
    cout << endl << *it1 << "\t" << *it2 <<endl;

    // This will print an unexpected value
    it1++;
    cout << *it1;

    cout << "\nmylist now contains:";
    for (it1=mylist.begin(); it1!=mylist.end(); ++it1)
        cout << ' ' << *it1;
    cout << '\n';

    /*
    =======
    HEAPS
    =======
    */

    // Creates a max heap
    priority_queue <int> pq;

    // To create a min heap instead, just uncomment the below line
    // priority_queue <int, vector<int>, greater<int> > pq;

    pq.push(5);
    pq.push(1);
    pq.push(10);
    pq.push(30);
    pq.push(20);

    // Extracting items from the heap
    while (!pq.empty())
    {
        cout << pq.top() << " ";
        pq.pop();
    }

    // creating heap from user defined objects
    // Let's initialize the properties of `Person` object first
    p1.name = "Linus Torvalds";
    p1.age = 47;

    p2.name = "Elon Musk";
    p2.age = 46;

    p3.name = "Me!";
    p3.age = 19;

    // Initialize a min heap
    // Note: We defined a comparator is_older in the beginning to
    // compare the ages of two person.
    priority_queue <struct Person, vector<struct Person>, is_older> mh;
    mh.push(p1);
    mh.push(p2);
    mh.push(p3);

    // Extracting items from the heap
    while (!mh.empty())
    {
    	struct Person p = mh.top();
        cout << p.name << " ";
        mh.pop();
    }

    /*
    =========
    SORTING
    =========
    */

    // list type initialization is only supported after C++11
    // If the style of initialization doesn't work, use the following one
    // static int arr[] = {56, 32, -43, 23, 12, 93, 132, -154};
    // int arr_len = sizeof(arr) / sizeof(arr[0]);
    // vector <int> int_vec(arr, arr + arr_len);
    vector<int> int_vec = {56, 32, -43, 23, 12, 93, 132, -154};

    cout << endl;
    
    // Default: ascending order
    // sort(int_vec.begin(), int_vec.end());
    // sort(int_vec.begin(), int_vec.end(), std::less<int>()); // to be explicit

    // sort in descending order:
    // alternatively, sort(int_vec.begin(), int_vec.end(), greater<int>());
	sort(int_vec.begin(), int_vec.end(), way_to_sort);
    for (vector <int>::iterator i = int_vec.begin(); i!=int_vec.end(); i++)
        cout << *i << " ";
    cout << endl;

    // sorting array
    sort(arr, arr + arr_len);

    // sorting user-defined objects
    static struct Person persons[] = {p1, p2, p3};
    sort(persons, persons+3, compare_names); // sort in alphabetical order

	return 0;
}
```

## Vectors

### Initialisation - Prefer to use “uniform initialisation” over “direct initialisation”

```cpp
std::vector<int> vec1{1, 2, 3, 4};  // Uniform initialization (Preferred)
std::vector<int> vec2(5, 10);       // five elements, each initialized to 10
std::vector<int> vec3(5);           // five elements, each initialized to 0
```

### Custom type vector

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Person {
    std::string name;
    int age;
};

int main() {
    std::vector<Person> people = {{"Alice", 30}, {"Bob", 25}, {"Charlie", 35}};

    std::for_each(people.begin(), people.end(), [](Person &p) {
        p.age += 1;
    });

    for (const auto &p : people) {
        std::cout << p.name << " is " << p.age << " years old." << std::endl;
    }
    // Output:
    // Alice is 31 years old.
    // Bob is 26 years old.
    // Charlie is 36 years old.

    return 0;
}
```

### Summing Elements (int vector sum)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    int sum = 0;

    std::for_each(numbers.begin(), numbers.end(), [&sum](int n) {
        sum += n;
    });

    std::cout << "Sum: " << sum << std::endl;
    return 0;
}
```

or use `std::accumulate`:

```cpp
#include <vector>
#include <numeric>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    int sum = std::accumulate(vec.begin(), vec.end(), 0);

    std::cout << "Sum: " << sum << std::endl;

    return 0;
}
```

### Multiplying Elements

```cpp
#include <vector>
#include <numeric>
#include <iostream>
#include <functional>

int main() {
    std::vector<int> vec{1, 2, 3, 4, 5};
    int product = std::accumulate(vec.begin(), vec.end(), 1, std::multiplies<int>());

    std::cout << "Product: " << product << std::endl;
    return 0;
}

```

### Sorting Elements - std::sort

```cpp
#include <vector>
#include <algorithm>

std::vector<int> vec{3, 1, 4, 1, 5, 9};
std::sort(vec.begin(), vec.end());  // default: ascending order
std::sort(vec.begin(), vec.end(), std::greater<int>()); // descending order
```

Look at <functional> for more useful function objects e.g. `std::greater<int>` :

[https://en.cppreference.com/w/cpp/utility/functional](https://en.cppreference.com/w/cpp/utility/functional)

### Finding Elements - std::find

```cpp
#include <algorithm>

auto it = std::find(vec.begin(), vec.end(), 4);
if (it != vec.end()) {
    // Element found, *it is the value
}
```

```cpp
#include <algorithm>

auto it = std::find_if(vec.begin(), vec.end(), [](int i) { return i > 4; });
if (it != vec.end()) {
    // Found an element greater than 4
}
```

### Counting Elements - std::count (similar to std::find)

```cpp
int count = std::count(vec.begin(), vec.end(), 1);  // Count all occurences of 1's
int count = std::count_if(vec.begin(), vec.end(), [](int i) { return i > 4; });
```

### Removing Elements - std::remove , std::remove_if

```cpp
#include <algorithm>

vec.erase(std::remove(vec.begin(), vec.end(), 1), vec.end()); // Remove all 1's

// Remove
vec.erase(std::remove_if(vec.begin(), vec.end(), [](int i) { return i < 4; }), vec.end());

```

### Removing Duplicates - std::unique / std::erase

```cpp
#include <algorithm>

std::sort(vec.begin(), vec.end());  // we must sort the vector first
vec.erase(std::unique(vec.begin(), vec.end()), vec.end());
```

### Rotating - std::rotate

```cpp
#include <algorithm>

std::rotate(vec.begin(), vec.begin() + 2, vec.end());  // Rotates vec, moving the first two elements to the end
```

### Reverse Order - std::reverse

```cpp
#include <algorithm>

std::reverse(vec.begin(), vec.end());  // Reverses the order of elements in vec
```

### Custom manipulating elements - std::transform

```cpp
#include <algorithm>

// In-place unary transformation: Doubles each element in vec
std::transform(vec.begin(), vec.end(), vec.begin(), [](int i) { return i * 2; });
```

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> vec{1, 2, 3, 4, 5};
    std::vector<int> result(vec.size());  // Transforming into a different container
    
    // Manipulate each element and store in the result vector
    std::transform(vec.begin(), vec.end(), result.begin(), [](int i) { return i * i; });

    for (int v : result) {
        std::cout << v << " ";  // Output: 1 4 9 16 25
    }

    return 0;
}
```

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> vec1{1, 2, 3};
    std::vector<int> vec2{4, 5, 6}; // Binary transformation using two ranges
    std::vector<int> result(vec1.size());

    std::transform(vec1.begin(), vec1.end(), vec2.begin(), result.begin(), std::plus<int>());

    for (int v : result) {
        std::cout << v << " ";  // Output: 5 7 9
    }

    return 0;
}

```

`std::plus<int>()` is a standard binary function object.

Look at <functional> for more useful function objects:

[https://en.cppreference.com/w/cpp/utility/functional](https://en.cppreference.com/w/cpp/utility/functional)

Template Vector

```cpp
#include <vector>
#include <algorithm>

template <typename T>
bool contains(const std::vector<T>& vec, const T& value) {
    return std::find(vec.begin(), vec.end(), value) != vec.end();
}

template <typename T>
void remove(std::vector<T>& vec, const T& value) {
    vec.erase(std::remove(vec.begin(), vec.end(), value), vec.end());
}

template <typename T>
std::vector<T> unique(const std::vector<T>& vec) {
    std::vector<T> result = vec;
    std::sort(result.begin(), result.end());
    auto last = std::unique(result.begin(), result.end());
    result.erase(last, result.end());
    return result;
}

template <typename T>
void sort(std::vector<T>& vec, bool ascending = true) {
    if (ascending) {
        std::sort(vec.begin(), vec.end());
    } else {
        std::sort(vec.begin(), vec.end(), std::greater<T>());
    }
}

template <typename T>
T max_element(const std::vector<T>& vec) {
    return *std::max_element(vec.begin(), vec.end());
}

template <typename T>
T min_element(const std::vector<T>& vec) {
    return *std::min_element(vec.begin(), vec.end());
}

template <typename T>
T sum(const std::vector<T>& vec) {
    return std::accumulate(vec.begin(), vec.end(), T(0));
}

```

.

