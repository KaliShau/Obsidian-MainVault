
___
```
        DataTable user;
        DataTable statuses;
        
        public CreateReques(DataTable dt)
        {
            InitializeComponent();
            user = dt;

            DatabaseManager db = new DatabaseManager();
            DataTable dataTable = new DataTable();
            this.statuses = db.getStatuses();


            comboBox1.DataSource = this.statuses;
            comboBox1.DisplayMember = "status_name";
            comboBox1.ValueMember = "status_id";

        }

        private void button1_Click(object sender, EventArgs e)
        {
            MessageBox.Show(Convert.ToString(comboBox1.SelectedValue));
        }
```