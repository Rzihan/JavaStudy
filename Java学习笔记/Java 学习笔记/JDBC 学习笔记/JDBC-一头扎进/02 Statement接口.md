
## 第一节：Statement 接口引入
&ensp;&ensp;作用：用于执行静态 SQL 语句并返回它所生成结果的对象。

&ensp;&ensp;int executeUpdate(String sql) 执行给定 SQL 语句，该语句可能为 INSERT、UPDATE 或 DELETE 语句，或者不返回任何内容的 SQL 语句（如 SQL DDL 语句）。

&ensp;&ensp;void close() 立即释放此 Statement 对象的数据库和 JDBC资源，而不是等待该对象自动关闭时发生此操作。
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class DbUtil {
	private static String dbUrl = "jdbc:mysql://localhost:3306/test2?useUnicode=true&characterEncoding=UTF-8";
	private static String dbUserName = "root";
	private static String dbPassword = "123456";
	private static String jdbcName = "com.mysql.jdbc.Driver";
	
	/**
	 * 获取连接
	 * @return
	 * @throws ClassNotFoundException
	 * @throws SQLException
	 */
	public Connection getCon() throws ClassNotFoundException, SQLException {
		Class.forName(jdbcName);
		Connection con = DriverManager.getConnection(dbUrl, dbUserName, dbPassword);
		return con;
	}
	
	/**
	 * 关闭流
	 * @param stmt
	 * @param con
	 * @throws SQLException
	 */
	public void close(Statement stmt,Connection con) throws SQLException {
		if(stmt != null) {
			stmt.close();
			if(con != null) {
				con.close();
			}
		}
	}
	
}
```

## 第二节：使用 Statement 接口实现添加数据操作
```
/**
	 * 添加图书
	 * @throws SQLException 
	 * @throws ClassNotFoundException 
	 */
	private static int addBook(Book book) throws ClassNotFoundException, SQLException {
		//获取连接
		Connection con = dbUtil.getCon();
		//创建Statement
		Statement stmt = con.createStatement();
		String sql = "INSERT INTO book(id,book_name,price,author,book_type_id) VALUES(" 
					+ book.getId() + ",'" + book.getBookName() + "'," + book.getPrice() + ",'"
					+ book.getAuthor() + "'," + book.getBookTypeId() +  ")";
		System.out.println(sql);
		int result = stmt.executeUpdate(sql);
		return result;
		
	}
```

## 第三节：使用 Statement 接口实现更新数据操作
```
private static int updateBook(Book book) throws ClassNotFoundException, SQLException {
		//获取连接
		Connection con = dbUtil.getCon();
		String sql = "UPDATE book SET book_name = '" +  book.getBookName()
					+ "',price = " +  book.getPrice() + ",author = '" + book.getAuthor()
					+ "',book_type_id = " + book.getBookTypeId() + " WHERE id = " 
					+ book.getId();	
		//创建Statement
		Statement stmt = con.createStatement();
		int result = stmt.executeUpdate(sql);
		//关闭Statement和连接
		dbUtil.close(stmt, con);
		return result;
	}
```

## 第四节：使用 Statement 接口实现删除数据操作
```
private static int deleteBook(int id) throws ClassNotFoundException, SQLException {
		//获取连接
		Connection con = dbUtil.getCon();
		String sql = "delete from book where id = " + id;
		//创建Statement
		Statement stmt = con.createStatement();
		int result = stmt.executeUpdate(sql);
		dbUtil.close(stmt, con);
		return result;
	}
```