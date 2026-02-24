# Phone JDBC Project

A Spring-based Java application for managing phone inventory with CRUD operations and advanced sorting/filtering capabilities using JDBC and PostgreSQL database.

## Project Overview

This application demonstrates direct database operations using Spring Framework for dependency injection and JDBC for data access. It manages phone records with features like adding, removing, sorting, and filtering phones by various attributes through a DAO layer.

## Technology Stack

- **Java**: 21
- **Spring Framework**: 7.0.3 (Spring Core & Context)
- **Database**: PostgreSQL
- **JDBC**: Direct database connectivity
- **Build Tool**: Maven
- **Architecture**: DAO Pattern with Spring DI

## Project Structure

```
Phone-JDBC/
├── src/main/java/org/example/
│   ├── entity/
│   │   └── Phone.java                 # Entity class representing phone data
│   ├── dao/
│   │   ├── PhoneDao.java              # DAO interface
│   │   └── PhoneDaoImpl.java          # DAO implementation with JDBC
│   └── ui/
│       └── UserInterface.java         # Main application entry point
├── src/main/resources/
│   └── applicationContext.xml         # Spring XML configuration
└── pom.xml                            # Maven dependencies
```

## Features

### Core Operations
- **Add Phone**: Insert new phone records with validation
- **Remove Phone**: Delete phones by ID with validation
- **Find All**: Retrieve all phone records from database

### Sorting Capabilities
- Sort by Price (Ascending/Descending)
- Sort by Brand (Ascending/Descending)
- Sort by Category/Model (Ascending/Descending)
- Sort by Release Date

### Filtering
- Filter phones by Brand
- Filter phones by Category/Model

## Database Schema

**Table Name**: `Phone`

| Column       | Type         | Description                    |
|--------------|--------------|--------------------------------|
| id           | INTEGER      | Primary key                    |
| name         | VARCHAR      | Phone model name               |
| brand        | VARCHAR      | Manufacturer brand             |
| category     | VARCHAR      | Phone category/type            |
| cost         | DOUBLE       | Price of the phone             |
| releaseDate  | DATE         | Release date of the phone      |

## Configuration

### Database Connection
Update the following in `PhoneDaoImpl.java`:
```java
String uname = "postgres";
String pass = "";  // Add your password
String url = "jdbc:postgresql://localhost:5433/demo";
```

### Spring Configuration

The application uses annotation-based configuration:
- `@Component(value="pdao")` on PhoneDaoImpl class
- `@Configuration` and `@ComponentScan` on UserInterface class
- Spring manages DAO bean lifecycle and dependency injection





1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Phone_Core_Spring
   ```

2. **Setup PostgreSQL Database**
   ```sql
   CREATE DATABASE demo;
   
   CREATE TABLE Phone (
       id INTEGER PRIMARY KEY,
       name VARCHAR(100),
       brand VARCHAR(50),
       category VARCHAR(50),
       cost DOUBLE PRECISION,
       releaseDate DATE
   );
   ```


## Usage Examples

### Adding Phones
```java
phoneDao.addPhone(new Phone(1, "iPhone 13", "Apple", "Smartphone", 999.99, LocalDate.parse("2021-09-24")));
```

### Retrieving All Phones
```java
List<Phone> phones = phoneDao.findAll();
phones.forEach(System.out::println);
```

### Sorting by Price
```java
phoneDao.sortByPrice();  // Ascending
phoneDao.sortPriceDescending();  // Descending
```

### Filtering by Brand
```java
List<Phone> applePhones = phoneDao.filterByBrand("Apple");
```

## Architecture Layers

### 1. Entity Layer
- `Phone.java`: POJO with getters, setters, and toString method
- Represents phone data with attributes: id, name, brand, category, cost, releaseDate

### 2. DAO Layer
- `PhoneDao`: Interface defining data access methods
- `PhoneDaoImpl`: JDBC implementation with direct SQL queries
- Uses PreparedStatement for secure database operations
- Implements CRUD operations and sorting/filtering methods

### 3. UI Layer
- `UserInterface`: Main class with Spring context initialization
- Entry point for the application

## Dependencies

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>7.0.3</version>
</dependency>
```

PostgreSQL JDBC driver is required (add to pom.xml if missing):
```xml
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.0</version>
</dependency>
```

