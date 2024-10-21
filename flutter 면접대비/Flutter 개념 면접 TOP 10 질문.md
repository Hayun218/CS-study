작성일시: 24.10.20 (Sun)

1. StatelessWidget과 StatefulWidget의 차이에 대해 설명해 주세요.

   **StatelessWidget**과 **StatefulWidget**은 둘 다 Flutter의 UI를 만드는 데 사용되지만, **상태 관리** 방식에서 차이가 있습니다. StatelessWidget은 내부적으로 상태를 변경할 수 없는 위젯입니다. 즉, 화면이 처음 빌드된 이후에는 데이터나 UI가 변하지 않습니다. 반면, StatefulWidget은 내부적으로 상태를 관리할 수 있으며, `setState` 메서드를 통해 상태가 변경되면 해당 위젯의 UI를 다시 렌더링할 수 있습니다. 상태 변화가 필요한 경우 StatefulWidget을 사용해야 합니다.
   
   
3. BuildContext에 대해 설명해주세요.

   **BuildContext**는 위젯 트리 내에서 현재 위젯의 위치와 관련된 정보를 제공합니다. Flutter는 트리 구조로 위젯을 구성하고, **BuildContext**를 통해 부모와 자식 간의 관계를 유지하고 위젯 트리 내에서 위젯 간에 상호작용이 가능하도록 합니다.
   
4. ListView와 ListView.builder의 차이점에 대해 설명 해주세요.

   ListView는 모든 아이템을 한 번에 렌더링하는 방식입니다. 즉, 리스트가 고정되어 있고 아이템의 개수가 적을 때 사용하기 적합합니다. 반면 ListView.builder는 스크롤할 때마다 필요한 아이템만 빌드하는 방식으로, 아이템이 많거나 무한 스크롤이 필요한 경우 메모리 효율적으로 사용할 수 있습니다.
   
5. Dart에서 제공하는 컬렉션의 종류와 각각의 개념을 설명해주실 수 있나요?

   - **List**: 순서가 있는 아이템의 모음으로, 중복된 값을 허용합니다. 배열과 유사합니다.
   - **Set**: 순서가 없고 중복을 허용하지 않는 컬렉션입니다.
   - **Map**: 키와 값의 쌍으로 이루어진 컬렉션으로, 키는 고유해야 하고 값은 중복될 수 있습니다.
   
6. 위젯이 빌드되는 과정을 주요 3가지의 위젯 트리를 통해 설명해 주세요.

   Flutter는 위젯을 렌더링하는 과정에서 세 가지 주요 트리를 사용합니다:
   - **Widget Tree**: 개발자가 작성하는 위젯 트리로, 위젯 간의 계층 구조를 나타냅니다.
   - **Element Tree**: 위젯의 인스턴스와 해당 위치를 관리하며, 위젯과 렌더 트리 간의 연결고리 역할을 합니다.
   - **Render Tree**: UI를 실제로 렌더링하기 위한 트리로, 각 위젯의 렌더링 동작을 정의합니다.

7. Inherited Widget에 대해 설명해주세요.

   **InheritedWidget**은 자식 위젯들이 상태에 접근할 수 있도록 상태를 위젯 트리 상위에서 하위로 전달하는 역할을 합니다. 이를 통해 자식 위젯들은 `context`를 사용하여 상위에서 정의한 데이터를 구독하고 필요할 때 접근할 수 있습니다.
   
8. Flutter에서 사용되는 Sliver에 대한 개념과 언제 사용하는지 설명해 주세요.

   **Sliver**는 스크롤 가능한 영역을 다룰 때 사용하는 위젯입니다. 리스트나 그리드를 스크롤할 때 Sliver를 사용하면 화면에 보이는 영역만 빌드하는 등의 최적화가 가능합니다. 주로 `CustomScrollView`와 함께 사용되며, `SliverList`, `SliverGrid`와 같은 Sliver 위젯을 배치합니다.
   
9. Scaffold.of(context) 코드가 어떻게 작동하는지 BuildContext의 개념을 사용하여 설명해 주세요.

   `Scaffold.of(context)`는 **BuildContext**를 통해 현재 위젯의 부모 위젯 트리에서 `Scaffold`를 찾습니다. `Scaffold`는 `MaterialApp`이나 화면 전체 레이아웃의 기본적인 구조를 담당하는 위젯입니다. `Scaffold`가 상위 위젯 트리에 없으면 오류가 발생할 수 있으며, 이 경우 `Builder`를 사용하여 별도의 `context`에서 접근하는 방식이 필요합니다.
   
10. mixin에 대해서 설명해주세요

   **Mixin**은 클래스의 기능을 다른 클래스에 추가할 수 있도록 하는 일종의 클래스입니다. Dart에서는 다중 상속을 지원하지 않지만, mixin을 사용하여 여러 클래스에서 공통 기능을 공유할 수 있습니다. `with` 키워드를 사용하여 mixin을 적용합니다.
   
11. 해당 코드에서 출력되는 알파벳 대문자를 순서대로 나열해 주세요.
  ```dart
void main() {  
  print('A');  
  Future(() {  
    print('B');  
    Future(() => print('C'));  
    Future.microtask(() => print('D'));  
    Future(() => print('E'));  
    print('F');  
  });  
  Future.microtask(() => print('G'));  
  print('H');  
}
```
- 동기 작업 `print('A')` → 출력: `A`
- 동기 작업 `print('H')` → 출력: `H`
- `Future.microtask(() => print('G'))` → 출력: `G`
- Future가 시작되고 내부 동기 작업인 `print('F')` → 출력: `F`
- `Future.microtask(() => print('D'))` → 출력: `D`
- 비동기 작업에서 예약된 `print('B')` → 출력: `B`
- 비동기 작업에서 예약된 `print('C')` → 출력: `C`
- 비동기 작업에서 예약된 `print('E')` → 출력: `E`
##### 흐름 설명:

1. **`Future(() { ... })` 블록**은 비동기적으로 예약되지만, **이 안의 동기 작업**은 예약과 동시에 즉시 실행됩니다.
    - 즉, 이 블록 안에서 **`print('B')`와 `print('F')`는 동기적으로 실행**되는데, `F`가 나중에 위치한 코드이므로 먼저 실행됩니다.
      
2. 그러나, 이 **비동기 예약 블록 내부**에서 `Future.microtask(() => print('D'))`는 **`microtask` 큐에 들어가서 최우선적으로 실행**됩니다.
    - **microtask**는 일반 `Future()`보다 우선순위가 높기 때문에 먼저 실행됩니다.
    - 그래서 `D`가 `B`보다 먼저 출력됩니다.
      
1. **`B`는 왜 나중에 출력되는가?**
    - `B`는 동기 코드이지만, **비동기 예약 블록** 내부에 있으므로, **비동기 예약과 microtask 처리 후** 나중에 실행됩니다.
    - `F`는 비동기 예약을 끝내고 동기적으로 즉시 실행되기 때문에 **먼저 출력**됩니다.


**참고문서**
1. https://velog.io/@ximya_hf/flutter-interview-questions
