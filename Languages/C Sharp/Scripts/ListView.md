
___
### 1. Настройка ListView

Сначала добавьте `ListView` на форму и настройте его:
```C#
// В методе InitializeComponent() или конструкторе формы:
listView1.View = View.Details;
listView1.FullRowSelect = true;
listView1.GridLines = true; // опционально - показывать линии сетки

// Добавляем колонки
listView1.Columns.Add("ID", 50);
listView1.Columns.Add("Дата создания", 120);
listView1.Columns.Add("Заголовок", 200);
listView1.Columns.Add("Статус", 100);
listView1.Columns.Add("Приоритет", 100);
listView1.Columns.Add("Назначено", 150);
```
### 2. Метод для заполнения ListView
```C#
public void DisplayTickets(List<TicketWithJoinDTO> tickets)
{
    listView1.Items.Clear();
    
    foreach (var ticket in tickets)
    {
        var item = new ListViewItem(ticket.ID.ToString());
        
        item.SubItems.Add(ticket.created_at.ToString("dd.MM.yyyy HH:mm"));
        item.SubItems.Add(ticket.title);
        item.SubItems.Add(ticket.status_name);
        item.SubItems.Add(ticket.priority_name);
        item.SubItems.Add(ticket.assigned_user_name ?? "Не назначено");
        
        // Можно сохранить весь объект в Tag для доступа к полным данным
        item.Tag = ticket;
        
        listView1.Items.Add(item);
    }
    
    // Автоподбор ширины колонок (опционально)
    listView1.AutoResizeColumns(ColumnHeaderAutoResizeStyle.ColumnContent);
}
```
### 3. Пример использования
```C#
// Где-то в коде формы (например, при загрузке или по кнопке):
var tickets = ticketService.GetTicketsByClientId(clientId).ToList();
DisplayTickets(tickets);
```
### 4. Дополнительные возможности:
**Сортировка по колонкам:**
```C#
private void listView1_ColumnClick(object sender, ColumnClickEventArgs e)
{
    var listView = (ListView)sender;
    listView.ListViewItemSorter = new ListViewItemComparer(e.Column);
    listView.Sort();
}

// Класс для сортировки
public class ListViewItemComparer : IComparer
{
    private readonly int col;
    public ListViewItemComparer(int column) { col = column; }
    
    public int Compare(object x, object y)
    {
        return string.Compare(
            ((ListViewItem)x).SubItems[col].Text,
            ((ListViewItem)y).SubItems[col].Text);
    }
}
```
**Обработка двойного клика:**
```C#
private void listView1_DoubleClick(object sender, EventArgs e)
{
    if (listView1.SelectedItems.Count > 0)
    {
        var selectedTicket = (TicketWithJoinDTO)listView1.SelectedItems[0].Tag;
        // Открываем форму редактирования или показываем детали
        ShowTicketDetails(selectedTicket);
    }
}
```
### Контекстное меню:
```C#
private void CommentsList_MouseClick(object sender, MouseEventArgs e)
{
    if (e.Button == MouseButtons.Right)
    {
        ListViewHitTestInfo hitTest = CommentsList.HitTest(e.Location);

        if (hitTest.Item != null)
        {
            hitTest.Item.Selected = true;

            _selectedCommentId = Convert.ToInt16(hitTest.Item.SubItems[0].Text);

            contextMenuStrip1.Show(CommentsList, e.Location);
        }
    }
}
```