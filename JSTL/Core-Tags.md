# JSTL Core Tags

The JSTL (JSP Standard Tag Library) core tags are a collection of tags that provide fundamental functionality to simplify the development of JSP (JavaServer Pages). They help in avoiding Java scriptlets in JSP pages, leading to cleaner and more maintainable code. These tags are used for tasks such as variable manipulation, flow control, and URL management.

To use the JSTL core tags in a JSP page, you must include the following directive at the top of the file:

```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
```

Here is a list of some of the most commonly used JSTL core tags with their descriptions:

### Variable and Scope Management

*   **`<c:set>`**: Sets the value of a variable in a specified scope (page, request, session, or application).
*   **`<c:remove>`**: Removes a variable from a specified scope.

### Flow Control

*   **`<c:if>`**: A simple conditional tag that processes its body content only if the supplied condition is true.
*   **`<c:choose>`, `<c:when>`, `<c:otherwise>`**: These tags work together to create a block of mutually exclusive conditional statements, similar to a `switch` statement in Java. `<c:choose>` is the parent tag, `<c:when>` represents a condition to test, and `<c:otherwise>` is the default case if no `<c:when>` condition is met.
*   **`<c:forEach>`**: Iterates over a collection of items, such as an array, list, or map.
*   **`<c:forTokens>`**: Iterates over tokens separated by a specified delimiter in a string.

### Output and URL Management

*   **`<c:out>`**: Displays the value of an expression, similar to a JSP expression tag (`<%= ... %>`), but with the added feature of escaping XML/HTML characters by default.
*   **`<c:url>`**: Creates a URL, automatically rewriting it to include the session ID if needed.
*   **`<c:redirect>`**: Redirects the response to a new URL.
*   **`<c:param>`**: Adds a parameter to a containing `<c:url>`, `<c:redirect>`, or `<c:import>` tag.

### Other Tags

*   **`<c:import>`**: Retrieves an absolute or relative URL and exposes its content to the page.
*   **`<c:catch>`**: Catches any `Throwable` exception that occurs in its body and optionally exposes it as a variable.

### Example Usage:

Here is a simple example demonstrating the use of a few JSTL core tags:

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<head>
    <title>JSTL Core Tags Example</title>
</head>
<body>

    <%-- Using <c:set> to create a variable --%>
    <c:set var="greeting" value="Hello, World!" scope="request" />

    <%-- Using <c:out> to display the variable's value --%>
    <h1><c:out value="${greeting}" /></h1>

    <%-- Using <c:if> for conditional logic --%>
    <c:set var="userRole" value="admin" />
    <c:if test="${userRole == 'admin'}">
        <p>Welcome, Administrator!</p>
    </c:if>

    <%-- Using <c:choose>, <c:when>, and <c:otherwise> --%>
    <c:set var="dayOfWeek" value="5" />
    <c:choose>
        <c:when test="${dayOfWeek >= 1 && dayOfWeek <= 5}">
            <p>It's a weekday.</p>
        </c:when>
        <c:otherwise>
            <p>It's the weekend!</p>
        </c:otherwise>
    </c:choose>

    <%-- Using <c:forEach> to loop through a list of items --%>
    <%
        java.util.ArrayList<String> names = new java.util.ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");
        request.setAttribute("userNames", names);
    %>
    <h2>User List:</h2>
    <ul>
        <c:forEach var="name" items="${userNames}">
            <li><c:out value="${name}" /></li>
        </c:forEach>
    </ul>

</body>
</html>
```
