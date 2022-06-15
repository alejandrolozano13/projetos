# projetos
Projeto destinado a um trabalho final para a disciplina de Laboratório de Programação, cujo tema foi escolhido como Banco de Sangue, onde é possível fazer login e listar doadores, assim como fazer a busca de tais.

# projects
Project intended for a final work for the Programming Laboratory discipline, whose theme was chosen as Blood Bank, where it is possible to login and list donors, as well as to search for them.


import java.util.Scanner;
import java.io.FileOutputStream;
import java.io.PrintWriter;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

public class cadastroPaciente {

    public static void main(String[] args) {
        Scanner leitor = new Scanner(System.in);
        int opcao;
        do {
            System.out.println("Escolha uma opção: ");
            System.out.println("\t 1 - Incluir Doador: ");
            System.out.println("\t 2 - Consultar Doador: ");
            System.out.println("\t 3 - Listar Doador: ");
            System.out.println("\t 4 - Sair ");
            opcao = leitor.nextInt();
            switch (opcao) {
                case 1:
                    incluirPaciente();
                    break;
                case 2:
                    pesquisarPaciente();
                    break;
                case 3:
                    listarPaciente();
                    break;
                case 4:
                    System.out.println("Saindo...");
                    break;
                default:
                    System.out.println("Opção Inválida...");
            }
        } while (opcao != 4);

        leitor.close();
    }

    public static void incluirPaciente() {
        // escritor
        try {
            FileOutputStream arquivo = new FileOutputStream("Paciente.txt", true);// Armazenando novas strings sendo
            // digitadas no arquivo.
            PrintWriter pr = new PrintWriter(arquivo);
            Scanner leitor = new Scanner(System.in);
            String nome, cpf, rg, tipoSangue, num;
            char tatuagens, resposta=0, ist;

            System.out.println("Nome completo:");
            nome = leitor.nextLine();
            System.out.println("CPF:");
            cpf = leitor.nextLine();
            System.out.println ("RG: ");
            rg = leitor.nextLine();
            System.out.println ("Possui tatuagens [S/N]? ");
            tatuagens = leitor.next().charAt(0);
            if (tatuagens == 'S' || tatuagens == 's'){
                System.out.println ("Fez alguma nos últimos 12 meses [S/N]? ");
                resposta = leitor.next().charAt(0);
            }
            if (resposta == 's' || resposta == 'S'){
                System.out.println ("Deverá esperar até completar 12 meses para doar.");
            }
            System.out.println ("Teve alguma IST recentemente [S/N]? ");
            ist = leitor.next().charAt(0);
            if (ist == 's' || ist == 'S'){
                System.out.println ("Consulte antes um médico para uma avaliação antes de doar.");
            }
            leitor.nextLine();
            System.out.println ("Tipo Sanguíneo: ");
            tipoSangue = leitor.nextLine();
            System.out.println ("Numero de Telefone p/ contato: ");
            num = leitor.nextLine();

            pr.println(nome + ";" + cpf);
            pr.println (num);
            pr.close();
            arquivo.close();

        } catch (Exception e) {
            System.out.println("Erro ao escrever o arquivo");
        }
    }

    public static void pesquisarPaciente() {
        // leitor
        try {
            FileInputStream arquivo = new FileInputStream("Paciente.txt");
            InputStreamReader input = new InputStreamReader(arquivo);
            BufferedReader br = new BufferedReader(input);
            Scanner leitor = new Scanner(System.in);
            String linha;
            String buscar;
            System.out.println("Insira o nome ou cpf do doador a buscar: ");
            buscar = leitor.nextLine();
            do {
                linha = br.readLine();
                if (linha.toLowerCase().contains(buscar.toLowerCase())) {
                    printarPaciente(linha);
                }
            } while (linha != null);
        } catch (Exception e) {

        }
    }

    public static void listarPaciente() {
        // leitor
        try {
            FileInputStream arquivo = new FileInputStream("Paciente.txt");
            InputStreamReader input = new InputStreamReader(arquivo);
            BufferedReader br = new BufferedReader(input);

            String linha;
            int pula = 0;
            do {
                linha = br.readLine();

                printarPaciente(linha);
            } while (linha != null);
        } catch (Exception e) {// pega a exceção e envia a mensagem de erro
            System.out.println("Erro ao ler o arquivo");
        }

    }

    public static void printarPaciente(String linha) {
        if (linha != null) {
            String[] split = linha.split(";");
            for (int i = 0; i < split.length; i++) {
                System.out.println("-" + split[i]);
            }
            System.out.println();
        }
    }

}
