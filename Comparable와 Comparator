# **JAVA - Comparable/ Comparator**

자바에서 **배열**을 정렬할 때는 **Arrays.sort()** 메서드를 사용하며, **Collection(List, Set, Map.. )** 을 정렬하기 위해서는 **Collections.sort()** 함수를 사용한다.

(Arrays.asList()는 배열을 ArrayList로 바꿔 반환하는 메서드)

```
public static void main(String[] args) {
	
	int[] intArray = {5, 9, 3, 4, 8};
	Arrays.sort(intArray);
	System.out.println(Arrays.toString(intArray));
	
	// Arrays.asList()는 배열을 ArrayList로 바꿔 반환하는 메서드
	List<String> strList = Arrays.asList("Java","Spring","Sql","Python","C");
	Collections.sort(strList);
	System.out.println(strList);
}
```

[##_Image|kage@XOtLD/btrI1Wn5Pm4/NK854qikbW4y1l7h8SJYr1/img.png|CDM|1.3|{"originWidth":354,"originHeight":52,"style":"alignCenter","filename":"1.png"}_##]

위 코드를 보면 두 함수 모두 내림차순으로 정렬한 것을 볼 수 있다.

이때 만약 strList를 알파벳 순이 아닌 문자열의 길이로 정렬하고 싶다거나 아래와 같이 Student 클래스를 객체로 생성해 정렬하고 싶다면 어떻게 해야할까? 이때 정렬 기준을 age로 할지 name 혹은 classNumber로 할지도 고민해야한다.

```
public class Student {
	int age;
	String name;
	int classNumber;

	public Student(int age, String name, int grade) {
		super();
		this.age = age;
		this.name = name;
		this.classNumber = grade;
	}

}
```

이때 사용하는 것이 **Comparable**과 **Comparator**이다. 일단, 두 개 모두 **인터페이스**이다.

정렬의 기본 조건을 생각해보면, 데이터가 순서를 가지고 있어야 한다는 것이다. 순서가 있어야 비교가 가능하기 때문이다. 즉, 데이터가 Comparable 한 특징을 가져야 한다는 것이다. 첫번째 예제에서 기본 자료형은 자바에서 자동으로 비교 가능하기 때문이고, String은 String.class를 보면 Comparable 인터페이스를 상속받는다는 것을 확인할 수 있다. 그렇기 때문에 정렬이 가능한 것!!!

(String.class)

[##_Image|kage@cDiA2V/btrI7MjKEWH/dnayosKSL9gHfFb3EXZIuk/img.png|CDM|1.3|{"originWidth":867,"originHeight":206,"style":"alignCenter","filename":"2.png"}_##]

Comparable과 Comparator 의 사용법을 알아보기 전, 각 인터페이스를 확인해보자.

**Comparable** 인터페이스는 compareTo(T o) 메서드 하나만 가지고 있다. 즉, Comparable 인터페이스를 상속받으면 **compareTo(T o) 하나의 메서드를 반드시 재정의(Override)** 해주어야 한다.

**Comparator** 인터페이스를 상속받으면 여러 메서드들 중, **compare(T o1, T o2) 메서드를 반드시 재정의** 해주어야 한다. 

(인터페이스의 모든 메서드들은 재정의해서 사용해야하지만, default, static 제한자가 붙어 있으면서 인터페이스 내에서 이미 구현된 메서드는 재정의 안 해도됨! default와 static의 차이는 재정의 가능 여부이다. (default : 재정의 가능/static : 재정의 불가능.) Comparator 인터페이스를 확인해보면 default, static으로 선언된 메서드를 제외하고 boolean equals(Object obj) 메서드 하나가 더 있음. 해당 메서드는 모든 객체의 최상위 타입 객체인 Object클래서에 이미 equals메서드가 정의되어있기 때문에 재정의 안 해도 됨.)

각 인터페이스가 재정의해야 할 함수는 아래와 같음.

**Comparable → compareTo(T o)**

**Comparator → compare(T o1, T o2)**

각 메서드를 보면 매개 변수의 갯수가 다르다. 정리하면, **Comparable 의 메서드는 자기 자신과 매개변수를 비교**하는 것이고, **Comparator 의 메서드는 두 매개변수를 비교하는 것**에서 차이가 난다.

각 인터페이스의 사용법을 알아보자.

### **Comparable**

위의 Student 클래스의 name의 알파벳 순으로 정렬하기 위해서 아래와 같이 코드를 작성하면 된다.

```
package sort;

import java.util.Arrays;

class Student implements Comparable<Student> {
	int age;
	String name;
	int classNumber;

	public Student(int age, String name, int grade) {
		super();
		this.age = age;
		this.name = name;
		this.classNumber = grade;
	}

	@Override
	public String toString() {
		return "Student [age=" + age + ", name=" + name + ", classNumber=" + classNumber + "]";
	}

	@Override
	public int compareTo(Student o) {
		return this.name.compareTo(o.name)*-1;
	}
}

public class Sort {
	public static void main(String[] args) {
		
		Student[] students = {new Student(22, "Kate", 11),new Student(20,"Anna", 12)};
		
    //Comparable 사용할 때 매개변수: 정렬하고 싶은 배열
		Arrays.sort(students); 

		
		System.out.println(Arrays.toString(students));
		
	}
}
```

아래와 같이 이름 순으로 정렬된 것을 확인할 수 있다.

[##_Image|kage@d6ervv/btrI4Uo24ex/t7IyXLMvu0so9cNTY4eXF0/img.png|CDM|1.3|{"originWidth":1044,"originHeight":34,"style":"alignCenter","filename":"3.png"}_##]

Student클래스에서 compareTo()메서드를 재정의 시,

String의 compareTo() 메서드를 사용하여 자기 자신과 매개변수의 name을 기준으로 문자열 비교하여 정렬하였다. String compareTo() 메서드는 비교 대상보다 자기 자신이 크면 양수, 작으면 음수가 return된다. (이것이 Student클래스의 compareTo()에서 return되기 때문에, Student클래스의 compareTo()메서드도 동일하게 return!!!!!)

재정의한 **compareTo() 메서드**는

-   현재 객체 < 파라미터로 넘어온 객체: 음수 return
-   현재 객체 == 파라미터로 넘어온 객체: 0 return
-   **현재 객체 > 파라미터로 넘어온 객체: 양수 return**

결과적으로 음수 또는 0이면 객체의 자리가 그대로 유지되며, **양수인 경우에는 두 객체의 자리가 바뀐다.(오름차순 정렬)**

내림차순으로 정렬하고 싶은 경우 return 값에 -1을 곱해주면 된다.

### Comparator

Collections.sort(list, comparator)와 Arrays.sort(array, comparator) 메서드는 리스트나 배열 뒤에 Comparator 객체가 들어간다. 이 메서드는 자바에서 제공하는 **정렬 기준과 다르게 정렬**하고 싶을 때 사용하는 메서드로 해당 매개변수에 들어가는 정렬 기준에 맞게 배열이나 리스트를 정렬할 수 있다.

위에서 말했듯이 Comparator는 compare(T o1, T o2)를 재정의하므로, 비교대상 2개를 가지고 비교하게 된다.

이 메서드는

-   o1의 객체 < o2의 객체: 음수 return
-   o1의 객체 ==o1의 객체: 0 return
-   **o1의 객체 >o2의 객체: 양수 return**

Comparable과 마찬가지로 음수 또는 0이 return되면 객체의 자리가 그대로 유지되며, **양수인 경우에는 두 객체의 자리가 바뀐다.(오름차순 정렬)** 내림차순으로 정렬하고 싶은 경우 return 값에 -1을 곱해주면 된다.

Student 클래스에서 이름의 알파벳 순이 아닌 길이로 비교하여 정렬하고 싶다면 아래와 같이 정렬하면 된다.

```
class StringLengthComparator implements Comparator<Student>{

	@Override
	public int compare(Student o1, Student o2) {
		int i1 = o1.name.length();
		int i2 = o2.name.length();
		
		return Integer.compare(i1,i2);
	}

}
class Student {
	int age;
	String name;
	int classNumber;

	public Student(int age, String name, int grade) {
		super();
		this.age = age;
		this.name = name;
		this.classNumber = grade;
	}

	@Override
	public String toString() {
		return "Student [age=" + age + ", name=" + name + ", classNumber=" + classNumber + "]";
	}
}

public class Sort {
	public static void main(String[] args) {
		
		Student[] students = {new Student(22, "KatePark", 11),new Student(20,"Anna", 12)};

		//Comparator 사용할 때 매개변수: 정렬하고 싶은 배열, 정렬 기준인 Comparator객체 
		Arrays.sort(students,new StringLengthComparator()); 
		
		System.out.println(Arrays.toString(students));
		
	}
}
```

[##_Image|kage@bgamI9/btrI3uqCWjF/KY7OjqKX3IZEg8fX7s5mGk/img.png|CDM|1.3|{"originWidth":1044,"originHeight":34,"style":"alignCenter","filename":"4.png"}_##]

동일한 작동(code 간략하게 수정)

```
//class StringLengthComparator implements Comparator<Student>{
//
//	@Override
//	public int compare(Student o1, Student o2) {
//		int i1 = o1.name.length();
//		int i2 = o2.name.length();
//		
//		return Integer.compare(i1,i2);
//	}
//
//}
class Student implements Comparator<Student> {
	int age;
	String name;
	int classNumber;

	public Student() {
	};

	public Student(int age, String name, int grade) {
		super();
		this.age = age;
		this.name = name;
		this.classNumber = grade;
	}

	@Override
	public String toString() {
		return "Student [age=" + age + ", name=" + name + ", classNumber=" + classNumber + "]";
	}

	@Override
	public int compare(Student o1, Student o2) {
		int i1 = o1.name.length();
		int i2 = o2.name.length();

		return Integer.compare(i1, i2);
	}

}

public class Sort {
	public static void main(String[] args) {

		Student[] students = { new Student(22, "KatePark", 11), new Student(20, "Anna", 12) };

		//Comparator 사용할 때 매개변수: 정렬하고 싶은 배열, 정렬 기준인 Comparator객체 
		Arrays.sort(students, new Student());

		System.out.println(Arrays.toString(students));

	}
}
```

### **Comparator - inner class 사용**

위 동작을 **inner class**로 구현.

```
class Student {
	int age;
	String name;
	int classNumber;

	public Student() {
	};

	public Student(int age, String name, int grade) {
		super();
		this.age = age;
		this.name = name;
		this.classNumber = grade;
	}

	@Override
	public String toString() {
		return "Student [age=" + age + ", name=" + name + ", classNumber=" + classNumber + "]";
	}
}

public class Sort {
	public static void main(String[] args) {

		Student[] students = { new Student(22, "KatePark", 11), new Student(20, "Anna", 12) };

		// inner class
		Arrays.sort(students, new Comparator<Student>() {
			@Override
			public int compare(Student o1, Student o2) {
				int i1 = o1.name.length();
				int i2 = o2.name.length();

				return Integer.compare(i1, i2);
			}

		});
		System.out.println(Arrays.toString(students));

	}
}
```

[Reference]
https://st-lab.tistory.com/243
https://velog.io/@injoon2019/%EC%9E%90%EB%B0%94-Comparator%EC%99%80-Comparable
