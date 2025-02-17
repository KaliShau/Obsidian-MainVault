
___
```
using Npgsql; // Подключаем библиотеку
using System;
using System.Collections.Generic;
using System.Data;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PRMS
{
    public class DB
    {


        string StrConnection = "Server=localhost; port=5432; User Id=postgres ;Password=postgres;database=prms;"; // Строка подключения
        NpgsqlConnection Con;
        NpgsqlCommand Cmd;


        public void connection()
        {
            Con = new NpgsqlConnection();
            Con.ConnectionString = StrConnection;

            if (Con.State == System.Data.ConnectionState.Closed)
            {
                Con.Open();
            }
        }


        public DataTable login(string Login, string Pass)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            Cmd.CommandText = "SELECT * FROM \"User\" WHERE email = :login AND password = :pass";
            Cmd.Parameters.AddWithValue("login", Login);
            Cmd.Parameters.AddWithValue("pass", Pass);

            NpgsqlDataReader dr = Cmd.ExecuteReader();
            dt.Load(dr);
            return dt;
        }


        public DataTable register(string Login, string pass, string Name, int departamentId)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            dt = this.login(Login, pass);

            if (dt.Rows.Count > 0)
            {
                DataTable error = new DataTable();
                return error;
            }

            Cmd.CommandText = "INSERT INTO \"User\"(\"FIO\",email,password,\"departmentId\") VALUES(:name,:login,:pass, :departamentId);";
            Cmd.Parameters.AddWithValue("name", Name);
            Cmd.Parameters.AddWithValue("login", Login);
            Cmd.Parameters.AddWithValue("pass", pass);
            Cmd.Parameters.AddWithValue("departamentId", departamentId);
            Cmd.ExecuteReader();


            dt = this.login(Login, pass);

            return dt;
        }

        public DataTable getSearchPatient(string keyword)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            Cmd.CommandText = "SELECT id as ID, created_at as \"Дата записи\", \"FIO\" as ФИО, record_type as \"Тип записи\", address as Адрес, content as Содержимое, \"userId\" as \"ID Врача\" FROM \"Patient\" \r\nWHERE CONCAT_WS(\"FIO\", record_type, address) LIKE :keyword";
            Cmd.Parameters.AddWithValue("keyword", '%' + keyword + '%');

            NpgsqlDataReader dr = Cmd.ExecuteReader();
            dt.Load(dr);
            return dt;
        }

        public DataTable getDepartamenthPatient(int departamentId)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            Cmd.CommandText = "SELECT id as ID, created_at as \"Дата записи\", \"FIO\" as ФИО, record_type as \"Тип записи\", address as Адрес, content as Содержимое, \"userId\" as \"ID Врача\" FROM \"Patient\" \r\nWHERE \"departmentId\" = :departamentId ";
            Cmd.Parameters.AddWithValue("departamentId", departamentId);

            NpgsqlDataReader dr = Cmd.ExecuteReader();
            dt.Load(dr);
            return dt;
        }
    }
}
```