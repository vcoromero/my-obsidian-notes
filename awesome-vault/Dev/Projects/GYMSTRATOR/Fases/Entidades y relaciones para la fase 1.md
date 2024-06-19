#### Código sql para creación de tablas y relaciones

```sql
CREATE TABLE Roles (
    id UUID PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE Functions (
    id UUID PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE RoleFunctions (
    role_id UUID,
    function_id UUID,
    PRIMARY KEY (role_id, function_id),
    FOREIGN KEY (role_id) REFERENCES Roles(id),
    FOREIGN KEY (function_id) REFERENCES Functions(id)
);

CREATE TABLE Selfies (
    id UUID PRIMARY KEY,
    user_id UUID UNIQUE NOT NULL,
    image_path VARCHAR(255) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

CREATE TABLE Users (
    id UUID PRIMARY KEY,
    user_code INT UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role_id UUID,
    pin VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP,
    FOREIGN KEY (role_id) REFERENCES Roles(id)
);

CREATE TABLE Memberships (
    id UUID PRIMARY KEY,
    type VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL,
    duration INT NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE AccessLogs (
    id UUID PRIMARY KEY,
    user_id UUID,
    entry_time TIMESTAMP NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

CREATE TABLE Contracts (
    id UUID PRIMARY KEY,
    user_id UUID,
    membership_id UUID,
    start_date DATE NOT NULL,
    end_date DATE NOT NULL,
    status VARCHAR(255) NOT NULL,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    deleted_at TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id),
    FOREIGN KEY (membership_id) REFERENCES Memberships(id)
);

-- Índices para mejorar las consultas
CREATE INDEX idx_users_role_id ON Users(role_id);
CREATE INDEX idx_accesslogs_user_id ON AccessLogs(user_id);
CREATE INDEX idx_contracts_user_id ON Contracts(user_id);
CREATE INDEX idx_contracts_membership_id ON Contracts(membership_id);

```

[[gym_management_er_diagram_updated_4.png]]