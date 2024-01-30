![psycopg2](../assets/icons/psycopg.png){: width="25%"}

**psycopg2-binary** and **psycopg2** are both Python database adapters for PostgreSQL, and they serve the same primary purpose of enabling Python applications to interact with PostgreSQL databases. However, there are some differences between the two:

1. **psycopg2-binary:**
    - **psycopg2-binary** is a pre-built binary distribution of the **psycopg2**2 library, including the C extensions necessary for PostgreSQL database connections.
    - It is convenient to use because you don't need to compile anything during installation. You can install it with a simple pip command.
    - It bundles the necessary PostgreSQL client library, so you don't need to separately install PostgreSQL or its development headers.
2. **psycopg2:**
    - **psycopg2** is the original PostgreSQL adapter for Python.
    - It is not a pre-built binary, so it requires compilation during installation, which might involve installing PostgreSQL development headers and libraries.
    - Some users prefer using **psycopg2** in production environments for better control over the PostgreSQL client library versions and customization options.  

Choosing between **psycopg2-binary** and **psycopg2** depends on your specific use case:

- For development and ease of use, especially in environments like development or testing, **psycopg2-binary** is a convenient choice as it simplifies installation and doesn't require additional dependencies.
- For production environments where you need precise control over library versions and have specific configuration requirements, you might opt for **psycopg2** to have more control over the compilation process and library compatibility.

Ultimately, the choice between the two often comes down to your project's specific needs and deployment requirements. Both libraries provide robust PostgreSQL connectivity for Python, so you can choose the one that best suits your use case.