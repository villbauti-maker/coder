# coder
[ventas_tech_db.sql](https://github.com/user-attachments/files/32712357/ventas_tech_db.sql)
-- =======================================================
-- Base de Datos: Ventas_Tech_DB
-- Checkpoint Módulo 3: Ingeniería de Datos / SQL
-- =======================================================

-- =======================================================
-- SECCIÓN 1: DROP TABLES (Orden inverso a dependencias)
-- =======================================================
DROP TABLE IF EXISTS ventas;
DROP TABLE IF EXISTS productos;
DROP TABLE IF EXISTS clientes;
DROP TABLE IF EXISTS categorias;

-- =======================================================
-- SECCIÓN 2: CREATE TABLES (DDL)
-- =======================================================

-- 1. Tabla categorias
CREATE TABLE categorias (
    id_categoria INT PRIMARY KEY,
    nombre_categoria VARCHAR(50) NOT NULL,
    descripcion VARCHAR(200)
);

-- 2. Tabla clientes
CREATE TABLE clientes (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    ciudad VARCHAR(50),
    fecha_registro DATE NOT NULL
);

-- 3. Tabla productos
CREATE TABLE productos (
    id_producto INT PRIMARY KEY,
    nombre_producto VARCHAR(100) NOT NULL,
    id_categoria INT NOT NULL,
    precio DECIMAL(10,2) NOT NULL,
    stock INT DEFAULT 0,
    activo BIT DEFAULT 1,
    CONSTRAINT fk_productos_categorias FOREIGN KEY (id_categoria) 
        REFERENCES categorias(id_categoria)
);

-- 4. Tabla ventas
CREATE TABLE ventas (
    id_venta INT PRIMARY KEY,
    id_cliente INT NOT NULL,
    id_producto INT NOT NULL,
    cantidad INT NOT NULL,
    precio_unitario DECIMAL(10,2) NOT NULL,
    fecha_venta DATE NOT NULL,
    CONSTRAINT fk_ventas_clientes FOREIGN KEY (id_cliente) 
        REFERENCES clientes(id_cliente),
    CONSTRAINT fk_ventas_productos FOREIGN KEY (id_producto) 
        REFERENCES productos(id_producto)
);

-- =======================================================
-- SECCIÓN 3: INSERT INTO (DML - Datos de prueba)
-- =======================================================

-- Cargar categorias
INSERT INTO categorias (id_categoria, nombre_categoria, descripcion) VALUES
(1, 'Laptops', 'Equipos portátiles para trabajo y gaming'),
(2, 'Smartphones', 'Teléfonos móviles y accesorios'),
(3, 'Audio', 'Auriculares, parlantes y micrófonos');

-- Cargar clientes
INSERT INTO clientes (id_cliente, nombre, email, ciudad, fecha_registro) VALUES
(1, 'Lucas Gómez', 'lucas.gomez@email.com', 'Buenos Aires', '2024-01-15'),
(2, 'Sofía Rodríguez', 'sofia.r@email.com', 'Córdoba', '2024-02-10'),
(3, 'Martín Silva', 'martin.silva@email.com', 'Rosario', '2024-03-05');

-- Cargar productos
INSERT INTO productos (id_producto, nombre_producto, id_categoria, precio, stock, activo) VALUES
(101, 'Notebook ThinkPad 14"', 1, 850.00, 15, 1),
(102, 'iPhone 13 128GB', 2, 750.00, 20, 1),
(103, 'Auriculares Sony WH-1000XM4', 3, 280.00, 30, 1),
(104, 'MacBook Air M2', 1, 1100.00, 10, 1);

-- Cargar ventas
INSERT INTO ventas (id_venta, id_cliente, id_producto, cantidad, precio_unitario, fecha_venta) VALUES
(1001, 1, 101, 1, 850.00, '2024-03-10'),
(1002, 2, 103, 2, 280.00, '2024-03-12'),
(1003, 3, 102, 1, 750.00, '2024-03-15'),
(1004, 1, 104, 1, 1100.00, '2024-03-20');

-- =======================================================
-- SECCIÓN 4: VALIDACIÓN
-- =======================================================
SELECT * FROM categorias;
SELECT * FROM clientes;
SELECT * FROM productos;
SELECT * FROM ventas;

