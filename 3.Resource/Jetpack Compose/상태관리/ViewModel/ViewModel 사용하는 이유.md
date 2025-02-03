
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


참고문서 :

Jetpack Compose 공식문서 : https://developer.android.com/topic/libraries/architecture/viewmodel
UI 상태저장 : https://developer.android.com/topic/libraries/architecture/saving-states#onsaveinstancestate

ViewModel을 안전하게 사용하자 : https://velog.io/@hs0204/ViewModel%EC%9D%84-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90

---------
