```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    unsigned short num1 = 65535u;
    unsigned short num2 = 0xFFFFU;           //0~65535
    signed short n1 = (signed short)(num1);
    signed short n2 = (signed short)(num2);  //-32767~32767
    cout << n1 << endl;
    cout << n2 << endl;

    short n = -1;
    unsigned short un = (unsigned short)(n);
    cout << un << endl;

    unsigned short num = 0x8001U;           //0~65535
    signed short tmp = (signed short)(num); //-32767~32767
    cout << tmp << endl;

    cout << sizeof(char) << endl;			//1
    cout << sizeof(short) << endl;			//2
    cout << sizeof(long) << endl;			//4
    cout << sizeof(int) << endl;			//4
    cout << sizeof(float) << endl;			//
    cout << sizeof(long long) << endl;
    cout << sizeof(double) << endl << endl;

    cout << sizeof(unsigned char) << endl;
    cout << sizeof(unsigned short) << endl;
    cout << sizeof(unsigned long) << endl;
    cout << sizeof(unsigned int) << endl;
    //cout << sizeof(unsigned float) << endl;
    //cout << sizeof(unsigned double) << endl;
    cout << sizeof(unsigned long long) << endl;

    cout << sizeof(unsigned long int) << endl;
    cout << sizeof(unsigned int) << endl;
    cout << LONG_LONG_MAX << endl;
    cout << LONG_MAX << endl;
    cout << (numeric_limits<long>::max)() << endl;
    cout << (numeric_limits<short>::max)() << endl;
    cout << (numeric_limits<long long>::max)() << endl;
    cout << (numeric_limits<float>::max)() << endl;
    cout << (numeric_limits<double>::max)() << endl;
    cout << (numeric_limits<long double>::max)() << endl;
    //cout << (numeric_limits<long long double>::max)() << endl;
    return 0;
}
```
