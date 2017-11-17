# java-builder-pattern-tricks
The java builder pattern has been described frequently but is nearly always described in a very basic form without revealing its true potential! 

So what are these extra tricks?

 * Shortcut the `builder()` method
 * Mandatory parameters with builder chaining C
 * Get compile time indications as the class evolves with field changes
 * Type safety with builder chaining (not just method chaining!)
 * Force formatting in IDEs of method chaining (avoid long lines of code!)

Let's start with a basic builder pattern and then we'll improve it. We'll consider how to build a `Book` object:

```java
public final class Book {
    // Make fields final!
    private final String author;
    private final String title;
    private final Optional<String> category;
    
    private Book(Builder builder) {
        //Be a bit defensive
        Preconditions.checkNotNull(builder.author);
        Preconditions.checkArgument(builder.author.trim().length() > 0);
        Preconditions.checkNotNull(builder.title);
        Preconditions.checkArgument(builder.title.trim().length() > 0);
        Preconditions.checkNotNull(category);
        this.author = builder.author;
        this.title = title;
        this.category = category;
    }
    
    public String author() {
        return author;
    }
    
    public String title() {
        return title();
    }
    
    public Optional<Category> category() {
       return category;
    }
    
    public static Builder builder() {
        return new Builder();
    }
    
    public static final class Builder {
        String author;
        String title;
        Optional<String> category = Optional.empty();
        
        Builder() {
        }
        
        public Builder author(String author) {
            this.author = author;
        }
        
        public Builder title(String title) {
            this.title = title;
        }
        
        public Book build() {
            return new Book(this);
        }      
}
```

To use this basic builder:

```java
Book book = Book
  .builder()
  .author("Charles Dickens")
  .title("Great Expectations")
  .category("Novel")
  .build();
```


