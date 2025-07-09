
Two states,
ValueNotifier: hold the data 
ValueListenableBuilder: listen to the data (don't need the setState)

```dart 
ValueNotifier<int> selectedPageNotifier = ValueNotifier(0);
```


```dart
ValueListenableBuilder(
	valueListenable: selectedPageNotifier,
	builder: (context, selectedPage, child) {
		 NavigationBar(`),
		 onDestinationSelected:
			 (value) => {selectedPageNotifier.value = value};
		selectedIndex: selectedPage,
	}
)
```




