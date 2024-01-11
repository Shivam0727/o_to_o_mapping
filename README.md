
# Spring Boot REST API with JPA, MySQL, and One-to-One Mapping

This README file provides a comprehensive guide for setting up a Spring Boot project with REST API endpoints for CRUD operations, MySQL database connectivity using JPA and MySQL Connector, and implementing One-to-One mapping between two entity classes.

## Prerequisites

Before you begin, ensure you have the following installed:

### Java Development Kit (JDK)
### Eclipse IDE (or any preferred IDE)
### MySQL Database Server

## Step 1: Create a Spring Boot Project

- Open Eclipse IDE and go to File -> New -> Spring Starter Project.

- Enter the project name, select the desired package, and include the dependencies: Spring Web, Spring Data JPA, and MySQL Driver.

- Click Finish to create the project.

## Step 2: Configure MySQL Database

Open the src/main/resources/application.properties file and configure the MySQL database connection properties:

    spring.datasource.url=jdbc:mysql://localhost:3306/your_database_name
    spring.datasource.username=your_username
    spring.datasource.password=your_password
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
    spring.jpa.hibernate.ddl-auto=update

Replace your_database_name, your_username, and your_password with your actual MySQL database details.

## Step 3: Implement REST API Endpoints

Create a package for your controllers (e.g., com.example.demo.controller) and create a class for your REST API endpoints similar to the previous example.

## Step 4: Add External MySQL JAR to Eclipse Build Path

- Download the MySQL Connector JAR file from the official MySQL website.

- In Eclipse, right-click on your project and select Build Path -> Configure Build Path.

- Go to the Libraries tab, click Add External JARs, and select the downloaded MySQL Connector JAR file.

- Click Apply and Close to save the changes.

## Step 5: Implement One-to-One Mapping

Create another entity class (e.g., PersonDetails) for one-to-one mapping:

    @Entity
    public class PersonDetails {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String address;
        // Getters and setters
    }
    
Update the existing entity class (e.g., Person) to include a reference to the new class:


    @Entity
    public class Person {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
        private String name;
        @OneToOne(cascade = CascadeType.ALL)
        @JoinColumn(name = "person_details_id", referencedColumnName = "id")
        private PersonDetails personDetails;
        // Getters and setters
    }

- This establishes a unidirectional one-to-one mapping from Person to PersonDetails.

- Continue with the necessary modifications to the controller to handle one-to-one mapping operations.

Now, you have a Spring Boot project with REST API endpoints, JPA for data persistence, MySQL as the database, and one-to-one mapping implemented between Person and PersonDetails entities. The MySQL Connector JAR is added to the Eclipse build path, and the database connection details are configured in application.properties. Customize the project based on your specific requirements.





