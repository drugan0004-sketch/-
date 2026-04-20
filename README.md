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
-----------------------------------------------------------------------------------
#include <iostream>
#include <fstream>
#include <string>
#include <cstring>

using namespace std;

// Структура данных студента
struct Student {
    int id;
    char name[50]; // Используем char[] для бинарной записи
    double averageGrade;
};

int main() {
    const int N = 10;
    const char* filename = "students.bin";

    // 1. Создание и запись бинарного файла
    ofstream outFile(filename, ios::binary);
    if (!outFile) {
        cerr << "Ошибка открытия файла для записи!" << endl;
        return 1;
    }

    Student s[N];
    for (int i = 0; i < N; ++i) {
        s[i].id = i + 1;
        string name = "Student_" + to_string(i + 1);
        strncpy(s[i].name, name.c_str(), 49);
        s[i].name[49] = '\0';
        s[i].averageGrade = 3.0 + (rand() % 20 + 10) / 10.0; // Случайная оценка 3.0-5.0
        
        // Запись структуры в бинарный файл [1]
        outFile.write(reinterpret_cast<char*>(&s[i]), sizeof(Student));
    }
    outFile.close();
    cout << "Данные успешно записаны в файл " << filename << endl;

    // 2. Чтение данных из файла в массив
    ifstream inFile(filename, ios::binary);
    if (!inFile) {
        cerr << "Ошибка открытия файла для чтения!" << endl;
        return 1;
    }

    Student readStudents[N];
    for (int i = 0; i < N; ++i) {
        // Чтение структуры из бинарного файла [1]
        inFile.read(reinterpret_cast<char*>(&readStudents[i]), sizeof(Student));
    }
    inFile.close();

    // 3. Вывод данных на экран
    cout << "\nДанные студентов из файла:" << endl;
    for (int i = 0; i < N; ++i) {
        cout << "ID: " << readStudents[i].id 
             << ", Имя: " << readStudents[i].name 
             << ", Ср. балл: " << readStudents[i].averageGrade << endl;
    }

    return 0;
}
------------------------------------------------------------------------------
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

struct Student {
    int id;
    char name[50];
    float grade;
};

// Функция для записи данных студентов в бинарный файл
void writeStudentsToFile(const string& filename) {
    ofstream outFile(filename, ios::binary);
    if (!outFile) {
        cerr << "Не удалось открыть файл для записи." << endl;
        return;
    }

    Student students[10];

    // Заполнение структур студентов
    for (int i = 0; i < 10; ++i) {
        students[i].id = i + 1;
        cout << "Введите имя студента " << (i + 1) << ": ";
        cin >> students[i].name;
        cout << "Введите оценку студента " << (i + 1) << ": ";
        cin >> students[i].grade;
    }

    // Запись данных в файл
    outFile.write(reinterpret_cast<char*>(students), sizeof(students));
    outFile.close();
}

// Функция для чтения данных студентов из бинарного файла
void readStudentsFromFile(const string& filename) {
    ifstream inFile(filename, ios::binary);
    if (!inFile) {
        cerr << "Не удалось открыть файл для чтения." << endl;
        return;
    }

    Student students[10];
    inFile.read(reinterpret_cast<char*>(students), sizeof(students));
    inFile.close();

    // Вывод данных студентов на экран
    cout << "\nСписок студентов:\n";
    for (int i = 0; i < 10; ++i) {
        cout << "ID: " << students[i].id << ", Имя: " << students[i].name 
             << ", Оценка: " << students[i].grade << endl;
    }
}

int main() {
    string filename = "students.dat";

    writeStudentsToFile(filename);
    readStudentsFromFile(filename);

    return 0;
}
