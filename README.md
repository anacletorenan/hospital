# hospital
esse repositorio e uma modelagem de banco de dados para um hospital.

## descrição do hospital
Um pequeno hospital local busca desenvolver um novo sistema que atenda melhor às suas necessidades. Atualmente, parte da operação ainda se apoia em planilhas e arquivos antigos, mas espera-se que esses dados sejam transferidos para o novo sistema assim que ele estiver funcional. Neste momento, é necessário analisar com cuidado as necessidades desse cliente e sugerir uma estrutura de banco de dados adequada por meio de um Diagrama Entidade-Relacionamento.
Analise a seguinte descrição e extraia dela os requisitos para o banco de dados:
O hospital necessita de um sistema para sua área clínica que ajude a controlar consultas realizadas. Os médicos podem ser generalistas, especialistas ou residentes e têm seus dados pessoais cadastrados em planilhas digitais. Cada médico pode ter uma ou mais especialidades, que podem ser pediatria, clínica geral, gastroenterologia e dermatologia. Alguns registros antigos ainda estão em formulário de papel, mas será necessário incluir esses dados no novo sistema.

Os pacientes também precisam de cadastro, contendo dados pessoais (nome, data de nascimento, endereço, telefone e e-mail), documentos (CPF e RG) e convênio. Para cada convênio, são registrados nome, CNPJ e tempo de carência.

As consultas também têm sido registradas em planilhas, com data e hora de realização, médico responsável, paciente, valor da consulta ou nome do convênio, com o número da carteira. Também é necessário indicar na consulta qual a especialidade buscada pelo paciente.

Deseja-se ainda informatizar a receita do médico, de maneira que, no encerramento da consulta, ele possa registrar os medicamentos receitados, a quantidade e as instruções de uso. A partir disso, espera-se que o sistema imprima um relatório da receita ao paciente ou permita sua visualização via internet.


![image](https://github.com/anacletorenan/hospital/assets/160495498/c8b96328-7544-44c7-8d48-0abd5b66a7a4)

# Diagrama ER


![image](https://github.com/anacletorenan/hospital/assets/160495498/684f71f8-c7d8-4320-b789-ae2d29989264)


# scripts SQL

create database hospital;
use hospital;

create table medico (
codigo_medico int primary key,
nome_medico varchar(50) not null,
cpf_medico varchar(14) unique not null,
rg_medico varchar(9) unique not null,
cargo_medico varchar(20) not null, 
data_nasc_medico date not null
);
alter table medico modify cpf_medico varchar(11) unique not null;

create table paciente (
codigo_paciente int primary key,
nome_paciente varchar(50) not null,
cpf_paciente varchar(11) unique not null, 
rg_paciente varchar(9) unique not null, 
telefone_paciente varchar(11) not null,
email_paciente varchar(50) unique not null,
data_nasc_paciente date not null,
codigo_convenio int not null
);

alter table paciente change codigo_cargo codigo_convenio int not null;

create table convenio (
numero_carteira int primary key, 
nome_convenio varchar(50) not null,
tempo_carencia varchar(10) not null,
cnpj_convenio varchar(14) unique not null
);

alter table paciente add foreign key fk_codigo_convenio (codigo_convenio) references convenio(numero_carteira);

create table consulta(
codigo_consulta int primary key,
data_consulta date not null,
horario_consulta time not null,
valor_consulta decimal(5,2) not null,
forma_pagamento varchar(20) not null,
codigo_paciente int not null,
codigo_medico int not null, 
codigo_especialidade int not null
);

create table especialidade(
codigo_especialidade int primary key,
descricao_especialidade varchar(50) not null
);

create table especialidade_medico(
codigo_especialidade_medico int primary key,
codigo_medico int not null,
codigo_paciente int not null
);

alter table consulta add foreign key fk_codigo_especialidade (codigo_especialidade) references especialidade(codigo_especialidade);

alter table especialidade_medico add foreign key fk_codigo_medico (codigo_medico) references medico(codigo_medico);

alter table especialidade_medico add foreign key fk_codigo_paciente (codigo_paciente) references paciente(codigo_paciente);


codigo do oscar 

-- EX001
SELECT count(*) FROM indicados_ao_oscar 
where nome_do_indicado = 'natalie portman';
-- EX002
SELECT count(*) FROM indicados_ao_oscar 
where nome_do_indicado = 'natalie portman' AND vencedor = 'true';
-- EX003
SELECT count(*) FROM indicados_ao_oscar 
where nome_do_indicado = 'Amy dams';
-- EX004
SELECT COUNT(ano_cerimonia) FROM indicados_ao_oscar 
where nome_do_filme like '%Toy Story%' AND vencedor = 'true';

select MAX(ano_filmagem) from indicados_ao_oscar
where categoria = 'Actress';





CODIGO KAUE

-- 5 
DELETE FROM indicados_ao_oscar
WHERE Actress = % ;
 
-- 6 
SELECT nome_do_indicado, MIN(ano_filmagem)
FROM indicados_ao_oscar
WHERE categoria = 'Melhor Atriz' AND vencedor = 'Sim';
 
-- 7 UPDATE indicados_ao_oscar
SET vencedor = CASE 
    WHEN vencedor = 'Sim' THEN 1
    WHEN vencedor = 'Não' THEN 0
    ELSE vencedor
END;
 
-- 8 SELECT DISTINCT cerimonia
FROM indicados_ao_oscar
WHERE nome_do_filme LIKE '%Crash%';
 
-- 9 INSERT INTO indicados_ao_oscar (ano_filmagem, ano_cerimonia, cerimonia, categoria, nome_do_indicado, nome_do_filme, vencedor)
VALUES (2023, 2024, 96, '%', 'Great Film', 'The Great Movie', 'Sim');
 
-- 10 SELECT *
FROM indicados_ao_oscar
WHERE nome_do_filme LIKE '%Central do Brasil%';
 
-- 11 SELECT DISTINCT cerimonia
FROM indicados_ao_oscar
WHERE nome_do_filme LIKE '%Crash%';
 
-- 12 UPDATE indicados_ao_oscar
SET nome_do_filme = 'The Matrix 8', ano_filmagem = 2040
WHERE categoria = 'Melhor Filme' AND nome_do_indicado = 'Great Film' AND ano_filmagem = 2025;
 
-- 13 SELECT *
FROM indicados_ao_oscar
WHERE nome_do_filme LIKE '%Central do Brasil%';
 
-- 14 INSERT INTO indicados_ao_oscar (ano_filmagem,  nome_do_filme, vencedor)
VALUES 
(1987, 'The Wolf of Wall Street', 'Não'),
(2002, 'Cidade de Deus', 'Não'),
(1998, 'Central do Brasil', 'Não');
 
-- 15 SELECT nome_do_indicado, nome_do_filme, cerimonia
 
-- dar update p atualizar o database
FROM indicados_ao_oscar
 
WHERE categoria IN ('Uma Mente Brilhante', 'Jennifer Connelly', 'David Lean') AND ano_filmagem = 2002 AND vencedor = 'Sim';
