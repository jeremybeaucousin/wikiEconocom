# MySQL

## Definition des variables sql_mode

```sql
SELECT @@GLOBAL.sql_mode global, @@SESSION.sql_mode session;

SET sql_mode = 'STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,ALLOW_INVALID_DATES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
SET GLOBAL sql_mode = 'STRICT_TRANS_TABLES,STRICT_ALL_TABLES,NO_ZERO_IN_DATE,ALLOW_INVALID_DATES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
```

## Plugin validate_password

[Documentation officielle](https://dev.mysql.com/doc/refman/5.7/en/validate-password.html)

### Montre les plugins 'validate%'

```sql
SELECT PLUGIN_NAME, PLUGIN_STATUS
FROM INFORMATION_SCHEMA.PLUGINS
WHERE PLUGIN_NAME LIKE 'validate%';
```

### Montre les variables 'validate_password%' utilisé par le plugin

```sql
SHOW VARIABLES LIKE 'validate_password%';
```

### Règles du plugin

**LOW** policy tests password length only. Passwords must be at least 8 characters long. To change this length, modify validate_password_length.

**MEDIUM** policy adds the conditions that passwords must contain at least 1 numeric character, 1 lowercase character, 1 uppercase character, and 1 special (nonalphanumeric) character. To change these values, modify validate_password_number_count, validate_password_mixed_case_count, and validate_password_special_char_count.

**STRONG** policy adds the condition that password substrings of length 4 or longer must not match words in the dictionary file, if one has been specified. To specify the dictionary file, modify validate_password_dictionary_file.