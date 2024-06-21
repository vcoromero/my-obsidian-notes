### Script base para crear la base de datos en la conexión de mysql

```sql
CREATE DATABASE IF NOT EXISTS gymstration DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

USE gymstration;

GRANT ALL PRIVILEGES ON gymstration.* TO 'gymstrator'@'%';

FLUSH PRIVILEGES;
```

#### Script sql para creación de la base de datos, tablas, relaciones, indices y datos necesarios

```sql
CREATE DATABASE IF NOT EXISTS gymstration DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

USE gymstration;

GRANT ALL PRIVILEGES ON gymstration.* TO 'gymstrator'@'%';

FLUSH PRIVILEGES;

CREATE TABLE IF NOT EXISTS roles (
id CHAR(36) PRIMARY KEY,
name VARCHAR(50) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL
);  

CREATE TABLE IF NOT EXISTS functions (
id CHAR(36) PRIMARY KEY,
name VARCHAR(50) NOT NULL,
description VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL
);

CREATE TABLE IF NOT EXISTS rolefunctions (
role_id CHAR(36),
function_id CHAR(36),
PRIMARY KEY (role_id, function_id),
FOREIGN KEY (role_id) REFERENCES roles(id),
FOREIGN KEY (function_id) REFERENCES functions(id)
);

CREATE TABLE IF NOT EXISTS users (
id CHAR(36) PRIMARY KEY,
user_code INT AUTO_INCREMENT UNIQUE NOT NULL,
name VARCHAR(50) NOT NULL,
second_name VARCHAR(50) NULL DEFAULT NULL,
surname VARCHAR(50) NOT NULL,
second_surname VARCHAR(50) NULL DEFAULT NULL,
email VARCHAR(60) NOT NULL UNIQUE,
password VARCHAR(255) NOT NULL,
role_id CHAR(36),
pin VARCHAR(6) UNIQUE NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL,
FOREIGN KEY (role_id) REFERENCES roles(id)
);

CREATE TABLE IF NOT EXISTS selfies (
id CHAR(36) PRIMARY KEY,
user_id CHAR(36) UNIQUE NOT NULL,
image_path VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL,
FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS memberships (
id CHAR(36) PRIMARY KEY,
type VARCHAR(50) NOT NULL,
description VARCHAR(255) NOT NULL,
price DECIMAL(10, 2) NOT NULL,
duration INT NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL
);

CREATE TABLE IF NOT EXISTS accesslogs (
id CHAR(36) PRIMARY KEY,
user_id CHAR(36),
entry_time TIMESTAMP NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL,
FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS contracts (
id CHAR(36) PRIMARY KEY,
user_id CHAR(36),
membership_id CHAR(36),
start_date DATE NOT NULL,
end_date DATE NOT NULL,
status VARCHAR(50) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
deleted_at TIMESTAMP NULL DEFAULT NULL,
FOREIGN KEY (user_id) REFERENCES users(id),
FOREIGN KEY (membership_id) REFERENCES memberships(id)
);

CREATE INDEX idx_users_role_id ON users(role_id);
CREATE INDEX idx_accesslogs_user_id ON accesslogs(user_id);
CREATE INDEX idx_contracts_user_id ON contracts(user_id);
CREATE INDEX idx_contracts_membership_id ON contracts(membership_id);

INSERT INTO roles (id, name) VALUES (UUID(), 'superuser');
INSERT INTO roles (id, name) VALUES (UUID(), 'admin');
INSERT INTO roles (id, name) VALUES (UUID(), 'employee');
INSERT INTO roles (id, name) VALUES (UUID(), 'trainer');
INSERT INTO roles (id, name) VALUES (UUID(), 'member');
INSERT INTO roles (id, name) VALUES (UUID(), 'visitor');

INSERT INTO functions (id, name, description) VALUES
(UUID(), 'manage_roles', 'Manage user roles and permissions'),
(UUID(), 'manage_functions', 'Manage system functions and capabilities'),
(UUID(), 'manage_roles_functions', 'Manage role functions and permissions'),
(UUID(), 'manage_admins', 'Manage administrators of the system'),
(UUID(), 'manage_employees', 'Manage gym employees'),
(UUID(), 'manage_trainers', 'Manage gym trainers'),
(UUID(), 'manage_members', 'Manage gym members'),
(UUID(), 'manage_visitors', 'Manage gym visitors'),
(UUID(), 'manage_selfies', 'Manage user selfies'),
(UUID(), 'manage_memberships', 'Manage gym memberships'),
(UUID(), 'manage_accesslogs', 'Manage user access logs'),
(UUID(), 'manage_contracts', 'Manage user contracts');

INSERT INTO rolefunctions (role_id, function_id) SELECT 
(SELECT id FROM roles WHERE name = 'superuser'), id FROM functions
WHERE name IN (
'manage_roqles',
'manage_functions',
'manage_roles_functions',
'manage_admins',
'manage_employees',
'manage_trainers',
'manage_members',
'manage_visitors',
'manage_selfies',
'manage_memberships',
'manage_accesslogs',
'manage_contracts'
);

INSERT INTO users (id, name, surname, email, password, role_id, pin)
VALUES (UUID(), 'Super','User', 'superuser@gymstration.dev', '8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92',
(SELECT id FROM roles WHERE name = 'superuser'), '123456');
```

[[gym_management_er_diagram_updated_4.png]]