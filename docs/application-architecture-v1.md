# Application Endpoints

4:      - RETAIL_UI_ENDPOINTS_CATALOG=http://catalog:8080
5:      - RETAIL_UI_ENDPOINTS_CARTS=http://carts:8080
6:      - RETAIL_UI_ENDPOINTS_ORDERS=http://orders:8080
7:      - RETAIL_UI_ENDPOINTS_CHECKOUT=http://checkout:8080
33:      - RETAIL_CHECKOUT_ENDPOINTS_ORDERS=http://orders:8080

# Databse dependencies
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:26:import org.spring
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:59:  public static f
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:61:  public static f
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:76:    return new Qu
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:80:  FanoutExchange 
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:81:    return new Fa
app/src/orders/src/main/java/com/amazon/sample/orders/config/messaging/RabbitMQMessagingConfig.java:85:  Binding binding

# Asynchronous messaging
app/src/orders/src/main/java/com/amazon/sample/orders/metrics/OrdersMetrics.java:29:import org.springframework.transaction.event.TransactionalEventListener;
app/src/orders/src/main/java/com/amazon/sample/orders/metrics/OrdersMetrics.java:49:  @TransactionalEventListener
app/src/orders/src/main/java/com/amazon/sample/orders/messaging/OrdersEventHandler.java:27:import org.springframework.transaction.event.TransactionalEventListener;
app/src/orders/src/main/java/com/amazon/sample/orders/messaging/OrdersEventHandler.java:38:  @TransactionalEventListener
