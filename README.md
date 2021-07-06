# JAVA8

1. 메소드 래퍼런스 ::

* ex\)\(Apple a\) -&gt; a.getWeight\(\)  =&gt; apple::getWeight

```text
File[] hiddenFiles = new File(".").listFiles(File::isHidden);
```

2.**프레디케이트\(predicate&lt;T&gt;\)** 인터페이스는 test 라는 추상 메서드를 정의하며 test는 제네릭 형식 T의 객체를 인수로 받아 불린을 반환한다.

* IntPredicate, DoublePredicate 등 특정 형식을 입력으로 받는 것으로 사용 가능
* ex\) Predicate&lt;String&gt; result = \(String s\) -&gt; !s.isEmpty\(\)
* ex\) IntPredicate result = \(int i\) -&gt; i%2 == 0 ;
* List&lt;Apple&gt; result = filterApples\(inventory, new     AppleheavyWeightPredicate\(\)\);
* negate ,and,or 세가지 메소드를 제공 한다.                                                  -  Pridecate&lt;Apple&gt; result = redApple.negate\(\)\(객체 결과 반환\)     - Pridecate&lt;Apple&gt; reuslt = redApple.and\(a-&gt;a.getWeight\(\)&gt;150\) 두 프레디케이티를 연결해서 새로운 프레디 테이트 만들기             -Pridecate&lt;Apple&gt; result = redApple.and\(a-&gt;a.getWeight\(\) &gt; 150\).or\(a -&gt; "green".equals\(a.getColor\(\)\)\); 두개의 조건 

```text
public interface ApplePridicate{
    boolean test(Apple apple)
}

pulbic class AppleheavyWeightPredicate implements ApplePredicate{
    public boolean test(Apple apple){
        return apple.getWight() > 150;
    }
}


pulbic class AppleGreenColorPredicate implements ApplePredicate{
    public boolean test(Apple apple){
        return "green".equals(apple.getColor));
    }
}


public static List<Apple> filterApples(List<Apple> inventory,ApplePredicate p){
    List<Apple> result = new ArrayList<>();
    for(Apple apple: inventory){
        if(p.test(apple)){
            result.add(apple);
        }
    }
    return result;
}


```

3. 람다로 사용 

\(parameters\) -&gt; expression

\(parameters\) -&gt; {statements;}

List&lt;Apple&gt; result 

= filterApples\(inventory,\(Apple apple\)-&gt;"red".equals\(apple.getColor\)\); 

4.Comparator로 정렬하기 

* inventory.sort\(Apple a1, Apple a2\) -&gt; a1.getWeight\(\).compareTo\(a2.getWeight\(\)\);
* Comparator&lt;Apple&gt; c = Comparator.comparing\(Apple::getWeigth\);
* Invetory.sort\(comparing\(Apple::getWeight\)\)
* Invetory.sort\(comparing\(Apple::getWeight\).reversed\(\).thenComparing\(Apple::getCountry\)\); 첫번째 인자 비교해서 같다고 판단되면 두번째 비교자에 객체 전달. 



5. **Consumer&lt;T&gt; 인터페이스**는 제네릭 형식 T를 객체를 받아서 void를 반환하는 accept라는 추상 메서드를 정의한다.\(\) -&gt; void

* ex\) aa\(Arrays.asList\(1,2,3,4,5\), \(Integer i\) -&gt; System.out.printld\(i\)
* IntConsumer 등 특정 형식을 입력으로 받는 것으로 사용 가능

6.**Function&lt;T,R&gt; 인터페이스**는 제네릭 형식 T를 인수로 받아서 제네릭 형식 R 객체를 반환하는 apply 라는 추상 메서드를 정의한다.

* List&lt;Integer&gt; result = map\(Arrays.asList\("lambda","in","action"\), \(String s\) -&gt; s.length\(\)\);
* Function&lt;Integer,Apple&gt; c2 = Apple::new;
* ToIntFunction&lt;T&gt;,IntToDubleFunction 등 특정 형식을 입력으로 받는 것으로 사용 가능
* andThen,compose 두가지 디폴트 메소드를 제공.                                Function&lt;Integer,Integer&gt; f = x-&gt; x+1;                                                      Function&lt;Integer,Integer&gt; g = x-&gt;x\*2;                                                       Function&lt;Integer,Integer&gt; h = f.andThen\(g\);                                         int result = h.apply\(1\); =&gt; 답은 4 andthen은 주어진 함수를 먼저 적용한 결과를 다른 함수의 입력으로 전달하는 함수를 반환                    Function&lt;Integer,Inter&gt; h = f.compose\(g\);                                                 int result = h.apply\(1\); =&gt; 답은 3 인수 주어진 함수를 먼저 실행한 다음에 그 결과를 외부 함수 인수로 제공.

7. Supplier&lt;T&gt;는 \(\) -&gt; T 형식의 시그너처를 갖는 수상 메서드 get을 정한다.

* ex\) \(\) -&gt; new Apple\(10\) 객체 생성 

8. IntBinaryOpreator는\(int,int\) -&gt;int 형식으로 추상메서드 applyAsInt 정의한다.

* ex\) \(int a, int b\) -&gt; a\*b  두값 조인 

