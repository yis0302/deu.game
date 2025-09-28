                                  // *#( 여러 코드의 복잡, 중복되는 것 으로 인해) #*
                /*  코드 닫힘..                      ~~~~                          코드 닫힘..*/
                                    // 위와 같이 코드를 구간 마다 나누었습니다.

//---------------------------------------------------------------------------------

// 1. 상속(Inheritance) 부분

                                                                          /*  코드 닫힘..                                                 

#include <iostream>
using namespace std;

// 부모 클래스(기본 클래스)
class Animal {
public:
    Animal() { cout << "Animal 생성자 호출!" << endl; }
    void eat() { cout << "Animal이 먹는 중..." << endl; }
};

// 자식 클래스(파생 클래스) - Animal 상속
class Dog : public Animal { 
public:
    Dog() { cout << "Dog 생성자 호출!" << endl; }
    void bark() { cout << "Dog이 짖는 중..." << endl; }
};

// 자식 클래스(파생 클래스) - Animal 상속
class Cat : public Animal {
public:
    Cat() { cout << "Cat 생성자 호출!" << endl; }
    void meow() { cout << "Cat이 야옹하는 중..." << endl; }
};

int main() {
    Dog d;
    d.eat();   // Animal(부모)의 함수 사용
    d.bark();  // Dog(자식)의 함수 사용

    Cat c;
    c.eat();   // Animal(부모)의 함수 사용
    c.meow();  // Cat(자식)의 함수 사용
    return 0;
} 
// 여기서 자식인 Dog, Cat은 부모인 Animal의 모든 public 멤버(함수, 변수)를 상속받음.
// 자식 Dog, Cat 객체는 모두 eat()(부모 함수) 사용 가능.
// 객체 생성 시 부모 생성자 → 자식 생성자 순서로 호출됨.
                                                                          코드 닫힘..*/ 

//---------------------------------------------------------------------------------

// 2. 접근 제어자(Access Specifiers) 부분

                                                                            /*  코드 닫힘..                                                                 

#include <iostream>
using namespace std;

class Parent {  //부모 클래스
public:
    int pubVar;      // 어디서든 접근 가능
protected:
    int protVar;     // 상속받은 클래스에서만 접근 가능
private:
    int privVar;     // 오직 Parent 클래스 내부에서만 접근 가능
public:
    Parent() : pubVar(1), protVar(2), privVar(3) {}
    void showVars() {
        cout << "pubVar: " << pubVar << endl;      // OK
        cout << "protVar: " << protVar << endl;    // OK
        cout << "privVar: " << privVar << endl;    // OK
    }
};

class Child : public Parent { //자식 클래스 부모 클래스로부터 상속 받음.
public:
    void accessVars() {
        pubVar = 10;      // OK: public 멤버
        protVar = 20;     // OK: protected 멤버
        // privVar = 30; // Error: private 멤버는 상속받아도 접근 불가
    }
};

int main() {
    Parent p; // 부모함수 p  
    p.pubVar = 100;      // OK: public 멤버 
    // p.protVar = 200;  // Error: protected 멤버는 외부에서 접근 불가 
    // p.privVar = 300;  // Error: private 멤버는 외부에서 접근 불가 
    p.showVars();        // OK: 클래스 내부 함수에서 private/protected 모두 접근 가능 

    Child c; // 자식 함수 c  
    c.pubVar = 500;      // OK: public 멤버 
    // c.protVar = 600;  // Error: 외부에서 protected 멤버 접근 불가 
    c.accessVars();      // OK: 자식 클래스 내부에서 protected 멤버 접근 가능 
    return 0; 
}                                                                           코드 닫힘..*/

                                                                    
//---------------------------------------------------------------------------------

// 3. 함수 재정의(Overriding) vs 함수 중복(Overloading) 부분

            // 3-1. 함수 중복(Overloading)

// 같은 이름의 함수를 매개변수(파라미터) 타입이나 개수만 다르게 여러 번 정의하는 것

                                                                                /*  코드 닫힘..


#include <iostream>
using namespace std;

class Calculator {
public:
    // 두 정수의 합
    int add(int a, int b) {
        return a + b;
    }
    // 두 실수의 합 (매개변수 타입 다름)
    double add(double a, double b) {
        return a + b;
    }
    // 세 정수의 합 (매개변수 개수 다름)
    int add(int a, int b, int c) {
        return a + b + c;
    }
};

int main() {
    Calculator calc;
    cout << calc.add(1, 2) << endl;        // 3 (int, int)
    cout << calc.add(1.5, 2.5) << endl;    // 4.0 (double, double)
    cout << calc.add(1, 2, 3) << endl;     // 6 (int, int, int)
    return 0;
}
// 함수 이름은 모두 add이지만, 매개변수의 타입 또는 개수가 다름
// 어떤 함수가 호출될지는 입력값에 따라 컴파일러가 자동으로 결정
                                                                                코드 닫힘..*/
                 // 3-2. 함수 중복(Overloading)
// 상속 관계에서, 부모 클래스의 함수를 자식 클래스에서 똑같은 이름, 똑같은 매개변수, 똑같은 반환 타입으로 "다시" 정의하는 것
// 주로 다형성(polymorphism)을 위해 사용

                                                                                /*  코드 닫힘..

#include <iostream>
using namespace std;

// 부모 클래스
class Animal {
public:
    virtual void sound() { // 가상 함수(virtual) 선언
        cout << "동물이 소리를 냅니다." << endl;
    }
};

// 자식 클래스
class Dog : public Animal {
public:
    void sound() override { // 부모의 sound()를 재정의(override)
        cout << "멍멍!" << endl;
    }
};

int main() {
    Animal* a = new Dog(); // 부모 타입 포인터로 자식 객체 가리킴
    a->sound();            // 멍멍! (Dog의 sound()가 실행됨)
    delete a;
    return 0;
}
                                                                                코드 닫힘..*/
//---------------------------------------------------------------------------------

// 문제 1번. 부모 클래스는 자식 클래스에게 접근할 수 있는가??

                                                                                /*  코드 닫힘..

#include <iostream>
using namespace std;

class Mom {
public:
    void callMom() {
        cout << "부모 함수 호출" << endl;
    }

    void callChild() {
        // childMom(); // 에러! 부모는 자식 함수에 직접 접근 불가
        cout << "부모는 자식의 함수에 직접 접근 불가" << endl;
    }
};

class Child : public Mom {
public:
    void child() {
        cout << "자식 함수 호출" << endl;
    }
};

int main() {
    Child c;
    c.callMom();  // 부모 함수 호출 가능
    c.child();   // 자식  함수 호출 가능
    c.callChild(); // 부모 함수에서 자식 함수 직접 호출 불가 메시지 출력

    return 0;
}
                                                                                 코드 닫힘..*/

//---------------------------------------------------------------------------------

// 문제 2번. 다음 코드 Student(string n, int a, string m) : Person(n, a), major(m) {}
// 에서 Person(n, a)가 빠지면 생기는 일?

                                                                                   /*  코드 닫힘..

#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}

    void introduce() {
        cout << "이름: " << name << ", 나이: " << age << endl;
    }
};

// 자식 클래스 (파생 클래스)
class Student : public Person {
private:
    string major;

public:
    //Student(string n, int a, string m) : Person(n, a), major(m) {}
    Student(string n, int a, string m) : , major(m) {}
    void study() {
        cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl;
    }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용
    return 0;
} 
                                                                                  코드 닫힘..*/

//---------------------------------------------------------------------------------

// 문제 3번 : 다음 상속 접근지정자를 public에서 private 또는 protected로 바꾸면?

                                                                                   /*  코드 닫힘..

#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

//public :
//private : 
protected :
    Person(string n, int a) : name(n), age(a) {}

    void introduce() {
        cout << "이름: " << name << ", 나이: " << age << endl;
    }
};

// 자식 클래스 (파생 클래스)
class Student : public Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}
    void study() {
        cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl;
    }
};

int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용
    return 0;
}
//부모 클래스가 private/protected 상속 됐다면 
//introduce()가 public이 아니고 private 또는 protected가 되어 외부에서 호출할 수 없게 됩니다.

                                                                                     코드 닫힘..*/

//---------------------------------------------------------------------------------

// 과제 외에 프로그램 작성한 것
#include <iostream>
using namespace std;

class Gun {
protected:
    int ammo;
public:
    Gun(int a) : ammo(a) {}
    virtual void attack() {
        if (ammo > 0) { cout << "총 공격! 탄환 남음: " << ammo-- << endl; }
        else cout << "탄약 없음!" << endl;
    }
};

class Rifle : public Gun {
    bool burst = false;
public:
    Rifle(int a) : Gun(a) {}
    void toggleBurst() { burst = !burst; cout << (burst ? "연사 모드 ON" : "연사 모드 OFF") << endl; }
    void attack() override {
        if (ammo <= 0) { cout << "탄약 없음!" << endl; return; }
        if (burst && ammo >= 3) { cout << "3발 연사!" << endl; ammo -= 3; }
        else { cout << "한 발 공격!" << endl; ammo--; }
    }
};

int main() {
    Gun* g = new Rifle(5);
    g->attack();
    dynamic_cast<Rifle*>(g)->toggleBurst();
    g->attack();
    g->attack();
    delete g;
}
