## EntityManagers, PersistenceContext and Transactions

EntityManagers:

- Container Managed
  - Managed by J2EE containers like Spring
  - Injected using @PersistenceContext
  ```
  @PersistenceContext(unitName="EmployeeService") 
  EntityManager em;
  ```
  
  - Types
    - Transaction Scoped
    - Extended Scoped
    ```
    @PersistenceContext(unitName="UserService" , type=PersistenceContextType.EXTENDED) 
    EntityManager em;
    ```

- Application Managed
  ```
  EntityManagerFactory emf = 
  Persistence.createEntityManagerFactory("myPersistenceUnit"); 
  EntityManager em = emf.createEntityManager();
  ```

There are two types of Transaction management types supported in JPA.

  - RESOURCE LOCAL Transactions
  - JTA or GLOBAL Transactions

Resource local transactions refer to the native transactions of the JDBC Driver whereas JTA transactions refer to the transactions of the JEE server. A Resource Local transaction involves a single transactional resource, for example a JDBC Connection. Whenever you need two or more resources(f or example a JMS Connection and a JDBC Connection) within a single transaction, you use  JTA Transaction.

Container Managed Entity Managers always use JTA transactions as the container takes care of transaction life cycle management and spawning the transaction across multiple transactional resources. Application Managed Entity Managers can use either Resource Local Transactions or JTA transactions.
