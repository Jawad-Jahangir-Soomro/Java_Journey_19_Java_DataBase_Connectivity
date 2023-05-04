# Java Journey, 19: Java DataBase Connectivity.

Repository 19 covers the topic of Java Database Connectivity (JDBC), which is a Java API that allows Java programs to interact with databases. JDBC provides a set of classes and interfaces to enable the development of database applications in Java. 

## Learn about JDBC and how to connect to a database in Java.

JDBC (Java Database Connectivity) is an API for connecting to and executing SQL queries on a database in Java. To use JDBC, one needs to first establish a connection to a database using a JDBC driver, which is a library that enables the connection to the specific database.

Here's an example code to connect to a database using JDBC:

```bash
import java.sql.*;

public class JdbcExample {
  public static void main(String[] args) {
    try {
      // Load the JDBC driver
      Class.forName("com.mysql.jdbc.Driver");

      // Establish a connection to the database
      String url = "jdbc:mysql://localhost:3306/mydatabase";
      String username = "myusername";
      String password = "mypassword";
      Connection conn = DriverManager.getConnection(url, username, password);

      // Execute a SQL query
      Statement stmt = conn.createStatement();
      ResultSet rs = stmt.executeQuery("SELECT * FROM mytable");

      // Iterate over the results and print them out
      while (rs.next()) {
        System.out.println(rs.getString("column1") + " " + rs.getString("column2"));
      }

      // Close the connection and resources
      rs.close();
      stmt.close();
      conn.close();
    } catch (Exception e) {
      System.err.println("Error: " + e.getMessage());
    }
  }
}
```

In this example, we first load the JDBC driver for MySQL, establish a connection to a database named "mydatabase" running on localhost with the given username and password, execute a SQL query to select all rows from a table named "mytable", and finally print out the results.

JDBC supports various types of statements such as SELECT, INSERT, UPDATE, and DELETE. It also supports prepared statements, which are precompiled SQL statements that can be executed multiple times with different parameters, improving performance and security.

## Study the use of JDBC drivers, such as MySQL Connector/J, for connecting to different database management systems.

JDBC (Java Database Connectivity) is an API that provides a standard way of connecting to relational databases from a Java application. To connect to a database using JDBC, we need a JDBC driver that allows the Java application to communicate with the database. There are different types of JDBC drivers available, such as Type 1, Type 2, Type 3, and Type 4 drivers.

For example, to connect to a MySQL database using JDBC, we can use the MySQL Connector/J driver. First, we need to download the driver JAR file from the MySQL website and add it to the classpath of our Java application. Then, we can establish a connection to the database using the DriverManager class as follows:

```bash
import java.sql.*;

public class JdbcExample {
  public static void main(String[] args) {
    try {
      // Load the MySQL Connector/J driver
      Class.forName("com.mysql.cj.jdbc.Driver");
      
      // Create a connection to the MySQL database
      Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/mydatabase", "username", "password");
      
      // Execute a SQL query on the database
      Statement stmt = conn.createStatement();
      ResultSet rs = stmt.executeQuery("SELECT * FROM mytable");
      
      // Process the results of the query
      while (rs.next()) {
        String name = rs.getString("name");
        int age = rs.getInt("age");
        System.out.println("Name: " + name + ", Age: " + age);
      }
      
      // Close the connection
      conn.close();
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

In this example, we first load the MySQL Connector/J driver using the Class.forName() method. Then, we create a connection to the database using the DriverManager.getConnection() method, which takes three arguments: the URL of the database, the username, and the password. We then execute a SQL query on the database using the Statement.executeQuery() method, and process the results using a ResultSet object. Finally, we close the connection using the Connection.close() method.

## Learn about the use of PreparedStatement for executing SQL statements.

In Java, the PreparedStatement interface is used to execute parameterized SQL queries. It is a subinterface of the Statement interface and allows us to write parameterized SQL statements that prevent SQL injection attacks.

Here is an example of using PreparedStatement to execute an SQL statement in Java:

```bash
String name = "John";
int age = 30;
PreparedStatement ps = connection.prepareStatement("INSERT INTO users (name, age) VALUES (?, ?)");
ps.setString(1, name);
ps.setInt(2, age);
int rowsInserted = ps.executeUpdate();
```

In this example, we are inserting a new user into the "users" table with a name of "John" and an age of 30. The question marks in the SQL statement represent placeholders for the actual values. We then use the setString and setInt methods of the PreparedStatement object to set the actual values for the placeholders. Finally, we execute the SQL statement using the executeUpdate method, which returns the number of rows affected by the statement.

Using PreparedStatement is preferred over Statement as it provides better performance and security. Additionally, it allows for better reuse of SQL statements with different parameter values, resulting in more maintainable code.

## Study the use of ResultSet for retrieving and manipulating data from a database.

ResultSet is an interface in the Java Database Connectivity (JDBC) API that provides methods for retrieving and manipulating data from a database. It is used to fetch records from the database after executing a SELECT statement.

To use ResultSet, we first need to establish a connection to the database using JDBC. Once the connection is established, we can execute SQL statements on the database using a Statement object. After executing the statement, we get a ResultSet object that contains the data retrieved from the database.

Here's an example code snippet that demonstrates the use of ResultSet to retrieve data from a database:

```bash
import java.sql.*;

public class RetrieveDataExample {
    public static void main(String[] args) throws SQLException {
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/mydatabase", "root", "password");
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM employees");

        while (rs.next()) {
            int id = rs.getInt("id");
            String name = rs.getString("name");
            String email = rs.getString("email");
            System.out.println(id + " " + name + " " + email);
        }

        rs.close();
        stmt.close();
        conn.close();
    }
}
```

In the example above, we first establish a connection to the database using the DriverManager.getConnection() method. We then create a Statement object using the Connection.createStatement() method and execute a SELECT statement to retrieve data from the employees table. The executeQuery() method of the Statement object returns a ResultSet object that contains the retrieved data.

We use the next() method of the ResultSet object to move the cursor to the next row of the result set. We can then use the getInt(), getString(), and other getter methods of the ResultSet object to retrieve the values of the columns in the current row. The getInt() method is used to retrieve the value of the id column, and the getString() method is used to retrieve the values of the name and email columns.

Finally, we close the ResultSet, Statement, and Connection objects to release the database resources.
