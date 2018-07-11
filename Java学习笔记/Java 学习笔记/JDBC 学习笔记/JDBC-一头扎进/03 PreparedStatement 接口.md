## 第一节：PreparedStatement 接口引入

&ensp;&ensp; PreparedStatement 是 Statement 的子接口，属于预处理操作，与直接使用 Statement 不同的是，PreparedStatement
在操作时，是先在数据表中准备好了一条 SQL 语句，但是此 SQL 语句的具体内容暂时不设置，而是之后再进
行设置。

&ensp;&ensp;（以后开发一般用 PreparedStatement，不用 Statement）

## 第二节：使用 PreparedStatement 接口实现添加数据操作
```
    
    /**
	 * 添加图书
	 * @param book
	 * @return
	 * @throws ClassNotFoundException
	 * @throws SQLException
	 */
	private static int addBook(Book book) throws ClassNotFoundException, SQLException {
        	//获取连接
		Connection con = dbUtil.getCon();
		String sql = "INSERT INTO book(book_name,price,author,book_type_id) VALUES(?,?,?,?)";
		//创建PreparedStatement
		PreparedStatement pstmt = con.prepareStatement(sql);
		pstmt.setString(1, book.getBookName());
		pstmt.setFloat(2, book.getPrice());
		pstmt.setString(3, book.getAuthor());
		pstmt.setInt(4, book.getBookTypeId());
		int result = pstmt.executeUpdate();
		dbUtil.close(pstmt, con);
		return result;
	}
```
## 第三节：使用 PreparedStatement 接口实现更新数据操作
```
/**
	 * 更新图书
	 * @param book
	 * @return
	 * @throws ClassNotFoundException
	 * @throws SQLException
	 */
	private static int updateBook(Book book) throws ClassNotFoundException, SQLException {
	        //获取连接
		Connection con = dbUtil.getCon();
		String sql = "UPDATE book SET book_name = ?,price = ?,author = ?,book_type_id = ? WHERE id = ?";
		//创建PreparedStatement
		PreparedStatement pstmt = con.prepareStatement(sql);
		pstmt.setString(1, book.getBookName());
		pstmt.setFloat(2, book.getPrice());
		pstmt.setString(3, book.getAuthor());
		pstmt.setInt(4, book.getBookTypeId());
		pstmt.setInt(5, book.getId());
		int result = pstmt.executeUpdate();
		//关闭流
		dbUtil.close(pstmt, con);
		return result;
	}
```

## 第四节：使用 PreparedStatement 接口实现删除数据操作
```
/**
	 * 删除图书
	 * @param id
	 * @return
	 * @throws ClassNotFoundException
	 * @throws SQLException
	 */
	private static int deleteBook(int id) throws ClassNotFoundException, SQLException {
		Connection con = dbUtil.getCon();//获取连接
		String sql = "DELETE From book WHERE id = ? ";
		PreparedStatement pstmt = con.prepareStatement(sql);//创建PreparedStatement
		pstmt.setInt(1, id);
		int result = pstmt.executeUpdate();
		dbUtil.close(pstmt, con);
		return result;
	}
```