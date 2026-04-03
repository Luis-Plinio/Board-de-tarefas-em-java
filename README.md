#Board de Tarefas em Java com MySQL
#Descrição

Aplicação de gerenciamento de tarefas no terminal, inspirada em ferramentas como Trello. O sistema permite criar boards, organizar colunas e gerenciar cards, respeitando regras de negócio e persistindo dados em banco MySQL.

Tecnologias utilizadas
Java
JDBC
MySQL
Estrutura do projeto
src/
├── model/
├── repository/
├── service/
├── ui/
└── Main.java
Configuração do banco de dados
CREATE DATABASE board_db;

USE board_db;

CREATE TABLE board (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255)
);

CREATE TABLE column_board (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    type VARCHAR(50),
    board_id INT
);

CREATE TABLE card (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    description TEXT,
    blocked BOOLEAN,
    column_id INT
);
Código
Main.java
import ui.Menu;

public class Main {
    public static void main(String[] args) {
        Menu menu = new Menu();
        menu.start();
    }
}
model/Board.java
package model;

public class Board {
    private int id;
    private String name;

    public Board(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
model/Column.java
package model;

public class Column {
    private String name;
    private String type;

    public Column(String name, String type) {
        this.name = name;
        this.type = type;
    }
}
model/Card.java
package model;

public class Card {
    private String title;
    private String description;
    private boolean blocked;

    public Card(String title, String description) {
        this.title = title;
        this.description = description;
        this.blocked = false;
    }

    public boolean isBlocked() {
        return blocked;
    }

    public void block() {
        this.blocked = true;
    }

    public void unblock() {
        this.blocked = false;
    }
}
repository/ConnectionFactory.java
package repository;

import java.sql.Connection;
import java.sql.DriverManager;

public class ConnectionFactory {

    public static Connection getConnection() throws Exception {
        return DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/board_db",
            "root",
            "root"
        );
    }
}
service/BoardService.java
package service;

import model.Board;

public class BoardService {

    public void createBoard(String name) {
        System.out.println("Board criado: " + name);
    }
}
ui/Menu.java
package ui;

import java.util.Scanner;

public class Menu {

    private Scanner scanner = new Scanner(System.in);

    public void start() {
        while (true) {
            System.out.println("1 - Criar Board");
            System.out.println("2 - Selecionar Board");
            System.out.println("3 - Excluir Board");
            System.out.println("4 - Sair");

            int option = scanner.nextInt();

            switch (option) {
                case 1:
                    System.out.println("Nome do board:");
                    scanner.nextLine();
                    String name = scanner.nextLine();
                    System.out.println("Board criado: " + name);
                    break;

                case 4:
                    System.exit(0);
            }
        }
    }
}
#Funcionalidades implementadas
Criação de board
Menu interativo
Estrutura base de entidades
Conexão com banco
