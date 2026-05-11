# prac-6-12
# ques 7 GCD Using Recursion
 include <iostream>
using namespace std;

int gcd(int a, int b)
{
    if(b == 0)
    {
        return a;
    }

    return gcd(b, a % b);
}

int main()
{
    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    cout << "GCD = " << gcd(a, b);

    return 0;
}

# 7b GCD Without Recursion
 include <iostream>
using namespace std;

int main()
{
    int a, b;

    cout << "Enter two numbers: ";
    cin >> a >> b;

    while(b != 0)
    {
        int temp = b;
        b = a % b;
        a = temp;
    }

    cout << "GCD = " << a;

    return 0;
}

# ques 8 Matrix Class Program
 include <iostream>
using namespace std;

class Matrix
{
    int a[10][10], r, c;

public:

    void input()
    {
        cout << "Enter rows and columns: ";
        cin >> r >> c;

        cout << "Enter matrix elements:\n";

        for(int i = 0; i < r; i++)
        {
            for(int j = 0; j < c; j++)
            {
                cin >> a[i][j];
            }
        }
    }

    void display()
    {
        for(int i = 0; i < r; i++)
        {
            for(int j = 0; j < c; j++)
            {
                cout << a[i][j] << " ";
            }

            cout << endl;
        }
    }

    Matrix sum(Matrix m)
    {
        if(r != m.r || c != m.c)
        {
            throw "Addition not possible";
        }

        Matrix temp;
        temp.r = r;
        temp.c = c;

        for(int i = 0; i < r; i++)
        {
            for(int j = 0; j < c; j++)
            {
                temp.a[i][j] = a[i][j] + m.a[i][j];
            }
        }

        return temp;
    }

    Matrix product(Matrix m)
    {
        if(c != m.r)
        {
            throw "Multiplication not possible";
        }

        Matrix temp;
        temp.r = r;
        temp.c = m.c;

        for(int i = 0; i < temp.r; i++)
        {
            for(int j = 0; j < temp.c; j++)
            {
                temp.a[i][j] = 0;

                for(int k = 0; k < c; k++)
                {
                    temp.a[i][j] += a[i][k] * m.a[k][j];
                }
            }
        }

        return temp;
    }

    void transpose()
    {
        for(int i = 0; i < c; i++)
        {
            for(int j = 0; j < r; j++)
            {
                cout << a[j][i] << " ";
            }

            cout << endl;
        }
    }
};

int main()
{
    Matrix m1, m2, result;
    int choice;

    m1.input();
    m2.input();

    cout << "\n1. Sum\n2. Product\n3. Transpose\n";
    cout << "Enter choice: ";
    cin >> choice;

    try
    {
        switch(choice)
        {
            case 1:
                result = m1.sum(m2);
                result.display();
                break;

            case 2:
                result = m1.product(m2);
                result.display();
                break;

            case 3:
                m1.transpose();
                break;

            default:
                cout << "Invalid Choice";
        }
    }

    catch(const char* msg)
    {
        cout << msg;
    }

    return 0;
}

# ques 9 Person, Student and Employee Class
 include <iostream>
using namespace std;

class Person
{
protected:
    string name;

public:
    void getName()
    {
        cout << "Enter name: ";
        cin >> name;
    }

    virtual void display()
    {
        cout << "Name: " << name << endl;
    }
};

class Student : public Person
{
    string course;
    int marks, year;

public:
    void getStudent()
    {
        getName();

        cout << "Enter course: ";
        cin >> course;

        cout << "Enter marks: ";
        cin >> marks;

        cout << "Enter year: ";
        cin >> year;
    }

    void display()
    {
        cout << "\nStudent Details\n";
        cout << "Name: " << name << endl;
        cout << "Course: " << course << endl;
        cout << "Marks: " << marks << endl;
        cout << "Year: " << year << endl;
    }
};

class Employee : public Person
{
    string department;
    int salary;

public:
    void getEmployee()
    {
        getName();

        cout << "Enter department: ";
        cin >> department;

        cout << "Enter salary: ";
        cin >> salary;
    }

    void display()
    {
        cout << "\nEmployee Details\n";
        cout << "Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Salary: " << salary << endl;
    }
};

int main()
{
    Person *p;

    Student s;
    Employee e;

    s.getStudent();
    e.getEmployee();

    p = &s;
    p->display();

    p = &e;
    p->display();

    return 0;
}

# ques 10 Triangle Class with Exception Handling
 include <iostream>
 include <cmath>
using namespace std;

class Triangle
{
    float a, b, c;

public:

    Triangle(float x, float y, float z)
    {
        if(x <= 0 || y <= 0 || z <= 0)
        {
            throw "Sides must be greater than 0";
        }

        if((x + y <= z) || (x + z <= y) || (y + z <= x))
        {
            throw "Invalid Triangle";
        }

        a = x;
        b = y;
        c = z;
    }

    float area(float base, float height)
    {
        return 0.5 * base * height;
    }

    float area()
    {
        float s = (a + b + c) / 2;

        return sqrt(s * (s - a) * (s - b) * (s - c));
    }
};

int main()
{
    float a, b, c;

    cout << "Enter sides of triangle: ";
    cin >> a >> b >> c;

    try
    {
        Triangle t(a, b, c);

        cout << "Area using Heron's Formula = "
             << t.area() << endl;

        cout << "Area of Right Triangle = "
             << t.area(5, 4);
    }

    catch(const char* msg)
    {
        cout << msg;
    }

    return 0;
}

# ques 11 Store and Retrieve Student Records from File
 include <iostream>
 include <fstream>
using namespace std;

class Student
{
    int roll;
    char name[20];
    char sclass[20];
    int year;
    float marks;

public:

    void input()
    {
        cout << "Enter Roll No: ";
        cin >> roll;

        cout << "Enter Name: ";
        cin >> name;

        cout << "Enter Class: ";
        cin >> sclass;

        cout << "Enter Year: ";
        cin >> year;

        cout << "Enter Total Marks: ";
        cin >> marks;
    }

    void display()
    {
        cout << "\nRoll No: " << roll;
        cout << "\nName: " << name;
        cout << "\nClass: " << sclass;
        cout << "\nYear: " << year;
        cout << "\nMarks: " << marks << endl;
    }
};

int main()
{
    Student s;

    ofstream fout("student.txt");

    for(int i = 0; i < 5; i++)
    {
        s.input();

        fout.write((char*)&s, sizeof(s));
    }

    fout.close();

    ifstream fin("student.txt");

    cout << "\nStored Records:\n";

    for(int i = 0; i < 5; i++)
    {
        fin.read((char*)&s, sizeof(s));

        s.display();
    }

    fin.close();

    return 0;
}

# ques 12 Copy One File to Another Without Whitespaces
 include <iostream>
 include <fstream>
using namespace std;

int main()
{
    ifstream fin("input.txt");
    ofstream fout("output.txt");

    char ch;

    while(fin.get(ch))
    {
        if(ch != ' ' && ch != '\n' && ch != '\t')
        {
            fout << ch;
        }
    }

    cout << "File copied successfully";

    fin.close();
    fout.close();

    return 0;
}
