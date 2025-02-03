
수명 주기와 구성 변경에 관한 수명 주기 문제에 대해서 설명할 때 viewModel을 사용하지않고
`rememberSaveable` 을 사용하면 손쉽게 앱의 데이터를 저장할 수 있다. -  인스턴스의 상태를 저장하거나 사용할 수 있다. 하지만 단점으로는 `composable` 근처에 보관하거나 `composable`에 내부에 보관해야 한다는 점인데

프로젝트의 규모가 켜질경우 데이터와 로직을 컴포저블에서 멀어지기 때문에 다른 해결방안을 찾게 되었는데 그게 `viewModel` 입니다.



1.viewModel을 사용하는 이유 ?

- 데이터 보존 : viewModel의 장점 `activity`가 파괴되더라도 저장된 데이터는 손실되지 않는다.
- 하지만 프로세스가 종료되어 액티비티가 파괴되는 경우에는 데이터가 손실된다.
- 액티비티의 재생성을 하는 경우에만 캐시를 이용하여 데이터를 캐시합니다.

---

ViewModel : UI에 상태를 노출하고 관련 비즈니스 로직을 캡슐화한다.
주요장점은 상태를 캐시하고 구성 변경을 통해 지속한다는 점

UI간 활동 간을 이동하거나 화면을 회전할 때와 같이 구성 변경을 따를 필요가 없다.

ViewModel의 역할

UI에 표시하는 데이터를 보관하는 일반 클래스 

----

2.UI 상태저장  

UI 상태에 대한 사용자 기대와 상태 보존에 사용할 수 있는 옵션에 대해 설명합니다.
시스템의 액티비티나 애플리케이션을 파괴된 후 액티비티의 UI 상태를 저장하고 복원하는 것은 좋은 사용자 경험을 위해 필수적

사용자는 UI 상태가 동일하게 유지되기를 기대하지만, 시스템은 액티비티와 저장된 상태를 파괴할 수 있습니다.
UI 상태를 동일하게 유지하기 위해 사용되는 것들

ViewModel
제트팩 컴포즈 rememberSaveable
조회수 onSaveInstanceState
뷰모델 : SavedStateHandle

----

ViewModel

Activity, Fragment에 대한 데이터를 처리하고 관리하는 클래스
Activity와 Fragment간의 통신도 처리한다.

ViewModel의 목적은 Activity 또는 Fragment에 필요한 정보를 수집하고 보관하는 것입니다.
ViewModel의 유일한 책임은 UI의 데이터를 관리하는 것입니다. , 
계층 구조에 액세스하거나 Activity또는 Fragment에 대한 참조를 보유해서는 안된다.


---

3.ViewModel 사용법

![[Pasted image 20250203215615.png]]

ViewModel은 UI에 필요한 모든 데이터를 보유하고 처리한다.

데이터를 관리하려고 ViewModel을 작성하려고 하는데 먼저 Kotlin의 속성위임(property delegate)과 delefate class 

`var`은 값을 할당할 때 setter, 속성 값을 읽을 때 getter를 호출한다.
`val`은 read-only기 때문에 기본적으로 getter만 생성된다.

`kotlin`에서 by를 활용해 속성 위임을 사용하면 getter-setter의 역할을 다른 클래스에 넘길 수 있다.
다른 클래스를 대리자 클래스(delegate class)라고 한다.


### 왜 속성을 위임하는데 ? 

```kotlin
private val viewModel = GameViewModel()
```

이렇게 기본 생성자를 사용해 초기화하면 참조상태를 읽게되는데, 기기를 회전하여 Activity가 소멸할 경우 다시
초기 상태의 액티비티가 실행된다.

```kotlin
private val viewModel: GameViewModel by viewModels()
```

	속성 위임 방식으로 Viewmodel 객체의 책임을 viewModels라는 별도 클래스에  위임을 하게 되면 
객체는 대리자 클래스인 viewModels에 의해 처리된다. 
첫번째 액서스 시에는 자동으로 viewModel을 만들어주고,
구성이 변경되어도 값을 유지하다가 반환해준다.

cf) Fragment 간 데이터 전달할 수 있는 공유 ViewModel

```kotlin
private val sharedViewModel: OrderViewModel by activityViewModels()
```


### ViewModel의 데이터 안전하게 보호하기(**backing property**)

잊지 말자. ViewModel의 데이터를 **다른 클래스에서 수정할 수 없도록** 해야한다. 그러려면 데이터를 public으로 노출하지 말아야 한다.

- ViewModel 내부에서는 데이터를 수정할 수 있어야 한다. 그래서 `privat var`이어야 한다.
- ViewModel 외부에서는 데이터 읽기만 가능하고 수정하면 안 되기 때문에 `public val`이어야 한다.

|내부에서 활용하는 데이터|외부에서 활용하는 데이터|
|---|---|
|private|public|
|var|val|


그래서 **지원 속성(backing property)**를 이용한다. 이렇게 하면 **앱 데이터가 외부 클래스로부터 원치 않게 변경되지 않게 보호**할 수 있다.



참고문서 :

Jetpack Compose 공식문서 : https://developer.android.com/topic/libraries/architecture/viewmodel
UI 상태저장 : https://developer.android.com/topic/libraries/architecture/saving-states#onsaveinstancestate

ViewModel을 안전하게 사용하자 : https://velog.io/@hs0204/ViewModel%EC%9D%84-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90

---------
