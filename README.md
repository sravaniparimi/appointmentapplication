package com.jnit;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.servlet.ServletConfig;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class PatientLogin extends HttpServlet {
	Connection con=null;
	PreparedStatement ps=null;
    public void init(ServletConfig config) {
    	try {
			Class.forName("com.mysql.jdbc.Driver");
			String url="jdbc:mysql://localhost:3306/jnit";
			String user="root";
			String pass="1234567890";
			con=DriverManager.getConnection(url,user,pass);
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
        }
	
	public void doPost(HttpServletRequest request,HttpServletResponse response) throws IOException {
          String username=request.getParameter("dname");
          String password=request.getParameter("password");
          
           try {
			ps=con.prepareStatement("select * from patient where name=? and password=?");
			ps.setString(1, username);
			ps.setString(2, password);
			ResultSet rs=ps.executeQuery();
		if(rs.next())
			response.sendRedirect("./patient_home.html");
			
			
			
			
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
           
          
          
          
          
          
          
          
          
          
          
          
          
          
          
}
}
