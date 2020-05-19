## web.xml

- reference: Java™ 2 Enterprise Edition (J2EE™) <br>
Web Component Developer Exam Cram™ 2 (Exam 310-080) <br>
[Chapter 2](https://learning.oreilly.com/library/view/javatm-2-enterprise/0789728621/ch02.html)<br>
[Chapter 3](https://learning.oreilly.com/library/view/javatm-2-enterprise/0789728621/ch03.html)

### context-param

```xml
<context-param>
	<param-name>contextConfigLocation</param-name>
	<param-value>
	    /WEB-INF/configs/root-context.xml
	</param-value>
</context-param>
```

The <code>context-param</code> element contains the declaration of a 
> Web application's servlet context-initialization parameters. 

In other words, these are the initialization parameters for the application. 

You can access these parameters in your code using the 

- <code>javax.servlet.ServletContext.getInitParameter()</code> and
- <code>javax.servlet.ServletContext.getInitParameterNames()</code> 

methods. 

The <code>param-name</code> element contains 
> the name (unique in the Web application) of a parameter. 

The <code>param-value</code> element contains 
>the value of a parameter.

### listener

```xml
<listener>
	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```

The <code>listener</code> element indicates 
> the deployment properties for a Web application listener bean. 

The <code>listener-class</code> element declares that 
>a class in the application must be registered as a Web application listener bean. 

The value is the fully qualified class name of the listener class.

### servlet

```xml
<servlet>
	<servlet-name>appServlet</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/configs/servlet-context.xml</param-value>
	</init-param>
	<load-on-startup>1</load-on-startup>
</servlet>		
```

The <code>servlet</code> element declares a servlet. 

This element most likely will be on the exam. 

A <code>servlet-name</code> element contains 
> - the canonical name of the servlet that is unique within the Web application. 
- It is used to reference the servlet definition elsewhere in the deployment descriptor. 
- Use either the <code>servlet-class</code> tags or the <code>jsp-file</code> tags in your servlet body, but not both. 
- If it's <code>jsp-file</code>, use the full path to the <acronym>JSP</acronym> file within the Web application. 
- This path is relative to the Web application root directory. 

The <code>servlet-class</code> element contains 
> the fully qualified class name of the servlet. 

The <code>init-param</code> element contains 
> a name/value pair as an initialization param of the servlet. 

You retrieve these as follows:

```java
PrintWriter writer = response.getWriter();
Enumeration params = getServletConfig().getInitParameterNames();
        
while (params.hasMoreElements()){
    String param = (String) params.nextElement();
    String value = getServletConfig().getInitParameter(param);
    writer.println(param + " = " + value);
}
```

---

The <code>load-on-startup</code> element indicates that <br>
this servlet should be loaded <br>
(should be instantiated and have its <code>init()</code> called) <br>
upon startup of the Web application. 

The optional contents of these elements must be an integer indicating the order in which the servlet should be loaded. 
> - If the value is a negative integer, or if the element is not present, the container is free to load the servlet whenever it chooses. 
- If the value is a positive integer or <code>0</code>, the container must load and initialize the servlet as the application is deployed. 

- The container must guarantee that servlets marked with lower integers are loaded before servlets marked with higher integers. 

- The container may choose the order of loading of servlets with the same <code>load-on-start-up</code> value. 

- The <code>run-as</code> element specifies the identity to be used for the execution of the Web application.

---

The <code>security-role-ref</code> element contains 

the declaration of a security role reference in the Web application's code. 

You use this to link a security role name defined by <code>security-role</code> to a role name that is hard-coded in the servlet. 

The declaration consists of an optional description, the security role name used in the code, and an optional link to a security role.

If the security role is not specified, the deployer must choose an appropriate security role. 

The value of the <code>role-name</code> element must be the string used as the parameter to the <code>HttpServletRequest.isUserInRole(String role)</code> method. 

The <code>role-link</code> element is a reference to a defined security role and must contain the name of one of the security roles defined in the <code>security-role</code> elements.

### servlet-mapping

The <code>servlet-mapping</code> element defines 
> a mapping between a servlet and a URL pattern. 

The <code>servlet-name</code> element contains 
- the canonical name of the servlet that is unique within the Web application. 

The <code>url-pattern</code> element contains 
- the URL pattern of the mapping and must follow the rules specified in Section 11.2 of the Servlet API Specification.

### login-config

### error-page

### security-role

### security-constraint

### session-config

### taglib
