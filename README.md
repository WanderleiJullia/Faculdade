# Faculdade
## Na atividade a seguir, possui o principal objetivo de estar realizando a utilização do Stored, armazenando tarefas repetitivas e aceitando parâmetros de entrada para que a tarefa seja efetuada de acordo com a necessidade individual. 

## 1º Faça a modelagem do banco e identifique as entidades, seus atributos e relacionamentos;
![image](https://github.com/WanderleiJullia/Faculdade/assets/144744092/362bd0b6-9dd3-4f04-982d-b4cdc97b8a7f)

## Na criação do maodelo logico, foi separado em três tabelas diferentes, Alunos, Cursos, Professor. 

## 2º Na transferência do modelo logico para o bancos de dados, foi utilizado o seguinte código. 

``` SQL
inserir aqui
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='TRADITIONAL,ALLOW_INVALID_DATES';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`Aluno`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Aluno` (
  `Id_Aluno` INT NOT NULL AUTO_INCREMENT,
  `Nome` VARCHAR(100) NULL,
  `RA` VARCHAR(45) NULL,
  `Email` VARCHAR(100) NULL,
  PRIMARY KEY (`Id_Aluno`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Curso`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Curso` (
  `Id_Curso` INT NOT NULL AUTO_INCREMENT,
  `NomeCurso` VARCHAR(100) NULL,
  PRIMARY KEY (`Id_Curso`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Professor`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Professor` (
  `Id_Professor` INT NOT NULL AUTO_INCREMENT,
  `NomeProf` VARCHAR(100) NULL,
  PRIMARY KEY (`Id_Professor`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Aluno_has_Curso`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Aluno_has_Curso` (
  `Aluno_Id_Aluno` INT NOT NULL,
  `Curso_Id_Curso` INT NOT NULL,
  PRIMARY KEY (`Aluno_Id_Aluno`, `Curso_Id_Curso`),
  INDEX `fk_Aluno_has_Curso_Curso1_idx` (`Curso_Id_Curso` ASC),
  INDEX `fk_Aluno_has_Curso_Aluno_idx` (`Aluno_Id_Aluno` ASC),
  CONSTRAINT `fk_Aluno_has_Curso_Aluno`
    FOREIGN KEY (`Aluno_Id_Aluno`)
    REFERENCES `mydb`.`Aluno` (`Id_Aluno`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Aluno_has_Curso_Curso1`
    FOREIGN KEY (`Curso_Id_Curso`)
    REFERENCES `mydb`.`Curso` (`Id_Curso`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`Curso_has_Professor`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`Curso_has_Professor` (
  `Curso_Id_Curso` INT NOT NULL,
  `Professor_Id_Professor` INT NOT NULL,
  PRIMARY KEY (`Curso_Id_Curso`, `Professor_Id_Professor`),
  INDEX `fk_Curso_has_Professor_Professor1_idx` (`Professor_Id_Professor` ASC),
  INDEX `fk_Curso_has_Professor_Curso1_idx` (`Curso_Id_Curso` ASC),
  CONSTRAINT `fk_Curso_has_Professor_Curso1`
    FOREIGN KEY (`Curso_Id_Curso`)
    REFERENCES `mydb`.`Curso` (`Id_Curso`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Curso_has_Professor_Professor1`
    FOREIGN KEY (`Professor_Id_Professor`)
    REFERENCES `mydb`.`Professor` (`Id_Professor`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```
## Criação das tabelas; 
![image](https://github.com/WanderleiJullia/Faculdade/assets/144744092/acb8993b-273a-4c33-95bf-580119bdcba4)

## Utilize Stored Procedures para automatizar a inserção e seleção dos cursos;
``` SQL
inserir aqui
delimiter $
create procedure Insert_cursos(
NomeCurso varchar(100)
)
begin 

insert into cursos (NomeCurso) values (NomeCurso);
end $ 
delimiter ;
```
## A inserção dos nomes do curso. 

``` SQL
Inserir aqui
delimiter $
create procedure select_cursos()
begin 
select * from cursos;
end $
delimiter ; 
```
## Seleção de cursos. 

![image](https://github.com/WanderleiJullia/Faculdade/assets/144744092/1b13b3e4-cc45-4cd7-9058-e229d1ddd2ff)


## O aluno possui um email que deve ter seu endereço gerado automaticamente no seguinte formato: nome.sobrenome@dominio.com 
## Como fica o email se duas pessoas tiverem o mesmo nome e sobrenome?
```SQL
Inserir aqui
DELIMITER $$
CREATE TRIGGER GenerateEmail
BEFORE INSERT ON alunos
FOR EACH ROW
BEGIN
  DECLARE email_count INT;
  SET email_count = 0;
  
 
  SELECT COUNT(*) INTO email_count FROM alunos WHERE email = CONCAT(NEW.nome, '.', NEW.nome , '@dominio.com');

  IF email_count > 0 THEN
    SET NEW.email = CONCAT(NEW.nome, '.', NEW.nome, email_count, '@dominio.com');
  ELSE
    SET NEW.email = CONCAT(NEW.nome, '.', NEW.nome, '@dominio.com');
  END IF;
END;
$$
DELIMITER ;
```
![image](https://github.com/WanderleiJullia/Faculdade/assets/144744092/f551f6f1-e79b-43c2-b295-23ea5122b069)

## Jullia Santos Wanderlei 
Bancos de Dados 
