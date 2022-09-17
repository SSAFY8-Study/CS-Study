## **📌1. Override**

Override(메서드 재정의)는 조상 클래스에 정의된 메서드를 자식 클래스에서 적합하게 수정하는 것을 의미합니다.

Override를 위해서는 몇 가지 조건이 필요한데,

- 메서드(Method)의 이름이 동일해야 한다.
- 매개 변수(Parameter)의 타입과 개수, 순서가 동일해야 한다. (만약 파라미터를 다르게 한다면 Overloading이 됩니다.)
- 접근 제한자는 부모 클래스의 메서드보다 범위가 같거나 더 넓어야 한다.
- Retrun type이 동일해야 한다.
- 조상 클래스보다 더 큰 예외(Exception)를 던질 수 없다.
- Override한 메서드의 오류를 확인하기 위한 디버깅을 진행할 때 위의 조건들을 충족하는지 일차적으로 확인하는 것이 많은 도움이 될 수 있습니다.


만약 오류를 정확히 파악하기 어렵다면 ***@Override***를 선언하여 컴파일러의 도움을 받는 것도 좋은 방법입니다.

***@Override***는 컴파일러에게 해당 메서드가 Override를 적용한 메서드인 것을 알려주는 역할을 해주며 코드에 직접적으로 영향을 주지 않아 선언을 하지 않는다고 해도 오류가 발생하지는 않습니다.

Override한 메서드들을 많이 사용하다 보면 조건들을 놓치는 경우가 발생할 수 있으므로, 가급적 @Override를 선언하며 코딩을 진행하는 것이 개발자 본인의 코드를 파악하는데도 도움이 될 수 있습니다.

 

코딩을 하면서 많이 보게 되는 대표적인 Override 사례 몇 가지를 보겠습니다.

<br>
 
 

### **Object Class의 toString()** ###
<pre><code>public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }</code></pre>
<br>
 

Object Class는 모든 클래스들의 조상 클래스이기 때문에 모든 클래스에서 Object 클래스의 메서드를 Override 할 수 있습니다.

Object Class의 toString()은 객체를 문자열로 변경하는 메서드로 객체의 이름을 return 하도록 정의되어 있습니다.

코딩할 때 객체의 이름을 출력하고 할 때도 있을 수 있으나, 대부분은 객체가 저장하고 있는 데이터를 출력하고 싶을 때가 많습니다.

따라서 이를 위해 toString() 메서드를 Override해서 활용할 수 있습니다.

 
<pre><code>
@Override
public String toString() { 
return "Name= "+ name + " Age: "+ age ;
}</code></pre>

 
<pre><code>
@Override

public String toString() {
  StringBuilder sb = new StringBuilder();

  sb.append(getName()).append("\t").append(getAge());

  return sb.toString();
}
</code></pre>
 

만약 클래스에 저장된 이름과 연령에 해당하는 데이터를 출력하고자 한다면 위와 같이 Override를 한 후에 System.out.println(className.toString());과 같은 방법을 활용할 수 있습니다.

 
<br>

### **Object Class의 equals()** ###
<br>
<pre><code>
 public boolean equals(Object obj) {
    return (this==obj);
}</code></pre>

 

equals() 메서드는 두 객체가 동일한 객체인지 비교해주는 메서드입니다.

두 객체가 참조하는 주소 값을 기준으로 객체를 비교하는데, 객체가 서로 동일한 데이터를 가지고 있더라도 참조하는 객체의 주소 값이 다르면 False를 리턴합니다.

객체의 데이터를 비교해보고 싶다면 위의 메서드를 Override 하여 사용해야 합니다.

 <br>
<pre><code>
@Override

public boolean equals (Object obj) {

  if(obj != null && obj instanceof ClassName) {
      ClassName class1 = (ClassName) obj;
      return var.equals(class1.var);

  }

 return false;
}
</code></pre>
 

Override는 파라미터가 동일해야 하므로, Object 클래스를 받아오기 때문에 비교하고자 하는 클래스에 맞게 형 변환을 해준 후 변수 값을 직접 비교할 수 있도록 구성해야 합니다.

위와 같은 구성을 통해 비교하고자 하는 클래스와 변수명을 직접 비교할 수 있도록 메서드를 Override 하여 활용할 수 있습니다.

 <br>


## 📌2. Singleton ##

Singleton은 자바에서 많이 활용하는 디자인 패턴으로 외부에서 객체 생성을 제한하여 한 번의 객체 생성으로 재 사용이 가능하도록 한 후 메모리 낭비를 방지하기 위해 활용합니다.

Singleton에도 몇 가지 조건들을 충족해야 하는데,

- 외부에서 생성자에 접근하지 못하도록 생성자의 접근 제한자를 private으로 설정해야 합니다.
- 내부에서는 직접 객체를 생성하고 멤버 변수(Parameter)들도 private로 설정합니다.
- 외부에서 멤버 변수(Parameter)에 접근할 수 있도록 getter method를 생성합니다.
- 객체 없이 외부에서 접근이 가능하도록 getter method와 변수들을 static으로 선언합니다.

Singleton을 활용한 class를 선언했을 때는 getter method를 통해 객체를 참조하기 때문에 하나의 객체를 재사용할 수 있게 됩니다. 

 <br>
<pre><code>
class SingletonClass {
  private static SingletonClass instance = new SingletonClass();

  private SingletonClass { } //default constructor

  

  public static SingletonClass getInstance() {
      return instance;
    }
  }</code></pre>
  <br>

Singleton 패턴의 기본 형식은 위와 같습니다.

내부에서 객체를 생성한 후에 private으로 설정하여 외부에서 접근할 수 없도록 제한해야 하고, getter method인 getInstance()를 통해 객체를 리턴해줘서 외부에서 하나의 객체를 재사용할 수 있도록 해줘야 합니다.

 
<br>
 
<pre><code>
 public class Main {

   public static void main(String[] args) {
      SingletonClass sc1 = SingletonClass.getInstance();
      SingletonClass sc2 = new SingletonClass(); //->오류 발생!!
    }

}
</code></pre>
<br>
외부인 Main에서 SingletonClass에 접근하기 위해서는 위와 같은 방법을 통해 객체에 접근할 수 있습니다.

 

Singleton을 활용할 때 가장 주의해야 할 점은 외부에서의 활용입니다.

만약 기존 class를 singleton class로 변형했다면, 외부에서 객체를 생성하는 부분이나 생성자에 접근하는 부분, 멤버 변수(Parameter)를 활용하는 부분을 다시 한번 확인하여, Singleton 패턴에 맞게 수정하여 오류가 발생하지 않도록 해줘야 합니다. 
