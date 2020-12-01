# 第七章 构建RESTful服务

## 7.2 JPA实现REST

### 创建数据库

不用创建表

```sql
CREATE DATABASE `jparestful` DEFAULT CHARACTER SET utf8;
```

### 依赖

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-rest</artifactId>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.10</version>
    </dependency>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

### 配置文件

```properties
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.url=jdbc:mysql://59.78.194.153:3306/jparestful?useUnicode=true&characterEncoding=utf8&useSSL=false&serverTimezone=Hongkong
spring.jpa.hibernate.ddl-auto=update
spring.jpa.database=mysql
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
spring.jpa.show-sql=true
```

### 创建实体类

```java
@Entity(name = "t_book") // @Entity 是一个必选的注解，声明这个类对应了一个数据库表。
public class Book {
    @Id  // 注解声明了实体唯一标识对应的属性
    @GeneratedValue(strategy = GenerationType.IDENTITY)  // 主键自增
    private Integer id;
    private String name;
    private String author;
}
```

### 创建BookRepository

```java
// 自定义请求路径
@RepositoryRestResource(path = "bs", collectionResourceRel = "bs", itemResourceRel = "b")
public interface BookRepository extends JpaRepository<Book, Integer> {
    @RestResource(path = "author", rel = "author")  // 自定义查询方法
    List<Book> findByAuthorContains(@Param("author") String author);
    @RestResource(path = "name", rel = "name")  // 自定义查询方法
    Book findByNameEquals(@Param("name") String name);
    @Override
    @RestResource(exported = false)  // 隐藏方法
    void deleteById(Integer integer);
}
```

### 测试

```
###
添加测试
###
POST http://localhost:8080/books
Content-Type: application/json

{
  "name": "三国演义",
  "author": "罗贯中"
}

###
POST http://localhost:8080/books
Content-Type: application/json

{
  "name": "红楼梦",
  "author": "曹雪芹"
}

###
查询测试
###
GET http://localhost:8080/books

###
修改测试
###
PUT http://localhost:8080/books/2
Content-Type: application/json

{
  "name": "红楼梦2",
  "author": "曹雪芹2"
}

###
删除测试
###
DELETE http://localhost:8080/books/1

```

## 7.2 MongoDB实现RESTful

todo