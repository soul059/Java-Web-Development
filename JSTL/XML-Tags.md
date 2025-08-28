# JSTL XML Tags

The JSTL (JSP Standard Tag Library) XML tags are used to create and manipulate XML documents within JSP pages. These tags utilize XPath expressions to select and process parts of an XML document.

To use the JSTL XML library, you need to include the following directive at the top of your JSP page:

```jsp
<%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %>
```

Here are the main JSTL XML tags and their functions:

### Core XML Tags:

*   **`<x:parse>`**: This tag parses XML data from a string, a URL, or the tag's body and stores the result in a scoped variable.
*   **`<x:out>`**: Similar to the `<c:out>` tag in the core library, this tag evaluates an XPath expression and outputs the result to the page.
*   **`<x:set>`**: This tag evaluates an XPath expression and sets the result to a scoped variable.

### Flow Control Tags:

*   **`<x:if>`**: This tag evaluates an XPath expression as a boolean. If the result is true, the body content of the tag is processed.
*   **`<x:forEach>`**: This tag iterates over a collection of nodes selected by an XPath expression.
*   **`<x:choose>`, `<x:when>`, `<x:otherwise>`**: These tags work together to provide conditional logic, similar to a switch statement. `<x:when>` evaluates an XPath expression, and if it's true, its body is processed. If no `<x:when>` condition is met, the `<x:otherwise>` block is executed.

### Transformation Tags:

*   **`<x:transform>`**: This tag applies an XSLT (Extensible Stylesheet Language Transformations) stylesheet to an XML document.
*   **`<x:param>`**: Used within the `<x:transform>` tag, this tag sets a parameter in the XSLT stylesheet.
