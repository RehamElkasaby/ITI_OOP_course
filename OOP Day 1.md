![[Pasted image 20241101160547.png]] 

# C++
![[Pasted image 20241101160851.png]]
- was created in 1985.
- c++ is *not* pure oop language:
	- main is not in a class.
	- Global variables can be used.
```c++
#include<iostream> 
using namespace std;
int main()
{
int x =10;
printf("Hello world!"); //won't work unless #include<stdio.h>
cin>>x;
cout<<"welcome"<<"hi"<<endl;
cout<<"x="<<x;
char arr [20]; //static allocation
//in c, dynamic allocation
int* ptr =(int*)malloc(5*sizeof(int)); // in heap
free(ptr); //NOTE need #include <malloc.h>
// in c++
int* ptr = new int[5]; //in heap 
delete [] ptr;
//using ptr after this-> runtime error
int* ptr_2 = new int (5); 
//NOTE will have one pointer to ONE int with 5 intialized 
delete ptr_2;

return 0;
}
```

- ### Access Specifiers
	- **Public:** anyone can access this data, if you have an object from that class.
	- **Private:** only members(functions: getter, setter) of the same class can access the data
		- if outside members try to access it (Ex: in main ) *Compilation Error* 
- Struct and class have a lot of similarities. 
```C++
struct employee_struct
{//unlike in C, struct can have functions
    //default public
    int id ;
    char name [100];
    int age;

    //can add functions
    //getter
    int getAge(){return age;}
    void setAge(int _age){age=_age;}

    int getId(){return age;}
    void setId(int _id){id=_id;}

    char* getName(){return name;}
    void setName(char* _name){strcpy(name,_name);}

};
int main()
{
    employee_struct e1 ;
    cout<<"Employee Id:";
    cin>>e1.id; // only takes till space/Enter
    cout<<"Employee Name:";
    //e1.name="ali"; //Error name is static allocated
    _flushall(); //clear the buffer
    gets(e1.name); //input a line including spaces until \n or Enter
    cout<<"Employee Age:";
    cin>>e1.age; // can access data directly since it is public
    cout<<"Employee ID: "<<e1.id<<" Employee Name: "<<e1.name<<" Employee Age: "<<e1.age<<endl;
    cout<<"Employee ID: "<<e1.getId()<<" Employee Name: "<<e1.getName()<<" Employee Age: "<<e1.getAge()<<endl;
    cout<<"*********************************************"<<endl;
```

Class
```C++

class employee_class
{ //default private

    int id ;
    char name [100];
    int age;

    //can add functions
    //getter and setter are better for maintenice and debugging
    //have to make them public
    public:
    int getAge(){return age;}
    void setAge(int _age){age=_age;}

    int getId(){return age;}
    void setId(int _id){id=_id;}
    
	//note the getter and setter of the array
    char* getName(){return name;} 
    void setName(char* _name){strcpy(name,_name);}
};
int main()
{
	employee_class e_class ;
    cout<<"Employee Id:";
    //cin>>e_class.id; //error id is private can not be accessed this way.
    int x;
    char n [100];
    cin>>x;
    e_class.setId(x);
//e_class.id =10; //Error, data is private can't be accessed directly
    cout<<"Employee Name:";
    _flushall();
    gets(n);//gets the whole line space included
    e_class.setName(n);
    cout<<"Employee Age:";
    cin>>x;
    e_class.setAge(x);
    //cout<<"Employee ID: "<<e_class.id<<" Employee Name: "<<e_class.name<<" Employee Age: "<<e_class.age<<endl; //error
    cout<<"Employee ID: "<<e_class.getId()<<" Employee Name: "<<e_class.getName()<<" Employee Age: "<<e_class.getAge()<<endl;
    return 0;
    }
```

- Any object in c++ is being created in the stack.
- if you want to create it in heap use keyword `new` .

```C++
int main()
{
    cout<<"Object in the stack"<<endl;
    employee_class e1;

    cout<<"Employee ID: "<<e1.getId()<<" Employee Name: "<<e1.getName()<<" Employee Age: "<<e1.getAge()<<endl;

    cout<<"object in the heap using new keyword"<<endl;
    employee_class* ptr = new employee_class;

    cout<<"Employee ID: "<<ptr->getId()<<" Employee Name: "<<ptr->getName()<<" Employee Age: "<<ptr->getAge()<<endl;

    return 0;
}
```

```C++
emp e1; //created in stack
emp* ptr = &e1; //create a pointer to struct
*ptr.setId(50);
ptr->setId(50);

emp* ptr = new emp; 
//create object of type emp in heap ,return address and use it as a refrence.
delete ptr;//free space from memory
//in C# don't have to do it have garbage collector
```

![[Pasted image 20241101222010.png]]

```C++
void swap (int a, int b)
{// pass by value
int temp=x;
x=y;
y = temp;
}

void swap (int*a,int*b)
{//pass by address
int temp = *x;
*x =*y;
*y = temp;
}
void swap(int &x,int &y)
{//pass by refrence
int temp =x;
x=y;
y=temp;
}
```