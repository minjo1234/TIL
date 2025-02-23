
UI가 활성화 된 경우에만 데이터를 업데이트함 ( 메모리 누수를 빙자힌다.)

```kotlin
class HomeViewModel : ViewModel() {
	private val _allPostList = MutableLiveData<List<Post>>()  // 내부에서 변경
	val allPostList: LiveData<Live<Post>> = _allPostList // 외부에서 읽기전용 
}
```


```
@Compoable
fun PostScreen(homeViewModel)
```