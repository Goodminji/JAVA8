# Stream

1. Stream 스트림이란 테이터 처리 연산을 지원하도록 소스에서 추출된 연속된 요소.

```text
List<String> result = meue.stream()
                          .filter(d -> d.getCalories() > 300)
                          .map(Dish::getName)
                          .limit(3)
                          .collect(toList());
```

* filter,map,limit는 서로 연결되어 파이프라인을 형성한다.\(중간연산- sorted,distinct,skip,flatmap\) 
* collect로 파이프라인을 실행한 다음에 닫는다.\(최종연산-foreach\(void반환\),count\(long 반환\),antyMatch,noneMatch,allMatch,findAny,findFirst,forEach,reduce,count\) 

```text
List<String> result = words.stream()
                          .map(w -> w.split("") // 각 단어를 개별 문자를 포함하는 배열로 변환
                          .flatMap(Arrays::stream) // 생성된 스트림을 하나의 스트림으로 평면화
                          .distinct()
                          .collect(toList());
```

flatMap은 각 배열을 스트림이 아니라 스트림 콘텐츠로 매핑한다. 하나의 평면화된 스트림을 반환.

```text
두개의 숫자 리스트가 있을때 모든 숫자 쌍의 리스트를 반환
예를 들어 [1.2.3] , [3,4] 가 주어지면 [(1,3),(1,4),(2,3),(2,4),(3,3),(3,4)] 반환
List<Integer> numbers1 = Arrays.asList(1,2,3);
List<Integer> numbers2 = Arrays.asList(3,4);
List<Int[]> pairs = number1.stream()
                           .flatMap(i -> numbers2.stream().map(j -> new int[i,j])
                           .collect(toList());
```

2. 검색과 매칭

* anyMatch: 프레디케이트가 주어진 스트림에서 적어도 한 요소가 일치하는지 확인할떄 불린을 반환하는 최종연산.
* allMatch: 스트림의 모든 요소가 주어진 프레디케이트와 일치하는 지를 검사.
* noneMatch: 주어진 프레디케이트와 일치하는 요소가 없는지 확인.
* findAny\(\) 현재 스트림에서 임의의 요소를 반환
* Optional&lt;T&gt;이란 값의 존재나 부재 여부를 표현하는 컨테이너 클래스다. 이것을 이용해서 null확인 관련 버그 피할수 있음.                                                                   -   inpresent\(\)는 Optional 이 값을 포함하면 true, 아니면 false 반환..                      -   ifPresent\(Consumer&lt;T&gt; bolck\)은 값이 있으면 bolck을 실행..                              -   T get\(\)은 값이 존재하면 값을 반환 없으면 NoSuchElementException 발생...      -   T orElse\(T other\)는 값이 있으면 값을 반환 값이 없으면 기본값을 반환..                                                      
* findFirst\(\) 첫번째 요소 찾기.

```text
ex) meus.stream().filter(Dish::isVegettrain)
                  .findAny()
                   .ifpresent(d -> System.out.println(d.getName());
// 값이 잇으면 출력되고 없으면 아무일도 일어 나지 않음.
```

3. 리듀싱 : 모든 스트림 요소를 처리해서 값으로 도출한다. reduce \(최종연산\)

* ex\) int sum = numbers.stream\(\).reduce\(0,\(a,b\)-&gt;a,b\);                             초기값 0 , 두요소를 조합에서 새로운 값을 만드는 BinaryOperator&lt;T&gt;를 사용
* 초기값을 받지 않아도 되는 reduce도 있는데 이건 Optional 객체를 반환한다.  Optional&lt;Integer&gt; max = numbers.stream\(\).reduce\(Integer::max\);

객체 스트림 복원하기 

* 숫자 스트림으로 만든 다음에 특화되지 않는 스트림으로 봉원하는 방법은 .boxed\(\)

4. 기본형 특화 스트림

1\) 숫자 스트림으로 매핑 

* mapToInt, mapToDouble,MapToLong ,, intStream은 max,min,sum,avg 많은 것을 메소드를 지원                                                      int calories = menu.strema\(\).mapToInt\(Dish::getCalories\).sum\(\);
* rangeClosed\(1,100\) 숫자 범위를 나타낸다 시작값과 종료값이 결과에 포함된다. \(range는 시작값과 종료값이 결과에 포함되지 않는다\)

2\) iterate\(무한 스트림\)

3\) generate는 Supplier&lt;t&gt;를 인수로 받아서 새로운 값을 생성 



[https://futurecreator.github.io/2018/08/26/java-8-streams/](https://futurecreator.github.io/2018/08/26/java-8-streams/) 

