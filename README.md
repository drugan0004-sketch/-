#include <iostream>
#include <iomanip>
#include <ctime>
#include "vkla.h"
using namespace std;

int main() {

setlocale(0, "");
time_t now = time(0);
struct tm* ltm = localtime(&now);
vklad vklads[5] = {{"АА",1,300,{12,04,2025}},
 {"АБ",2,1500,{14,02,2026}},{"БВ",3,2990,{30,01,2026}},
 {"ВГ",3,400,{16,11,2025}},{"ГД",5,10000,{05,03,2026}}};
for (int i = 0;i<5;i++) {
    if (ltm->tm_year + 1900 == vklads[i].oper.year and ltm->tm_mon+1 - vklads[i].oper.month < 3){
        cout << vklads[i].fam << endl;}
    if (ltm->tm_year + 1900 == vklads[i].oper.year and ltm->tm_mon+1 - vklads[i].oper.month == 3 
        and ltm->tm_mday > vklads[i].oper.day){
        cout << vklads[i].fam << endl;}
    };
return 0;
}

#include <iostream>
#include <iomanip>
#include <ctime>
#include "vkla.h"
using namespace std;
int main() {
setlocale(0, "");
time_t now = time(0);
struct tm* ltm = localtime(&now);
stud studs[5] = {{"Иванов","Дима","м",{12,04,2007}},
 {"Попов","Коля","м",{14,02,2005}},{"Горшков","Ваня","м",{30,01,2000}},
 {"Дудков","Данила","м",{16,11,2015}},{"Совков","Кирилл","м",{05,03,2009}}};
for (int i = 0;i<5;i++) {
    if (ltm->tm_year + 1900 - studs[i].oper.year > 18){
        cout << studs[i].fam << endl;}
    if (ltm->tm_year + 1900 - studs[i].oper.year == 18 and ltm->tm_mon+1 > studs[i].oper.month 
        and ltm->tm_mday > studs[i].oper.day){
        cout << studs[i].fam << endl;}
    };
return 0;
}
