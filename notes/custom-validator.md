# Custom Validator

Create an annotation:
```
package com.cybr406.bookdemo;

import javax.validation.Constraint;
import javax.validation.Payload;
import java.lang.annotation.*;

@Documented
@Constraint(validatedBy = UsernameDoesNotExistValidator.class)
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface UsernameDoesNotExist {

    String message() default "The username you chose is already in use.";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};

}
```

Create a validator:
```
package com.cybr406.bookdemo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.provisioning.JdbcUserDetailsManager;
import org.springframework.stereotype.Component;

import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

@Component
public class UsernameDoesNotExistValidator implements ConstraintValidator<UsernameDoesNotExist, String> {

    @Autowired
    private JdbcUserDetailsManager userDetailsManager;

    @Override
    public void initialize(UsernameDoesNotExist constraintAnnotation) {

    }

    @Override
    public boolean isValid(String value, ConstraintValidatorContext context) {
        return !userDetailsManager.userExists(value);
    }
}
```
