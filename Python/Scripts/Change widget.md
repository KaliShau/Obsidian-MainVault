
___
#### Change widget:
```Python
def change(self, widget):
	layout = self.main_window.navigationLayout.layout()
	layout.itemAt(0).widget().setParent(None)
	layout.addWidget(widget)
```
#### Change widget and deleting the previous:
```Python
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
