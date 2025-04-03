
___
### Репозиторий БД для удобного создания запросов: 
```C#
using System;
using System.Collections.Generic;
using System.Data.SqlClient;

namespace CSWT.src.core.database
{
    public class DatabaseRepository
{
    private readonly string _connectionString = "Server=localhost; User Id=postgres ;Password=root;database=cswt;";

    public DatabaseRepository(string connectionString)
    {
    }

    public List<T> Query<T>(
        string sql,
        Func<NpgsqlDataReader, T> mapper,
        params NpgsqlParameter[] parameters)
    {
        using (var connection = new NpgsqlConnection(_connectionString))
        using (var command = new NpgsqlCommand(sql, connection))
        {
            command.Parameters.AddRange(parameters);
            connection.Open();

            var results = new List<T>();
            using (var reader = command.ExecuteReader())
            {
                while (reader.Read())
                    results.Add(mapper(reader));
            }

            return results;
        }
    }

    public int Execute(string sql, params NpgsqlParameter[] parameters)
    {
        using (var connection = new NpgsqlConnection(_connectionString))
        using (var command = new NpgsqlCommand(sql, connection))
        {
            command.Parameters.AddRange(parameters);
            connection.Open();
            return command.ExecuteNonQuery();
        }
    }
}
}
```
### Для удобства можно добавить в DI
```C#
services.AddSingleton<DatabaseRepository>()
```

```C#
private bool UserExists(string username)
{
    const string sql = "SELECT COUNT(1) FROM Users WHERE username = @username";

    var count = _repository.Query<int>(
        sql,
        reader => reader.GetInt32(0),
        new NpgsqlParameter("@username", username)
    ).FirstOrDefault();

    return count > 0;
}
```