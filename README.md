# Optional Java 7
Tired of handling nullpointers in Java 7.
See the Optional Implementation for Java 7.

```java
import java.util.NoSuchElementException;

public class Optional<T> {

    private static final Optional<?> EMPTY = new Optional(Null.INSTANCE);
    private T value;

    protected Optional(T value){
        this.value = value;
    }

    public static <T> Optional<T> of(T value){
        return new Optional<T>(value);
    }

    @SuppressWarnings("unchecked")
    public static <T> Optional<T> empty(){
        return (Optional<T>) EMPTY;
    }

    public static <T> Optional<T> ofNullable(T value){
        if(value == null){
            return empty();
        }else{
            return of(value);
        }
    }

    public boolean isPresent(){
        return !(this.value == null || this == EMPTY);
    }

    public T get() throws NoSuchElementException {
        if(isPresent()){
            return value;
        }else{
            throw new NoSuchElementException();
        }
    }

    public T orElse(T other) {
        if(isPresent()){
            return value;
        }else{
            return other;
        }
    }

    private static class Null {
        private static final Null INSTANCE = new Null();
        private Null(){
            // Private constructor
            super();
        }
    }

}

```
