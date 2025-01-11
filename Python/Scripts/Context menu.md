
___
##### Create context menu example:
```
def __init__:
	tableView.setContextMenuPolicy(Qt.ContextMenuPolicy.CustomContextMenu)
	tableView.customContextMenuRequested.connect(self.showContextMenu)

def showContextMenu(self, position: QPoint):
	menu = QMenu(self.my_create_tickets.tableView)
	
	delete_action = menu.addAction('Удалить')
	
	index = self.my_create_tickets.tableView.indexAt(position)
	
	if index.isValid():
		model = self.my_create_tickets.tableView.model()
		row = index.row()
		id_item = model.item(row, 0)
		
		if id_item:
			ticket_id = int(id_item.text())
			action = menu.exec(self.my_create_tickets.tableView.viewport().mapToGlobal(position))
			
			if action == delete_action:
				print('delete', ticket_id)
```