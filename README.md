# Taller_MySQL
## Base de datos
```sql
CREATE DATABASE vtaszfs;
USE vtaszfs;

-- Tabla Clientes

CREATE TABLE Clientes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);

-- Tabla Ubicación de Clientes

CREATE TABLE UbicacionCliente (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT NOT NULL,
    direccion VARCHAR(255) NOT NULL,
    ciudad VARCHAR(100) NOT NULL,
    estado VARCHAR(50),
    codigo_postal VARCHAR(10),
    pais VARCHAR(50),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

-- Tabla Contactos de Clientes

CREATE TABLE ContactoCliente (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT NOT NULL,
    telefono VARCHAR(20),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id)
);

-- Tabla Empleados

CREATE TABLE Empleados (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    puesto VARCHAR(50) NOT NULL,
    salario DECIMAL(10, 2) NOT NULL,
    fecha_contratacion DATE NOT NULL
);

-- Tabla Puestos

CREATE TABLE Puestos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(80) NOT NULL
);

-- Tabla Datos de Empleados

CREATE TABLE DatosEmpleado (
    id INT PRIMARY KEY AUTO_INCREMENT,
    empleado_id INT NOT NULL,
    salario_anterior DECIMAL(10, 2),
    fecha_modificacion DATE,
    FOREIGN KEY (empleado_id) REFERENCES Empleados(id)
);

-- Tabla Proveedores

CREATE TABLE Proveedores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    contacto VARCHAR(100),
    telefono VARCHAR(20),
    direccion VARCHAR(255)
);

-- Tabla Contactos de Proveedores

CREATE TABLE ProveedorContactos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    proveedor_id INT NOT NULL,
    contacto VARCHAR(100),
    telefono VARCHAR(20),
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id)
);

-- Tabla Tipos de Productos

CREATE TABLE TiposProductos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    tipo_nombre VARCHAR(100) NOT NULL,
    descripcion TEXT
);

-- Tabla Productos

CREATE TABLE Productos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    precio DECIMAL(10, 2) NOT NULL,
    proveedor_id INT NOT NULL,
    tipo_id INT NOT NULL,
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id),
    FOREIGN KEY (tipo_id) REFERENCES TiposProductos(id)
);

-- Tabla Inventario de Productos

CREATE TABLE InventarioProductos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    producto_id INT NOT NULL,
    cantidad INT NOT NULL,
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

-- Tabla Pedidos

CREATE TABLE Pedidos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    cliente_id INT NOT NULL,
    empleado_id INT NOT NULL,
    fecha DATE NOT NULL,
    total DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES Clientes(id),
    FOREIGN KEY (empleado_id) REFERENCES Empleados(id)
);

-- Tabla Detalles de Pedidos

CREATE TABLE DetallesPedido (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pedido_id INT NOT NULL,
    producto_id INT NOT NULL,
    cantidad INT NOT NULL,
    precio DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);

-- Tabla Historial de Pedidos

CREATE TABLE HistorialPedidos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pedido_id INT NOT NULL,
    fecha_modificacion DATETIME DEFAULT CURRENT_TIMESTAMP,
    comentarios TEXT,
    FOREIGN KEY (pedido_id) REFERENCES Pedidos(id)
);

-- Tabla País

CREATE TABLE Pais (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(80) NOT NULL
);

-- Tabla Región

CREATE TABLE Region (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(80) NOT NULL
);

-- Tabla Ciudad

CREATE TABLE Ciudad (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(80) NOT NULL
);

-- Tabla Ubicación

CREATE TABLE Ubicacion (
    id INT PRIMARY KEY AUTO_INCREMENT,
    pais_id INT NOT NULL,
    direccion VARCHAR(255),
    region_id INT NOT NULL,
    ciudad_id INT NOT NULL,
    FOREIGN KEY (pais_id) REFERENCES Pais(id),
    FOREIGN KEY (region_id) REFERENCES Region(id),
    FOREIGN KEY (ciudad_id) REFERENCES Ciudad(id)
);

-- Tabla Sucursales

CREATE TABLE Sucursal (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(80) NOT NULL,
    ubicacion_id INT NOT NULL,
    ciudad_id INT NOT NULL,
    proveedor_id INT NOT NULL,
    FOREIGN KEY (ubicacion_id) REFERENCES Ubicacion(id),
    FOREIGN KEY (ciudad_id) REFERENCES Ciudad(id),
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(id)
);

-- Tabla Ingreso de Productos

CREATE TABLE ProductoIngreso (
    id INT PRIMARY KEY AUTO_INCREMENT,
    producto_id INT NOT NULL,
    descripcion VARCHAR(255),
    faltantes VARCHAR(80),
    FOREIGN KEY (producto_id) REFERENCES Productos(id)
);
```
