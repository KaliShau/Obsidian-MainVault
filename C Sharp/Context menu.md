
___
```
DataTable user;
private string _selectedRequestId;

public AllRequests(DataTable dt)
{
    InitializeComponent();
    this.user = dt;

    DatabaseManager db = new DatabaseManager();
    dataGridView1.DataSource = db.getRequests();



}

private void DataGridView1_MouseClick(object sender, MouseEventArgs e)
{
    if (e.Button == MouseButtons.Right)
    {
        // Определяем, по какой строке и столбцу был клик
        var hitTest = dataGridView1.HitTest(e.X, e.Y);

        if (hitTest.RowIndex >= 0 && hitTest.ColumnIndex >= 0)
        {
            // Выделяем строку
            dataGridView1.Rows[hitTest.RowIndex].Selected = true;

            // Получаем значение столбца "request_id"
            this._selectedRequestId = dataGridView1.Rows[hitTest.RowIndex].Cells[0].Value?.ToString();

            // Показываем контекстное меню
            contextMenuStrip1.Show(dataGridView1, e.Location);
        }
    }


}

private void CopyToolStripMenuItem_Click(object sender, EventArgs e)
{
    if (!string.IsNullOrEmpty(_selectedRequestId))
    {
        try
        {
            MessageBox.Show($"Запрос с ID: {_selectedRequestId} принят.");
        }
        catch (Exception ex)
        {
            MessageBox.Show($"Ошибка при принятии запроса: {ex.Message}");
        }
    }
    else
    {
        MessageBox.Show("Не выбран request_id.");
    }
}
```