La tabla de funciones tendrá los siguientes datos:
- Id
- name
- description
- created_at
- updates_at
- deleted_at

Los roles podrán tener algunas de estas funcionalidades:

1. **Gestionar roles** ('manage_roles', 'Gestionar roles de usuario y permisos')
   - Administración de los diferentes roles de usuarios dentro del sistema, definiendo y controlando los permisos y accesos correspondientes a cada rol.

2. **Gestionar funcionalidades** ('manage_functions', 'Gestionar funciones y capacidades del sistema')
   - Manejo de las diversas funciones y capacidades que el sistema ofrece, permitiendo definir qué acciones específicas pueden realizar los usuarios.

3. **Gestionar roles y funciones** ('manage_roles_functions', 'Gestionar funciones de roles y permisos')
   - Control y asignación de funciones CREATE DATABASE IF NOT EXISTS gymstration DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;

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

INSERT INTO rolefunctions (role_id, function_id)
SELECT
    (SELECT id FROM roles WHERE name = 'superuser'),
    id
FROM functions
WHERE name IN (
    'manage_roles',
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
(SELECT id FROM roles WHERE name = 'superuser'), '123456');específicas a los diferentes roles de usuario, gestionando las capacidades y permisos de cada rol.

4. **Gestionar administradores** ('manage_admins', 'Gestionar administradores del sistema')
   - Administración de los usuarios con privilegios de administrador, quienes supervisan y gestionan el funcionamiento general del sistema.

5. **Gestionar empleados** ('manage_employees', 'Gestionar empleados del gimnasio')
   - Gestión del personal del gimnasio, incluyendo recepcionistas y personal de limpieza, para el control del funcionamiento diario.

6. **Gestionar entrenadores** ('manage_trainers', 'Gestionar entrenadores del gimnasio')
   - Administración de los entrenadores que interactúan con los miembros y ofrecen servicios de entrenamiento, asegurando la calidad y programación adecuada de los entrenamientos.

7. **Gestionar miembros** ('manage_members', 'Gestionar miembros del gimnasio')
   - Registro, actualización de datos y seguimiento de la actividad de los miembros del gimnasio, una función fundamental para cualquier sistema de gestión de gimnasio.

8. **Gestionar visitantes** ('manage_visitors', 'Gestionar visitantes del gimnasio')
   - Manejo de los pases diarios o visitantes que no son miembros regulares, ayudando a convertir potenciales visitantes en miembros.

9. **Gestionar selfies** ('manage_selfies', 'Gestionar selfies de usuarios')
   - Administración de las selfies de los usuarios, utilizadas para propósitos de verificación y seguridad dentro del gimnasio.

10. **Gestionar membresías** ('manage_memberships', 'Gestionar membresías del gimnasio')
    - Administración de los tipos de membresías, precios, duraciones y condiciones, crucial para la generación de ingresos y retención de miembros.

11. **Gestionar registros de acceso** ('manage_accesslogs', 'Gestionar registros de acceso de usuarios')
    - Registro y seguimiento de las asistencias y accesos de miembros y personal, importante para análisis y control de uso de las instalaciones.

12. **Gestionar contratos** ('manage_contracts', 'Gestionar contratos de usuarios')
    - Administración de la contratación de nuevos miembros y la renovación de membresías existentes, manteniendo el flujo de ingresos y asegurando la continuidad del uso del gimnasio.