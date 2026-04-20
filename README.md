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
