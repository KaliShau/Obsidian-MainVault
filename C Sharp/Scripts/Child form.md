
___
##### Child form add in panel:
```C#
Form child = new Materials();
child.Dock = DockStyle.Fill;
child.TopLevel = false;
child.FormBorderStyle = FormBorderStyle.None;
panel3.Controls.Clear();
panel3.Controls.Add(child);
child.Show();
```