# JavaCart E-Commerce System (Java 8)

A comprehensive mini e-commerce console application built with Java 8, featuring product browsing, cart management, order processing, and database-driven inventory management using JDBC, Stream API, and multithreading.

## 🚀 Features

### Core Functionality
- **User Authentication**: Login/registration system with role-based access (Admin/Customer)
- **Product Management**: Browse, search, filter, and sort products using Stream API
- **Shopping Cart**: Add/remove items, quantity management, and price calculations
- **Order Processing**: Complete checkout flow with inventory updates
- **Admin Dashboard**: Product CRUD operations and order management

### Java 8 Technical Highlights
- **Stream API Integration**: Advanced filtering, sorting, and aggregation operations with lambda expressions
- **Optional Class**: Null-safe operations throughout the application
- **Method References**: Clean, readable code with method references
- **Functional Interfaces**: Custom predicates, functions, and consumers
- **Default Interface Methods**: Enhanced interfaces with default implementations
- **JDBC Database Operations**: MySQL integration with prepared statements and transactions
- **Multithreading**: Concurrent order processing with thread-safe inventory updates
- **Custom Exception Handling**: Robust error management for business logic

## 🛠️ Technology Stack

- **Java 8**: Core programming language with modern functional features
- **MySQL 8.0**: Relational database for persistent storage
- **JDBC**: Database connectivity and operations
- **Stream API**: Functional programming for data processing
- **JUnit 5**: Unit testing framework
- **Maven**: Build automation and dependency management

## 📋 Prerequisites

- Java 8 or higher
- MySQL 8.0 or higher
- Maven 3.6 or higher

## 🔧 Setup Instructions

### 1. Database Setup

1. Install MySQL and create a database:
\`\`\`sql
CREATE DATABASE javacart;
\`\`\`

2. Update database credentials in `DatabaseManager.java`:
\`\`\`java
private static final String URL = "jdbc:mysql://localhost:3306/javacart";
private static final String USERNAME = "your_username";
private static final String PASSWORD = "your_password";
\`\`\`

### 2. Build and Run

1. Clone the repository:
\`\`\`bash
git clone <repository-url>
cd javacart-ecommerce
\`\`\`

2. Build the project:
\`\`\`bash
mvn clean compile
\`\`\`

3. Run the application:
\`\`\`bash
mvn exec:java -Dexec.mainClass="com.javacart.Main"
\`\`\`

Alternatively, create an executable JAR:
\`\`\`bash
mvn clean package
java -jar target/javacart-ecommerce-1.0.0.jar
\`\`\`

### 3. Database Initialization

The application automatically creates tables and inserts sample data on first run. You can also run the SQL scripts manually:

\`\`\`bash
mysql -u your_username -p javacart < scripts/01_create_database.sql
mysql -u your_username -p javacart < scripts/02_insert_sample_data.sql
\`\`\`

## 👥 Default User Accounts

| Username | Password | Role |
|----------|----------|------|
| admin | password | ADMIN |
| customer | password | CUSTOMER |

## 🎯 Usage Guide

### Customer Features
1. **Browse Products**: View all products with filtering and sorting options
2. **Search**: Find products by name, description, or category
3. **Shopping Cart**: Add/remove items and manage quantities
4. **Checkout**: Complete orders with automatic inventory updates
5. **Order History**: View past orders and order details

### Admin Features
1. **Product Management**: Add, update, and delete products
2. **Inventory Control**: Monitor and update stock levels
3. **Order Management**: View all customer orders
4. **Concurrent Processing**: Simulate multiple simultaneous orders

## 🔍 Java 8 Stream API Examples

The application showcases various Java 8 Stream API operations:

\`\`\`java
// Lambda expressions with filtering
products.stream()
    .filter(product -> product.getCategory().equalsIgnoreCase(category))
    .filter(Product::isInStock)  // Method reference
    .collect(Collectors.toList());

// Method references with sorting
products.stream()
    .sorted(Comparator.comparing(Product::getPrice))
    .collect(Collectors.toList());

// Functional reduction with method references
cartItems.stream()
    .map(Cart::getTotalPrice)
    .reduce(BigDecimal.ZERO, BigDecimal::add);

// Complex filtering with lambda expressions
products.stream()
    .filter(product -> 
        product.getName().toLowerCase().contains(keyword.toLowerCase()) ||
        product.getDescription().orElse("").toLowerCase().contains(keyword.toLowerCase()) ||
        product.getCategory().toLowerCase().contains(keyword.toLowerCase())
    )
    .collect(Collectors.toList());

// Optional chaining for null safety
return getProduct()
    .map(Product::getPrice)
    .filter(Objects::nonNull)
    .map(price -> price.multiply(BigDecimal.valueOf(quantity)))
    .orElse(BigDecimal.ZERO);
\`\`\`

## 🔧 Java 8 Features Demonstrated

### 1. Lambda Expressions
\`\`\`java
// Menu actions with lambdas
Runnable[] menuActions = {
    () -> ui.handleLogin(authService),
    () -> ui.handleRegistration(authService),
    () -> System.exit(0)
};
\`\`\`

### 2. Optional Class
\`\`\`java
// Null-safe operations
public Optional<User> getCurrentUser() {
    return Optional.ofNullable(currentUser);
}
\`\`\`

### 3. Default Interface Methods
\`\`\`java
// Interface with default methods
public interface AuthService {
    default boolean isAdmin() {
        return getCurrentUser()
            .map(User::getRole)
            .filter("ADMIN"::equals)
            .isPresent();
    }
}
\`\`\`

### 4. Functional Interfaces
\`\`\`java
// Custom predicates and functions
public static final Predicate<Product> IN_STOCK = product -> 
    product.getStockQuantity() != null && product.getStockQuantity() > 0;

public static final Function<List<Cart>, BigDecimal> CALCULATE_TOTAL = cartItems ->
    cartItems.stream()
        .map(Cart::getTotalPrice)
        .reduce(BigDecimal.ZERO, BigDecimal::add);
\`\`\`

## 🧵 Multithreading Features

- **Concurrent Order Processing**: Multiple orders can be processed simultaneously
- **Thread-Safe Inventory Updates**: ReentrantLock ensures data consistency
- **Executor Service**: Manages thread pool for optimal performance

## 🧪 Testing

Run the test suite:
\`\`\`bash
mvn test
\`\`\`

The project includes comprehensive unit tests for:
- Product service operations
- Cart management functionality
- Password utility methods
- Stream API operations

## 📊 Database Schema

### Tables
- **users**: User accounts with role-based access
- **products**: Product catalog with inventory tracking
- **cart**: Shopping cart items per user
- **orders**: Order records with status tracking
- **order_items**: Individual items within orders

### Key Relationships
- Users have many cart items and orders
- Products can be in multiple carts and orders
- Orders contain multiple order items

## 🚀 Advanced Features

### Exception Handling
- `ProductNotFoundException`: When products don't exist
- `OutOfStockException`: When inventory is insufficient
- `UserNotFoundException`: For authentication failures

### Design Patterns
- **Service Layer Pattern**: Separation of business logic
- **DAO Pattern**: Data access abstraction
- **Singleton Pattern**: Database connection management
- **Strategy Pattern**: Different sorting and filtering strategies

## 📈 Performance Considerations

- **Connection Pooling**: Efficient database connection management
- **Prepared Statements**: SQL injection prevention and performance
- **Transaction Management**: ACID compliance for order processing
- **Lazy Loading**: Efficient data retrieval strategies
- **Parallel Streams**: For large dataset processing

## 🔒 Security Features

- **Password Hashing**: SHA-256 with salt for secure password storage
- **SQL Injection Prevention**: Parameterized queries throughout
- **Role-Based Access**: Admin vs Customer functionality separation
- **Input Validation**: Comprehensive data validation

## 📁 Project Structure

\`\`\`
javacart-ecommerce/
├── src/
│   ├── main/java/com/javacart/
│   │   ├── Main.java                    # Application entry point
│   │   ├── database/
│   │   │   └── DatabaseManager.java     # Database connection management
│   │   ├── exceptions/                  # Custom exception classes
│   │   │   ├── OutOfStockException.java
│   │   │   ├── ProductNotFoundException.java
│   │   │   └── UserNotFoundException.java
│   │   ├── models/                      # Entity classes
│   │   │   ├── Cart.java
│   │   │   ├── Order.java
│   │   │   ├── OrderItem.java
│   │   │   ├── Product.java
│   │   │   └── User.java
│   │   ├── services/                    # Business logic interfaces
│   │   │   ├── AuthService.java
│   │   │   ├── CartService.java
│   │   │   ├── OrderService.java
│   │   │   ├── ProductService.java
│   │   │   └── impl/                    # Service implementations
│   │   │       ├── AuthServiceImpl.java
│   │   │       ├── CartServiceImpl.java
│   │   │       ├── OrderServiceImpl.java
│   │   │       └── ProductServiceImpl.java
│   │   └── utils/                       # Utility classes
│   │       ├── ConsoleUI.java
│   │       ├── Java8StreamExamples.java
│   │       └── PasswordUtil.java
│   └── test/java/com/javacart/         # Unit tests
│       ├── services/
│       │   ├── CartServiceTest.java
│       │   └── ProductServiceTest.java
│       └── utils/
│           └── PasswordUtilTest.java
├── scripts/                            # Database scripts
│   ├── 01_create_database.sql
│   └── 02_insert_sample_data.sql
├── pom.xml                            # Maven configuration
├── .gitignore                         # Git ignore rules
└── README.md                          # Project documentation
\`\`\`

## 📝 Future Enhancements

- REST API implementation with Spring Boot
- Web-based user interface
- Payment gateway integration
- Email notifications
- Product reviews and ratings
- Advanced reporting and analytics

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support

For questions or issues, please create an issue in the repository or contact the development team.

---

**JavaCart** - Demonstrating enterprise-level Java 8 development with modern functional programming practices and comprehensive feature implementation.
