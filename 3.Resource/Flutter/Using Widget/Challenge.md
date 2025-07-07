
App Dark Mode, White Mode challenge 


```dart
appBar: AppBar(
	centerTitle: true, 
	title: Text('flutter dark mode test),
	actions: [
		IconButton() {
			onPressed: () {
				isDarkModeNotifier.value = !isDarkModeNotifier.value
			}
			icon: ValueListenableBuilder(
				valueListenable: isDarkModeNotifier
				builder: (context, isDarkMode, child) {
					return isDarkMode  
						? Icon(Icons.light_mode) 
						: Icon(Icons.dark_mode)
				}
			)
		}
	]
)
```


---


	.gridWrap .top .control .new



- css 수정 - 1  - o 
- 실시간 default 설정  - 2  - o 
- 모니터링 - 가상머신 리소스현황 : 검색확인 - 3  진행중 
- dashBoard 데이터확인,  - 4  
- aria_vm_day_metric 수정 - IDLE 정상적으로 나오도록  4 
- 데이터 채워넣기.  5 



스케쥴러에서 조회가 안되는것인지 telegraf 연동이 안 된 것인지 확인하기.


