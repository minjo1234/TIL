
```dart
home: Scaffold(
	appBar: AppBar(title: Text('Flutter Map'), centerTitle: true),
	bottomNavigationBar: NavigationBar(
		destinations: [
			NavigationDestination(icon: Icon(Icons.home), label: 'Home'),
			NavigationDestination(icon: Icon(Icons.person), label: 'Person'),
		],
		onDestinationSelected: (int value) => {},
		selectedIndex: 1,
	)
)```


![[Pasted image 20250518163810.png| 300]]


---
