# JavaServer Pages Standard Tag Library (JSTL)

JSTL is a collection of custom tags that encapsulate common functionality in JSPs. Using JSTL is highly recommended as it helps to eliminate Java code (scriptlets) from your JSPs, leading to cleaner and more maintainable code.

To use JSTL, you need to include the JSTL dependency in your project. For Maven, you can add the following to your `pom.xml`:

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
```

## JSTL Libraries

JSTL is divided into several libraries, each with a specific purpose.

### Core Tags

The core tags are the most commonly used JSTL tags. They provide functionality for iteration, conditional logic, and variable manipulation.

**Taglib directive:** `<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>`

*   **`<c:out>`:** Displays the value of an expression, escaping XML special characters by default.
    ```jsp
    <c:out value="${user.name}" default="Guest" />
    ```
*   **`<c:set>`:** Sets a variable in a specified scope (page, request, session, or application).
    ```jsp
    <c:set var="isAdmin" value="${user.role == 'admin'}" scope="session" />
    ```
*   **`<c:if>`:** Executes its body if a condition is true.
    ```jsp
    <c:if test="${isAdmin}">
        <p>Welcome, admin!</p>
    </c:if>
    ```
*   **`<c:choose>`, `<c:when>`, `<c:otherwise>`:** A switch-like statement.
    ```jsp
    <c:choose>
        <c:when test="${user.role == 'admin'}">
            <p>Admin dashboard</p>
        </c:when>
        <c:when test="${user.role == 'user'}">
            <p>User profile</p>
        </c:when>
        <c:otherwise>
            <p>Guest area</p>
        </c:otherwise>
    </c:choose>
    ```
*   **`<c:forEach>`:** Iterates over a collection.
    ```jsp
    <c:forEach var="product" items="${products}">
        <p>${product.name}: $${product.price}</p>
    </c:forEach>
    ```

### Formatting Tags

The formatting tags are used to format and parse numbers, dates, and times.

**Taglib directive:** `<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>`

*   **`<fmt:formatNumber>`:** Formats a number.
    ```jsp
    <fmt:formatNumber value="${product.price}" type="currency" />
    ```
*   **`<fmt:formatDate>`:** Formats a date and/or time.
    ```jsp
    <fmt:formatDate value="${order.date}" pattern="yyyy-MM-dd HH:mm" />
    ```

### SQL Tags

The SQL tags are used to interact with a database. **Note:** It is generally not recommended to use the SQL tags in production applications, as it mixes business logic with the view layer. It is better to use a DAO or a service layer to handle database operations.

**Taglib directive:** `<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql" %>`

### XML Tags

The XML tags are used to work with XML data.

**Taglib directive:** `<%@ taglib uri="http://java.sun.com/jsp/jstl/xml" prefix="x" %>`

## Expression Language (EL)

JSTL tags rely heavily on Expression Language (EL) to access data. EL provides a simple and convenient way to access data stored in JavaBeans, maps, arrays, and lists.

EL expressions are enclosed in `${...}`.

### Key Features of EL

*   **Accessing JavaBeans:** `${user.name}` is equivalent to `user.getName()`.
*   **Accessing Map Values:** `${myMap['key']}` or `${myMap.key}`.
*   **Accessing List/Array Elements:** `${myList[0]}`.
*   **Implicit Objects:** EL provides several implicit objects, including `pageScope`, `requestScope`, `sessionScope`, `applicationScope`, `param`, `header`, and `cookie`.
*   **Operators:** EL supports arithmetic, logical, and relational operators.
    ```jsp
    ${(price * 1.05) + shippingCost}
    ${user.isAdmin && !user.isGuest}
    ```