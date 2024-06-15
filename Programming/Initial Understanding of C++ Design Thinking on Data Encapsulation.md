
Initial Understanding of C++ Design Thinking on Data Encapsulation
This document aims to introduce the concept of data encapsulation in C++. It does not teach the basic knowledge of C++, and some parts are not covered. The focus is on explaining the concept, and after reading this, you can refer to other introductory C++ videos for a better understanding.

0x00 We Need a Container to Store Data
Suppose we need to process some information about students. Each student has four pieces of information: student ID, age, grade in subject A, and grade in subject B.

In C, we can define a structure to represent this data type (for simplicity, all data is represented as int):

c
Copy code
struct Student {
    int ID;
    int Age;
    int SubA;
    int SubB;
};
This means defining a Student type, which describes a student's information, occupying 4*4 bytes (one int is 4 bytes in a 32-bit system).

When defining a variable, we usually write:

c
Copy code
int a = 0;
This means defining an int type variable a and initializing it to 0. Similarly:

c
Copy code
Student xiaoming = { 0 };
This means defining a Student type variable xiaoming and initializing it to 0. The { 0 } means initializing the structure, equivalent to a = 0. Actually, int a = { 0 }; is also valid.

c
Copy code
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
Now, we have defined a data type called Student and allocated 4*4 bytes of memory space to store the data of this type. This space is named xiaoming and all its data is initialized to 0.

0x01 Assigning Information to Xiaoming
Let's put some information into this student's data:

Student ID: 10086
Age: 20
Grade in Subject A: 80
Grade in Subject B: 60
How do we store this data?

It's simple. By using the dot operator ., we can access some data of this student:

c
Copy code
xiaoming.ID = 10086;
xiaoming.Age = 20;
xiaoming.SubA = 80;
xiaoming.SubB = 60;
The dot operator is called the member access operator. To access some data of a student, add a dot after the student variable.

Later, we will discuss accessing not only data but also functions, which are methods to process the data.

c
Copy code
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
0x02 Calculating Xiaoming's Average Score
Now that the student's information has been entered into the computer, let's calculate his average score.

The average score is simply SubA + SubB divided by 2. However, there is more than one student in a class. If we always write (xiaoming.SubA + xiaoming.SubB) / 2, it is quite tedious. First, we need to write the student's name xiaoming, then access the specific subject scores, add them, and then calculate the average.

At this point, we might consider a general function that takes two scores as input and returns their average.
