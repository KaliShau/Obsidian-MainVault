
___
```
public partial class MainForm : Form
{
    public MainForm()
    {
        InitializeComponent();

        // Привязываем контекстное меню к DataGridView
        dataGridView1.ContextMenuStrip = contextMenuStrip1;

        // Подписываемся на событие клика правой кнопкой мыши
        dataGridView1.MouseClick += DataGridView1_MouseClick;

        // Подписываемся на событие клика по кнопке в контекстном меню
        copyToolStripMenuItem.Click += CopyToolStripMenuItem_Click;
    }

    private void DataGridView1_MouseClick(object sender, MouseEventArgs e)
    {
        // Проверяем, что клик был правой кнопкой мыши
        if (e.Button == MouseButtons.Right)
        {
            // Получаем строку, по которой был клик
            var hitTest = dataGridView1.HitTest(e.X, e.Y);

            if (hitTest.RowIndex >= 0) // Если клик был по строке
            {
                // Выделяем строку
                dataGridView1.Rows[hitTest.RowIndex].Selected = true;

                // Показываем контекстное меню
                contextMenuStrip1.Show(dataGridView1, e.Location);
            }
        }
    }

    private void CopyToolStripMenuItem_Click(object sender, EventArgs e)
    {
		if (dataGridView1.SelectedRows.Count > 0)
		{
		    var selectedRow = dataGridView1.SelectedRows[0];
		
		    // Получаем значение столбца "request_id"
		    var requestId = selectedRow.Cells["request_id"].Value?.ToString();
		
		    if (!string.IsNullOrEmpty(requestId))
		    {
		        MessageBox.Show($"Скопировано request_id: {requestId}");
		    }
		    else
		    {
		        MessageBox.Show("Значение request_id отсутствует.");
		    }
		}
		else
		{
		    MessageBox.Show("Строка не выбрана.");
		}
	}
}
```