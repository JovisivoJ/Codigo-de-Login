_# Codigo-de-Login
é um codigo para ajudar desenvolvedores de apps com a parte de login ou criação de conta ou usuário 
uso para JAVA e recomendo fortemente o uso de eclipse IDE ou netbeans IDE


import java.io.*;
import java.util.*;

public class (nome do seu arquivo) {
	private static final String FILE_NAME = "users.txt";

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);

		while (true) {
			System.out.println("\n1 - Criar Conta\n2 - Fazer Login\n3 - Sair");
			System.out.print("Escolha uma opção: ");
			int option = scanner.nextInt();
			scanner.nextLine(); // Consumir quebra de linha

			switch (option) {
			case 1:
				criarConta(scanner);
				break;
			case 2:
				fazerLogin(scanner);
				break;
			case 3:
				System.out.println("Saindo...");
				scanner.close();
				return;
			default:
				System.out.println("Opção inválida!");
			}
		}
	}

	private static void criarConta(Scanner scanner) {
		System.out.print("Digite um nome de usuário: ");
		String username = scanner.nextLine();
		System.out.print("Digite uma senha: ");
		String password = scanner.nextLine();

		if (usuarioExiste(username)) {
			System.out.println("Usuário já existe! Escolha outro nome.");
			return;
		}

		try (FileWriter writer = new FileWriter(FILE_NAME, true)) {
			writer.write(username + "," + password + "\n");
			System.out.println("Conta criada com sucesso!");
		} catch (IOException e) {
			System.out.println("Erro ao salvar usuário: " + e.getMessage());
		}
	}

	private static void fazerLogin(Scanner scanner) {
		System.out.print("Nome de usuário: ");
		String username = scanner.nextLine();
		System.out.print("Senha: ");
		String password = scanner.nextLine();

		if (verificarCredenciais(username, password)) {
			System.out.println("Login bem-sucedido! Bem-vindo, " + username);
		} else {
			System.out.println("Nome de usuário ou senha incorretos.");
		}
	}

	private static boolean usuarioExiste(String username) {
		try (BufferedReader reader = new BufferedReader(new FileReader(FILE_NAME))) {
			String line;
			while ((line = reader.readLine()) != null) {
				String[] parts = line.split(",");
				if (parts[0].equals(username)) {
					return true;
				}
			}
		} catch (IOException e) {
			System.out.println("Erro ao verificar usuário: " + e.getMessage());
		}
		return false;
	}

	private static boolean verificarCredenciais(String username, String password) {
		try (BufferedReader reader = new BufferedReader(new FileReader(FILE_NAME))) {
			String line;
			while ((line = reader.readLine()) != null) {
				String[] parts = line.split(",");
				if (parts.length == 2 && parts[0].equals(username) && parts[1].equals(password)) {
					return true;
				}
			}
		} catch (IOException e) {
			System.out.println("Erro ao verificar login: " + e.getMessage());
		}
		return false;
	}
}

_
