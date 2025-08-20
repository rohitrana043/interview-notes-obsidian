## 📚 Table of Contents

### Main Sections
1. [[#Part 1 Spring Essentials]]
2. [[#Part 2 Spring in Business Layer]]
3. [[#Part 3 Spring in Web Layer]]
4. [[#Master Interview Section]]
5. [[#Quick Reference]]

### Chapters
- [[#Chapter 1 Spring Jump Start]]
- [[#Chapter 2 Wiring Beans]]
- [[#Chapter 3 Creating Aspects]]
- [[#Chapter 4 Database Access]]
- [[#Chapter 5 Transaction Management]]
- [[#Chapter 6 Remoting]]
- [[#Chapter 7 Enterprise Services]]
- [[#Chapter 8 Building Web Layer]]
- [[#Chapter 9 View Layer Alternatives]]
- [[#Chapter 10 Other Web Frameworks]]
- [[#Chapter 11 Security]]
---

## Part 1: Spring Essentials

### Chapter 1: Spring Jump Start

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Why Spring?**|• Simplifies J2EE development complexity<br>• Reduces boilerplate code<br>• Promotes loose coupling through dependency injection<br>• Enables testability without application server<br>• Provides comprehensive infrastructure support|
|**Spring Modules**|• **Core Container**: Bean factory, ApplicationContext<br>• **AOP Module**: Aspect-oriented programming support<br>• **Data Access**: JDBC, ORM integration<br>• **Web Module**: MVC framework, integration<br>• **Test Module**: Unit and integration testing support|
|**Inversion of Control (IoC)**|• Hollywood Principle: "Don't call us, we'll call you"<br>• Container manages object lifecycle and dependencies<br>• Objects declare dependencies, container provides them<br>• Promotes loose coupling and testability|
|**Dependency Injection Types**|• **Constructor Injection**: Dependencies via constructor<br>• **Setter Injection**: Dependencies via setter methods<br>• **Field Injection**: Direct field access (not recommended)<br>• **Method Injection**: For prototype beans in singletons|
|**AOP Introduction**|• Separates cross-cutting concerns from business logic<br>• Examples: logging, security, transactions<br>• Implemented via proxies in Spring<br>• Reduces code duplication and improves modularity|
|**Spring vs EJB**|• Spring: Lightweight, POJO-based, testable<br>• EJB: Heavyweight, requires app server<br>• Spring provides similar services with less complexity<br>• Better development experience and flexibility|

#### Code Examples

```java
// Traditional approach - tight coupling
public class UserService {
    private UserRepository repository = new UserRepository();
    
    public void createUser(String name) {
        // Tightly coupled to UserRepository implementation
        repository.save(name);
    }
}

// Spring IoC approach - loose coupling
@Component
public class UserService {
    private final UserRepository repository;
    
    @Autowired
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
    
    public void createUser(String name) {
        // Loosely coupled, repository can be mocked for testing
        repository.save(name);
    }
}

// Configuration Example
@Configuration
@ComponentScan("com.example")
public class AppConfig {
    
    @Bean
    public DataSource dataSource() {
        BasicDataSource ds = new BasicDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/mydb");
        ds.setUsername("root");
        ds.setPassword("password");
        return ds;
    }
}
```

#### Chapter 1 Interview Q&A

**Q1: What problems does Spring solve in J2EE development?** **A:** Spring addresses:

- Boilerplate code reduction
- Complex JNDI lookups simplified
- Testing difficulties (no container needed)
- Tight coupling between components
- Heavy EJB model replaced with POJOs

**Q2: Explain the Hollywood Principle in Spring context.** **A:** "Don't call us, we'll call you" means:

- Components don't create dependencies
- Container calls components with dependencies
- Inversion of control flow
- Example: Container calls setter/constructor, not vice versa

**Q3: How does Spring achieve loose coupling?** **A:** Through:

- Dependency Injection (dependencies provided externally)
- Interface-based programming
- Configuration externalization
- AOP for cross-cutting concerns

---

### Chapter 2: Wiring Beans

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**BeanFactory vs ApplicationContext**|• **BeanFactory**: Basic container, lazy loading<br>• **ApplicationContext**: Advanced features, eager loading<br>• ApplicationContext preferred for most applications<br>• Provides i18n, event propagation, declarative mechanisms|
|**Bean Lifecycle**|1. Instantiation<br>2. Populate properties<br>3. BeanNameAware's setBeanName()<br>4. BeanFactoryAware's setBeanFactory()<br>5. ApplicationContextAware's setApplicationContext()<br>6. BeanPostProcessor's postProcessBeforeInitialization()<br>7. InitializingBean's afterPropertiesSet()<br>8. Custom init-method<br>9. BeanPostProcessor's postProcessAfterInitialization()<br>10. Bean is ready for use<br>11. DisposableBean's destroy()<br>12. Custom destroy-method|
|**Bean Scopes**|• **singleton**: One instance per container (default)<br>• **prototype**: New instance for each request<br>• **request**: One instance per HTTP request<br>• **session**: One instance per HTTP session<br>• **global-session**: One instance per global HTTP session|
|**Autowiring Modes**|• **no**: Default, no autowiring<br>• **byName**: Match property name with bean name<br>• **byType**: Match property type with bean type<br>• **constructor**: Like byType for constructor arguments<br>• **autodetect**: Choose constructor or byType|
|**Special Beans**|• **BeanPostProcessor**: Modify beans after creation<br>• **BeanFactoryPostProcessor**: Modify bean definitions<br>• **PropertyPlaceholderConfigurer**: External properties<br>• **CustomEditorConfigurer**: Custom property editors<br>• **MessageSource**: i18n support|

#### Code Examples

```xml
<!-- XML Configuration -->
<beans xmlns="http://www.springframework.org/schema/beans">
    
    <!-- Simple bean definition -->
    <bean id="userService" class="com.example.UserService">
        <property name="maxUsers" value="100"/>
        <property name="repository" ref="userRepository"/>
    </bean>
    
    <!-- Constructor injection -->
    <bean id="userRepository" class="com.example.UserRepository">
        <constructor-arg ref="dataSource"/>
        <constructor-arg value="users_table"/>
    </bean>
    
    <!-- Collections injection -->
    <bean id="emailService" class="com.example.EmailService">
        <property name="servers">
            <list>
                <value>smtp1.example.com</value>
                <value>smtp2.example.com</value>
            </list>
        </property>
        <property name="config">
            <map>
                <entry key="timeout" value="5000"/>
                <entry key="retries" value="3"/>
            </map>
        </property>
    </bean>
    
    <!-- Autowiring example -->
    <bean id="orderService" class="com.example.OrderService" autowire="byType"/>
    
    <!-- Bean with lifecycle methods -->
    <bean id="connectionPool" 
          class="com.example.ConnectionPool"
          init-method="initialize"
          destroy-method="cleanup"
          scope="singleton"/>
</beans>
```

```java
// Java Configuration
@Configuration
public class AppConfig {
    
    @Bean(initMethod = "init", destroyMethod = "cleanup")
    @Scope("singleton")
    public ConnectionPool connectionPool() {
        ConnectionPool pool = new ConnectionPool();
        pool.setMaxConnections(10);
        return pool;
    }
    
    @Bean
    @Scope("prototype")
    public UserSession userSession() {
        return new UserSession();
    }
}

// Bean Post Processor Example
@Component
public class LoggingBeanPostProcessor implements BeanPostProcessor {
    
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) {
        System.out.println("Initializing bean: " + beanName);
        return bean;
    }
    
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) {
        System.out.println("Bean initialized: " + beanName);
        return bean;
    }
}

// Property Placeholder Example
@Component
public class DatabaseConfig {
    
    @Value("${db.url}")
    private String url;
    
    @Value("${db.username}")
    private String username;
    
    @Value("${db.password}")
    private String password;
    
    @Bean
    public DataSource dataSource() {
        BasicDataSource ds = new BasicDataSource();
        ds.setUrl(url);
        ds.setUsername(username);
        ds.setPassword(password);
        return ds;
    }
}
```

#### Chapter 2 Interview Q&A

**Q1: When would you use prototype scope vs singleton?** **A:**

- **Singleton**: Stateless services, DAOs, controllers
- **Prototype**: Stateful objects, user sessions, requests
- Example: UserService (singleton) vs UserSession (prototype)

**Q2: How do you handle circular dependencies?** **A:**

- Use setter injection (Spring handles it)
- @Lazy annotation delays initialization
- Redesign to avoid circular dependencies
- Constructor injection will fail with circular deps

**Q3: What happens during bean initialization?** **A:** Sequential process:

1. Container creates instance
2. Dependencies injected
3. Aware interfaces called
4. BeanPostProcessor pre-initialization
5. @PostConstruct/InitializingBean
6. Custom init-method
7. BeanPostProcessor post-initialization

**Q4: How does autowiring by type handle multiple candidates?** **A:**

- Throws exception if multiple beans match
- Solutions: @Primary, @Qualifier, or explicit wiring
- Can exclude beans with autowire-candidate="false"

---

### Chapter 3: Creating Aspects

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**AOP Terminology**|• **Aspect**: Module of cross-cutting concern<br>• **Join Point**: Point during execution<br>• **Advice**: Action taken at join point<br>• **Pointcut**: Predicate matching join points<br>• **Introduction**: Adding methods/fields to types<br>• **Target**: Object being advised<br>• **Proxy**: Object created after applying advice<br>• **Weaving**: Linking aspects with objects|
|**Advice Types**|• **Before**: Runs before method execution<br>• **After Returning**: After successful completion<br>• **After Throwing**: After exception thrown<br>• **After (Finally)**: After method completion<br>• **Around**: Wraps method execution|
|**Pointcut Expressions**|• **execution()**: Method execution matching<br>• **within()**: Type matching<br>• **this()**: Proxy type matching<br>• **target()**: Target object matching<br>• **args()**: Argument matching<br>• **@annotation**: Annotation matching|
|**ProxyFactoryBean**|• Creates AOP proxies programmatically<br>• Configures target, interceptors, interfaces<br>• JDK dynamic proxy for interfaces<br>• CGLIB proxy for classes|
|**Autoproxying**|• **BeanNameAutoProxyCreator**: By bean name<br>• **DefaultAdvisorAutoProxyCreator**: By advisor<br>• Automatic proxy creation<br>• Reduces configuration|

#### Code Examples

```java
// Aspect Definition
@Aspect
@Component
public class LoggingAspect {
    
    // Simple before advice
    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Executing: " + joinPoint.getSignature().getName());
        System.out.println("Arguments: " + Arrays.toString(joinPoint.getArgs()));
    }
    
    // After returning with return value
    @AfterReturning(
        pointcut = "execution(* com.example.service.*.find*(..))",
        returning = "result"
    )
    public void logAfterReturning(JoinPoint joinPoint, Object result) {
        System.out.println("Method returned: " + result);
    }
    
    // After throwing advice
    @AfterThrowing(
        pointcut = "execution(* com.example.service.*.*(..))",
        throwing = "error"
    )
    public void logAfterThrowing(JoinPoint joinPoint, Throwable error) {
        System.out.println("Exception in: " + joinPoint.getSignature().getName());
        System.out.println("Exception: " + error.getMessage());
    }
    
    // Around advice with performance monitoring
    @Around("@annotation(Monitored)")
    public Object monitorPerformance(ProceedingJoinPoint pjp) throws Throwable {
        long start = System.currentTimeMillis();
        
        try {
            Object result = pjp.proceed();
            return result;
        } finally {
            long duration = System.currentTimeMillis() - start;
            System.out.println(pjp.getSignature().getName() + " took " + duration + "ms");
        }
    }
    
    // Pointcut definition
    @Pointcut("execution(* com.example.repository.*.*(..))")
    public void repositoryMethods() {}
    
    @Pointcut("@annotation(Transactional)")
    public void transactionalMethods() {}
    
    // Combining pointcuts
    @Before("repositoryMethods() && transactionalMethods()")
    public void auditDataAccess(JoinPoint joinPoint) {
        System.out.println("Transactional repository access: " + joinPoint.getSignature());
    }
}

// Introduction Example
@Aspect
@Component
public class AuditingAspect {
    
    @DeclareParents(
        value = "com.example.service.*+",
        defaultImpl = DefaultAuditable.class
    )
    public static Auditable mixin;
}

interface Auditable {
    void setLastModified(Date date);
    Date getLastModified();
}

class DefaultAuditable implements Auditable {
    private Date lastModified;
    
    public void setLastModified(Date date) {
        this.lastModified = date;
    }
    
    public Date getLastModified() {
        return lastModified;
    }
}

// ProxyFactoryBean Example
@Configuration
public class AopConfig {
    
    @Bean
    public ProxyFactoryBean userService(UserServiceImpl target) {
        ProxyFactoryBean proxy = new ProxyFactoryBean();
        proxy.setTarget(target);
        proxy.setInterceptorNames("loggingInterceptor", "securityInterceptor");
        proxy.setProxyTargetClass(true); // Use CGLIB
        return proxy;
    }
    
    @Bean
    public MethodInterceptor loggingInterceptor() {
        return invocation -> {
            System.out.println("Before: " + invocation.getMethod().getName());
            Object result = invocation.proceed();
            System.out.println("After: " + invocation.getMethod().getName());
            return result;
        };
    }
}
```

#### Chapter 3 Interview Q&A

**Q1: What's the difference between JDK dynamic proxy and CGLIB?** **A:**

- **JDK Proxy**: Interface-based, built-in Java
- **CGLIB**: Subclass-based, works with classes
- JDK proxy faster but requires interfaces
- CGLIB can proxy concrete classes

**Q2: When would you use different advice types?** **A:**

- **@Before**: Validation, logging entry
- **@AfterReturning**: Process results, logging success
- **@AfterThrowing**: Error handling, alerting
- **@Around**: Performance monitoring, caching, retry logic

**Q3: How do you test aspects?** **A:**

```java
@SpringBootTest
class AspectTest {
    @Autowired
    UserService userService;
    
    @Test
    void testLoggingAspect() {
        // Aspect will be applied automatically
        userService.findUser(1L);
        // Verify aspect behavior through side effects
    }
}
```

---

## Part 2: Spring in Business Layer

### Chapter 4: Database Access

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**DAO Philosophy**|• Consistent exception hierarchy<br>• Technology-agnostic interfaces<br>• Resource management abstraction<br>• Template method pattern|
|**DataAccessException**|• Unchecked exception hierarchy<br>• Consistent across data access technologies<br>• Translates vendor-specific exceptions<br>• Enables technology-agnostic DAO layer|
|**DataSource Types**|• **DriverManagerDataSource**: Simple, no pooling<br>• **BasicDataSource**: Apache DBCP pooling<br>• **ComboPooledDataSource**: C3P0 pooling<br>• **HikariDataSource**: High-performance pooling|
|**JdbcTemplate**|• Simplifies JDBC usage<br>• Handles resource management<br>• Translates SQLExceptions<br>• Thread-safe after configuration|
|**ORM Integration**|• **Hibernate**: SessionFactory, HibernateTemplate<br>• **JPA**: EntityManagerFactory, JpaTemplate<br>• **JDO**: PersistenceManagerFactory<br>• **iBATIS/MyBatis**: SqlMapClient<br>• **OJB**: PersistenceBroker|

#### Code Examples

```java
// JDBC Template Example
@Repository
public class JdbcUserRepository implements UserRepository {
    private final JdbcTemplate jdbcTemplate;
    private final NamedParameterJdbcTemplate namedTemplate;
    
    @Autowired
    public JdbcUserRepository(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.namedTemplate = new NamedParameterJdbcTemplate(dataSource);
    }
    
    // Simple query with RowMapper
    public User findById(Long id) {
        String sql = "SELECT * FROM users WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, new UserRowMapper());
    }
    
    // Query with lambda RowMapper
    public List<User> findAll() {
        return jdbcTemplate.query(
            "SELECT * FROM users",
            (rs, rowNum) -> User.builder()
                .id(rs.getLong("id"))
                .username(rs.getString("username"))
                .email(rs.getString("email"))
                .createdAt(rs.getTimestamp("created_at").toLocalDateTime())
                .build()
        );
    }
    
    // Named parameters
    public List<User> findByStatus(String status) {
        String sql = "SELECT * FROM users WHERE status = :status";
        Map<String, Object> params = new HashMap<>();
        params.put("status", status);
        return namedTemplate.query(sql, params, new UserRowMapper());
    }
    
    // Batch update
    public void batchUpdate(List<User> users) {
        String sql = "UPDATE users SET email = ?, updated_at = ? WHERE id = ?";
        
        jdbcTemplate.batchUpdate(sql, new BatchPreparedStatementSetter() {
            @Override
            public void setValues(PreparedStatement ps, int i) throws SQLException {
                User user = users.get(i);
                ps.setString(1, user.getEmail());
                ps.setTimestamp(2, Timestamp.valueOf(LocalDateTime.now()));
                ps.setLong(3, user.getId());
            }
            
            @Override
            public int getBatchSize() {
                return users.size();
            }
        });
    }
    
    // Using SimpleJdbcInsert for auto-generated keys
    public Long insert(User user) {
        SimpleJdbcInsert insert = new SimpleJdbcInsert(jdbcTemplate)
            .withTableName("users")
            .usingGeneratedKeyColumns("id");
        
        Map<String, Object> params = new HashMap<>();
        params.put("username", user.getUsername());
        params.put("email", user.getEmail());
        params.put("created_at", Timestamp.valueOf(LocalDateTime.now()));
        
        return insert.executeAndReturnKey(params).longValue();
    }
    
    // Custom RowMapper
    private static class UserRowMapper implements RowMapper<User> {
        @Override
        public User mapRow(ResultSet rs, int rowNum) throws SQLException {
            return User.builder()
                .id(rs.getLong("id"))
                .username(rs.getString("username"))
                .email(rs.getString("email"))
                .build();
        }
    }
}

// Hibernate Integration Example
@Repository
public class HibernateUserRepository extends HibernateDaoSupport implements UserRepository {
    
    @Autowired
    public HibernateUserRepository(SessionFactory sessionFactory) {
        setSessionFactory(sessionFactory);
    }
    
    public User findById(Long id) {
        return getHibernateTemplate().get(User.class, id);
    }
    
    public List<User> findByEmail(String email) {
        return (List<User>) getHibernateTemplate().find(
            "FROM User u WHERE u.email = ?", email
        );
    }
    
    public void save(User user) {
        getHibernateTemplate().saveOrUpdate(user);
    }
    
    // Using native Hibernate Session
    public List<User> findActiveUsers() {
        return getHibernateTemplate().execute(session -> {
            Query query = session.createQuery("FROM User u WHERE u.active = true");
            query.setMaxResults(100);
            return query.list();
        });
    }
}

// JPA Example
@Repository
public class JpaUserRepository {
    
    @PersistenceContext
    private EntityManager entityManager;
    
    public User findById(Long id) {
        return entityManager.find(User.class, id);
    }
    
    public List<User> findByUsername(String username) {
        TypedQuery<User> query = entityManager.createQuery(
            "SELECT u FROM User u WHERE u.username = :username", 
            User.class
        );
        query.setParameter("username", username);
        return query.getResultList();
    }
    
    @Transactional
    public void save(User user) {
        if (user.getId() == null) {
            entityManager.persist(user);
        } else {
            entityManager.merge(user);
        }
    }
    
    // Using Criteria API
    public List<User> findByCriteria(String email, Boolean active) {
        CriteriaBuilder cb = entityManager.getCriteriaBuilder();
        CriteriaQuery<User> query = cb.createQuery(User.class);
        Root<User> root = query.from(User.class);
        
        List<Predicate> predicates = new ArrayList<>();
        if (email != null) {
            predicates.add(cb.equal(root.get("email"), email));
        }
        if (active != null) {
            predicates.add(cb.equal(root.get("active"), active));
        }
        
        query.where(predicates.toArray(new Predicate[0]));
        return entityManager.createQuery(query).getResultList();
    }
}

// MyBatis Example
@Repository
public class MyBatisUserRepository {
    
    @Autowired
    private SqlMapClient sqlMapClient;
    
    public User findById(Long id) throws SQLException {
        return (User) sqlMapClient.queryForObject("User.findById", id);
    }
    
    public List<User> findAll() throws SQLException {
        return sqlMapClient.queryForList("User.findAll");
    }
    
    public void insert(User user) throws SQLException {
        sqlMapClient.insert("User.insert", user);
    }
}
```

#### Chapter 4 Interview Q&A

**Q1: Why use Spring's DataAccessException instead of SQLException?** **A:**

- Unchecked exceptions (no try-catch required)
- Consistent hierarchy across technologies
- More specific exception types
- Vendor-neutral error handling

**Q2: When would you choose JdbcTemplate over ORM?** **A:**

- Complex queries with specific SQL
- Stored procedures
- Performance-critical operations
- Legacy database schemas
- Reporting queries

**Q3: How do you handle connection pooling in Spring?** **A:**

```java
@Bean
public DataSource dataSource() {
    HikariConfig config = new HikariConfig();
    config.setJdbcUrl("jdbc:mysql://localhost/db");
    config.setUsername("user");
    config.setPassword("pass");
    config.setMaximumPoolSize(10);
    config.setMinimumIdle(5);
    config.setConnectionTimeout(30000);
    return new HikariDataSource(config);
}
```

**Q4: What's the N+1 problem and how to solve it?** **A:**

- Loading collection causes N additional queries
- Solutions: Eager fetching, JOIN FETCH, batch size
- Example: `@Fetch(FetchMode.JOIN)` or `@BatchSize(size=10)`

---

### Chapter 5: Transaction Management

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Transaction Attributes**|• **Propagation**: How transactions relate<br>• **Isolation**: Concurrent access behavior<br>• **Timeout**: Maximum duration<br>• **Read-only**: Optimization hint<br>• **Rollback rules**: Exception handling|
|**Propagation Levels**|• **REQUIRED**: Join or create (default)<br>• **REQUIRES_NEW**: Always new transaction<br>• **SUPPORTS**: Use if exists<br>• **MANDATORY**: Must have existing<br>• **NOT_SUPPORTED**: Suspend if exists<br>• **NEVER**: Fail if exists<br>• **NESTED**: Savepoint-based nesting|
|**Isolation Levels**|• **DEFAULT**: Database default<br>• **READ_UNCOMMITTED**: Dirty reads<br>• **READ_COMMITTED**: No dirty reads<br>• **REPEATABLE_READ**: No phantom reads<br>• **SERIALIZABLE**: Full isolation|
|**Transaction Managers**|• **DataSourceTransactionManager**: JDBC<br>• **HibernateTransactionManager**: Hibernate<br>• **JpaTransactionManager**: JPA<br>• **JtaTransactionManager**: Distributed|
|**Declaration Methods**|• **Programmatic**: TransactionTemplate<br>• **Declarative**: @Transactional<br>• **XML**: tx:advice<br>• **AspectJ**: Compile-time weaving|

#### Code Examples

```java
// Declarative Transaction Management
@Service
@Transactional // Class-level default
public class AccountService {
    
    @Autowired
    private AccountRepository accountRepository;
    
    @Autowired
    private TransactionHistoryRepository historyRepository;
    
    // Uses class-level @Transactional settings
    public Account findById(Long id) {
        return accountRepository.findById(id);
    }
    
    // Custom transaction settings
    @Transactional(
        propagation = Propagation.REQUIRED,
        isolation = Isolation.READ_COMMITTED,
        timeout = 30,
        readOnly = false,
        rollbackFor = Exception.class,
        noRollbackFor = BusinessException.class
    )
    public void transfer(Long fromId, Long toId, BigDecimal amount) 
            throws InsufficientFundsException {
        
        Account from = accountRepository.findById(fromId);
        Account to = accountRepository.findById(toId);
        
        if (from.getBalance().compareTo(amount) < 0) {
            throw new InsufficientFundsException("Insufficient funds");
        }
        
        from.setBalance(from.getBalance().subtract(amount));
        to.setBalance(to.getBalance().add(amount));
        
        accountRepository.save(from);
        accountRepository.save(to);
        
        // Audit in separate transaction
        auditTransfer(fromId, toId, amount);
    }
    
    // Always runs in new transaction
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void auditTransfer(Long fromId, Long toId, BigDecimal amount) {
        TransactionHistory history = new TransactionHistory();
        history.setFromAccount(fromId);
        history.setToAccount(toId);
        history.setAmount(amount);
        history.setTimestamp(LocalDateTime.now());
        historyRepository.save(history);
    }
    
    // Nested transaction with savepoint
    @Transactional(propagation = Propagation.NESTED)
    public void updateAccountStatus(Long accountId, String status) {
        try {
            Account account = accountRepository.findById(accountId);
            account.setStatus(status);
            accountRepository.save(account);
            
            // May fail but won't rollback outer transaction
            notifyStatusChange(accountId, status);
        } catch (Exception e) {
            // Handle nested transaction failure
            log.error("Failed to update status", e);
        }
    }
    
    // Read-only optimization
    @Transactional(readOnly = true)
    public List<Account> findInactiveAccounts() {
        return accountRepository.findByStatus("INACTIVE");
    }
}

// Programmatic Transaction Management
@Service
public class ProgrammaticTransactionService {
    
    @Autowired
    private TransactionTemplate transactionTemplate;
    
    @Autowired
    private AccountRepository accountRepository;
    
    public void performComplexOperation(final Long accountId) {
        // Configure transaction template
        transactionTemplate.setPropagationBehavior(
            TransactionDefinition.PROPAGATION_REQUIRED
        );
        transactionTemplate.setIsolationLevel(
            TransactionDefinition.ISOLATION_SERIALIZABLE
        );
        
        // Execute in transaction
        transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            @Override
            protected void doInTransactionWithoutResult(TransactionStatus status) {
                try {
                    Account account = accountRepository.findById(accountId);
                    
                    // Complex operations
                    processAccount(account);
                    
                    if (shouldRollback(account)) {
                        status.setRollbackOnly();
                    }
                    
                    accountRepository.save(account);
                } catch (Exception e) {
                    status.setRollbackOnly();
                    throw new RuntimeException(e);
                }
            }
        });
    }
    
    // With return value
    public Account createAccount(final String username) {
        return transactionTemplate.execute(status -> {
            Account account = new Account();
            account.setUsername(username);
            account.setBalance(BigDecimal.ZERO);
            account.setCreatedAt(LocalDateTime.now());
            
            return accountRepository.save(account);
        });
    }
}

// XML Configuration for Transactions
/*
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <tx:attributes>
        <tx:method name="find*" read-only="true" timeout="30"/>
        <tx:method name="save*" propagation="REQUIRED"/>
        <tx:method name="update*" propagation="REQUIRED"/>
        <tx:method name="delete*" propagation="REQUIRED"/>
        <tx:method name="*" propagation="SUPPORTS" read-only="true"/>
    </tx:attributes>
</tx:advice>

<aop:config>
    <aop:pointcut id="serviceMethods" 
        expression="execution(* com.example.service.*.*(..))"/>
    <aop:advisor advice-ref="txAdvice" pointcut-ref="serviceMethods"/>
</aop:config>
*/

// Transaction Configuration
@Configuration
@EnableTransactionManagement
public class TransactionConfig {
    
    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource) {
        DataSourceTransactionManager tm = new DataSourceTransactionManager();
        tm.setDataSource(dataSource);
        tm.setGlobalRollbackOnParticipationFailure(false);
        return tm;
    }
    
    @Bean
    public TransactionTemplate transactionTemplate(
            PlatformTransactionManager transactionManager) {
        TransactionTemplate template = new TransactionTemplate();
        template.setTransactionManager(transactionManager);
        template.setIsolationLevel(TransactionDefinition.ISOLATION_READ_COMMITTED);
        template.setTimeout(30);
        return template;
    }
}

// Testing Transactions
@SpringBootTest
@Transactional
@Rollback // Rollback after each test
class TransactionTest {
    
    @Test
    @Commit // Override rollback for this test
    void testTransactionCommit() {
        // Test with actual commit
    }
    
    @Test
    void testTransactionRollback() {
        // Automatically rolled back after test
    }
}
```

#### Chapter 5 Interview Q&A

**Q1: Explain ACID properties with examples.** **A:**

- **Atomicity**: Transfer either completes fully or not at all
- **Consistency**: Account balance can't be negative
- **Isolation**: Concurrent transfers don't interfere
- **Durability**: Committed transfer survives system crash

**Q2: When to use REQUIRES_NEW vs NESTED?** **A:**

- **REQUIRES_NEW**: Independent transaction (audit logs)
- **NESTED**: Can rollback without affecting outer (batch processing)
- REQUIRES_NEW suspends outer, NESTED uses savepoints

**Q3: How do you handle distributed transactions?** **A:**

```java
@Bean
public JtaTransactionManager transactionManager() {
    UserTransaction userTransaction = new UserTransactionImp();
    TransactionManager transactionManager = new TransactionManagerImp();
    return new JtaTransactionManager(userTransaction, transactionManager);
}
```

**Q4: What's the difference between @Transactional on class vs method?** **A:**

- Class-level: Default for all public methods
- Method-level: Overrides class-level settings
- Private methods: Not proxied, annotation ignored
- Interface methods: Applied to all implementations

---

### Chapter 6: Remoting

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Spring Remoting**|• Transparent remote service access<br>• Multiple protocol support<br>• Service exporting and consuming<br>• Exception translation|
|**RMI Support**|• **RmiServiceExporter**: Export beans<br>• **RmiProxyFactoryBean**: Import services<br>• No RemoteException handling needed<br>• Registry management|
|**HTTP Invoker**|• Spring's binary protocol over HTTP<br>• Java serialization<br>• Firewall-friendly<br>• Full object graph support|
|**Hessian/Burlap**|• Binary/XML web services<br>• Language independent<br>• Lightweight protocol<br>• Limited type support|
|**JAX-RPC/JAX-WS**|• Standard web services<br>• SOAP protocol<br>• WSDL support<br>• Interoperable|

#### Code Examples

```java
// RMI Service Interface
public interface UserService extends Remote {
    User findUser(Long id) throws RemoteException;
    List<User> findAllUsers() throws RemoteException;
}

// RMI Service Implementation
@Service("userService")
public class UserServiceImpl implements UserService {
    
    @Autowired
    private UserRepository userRepository;
    
    @Override
    public User findUser(Long id) {
        return userRepository.findById(id);
    }
    
    @Override
    public List<User> findAllUsers() {
        return userRepository.findAll();
    }
}

// RMI Server Configuration
@Configuration
public class RmiServerConfig {
    
    @Bean
    public RmiServiceExporter userServiceExporter(UserService userService) {
        RmiServiceExporter exporter = new RmiServiceExporter();
        exporter.setService(userService);
        exporter.setServiceName("UserService");
        exporter.setServiceInterface(UserService.class);
        exporter.setRegistryPort(1099);
        return exporter;
    }
}

// RMI Client Configuration
@Configuration
public class RmiClientConfig {
    
    @Bean
    public RmiProxyFactoryBean userService() {
        RmiProxyFactoryBean proxy = new RmiProxyFactoryBean();
        proxy.setServiceUrl("rmi://localhost:1099/UserService");
        proxy.setServiceInterface(UserService.class);
        proxy.setLookupStubOnStartup(false);
        proxy.setRefreshStubOnConnectFailure(true);
        return proxy;
    }
}

// HTTP Invoker Server
@Configuration
public class HttpInvokerServerConfig {
    
    @Bean("/userService")
    public HttpInvokerServiceExporter userServiceExporter(UserService userService) {
        HttpInvokerServiceExporter exporter = new HttpInvokerServiceExporter();
        exporter.setService(userService);
        exporter.setServiceInterface(UserService.class);
        return exporter;
    }
}

// HTTP Invoker Client
@Configuration
public class HttpInvokerClientConfig {
    
    @Bean
    public HttpInvokerProxyFactoryBean userService() {
        HttpInvokerProxyFactoryBean proxy = new HttpInvokerProxyFactoryBean();
        proxy.setServiceUrl("http://localhost:8080/services/userService");
        proxy.setServiceInterface(UserService.class);
        
        // Configure HTTP client
        CommonsHttpInvokerRequestExecutor executor = 
            new CommonsHttpInvokerRequestExecutor();
        HttpClient httpClient = new HttpClient();
        httpClient.getParams().setConnectionManagerTimeout(5000);
        executor.setHttpClient(httpClient);
        proxy.setHttpInvokerRequestExecutor(executor);
        
        return proxy;
    }
}

// Hessian Service Configuration
@Configuration
public class HessianConfig {
    
    // Server side
    @Bean("/hessianUserService")
    public HessianServiceExporter hessianExporter(UserService userService) {
        HessianServiceExporter exporter = new HessianServiceExporter();
        exporter.setService(userService);
        exporter.setServiceInterface(UserService.class);
        return exporter;
    }
    
    // Client side
    @Bean
    public HessianProxyFactoryBean hessianUserService() {
        HessianProxyFactoryBean proxy = new HessianProxyFactoryBean();
        proxy.setServiceUrl("http://localhost:8080/services/hessianUserService");
        proxy.setServiceInterface(UserService.class);
        proxy.setOverloadEnabled(true);
        return proxy;
    }
}

// JAX-WS Web Service
@WebService
public interface UserWebService {
    @WebMethod
    UserDTO findUser(@WebParam(name = "id") Long id);
    
    @WebMethod
    List<UserDTO> findAllUsers();
}

@Service
@WebService(endpointInterface = "com.example.UserWebService")
public class UserWebServiceImpl implements UserWebService {
    
    @Autowired
    private UserService userService;
    
    @Override
    public UserDTO findUser(Long id) {
        User user = userService.findUser(id);
        return convertToDTO(user);
    }
    
    @Override
    public List<UserDTO> findAllUsers() {
        return userService.findAllUsers().stream()
            .map(this::convertToDTO)
            .collect(Collectors.toList());
    }
}

// JAX-WS Client Configuration
@Configuration
public class JaxWsClientConfig {
    
    @Bean
    public JaxWsPortProxyFactoryBean userWebService() {
        JaxWsPortProxyFactoryBean proxy = new JaxWsPortProxyFactoryBean();
        proxy.setServiceInterface(UserWebService.class);
        proxy.setWsdlDocumentUrl("http://localhost:8080/services/user?wsdl");
        proxy.setNamespaceUri("http://example.com/");
        proxy.setServiceName("UserWebService");
        proxy.setPortName("UserWebServicePort");
        return proxy;
    }
}

// EJB Integration
@Configuration
public class EjbConfig {
    
    // Local EJB
    @Bean
    public LocalStatelessSessionProxyFactoryBean localUserService() {
        LocalStatelessSessionProxyFactoryBean proxy = 
            new LocalStatelessSessionProxyFactoryBean();
        proxy.setJndiName("java:comp/env/ejb/UserService");
        proxy.setBusinessInterface(UserService.class);
        return proxy;
    }
    
    // Remote EJB
    @Bean
    public SimpleRemoteStatelessSessionProxyFactoryBean remoteUserService() {
        SimpleRemoteStatelessSessionProxyFactoryBean proxy = 
            new SimpleRemoteStatelessSessionProxyFactoryBean();
        proxy.setJndiName("ejb/UserService");
        proxy.setBusinessInterface(UserService.class);
        proxy.setHomeInterface(UserServiceHome.class);
        return proxy;
    }
}
```

#### Chapter 6 Interview Q&A

**Q1: When would you choose HTTP Invoker over RMI?** **A:**

- HTTP Invoker works through firewalls
- Uses standard HTTP ports
- Better for internet communication
- RMI better for intranet with full control

**Q2: What are the limitations of Hessian?** **A:**

- Limited type system (no custom serialization)
- No transaction context propagation
- Binary protocol may have firewall issues
- Good for simple cross-language services

**Q3: How do you handle remote service failures?** **A:**

```java
@Bean
public RmiProxyFactoryBean userService() {
    RmiProxyFactoryBean proxy = new RmiProxyFactoryBean();
    proxy.setRefreshStubOnConnectFailure(true);
    proxy.setCacheStub(false);
    // Add retry logic with Spring Retry
    return proxy;
}
```

---

### Chapter 7: Enterprise Services

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**JNDI Integration**|• **JndiObjectFactoryBean**: JNDI lookups<br>• **JndiTemplate**: Simplified JNDI access<br>• Resource caching<br>• Environment abstraction|
|**Email Support**|• **JavaMailSender**: Mail abstraction<br>• **SimpleMailMessage**: Text emails<br>• **MimeMessage**: HTML/attachments<br>• Template support|
|**Task Scheduling**|• **TaskScheduler**: Scheduling abstraction<br>• Timer/TimerTask support<br>• Quartz integration<br>• @Scheduled annotation|
|**JMS Support**|• **JmsTemplate**: Message operations<br>• **MessageListener**: Async consumption<br>• **MessageConverter**: Object conversion<br>• Transaction support|

#### Code Examples

```java
// JNDI Configuration
@Configuration
public class JndiConfig {
    
    @Bean
    public JndiObjectFactoryBean dataSource() {
        JndiObjectFactoryBean jndi = new JndiObjectFactoryBean();
        jndi.setJndiName("java:comp/env/jdbc/myDataSource");
        jndi.setResourceRef(true);
        jndi.setLookupOnStartup(false);
        jndi.setCache(true);
        jndi.setProxyInterface(DataSource.class);
        return jndi;
    }
    
    @Bean
    public JndiTemplate jndiTemplate() {
        Properties props = new Properties();
        props.setProperty(Context.INITIAL_CONTEXT_FACTORY, 
            "com.sun.jndi.ldap.LdapCtxFactory");
        props.setProperty(Context.PROVIDER_URL, "ldap://localhost:389");
        return new JndiTemplate(props);
    }
}

// Email Service
@Service
public class EmailService {
    
    @Autowired
    private JavaMailSender mailSender;
    
    @Autowired
    private TemplateEngine templateEngine;
    
    @Value("${mail.from}")
    private String fromAddress;
    
    // Simple text email
    public void sendSimpleEmail(String to, String subject, String text) {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setFrom(fromAddress);
        message.setTo(to);
        message.setSubject(subject);
        message.setText(text);
        message.setSentDate(new Date());
        
        mailSender.send(message);
    }
    
    // HTML email with attachments
    public void sendHtmlEmail(String to, String subject, 
                             Map<String, Object> templateModel,
                             File attachment) throws MessagingException {
        
        MimeMessage message = mailSender.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(message, true, "UTF-8");
        
        helper.setFrom(fromAddress);
        helper.setTo(to);
        helper.setSubject(subject);
        
        // Process template
        Context context = new Context();
        context.setVariables(templateModel);
        String htmlContent = templateEngine.process("email-template", context);
        helper.setText(htmlContent, true);
        
        // Add attachment
        if (attachment != null) {
            helper.addAttachment(attachment.getName(), attachment);
        }
        
        // Add inline image
        ClassPathResource image = new ClassPathResource("logo.png");
        helper.addInline("logo", image);
        
        mailSender.send(message);
    }
    
    // Batch email sending
    public void sendBatchEmails(List<EmailMessage> messages) {
        MimeMessage[] mimeMessages = new MimeMessage[messages.size()];
        
        for (int i = 0; i < messages.size(); i++) {
            mimeMessages[i] = createMimeMessage(messages.get(i));
        }
        
        mailSender.send(mimeMessages);
    }
}

// Task Scheduling
@Configuration
@EnableScheduling
public class SchedulingConfig {
    
    @Bean
    public TaskScheduler taskScheduler() {
        ThreadPoolTaskScheduler scheduler = new ThreadPoolTaskScheduler();
        scheduler.setPoolSize(10);
        scheduler.setThreadNamePrefix("scheduled-");
        scheduler.setWaitForTasksToCompleteOnShutdown(true);
        scheduler.setAwaitTerminationSeconds(60);
        return scheduler;
    }
}

@Component
public class ScheduledTasks {
    
    // Fixed rate - every 5 seconds
    @Scheduled(fixedRate = 5000)
    public void reportCurrentTime() {
        System.out.println("Current time: " + new Date());
    }
    
    // Fixed delay - 5 seconds after completion
    @Scheduled(fixedDelay = 5000, initialDelay = 10000)
    public void processData() {
        System.out.println("Processing data...");
    }
    
    // Cron expression - every day at 2 AM
    @Scheduled(cron = "0 0 2 * * ?")
    public void dailyCleanup() {
        System.out.println("Running daily cleanup");
    }
    
    // Dynamic scheduling
    @Autowired
    private TaskScheduler taskScheduler;
    
    public void scheduleTask(Runnable task, Date startTime) {
        taskScheduler.schedule(task, startTime);
    }
    
    public void scheduleRecurringTask(Runnable task, long period) {
        taskScheduler.scheduleAtFixedRate(task, period);
    }
}

// Quartz Integration
@Configuration
public class QuartzConfig {
    
    @Bean
    public JobDetailFactoryBean userSyncJob() {
        JobDetailFactoryBean factory = new JobDetailFactoryBean();
        factory.setJobClass(UserSyncJob.class);
        factory.setDurability(true);
        factory.setDescription("Sync users from external system");
        return factory;
    }
    
    @Bean
    public SimpleTriggerFactoryBean userSyncTrigger(JobDetail userSyncJob) {
        SimpleTriggerFactoryBean trigger = new SimpleTriggerFactoryBean();
        trigger.setJobDetail(userSyncJob);
        trigger.setRepeatInterval(3600000); // 1 hour
        trigger.setStartDelay(5000);
        return trigger;
    }
    
    @Bean
    public CronTriggerFactoryBean reportTrigger(JobDetail reportJob) {
        CronTriggerFactoryBean trigger = new CronTriggerFactoryBean();
        trigger.setJobDetail(reportJob);
        trigger.setCronExpression("0 0 6 * * MON-FRI"); // 6 AM weekdays
        return trigger;
    }
    
    @Bean
    public SchedulerFactoryBean scheduler(Trigger... triggers) {
        SchedulerFactoryBean scheduler = new SchedulerFactoryBean();
        scheduler.setTriggers(triggers);
        scheduler.setAutoStartup(true);
        scheduler.setApplicationContextSchedulerContextKey("applicationContext");
        return scheduler;
    }
}

@Component
public class UserSyncJob extends QuartzJobBean {
    
    @Autowired
    private UserService userService;
    
    @Override
    protected void executeInternal(JobExecutionContext context) {
        System.out.println("Executing user sync at " + new Date());
        userService.syncUsers();
    }
}

// JMS Configuration and Usage
@Configuration
@EnableJms
public class JmsConfig {
    
    @Bean
    public ConnectionFactory connectionFactory() {
        ActiveMQConnectionFactory factory = new ActiveMQConnectionFactory();
        factory.setBrokerURL("tcp://localhost:61616");
        return factory;
    }
    
    @Bean
    public JmsTemplate jmsTemplate(ConnectionFactory connectionFactory) {
        JmsTemplate template = new JmsTemplate();
        template.setConnectionFactory(connectionFactory);
        template.setDefaultDestinationName("user.queue");
        template.setReceiveTimeout(10000);
        template.setMessageConverter(jacksonMessageConverter());
        return template;
    }
    
    @Bean
    public MessageConverter jacksonMessageConverter() {
        MappingJackson2MessageConverter converter = 
            new MappingJackson2MessageConverter();
        converter.setTargetType(MessageType.TEXT);
        converter.setTypeIdPropertyName("_type");
        return converter;
    }
    
    @Bean
    public DefaultJmsListenerContainerFactory jmsListenerContainerFactory(
            ConnectionFactory connectionFactory) {
        DefaultJmsListenerContainerFactory factory = 
            new DefaultJmsListenerContainerFactory();
        factory.setConnectionFactory(connectionFactory);
        factory.setConcurrency("3-10");
        factory.setMessageConverter(jacksonMessageConverter());
        return factory;
    }
}

@Service
public class JmsMessageService {
    
    @Autowired
    private JmsTemplate jmsTemplate;
    
    // Send simple message
    public void sendMessage(String destination, String message) {
        jmsTemplate.convertAndSend(destination, message);
    }
    
    // Send object message
    public void sendUserMessage(User user) {
        jmsTemplate.convertAndSend("user.queue", user);
    }
    
    // Send with post processor
    public void sendPriorityMessage(String message, final int priority) {
        jmsTemplate.convertAndSend("priority.queue", message, 
            new MessagePostProcessor() {
                @Override
                public Message postProcessMessage(Message message) throws JMSException {
                    message.setJMSPriority(priority);
                    message.setStringProperty("type", "urgent");
                    return message;
                }
            });
    }
    
    // Receive message
    public String receiveMessage(String destination) {
        return (String) jmsTemplate.receiveAndConvert(destination);
    }
}

@Component
public class JmsMessageListener {
    
    @JmsListener(destination = "user.queue")
    public void processUser(User user) {
        System.out.println("Received user: " + user);
        // Process user
    }
    
    @JmsListener(destination = "order.queue", containerFactory = "jmsListenerContainerFactory")
    @SendTo("order.processed.queue")
    public OrderResult processOrder(Order order) {
        System.out.println("Processing order: " + order);
        // Process and return result
        return new OrderResult(order.getId(), "PROCESSED");
    }
    
    @JmsListener(destination = "error.queue")
    public void handleError(Message message) throws JMSException {
        System.err.println("Error message: " + message.getBody(String.class));
    }
}
```

#### Chapter 7 Interview Q&A

**Q1: How do you handle email template processing?** **A:**

- Use template engines (Thymeleaf, Velocity, FreeMarker)
- Separate content from code
- Support i18n for multi-language
- Cache compiled templates

**Q2: What's the difference between @Scheduled and Quartz?** **A:**

- **@Scheduled**: Simple, annotation-based, in-memory
- **Quartz**: Complex scheduling, persistent, clustering
- Use @Scheduled for simple tasks, Quartz for enterprise

**Q3: How do you ensure JMS message reliability?** **A:**

```java
@JmsListener(destination = "critical.queue")
@Transactional
public void processMessage(Message message) {
    // Process in transaction
    // Auto-acknowledge on success
    // Rollback redelivers message
}
```

**Q4: How do you implement retry logic for failed tasks?** **A:**

```java
@Retryable(maxAttempts = 3, backoff = @Backoff(delay = 1000))
public void sendEmail(String to, String subject) {
    // Will retry 3 times with 1 second delay
}
```

---

## Part 3: Spring in Web Layer

### Chapter 8: Building Web Layer

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Spring MVC Flow**|1. Request → DispatcherServlet<br>2. HandlerMapping selection<br>3. Controller execution<br>4. ModelAndView return<br>5. ViewResolver resolution<br>6. View rendering<br>7. Response|
|**DispatcherServlet**|• Front controller pattern<br>• Delegates to components<br>• WebApplicationContext<br>• Servlet configuration|
|**HandlerMapping**|• Maps URLs to handlers<br>• Multiple strategies<br>• Chain of mappings<br>• Interceptor support|
|**Controllers**|• @Controller annotation<br>• Request handling methods<br>• Model population<br>• View selection|
|**View Resolution**|• Logical view names<br>• ViewResolver chain<br>• Content negotiation<br>• Multiple view technologies|

#### Code Examples

```java
// Web Configuration
@Configuration
@EnableWebMvc
@ComponentScan("com.example.web")
public class WebConfig implements WebMvcConfigurer {
    
    @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
        registry.jsp("/WEB-INF/views/", ".jsp");
    }
    
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/resources/**")
                .addResourceLocations("/resources/");
    }
    
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoggingInterceptor());
        registry.addInterceptor(new AuthenticationInterceptor())
                .addPathPatterns("/secure/**");
    }
    
    @Override
    public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {
        converters.add(new MappingJackson2HttpMessageConverter());
    }
    
    @Bean
    public InternalResourceViewResolver viewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        resolver.setOrder(2);
        return resolver;
    }
    
    @Bean
    public BeanNameViewResolver beanNameViewResolver() {
        BeanNameViewResolver resolver = new BeanNameViewResolver();
        resolver.setOrder(1);
        return resolver;
    }
}

// Controller Examples
@Controller
@RequestMapping("/users")
public class UserController {
    
    @Autowired
    private UserService userService;
    
    // Simple GET mapping
    @GetMapping
    public String listUsers(Model model) {
        model.addAttribute("users", userService.findAll());
        return "users/list"; // Logical view name
    }
    
    // Path variable
    @GetMapping("/{id}")
    public String showUser(@PathVariable Long id, Model model) {
        User user = userService.findById(id);
        if (user == null) {
            throw new ResourceNotFoundException("User not found");
        }
        model.addAttribute("user", user);
        return "users/show";
    }
    
    // Form display
    @GetMapping("/new")
    public String newUserForm(Model model) {
        model.addAttribute("user", new User());
        model.addAttribute("roles", Role.values());
        return "users/form";
    }
    
    // Form submission
    @PostMapping
    public String createUser(@Valid @ModelAttribute User user, 
                            BindingResult result,
                            RedirectAttributes redirectAttrs) {
        if (result.hasErrors()) {
            return "users/form";
        }
        
        User saved = userService.save(user);
        redirectAttrs.addFlashAttribute("message", "User created successfully");
        return "redirect:/users/" + saved.getId();
    }
    
    // Request parameters
    @GetMapping("/search")
    public String searchUsers(@RequestParam(required = false) String query,
                             @RequestParam(defaultValue = "0") int page,
                             @RequestParam(defaultValue = "10") int size,
                             Model model) {
        Page<User> users = userService.search(query, page, size);
        model.addAttribute("users", users);
        model.addAttribute("query", query);
        return "users/search";
    }
    
    // Multiple request methods
    @RequestMapping(value = "/{id}/edit", method = {RequestMethod.GET, RequestMethod.POST})
    public String editUser(@PathVariable Long id,
                          @ModelAttribute User user,
                          BindingResult result,
                          Model model) {
        if (RequestMethod.GET.equals(request.getMethod())) {
            model.addAttribute("user", userService.findById(id));
            return "users/edit";
        } else {
            if (result.hasErrors()) {
                return "users/edit";
            }
            userService.update(user);
            return "redirect:/users/" + id;
        }
    }
    
    // Session attributes
    @GetMapping("/wizard")
    @SessionAttributes("userForm")
    public String startWizard(Model model) {
        model.addAttribute("userForm", new UserForm());
        return "users/wizard-step1";
    }
    
    // Model attribute method
    @ModelAttribute("currentUser")
    public User getCurrentUser(Principal principal) {
        return userService.findByUsername(principal.getName());
    }
    
    // Exception handler
    @ExceptionHandler(ResourceNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public String handleNotFound(ResourceNotFoundException ex, Model model) {
        model.addAttribute("error", ex.getMessage());
        return "errors/404";
    }
}

// REST Controller
@RestController
@RequestMapping("/api/users")
public class UserRestController {
    
    @Autowired
    private UserService userService;
    
    @GetMapping
    public List<User> getAllUsers() {
        return userService.findAll();
    }
    
    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        User user = userService.findById(id);
        if (user == null) {
            return ResponseEntity.notFound().build();
        }
        return ResponseEntity.ok(user);
    }
    
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public User createUser(@Valid @RequestBody User user) {
        return userService.save(user);
    }
    
    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, 
                          @Valid @RequestBody User user) {
        user.setId(id);
        return userService.update(user);
    }
    
    @DeleteMapping("/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void deleteUser(@PathVariable Long id) {
        userService.delete(id);
    }
    
    // Content negotiation
    @GetMapping(value = "/{id}", produces = {MediaType.APPLICATION_JSON_VALUE, 
                                             MediaType.APPLICATION_XML_VALUE})
    public User getUserNegotiated(@PathVariable Long id) {
        return userService.findById(id);
    }
}

// Form Controller with Validation
@Controller
@RequestMapping("/register")
public class RegistrationController {
    
    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.setDisallowedFields("id");
        binder.registerCustomEditor(Date.class, 
            new CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd"), false));
    }
    
    @GetMapping
    public String showForm(Model model) {
        model.addAttribute("registration", new Registration());
        return "register/form";
    }
    
    @PostMapping
    public String processRegistration(
            @Valid @ModelAttribute Registration registration,
            BindingResult result,
            Model model) {
        
        // Custom validation
        if (userService.existsByEmail(registration.getEmail())) {
            result.rejectValue("email", "duplicate", "Email already exists");
        }
        
        if (result.hasErrors()) {
            return "register/form";
        }
        
        userService.register(registration);
        return "redirect:/register/success";
    }
}

// Multi-action Controller
@Controller
@RequestMapping("/admin")
public class AdminController extends MultiActionController {
    
    @RequestMapping("/dashboard")
    public ModelAndView dashboard(HttpServletRequest request) {
        ModelAndView mav = new ModelAndView("admin/dashboard");
        mav.addObject("stats", adminService.getStatistics());
        return mav;
    }
    
    @RequestMapping(value = "/users", params = "action=list")
    public ModelAndView listUsers() {
        return new ModelAndView("admin/users", "users", userService.findAll());
    }
    
    @RequestMapping(value = "/users", params = "action=export")
    public void exportUsers(HttpServletResponse response) throws IOException {
        response.setContentType("text/csv");
        response.setHeader("Content-Disposition", "attachment; filename=users.csv");
        
        PrintWriter writer = response.getWriter();
        userService.exportToCsv(writer);
    }
}

// Interceptor Example
public class AuthenticationInterceptor implements HandlerInterceptor {
    
    @Override
    public boolean preHandle(HttpServletRequest request, 
                           HttpServletResponse response, 
                           Object handler) throws Exception {
        HttpSession session = request.getSession();
        if (session.getAttribute("user") == null) {
            response.sendRedirect("/login");
            return false;
        }
        return true;
    }
    
    @Override
    public void postHandle(HttpServletRequest request, 
                          HttpServletResponse response, 
                          Object handler, 
                          ModelAndView modelAndView) throws Exception {
        if (modelAndView != null) {
            modelAndView.addObject("currentTime", new Date());
        }
    }
    
    @Override
    public void afterCompletion(HttpServletRequest request, 
                               HttpServletResponse response, 
                               Object handler, 
                               Exception ex) throws Exception {
        // Cleanup resources
    }
}
```

#### Chapter 8 Interview Q&A

**Q1: Explain the Spring MVC request flow in detail.** **A:**

1. Request arrives at DispatcherServlet
2. DispatcherServlet queries HandlerMapping for controller
3. HandlerMapping returns HandlerExecutionChain
4. DispatcherServlet calls HandlerAdapter
5. HandlerAdapter invokes controller
6. Controller returns ModelAndView
7. DispatcherServlet passes to ViewResolver
8. ViewResolver returns View
9. DispatcherServlet renders View
10. Response sent to client

**Q2: How do you handle file uploads in Spring MVC?** **A:**

```java
@PostMapping("/upload")
public String handleFileUpload(@RequestParam("file") MultipartFile file) {
    if (!file.isEmpty()) {
        byte[] bytes = file.getBytes();
        // Process file
    }
    return "success";
}
```

**Q3: What's the difference between @RequestParam and @PathVariable?** **A:**

- **@RequestParam**: Query parameters (?name=value)
- **@PathVariable**: URL path segments (/users/{id})
- RequestParam can be optional, PathVariable cannot

**Q4: How do you implement global exception handling?** **A:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(Exception.class)
    public ModelAndView handleException(Exception e) {
        ModelAndView mav = new ModelAndView("error");
        mav.addObject("exception", e);
        return mav;
    }
}
```

---

### Chapter 9: View Layer Alternatives

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**View Technologies**|• JSP: Traditional Java views<br>• Velocity: Simple template syntax<br>• FreeMarker: Powerful templating<br>• Thymeleaf: Natural templates<br>• Tiles: Composite views|
|**Template Configuration**|• View resolver setup<br>• Template location<br>• Encoding settings<br>• Cache configuration|
|**Document Generation**|• PDF with iText<br>• Excel with Apache POI<br>• CSV generation<br>• JSON/XML views|
|**Content Negotiation**|• Accept header based<br>• URL extension based<br>• Parameter based<br>• Custom strategies|

#### Code Examples

```java
// Velocity Configuration
@Configuration
public class VelocityConfig {
    
    @Bean
    public VelocityConfigurer velocityConfigurer() {
        VelocityConfigurer configurer = new VelocityConfigurer();
        configurer.setResourceLoaderPath("/WEB-INF/velocity/");
        configurer.setVelocityProperties(velocityProperties());
        return configurer;
    }
    
    private Properties velocityProperties() {
        Properties props = new Properties();
        props.setProperty("input.encoding", "UTF-8");
        props.setProperty("output.encoding", "UTF-8");
        props.setProperty("velocimacro.library.autoreload", "true");
        props.setProperty("directive.foreach.counter.initial.value", "0");
        return props;
    }
    
    @Bean
    public VelocityViewResolver velocityViewResolver() {
        VelocityViewResolver resolver = new VelocityViewResolver();
        resolver.setPrefix("");
        resolver.setSuffix(".vm");
        resolver.setContentType("text/html;charset=UTF-8");
        resolver.setExposeSpringMacroHelpers(true);
        resolver.setExposeRequestAttributes(true);
        resolver.setExposeSessionAttributes(true);
        return resolver;
    }
}

// FreeMarker Configuration
@Configuration
public class FreeMarkerConfig {
    
    @Bean
    public FreeMarkerConfigurer freeMarkerConfigurer() {
        FreeMarkerConfigurer configurer = new FreeMarkerConfigurer();
        configurer.setTemplateLoaderPath("/WEB-INF/freemarker/");
        configurer.setDefaultEncoding("UTF-8");
        
        Properties settings = new Properties();
        settings.setProperty("template_update_delay", "0");
        settings.setProperty("default_encoding", "UTF-8");
        settings.setProperty("number_format", "0.##");
        settings.setProperty("datetime_format", "yyyy-MM-dd HH:mm:ss");
        configurer.setFreemarkerSettings(settings);
        
        Map<String, Object> variables = new HashMap<>();
        variables.put("xml_escape", new XmlEscape());
        configurer.setFreemarkerVariables(variables);
        
        return configurer;
    }
    
    @Bean
    public FreeMarkerViewResolver freeMarkerViewResolver() {
        FreeMarkerViewResolver resolver = new FreeMarkerViewResolver();
        resolver.setPrefix("");
        resolver.setSuffix(".ftl");
        resolver.setContentType("text/html;charset=UTF-8");
        resolver.setCache(false);
        resolver.setExposeSpringMacroHelpers(true);
        return resolver;
    }
}

// Thymeleaf Configuration
@Configuration
public class ThymeleafConfig {
    
    @Bean
    public SpringResourceTemplateResolver templateResolver() {
        SpringResourceTemplateResolver resolver = new SpringResourceTemplateResolver();
        resolver.setPrefix("/WEB-INF/templates/");
        resolver.setSuffix(".html");
        resolver.setTemplateMode(TemplateMode.HTML);
        resolver.setCacheable(false);
        resolver.setCharacterEncoding("UTF-8");
        return resolver;
    }
    
    @Bean
    public SpringTemplateEngine templateEngine(SpringResourceTemplateResolver resolver) {
        SpringTemplateEngine engine = new SpringTemplateEngine();
        engine.setTemplateResolver(resolver);
        engine.setEnableSpringELCompiler(true);
        
        // Add custom dialect
        engine.addDialect(new LayoutDialect());
        
        return engine;
    }
    
    @Bean
    public ThymeleafViewResolver thymeleafViewResolver(SpringTemplateEngine engine) {
        ThymeleafViewResolver resolver = new ThymeleafViewResolver();
        resolver.setTemplateEngine(engine);
        resolver.setCharacterEncoding("UTF-8");
        resolver.setContentType("text/html;charset=UTF-8");
        return resolver;
    }
}

// Tiles Configuration
@Configuration
public class TilesConfig {
    
    @Bean
    public TilesConfigurer tilesConfigurer() {
        TilesConfigurer configurer = new TilesConfigurer();
        configurer.setDefinitions("/WEB-INF/tiles/tiles.xml");
        configurer.setCheckRefresh(true);
        return configurer;
    }
    
    @Bean
    public TilesViewResolver tilesViewResolver() {
        TilesViewResolver resolver = new TilesViewResolver();
        resolver.setOrder(1);
        return resolver;
    }
}

// PDF Generation View
public class UserPdfView extends AbstractPdfView {
    
    @Override
    protected void buildPdfDocument(Map<String, Object> model, 
                                   Document document, 
                                   PdfWriter writer, 
                                   HttpServletRequest request, 
                                   HttpServletResponse response) throws Exception {
        
        List<User> users = (List<User>) model.get("users");
        
        // Document metadata
        document.addTitle("User Report");
        document.addAuthor("Spring Application");
        document.addCreationDate();
        
        // Add content
        Font titleFont = FontFactory.getFont(FontFactory.HELVETICA_BOLD, 18);
        Paragraph title = new Paragraph("User Report", titleFont);
        title.setAlignment(Element.ALIGN_CENTER);
        document.add(title);
        
        document.add(new Paragraph(" "));
        
        // Create table
        PdfPTable table = new PdfPTable(4);
        table.setWidthPercentage(100);
        table.setWidths(new float[]{1, 3, 3, 2});
        
        // Headers
        addTableHeader(table, "ID", "Username", "Email", "Status");
        
        // Data rows
        for (User user : users) {
            table.addCell(String.valueOf(user.getId()));
            table.addCell(user.getUsername());
            table.addCell(user.getEmail());
            table.addCell(user.getStatus());
        }
        
        document.add(table);
    }
    
    private void addTableHeader(PdfPTable table, String... headers) {
        Font headerFont = FontFactory.getFont(FontFactory.HELVETICA_BOLD);
        for (String header : headers) {
            PdfPCell cell = new PdfPCell(new Phrase(header, headerFont));
            cell.setBackgroundColor(BaseColor.LIGHT_GRAY);
            cell.setHorizontalAlignment(Element.ALIGN_CENTER);
            table.addCell(cell);
        }
    }
}

// Excel Generation View
public class UserExcelView extends AbstractXlsxView {
    
    @Override
    protected void buildExcelDocument(Map<String, Object> model, 
                                     Workbook workbook, 
                                     HttpServletRequest request, 
                                     HttpServletResponse response) throws Exception {
        
        List<User> users = (List<User>) model.get("users");
        
        // Create sheet
        Sheet sheet = workbook.createSheet("Users");
        sheet.setDefaultColumnWidth(15);
        
        // Style for header
        CellStyle headerStyle = workbook.createCellStyle();
        Font headerFont = workbook.createFont();
        headerFont.setBold(true);
        headerStyle.setFont(headerFont);
        headerStyle.setFillForegroundColor(IndexedColors.GREY_25_PERCENT.getIndex());
        headerStyle.setFillPattern(FillPatternType.SOLID_FOREGROUND);
        
        // Create header row
        Row headerRow = sheet.createRow(0);
        String[] headers = {"ID", "Username", "Email", "Created Date", "Status"};
        for (int i = 0; i < headers.length; i++) {
            Cell cell = headerRow.createCell(i);
            cell.setCellValue(headers[i]);
            cell.setCellStyle(headerStyle);
        }
        
        // Date style
        CellStyle dateStyle = workbook.createCellStyle();
        CreationHelper creationHelper = workbook.getCreationHelper();
        dateStyle.setDataFormat(creationHelper.createDataFormat()
            .getFormat("yyyy-mm-dd hh:mm"));
        
        // Create data rows
        int rowNum = 1;
        for (User user : users) {
            Row row = sheet.createRow(rowNum++);
            row.createCell(0).setCellValue(user.getId());
            row.createCell(1).setCellValue(user.getUsername());
            row.createCell(2).setCellValue(user.getEmail());
            
            Cell dateCell = row.createCell(3);
            dateCell.setCellValue(user.getCreatedDate());
            dateCell.setCellStyle(dateStyle);
            
            row.createCell(4).setCellValue(user.getStatus());
        }
        
        // Auto-size columns
        for (int i = 0; i < headers.length; i++) {
            sheet.autoSizeColumn(i);
        }
        
        // Set response headers
        response.setHeader("Content-Disposition", 
            "attachment; filename=users.xlsx");
    }
}

// Controller using different views
@Controller
@RequestMapping("/reports")
public class ReportController {
    
    @Autowired
    private UserService userService;
    
    @GetMapping("/users.pdf")
    public ModelAndView usersPdf() {
        List<User> users = userService.findAll();
        return new ModelAndView(new UserPdfView(), "users", users);
    }
    
    @GetMapping("/users.xlsx")
    public ModelAndView usersExcel() {
        List<User> users = userService.findAll();
        return new ModelAndView(new UserExcelView(), "users", users);
    }
    
    @GetMapping("/users.csv")
    public void usersCsv(HttpServletResponse response) throws IOException {
        response.setContentType("text/csv");
        response.setHeader("Content-Disposition", 
            "attachment; filename=users.csv");
        
        PrintWriter writer = response.getWriter();
        writer.println("ID,Username,Email,Status");
        
        for (User user : userService.findAll()) {
            writer.println(String.format("%d,%s,%s,%s",
                user.getId(),
                user.getUsername(),
                user.getEmail(),
                user.getStatus()));
        }
    }
}

// Content Negotiation Configuration
@Configuration
public class ContentNegotiationConfig implements WebMvcConfigurer {
    
    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer
            .favorPathExtension(true)
            .favorParameter(true)
            .parameterName("format")
            .ignoreAcceptHeader(false)
            .defaultContentType(MediaType.TEXT_HTML)
            .mediaType("html", MediaType.TEXT_HTML)
            .mediaType("json", MediaType.APPLICATION_JSON)
            .mediaType("xml", MediaType.APPLICATION_XML)
            .mediaType("pdf", MediaType.APPLICATION_PDF)
            .mediaType("xlsx", MediaType.valueOf("application/vnd.ms-excel"));
    }
    
    @Bean
    public ContentNegotiatingViewResolver contentNegotiatingViewResolver() {
        ContentNegotiatingViewResolver resolver = new ContentNegotiatingViewResolver();
        
        List<ViewResolver> viewResolvers = new ArrayList<>();
        viewResolvers.add(thymeleafViewResolver());
        viewResolvers.add(new BeanNameViewResolver());
        resolver.setViewResolvers(viewResolvers);
        
        List<View> defaultViews = new ArrayList<>();
        defaultViews.add(new MappingJackson2JsonView());
        defaultViews.add(new MarshallingView(jaxb2Marshaller()));
        resolver.setDefaultViews(defaultViews);
        
        return resolver;
    }
}
```

#### Chapter 9 Interview Q&A

**Q1: When would you choose Thymeleaf over JSP?** **A:**

- Thymeleaf: Natural templates, can be viewed in browser
- JSP: Requires servlet container, compiled
- Thymeleaf better for designer-developer collaboration
- JSP better for legacy systems

**Q2: How do you optimize view rendering performance?** **A:**

- Enable template caching in production
- Use CDN for static resources
- Minimize template complexity
- Pre-compile templates where possible

**Q3: How do you handle multiple output formats from same controller?** **A:**

```java
@GetMapping("/users")
public String users(Model model, 
                   @RequestHeader("Accept") String accept) {
    model.addAttribute("users", userService.findAll());
    
    if (accept.contains("application/pdf")) {
        return "usersPdfView";
    } else if (accept.contains("application/json")) {
        return "usersJsonView";
    }
    return "users/list";
}
```

---

### Chapter 10: Other Web Frameworks

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Struts Integration**|• ContextLoaderPlugin for Spring<br>• DelegatingActionProxy<br>• Dependency injection in Actions<br>• Shared application context|
|**JSF Integration**|• SpringBeanFacesELResolver<br>• Managed bean injection<br>• Scope management<br>• Navigation handling|
|**Tapestry Integration**|• Spring bean injection<br>• Page and component DI<br>• Service layer sharing<br>• Configuration integration|
|**WebWork Integration**|• SpringObjectFactory<br>• Action dependency injection<br>• Interceptor integration<br>• Result type configuration|

#### Code Examples

```java
// Struts Integration
// struts-config.xml
/*
<plug-in className="org.springframework.web.struts.ContextLoaderPlugIn">
    <set-property property="contextConfigLocation" 
                  value="/WEB-INF/applicationContext.xml"/>
</plug-in>

<action path="/user" 
        type="org.springframework.web.struts.DelegatingActionProxy"
        name="userForm"
        scope="request">
    <forward name="success" path="/users.jsp"/>
    <forward name="error" path="/error.jsp"/>
</action>
*/

// Struts Action with Spring
public class UserAction extends ActionSupport {
    
    private UserService userService; // Injected by Spring
    
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    
    public ActionForward execute(ActionMapping mapping,
                                 ActionForm form,
                                 HttpServletRequest request,
                                 HttpServletResponse response) {
        
        UserForm userForm = (UserForm) form;
        
        try {
            User user = new User();
            BeanUtils.copyProperties(user, userForm);
            userService.save(user);
            
            return mapping.findForward("success");
        } catch (Exception e) {
            ActionMessages errors = new ActionMessages();
            errors.add(ActionMessages.GLOBAL_MESSAGE,
                      new ActionMessage("error.user.save"));
            saveErrors(request, errors);
            return mapping.findForward("error");
        }
    }
}

// Spring configuration for Struts Action
@Configuration
public class StrutsConfig {
    
    @Bean("userAction")
    @Scope("prototype") // Important: Struts actions are not thread-safe
    public UserAction userAction(UserService userService) {
        UserAction action = new UserAction();
        action.setUserService(userService);
        return action;
    }
}

// JSF Integration
// faces-config.xml
/*
<application>
    <el-resolver>
        org.springframework.web.jsf.el.SpringBeanFacesELResolver
    </el-resolver>
</application>

<managed-bean>
    <managed-bean-name>userBean</managed-bean-name>
    <managed-bean-class>com.example.UserManagedBean</managed-bean-class>
    <managed-bean-scope>session</managed-bean-scope>
    <managed-property>
        <property-name>userService</property-name>
        <value>#{userService}</value>
    </managed-property>
</managed-bean>
*/

// JSF Managed Bean with Spring
@ManagedBean
@SessionScoped
public class UserManagedBean implements Serializable {
    
    @ManagedProperty(value = "#{userService}")
    private UserService userService;
    
    private User currentUser;
    private List<User> users;
    
    @PostConstruct
    public void init() {
        loadUsers();
    }
    
    public String save() {
        try {
            userService.save(currentUser);
            FacesContext.getCurrentInstance().addMessage(null,
                new FacesMessage("User saved successfully"));
            return "success";
        } catch (Exception e) {
            FacesContext.getCurrentInstance().addMessage(null,
                new FacesMessage(FacesMessage.SEVERITY_ERROR, 
                                "Error saving user", e.getMessage()));
            return null;
        }
    }
    
    public void loadUsers() {
        users = userService.findAll();
    }
    
    // Getters and setters
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
}

// Alternative: Pure Spring approach for JSF
@Component
@Scope("session")
public class SpringUserBean {
    
    @Autowired
    private UserService userService;
    
    public String saveUser(User user) {
        userService.save(user);
        return "success";
    }
}

// Tapestry Integration
public class UserPage extends BasePage {
    
    @InjectObject("spring:userService")
    public abstract UserService getUserService();
    
    @InjectState("currentUser")
    public abstract User getCurrentUser();
    
    public void saveUser(IRequestCycle cycle) {
        getUserService().save(getCurrentUser());
        cycle.activate("UserList");
    }
}

// Tapestry with Spring configuration
public class SpringModule {
    
    public static void contributeApplicationDefaults(
            MappedConfiguration<String, Object> configuration) {
        configuration.add("spring.context", 
            "classpath:applicationContext.xml");
    }
    
    @Contribute(ServiceBinder.class)
    public static void bind(ServiceBinder binder) {
        binder.bind(UserService.class, UserServiceImpl.class);
    }
}

// WebWork/Struts2 Integration
// xwork.xml
/*
<constant name="struts.objectFactory" 
          value="org.apache.struts2.spring.StrutsSpringObjectFactory"/>

<action name="user" class="userAction">
    <result>/user.jsp</result>
    <result name="input">/userForm.jsp</result>
</action>
*/

// WebWork Action with Spring
@Component("userAction")
@Scope("prototype")
public class UserAction extends ActionSupport {
    
    @Autowired
    private UserService userService;
    
    private User user;
    
    @Override
    public String execute() {
        users = userService.findAll();
        return SUCCESS;
    }
    
    public String save() {
        userService.save(user);
        addActionMessage("User saved successfully");
        return SUCCESS;
    }
    
    @Override
    public void validate() {
        if (user.getUsername() == null || user.getUsername().isEmpty()) {
            addFieldError("user.username", "Username is required");
        }
    }
    
    // Getters and setters
    public User getUser() {
        return user;
    }
    
    public void setUser(User user) {
        this.user = user;
    }
}

// Wicket Integration
public class UserPage extends WebPage {
    
    @SpringBean
    private UserService userService;
    
    public UserPage() {
        InjectorHolder.getInjector().inject(this);
        
        List<User> users = userService.findAll();
        
        add(new ListView<User>("users", users) {
            @Override
            protected void populateItem(ListItem<User> item) {
                User user = item.getModelObject();
                item.add(new Label("username", user.getUsername()));
                item.add(new Label("email", user.getEmail()));
            }
        });
        
        add(new Link<Void>("addUser") {
            @Override
            public void onClick() {
                setResponsePage(new EditUserPage());
            }
        });
    }
}

// Wicket Application with Spring
public class WicketApplication extends WebApplication {
    
    @Override
    public void init() {
        super.init();
        
        // Spring integration
        getComponentInstantiationListeners().add(
            new SpringComponentInjector(this));
    }
    
    @Override
    public Class<? extends Page> getHomePage() {
        return UserPage.class;
    }
}
```

#### Chapter 10 Interview Q&A

**Q1: Why integrate Spring with other web frameworks?** **A:**

- Leverage Spring's DI and services
- Use existing framework expertise
- Gradual migration strategy
- Best of both worlds approach

**Q2: What are the challenges in framework integration?** **A:**

- Scope mismatches (request vs singleton)
- Transaction boundary management
- Session handling differences
- Configuration complexity

**Q3: How do you share Spring context across frameworks?** **A:**

```java
// web.xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/applicationContext.xml</param-value>
</context-param>

<listener>
    <listener-class>
        org.springframework.web.context.ContextLoaderListener
    </listener-class>
</listener>
```

---

### Chapter 11: Security

|**Key Concepts**|**Detailed Explanation**|
|---|---|
|**Acegi/Spring Security**|• Authentication framework<br>• Authorization framework<br>• Web security<br>• Method security<br>• Remember-me services|
|**Authentication**|• AuthenticationManager<br>• AuthenticationProvider<br>• UserDetailsService<br>• Password encoding|
|**Authorization**|• AccessDecisionManager<br>• Voters and voting<br>• Role hierarchies<br>• Expression-based access|
|**Security Filters**|• FilterChainProxy<br>• SecurityContextFilter<br>• AuthenticationFilter<br>• AuthorizationFilter|

#### Code Examples

```java
// Security Configuration
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true, securedEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    
    @Autowired
    private UserDetailsService userDetailsService;
    
    @Autowired
    private CustomAuthenticationSuccessHandler successHandler;
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/", "/home", "/register").permitAll()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .antMatchers("/user/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .loginPage("/login")
                .loginProcessingUrl("/authenticate")
                .successHandler(successHandler)
                .failureUrl("/login?error=true")
                .permitAll()
                .and()
            .logout()
                .logoutUrl("/logout")
                .logoutSuccessUrl("/")
                .invalidateHttpSession(true)
                .deleteCookies("JSESSIONID")
                .and()
            .rememberMe()
                .key("uniqueAndSecret")
                .tokenValiditySeconds(86400)
                .and()
            .csrf()
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
                .and()
            .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.IF_REQUIRED)
                .maximumSessions(1)
                .expiredUrl("/login?expired=true");
    }
    
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .userDetailsService(userDetailsService)
            .passwordEncoder(passwordEncoder());
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    @Bean
    @Override
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }
}

// Custom UserDetailsService
@Service
public class CustomUserDetailsService implements UserDetailsService {
    
    @Autowired
    private UserRepository userRepository;
    
    @Override
    @Transactional(readOnly = true)
    public UserDetails loadUserByUsername(String username) 
            throws UsernameNotFoundException {
        
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException(
                "User not found: " + username));
        
        Set<GrantedAuthority> authorities = user.getRoles().stream()
            .map(role -> new SimpleGrantedAuthority("ROLE_" + role.getName()))
            .collect(Collectors.toSet());
        
        return new org.springframework.security.core.userdetails.User(
            user.getUsername(),
            user.getPassword(),
            user.isEnabled(),
            true, // accountNonExpired
            true, // credentialsNonExpired
            !user.isLocked(), // accountNonLocked
            authorities
        );
    }
}

// Authentication Success Handler
@Component
public class CustomAuthenticationSuccessHandler 
        implements AuthenticationSuccessHandler {
    
    @Override
    public void onAuthenticationSuccess(HttpServletRequest request,
                                      HttpServletResponse response,
                                      Authentication authentication) 
            throws IOException, ServletException {
        
        String username = authentication.getName();
        userService.updateLastLogin(username);
        
        // Role-based redirection
        Collection<? extends GrantedAuthority> authorities = 
            authentication.getAuthorities();
        
        String targetUrl = "/home";
        if (authorities.stream().anyMatch(a -> a.getAuthority().equals("ROLE_ADMIN"))) {
            targetUrl = "/admin/dashboard";
        } else if (authorities.stream().anyMatch(a -> a.getAuthority().equals("ROLE_USER"))) {
            targetUrl = "/user/profile";
        }
        
        response.sendRedirect(targetUrl);
    }
}

// Method Security Examples
@Service
public class SecureUserService {
    
    @PreAuthorize("hasRole('ADMIN')")
    public void deleteUser(Long userId) {
        // Only ADMIN can delete users
        userRepository.deleteById(userId);
    }
    
    @PreAuthorize("hasRole('USER') and #username == authentication.principal.username")
    public UserProfile getProfile(String username) {
        // Users can only access their own profile
        return userRepository.findProfileByUsername(username);
    }
    
    @PostAuthorize("returnObject.owner == authentication.principal.username or hasRole('ADMIN')")
    public Document getDocument(Long documentId) {
        // Can access if owner or admin
        return documentRepository.findById(documentId);
    }
    
    @PreFilter("hasRole('ADMIN') or filterObject.owner == authentication.principal.username")
    public void processDocuments(List<Document> documents) {
        // Filter documents before processing
        documents.forEach(this::process);
    }
    
    @PostFilter("hasRole('ADMIN') or filterObject.isPublic")
    public List<Article> getArticles() {
        // Filter results after retrieval
        return articleRepository.findAll();
    }
    
    @Secured({"ROLE_ADMIN", "ROLE_MODERATOR"})
    public void moderateContent(Long contentId) {
        // Multiple roles allowed
        contentRepository.moderate(contentId);
    }
}

// LDAP Authentication Configuration
@Configuration
public class LdapSecurityConfig {
    
    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .userSearchBase("ou=people")
                .userSearchFilter("(uid={0})")
                .groupSearchBase("ou=groups")
                .groupSearchFilter("member={0}")
                .contextSource()
                    .url("ldap://localhost:389/dc=springframework,dc=org")
                    .managerDn("cn=admin,dc=springframework,dc=org")
                    .managerPassword("password")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new BCryptPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}

// Database Authentication with Custom Tables
@Configuration
public class JdbcSecurityConfig {
    
    @Autowired
    private DataSource dataSource;
    
    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .jdbcAuthentication()
                .dataSource(dataSource)
                .usersByUsernameQuery(
                    "SELECT username, password, enabled " +
                    "FROM users WHERE username = ?")
                .authoritiesByUsernameQuery(
                    "SELECT u.username, r.role " +
                    "FROM users u " +
                    "JOIN user_roles ur ON u.id = ur.user_id " +
                    "JOIN roles r ON ur.role_id = r.id " +
                    "WHERE u.username = ?")
                .passwordEncoder(passwordEncoder());
    }
}

// Custom Authentication Provider
@Component
public class CustomAuthenticationProvider implements AuthenticationProvider {
    
    @Autowired
    private UserService userService;
    
    @Autowired
    private PasswordEncoder passwordEncoder;
    
    @Override
    public Authentication authenticate(Authentication authentication) 
            throws AuthenticationException {
        
        String username = authentication.getName();
        String password = authentication.getCredentials().toString();
        
        User user = userService.findByUsername(username);
        if (user == null) {
            throw new UsernameNotFoundException("User not found");
        }
        
        if (!passwordEncoder.matches(password, user.getPassword())) {
            throw new BadCredentialsException("Invalid password");
        }
        
        if (!user.isEnabled()) {
            throw new DisabledException("User is disabled");
        }
        
        if (user.isLocked()) {
            throw new LockedException("User account is locked");
        }
        
        List<SimpleGrantedAuthority> authorities = user.getRoles().stream()
            .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
            .collect(Collectors.toList());
        
        return new UsernamePasswordAuthenticationToken(
            username, password, authorities);
    }
    
    @Override
    public boolean supports(Class<?> authentication) {
        return authentication.equals(UsernamePasswordAuthenticationToken.class);
    }
}

// Security Filter Configuration
@Component
public class JwtAuthenticationFilter extends OncePerRequestFilter {
    
    @Autowired
    private JwtTokenProvider tokenProvider;
    
    @Autowired
    private UserDetailsService userDetailsService;
    
    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                  HttpServletResponse response,
                                  FilterChain filterChain) 
            throws ServletException, IOException {
        
        String token = extractToken(request);
        
        if (token != null && tokenProvider.validateToken(token)) {
            String username = tokenProvider.getUsernameFromToken(token);
            UserDetails userDetails = userDetailsService.loadUserByUsername(username);
            
            UsernamePasswordAuthenticationToken authentication = 
                new UsernamePasswordAuthenticationToken(
                    userDetails, null, userDetails.getAuthorities());
            
            authentication.setDetails(
                new WebAuthenticationDetailsSource().buildDetails(request));
            
            SecurityContextHolder.getContext().setAuthentication(authentication);
        }
        
        filterChain.doFilter(request, response);
    }
    
    private String extractToken(HttpServletRequest request) {
        String bearerToken = request.getHeader("Authorization");
        if (bearerToken != null && bearerToken.startsWith("Bearer ")) {
            return bearerToken.substring(7);
        }
        return null;
    }
}

// Access Decision Voter
@Component
public class CustomAccessDecisionVoter implements AccessDecisionVoter<Object> {
    
    @Override
    public boolean supports(ConfigAttribute attribute) {
        return true;
    }
    
    @Override
    public boolean supports(Class<?> clazz) {
        return true;
    }
    
    @Override
    public int vote(Authentication authentication, Object object,
                   Collection<ConfigAttribute> attributes) {
        
        if (authentication == null) {
            return ACCESS_DENIED;
        }
        
        // Custom voting logic
        FilterInvocation fi = (FilterInvocation) object;
        String url = fi.getRequestUrl();
        
        if (url.startsWith("/public")) {
            return ACCESS_GRANTED;
        }
        
        if (url.startsWith("/admin") && 
            !hasRole(authentication, "ROLE_ADMIN")) {
            return ACCESS_DENIED;
        }
        
        return ACCESS_ABSTAIN;
    }
    
    private boolean hasRole(Authentication auth, String role) {
        return auth.getAuthorities().stream()
            .anyMatch(a -> a.getAuthority().equals(role));
    }
}

// Remember Me Service
@Service
public class CustomRememberMeService extends 
        TokenBasedRememberMeServices {
    
    public CustomRememberMeService(String key, 
                                  UserDetailsService userDetailsService) {
        super(key, userDetailsService);
        setTokenValiditySeconds(2592000); // 30 days
        setCookieName("remember-me-token");
        setUseSecureCookie(true);
    }
    
    @Override
    protected String makeTokenSignature(long tokenExpiryTime, 
                                       String username, 
                                       String password) {
        // Custom token signature generation
        String data = username + ":" + tokenExpiryTime + ":" + password + ":" + getKey();
        MessageDigest digest;
        try {
            digest = MessageDigest.getInstance("MD5");
        } catch (NoSuchAlgorithmException e) {
            throw new IllegalStateException("No MD5 algorithm available!");
        }
        return new String(Hex.encode(digest.digest(data.getBytes())));
    }
}

// CAS Single Sign-On Configuration
@Configuration
public class CasSecurityConfig {
    
    @Bean
    public ServiceProperties serviceProperties() {
        ServiceProperties serviceProperties = new ServiceProperties();
        serviceProperties.setService("http://localhost:8080/login/cas");
        serviceProperties.setSendRenew(false);
        return serviceProperties;
    }
    
    @Bean
    public CasAuthenticationProvider casAuthenticationProvider() {
        CasAuthenticationProvider provider = new CasAuthenticationProvider();
        provider.setServiceProperties(serviceProperties());
        provider.setTicketValidator(cas20ServiceTicketValidator());
        provider.setUserDetailsService(userDetailsService());
        provider.setKey("CAS_PROVIDER_KEY");
        return provider;
    }
    
    @Bean
    public Cas20ServiceTicketValidator cas20ServiceTicketValidator() {
        return new Cas20ServiceTicketValidator("https://cas.server.com");
    }
    
    @Bean
    public CasAuthenticationFilter casAuthenticationFilter() throws Exception {
        CasAuthenticationFilter filter = new CasAuthenticationFilter();
        filter.setAuthenticationManager(authenticationManager());
        filter.setFilterProcessesUrl("/login/cas");
        return filter;
    }
    
    @Bean
    public CasAuthenticationEntryPoint casAuthenticationEntryPoint() {
        CasAuthenticationEntryPoint entryPoint = new CasAuthenticationEntryPoint();
        entryPoint.setLoginUrl("https://cas.server.com/login");
        entryPoint.setServiceProperties(serviceProperties());
        return entryPoint;
    }
}
```

### Chapter 11 Interview Q&A

**Q1: How does Spring Security authentication flow work?**
**A:**
1. User submits credentials
2. AuthenticationManager receives authentication request
3. Delegates to AuthenticationProvider(s)
4. Provider validates credentials
5. Returns Authentication object or throws exception
6. SecurityContext stores authenticated principal
7. User proceeds with authenticated session

**Q2: What's the difference between authentication and authorization?**
**A:**
- **Authentication**: Who you are (identity verification)
- **Authorization**: What you can do (access control)
- Authentication happens first, then authorization
- Example: Login (authentication) vs role checking (authorization)

**Q3: How do you implement custom login logic?**
**A:**
```java
@Service
public class CustomAuthenticationService {
    
    @Autowired
    private AuthenticationManager authenticationManager;
    
    public Authentication login(String username, String password) {
        UsernamePasswordAuthenticationToken token = 
            new UsernamePasswordAuthenticationToken(username, password);
        
        Authentication auth = authenticationManager.authenticate(token);
        SecurityContextHolder.getContext().setAuthentication(auth);
        
        return auth;
    }
}
```

**Q4: How do you secure REST APIs?**
**A:**
- Use stateless authentication (JWT tokens)
- Configure CORS properly
- Disable CSRF for stateless APIs
- Use HTTPS only
- Implement rate limiting

**Q5: What are common security vulnerabilities to avoid?**
**A:**
- SQL Injection: Use parameterized queries
- XSS: Sanitize user input, use Content Security Policy
- CSRF: Use tokens for state-changing operations
- Session fixation: Regenerate session ID after login
- Insecure direct object references: Always authorize access

---

## Master Interview Section

### Core Spring Framework Questions

#### Dependency Injection & IoC

**Q1: Explain the benefits of Dependency Injection.**
**A:**
- **Loose Coupling**: Components depend on abstractions, not implementations
- **Testability**: Easy to mock dependencies
- **Configurability**: Change behavior without code changes
- **Reusability**: Components can be used in different contexts
- **Maintainability**: Clear separation of concerns

**Q2: How does Spring resolve circular dependencies?**
**A:**
```java
// Circular dependency scenario
@Component
public class A {
    @Autowired
    private B b; // Setter injection works
}

@Component 
public class B {
    @Autowired
    private A a; // Spring can handle this
}

// Solutions:
// 1. Use setter injection (Spring creates proxy)
// 2. Use @Lazy annotation
// 3. Redesign to avoid circular dependency (best)
```

**Q3: What is the order of bean initialization?**
**A:**
```java
@Component
public class BeanLifecycleDemo implements 
    BeanNameAware, 
    BeanFactoryAware,
    ApplicationContextAware,
    InitializingBean,
    DisposableBean {
    
    // 1. Constructor
    public BeanLifecycleDemo() {
        System.out.println("1. Constructor");
    }
    
    // 2. Properties set
    @Autowired
    public void setDependency(Dependency dep) {
        System.out.println("2. Properties set");
    }
    
    // 3. BeanNameAware
    @Override
    public void setBeanName(String name) {
        System.out.println("3. BeanNameAware");
    }
    
    // 4. BeanFactoryAware
    @Override
    public void setBeanFactory(BeanFactory factory) {
        System.out.println("4. BeanFactoryAware");
    }
    
    // 5. ApplicationContextAware
    @Override
    public void setApplicationContext(ApplicationContext context) {
        System.out.println("5. ApplicationContextAware");
    }
    
    // 6. @PostConstruct
    @PostConstruct
    public void postConstruct() {
        System.out.println("6. @PostConstruct");
    }
    
    // 7. InitializingBean
    @Override
    public void afterPropertiesSet() {
        System.out.println("7. InitializingBean");
    }
    
    // 8. Custom init-method
    public void customInit() {
        System.out.println("8. Custom init-method");
    }
    
    // 9. @PreDestroy
    @PreDestroy
    public void preDestroy() {
        System.out.println("9. @PreDestroy");
    }
    
    // 10. DisposableBean
    @Override
    public void destroy() {
        System.out.println("10. DisposableBean");
    }
    
    // 11. Custom destroy-method
    public void customDestroy() {
        System.out.println("11. Custom destroy-method");
    }
}
```

#### AOP Questions

**Q4: How do you implement caching with AOP?**
**A:**
```java
@Aspect
@Component
public class CachingAspect {
    
    private Map<String, Object> cache = new ConcurrentHashMap<>();
    
    @Around("@annotation(Cacheable)")
    public Object cache(ProceedingJoinPoint pjp) throws Throwable {
        String key = generateKey(pjp);
        
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        
        Object result = pjp.proceed();
        cache.put(key, result);
        return result;
    }
    
    private String generateKey(ProceedingJoinPoint pjp) {
        return pjp.getSignature().toString() + 
               Arrays.toString(pjp.getArgs());
    }
}
```

**Q5: What's the difference between @Before and @Around advice?**
**A:**
- **@Before**: Cannot prevent method execution, cannot modify return value
- **@Around**: Full control, can prevent execution, modify arguments/return
- @Around must call proceed() to execute target method
- @Before is simpler for logging/validation

#### Transaction Questions

**Q6: How do you handle transactions across multiple databases?**
**A:**
```java
@Configuration
public class MultiDbTransactionConfig {
    
    @Bean
    @Primary
    public PlatformTransactionManager primaryTransactionManager(
            @Qualifier("primaryDataSource") DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
    
    @Bean
    public PlatformTransactionManager secondaryTransactionManager(
            @Qualifier("secondaryDataSource") DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
    
    // For distributed transactions
    @Bean
    public JtaTransactionManager jtaTransactionManager() {
        UserTransaction userTransaction = new UserTransactionImp();
        TransactionManager transactionManager = new TransactionManagerImp();
        return new JtaTransactionManager(userTransaction, transactionManager);
    }
}

@Service
public class MultiDbService {
    
    @Transactional("primaryTransactionManager")
    public void updatePrimaryDb() {
        // Updates primary database
    }
    
    @Transactional("secondaryTransactionManager")
    public void updateSecondaryDb() {
        // Updates secondary database
    }
    
    @Transactional("jtaTransactionManager")
    public void updateBothDbs() {
        // Distributed transaction across both databases
    }
}
```

**Q7: What happens when @Transactional method calls another @Transactional method?**
**A:**
- Same class: Annotation ignored (no proxy interception)
- Different class: New transaction behavior depends on propagation
- Solution for same class: Use self-injection or AspectJ

```java
@Service
public class TransactionService {
    
    @Autowired
    private TransactionService self; // Self-injection
    
    @Transactional
    public void methodA() {
        // This won't work - no proxy interception
        methodB(); 
        
        // This works - goes through proxy
        self.methodB();
    }
    
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void methodB() {
        // Business logic
    }
}
```

#### Database Access Questions

**Q8: How do you implement pagination and sorting?**
**A:**
```java
// Using Spring Data JPA
public interface UserRepository extends PagingAndSortingRepository<User, Long> {
    
    Page<User> findByStatus(String status, Pageable pageable);
    
    @Query("SELECT u FROM User u WHERE u.age > :age")
    Page<User> findByAgeGreaterThan(@Param("age") int age, Pageable pageable);
}

@Service
public class UserService {
    
    public Page<User> getUsers(int page, int size, String sortBy) {
        Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
        return userRepository.findAll(pageable);
    }
    
    public Page<User> getUsersMultiSort(int page, int size) {
        Sort sort = Sort.by(
            Sort.Order.desc("createdDate"),
            Sort.Order.asc("username")
        );
        Pageable pageable = PageRequest.of(page, size, sort);
        return userRepository.findAll(pageable);
    }
}

// Using JdbcTemplate
public List<User> getUsersPaginated(int page, int size) {
    String sql = "SELECT * FROM users ORDER BY id LIMIT ? OFFSET ?";
    return jdbcTemplate.query(sql, 
        new Object[]{size, page * size}, 
        new UserRowMapper());
}
```

**Q9: How do you handle database connection pooling?**
**A:**
```java
@Configuration
public class DataSourceConfig {
    
    @Bean
    @ConfigurationProperties("spring.datasource.hikari")
    public HikariConfig hikariConfig() {
        return new HikariConfig();
    }
    
    @Bean
    public DataSource dataSource(HikariConfig config) {
        // HikariCP configuration
        config.setMaximumPoolSize(20);
        config.setMinimumIdle(5);
        config.setConnectionTimeout(30000);
        config.setIdleTimeout(600000);
        config.setMaxLifetime(1800000);
        config.setLeakDetectionThreshold(60000);
        
        return new HikariDataSource(config);
    }
    
    // Alternative: Apache DBCP2
    @Bean
    public DataSource dbcp2DataSource() {
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/db");
        dataSource.setUsername("user");
        dataSource.setPassword("password");
        
        // Pool configuration
        dataSource.setInitialSize(5);
        dataSource.setMaxTotal(20);
        dataSource.setMaxIdle(10);
        dataSource.setMinIdle(5);
        dataSource.setMaxWaitMillis(30000);
        dataSource.setValidationQuery("SELECT 1");
        dataSource.setTestOnBorrow(true);
        dataSource.setTestWhileIdle(true);
        dataSource.setTimeBetweenEvictionRunsMillis(30000);
        
        return dataSource;
    }
}
```

#### Web Layer Questions

**Q10: How do you handle cross-origin requests (CORS)?**
**A:**
```java
@Configuration
public class CorsConfig {
    
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**")
                    .allowedOrigins("http://localhost:3000", "https://example.com")
                    .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                    .allowedHeaders("*")
                    .allowCredentials(true)
                    .maxAge(3600);
            }
        };
    }
}

// Or at controller level
@RestController
@CrossOrigin(origins = "http://localhost:3000")
public class ApiController {
    
    @GetMapping("/data")
    public ResponseEntity<?> getData() {
        return ResponseEntity.ok(data);
    }
}

// Or with Spring Security
@Configuration
public class SecurityCorsConfig {
    
    @Bean
    public CorsConfigurationSource corsConfigurationSource() {
        CorsConfiguration configuration = new CorsConfiguration();
        configuration.setAllowedOrigins(Arrays.asList("*"));
        configuration.setAllowedMethods(Arrays.asList("GET", "POST", "PUT", "DELETE"));
        configuration.setAllowedHeaders(Arrays.asList("*"));
        configuration.setAllowCredentials(true);
        
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/**", configuration);
        return source;
    }
}
```

**Q11: How do you implement API versioning?**
**A:**
```java
// 1. URL Path Versioning
@RestController
@RequestMapping("/api/v1/users")
public class UserControllerV1 {
    // Version 1 implementation
}

@RestController
@RequestMapping("/api/v2/users")
public class UserControllerV2 {
    // Version 2 implementation
}

// 2. Request Parameter Versioning
@RestController
@RequestMapping("/api/users")
public class UserController {
    
    @GetMapping(params = "version=1")
    public List<UserV1> getUsersV1() {
        return userServiceV1.getUsers();
    }
    
    @GetMapping(params = "version=2")
    public List<UserV2> getUsersV2() {
        return userServiceV2.getUsers();
    }
}

// 3. Header Versioning
@RestController
@RequestMapping("/api/users")
public class UserController {
    
    @GetMapping(headers = "API-VERSION=1")
    public List<UserV1> getUsersV1() {
        return userServiceV1.getUsers();
    }
    
    @GetMapping(headers = "API-VERSION=2")
    public List<UserV2> getUsersV2() {
        return userServiceV2.getUsers();
    }
}

// 4. Content Negotiation Versioning
@RestController
@RequestMapping("/api/users")
public class UserController {
    
    @GetMapping(produces = "application/vnd.company.api-v1+json")
    public List<UserV1> getUsersV1() {
        return userServiceV1.getUsers();
    }
    
    @GetMapping(produces = "application/vnd.company.api-v2+json")
    public List<UserV2> getUsersV2() {
        return userServiceV2.getUsers();
    }
}
```

### Performance & Optimization Questions

**Q12: How do you optimize Spring application performance?**
**A:**

```java
// 1. Connection Pool Optimization
@Bean
public DataSource dataSource() {
    HikariConfig config = new HikariConfig();
    config.setMaximumPoolSize(20); // Based on formula: connections = ((core_count * 2) + effective_spindle_count)
    config.setConnectionTimeout(30000);
    config.setLeakDetectionThreshold(60000);
    return new HikariDataSource(config);
}

// 2. Caching
@Configuration
@EnableCaching
public class CacheConfig {
    
    @Bean
    public CacheManager cacheManager() {
        CaffeineCacheManager cacheManager = new CaffeineCacheManager();
        cacheManager.setCaffeine(Caffeine.newBuilder()
            .maximumSize(1000)
            .expireAfterWrite(10, TimeUnit.MINUTES)
            .recordStats());
        return cacheManager;
    }
}

@Service
public class UserService {
    
    @Cacheable(value = "users", key = "#id")
    public User findById(Long id) {
        return userRepository.findById(id);
    }
    
    @CacheEvict(value = "users", key = "#user.id")
    public void updateUser(User user) {
        userRepository.save(user);
    }
}

// 3. Lazy Loading
@Configuration
@ComponentScan(lazyInit = true)
public class AppConfig {
    // Beans initialized on first use
}

// 4. Async Processing
@Configuration
@EnableAsync
public class AsyncConfig {
    
    @Bean
    public TaskExecutor taskExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(5);
        executor.setMaxPoolSize(10);
        executor.setQueueCapacity(100);
        executor.setThreadNamePrefix("Async-");
        executor.initialize();
        return executor;
    }
}

@Service
public class AsyncService {
    
    @Async
    public CompletableFuture<User> findUserAsync(Long id) {
        User user = userRepository.findById(id);
        return CompletableFuture.completedFuture(user);
    }
}

// 5. Database Query Optimization
@Entity
@NamedEntityGraph(name = "User.withRoles",
    attributeNodes = @NamedAttributeNode("roles"))
public class User {
    // Prevent N+1 queries
}

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    @EntityGraph("User.withRoles")
    List<User> findAll();
    
    @Query("SELECT u FROM User u JOIN FETCH u.roles WHERE u.status = :status")
    List<User> findByStatusWithRoles(@Param("status") String status);
}
```

**Q13: How do you monitor Spring application performance?**
**A:**
```java
// 1. Spring Boot Actuator
@Configuration
@EnableActuator
public class ActuatorConfig {
    // Exposes metrics, health, info endpoints
}

// 2. Custom Metrics
@Component
public class MetricsService {
    
    private final MeterRegistry meterRegistry;
    
    @Autowired
    public MetricsService(MeterRegistry meterRegistry) {
        this.meterRegistry = meterRegistry;
    }
    
    public void recordMetric(String name, double value) {
        meterRegistry.gauge(name, value);
    }
    
    @EventListener
    public void handleUserLogin(UserLoginEvent event) {
        meterRegistry.counter("user.login", "type", event.getType()).increment();
    }
}

// 3. Performance Interceptor
@Component
public class PerformanceInterceptor implements HandlerInterceptor {
    
    @Override
    public boolean preHandle(HttpServletRequest request, 
                           HttpServletResponse response, 
                           Object handler) {
        request.setAttribute("startTime", System.currentTimeMillis());
        return true;
    }
    
    @Override
    public void afterCompletion(HttpServletRequest request, 
                               HttpServletResponse response, 
                               Object handler, 
                               Exception ex) {
        long startTime = (Long) request.getAttribute("startTime");
        long endTime = System.currentTimeMillis();
        long executeTime = endTime - startTime;
        
        if (executeTime > 1000) {
            logger.warn("Request {} took {}ms", request.getRequestURI(), executeTime);
        }
    }
}
```

### Testing Questions

**Q14: How do you test Spring applications?**
**A:**
```java
// 1. Unit Testing with Mockito
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    
    @Mock
    private UserRepository userRepository;
    
    @InjectMocks
    private UserService userService;
    
    @Test
    void testFindUser() {
        // Given
        User mockUser = new User(1L, "test");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));
        
        // When
        User result = userService.findById(1L);
        
        // Then
        assertEquals("test", result.getName());
        verify(userRepository).findById(1L);
    }
}

// 2. Integration Testing
@SpringBootTest
@AutoConfigureMockMvc
class UserControllerIntegrationTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @Test
    void testGetUser() throws Exception {
        mockMvc.perform(get("/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("test"))
            .andDo(print());
    }
    
    @Test
    @Transactional
    @Rollback
    void testCreateUser() throws Exception {
        String userJson = "{\"name\":\"test\",\"email\":\"test@example.com\"}";
        
        mockMvc.perform(post("/users")
                .contentType(MediaType.APPLICATION_JSON)
                .content(userJson))
            .andExpect(status().isCreated())
            .andExpect(header().exists("Location"));
    }
}

// 3. Repository Testing
@DataJpaTest
class UserRepositoryTest {
    
    @Autowired
    private TestEntityManager entityManager;
    
    @Autowired
    private UserRepository userRepository;
    
    @Test
    void testFindByEmail() {
        // Given
        User user = new User("test", "test@example.com");
        entityManager.persistAndFlush(user);
        
        // When
        Optional<User> found = userRepository.findByEmail("test@example.com");
        
        // Then
        assertTrue(found.isPresent());
        assertEquals("test", found.get().getName());
    }
}

// 4. Web Layer Testing
@WebMvcTest(UserController.class)
class UserControllerTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @MockBean
    private UserService userService;
    
    @Test
    void testGetUsers() throws Exception {
        List<User> users = Arrays.asList(
            new User(1L, "user1"),
            new User(2L, "user2")
        );
        
        when(userService.findAll()).thenReturn(users);
        
        mockMvc.perform(get("/users"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$", hasSize(2)))
            .andExpect(jsonPath("$[0].name").value("user1"));
    }
}
```

### Best Practices & Design Patterns

**Q15: What are Spring best practices?**
**A:**

```java
// 1. Use Constructor Injection
@Service
public class UserService {
    private final UserRepository repository;
    private final EmailService emailService;
    
    // Constructor injection - immutable, testable
    public UserService(UserRepository repository, EmailService emailService) {
        this.repository = repository;
        this.emailService = emailService;
    }
}

// 2. Separate Concerns with Layers
@RestController // Presentation Layer
public class UserController {
    private final UserService userService;
}

@Service // Business Layer
public class UserService {
    private final UserRepository userRepository;
}

@Repository // Data Access Layer
public interface UserRepository extends JpaRepository<User, Long> {
}

// 3. Use DTOs for Data Transfer
@Data
public class UserDTO {
    private Long id;
    private String username;
    private String email;
    // No password or sensitive data
}

@Component
public class UserMapper {
    public UserDTO toDto(User user) {
        return UserDTO.builder()
            .id(user.getId())
            .username(user.getUsername())
            .email(user.getEmail())
            .build();
    }
}

// 4. Proper Exception Handling
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(ResourceNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ErrorResponse handleNotFound(ResourceNotFoundException e) {
        return new ErrorResponse(e.getMessage(), HttpStatus.NOT_FOUND.value());
    }
    
    @ExceptionHandler(ValidationException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public ErrorResponse handleValidation(ValidationException e) {
        return new ErrorResponse(e.getMessage(), HttpStatus.BAD_REQUEST.value());
    }
}

// 5. Use Profiles for Environment Configuration
@Configuration
@Profile("production")
public class ProductionConfig {
    // Production-specific beans
}

@Configuration
@Profile("development")
public class DevelopmentConfig {
    // Development-specific beans
}

// 6. Validate Input
@RestController
public class UserController {
    
    @PostMapping("/users")
    public ResponseEntity<User> createUser(@Valid @RequestBody UserRequest request) {
        // @Valid triggers validation
        return ResponseEntity.ok(userService.create(request));
    }
}

@Data
public class UserRequest {
    @NotBlank(message = "Username is required")
    @Size(min = 3, max = 50)
    private String username;
    
    @Email(message = "Invalid email format")
    @NotBlank(message = "Email is required")
    private String email;
    
    @Pattern(regexp = "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
             message = "Password must be at least 8 characters with letters and numbers")
    private String password;
}
```

---

## Quick Reference

### Essential Annotations Cheat Sheet

```java
// Core Spring
@Component          // Generic component
@Service           // Business logic layer
@Repository        // Data access layer
@Controller        // Web controller
@Configuration     // Java configuration class
@Bean             // Method produces a bean
@Autowired        // Dependency injection
@Qualifier        // Specify which bean to inject
@Primary          // Default bean when multiple candidates
@Value            // Inject property values
@PropertySource   // Specify properties file
@Scope            // Bean scope (singleton, prototype, etc.)
@Lazy             // Lazy initialization
@DependsOn        // Bean initialization order
@PostConstruct    // Method called after bean creation
@PreDestroy       // Method called before bean destruction

// Web Annotations
@RestController    // @Controller + @ResponseBody
@RequestMapping   // Map HTTP requests
@GetMapping       // GET request mapping
@PostMapping      // POST request mapping
@PutMapping       // PUT request mapping
@DeleteMapping    // DELETE request mapping
@PatchMapping     // PATCH request mapping
@PathVariable     // Extract URL path variables
@RequestParam     // Extract query parameters
@RequestBody      // Bind request body
@ResponseBody     // Return object as response body
@ResponseStatus   // Set HTTP response status
@ExceptionHandler // Handle exceptions
@ControllerAdvice // Global exception handling
@CrossOrigin      // Enable CORS
@SessionAttributes // Store model attributes in session
@ModelAttribute   // Bind method parameter or return value to model

// Validation
@Valid            // Trigger validation
@Validated        // Group validation
@NotNull          // Field cannot be null
@NotEmpty         // Field cannot be null or empty
@NotBlank         // Field cannot be null, empty, or whitespace
@Size             // String/Collection size constraints
@Min              // Minimum numeric value
@Max              // Maximum numeric value
@Email            // Valid email format
@Pattern          // Regex pattern matching
@Past             // Date in the past
@Future           // Date in the future

// Transaction
@Transactional    // Declarative transaction
@EnableTransactionManagement // Enable transaction support

// AOP
@Aspect           // Aspect class
@Before           // Before advice
@After            // After advice (finally)
@AfterReturning   // After successful return
@AfterThrowing    // After exception
@Around           // Around advice
@Pointcut         // Pointcut definition
@EnableAspectJAutoProxy // Enable AOP

// Security
@EnableWebSecurity // Enable Spring Security
@PreAuthorize     // Method-level security (before)
@PostAuthorize    // Method-level security (after)
@Secured          // Method-level security
@RolesAllowed     // JSR-250 role checking
@EnableGlobalMethodSecurity // Enable method security

// Caching
@Cacheable        // Cache method results
@CacheEvict       // Remove from cache
@CachePut         // Update cache
@Caching          // Multiple cache operations
@EnableCaching    // Enable caching support

// Scheduling
@Scheduled        // Schedule method execution
@EnableScheduling // Enable scheduling support
@Async           // Asynchronous execution
@EnableAsync     // Enable async support

// Testing
@SpringBootTest   // Integration test
@WebMvcTest      // Test web layer
@DataJpaTest     // Test JPA repositories
@MockBean        // Mock Spring bean
@SpyBean         // Spy on Spring bean
@TestConfiguration // Test-specific configuration
@DirtiesContext  // Reset application context
@ActiveProfiles  // Activate profiles for test
@TestPropertySource // Test-specific properties
```

### Common Configuration Patterns

```yaml
# application.yml
spring:
  profiles:
    active: dev
  
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: password
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      connection-timeout: 30000
  
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: true
    properties:
      hibernate:
        format_sql: true
        dialect: org.hibernate.dialect.MySQL5Dialect
  
  redis:
    host: localhost
    port: 6379
    timeout: 2000
    jedis:
      pool:
        max-active: 8
        max-idle: 8
        min-idle: 0
  
  kafka:
    bootstrap-servers: localhost:9092
    consumer:
      group-id: my-group
      auto-offset-reset: earliest
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.springframework.kafka.support.serializer.JsonSerializer

server:
  port: 8080
  servlet:
    context-path: /api
  compression:
    enabled: true
    mime-types: application/json,application/xml,text/html
    min-response-size: 1024

logging:
  level:
    root: INFO
    com.example: DEBUG
    org.springframework.web: DEBUG
    org.hibernate.SQL: DEBUG
  pattern:
    console: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"
    file: "%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n"
  file:
    name: app.log
    max-size: 10MB
    max-history: 30

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  metrics:
    export:
      prometheus:
        enabled: true
```

### Troubleshooting Guide

| **Problem** | **Solution** |
|------------|------------|
| **Bean not found** | Check @ComponentScan, @Component annotations, package structure |
| **Circular dependency** | Use setter injection, @Lazy, or redesign |
| **Transaction not working** | Ensure @EnableTransactionManagement, check proxy mode, public methods |
| **AOP not working** | Check @EnableAspectJAutoProxy, proxy limitations, pointcut expressions |
| **Validation not triggered** | Add @Valid/@Validated, ensure validator on classpath |
| **@Autowired null** | Check if class is Spring-managed, constructor injection recommended |
| **Multiple beans found** | Use @Qualifier or @Primary |
| **SQL logging not showing** | Enable hibernate.show_sql and logging.level.org.hibernate.SQL=DEBUG |
| **CORS issues** | Configure CORS mappings, check allowed origins/methods |
| **Session timeout** | Configure server.servlet.session.timeout |
| **Memory leaks** | Check for unclosed resources, circular references, thread locals |
| **Slow startup** | Use lazy initialization, optimize component scanning |
| **Test rollback not working** | Add @Transactional and @Rollback to test class |

---

## Final Study Tips

### Learning Path
1. **Week 1-2**: Core Spring (IoC, DI, Beans)
2. **Week 3**: AOP and Testing
3. **Week 4**: Data Access (JDBC, JPA, Transactions)
4. **Week 5**: Web Layer (MVC, REST)
5. **Week 6**: Security and Advanced Topics
6. **Week 7-8**: Build a complete project

### Practice Projects
1. **Basic CRUD Application**: User management system
2. **E-commerce Backend**: Products, orders, payments
3. **Microservices**: Break monolith into services
4. **Real-time Chat**: WebSockets, messaging
5. **API Gateway**: Security, routing, rate limiting

### Interview Preparation Checklist
- [ ] Understand IoC and DI principles
- [ ] Know bean lifecycle thoroughly
- [ ] Practice writing AOP aspects
- [ ] Master transaction management
- [ ] Understand Spring MVC flow
- [ ] Know security best practices
- [ ] Practice coding common patterns
- [ ] Review your project experiences
- [ ] Prepare STAR format answers
- [ ] Mock interview practice

### Resources for Continued Learning
- [Spring Official Documentation](https://spring.io/docs)
- [Spring Guides](https://spring.io/guides)
- [Baeldung Tutorials](https://www.baeldung.com)
- [Spring Source Code](https://github.com/spring-projects)
- [Spring Boot Reference](https://docs.spring.io/spring-boot/docs/current/reference/html/)

---

*Remember: The key to mastering Spring is not just understanding concepts but implementing them. Build projects, contribute to open source, and keep practicing!*

**Last Updated**: Based on Spring Framework 5.x and Spring Boot 2.x patterns. Always check current documentation for the latest features and best practices.