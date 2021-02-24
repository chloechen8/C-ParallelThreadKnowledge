### Clock:
- ```std::chrono::system_clock```:	current time according to the system, is not steady
- ```std::chrono::steady_clock```:	goes at a uniform rare;
- ```std::chrono::high_resolution__clock```: provides smallest possible tick period.

### Duration:
- ```std::chrono::duration<>```: represents time duration
	- 2 hours( a number and a unit)
- ```duration<int, ratio<1,1>>``` //number of second stored in a int, default duration
- ```duration<double, ratio<60,1>>``` //number of minutes stored in a double
  - ns, microseconds, millionseconds, s,min,hrs
- ```system_clock::duration``` -- duration<T, system_clock::period>

### Time Point:
- ```std::chrono::time_point<>```: represents a point of a time
- ```time_point<system_cleck, milliseconds>```: according to the system clock, the elapsed time 运行时间 since epoch(UTC开始的时间) in milliseconds.

	- ```system_clock::time_point``` -- time_point<system_clock, system_clock::duration>
	- ```steady_clock::time_point``` -- time_point<steady_clock, steady_clock::duration>
  
  
```C++
#include <chrono>
#include<iostream>
using namespace std;


int main() {

	/* Clock Example:
	std::ratio<1, 10> r;//1/10
	cout << r.num << "/" << r.den << endl;
	
	cout<< std::chrono::system_clock::period::num << "/" << std::chrono::system_clock::period::den << endl;
	*/

	/* Duration Example:
	chrono::microseconds mi{ 2700 };// 2700 microseconds
	cout<< mi.count() << endl; //2700
	chrono::nanoseconds na = mi; //2700000nanoseconds
	cout<< na.count(); //2700000
	//chrono::milliseconds mill = mi; //error, cannot convert
	chrono::milliseconds mill = chrono::duration_cast<chrono::milliseconds>(mi); //2 milliseconds

	mi = mill + mi;//2000+2700 = 4700
	*/

	/*Time point Example*/
	chrono::system_clock::time_point tp = chrono::system_clock::now(); // current time of system clock
	cout << tp.time_since_epoch().count() << endl;
	tp = tp + chrono::seconds(2);
	cout << tp.time_since_epoch().count() << endl;

	chrono::steady_clock::time_point start = chrono::steady_clock::now();
	cout << "*******" << endl;
	chrono::steady_clock::time_point end = chrono::steady_clock::now();
	chrono::steady_clock::duration d = end - start;
	if (d == chrono::steady_clock::duration::zero()) cout << "NO time elapsed"<<endl;
	cout << chrono::duration_cast<chrono::milliseconds>(d).count() << endl;

	return 0;
}
```
