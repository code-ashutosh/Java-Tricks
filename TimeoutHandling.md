### Connect Timeout vs Socket Timeout

#### Connect Timeout
- **Definition**: The maximum time the client will wait for a connection to be established with the server.
- **Usage**: It is used to specify the time limit for establishing a connection.
- **Example**: If the server is down or unreachable, the client will wait for the specified connect timeout duration before throwing an exception.

#### Socket Timeout
- **Definition**: The maximum time the client will wait for data to be available for reading or writing on an established connection.
- **Usage**: It is used to specify the time limit for waiting for data after the connection has been established.
- **Example**: If the server takes too long to respond after the connection is established, the client will wait for the specified socket timeout duration before throwing an exception.

### Example in Java (Spring Boot Configuration)
```properties
# Connect Timeout: 2000 milliseconds (2 seconds)
spring.datasource.hikari.connection-timeout=2000

# Socket Timeout: 6000 milliseconds (6 seconds)
spring.datasource.hikari.socket-timeout=6000
```

### Example in Java (HttpClient Configuration)
```java
import org.apache.http.client.config.RequestConfig;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

public class HttpClientConfig {
    public static void main(String[] args) {
        RequestConfig requestConfig = RequestConfig.custom()
                .setConnectTimeout(2000) // Connect Timeout: 2000 milliseconds (2 seconds)
                .setSocketTimeout(6000)  // Socket Timeout: 6000 milliseconds (6 seconds)
                .build();

        CloseableHttpClient httpClient = HttpClients.custom()
                .setDefaultRequestConfig(requestConfig)
                .build();
    }
}
```
