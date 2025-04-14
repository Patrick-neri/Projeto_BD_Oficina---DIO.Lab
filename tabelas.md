# 📋 Projeto Banco de Dados Oficina - DIO.Lab  

Este projeto consiste na modelagem e construção de um banco de dados para uma oficina mecânica. O esquema SQL inclui tabelas como `Clients`, `Vehicles`, `Teams`, `Mechanics`, `ServiceOrders`, entre outras, com relacionamentos bem definidos usando **chaves primárias**, **chaves estrangeiras** e **constraints**.  


---

OBS: Projeto ainda em atualização.

## 🛠️ Estrutura do Banco de Dados  

### **1️⃣ Tabela `Clients`**  
Armazena informações dos clientes da oficina.  
- Cada cliente possui um CPF único e opcionalmente endereço e telefone.  

```sql
CREATE TABLE Clients (
    idClient INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    CPF CHAR(11) NOT NULL UNIQUE,
    Address VARCHAR(255),
    Phone CHAR(11)
);

2️⃣ Tabela Vehicles
Armazena os veículos registrados na oficina.

CREATE TABLE Vehicles (
    idVehicle INT AUTO_INCREMENT PRIMARY KEY,
    LicensePlate CHAR(7) NOT NULL UNIQUE,
    Brand VARCHAR(50),
    Model VARCHAR(50),
    Year INT,
    idClient INT NOT NULL,
    CONSTRAINT fk_vehicle_client FOREIGN KEY (idClient) REFERENCES Clients(idClient)
);

3️⃣ Tabela Teams
Armazena informações das equipes de trabalho da oficina.

CREATE TABLE Teams (
    idTeam INT AUTO_INCREMENT PRIMARY KEY,
    TeamName VARCHAR(50) NOT NULL
);

4️⃣ Tabela Mechanics
Armazena informações dos mecânicos da oficina.

CREATE TABLE Mechanics (
    idMechanic INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Address VARCHAR(255),
    Specialty VARCHAR(100),
    idTeam INT NOT NULL,
    CONSTRAINT fk_mechanic_team FOREIGN KEY (idTeam) REFERENCES Teams(idTeam)
);

5️⃣ Tabela ServiceOrders
Registra as ordens de serviço da oficina.

CREATE TABLE ServiceOrders (
    idOrder INT AUTO_INCREMENT PRIMARY KEY,
    IssueDate DATE NOT NULL,
    CompletionDate DATE,
    Status ENUM('Em andamento', 'Concluído', 'Cancelado') DEFAULT 'Em andamento',
    TotalValue DECIMAL(10, 2) DEFAULT 0.00,
    idVehicle INT NOT NULL,
    idTeam INT NOT NULL,
    CONSTRAINT fk_order_vehicle FOREIGN KEY (idVehicle) REFERENCES Vehicles(idVehicle),
    CONSTRAINT fk_order_team FOREIGN KEY (idTeam) REFERENCES Teams(idTeam)
);

6️⃣ Tabela LaborReference
Armazena os tipos de serviços realizados pela oficina.

CREATE TABLE LaborReference (
    idLabor INT AUTO_INCREMENT PRIMARY KEY,
    Description VARCHAR(255) NOT NULL,
    Price DECIMAL(10, 2) NOT NULL
);

7️⃣ Tabela ServiceDetails
Relaciona ordens de serviço com os serviços realizados.

CREATE TABLE ServiceDetails (
    idServiceDetail INT AUTO_INCREMENT PRIMARY KEY,
    idOrder INT NOT NULL,
    idLabor INT NOT NULL,
    Quantity INT DEFAULT 1,
    TotalPrice DECIMAL(10, 2) NOT NULL,
    CONSTRAINT fk_service_order FOREIGN KEY (idOrder) REFERENCES ServiceOrders(idOrder),
    CONSTRAINT fk_service_labor FOREIGN KEY (idLabor) REFERENCES LaborReference(idLabor)
);

8️⃣ Tabela Parts
Armazena informações sobre as peças utilizadas nos serviços da oficina.

CREATE TABLE Parts (
    idPart INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Price DECIMAL(10, 2) NOT NULL
);

9️⃣ Tabela PartsUsed
Relaciona ordens de serviço com as peças utilizadas.

CREATE TABLE PartsUsed (
    idPartUsed INT AUTO_INCREMENT PRIMARY KEY,
    idOrder INT NOT NULL,
    idPart INT NOT NULL,
    Quantity INT DEFAULT 1,
    TotalPrice DECIMAL(10, 2) NOT NULL,
    CONSTRAINT fk_part_order FOREIGN KEY (idOrder) REFERENCES ServiceOrders(idOrder),
    CONSTRAINT fk_part_part FOREIGN KEY (idPart) REFERENCES Parts(idPart)
);
