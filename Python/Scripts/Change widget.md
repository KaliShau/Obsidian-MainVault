
___
#### Change widget:
```
def change(self, widget):
	layout = self.main_window.navigationLayout.layout()
	layout.itemAt(0).widget().setParent(None)
	layout.addWidget(widget)
```
Данный скрипт предназначен для смены окон внутри layout