# Application Overview

# Purpose of each application, language, port, dependencies.



=== ui
| Language | Persistence |
| Java     | N/A         |
| `PORT`                            | The port which the server will listen on  
| `RETAIL_UI_THEME`                 | Name of the theme for the UI, valid values
| `RETAIL_UI_DISABLE_DEMO_WARNINGS` | Disable the UI messages warning about demo
| `RETAIL_UI_PRODUCT_IMAGES_PATH`   | Overrides the location where the sample pr
| `RETAIL_UI_ENDPOINTS_CATALOG`     | The endpoint of the catalog API. If set to
| `RETAIL_UI_ENDPOINTS_CARTS`       | The endpoint of the carts API. If set to `
=== catalog
| Language | Persistence |
| Go       | MySQL       |
| PORT                                       | The port which the server will li
| RETAIL_CATALOG_PERSISTENCE_PROVIDER        | The persistence provider to use, 
| RETAIL_CATALOG_PERSISTENCE_ENDPOINT        | Database endpoint URL            
| RETAIL_CATALOG_PERSISTENCE_DB_NAME         | Database name                    
| RETAIL_CATALOG_PERSISTENCE_USER            | Database user                    
| RETAIL_CATALOG_PERSISTENCE_PASSWORD        | Database password                
=== cart
| Language | Persistence     |
| Java     | Amazon DynamoDB |
| `PORT`                                          | The port which the server wi
| `RETAIL_CART_PERSISTENCE_PROVIDER`              | The persistence provider to 
| `RETAIL_CART_PERSISTENCE_DYNAMODB_TABLE_NAME`   | The name of the Amazon Dynam
| `RETAIL_CART_PERSISTENCE_DYNAMODB_ENDPOINT`     | The Amazon DynamoDB endpoint
| `RETAIL_CART_PERSISTENCE_DYNAMODB_CREATE_TABLE` | Enable to automatically crea
=== checkout
| Language | Persistence |
| Node     | Redis       |
| `PORT`                                  | The port which the server will liste
| `RETAIL_CHECKOUT_PERSISTENCE_PROVIDER`  | The persistence provider to use, can
| `RETAIL_CHECKOUT_PERSISTENCE_REDIS_URL` | The endpoint of the Redis server use
| `RETAIL_CHECKOUT_ENDPOINTS_ORDERS`      | The endpoint of the orders API. If e
| `RETAIL_CHECKOUT_SHIPPING_NAME_PREFIX`  | A string prefix that can be applied 
=== orders
| Language | Persistence |
| Java     | PostgreSQL  |
| `PORT`                                        | The port which the server will
| `RETAIL_CHECKOUT_PERSISTENCE_PROVIDER`        | The persistence provider to us
| `RETAIL_ORDERS_PERSISTENCE_ENDPOINT`          | The postgres database endpoint
| `RETAIL_ORDERS_PERSISTENCE_NAME`              | The postgres database name    
| `RETAIL_ORDERS_PERSISTENCE_USERNAME`          | Username to authenticate with 
| `RETAIL_ORDERS_PERSISTENCE_PASSWORD`          | Password to authenticate with 


# Host port mapping

cart/docker-compose.yml:    ports:
cart/docker-compose.yml-      - "8082:8080"
cart/docker-compose.yml-    healthcheck:
cart/docker-compose.yml-      test:
--
catalog/docker-compose.yml:    ports:
catalog/docker-compose.yml-      - "8081:8080"
catalog/docker-compose.yml-    healthcheck:
catalog/docker-compose.yml-      test: ["CMD-SHELL", "curl -f http://localhost:8080/health || exit 1"]
--
checkout/docker-compose.yml:    ports:
checkout/docker-compose.yml-      - '8085:8080'
checkout/docker-compose.yml-    healthcheck:
checkout/docker-compose.yml-      test: ['CMD-SHELL', 'curl -f http://localhost:8080/health || exit 1']
--
checkout/docker-compose.yml:    ports:
checkout/docker-compose.yml-      - '6379:6379'
checkout/docker-compose.yml-    healthcheck:
checkout/docker-compose.yml-      test: ['CMD', 'redis-cli', 'ping']
--
orders/docker-compose.yml:    ports:
orders/docker-compose.yml-      - "8083:8080"
orders/docker-compose.yml-    depends_on:
orders/docker-compose.yml-      orders-db:
--
orders/docker-compose.yml:    ports:
orders/docker-compose.yml-      - "5432:5432"
orders/docker-compose.yml-    healthcheck:
orders/docker-compose.yml-      test: ["CMD-SHELL", "pg_isready -d orders -U orders_user"]
--
orders/docker-compose.yml:    ports:
orders/docker-compose.yml-      - "61616:61616"
orders/docker-compose.yml-      - "8161:8161"
--
ui/docker-compose.yml:    ports:
ui/docker-compose.yml-      - 8888:8080
ui/docker-compose.yml-    environment:
ui/docker-compose.yml-      - JAVA_OPTS=-XX:MaxRAMPercentage=75.0 -Djava.security.egd=file:/dev/urandom


# API paths per service

cart/openapi.yml:  /carts/{customerId}/items:
cart/openapi.yml:  /carts/{customerId}:
cart/openapi.yml:  /carts/{customerId}/merge:
cart/openapi.yml:  /carts/{customerId}/items/{itemId}:
catalog/openapi.yml:  "/catalog/products":
catalog/openapi.yml:  "/catalog/products/{id}":
catalog/openapi.yml:  "/catalog/size":
catalog/openapi.yml:  "/catalog/tags":
checkout/openapi.yml:  /checkout/{customerId}:
checkout/openapi.yml:  /checkout/{customerId}/update:
checkout/openapi.yml:  /checkout/{customerId}/submit:
orders/openapi.yml:  /orders:


