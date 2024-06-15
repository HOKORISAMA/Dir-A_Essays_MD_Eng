
### Initial Understanding of C++ Design Thinking on Data Encapsulation
This document aims to introduce the concept of data encapsulation in C++. It does not teach the basic knowledge of C++, and some parts are not covered. The focus is on explaining the concept, and after reading this, you can refer to other introductory C++ videos for a better understanding.

## 0x00 
We Need a Container to Store Data
Suppose we need to process some information about students. Each student has four pieces of information: student ID, age, grade in subject A, and grade in subject B.

In C, we can define a structure to represent this data type (for simplicity, all data is represented as int):

```
struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;
};
```

This means defining a Student type, which describes a student's information, occupying 4*4 bytes (one int is 4 bytes in a 32-bit system).

When defining a variable, we usually write:

```
int a = 0;
```

This means defining an int type variable a and initializing it to 0. Similarly:

```
Student xiaoming = { 0 };
```
This means defining a Student type variable xiaoming and initializing it to 0. The { 0 } means initializing the structure, equivalent to a = 0. Actually, int a = { 0 }; is also valid.

```
struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;
};

int main() {
    // Equivalent to int a = 0;
    Student xiaoming = { 0 };
}
```
Now, we have defined a data type called Student and allocated 4*4 bytes of memory space to store the data of this type. This space is named xiaoming and all its data is initialized to 0.

## 0x01 
Assigning Information to Xiaoming
Let's put some information into this student's data:

```
Student ID: 10086
Age: 20
Grade in Subject A: 80
Grade in Subject B: 60
How do we store this data?
```

It's simple. By using the dot operator ., we can access some data of this student:

```
xiaoming.ID = 10086;
xiaoming.Age = 20;
xiaoming.SubA = 80;
xiaoming.SubB = 60;
```
The dot operator is called the member access operator. To access some data of a student, add a dot after the student variable.

Later, we will discuss accessing not only data but also functions, which are methods to process the data.

```
struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;
};

int main() {
    // Equivalent to int a = 0;
    Student xiaoming = { 0 };
    xiaoming.ID = 10086;
    xiaoming.Age = 20;
    xiaoming.SubA = 80;
    xiaoming.SubB = 60;
}
```
## 0x02 
Calculating Xiaoming's Average Score
Now that the student's information has been entered into the computer, let's calculate his average score.

The average score is simply SubA + SubB divided by 2. However, there is more than one student in a class. If we always write (xiaoming.SubA + xiaoming.SubB) / 2, it is quite tedious. First, we need to write the student's name xiaoming, then access the specific subject scores, add them, and then calculate the average.

At this point, we might consider a general function that takes two scores as input and returns their average.
```
int Average(int A, int B)
{
    int aver = (A + B) / 2;
    return aver;
}
```
## 0x03 
How to Write it More Elegantly?
The current code works fine, but if we add another student, they can also use the Average() function to calculate the average score of two subjects. However, this Average() function is global, meaning it can be called by anyone, even those who are not students in your class. Furthermore, any two integers can be passed to this function, even if they are not scores.

For example:

```
int err = Average(xiaoming.ID, xiaoming.Age);
```
Adding the student ID and age to calculate an average score doesn't make sense. Also, a student from another class might have different subjects, and they can still use this function to calculate their average score. If their subjects are easier, their average score could be higher than ours, which isn't fair.

The code looks like a machine without a casing, with pipes and screws exposed, ready to be taken apart or modified at any time. Would you buy a phone or computer without a casing, with batteries and circuit boards exposed? Obviously not. You might buy a phone with a metal frame and glass back or a computer with a metal case, which feels smooth and may even have waterproof features, working even when dropped in water.

Let's give our program a casing. The Average() function is clearly meant to calculate the average score for students in our class, not for other classes, and certainly not for averaging ages and IDs. We previously defined the Student data type, so let's add some more to it.

```
struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;

    int Average() {
        int aver = (SubA + SubB) / 2;
        return aver;
    }
};
```
Now, doesn't it seem like Average() is part of the Student type? We can use the member access operator . to access this function, similar to before. However, instead of writing:

```
int c = Average(xiaoming.SubA, xiaoming.SubB);
```
We write:

```
int c = xiaoming.Average();
```
Now, the function belongs to the Student type, and it can only be called for student instances. It uses the instance's data directly, ensuring that only relevant data is used.

Here is the complete, improved code:

```
#include <iostream>

struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;

    int Average() {
        return (SubA + SubB) / 2;
    }
};

int main() {
    // Equivalent to int a = 0;
    Student xiaoming = {10086, 20, 80, 60};
    // Calculate Xiaoming's average score
    int c = xiaoming.Average();
    std::cout << "Xiaoming's average score is " << c << std::endl;
}
```
Summary
By encapsulating the Average function within the Student structure, we ensure that the function operates on relevant data only, providing a more elegant and logical structure to our code. This encapsulation is a core concept in C++ that helps to maintain the integrity and reusability of code, making it easier to understand and manage.
