# Utility Functions

# Conversion Utilities

- `int stringToInt(const std::string& input)`
- `double stringToDouble(const std::string& input)`
- `float stringToFloat(const std::string& input)`
- `bool stringToBool(const std::string& input)`
- `std::string intToString(int input)`
- `std::string doubleToString(double input)`
- `std::string floatToString(float input)`
- `std::string boolToString(bool input)`
- `char stringToChar(const std::string& input)`
- `std::string charToString(char input)`
- `int hexStringToInt(const std::string& input)`
- `std::string intToHexString(int input)`
- `int binaryStringToInt(const std::string& input)`
- `std::string intToBinaryString(int input)`
- `int octalStringToInt(const std::string& input)`
- `std::string intToOctalString(int input)`
- `std::string toUpperCase(const std::string& input)`
- `std::string toLowerCase(const std::string& input)`
- `std::wstring stringToWString(const std::string& input)`
- `std::string wstringToString(const std::wstring& input)`
- `int asciiToInteger(char input)`
- `char integerToAscii(int input)`
- `std::string base64ToHexString(const std::string& input)`
- `std::string hexStringToBase64(const std::string& input)`
- `std::vector<uint8_t> stringToByteArray(const std::string& input)`
- `std::string byteArrayToString(const std::vector<uint8_t>& input)`
- `int romanToInteger(const std::string& input)`
- `std::string integerToRoman(int input)`
- `std::string htmlEntityToString(const std::string& input)`
- `std::string stringToHtmlEntity(const std::string& input)`
- `std::string unixTimestampToString(time_t input)`
- `time_t stringToUnixTimestamp(const std::string& input)`
- `std::string colorCodeToRGB(const std::string& hex)`
- `std::string rgbToColorCode(int r, int g, int b)`
- `std::string htmlColorNameToHex(const std::string& colorName)`
- `std::string hexToHtmlColorName(const std::string& hex)`
- `std::string celsiusToFahrenheit(double celsius)`
- `double fahrenheitToCelsius(double fahrenheit)`
- `double celsiusToKelvin(double celsius)`
- `double kelvinToCelsius(double kelvin)`
- `double milesToKilometers(double miles)`
- `double kilometersToMiles(double kilometers)`
- `double poundsToKilograms(double pounds)`
- `double kilogramsToPounds(double kilograms)`
- `double inchesToCentimeters(double inches)`
- `double centimetersToInches(double centimeters)`
- `double feetToMeters(double feet)`
- `double metersToFeet(double meters)`
- `double yardsToMeters(double yards)`
- `double metersToYards(double meters)`

```cpp
#include <string>
#include <vector>
#include <ctime>
#include <sstream>
#include <iomanip>
#include <algorithm>
#include <cctype>
#include <stdexcept>
#include <cmath>
#include <unordered_map>

// String to primitive type conversions
int stringToInt(const std::string& input) {
    return std::stoi(input);
}

double stringToDouble(const std::string& input) {
    return std::stod(input);
}

float stringToFloat(const std::string& input) {
    return std::stof(input);
}

bool stringToBool(const std::string& input) {
    return (input == "true" || input == "1" || input == "yes");
}

// Primitive type to string conversions
std::string intToString(int input) {
    return std::to_string(input);
}

std::string doubleToString(double input) {
    return std::to_string(input);
}

std::string floatToString(float input) {
    return std::to_string(input);
}

std::string boolToString(bool input) {
    return input ? "true" : "false";
}

// Character conversions
char stringToChar(const std::string& input) {
    return input.empty() ? '\0' : input[0];
}

std::string charToString(char input) {
    return std::string(1, input);
}

// Hexadecimal conversions
int hexStringToInt(const std::string& input) {
    return std::stoi(input, nullptr, 16);
}

std::string intToHexString(int input) {
    std::stringstream ss;
    ss << std::hex << input;
    return ss.str();
}

// Binary conversions
int binaryStringToInt(const std::string& input) {
    return std::stoi(input, nullptr, 2);
}

std::string intToBinaryString(int input) {
    return std::bitset<32>(input).to_string();
}

// Octal conversions
int octalStringToInt(const std::string& input) {
    return std::stoi(input, nullptr, 8);
}

std::string intToOctalString(int input) {
    std::stringstream ss;
    ss << std::oct << input;
    return ss.str();
}

// Case conversions
std::string toUpperCase(const std::string& input) {
    std::string result = input;
    std::transform(result.begin(), result.end(), result.begin(), ::toupper);
    return result;
}

std::string toLowerCase(const std::string& input) {
    std::string result = input;
    std::transform(result.begin(), result.end(), result.begin(), ::tolower);
    return result;
}

// Wide string conversions
std::wstring stringToWString(const std::string& input) {
    return std::wstring(input.begin(), input.end());
}

std::string wstringToString(const std::wstring& input) {
    return std::string(input.begin(), input.end());
}

// ASCII conversions
int asciiToInteger(char input) {
    return static_cast<int>(input);
}

char integerToAscii(int input) {
    return static_cast<char>(input);
}

// Base64 and Hex conversions
// Note: These functions require additional implementation for Base64 encoding/decoding
std::string base64ToHexString(const std::string& input) {
    // Implement Base64 to Hex conversion
    throw std::runtime_error("Not implemented");
}

std::string hexStringToBase64(const std::string& input) {
    // Implement Hex to Base64 conversion
    throw std::runtime_error("Not implemented");
}

// Byte array conversions
std::vector<uint8_t> stringToByteArray(const std::string& input) {
    return std::vector<uint8_t>(input.begin(), input.end());
}

std::string byteArrayToString(const std::vector<uint8_t>& input) {
    return std::string(input.begin(), input.end());
}

// Roman numeral conversions
int romanToInteger(const std::string& input) {
    std::unordered_map<char, int> romanValues = {
        {'I', 1}, {'V', 5}, {'X', 10}, {'L', 50},
        {'C', 100}, {'D', 500}, {'M', 1000}
    };
    
    int result = 0;
    for (size_t i = 0; i < input.length(); ++i) {
        if (i > 0 && romanValues[input[i]] > romanValues[input[i - 1]]) {
            result += romanValues[input[i]] - 2 * romanValues[input[i - 1]];
        } else {
            result += romanValues[input[i]];
        }
    }
    return result;
}

std::string integerToRoman(int input) {
    const std::vector<std::pair<int, std::string>> romanNumerals = {
        {1000, "M"}, {900, "CM"}, {500, "D"}, {400, "CD"},
        {100, "C"}, {90, "XC"}, {50, "L"}, {40, "XL"},
        {10, "X"}, {9, "IX"}, {5, "V"}, {4, "IV"}, {1, "I"}
    };
    
    std::string result;
    for (const auto& pair : romanNumerals) {
        while (input >= pair.first) {
            result += pair.second;
            input -= pair.first;
        }
    }
    return result;
}

// HTML entity conversions
std::string htmlEntityToString(const std::string& input) {
    // Implement HTML entity decoding
    throw std::runtime_error("Not implemented");
}

std::string stringToHtmlEntity(const std::string& input) {
    // Implement HTML entity encoding
    throw std::runtime_error("Not implemented");
}

// Unix timestamp conversions
std::string unixTimestampToString(time_t input) {
    char buffer[30];
    struct tm* timeinfo = localtime(&input);
    strftime(buffer, sizeof(buffer), "%Y-%m-%d %H:%M:%S", timeinfo);
    return std::string(buffer);
}

time_t stringToUnixTimestamp(const std::string& input) {
    struct tm timeinfo = {};
    std::istringstream ss(input);
    ss >> std::get_time(&timeinfo, "%Y-%m-%d %H:%M:%S");
    return mktime(&timeinfo);
}

// Color code conversions
std::string colorCodeToRGB(const std::string& hex) {
    int r = std::stoi(hex.substr(1, 2), nullptr, 16);
    int g = std::stoi(hex.substr(3, 2), nullptr, 16);
    int b = std::stoi(hex.substr(5, 2), nullptr, 16);
    return "rgb(" + std::to_string(r) + "," + std::to_string(g) + "," + std::to_string(b) + ")";
}

std::string rgbToColorCode(int r, int g, int b) {
    std::stringstream ss;
    ss << "#" << std::hex << std::setfill('0') << std::setw(2) << r
       << std::setw(2) << g << std::setw(2) << b;
    return ss.str();
}

// HTML color name conversions
// Note: These functions require a complete mapping of color names to hex codes
std::string htmlColorNameToHex(const std::string& colorName) {
    // Implement color name to hex conversion
    throw std::runtime_error("Not implemented");
}

std::string hexToHtmlColorName(const std::string& hex) {
    // Implement hex to color name conversion
    throw std::runtime_error("Not implemented");
}

// Temperature conversions
std::string celsiusToFahrenheit(double celsius) {
    double fahrenheit = (celsius * 9.0 / 5.0) + 32;
    return std::to_string(fahrenheit) + "°F";
}

double fahrenheitToCelsius(double fahrenheit) {
    return (fahrenheit - 32) * 5.0 / 9.0;
}

double celsiusToKelvin(double celsius) {
    return celsius + 273.15;
}

double kelvinToCelsius(double kelvin) {
    return kelvin - 273.15;
}

// Length conversions
double milesToKilometers(double miles) {
    return miles * 1.60934;
}

double kilometersToMiles(double kilometers) {
    return kilometers / 1.60934;
}

// Weight conversions
double poundsToKilograms(double pounds) {
    return pounds * 0.453592;
}

double kilogramsToPounds(double kilograms) {
    return kilograms / 0.453592;
}

// More length conversions
double inchesToCentimeters(double inches) {
    return inches * 2.54;
}

double centimetersToInches(double centimeters) {
    return centimeters / 2.54;
}

double feetToMeters(double feet) {
    return feet * 0.3048;
}

double metersToFeet(double meters) {
    return meters / 0.3048;
}

double yardsToMeters(double yards) {
    return yards * 0.9144;
}

double metersToYards(double meters) {
    return meters / 0.9144;
}
```

- `double gallonsToLiters(double gallons)`
- `double litersToGallons(double liters)`
- `double psiToPascal(double psi)`
- `double pascalToPsi(double pascal)`
- `double barToPascal(double bar)`
- `double pascalToBar(double pascal)`
- `double knotsToKph(double knots)`
- `double kphToKnots(double kph)`
- `double degreesToRadians(double degrees)`
- `double radiansToDegrees(double radians)`
- `double parsecToLightYears(double parsec)`
- `double lightYearsToParsec(double lightYears)`
- `double gramsToOunces(double grams)`
- `double ouncesToGrams(double ounces)`
- `double joulesToCalories(double joules)`
- `double caloriesToJoules(double calories)`
- `double wattsToHorsepower(double watts)`
- `double horsepowerToWatts(double horsepower)`
- `double lumensToCandela(double lumens)`
- `double candelaToLumens(double candela)`
- `double luxToFootcandles(double lux)`
- `double footcandlesToLux(double footcandles)`
- `double hertzToKilohertz(double hertz)`
- `double kilohertzToHertz(double kilohertz)`
- `double binaryToDecimal(const std::string& binary)`
- `std::string decimalToBinary(int decimal)`
- `double octalToDecimal(const std::string& octal)`
- `std::string decimalToOctal(int decimal)`
- `double hexToDecimal(const std::string& hex)`
- `std::string decimalToHex(int decimal)`
- `std::string binaryToHex(const std::string& binary)`
- `std::string hexToBinary(const std::string& hex)`
- `std::string octalToHex(const std::string& octal)`
- `std::string hexToOctal(const std::string& hex)`
- `std::string ieee754ToHex(float input)`
- `float hexToIEEE754(const std::string& hex)`
- `std::string ieee754ToBinary(float input)`
- `float binaryToIEEE754(const std::string& binary)`
- `std::string encodeToUTF8(const std::wstring& input)`
- `std::wstring decodeFromUTF8(const std::string& input)`
- `std::vector<int> convertStringToAsciiCodes(const std::string& input)`
- `std::string convertAsciiCodesToString(const std::vector<int>& codes)`
- `double mphToKph(double mph)`
- `double kphToMph(double kph)`
- `double nauticalMilesToKilometers(double nauticalMiles)`
- `double kilometersToNauticalMiles(double kilometers)`
- `double tonsToKilograms(double tons)`
- `double kilogramsToTons(double kilograms)`
- `std::string ipToHex(const std::string& ip)`
- `std::string hexToIp(const std::string& hex)`

```cpp
#include <string>
#include <vector>
#include <cmath>
#include <sstream>
#include <iomanip>
#include <bitset>
#include <stdexcept>
#include <regex>
#include <codecvt>
#include <locale>

const double PI = 3.14159265358979323846;

// Volume conversions
double gallonsToLiters(double gallons) {
    return gallons * 3.78541;
}

double litersToGallons(double liters) {
    return liters / 3.78541;
}

// Pressure conversions
double psiToPascal(double psi) {
    return psi * 6894.75729;
}

double pascalToPsi(double pascal) {
    return pascal / 6894.75729;
}

double barToPascal(double bar) {
    return bar * 100000;
}

double pascalToBar(double pascal) {
    return pascal / 100000;
}

// Speed conversions
double knotsToKph(double knots) {
    return knots * 1.852;
}

double kphToKnots(double kph) {
    return kph / 1.852;
}

// Angle conversions
double degreesToRadians(double degrees) {
    return degrees * (PI / 180.0);
}

double radiansToDegrees(double radians) {
    return radians * (180.0 / PI);
}

// Astronomical distance conversions
double parsecToLightYears(double parsec) {
    return parsec * 3.26156;
}

double lightYearsToParsec(double lightYears) {
    return lightYears / 3.26156;
}

// Weight conversions
double gramsToOunces(double grams) {
    return grams / 28.34952;
}

double ouncesToGrams(double ounces) {
    return ounces * 28.34952;
}

// Energy conversions
double joulesToCalories(double joules) {
    return joules / 4.184;
}

double caloriesToJoules(double calories) {
    return calories * 4.184;
}

// Power conversions
double wattsToHorsepower(double watts) {
    return watts / 745.699872;
}

double horsepowerToWatts(double horsepower) {
    return horsepower * 745.699872;
}

// Light conversions
double lumensToCandela(double lumens) {
    // This conversion depends on the solid angle, assuming 1 steradian
    return lumens;
}

double candelaToLumens(double candela) {
    // This conversion depends on the solid angle, assuming 1 steradian
    return candela;
}

double luxToFootcandles(double lux) {
    return lux / 10.7639;
}

double footcandlesToLux(double footcandles) {
    return footcandles * 10.7639;
}

// Frequency conversions
double hertzToKilohertz(double hertz) {
    return hertz / 1000.0;
}

double kilohertzToHertz(double kilohertz) {
    return kilohertz * 1000.0;
}

// Number base conversions
double binaryToDecimal(const std::string& binary) {
    return std::stoll(binary, nullptr, 2);
}

std::string decimalToBinary(int decimal) {
    return std::bitset<32>(decimal).to_string();
}

double octalToDecimal(const std::string& octal) {
    return std::stoll(octal, nullptr, 8);
}

std::string decimalToOctal(int decimal) {
    std::ostringstream oss;
    oss << std::oct << decimal;
    return oss.str();
}

double hexToDecimal(const std::string& hex) {
    return std::stoll(hex, nullptr, 16);
}

std::string decimalToHex(int decimal) {
    std::ostringstream oss;
    oss << std::hex << decimal;
    return oss.str();
}

std::string binaryToHex(const std::string& binary) {
    int decimal = std::stoi(binary, nullptr, 2);
    std::stringstream ss;
    ss << std::hex << decimal;
    return ss.str();
}

std::string hexToBinary(const std::string& hex) {
    int decimal = std::stoi(hex, nullptr, 16);
    return std::bitset<32>(decimal).to_string();
}

std::string octalToHex(const std::string& octal) {
    int decimal = std::stoi(octal, nullptr, 8);
    std::stringstream ss;
    ss << std::hex << decimal;
    return ss.str();
}

std::string hexToOctal(const std::string& hex) {
    int decimal = std::stoi(hex, nullptr, 16);
    std::stringstream ss;
    ss << std::oct << decimal;
    return ss.str();
}

// IEEE 754 conversions
std::string ieee754ToHex(float input) {
    union {
        float f;
        uint32_t i;
    } u;
    u.f = input;
    std::stringstream ss;
    ss << std::hex << std::setfill('0') << std::setw(8) << u.i;
    return ss.str();
}

float hexToIEEE754(const std::string& hex) {
    union {
        float f;
        uint32_t i;
    } u;
    u.i = std::stoul(hex, nullptr, 16);
    return u.f;
}

std::string ieee754ToBinary(float input) {
    union {
        float f;
        uint32_t i;
    } u;
    u.f = input;
    return std::bitset<32>(u.i).to_string();
}

float binaryToIEEE754(const std::string& binary) {
    union {
        float f;
        uint32_t i;
    } u;
    u.i = std::stoul(binary, nullptr, 2);
    return u.f;
}

// UTF-8 conversions
std::string encodeToUTF8(const std::wstring& input) {
    std::wstring_convert<std::codecvt_utf8<wchar_t>> converter;
    return converter.to_bytes(input);
}

std::wstring decodeFromUTF8(const std::string& input) {
    std::wstring_convert<std::codecvt_utf8<wchar_t>> converter;
    return converter.from_bytes(input);
}

// ASCII conversions
std::vector<int> convertStringToAsciiCodes(const std::string& input) {
    std::vector<int> codes;
    for (char c : input) {
        codes.push_back(static_cast<int>(c));
    }
    return codes;
}

std::string convertAsciiCodesToString(const std::vector<int>& codes) {
    std::string result;
    for (int code : codes) {
        result += static_cast<char>(code);
    }
    return result;
}

// Additional speed conversions
double mphToKph(double mph) {
    return mph * 1.60934;
}

double kphToMph(double kph) {
    return kph / 1.60934;
}

// Nautical mile conversions
double nauticalMilesToKilometers(double nauticalMiles) {
    return nauticalMiles * 1.852;
}

double kilometersToNauticalMiles(double kilometers) {
    return kilometers / 1.852;
}

// Ton conversions
double tonsToKilograms(double tons) {
    return tons * 907.18474;
}

double kilogramsToTons(double kilograms) {
    return kilograms / 907.18474;
}

// IP address conversions
std::string ipToHex(const std::string& ip) {
    std::regex ipRegex("(\\d+)\\.(\\d+)\\.(\\d+)\\.(\\d+)");
    std::smatch match;
    if (std::regex_match(ip, match, ipRegex)) {
        std::stringstream ss;
        for (int i = 1; i <= 4; ++i) {
            int octet = std::stoi(match[i]);
            ss << std::hex << std::setw(2) << std::setfill('0') << octet;
        }
        return ss.str();
    }
    throw std::invalid_argument("Invalid IP address format");
}

std::string hexToIp(const std::string& hex) {
    if (hex.length() != 8) {
        throw std::invalid_argument("Invalid hex string length");
    }
    std::stringstream ss;
    for (int i = 0; i < 4; ++i) {
        int octet = std::stoi(hex.substr(i*2, 2), nullptr, 16);
        if (i > 0) ss << ".";
        ss << octet;
    }
    return ss.str();
}
```

# String manipulation

- `std::string toUpperCase(const std::string& str)`
- `std::string toLowerCase(const std::string& str)`
- `std::string trim(const std::string& str)`
- `std::string ltrim(const std::string& str)`
- `std::string rtrim(const std::string& str)`
- `bool startsWith(const std::string& str, const std::string& prefix)`
- `bool endsWith(const std::string& str, const std::string& suffix)`
- `std::string replaceAll(std::string str, const std::string& from, const std::string& to)`
- `std::string replaceFirst(std::string str, const std::string& from, const std::string& to)`
- `std::string replaceLast(std::string str, const std::string& from, const std::string& to)`
- `std::string removeAll(std::string str, const std::string& toRemove)`
- `std::string removeFirst(std::string str, const std::string& toRemove)`
- `std::string removeLast(std::string str, const std::string& toRemove)`
- `std::string reverse(const std::string& str)`
- `std::string join(const std::vector<std::string>& elements, const std::string& delimiter)`
- `std::vector<std::string> split(const std::string& str, const std::string& delimiter)`
- `std::vector<std::string> splitWhitespace(const std::string& str)`
- `std::string repeat(const std::string& str, int times)`
- `std::string capitalize(const std::string& str)`
- `std::string title(const std::string& str)`
- `bool isUpperCase(const std::string& str)`
- `bool isLowerCase(const std::string& str)`
- `bool isDigit(const std::string& str)`
- `bool isAlpha(const std::string& str)`
- `bool isAlphanumeric(const std::string& str)`
- `bool isSpace(const std::string& str)`
- `bool isPunctuation(const std::string& str)`
- `bool contains(const std::string& str, const std::string& substr)`
- `int countOccurrences(const std::string& str, const std::string& substr)`
- `std::string substring(const std::string& str, int start, int length)`

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cctype>
#include <regex>

std::string toUpperCase(const std::string& str) {
    std::string result = str;
    std::transform(result.begin(), result.end(), result.begin(),
                   [](unsigned char c){ return std::toupper(c); });
    return result;
}

std::string toLowerCase(const std::string& str) {
    std::string result = str;
    std::transform(result.begin(), result.end(), result.begin(),
                   [](unsigned char c){ return std::tolower(c); });
    return result;
}

std::string trim(const std::string& str) {
    auto start = str.begin();
    auto end = str.end();
    while (start != end && std::isspace(*start)) ++start;
    do {
        --end;
    } while (start != end && std::isspace(*end));
    return std::string(start, end + 1);
}

std::string ltrim(const std::string& str) {
    auto start = str.begin();
    while (start != str.end() && std::isspace(*start)) ++start;
    return std::string(start, str.end());
}

std::string rtrim(const std::string& str) {
    auto end = str.end();
    do {
        --end;
    } while (end != str.begin() && std::isspace(*end));
    return std::string(str.begin(), end + 1);
}

bool startsWith(const std::string& str, const std::string& prefix) {
    return str.size() >= prefix.size() && str.compare(0, prefix.size(), prefix) == 0;
}

bool endsWith(const std::string& str, const std::string& suffix) {
    return str.size() >= suffix.size() && 
           str.compare(str.size() - suffix.size(), suffix.size(), suffix) == 0;
}

std::string replaceAll(std::string str, const std::string& from, const std::string& to) {
    size_t start_pos = 0;
    while((start_pos = str.find(from, start_pos)) != std::string::npos) {
        str.replace(start_pos, from.length(), to);
        start_pos += to.length();
    }
    return str;
}

std::string replaceFirst(std::string str, const std::string& from, const std::string& to) {
    size_t pos = str.find(from);
    if (pos != std::string::npos) {
        str.replace(pos, from.length(), to);
    }
    return str;
}

std::string replaceLast(std::string str, const std::string& from, const std::string& to) {
    size_t pos = str.rfind(from);
    if (pos != std::string::npos) {
        str.replace(pos, from.length(), to);
    }
    return str;
}

std::string removeAll(std::string str, const std::string& toRemove) {
    return replaceAll(str, toRemove, "");
}

std::string removeFirst(std::string str, const std::string& toRemove) {
    return replaceFirst(str, toRemove, "");
}

std::string removeLast(std::string str, const std::string& toRemove) {
    return replaceLast(str, toRemove, "");
}

std::string reverse(const std::string& str) {
    return std::string(str.rbegin(), str.rend());
}

std::string join(const std::vector<std::string>& elements, const std::string& delimiter) {
    std::string result;
    for (size_t i = 0; i < elements.size(); ++i) {
        result += elements[i];
        if (i < elements.size() - 1) {
            result += delimiter;
        }
    }
    return result;
}

std::vector<std::string> split(const std::string& str, const std::string& delimiter) {
    std::vector<std::string> result;
    size_t start = 0;
    size_t end = str.find(delimiter);
    while (end != std::string::npos) {
        result.push_back(str.substr(start, end - start));
        start = end + delimiter.length();
        end = str.find(delimiter, start);
    }
    result.push_back(str.substr(start));
    return result;
}

std::vector<std::string> splitWhitespace(const std::string& str) {
    std::vector<std::string> result;
    std::istringstream iss(str);
    std::string token;
    while (iss >> token) {
        result.push_back(token);
    }
    return result;
}

std::string repeat(const std::string& str, int times) {
    std::string result;
    result.reserve(str.length() * times);
    for (int i = 0; i < times; ++i) {
        result += str;
    }
    return result;
}

std::string capitalize(const std::string& str) {
    if (str.empty()) return str;
    std::string result = str;
    result[0] = std::toupper(result[0]);
    return result;
}

std::string title(const std::string& str) {
    std::string result = str;
    bool capitalize_next = true;
    for (char& c : result) {
        if (std::isspace(c)) {
            capitalize_next = true;
        } else if (capitalize_next) {
            c = std::toupper(c);
            capitalize_next = false;
        } else {
            c = std::tolower(c);
        }
    }
    return result;
}

bool isUpperCase(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::isupper(c) || !std::isalpha(c); });
}

bool isLowerCase(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::islower(c) || !std::isalpha(c); });
}

bool isDigit(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::isdigit(c); });
}

bool isAlpha(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::isalpha(c); });
}

bool isAlphanumeric(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::isalnum(c); });
}

bool isSpace(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::isspace(c); });
}

bool isPunctuation(const std::string& str) {
    return std::all_of(str.begin(), str.end(), [](unsigned char c){ return std::ispunct(c); });
}

bool contains(const std::string& str, const std::string& substr) {
    return str.find(substr) != std::string::npos;
}

int countOccurrences(const std::string& str, const std::string& substr) {
    int count = 0;
    size_t pos = 0;
    while ((pos = str.find(substr, pos)) != std::string::npos) {
        ++count;
        pos += substr.length();
    }
    return count;
}

std::string substring(const std::string& str, int start, int length) {
    return str.substr(start, length);
}
```

- `std::string removePrefix(const std::string& str, const std::string& prefix)`
- `std::string removeSuffix(const std::string& str, const std::string& suffix)`
- `std::vector<std::string> splitLines(const std::string& str)`
- `std::string joinLines(const std::vector<std::string>& lines)`
- `std::string replaceLineBreaks(const std::string& str, const std::string& replacement)`
- `std::string removeLineBreaks(const std::string& str)`
- `std::string keepAlpha(const std::string& str)`
- `std::string keepDigits(const std::string& str)`
- `std::string keepAlphanumeric(const std::string& str)`
- `std::string removeDigits(const std::string& str)`
- `std::string swapFirstAndLast(const std::string& str)`
- `std::string swapFirstAndLastWords(const std::string& str)`
- `std::string extractFirstWord(const std::string& str)`
- `std::string extractLastWord(const std::string& str)`
- `std::string stripQuotes(const std::string& str)`
- `std::string wrapWithQuotes(const std::string& str)`
- `std::string encloseInBrackets(const std::string& str)`
- `std::string encloseInParentheses(const std::string& str)`
- `std::string encloseInCurlyBraces(const std::string& str)`
- `std::string replaceWordAt(const std::string& str, int wordIndex, const std::string& replacement)`
- `std::string insertWordAt(const std::string& str, int wordIndex, const std::string& toInsert)`
- `std::string eraseWordAt(const std::string& str, int wordIndex)`
- `std::string replaceNthOccurrence(std::string str, const std::string& from, const std::string& to, int n)`
- `std::string rotateWordsLeft(const std::string& str, int n)`
- `std::string rotateWordsRight(const std::string& str, int n)`
- `std::string reverseWordOrder(const std::string& str)`
- `std::string sortWordsAlphabetically(const std::string& str)`
- `std::string sortWordsByLength(const std::string& str)`
- `std::string capitalizeWords(const std::string& str)`
- `std::string decapitalizeWords(const std::string& str)`
- `std::string toggleCase(const std::string& str)`
- `std::string transposeCharacters(const std::string& str)`
- `std::string swapAdjacentCharacters(const std::string& str)`
- `std::string swapAdjacentWords(const std::string& str)`
- `std::string findAndReplaceAllWords(std::string str, const std::string& from, const std::string& to)`
- `std::string replaceFirstWord(std::string str, const std::string& from, const std::string& to)`
- `std::string replaceLastWord(std::string str, const std::string& from, const std::string& to)`

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <sstream>
#include <cctype>
#include <regex>
#include <random>

std::string removePrefix(const std::string& str, const std::string& prefix) {
    if (str.substr(0, prefix.length()) == prefix) {
        return str.substr(prefix.length());
    }
    return str;
}

std::string removeSuffix(const std::string& str, const std::string& suffix) {
    if (str.length() >= suffix.length() && str.substr(str.length() - suffix.length()) == suffix) {
        return str.substr(0, str.length() - suffix.length());
    }
    return str;
}

std::vector<std::string> splitLines(const std::string& str) {
    std::vector<std::string> lines;
    std::istringstream iss(str);
    std::string line;
    while (std::getline(iss, line)) {
        lines.push_back(line);
    }
    return lines;
}

std::string joinLines(const std::vector<std::string>& lines) {
    std::ostringstream oss;
    for (size_t i = 0; i < lines.size(); ++i) {
        if (i > 0) oss << '\n';
        oss << lines[i];
    }
    return oss.str();
}

std::string replaceLineBreaks(const std::string& str, const std::string& replacement) {
    std::string result = str;
    std::regex lineBreaks("\r\n|\n|\r");
    return std::regex_replace(result, lineBreaks, replacement);
}

std::string removeLineBreaks(const std::string& str) {
    return replaceLineBreaks(str, "");
}

std::string keepAlpha(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result), 
                 [](char c) { return std::isalpha(c); });
    return result;
}

std::string keepDigits(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result), 
                 [](char c) { return std::isdigit(c); });
    return result;
}

std::string keepAlphanumeric(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result), 
                 [](char c) { return std::isalnum(c); });
    return result;
}

std::string removeDigits(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result), 
                 [](char c) { return !std::isdigit(c); });
    return result;
}

std::string swapFirstAndLast(const std::string& str) {
    if (str.length() < 2) return str;
    std::string result = str;
    std::swap(result.front(), result.back());
    return result;
}

std::string swapFirstAndLastWords(const std::string& str) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (words.size() < 2) return str;
    std::swap(words.front(), words.back());
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string extractFirstWord(const std::string& str) {
    std::istringstream iss(str);
    std::string word;
    iss >> word;
    return word;
}

std::string extractLastWord(const std::string& str) {
    std::istringstream iss(str);
    std::string word, last;
    while (iss >> word) {
        last = word;
    }
    return last;
}

std::string stripQuotes(const std::string& str) {
    if (str.length() >= 2 && 
        ((str.front() == '\'' && str.back() == '\'') || 
         (str.front() == '\"' && str.back() == '\"'))) {
        return str.substr(1, str.length() - 2);
    }
    return str;
}

std::string wrapWithQuotes(const std::string& str) {
    return "\"" + str + "\"";
}

std::string encloseInBrackets(const std::string& str) {
    return "[" + str + "]";
}

std::string encloseInParentheses(const std::string& str) {
    return "(" + str + ")";
}

std::string encloseInCurlyBraces(const std::string& str) {
    return "{" + str + "}";
}

std::string replaceWordAt(const std::string& str, int wordIndex, const std::string& replacement) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (wordIndex >= 0 && wordIndex < static_cast<int>(words.size())) {
        words[wordIndex] = replacement;
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string insertWordAt(const std::string& str, int wordIndex, const std::string& toInsert) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (wordIndex >= 0 && wordIndex <= static_cast<int>(words.size())) {
        words.insert(words.begin() + wordIndex, toInsert);
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string eraseWordAt(const std::string& str, int wordIndex) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (wordIndex >= 0 && wordIndex < static_cast<int>(words.size())) {
        words.erase(words.begin() + wordIndex);
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string replaceNthOccurrence(std::string str, const std::string& from, const std::string& to, int n) {
    size_t pos = str.find(from);
    int count = 1;
    while (pos != std::string::npos && count < n) {
        pos = str.find(from, pos + 1);
        ++count;
    }
    if (pos != std::string::npos) {
        str.replace(pos, from.length(), to);
    }
    return str;
}

std::string rotateWordsLeft(const std::string& str, int n) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (!words.empty()) {
        n %= words.size();
        std::rotate(words.begin(), words.begin() + n, words.end());
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string rotateWordsRight(const std::string& str, int n) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    if (!words.empty()) {
        n %= words.size();
        std::rotate(words.rbegin(), words.rbegin() + n, words.rend());
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string reverseWordOrder(const std::string& str) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    std::reverse(words.begin(), words.end());
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string sortWordsAlphabetically(const std::string& str) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    std::sort(words.begin(), words.end());
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string sortWordsByLength(const std::string& str) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    std::sort(words.begin(), words.end(), 
              [](const std::string& a, const std::string& b) { 
                  return a.length() < b.length(); 
              });
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string capitalizeWords(const std::string& str) {
    std::istringstream iss(str);
    std::ostringstream oss;
    std::string word;
    while (iss >> word) {
        if (!word.empty()) {
            word[0] = std::toupper(word[0]);
        }
        oss << word << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string decapitalizeWords(const std::string& str) {
    std::istringstream iss(str);
    std::ostringstream oss;
    std::string word;
    while (iss >> word) {
        if (!word.empty()) {
            word[0] = std::tolower(word[0]);
        }
        oss << word << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string toggleCase(const std::string& str) {
    std::string result = str;
    for (char& c : result) {
        if (std::islower(c)) {
            c = std::toupper(c);
        } else if (std::isupper(c)) {
            c = std::tolower(c);
        }
    }
    return result;
}

std::string transposeCharacters(const std::string& str) {
    std::string result = str;
    for (size_t i = 0; i < result.length() - 1; i += 2) {
        std::swap(result[i], result[i + 1]);
    }
    return result;
}

std::string swapAdjacentCharacters(const std::string& str) {
    return transposeCharacters(str);
}

std::string swapAdjacentWords(const std::string& str) {
    std::istringstream iss(str);
    std::vector<std::string> words;
    std::string word;
    while (iss >> word) {
        words.push_back(word);
    }
    for (size_t i = 0; i < words.size() - 1; i += 2) {
        std::swap(words[i], words[i + 1]);
    }
    std::ostringstream oss;
    for (const auto& w : words) {
        oss << w << ' ';
    }
    std::string result = oss.str();
    if (!result.empty()) result.pop_back(); // Remove trailing space
    return result;
}

std::string findAndReplaceAllWords(std::string str, const std::string& from, const std::string& to) {
    std::regex word_regex("\\b" + from + "\\b");
    return std::regex_replace(str, word_regex, to);
}

std::string replaceFirstWord(std::string str, const std::string& from, const std::string& to) {
    std::regex word_regex("\\b" + from + "\\b");
    std::smatch match;
    if (std::regex_search(str, match, word_regex)) {
        str.replace(match.position(), match.length(), to);
    }
    return str;
}

std::string replaceLastWord(std::string str, const std::string& from, const std::string& to) {
    std::regex word_regex("\\b" + from + "\\b");
    std::smatch match;
    std::string::const_reverse_iterator search_start(str.end());
    if (std::regex_search(search_start, str.rend(), match, word_regex)) {
        auto rpos = match.position();
        str.replace(str.length() - rpos - match.length(), match.length(), to);
    }
    return str;
}
```

- `std::string padLeft(const std::string& str, int totalLength, char padChar = ' ')`
- `std::string padRight(const std::string& str, int totalLength, char padChar = ' ')`
- `std::string padCenter(const std::string& str, int totalLength, char padChar = ' ')`
- `std::string removeDuplicates(const std::string& str)`
- `std::string removeWhitespace(const std::string& str)`
- `std::string removeNonAlpha(const std::string& str)`
- `std::string removeNonAlphanumeric(const std::string& str)`
- `std::string removeNonDigits(const std::string& str)`
- `std::string removePunctuation(const std::string& str)`
- `std::string removeVowels(const std::string& str)`
- `std::string removeConsonants(const std::string& str)`
- `std::string insertAt(const std::string& str, const std::string& toInsert, int position)`
- `std::string eraseAt(std::string str, int position, int length)`
- `std::string swapCase(const std::string& str)`
- `std::string replaceSpacesWithUnderscore(const std::string& str)`
- `std::string removeDuplicateSpaces(const std::string& str)`
- `bool equalsIgnoreCase(const std::string& str1, const std::string& str2)`
- `std::string stripAccents(const std::string& str)`
- `bool isPalindrome(const std::string& str)`
- `std::string interleave(const std::string& str1, const std::string& str2)`
- `std::string reverseWords(const std::string& str)`
- `std::string reverseEachWord(const std::string& str)`

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cctype>
#include <regex>
#include <random>
#include <sstream>
#include <iomanip>
#include <cmath>
#include <unordered_map>
#include <boost/uuid/uuid.hpp>
#include <boost/uuid/uuid_generators.hpp>
#include <boost/uuid/uuid_io.hpp>
#include <boost/algorithm/string.hpp>

std::string padLeft(const std::string& str, int totalLength, char padChar = ' ') {
    if (totalLength <= str.length()) return str;
    return std::string(totalLength - str.length(), padChar) + str;
}

std::string padRight(const std::string& str, int totalLength, char padChar = ' ') {
    if (totalLength <= str.length()) return str;
    return str + std::string(totalLength - str.length(), padChar);
}

std::string padCenter(const std::string& str, int totalLength, char padChar = ' ') {
    if (totalLength <= str.length()) return str;
    int leftPad = (totalLength - str.length()) / 2;
    int rightPad = totalLength - str.length() - leftPad;
    return std::string(leftPad, padChar) + str + std::string(rightPad, padChar);
}

std::string removeDuplicates(const std::string& str) {
    std::string result;
    std::unordered_set<char> seen;
    for (char c : str) {
        if (seen.insert(c).second) {
            result += c;
        }
    }
    return result;
}

std::string removeWhitespace(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return !std::isspace(c); });
    return result;
}

std::string removeNonAlpha(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isalpha(c); });
    return result;
}

std::string removeNonAlphanumeric(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isalnum(c); });
    return result;
}

std::string removeNonDigits(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isdigit(c); });
    return result;
}

std::string removePunctuation(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return !std::ispunct(c); });
    return result;
}

std::string removeVowels(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::string("aeiouAEIOU").find(c) == std::string::npos; });
    return result;
}

std::string removeConsonants(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::string("aeiouAEIOU").find(c) != std::string::npos || !std::isalpha(c); });
    return result;
}

std::string insertAt(const std::string& str, const std::string& toInsert, int position) {
    if (position < 0 || position > str.length()) return str;
    return str.substr(0, position) + toInsert + str.substr(position);
}

std::string eraseAt(std::string str, int position, int length) {
    if (position < 0 || position >= str.length()) return str;
    return str.erase(position, length);
}

std::string swapCase(const std::string& str) {
    std::string result = str;
    for (char& c : result) {
        if (std::islower(c)) c = std::toupper(c);
        else if (std::isupper(c)) c = std::tolower(c);
    }
    return result;
}

std::string replaceSpacesWithUnderscore(const std::string& str) {
    std::string result = str;
    std::replace(result.begin(), result.end(), ' ', '_');
    return result;
}

std::string removeDuplicateSpaces(const std::string& str) {
    std::string result;
    bool lastWasSpace = false;
    for (char c : str) {
        if (!std::isspace(c) || !lastWasSpace) {
            result += c;
        }
        lastWasSpace = std::isspace(c);
    }
    return result;
}

bool equalsIgnoreCase(const std::string& str1, const std::string& str2) {
    return boost::iequals(str1, str2);
}

std::string stripAccents(const std::string& str) {
    // This is a simplified version and doesn't cover all possible accents
    static const std::unordered_map<char, char> accentMap = {
        {'à', 'a'}, {'á', 'a'}, {'â', 'a'}, {'ã', 'a'}, {'ä', 'a'}, {'å', 'a'},
        {'è', 'e'}, {'é', 'e'}, {'ê', 'e'}, {'ë', 'e'},
        {'ì', 'i'}, {'í', 'i'}, {'î', 'i'}, {'ï', 'i'},
        {'ò', 'o'}, {'ó', 'o'}, {'ô', 'o'}, {'õ', 'o'}, {'ö', 'o'},
        {'ù', 'u'}, {'ú', 'u'}, {'û', 'u'}, {'ü', 'u'},
        {'ý', 'y'}, {'ÿ', 'y'}, {'ñ', 'n'}
    };

    std::string result;
    for (char c : str) {
        auto it = accentMap.find(std::tolower(c));
        if (it != accentMap.end()) {
            result += it->second;
        } else {
            result += c;
        }
    }
    return result;
}

bool isPalindrome(const std::string& str) {
    std::string cleaned;
    std::copy_if(str.begin(), str.end(), std::back_inserter(cleaned),
                 [](char c) { return std::isalnum(c); });
    std::transform(cleaned.begin(), cleaned.end(), cleaned.begin(), ::tolower);
    return cleaned == std::string(cleaned.rbegin(), cleaned.rend());
}

std::string interleave(const std::string& str1, const std::string& str2) {
    std::string result;
    size_t maxLength = std::max(str1.length(), str2.length());
    for (size_t i = 0; i < maxLength; ++i) {
        if (i < str1.length()) result += str1[i];
        if (i < str2.length()) result += str2[i];
    }
    return result;
}

std::string reverseWords(const std::string& str) {
    std::vector<std::string> words;
    boost::split(words, str, boost::is_any_of(" "), boost::token_compress_on);
    std::reverse(words.begin(), words.end());
    return boost::join(words, " ");
}

std::string reverseEachWord(const std::string& str) {
    std::vector<std::string> words;
    boost::split(words, str, boost::is_any_of(" "), boost::token_compress_on);
    for (auto& word : words) {
        std::reverse(word.begin(), word.end());
    }
    return boost::join(words, " ");
}
```

- `std::string toCamelCase(const std::string& str)`
- `std::string toSnakeCase(const std::string& str)`
- `std::string toKebabCase(const std::string& str)`
- `std::string toPascalCase(const std::string& str)`
- `std::string removeHtmlTags(const std::string& str)`
- `std::string extractNumbers(const std::string& str)`
- `std::string extractLetters(const std::string& str)`
- `std::string extractAlphanumeric(const std::string& str)`
- `std::vector<std::string> findAllOccurrences(const std::string& str, const std::string& substr)`
- `int indexOf(const std::string& str, const std::string& substr)`
- `int lastIndexOf(const std::string& str, const std::string& substr)`
- `bool isEmpty(const std::string& str)`
- `std::string intToString(int value)`
- `int stringToInt(const std::string& str)`
- `std::string floatToString(float value, int precision = 2)`
- `float stringToFloat(const std::string& str)`
- `std::string doubleToString(double value, int precision = 2)`
- `double stringToDouble(const std::string& str)`
- `std::string removeControlCharacters(const std::string& str)`
- `std::string rotateLeft(const std::string& str, int n)`
- `std::string rotateRight(const std::string& str, int n)`
- `std::string shuffleString(const std::string& str)`
- `std::string toBinaryString(int number)`
- `int binaryStringToInt(const std::string& str)`
- `std::string toHexString(int number)`
- `int hexStringToInt(const std::string& str)`
- `std::string toOctalString(int number)`
- `int octalStringToInt(const std::string& str)`
- `std::string toRomanNumerals(int number)`
- `int romanNumeralsToInt(const std::string& str)`
- `std::string addCommasToNumericString(const std::string& str)`
- `std::string toCurrencyFormat(const std::string& str, const std::string& currencySymbol)`
- `std::string removeNonPrintableCharacters(const std::string& str)`
- `std::string wrapText(const std::string& str, int lineWidth)`
- `std::string obfuscateString(const std::string& str)`
- `std::string maskString(const std::string& str, char maskChar = '*')`
- `std::string obfuscateEmail(const std::string& email)`
- `std::string generateUUID()`
- `std::string repeatEachCharacter(const std::string& str, int times)`

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cctype>
#include <regex>
#include <random>
#include <sstream>
#include <iomanip>
#include <cmath>
#include <unordered_map>
#include <boost/uuid/uuid.hpp>
#include <boost/uuid/uuid_generators.hpp>
#include <boost/uuid/uuid_io.hpp>
#include <boost/algorithm/string.hpp>

std::string toCamelCase(const std::string& str) {
    std::string result;
    bool capitalizeNext = false;
    for (char c : str) {
        if (std::isalnum(c)) {
            if (capitalizeNext) {
                result += std::toupper(c);
                capitalizeNext = false;
            } else {
                result += std::tolower(c);
            }
        } else {
            capitalizeNext = true;
        }
    }
    return result;
}

std::string toSnakeCase(const std::string& str) {
    std::string result;
    bool lastWasUpper = false;
    for (size_t i = 0; i < str.length(); ++i) {
        if (std::isupper(str[i])) {
            if (i > 0 && !lastWasUpper) {
                result += '_';
            }
            result += std::tolower(str[i]);
            lastWasUpper = true;
        } else {
            result += std::tolower(str[i]);
            lastWasUpper = false;
        }
    }
    return result;
}

std::string toKebabCase(const std::string& str) {
    std::string result;
    bool lastWasUpper = false;
    for (size_t i = 0; i < str.length(); ++i) {
        if (std::isupper(str[i])) {
            if (i > 0 && !lastWasUpper) {
                result += '-';
            }
            result += std::tolower(str[i]);
            lastWasUpper = true;
        } else {
            result += std::tolower(str[i]);
            lastWasUpper = false;
        }
    }
    return result;
}

std::string toPascalCase(const std::string& str) {
    std::string result;
    bool capitalizeNext = true;
    for (char c : str) {
        if (std::isalnum(c)) {
            if (capitalizeNext) {
                result += std::toupper(c);
                capitalizeNext = false;
            } else {
                result += std::tolower(c);
            }
        } else {
            capitalizeNext = true;
        }
    }
    return result;
}

std::string removeHtmlTags(const std::string& str) {
    std::regex html_tag("<[^>]*>");
    return std::regex_replace(str, html_tag, "");
}

std::string extractNumbers(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isdigit(c); });
    return result;
}

std::string extractLetters(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isalpha(c); });
    return result;
}

std::string extractAlphanumeric(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isalnum(c); });
    return result;
}

std::vector<std::string> findAllOccurrences(const std::string& str, const std::string& substr) {
    std::vector<std::string> result;
    size_t pos = str.find(substr);
    while (pos != std::string::npos) {
        result.push_back(str.substr(pos, substr.length()));
        pos = str.find(substr, pos + 1);
    }
    return result;
}

int indexOf(const std::string& str, const std::string& substr) {
    size_t pos = str.find(substr);
    return (pos != std::string::npos) ? static_cast<int>(pos) : -1;
}

int lastIndexOf(const std::string& str, const std::string& substr) {
    size_t pos = str.rfind(substr);
    return (pos != std::string::npos) ? static_cast<int>(pos) : -1;
}

bool isEmpty(const std::string& str) {
    return str.empty();
}

std::string intToString(int value) {
    return std::to_string(value);
}

int stringToInt(const std::string& str) {
    return std::stoi(str);
}

std::string floatToString(float value, int precision = 2) {
    std::ostringstream oss;
    oss << std::fixed << std::setprecision(precision) << value;
    return oss.str();
}

float stringToFloat(const std::string& str) {
    return std::stof(str);
}

std::string doubleToString(double value, int precision = 2) {
    std::ostringstream oss;
    oss << std::fixed << std::setprecision(precision) << value;
    return oss.str();
}

double stringToDouble(const std::string& str) {
    return std::stod(str);
}

std::string removeControlCharacters(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return c >= 32 && c != 127; });
    return result;
}

std::string rotateLeft(const std::string& str, int n) {
    if (str.empty()) return str;
    n %= str.length();
    return str.substr(n) + str.substr(0, n);
}

std::string rotateRight(const std::string& str, int n) {
    if (str.empty()) return str;
    n %= str.length();
    return str.substr(str.length() - n) + str.substr(0, str.length() - n);
}

std::string shuffleString(const std::string& str) {
    std::string result = str;
    std::random_device rd;
    std::mt19937 g(rd());
    std::shuffle(result.begin(), result.end(), g);
    return result;
}

std::string toBinaryString(int number) {
    return std::bitset<32>(number).to_string();
}

int binaryStringToInt(const std::string& str) {
    return std::bitset<32>(str).to_ulong();
}

std::string toHexString(int number) {
    std::ostringstream oss;
    oss << std::hex << number;
    return oss.str();
}

int hexStringToInt(const std::string& str) {
    int result;
    std::istringstream(str) >> std::hex >> result;
    return result;
}

std::string toOctalString(int number) {
    std::ostringstream oss;
    oss << std::oct << number;
    return oss.str();
}

int octalStringToInt(const std::string& str) {
    int result;
    std::istringstream(str) >> std::oct >> result;
    return result;
}

std::string toRomanNumerals(int number) {
    const std::vector<std::pair<int, std::string>> roman = {
        {1000, "M"}, {900, "CM"}, {500, "D"}, {400, "CD"}, {100, "C"}, 
        {90, "XC"}, {50, "L"}, {40, "XL"}, {10, "X"}, {9, "IX"}, 
        {5, "V"}, {4, "IV"}, {1, "I"}
    };
    
    std::string result;
    for (const auto& p : roman) {
        while (number >= p.first) {
            result += p.second;
            number -= p.first;
        }
    }
    return result;
}

int romanNumeralsToInt(const std::string& str) {
    std::unordered_map<char, int> romanMap = {
        {'I', 1}, {'V', 5}, {'X', 10}, {'L', 50},
        {'C', 100}, {'D', 500}, {'M', 1000}
    };
    
    int result = 0;
    for (size_t i = 0; i < str.length(); ++i) {
        if (i > 0 && romanMap[str[i]] > romanMap[str[i-1]]) {
            result += romanMap[str[i]] - 2 * romanMap[str[i-1]];
        } else {
            result += romanMap[str[i]];
        }
    }
    return result;
}

std::string addCommasToNumericString(const std::string& str) {
    std::string result;
    int count = 0;
    for (auto it = str.rbegin(); it != str.rend(); ++it) {
        if (count && count % 3 == 0) {
            result = ',' + result;
        }
        result = *it + result;
        ++count;
    }
    return result;
}

std::string toCurrencyFormat(const std::string& str, const std::string& currencySymbol) {
    std::string numericPart = extractNumbers(str);
    return currencySymbol + addCommasToNumericString(numericPart);
}

std::string removeNonPrintableCharacters(const std::string& str) {
    std::string result;
    std::copy_if(str.begin(), str.end(), std::back_inserter(result),
                 [](char c) { return std::isprint(c); });
    return result;
}

std::string wrapText(const std::string& str, int lineWidth) {
    std::istringstream words(str);
    std::ostringstream wrapped;
    std::string word;

    if (words >> word) {
        wrapped << word;
        int lineLength = word.length();

        while (words >> word) {
            if (lineLength + word.length() + 1 > lineWidth) {
                wrapped << '\n' << word;
                lineLength = word.length();
            } else {
                wrapped << ' ' << word;
                lineLength += word.length() + 1;
            }
        }
    }
    return wrapped.str();
}

std::string obfuscateString(const std::string& str) {
    std::string result;
    for (char c : str) {
        result += std::to_string(static_cast<int>(c)) + " ";
    }
    return result;
}

std::string maskString(const std::string& str, char maskChar = '*') {
    if (str.length() <= 4) return std::string(str.length(), maskChar);
    return str.substr(0, 2) + std::string(str.length() - 4, maskChar) + str.substr(str.length() - 2);
}

std::string obfuscateEmail(const std::string& email) {
    size_t atPos = email.find('@');
    if (atPos == std::string::npos) return email;
    
    std::string localPart = email.substr(0, atPos);
    std::string domainPart = email.substr(atPos + 1);
    
    return maskString(localPart) + "@" + maskString(domainPart);
}

std::string generateUUID() {
    boost::uuids::random_generator gen;
    boost::uuids::uuid uuid = gen();
    return boost::uuids::to_string(uuid);
}

std::string repeatEachCharacter(const std::string& str, int times) {
    std::string result;
    for (char c : str) {
        result.append(times, c);
    }
    return result;
}
```

# HEX/BINARY CONVERSION UTILITY

- `std::string hexToBinary(const std::string& hex)`
- `std::string binaryToHex(const std::string& binary)`
- `int hexToDecimal(const std::string& hex)`
- `std::string decimalToHex(int decimal)`
- `int binaryToDecimal(const std::string& binary)`
- `std::string decimalToBinary(int decimal)`
- `std::string hexToOctal(const std::string& hex)`
- `std::string octalToHex(const std::string& octal)`
- `std::string binaryToOctal(const std::string& binary)`
- `std::string octalToBinary(const std::string& octal)`
- `std::string hexToAscii(const std::string& hex)`
- `std::string asciiToHex(const std::string& ascii)`
- `std::string binaryToAscii(const std::string& binary)`
- `std::string asciiToBinary(const std::string& ascii)`
- `std::string hexToUtf8(const std::string& hex)`
- `std::string utf8ToHex(const std::string& utf8)`
- `std::string binaryToUtf8(const std::string& binary)`
- `std::string utf8ToBinary(const std::string& utf8)`
- `std::string hexToBase64(const std::string& hex)`
- `std::string base64ToHex(const std::string& base64)`
- `std::string binaryToBase64(const std::string& binary)`
- `std::string base64ToBinary(const std::string& base64)`
- `std::string hexToUuid(const std::string& hex)`
- `std::string uuidToHex(const std::string& uuid)`
- `std::string binaryToUuid(const std::string& binary)`
- `std::string uuidToBinary(const std::string& uuid)`
- `std::string hexToIPAddress(const std::string& hex)`
- `std::string ipAddressToHex(const std::string& ip)`
- `std::string binaryToIPAddress(const std::string& binary)`
- `std::string ipAddressToBinary(const std::string& ip)`
- `std::string hexToMacAddress(const std::string& hex)`
- `std::string macAddressToHex(const std::string& mac)`
- `std::string binaryToMacAddress(const std::string& binary)`
- `std::string macAddressToBinary(const std::string& mac)`
- `std::string hexToRgba(const std::string& hex)`
- `std::string rgbaToHex(int r, int g, int b, int a)`
- `std::string binaryToRgba(const std::string& binary)`
- `std::string rgbaToBinary(int r, int g, int b, int a)`
- `std::string hexToColorName(const std::string& hex)`
- `std::string colorNameToHex(const std::string& colorName)`
- `std::string binaryToColorName(const std::string& binary)`
- `std::string colorNameToBinary(const std::string& colorName)`

```cpp
#include <string>
#include <sstream>
#include <iomanip>
#include <algorithm>
#include <unordered_map>
#include <vector>
#include <cstdint>
#include <bitset>
#include <boost/uuid/uuid.hpp>
#include <boost/uuid/uuid_io.hpp>
#include <boost/algorithm/string.hpp>

std::string hexToBinary(const std::string& hex) {
    std::string binary;
    for (char c : hex) {
        int value = (c >= '0' && c <= '9') ? c - '0' : std::tolower(c) - 'a' + 10;
        binary += std::bitset<4>(value).to_string();
    }
    return binary;
}

std::string binaryToHex(const std::string& binary) {
    std::stringstream ss;
    for (size_t i = 0; i < binary.length(); i += 4) {
        std::bitset<4> bits(binary.substr(i, 4));
        ss << std::hex << bits.to_ulong();
    }
    return ss.str();
}

int hexToDecimal(const std::string& hex) {
    return std::stoi(hex, nullptr, 16);
}

std::string decimalToHex(int decimal) {
    std::stringstream ss;
    ss << std::hex << decimal;
    return ss.str();
}

int binaryToDecimal(const std::string& binary) {
    return std::stoi(binary, nullptr, 2);
}

std::string decimalToBinary(int decimal) {
    return std::bitset<32>(decimal).to_string();
}

std::string hexToOctal(const std::string& hex) {
    int decimal = hexToDecimal(hex);
    std::stringstream ss;
    ss << std::oct << decimal;
    return ss.str();
}

std::string octalToHex(const std::string& octal) {
    int decimal = std::stoi(octal, nullptr, 8);
    return decimalToHex(decimal);
}

std::string binaryToOctal(const std::string& binary) {
    int decimal = binaryToDecimal(binary);
    std::stringstream ss;
    ss << std::oct << decimal;
    return ss.str();
}

std::string octalToBinary(const std::string& octal) {
    int decimal = std::stoi(octal, nullptr, 8);
    return decimalToBinary(decimal);
}

std::string hexToAscii(const std::string& hex) {
    std::string ascii;
    for (size_t i = 0; i < hex.length(); i += 2) {
        std::string byte = hex.substr(i, 2);
        char c = static_cast<char>(std::stoi(byte, nullptr, 16));
        ascii += c;
    }
    return ascii;
}

std::string asciiToHex(const std::string& ascii) {
    std::stringstream ss;
    for (char c : ascii) {
        ss << std::hex << std::setw(2) << std::setfill('0') << static_cast<int>(c);
    }
    return ss.str();
}

std::string binaryToAscii(const std::string& binary) {
    std::string ascii;
    for (size_t i = 0; i < binary.length(); i += 8) {
        std::bitset<8> bits(binary.substr(i, 8));
        ascii += static_cast<char>(bits.to_ulong());
    }
    return ascii;
}

std::string asciiToBinary(const std::string& ascii) {
    std::string binary;
    for (char c : ascii) {
        binary += std::bitset<8>(c).to_string();
    }
    return binary;
}

std::string hexToUtf8(const std::string& hex) {
    // This is a simplified version and may not cover all UTF-8 cases
    return hexToAscii(hex);
}

std::string utf8ToHex(const std::string& utf8) {
    // This is a simplified version and may not cover all UTF-8 cases
    return asciiToHex(utf8);
}

std::string binaryToUtf8(const std::string& binary) {
    // This is a simplified version and may not cover all UTF-8 cases
    return binaryToAscii(binary);
}

std::string utf8ToBinary(const std::string& utf8) {
    // This is a simplified version and may not cover all UTF-8 cases
    return asciiToBinary(utf8);
}

std::string hexToBase64(const std::string& hex) {
    static const std::string base64_chars = 
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
    
    std::string binary = hexToBinary(hex);
    std::string base64;
    
    for (size_t i = 0; i < binary.length(); i += 6) {
        std::bitset<6> bits(binary.substr(i, 6));
        base64 += base64_chars[bits.to_ulong()];
    }
    
    while (base64.length() % 4 != 0) {
        base64 += '=';
    }
    
    return base64;
}

std::string base64ToHex(const std::string& base64) {
    static const std::string base64_chars = 
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";
    
    std::string binary;
    for (char c : base64) {
        if (c == '=') break;
        size_t index = base64_chars.find(c);
        binary += std::bitset<6>(index).to_string();
    }
    
    return binaryToHex(binary);
}

std::string binaryToBase64(const std::string& binary) {
    return hexToBase64(binaryToHex(binary));
}

std::string base64ToBinary(const std::string& base64) {
    return hexToBinary(base64ToHex(base64));
}

std::string hexToUuid(const std::string& hex) {
    if (hex.length() != 32) throw std::invalid_argument("Invalid hex length for UUID");
    std::string uuid = hex;
    uuid.insert(8, "-");
    uuid.insert(13, "-");
    uuid.insert(18, "-");
    uuid.insert(23, "-");
    return uuid;
}

std::string uuidToHex(const std::string& uuid) {
    std::string hex = uuid;
    boost::erase_all(hex, "-");
    if (hex.length() != 32) throw std::invalid_argument("Invalid UUID format");
    return hex;
}

std::string binaryToUuid(const std::string& binary) {
    if (binary.length() != 128) throw std::invalid_argument("Invalid binary length for UUID");
    return hexToUuid(binaryToHex(binary));
}

std::string uuidToBinary(const std::string& uuid) {
    return hexToBinary(uuidToHex(uuid));
}

std::string hexToIPAddress(const std::string& hex) {
    if (hex.length() != 8) throw std::invalid_argument("Invalid hex length for IP address");
    std::stringstream ss;
    for (size_t i = 0; i < 8; i += 2) {
        if (i > 0) ss << ".";
        ss << std::stoi(hex.substr(i, 2), nullptr, 16);
    }
    return ss.str();
}

std::string ipAddressToHex(const std::string& ip) {
    std::vector<std::string> octets;
    boost::split(octets, ip, boost::is_any_of("."));
    if (octets.size() != 4) throw std::invalid_argument("Invalid IP address format");
    
    std::stringstream ss;
    for (const auto& octet : octets) {
        int value = std::stoi(octet);
        ss << std::hex << std::setw(2) << std::setfill('0') << value;
    }
    return ss.str();
}

std::string binaryToIPAddress(const std::string& binary) {
    if (binary.length() != 32) throw std::invalid_argument("Invalid binary length for IP address");
    return hexToIPAddress(binaryToHex(binary));
}

std::string ipAddressToBinary(const std::string& ip) {
    return hexToBinary(ipAddressToHex(ip));
}

std::string hexToMacAddress(const std::string& hex) {
    if (hex.length() != 12) throw std::invalid_argument("Invalid hex length for MAC address");
    std::stringstream ss;
    for (size_t i = 0; i < 12; i += 2) {
        if (i > 0) ss << ":";
        ss << hex.substr(i, 2);
    }
    return ss.str();
}

std::string macAddressToHex(const std::string& mac) {
    std::string hex;
    for (char c : mac) {
        if (c != ':') hex += c;
    }
    if (hex.length() != 12) throw std::invalid_argument("Invalid MAC address format");
    return hex;
}

std::string binaryToMacAddress(const std::string& binary) {
    if (binary.length() != 48) throw std::invalid_argument("Invalid binary length for MAC address");
    return hexToMacAddress(binaryToHex(binary));
}

std::string macAddressToBinary(const std::string& mac) {
    return hexToBinary(macAddressToHex(mac));
}

std::string hexToRgba(const std::string& hex) {
    if (hex.length() != 8) throw std::invalid_argument("Invalid hex length for RGBA");
    int r = std::stoi(hex.substr(0, 2), nullptr, 16);
    int g = std::stoi(hex.substr(2, 2), nullptr, 16);
    int b = std::stoi(hex.substr(4, 2), nullptr, 16);
    int a = std::stoi(hex.substr(6, 2), nullptr, 16);
    std::stringstream ss;
    ss << "rgba(" << r << "," << g << "," << b << "," << std::fixed << std::setprecision(2) << (a / 255.0) << ")";
    return ss.str();
}

std::string rgbaToHex(int r, int g, int b, int a) {
    std::stringstream ss;
    ss << std::hex << std::setw(2) << std::setfill('0') << r
       << std::hex << std::setw(2) << std::setfill('0') << g
       << std::hex << std::setw(2) << std::setfill('0') << b
       << std::hex << std::setw(2) << std::setfill('0') << a;
    return ss.str();
}

std::string binaryToRgba(const std::string& binary) {
    if (binary.length() != 32) throw std::invalid_argument("Invalid binary length for RGBA");
    return hexToRgba(binaryToHex(binary));
}

std::string rgbaToBinary(int r, int g, int b, int a) {
    return hexToBinary(rgbaToHex(r, g, b, a));
}

std::string hexToColorName(const std::string& hex) {
    // This would require a large color name database. Here's a very simplified version:
    static const std::unordered_map<std::string, std::string> colorMap = {
        {"FF0000", "Red"}, {"00FF00", "Green"}, {"0000FF", "Blue"},
        {"FFFF00", "Yellow"}, {"FF00FF", "Magenta"}, {"00FFFF", "Cyan"},
        {"000000", "Black"}, {"FFFFFF", "White"}
    };
    auto it = colorMap.find(hex);
    return (it != colorMap.end()) ? it->second : "Unknown";
}

std::string colorNameToHex(const std::string& colorName) {
    // This would require a large color name database. Here's a very simplified version:
    static const std::unordered_map<std::string, std::string> colorMap = {
        {"Red", "FF0000"}, {"Green", "00FF00"}, {"Blue", "0000FF"},
        {"Yellow", "FFFF00"}, {"Magenta", "FF00FF"}, {"Cyan", "00FFFF"},
        {"Black", "000000"}, {"White", "FFFFFF"}
    };
    auto it = colorMap.find(colorName);
    return (it != colorMap.end()) ? it->second : "Unknown";
}

std::string binaryToColorName(const std::string& binary) {
    return hexToColorName(binaryToHex(binary));
}

std::string colorNameToBinary(const std::string& colorName) {
    return hexToBinary(colorNameToHex(colorName));
}
```

## Regex Utilities

```cpp

#include <iostream>
#include <regex>
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>
#include <cctype>

bool isMatch(const std::string& text, const std::string& pattern) {
    // Matches the entire text against the given pattern
    return std::regex_match(text, std::regex(pattern));
}

std::vector<std::string> findAllMatches(const std::string& text, const std::string& pattern) {
    std::vector<std::string> matches;
    std::regex re(pattern);
    std::sregex_iterator begin(text.begin(), text.end(), re);
    std::sregex_iterator end;
    
    for (auto it = begin; it != end; ++it) {
        matches.push_back(it->str());
    }
    
    return matches;
}

std::string findFirstMatch(const std::string& text, const std::string& pattern) {
    std::regex re(pattern);
    std::smatch match;
    if (std::regex_search(text, match, re)) {
        return match.str();
    }
    return "";
}

int countMatches(const std::string& text, const std::string& pattern) {
    std::regex re(pattern);
    return std::distance(std::sregex_iterator(text.begin(), text.end(), re), std::sregex_iterator());
}

std::string replaceAll(const std::string& text, const std::string& pattern, const std::string& replacement) {
    return std::regex_replace(text, std::regex(pattern), replacement);
}

std::string replaceFirst(const std::string& text, const std::string& pattern, const std::string& replacement) {
    return std::regex_replace(text, std::regex(pattern), replacement, std::regex_constants::format_first_only);
}

std::string replaceLast(const std::string& text, const std::string& pattern, const std::string& replacement) {
    std::string reversedText = text;
    std::reverse(reversedText.begin(), reversedText.end());
    std::string reversedPattern = pattern;
    std::reverse(reversedPattern.begin(), reversedPattern.end());
    std::string reversedReplacement = replacement;
    std::reverse(reversedReplacement.begin(), reversedReplacement.end());

    reversedText = replaceFirst(reversedText, reversedPattern, reversedReplacement);
    std::reverse(reversedText.begin(), reversedText.end());

    return reversedText;
}

std::vector<std::string> splitByPattern(const std::string& text, const std::string& pattern) {
    std::regex re(pattern);
    std::sregex_token_iterator it(text.begin(), text.end(), re, -1);
    std::sregex_token_iterator end;
    std::vector<std::string> tokens(it, end);
    return tokens;
}

std::string removeAllMatches(const std::string& text, const std::string& pattern) {
    return replaceAll(text, pattern, "");
}

std::string removeFirstMatch(const std::string& text, const std::string& pattern) {
    return replaceFirst(text, pattern, "");
}

std::string removeLastMatch(const std::string& text, const std::string& pattern) {
    return replaceLast(text, pattern, "");
}

bool isPatternInText(const std::string& text, const std::string& pattern) {
    return std::regex_search(text, std::regex(pattern));
}

std::string extractFirstMatch(const std::string& text, const std::string& pattern) {
    return findFirstMatch(text, pattern);
}

std::string extractLastMatch(const std::string& text, const std::string& pattern) {
    auto matches = findAllMatches(text, pattern);
    if (!matches.empty()) {
        return matches.back();
    }
    return "";
}

std::string extractAllMatchesAsString(const std::string& text, const std::string& pattern) {
    auto matches = findAllMatches(text, pattern);
    std::ostringstream oss;
    for (const auto& match : matches) {
        oss << match << " ";
    }
    return oss.str();
}

bool containsDigit(const std::string& text) {
    return std::any_of(text.begin(), text.end(), ::isdigit);
}

bool containsLetter(const std::string& text) {
    return std::any_of(text.begin(), text.end(), ::isalpha);
}

bool containsUppercase(const std::string& text) {
    return std::any_of(text.begin(), text.end(), ::isupper);
}

bool containsLowercase(const std::string& text) {
    return std::any_of(text.begin(), text.end(), ::islower);
}

bool containsWhitespace(const std::string& text) {
    return std::any_of(text.begin(), text.end(), ::isspace);
}

bool containsOnlyDigits(const std::string& text) {
    return std::all_of(text.begin(), text.end(), ::isdigit);
}

bool containsOnlyLetters(const std::string& text) {
    return std::all_of(text.begin(), text.end(), ::isalpha);
}

bool containsOnlyAlphanumeric(const std::string& text) {
    return std::all_of(text.begin(), text.end(), ::isalnum);
}

bool containsOnlyWhitespace(const std::string& text) {
    return std::all_of(text.begin(), text.end(), ::isspace);
}

bool startsWithPattern(const std::string& text, const std::string& pattern) {
    return text.compare(0, pattern.length(), pattern) == 0;
}

bool endsWithPattern(const std::string& text, const std::string& pattern) {
    if (pattern.size() > text.size()) return false;
    return std::equal(pattern.rbegin(), pattern.rend(), text.rbegin());
}

bool isValidEmail(const std::string& email) {
    const std::regex pattern(R"((\w+)(\.\w+)*@(\w+\.)+\w{2,})");
    // Pattern explanation:
    // (\w+): Matches one or more word characters (alphanumeric or underscore).
    // (\.\w+)*: Matches zero or more occurrences of a period followed by one or more word characters.
    // @: Matches the '@' symbol.
    // (\w+\.)+: Matches one or more occurrences of one or more word characters followed by a period.
    // \w{2,}: Matches two or more word characters (the domain part after the dot).
    return isMatch(email, pattern);
}

```

```cpp
bool isValidPhoneNumber(const std::string& phone) {
    const std::regex pattern(R"(^(\+?\d{1,3}[- ]?)?\d{10}$)");
    // Pattern explanation:
    // ^: Start of the string.
    // (\+?\d{1,3}[- ]?)?: Optionally matches an international code (e.g., +123 or 123-).
    // \d{10}: Matches exactly 10 digits.
    // $: End of the string.
    return isMatch(phone, pattern);
}

bool isValidURL(const std::string& url) {
    const std::regex pattern(R"(https?:\/\/[\w\-]+(\.[\w\-]+)+[\w\-\._~:\/?#[\]@!\$&'\(\)\*\+,;=]+)");
    // Pattern explanation:
    // https?:\/\/: Matches 'http' or 'https' followed by '://'.
    // [\w\-]+: Matches one or more word characters or hyphens (the domain name).
    // (\.[\w\-]+)+: Matches one or more periods followed by one or more word characters or hyphens.
    // [\w\-\._~:\/?#[\]@!\$&'\(\)\*\+,;=]+: Matches the rest of the URL, allowing various URL-safe characters.
    return isMatch(url, pattern);
}

bool isValidIPAddress(const std::string& ip) {
    const std::regex pattern(R"((\d{1,3}\.){3}\d{1,3})");
    // Pattern explanation:
    // (\d{1,3}\.){3}: Matches three groups of 1 to 3 digits followed by a period.
    // \d{1,3}: Matches 1 to 3 digits (the last segment of the IP address).
    return isMatch(ip, pattern);
}

bool isValidDate(const std::string& date, const std::string& format) {
    if (format == "YYYY-MM-DD") {
        const std::regex pattern(R"(\d{4}-\d{2}-\d{2})");
        // Pattern explanation:
        // \d{4}: Matches exactly 4 digits (year).
        // -: Matches a hyphen.
        // \d{2}: Matches exactly 2 digits (month or day).
        return isMatch(date, pattern);
    }
    return false;
}

bool isValidTime(const std::string& time, const std::string& format) {
    if (format == "HH:MM") {
        const std::regex pattern(R"(\d{2}:\d{2})");
        // Pattern explanation:
        // \d{2}: Matches exactly 2 digits (hours or minutes).
        // :: Matches a colon.
        return isMatch(time, pattern);
    }
    return false;
}

bool isValidHexColor(const std::string& color) {
    const std::regex pattern(R"(^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$)");
    // Pattern explanation:
    // ^: Start of the string.
    // #?: Optionally matches the '#' character.
    // ([a-fA-F0-9]{6}|[a-fA-F0-9]{3}): Matches either 6 or 3 hexadecimal digits.
    // $: End of the string.
    return isMatch(color, pattern);
}

bool isValidPostalCode(const std::string& postalCode) {
    const std::regex pattern(R"(\d{5}(-\d{4})?)");
    // Pattern explanation:
    // \d{5}: Matches exactly 5 digits (the main part of the postal code).
    // (-\d{4})?: Optionally matches a hyphen followed by exactly 4 digits (the extended ZIP+4 code).
    return isMatch(postalCode, pattern);
}

bool isValidSocialSecurityNumber(const std::string& ssn) {
    const std::regex pattern(R"(\d{3}-\d{2}-\d{4})");
    // Pattern explanation:
    // \d{3}: Matches exactly 3 digits (the first part of the SSN).
    // -: Matches a hyphen.
    // \d{2}: Matches exactly 2 digits (the middle part of the SSN).
    // -: Matches another hyphen.
    // \d{4}: Matches exactly 4 digits (the last part of the SSN).
    return isMatch(ssn, pattern);
}

bool isValidCreditCardNumber(const std::string& cardNumber) {
    const std::regex pattern(R"(^\d{16}$)");
    // Pattern explanation:
    // ^: Start of the string.
    // \d{16}: Matches exactly 16 digits.
    // $: End of the string.
    return isMatch(cardNumber, pattern);
}

bool isValidMACAddress(const std::string& mac) {
    const std::regex pattern(R"(^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$)");
    // Pattern explanation:
    // ^: Start of the string.
    // ([0-9A-Fa-f]{2}:){5}: Matches exactly 5 groups of 2 hexadecimal digits followed by a colon.
    // [0-9A-Fa-f]{2}: Matches the last group of 2 hexadecimal digits.
    // $: End of the string.
    return isMatch(mac, pattern);
}

bool isValidUUID(const std::string& uuid) {
    const std::regex pattern(R"([a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12})");
    // Pattern explanation:
    // [a-f0-9]{8}: Matches exactly 8 hexadecimal digits (first segment).
    // -: Matches a hyphen.
    // [a-f0-9]{4}: Matches exactly 4 hexadecimal digits (second, third, and fourth segments).
    // -: Matches another hyphen.
    // [a-f0-9]{12}: Matches exactly 12 hexadecimal digits (fifth segment).
    return isMatch(uuid, pattern);
}

std::string maskSensitiveData(const std::string& text, const std::string& pattern) {
    return replaceAll(text, pattern, "****");
}

std::string highlightMatches(const std::string& text, const std::string& pattern, const std::string& highlight) {
    std::string highlightedText = text;
    std::string highlightedPattern = highlight + "$&" + highlight;
    return replaceAll(highlightedText, pattern, highlightedPattern);
}

std::string escapeRegex(const std::string& text) {
    std::string escaped;
    for (char c : text) {
        if (std::ispunct(c)) escaped += '\\';
        escaped += c;
    }
    return escaped;
}

std::string unescapeRegex(const std::string& text) {
    std::string unescaped;
    bool escaping = false;
    for (char c : text) {
        if (escaping) {
            unescaped += c;
            escaping = false;
        } else if (c == '\\') {
            escaping = true;
        } else {
            unescaped += c;
        }
    }
    return unescaped;
}

bool isAlphaNumeric(const std::string& text) {
    return containsOnlyAlphanumeric(text);
}

bool isOnlySpecialCharacters(const std::string& text) {
    return std::all_of(text.begin(), text.end(), [](char c) { return std::ispunct(c); });
}

std::string extractDigits(const std::string& text) {
    return replaceAll(text, R"(\D)", "");
    // Pattern explanation:
    // \D: Matches any non-digit character.
}

std::string extractLetters(const std::string& text) {
    return replaceAll(text, R"([^a-zA-Z])", "");
    // Pattern explanation:
    // [^a-zA-Z]: Matches any character that is not a letter (uppercase or lowercase).
}

std::string extractSpecialCharacters(const std::string& text) {
    std::string specialChars;
    std::copy_if(text.begin(), text.end(), std::back_inserter(specialChars), [](char c) { return std::ispunct(c); });
    return specialChars;
}

std::string extractWords(const std::string& text) {
    std::stringstream ss(text);
    std::string word, result;
    while (ss >> word) {
        result += word + " ";
    }
    result.pop_back(); // Remove last space
    return result;
}

std::vector<std::string> findAllWords(const std::string& text) {
    return splitByPattern(text, R"(\W+)");
    // Pattern explanation:
    // \W+: Matches one or more non-word characters (this acts as a delimiter between words).
}

std::vector<int> findAllIndicesOfPattern(const std::string& text, const std::string& pattern) {
    std::vector<int> indices;
    std::regex re(pattern);
    std::sregex_iterator begin(text.begin(), text.end(), re);
    std::sregex_iterator end;
    
    for (auto it = begin; it != end; ++it) {
        indices.push_back(it->position());
    }
    
    return indices;
}

int findFirstIndexOfPattern(const std::string& text, const std::string& pattern) {
    auto indices = findAllIndicesOfPattern(text, pattern);
    if (!indices.empty()) {
        return indices.front();
    }
    return -1;
}

int findLastIndexOfPattern(const std::string& text, const std::string& pattern) {
    auto indices = findAllIndicesOfPattern(text, pattern);
    if (!indices.empty()) {
        return indices.back();
    }
    return -1;
}
```

```cpp

bool isValidFilename(const std::string& filename) {
    const std::regex pattern(R"(^[^\0/<>:"\\|?*]+$)");
    // Pattern explanation:
    // ^: Start of the string.
    // [^\0/<>:"\\|?*]+: Matches one or more characters that are not null, '/', '<', '>', ':', '"', '\\', '|', '?', or '*'.
    // $: End of the string.
    return isMatch(filename, pattern);
}

bool isValidWindowsPath(const std::string& path) {
    const std::regex pattern(R"(^[a-zA-Z]:\\(([a-zA-Z0-9 _\-\.])+\\?)*$)");
    // Pattern explanation:
    // ^: Start of the string.
    // [a-zA-Z]: Matches a single drive letter.
    // :\\: Matches a colon followed by a backslash.
    // (([a-zA-Z0-9 _\-\.])+\\?)*: Matches zero or more folders, each consisting of one or more valid filename characters followed by an optional backslash.
    // $: End of the string.
    return isMatch(path, pattern);
}

bool isValidUnixPath(const std::string& path) {
    const std::regex pattern(R"(^/([^/\0]+/)*([^/\0]+)$)");
    // Pattern explanation:
    // ^: Start of the string.
    // /: Matches the root directory.
    // ([^/\0]+/)*: Matches zero or more folders, each consisting of one or more characters that are not '/' or null, followed by a slash.
    // ([^/\0]+): Matches the final folder or file name.
    // $: End of the string.
    return isMatch(path, pattern);
}

bool isValidEnvironmentVariableName(const std::string& name) {
    const std::regex pattern(R"(^[a-zA-Z_]+[a-zA-Z0-9_]*$)");
    // Pattern explanation:
    // ^: Start of the string.
    // [a-zA-Z_]+: Matches one or more letters or underscores (the first character(s) of the variable name).
    // [a-zA-Z0-9_]*: Matches zero or more letters, digits, or underscores (the remaining characters of the variable name).
    // $: End of the string.
    return isMatch(name, pattern);
}

bool isValidHashtag(const std::string& hashtag) {
    const std::regex pattern(R"(#\w+)");
    // Pattern explanation:
    // #: Matches the '#' character.
    // \w+: Matches one or more word characters (letters, digits, or underscores).
    return isMatch(hashtag, pattern);
}

bool isValidMention(const std::string& mention) {
    const std::regex pattern(R"(@\w+)");
    // Pattern explanation:
    // @: Matches the '@' character.
    // \w+: Matches one or more word characters (letters, digits, or underscores).
    return isMatch(mention, pattern);
}

std::vector<std::string> extractAllEmailAddresses(const std::string& text) {
    return findAllMatches(text, R"((\w+)(\.\w+)*@(\w+\.)+\w{2,})");
    // Same pattern as isValidEmail.
}

std::vector<std::string> extractAllURLs(const std::string& text) {
    return findAllMatches(text, R"(https?:\/\/[\w\-]+(\.[\w\-]+)+[\w\-\._~:\/?#[\]@!\$&'\(\)\*\+,;=]+)");
    // Same pattern as isValidURL.
}

std::vector<std::string> extractAllPhoneNumbers(const std::string& text) {
    return findAllMatches(text, R"((\+?\d{1,3}[- ]?)?\d{10})");
    // Same pattern as isValidPhoneNumber.
}

std::vector<std::string> extractAllDates(const std::string& text, const std::string& format) {
    if (format == "YYYY-MM-DD") {
        return findAllMatches(text, R"(\d{4}-\d{2}-\d{2})");
        // Same pattern as isValidDate.
    }
    return {};
}

std::vector<std::string> extractAllTimes(const std::string& text, const std::string& format) {
    if (format == "HH:MM") {
        return findAllMatches(text, R"(\d{2}:\d{2})");
        // Same pattern as isValidTime.
    }
    return {};
}

std::vector<std::string> extractAllIPAddresses(const std::string& text) {
    return findAllMatches(text, R"((\d{1,3}\.){3}\d{1,3})");
    // Same pattern as isValidIPAddress.
}

std::vector<std::string> extractAllHexColors(const std::string& text) {
    return findAllMatches(text, R"(^#?([a-fA-F0-9]{6}|[a-fA-F0-9]{3})$)");
    // Same pattern as isValidHexColor.
}

std::vector<std::string> extractAllPostalCodes(const std::string& text) {
    return findAllMatches(text, R"(\d{5}(-\d{4})?)");
    // Same pattern as isValidPostalCode.
}

std::vector<std::string> extractAllCreditCardNumbers(const std::string& text) {
    return findAllMatches(text, R"(^\d{16}$)");
    // Same pattern as isValidCreditCardNumber.
}

std::vector<std::string> extractAllMACAddresses(const std::string& text) {
    return findAllMatches(text, R"(^([0-9A-Fa-f]{2}:){5}[0-9A-Fa-f]{2}$)");
    // Same pattern as isValidMACAddress.
}

std::vector<std::string> extractAllUUIDs(const std::string& text) {
    return findAllMatches(text, R"([a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12})");
    // Same pattern as isValidUUID.
}

std::string replaceDigitsWithPattern(const std::string& text, const std::string& pattern) {
    return replaceAll(text, R"(\d)", pattern);
    // Pattern explanation:
    // \d: Matches any digit.
}

std::string replaceLettersWithPattern(const std::string& text, const std::string& pattern) {
    return replaceAll(text, R"([a-zA-Z])", pattern);
    // Pattern explanation:
    // [a-zA-Z]: Matches any letter (uppercase or lowercase).
}

std::string replaceSpecialCharactersWithPattern(const std::string& text, const std::string& pattern) {
    return replaceAll(text, R"([^a-zA-Z0-9\s])", pattern);
    // Pattern explanation:
    // [^a-zA-Z0-9\s]: Matches any character that is not a letter, digit, or whitespace (i.e., special characters).
}

std::string replaceWordsWithPattern(const std::string& text, const std::string& pattern) {
    return replaceAll(text, R"(\w+)", pattern);
    // Pattern explanation:
    // \w+: Matches one or more word characters (letters, digits, or underscores).
}

std::string replaceWhitespaceWithPattern(const std::string& text, const std::string& pattern) {
    return replaceAll(text, R"(\s+)", pattern);
    // Pattern explanation:
    // \s+: Matches one or more whitespace characters (spaces, tabs, line breaks, etc.).
}
```
