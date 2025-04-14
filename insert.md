# 📋 Dados de Inserção - Banco de Dados Oficina  

Abaixo estão as instruções SQL para popular o banco de dados da oficina com dados iniciais, abrangendo clientes, veículos, equipes, mecânicos, ordens de serviço, serviços, peças e detalhes relacionados.  

---

## 🧑‍💼 **Clientes**  

Tabela `Clients` populada com informações de clientes, incluindo nome, CPF, endereço e telefone.  

```sql
INSERT INTO Clients (Name, CPF, Address, Phone) VALUES
('Alice Ferreira', '12345678901', 'Av. Brasil, 123', '11987654321'),
('Miguel Silva', '98765432102', 'Rua das Palmeiras, 456', '11912345678'),
('Fernanda Souza', '45678912345', 'Av. Paulista, 789', '11965498732'),
('Carlos Lima', '78945612301', 'Rua dos Pinheiros, 321', '11985274136'),
('Juliana Oliveira', '12312312312', 'Rua da Liberdade, 654', '11995175382'),
('Pedro Santos', '65465465465', 'Rua do Sol, 234', '11954176398'),
('Mariana Rocha', '32132132132', 'Av. Central, 876', '11987651234'),
('João Martins', '98798798798', 'Rua das Acácias, 567', '11998761432'),
('Ana Costa', '55566677788', 'Av. Independência, 324', '11921346587'),
('Paulo Henrique', '88899900011', 'Rua das Flores, 890', '11932465871'),
('Cláudia Vieira', '12398765432', 'Rua do Carmo, 111', '11934567890'),
('Roberto Nunes', '98732165409', 'Av. dos Sonhos, 555', '11987654322'),
('Daniela Borges', '45612378909', 'Rua Jardim, 77', '11912398765'),
('Felipe Barros', '12345678912', 'Av. Verde, 99', '11965432188'),
('Simone Alves', '65478932145', 'Rua das Orquídeas, 33', '11987654333');

🚗 Veículos
Tabela Vehicles populada com informações dos veículos registrados, incluindo placa, marca, modelo, ano e cliente associado.

INSERT INTO Vehicles (LicensePlate, Brand, Model, Year, idClient) VALUES
('ABC1234', 'Toyota', 'Corolla', 2020, 1),
('DEF5678', 'Honda', 'Civic', 2019, 1),
('GHI9012', 'Ford', 'Focus', 2018, 2),
('JKL2345', 'Chevrolet', 'Cruze', 2021, 2),
('MNO6789', 'Volkswagen', 'Golf', 2022, 3),
('PQR3456', 'Hyundai', 'Elantra', 2020, 3),
('STU7890', 'Kia', 'Sportage', 2019, 4),
('VWX9012', 'Nissan', 'Sentra', 2021, 5),
('YZA2345', 'Fiat', 'Argo', 2020, 5),
('BCD5678', 'Jeep', 'Compass', 2023, 6),
('EFG4567', 'Toyota', 'Hilux', 2023, 7),
('HIJ7890', 'Honda', 'HR-V', 2022, 7),
('KLM0123', 'Ford', 'Fusion', 2021, 8),
('NOP3456', 'Chevrolet', 'Tracker', 2022, 9),
('QRS6789', 'Volkswagen', 'Polo', 2021, 10);

🛠️ Equipes
Tabela Teams populada com os nomes das equipes de trabalho.

INSERT INTO Teams (TeamName) VALUES
('Equipe Alfa'),
('Equipe Beta'),
('Equipe Gama'),
('Equipe Delta'),
('Equipe Épsilon'),
('Equipe Zeta'),
('Equipe Eta'),
('Equipe Teta'),
('Equipe Iota'),
('Equipe Kappa'),
('Equipe Lambda'),
('Equipe Mu'),
('Equipe Nu'),
('Equipe Xi'),
('Equipe Omicron');

🔧 Mecânicos
Tabela Mechanics com informações dos mecânicos, incluindo nome, endereço, especialidade e equipe associada.

INSERT INTO Mechanics (Name, Address, Specialty, idTeam) VALUES
('José Pereira', 'Rua A, 1', 'Motor', 1),
('Carlos Silva', 'Rua B, 2', 'Suspensão', 2),
('Ana Oliveira', 'Rua C, 3', 'Freios', 3),
('Marcos Lima', 'Rua D, 4', 'Transmissão', 4),
('Fernanda Souza', 'Rua E, 5', 'Pintura', 5),
('Ricardo Santos', 'Rua F, 6', 'Diagnóstico', 6),
('Juliana Silva', 'Rua G, 7', 'Eletrônica', 7),
('Pedro Alves', 'Rua H, 8', 'Troca de óleo', 8),
('Cláudia Costa', 'Rua I, 9', 'Refrigeração', 9),
('Márcio Almeida', 'Rua J, 10', 'Direção', 10),
('Sofia Almeida', 'Rua K, 11', 'Sistema elétrico', 11),
('Lucas Ribeiro', 'Rua L, 12', 'Ar condicionado', 12),
('Camila Nogueira', 'Rua M, 13', 'Motor esportivo', 13),
('Fábio Moreira', 'Rua N, 14', 'Revisão completa', 14),
('Lúcia Mendes', 'Rua O, 15', 'Suspensão esportiva', 15);

📄 Ordens de Serviço
Tabela ServiceOrders populada com informações de ordens, incluindo datas, status, valor total, veículo e equipe responsáveis.

INSERT INTO ServiceOrders (IssueDate, CompletionDate, Status, TotalValue, idVehicle, idTeam) VALUES
('2025-01-01', '2025-01-05', 'Concluído', 1500.00, 1, 1),
('2025-01-10', '2025-01-15', 'Concluído', 800.00, 2, 2),
('2025-02-01', '2025-02-07', 'Cancelado', 0.00, 3, 3),
('2025-03-01', '2025-03-10', 'Concluído', 1200.00, 4, 4),
('2025-04-01', NULL, 'Em andamento', 500.00, 5, 5),
('2025-05-01', '2025-05-05', 'Concluído', 700.00, 6, 6),
('2025-06-01', NULL, 'Em andamento', 350.00, 7, 7),
('2025-07-01', '2025-07-10', 'Concluído', 2200.00, 8, 8),
('2025-08-01', NULL, 'Em andamento', 400.00, 9, 9),
('2025-09-01', '2025-09-15', 'Concluído', 1800.00, 10, 10),
('2025-10-01', '2025-10-05', 'Concluído', 2500.00, 11, 2),
('2025-11-01', NULL, 'Em andamento', 700.00, 12, 3),
('2025-10-15', '2025-10-20', 'Concluído', 1200.00, 13, 4),
('2025-11-10', NULL, 'Em andamento', 400.00, 14, 5),
('2025-12-01', NULL, 'Em andamento', 550.00, 15, 6);

🛠️ Serviços e Peças
Serviços Referenciados
Tabela LaborReference com os tipos de serviços realizados e seus preços.

INSERT INTO LaborReference (Description, Price) VALUES
('Troca de óleo', 100.00),
('Troca de pneus', 300.00),
('Revisão geral', 500.00),
('Pintura', 800.00),
('Diagnóstico eletrônico', 150.00),
('Alinhamento e balanceamento', 200.00),
('Troca de pastilhas de freio', 250.00),
('Reparo de suspensão', 700.00),
('Revisão de motor', 1200.00),
('Reparo de transmissão', 900.00),
('Troca de filtro de ar', 80.00),
('Revisão elétrica', 400.00),
('Reparo de climatização', 600.00),
('Troca de bateria', 350.00),
('Instalação de acessórios', 500.00);

Peças Utilizadas
Tabela Parts populada com informações de peças e seus preços.

INSERT INTO Parts (Name, Price) VALUES
('Filtro de óleo', 50.00),
('Velas de ignição', 100.00),
('Pastilhas de freio', 200.00),
('Amortecedores', 300.00),
('Bateria', 400.00),
('Pneus', 500.00),
('Parafusos', 20.00),
('Radiador', 600.00),
('Correia dentada', 150.00),
('Alternador', 800.00),
('Filtro de ar', 80.00),
('Sensor de temperatura', 120.00),
('Compressor de ar condicionado', 700.00),
('Bomba de combustível', 450.00),
('Cabos de vela', 200.00);
