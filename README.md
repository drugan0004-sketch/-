#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>
#include <sstream>
using namespace std;
int main() {
setlocale(0, "");
ifstream fin("C:\\Temp\\data.txt");
ofstream fout("C:\\Temp\\total.txt");
string line;
while (getline(fin, line)) {
    istringstream iss(line);
    int number;
    bool firstInLine = true;
    while (iss >> number) {
        if (number < 0) {
            if (!firstInLine) {
                fout << " ";
            }
            fout << number;
            firstInLine = false;
        }
    }
    fout << "\n";
}
fin.close();
fout.close();
return 0;
#include <iostream>
#include <iomanip>
#include <string>
#include <limits>
#include <fstream>

using namespace std;

int main() {
  ofstream file("типы данных.txt");

  file << setw(20) << right << "data type" << setw(10) << right << "byte" << setw(25)
    << right << "min value" << setw(25) << "max value" << endl;

  file << string(80, '-') << endl;

  string type[10] = {                            // data type
    "char", "short int", "unsigned short int", "int", "unsigned int",
    "long int", "unsigned long int", "float", "double", "long double"
  };
  int size_type[10] = { 1, 2, 2, 4, 4, 8, 8, 4, 8, 16 };          // byte

  long double max_values[10] = {
    (long double)numeric_limits<char>::max(),
    (long double)numeric_limits<short int>::max(),
    (long double)numeric_limits<unsigned short int>::max(),
    (long double)numeric_limits<int>::max(),
    (long double)numeric_limits<unsigned int>::max(),
    (long double)numeric_limits<long int>::max(),
    (long double)numeric_limits<unsigned long int>::max(),
    (long double)numeric_limits<float>::max(),
    (long double)numeric_limits<double>::max(),
    (long double)numeric_limits<long double>::max(),
  };

  long double min_values[10] = {
    (long double)numeric_limits<char>::min(),
    (long double)numeric_limits<short int>::min(),
    (long double)numeric_limits<unsigned short int>::min(),
    (long double)numeric_limits<int>::min(),
    (long double)numeric_limits<unsigned int>::min(),
    (long double)numeric_limits<long int>::min(),
    (long double)numeric_limits<unsigned long int>::min(),
    (long double)numeric_limits<float>::min(),
    (long double)numeric_limits<double>::min(),
    (long double)numeric_limits<long double>::max(),
  };


  for (int i = 0; i < 10; i += 1) {
    file << setw(20) << right << type[i] << setw(10) << right << size_type[i] << setw(25)
      << right << min_values[i] << setw(25) << max_values[i] << endl;
  }
}
