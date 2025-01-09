
___
#### Change widget:
```
def change(self, widget):
	layout = self.main_window.navigationLayout.layout()
	layout.itemAt(0).widget().setParent(None)
	layout.addWidget(widget)
```
Данный скрипт предназначен для смены окон внутри layout
#### Change widget and deleting the previous:
```
def __init__(self):
	self.current_widget = start_widget
	
	def change(self, widget):
		layout = self.main_window.navigationLayout.layout()
		
		if self.current_widget:
			self.current_widget.setParent(None)
			self.current_widget.deleteLater()
		
		layout.addWidget(widget)
		self.current_widget = widget
```
Данный скрипт предназначен для смена окна внутри layout с удалением предыдущего окна