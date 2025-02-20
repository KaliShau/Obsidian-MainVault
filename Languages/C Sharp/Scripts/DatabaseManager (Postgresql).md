
___
##### Code:
```C#
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
		
        public DataTable login(string username, string pass)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            Cmd.CommandText = "SELECT * FROM Users WHERE username = :username AND password = :pass";
            Cmd.Parameters.AddWithValue("username", username);
            Cmd.Parameters.AddWithValue("pass", pass);
			
            NpgsqlDataReader dr = Cmd.ExecuteReader();
            dt.Load(dr);
            return dt;
        }
		
        public DataTable register(string username, string pass, string Name, int departamentId)
        {
            DataTable dt = new DataTable();
            connection();
            Cmd = new NpgsqlCommand();
            Cmd.Connection = Con;
            dt = this.login(username, pass);
			
            if (dt.Rows.Count > 0)
            {
                DataTable error = new DataTable();
                return error;
            }
			
            Cmd.CommandText = "INSERT INTO Users (FIO,username,password,departmentId) VALUES(:name,:username,:pass, :departamentId);";
            Cmd.Parameters.AddWithValue("name", Name);
            Cmd.Parameters.AddWithValue("username", username);
            Cmd.Parameters.AddWithValue("pass", pass);
            Cmd.Parameters.AddWithValue("departamentId", departamentId);
            Cmd.ExecuteReader();
			
            dt = this.login(username, pass);
			
            return dt;
        }
        
    }
}
```
##### Connection:
```C#
public void connection()
{
	Con = new NpgsqlConnection();
	Con.ConnectionString = StrConnection;
	
	if (Con.State == System.Data.ConnectionState.Closed)
	{
		Con.Open();
	}
}
```
##### SQL Request:
```C#
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
```