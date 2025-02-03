
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

UI 상태저장 


참고문서 :

Jetpack Compose 공식문서 : https://developer.android.com/topic/libraries/architecture/viewmodel
