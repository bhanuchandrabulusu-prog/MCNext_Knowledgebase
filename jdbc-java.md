# Use JDBC with Java | Get Started with Data 360 JDBC | Data 360 Query Guide

**Source:** https://developer.salesforce.com/docs/data/data-cloud-query-guide/guide/jdbc-java.html

---

Note: External Client Apps support the JWT Bearer Flow for JDBC connections. Username-Password Flow and Refresh Token Flow are not supported with External Client Apps.

The Data 360 JDBC driver JAR file is available in the global Maven package registry at https://central.sonatype.com/artifact/com.salesforce.datacloud/jdbc.

Maven is a popular build automation tool that’s used primarily for Java projects. It helps manage dependencies, builds, and reporting. To include the JDBC driver in your Maven project, add this dependency to your pom.xml file.

The fully qualified class name for the driver is com.salesforce.datacloud.jdbc.DataCloudJDBCDriver.

If you cloned the JDBC driver repository, you can build and test the driver locally by using this Maven command.

To establish a connection, the driver requires a connection URL and authentication properties, as detailed in the Driver URL and Properties section. Here’s the general structure for establishing a connection by using the JDBC driver.

Here is an example for JWT Bearer Flow authentication with External Client Apps.

For property descriptions, see Required Properties for JWT Bearer Flow.

Note: The clientSecret (Consumer Secret) is not required for JWT Bearer Flow authentication with External Client Apps.

This section provides a concise Java example that demonstrates how to establish a connection, execute a query, process the results, and release resources. The example uses a PreparedStatement to execute a parameterized query, which helps prevent SQL injection vulnerabilities and can improve performance.

Before running this example:

Ensure that you have Java 8 or later installed on your system.
Add the Data 360 JDBC driver and the SLF4j library (for logging) to your project’s classpath. If you’re using Maven, include the appropriate dependencies in your pom.xml file. If you’re not using a build tool, manually download the JAR files for the JDBC driver and SLF4j, and add them to your project’s classpath.

The example code demonstrates these steps:

Establish a Connection: The createConnection() method establishes a connection to Data 360 by using the DriverManager.getConnection() method along with JWT Bearer Flow authentication credentials. Make sure you replace the placeholder values with your actual username, client ID, and private key.

Prepare the SQL Statement: The connection.prepareStatement() method creates a PreparedStatement object. The SQL query in this example uses placeholders (?) to represent values that will be dynamically inserted later. This technique, known as parameterized querying, is crucial for preventing SQL injection vulnerabilities and can improve query performance.

Set Parameter Values: The code sets the values for the placeholders in the prepared statement.

statement.setString(1, "Angella") sets the first placeholder (index 1) to the string value “Angella.”
statement.setInt(2, 1000) sets the second placeholder (index 2) to the integer value 1000. The JDBC driver provides various methods, such as setString, setInt, and setDate, to set parameter values based on their data types.

Execute the Query: The statement.executeQuery() method executes the parameterized query. Because the parameter values have already been set, there’s no need to pass any additional values here.

Process the Result Set: The code uses a while loop to iterate through the ResultSet obtained from the query execution. The resultSet.next() method moves the cursor to the next row in the result set, and the code within the loop retrieves and logs the data for each row.

Close Resources: It’s important to close the ResultSet and the PreparedStatement to release any database resources that are held by these objects.

Execute the Java Application: After you set up your project and complete the code, compile and run your Java application to execute the example.

You can now query and interact with your Data 360 data through your Java application. See the Get Started with Data 360 SQL guide.
