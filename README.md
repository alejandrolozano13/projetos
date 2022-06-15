# projetos
Projeto destinado a um trabalho final para a disciplina de Laboratório de Programação, cujo tema foi escolhido como Banco de Sangue, onde é possível fazer login e listar doadores, assim como fazer a busca de tais.
pacote  faculdade . semestre . primeiro . lista5 ;

importar  java . útil . Scanner ;
importar  java . io . FileOutputStream ;
importar  java . io . PrintWriter ;
importar  java . io . Leitor Buffer ;
importar  java . io . FileInputStream ;
importar  java . io . Leitor de Entrada ;

public  class  cadastroPaciente {

    public  static  void  main ( String [] args ) {
         Leitor de scanner = novo  Scanner ( System . in );
        int  opcao ;
        fazer {
            Sistema . fora . println ( "Escolher uma opção: " );
            Sistema . fora . println ( "\t 1 - Incluir Doador: " );
            Sistema . fora . println ( "\t 2 - Consultar Doador: " );
            Sistema . fora . println ( "\t 3 - Listar Doador: " );
            Sistema . fora . println ( "\t 4 - Sair" );
            opcao = leitor . nextInt ();
            switch ( opcao ) {
                caso  1 :
                    incluirPaciente ();
                    quebrar ;
                caso  2 :
                    pesquisaPaciente ();
                    quebrar ;
                caso  3 :
                    listarPaciente ();
                    quebrar ;
                caso  4 :
                    Sistema . fora . println ( "Saindo..." );
                    quebrar ;
                padrão :
                    Sistema . fora . println ( "Opção Inválida..." );
            }
        } while ( opcao != 4 );

        leitor . fechar ();
    }

    public  static  void  incluirPaciente () {
        // escritor
        tente {
            FileOutputStream  arquivo = new  FileOutputStream ( "Paciente.txt" , true ); // Armazenando novas strings sendo
            // digitadas no arquivo.
            PrintWriter  pr = new  PrintWriter ( arquivo );
             Leitor de scanner = novo  Scanner ( System . in );
            String  nome , cpf , rg , tipoSangue , num ;
            char  tatuagens , resposta = 0 , ist ;

            Sistema . fora . println ( "Nome completo:" );
            nome = leitor . próximaLinha ();
            Sistema . fora . println ( "CPF:" );
            cpf = leitor . próximaLinha ();
            Sistema . fora . println ( "RG:" );
            rg = leitor . próximaLinha ();
            Sistema . fora . println ( "Possui tatuagens [S/N]? " );
            tatuagens = leitor . seguinte (). charAt ( 0 );
            if ( tatuagens == 'S' || tatuagens == 's' ){
                Sistema . fora . println ( "Fez alguma nos últimos 12 meses [S/N]?" );
                resposta = leitor . seguinte (). charAt ( 0 );
            }
            if ( resposta == 's' || resposta == 'S' ){
                Sistema . fora . println ( "Deverá esperar até completar 12 meses para doar." );
            }
            Sistema . fora . println ( "Teve alguma IST recentemente [S/N]?" );
            ist = leitor . seguinte (). charAt ( 0 );
            if ( ist == 's' || ist == 'S' ){
                Sistema . fora . println ( "Consulte antes um médico para uma avaliação antes de doar." );
            }
            leitor . próximaLinha ();
            Sistema . fora . println ( "Tipo Sanguíneo: " );
            tipo Sangue = leitor . próximaLinha ();
            Sistema . fora . println ( "Número de Telefone p/ contato: " );
            num = leitor . próximaLinha ();

            pr . println ( nome + ";" + cpf );
            pr . println ( num );
            pr . fechar ();
            arquivo . fechar ();

        } catch ( Exceção  e ) {
            Sistema . fora . println ( "Erro ao escrever o arquivo" );
        }
    }

    public  static  void  pesquisarPaciente () {
        // leitor
        tente {
            FileInputStream  arquivo = new  FileInputStream ( "Paciente.txt" );
            InputStreamReader  input = new  InputStreamReader ( arquivo );
            BufferedReader  br = new  BufferedReader ( input );
             Leitor de scanner = novo  Scanner ( System . in );
            Linha  linha ;
             Busca de string ;
            Sistema . fora . println ( "Insira o nome ou cpf doador a buscar: " );
            buscar = leitor . próximaLinha ();
            fazer {
                linha = br . leiaLinha ();
                if ( linha . toLowerCase (). contém ( buscar . toLowerCase ())) {
                    printarPaciente ( linha );
                }
            } while ( linha != null );
        } catch ( Exceção  e ) {

        }
    }

    public  static  void  listarPaciente () {
        // leitor
        tente {
            FileInputStream  arquivo = new  FileInputStream ( "Paciente.txt" );
            InputStreamReader  input = new  InputStreamReader ( arquivo );
            BufferedReader  br = new  BufferedReader ( input );

            Linha  linha ;
            int  pula = 0 ;
            fazer {
                linha = br . leiaLinha ();

                printarPaciente ( linha );
            } while ( linha != null );
        } catch ( Exception  e ) { // pega a exceção e envia a mensagem de erro
            Sistema . fora . println ( "Erro ao ler o arquivo" );
        }

    }

    public  static  void  printarPaciente ( String  linha ) {
        if ( linha != null ) {
            String [] split = linha . divisão ( ";" );
            for ( int  i = 0 ; i < split . length ; i ++) {
                Sistema . fora . println ( "-" + split [ i ]);
            }
            Sistema . fora . println ();
        }
    }

}
