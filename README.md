# Cheatsheet

File Input/Output

```cpp
#include <fstream>
#include <sstream>
#include <string>
#include <vector>

ifstream inputFile("input.txt"); 
ofstream outputFile("output.txt");

string line;
while (getline(inputFile, line)) {
    stringstream ss(line);
    string token;
    while (ss >> token) {
        
    }
}

inputFile.close();
outputFile.close();
```

String split by spaces or newlines

```cpp
#include <sstream>
#include <string>
#include <vector>

vector<string> splitString(const string &str) {
    vector<string> tokens;
    stringstream ss(str);
    string token;
    
    while (ss >> token) {
        tokens.push_back(token);
    }
    
    return tokens;
}
```

String Input/Output

```cpp
#include <vector>
#include <string>

vector<string> input = {"10", "20", "sub", "4", "3", "add"};

for (const auto &token : input) {
     // handle each token
}

vector<string> output;
output.push_back("Result: " + to_string(result)); 

for (const auto &line : output) {
    cout << line << endl;
}
```

std::npos - Not found / To the end of the string

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

Floating point (precision)

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
