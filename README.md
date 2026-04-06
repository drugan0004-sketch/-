include <bits/stdc++.h>
#include <iostream>
#include <iomanip>
#include <ctime>
using namespace std;

int main() {
struct data {
 int day;
 int month;
 int year;
};
struct vklad {
 char fam[30];
 int nomer;
 int suma;
 data oper;
};
setlocale(0, "");
time_t now = time(0);
tm ltm;
localtime(&ltm, &now);
vklad vklads[5] = {{"АА",1,300,{12,04,2025}},
 {"АБ",2,1500,{14,02,2026}},{"БВ",3,2990,{30,01,2026}},
 {"ВГ",3,400,{16,11,2025}},{"ГД",5,10000,{05,03,2026}}};
for (int i = 0;i<5;i++) {
    if (ltm.tm_year + 1990 == vklads[i].oper.year){
        cout << vklads[i].fam << endl;}
    };
return 0;


}
