#include <iostream>
#include <iomanip>
#include <fstream>
using namespace std;
int main() {
setlocale(0, "");
ifstream fin("C:\\Temp\\data.txt");
ofstream fout("C:\\Temp\\positive.txt");
int buff;
for (int i = 0; i < 14; i++) {
    
    fin >> buff;
    
    fout << buff;
        
    
}
return 0;
}
