```java
package com.pzh.servlet;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashSet;
import java.util.Random;
import java.util.Set;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class DoubleColorBallServlet
 */
@WebServlet("/DoubleColorBallServlet")
public class DoubleColorBallServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public DoubleColorBallServlet() {
        
    }

	
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		Set<Integer> set = new HashSet<Integer>();
		Random random = new Random();
		while(set.size() != 6) {
			int randomValue = random.nextInt(33) + 1;
			set.add(randomValue);
		}
		String result = "red ball:";
		for(Integer i : set) {
			result += i + " ";
		}
		int randomValue = random.nextInt(16) + 1;
		result +="<br>blue ball:" + randomValue;
		PrintWriter out  = response.getWriter();
		out.println("<html><head><title>Result</title></head>");
		out.println("<body><h1>" + result + "</h1></body></html>");
	}

	
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		this.doGet(request, response);
	}

}
```
