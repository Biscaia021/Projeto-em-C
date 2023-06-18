# Projeto-em-C
Jogo da velha, da forca e de advinhação com menu


#include<stdio.h> //cabeçalho para a entrada de dados
#include<stdlib.h>//entrada de dados
#include<ctype.h>//classificação de caracteres
#include<string.h>//manipulação de caractres
#include<time.h>//manipulação de horário
#include <locale.h> //caracteres para o portugues
void tabuleiro(char casas2 [3] [3]){ //MONTAGEM DA CONTRUÇÃO DO GRÁFICO DO JOGO DA VELHA, O VOID VAI SER PUXADO PELA ESTRURA DO MAIN
system("cls");
printf("\t%c|%c|%c\n", casas2[0] [0], casas2[0] [1], casas2[0] [2]);
printf("\t--------\n");
printf("\t%c|%c|%c\n", casas2[0] [0], casas2[1] [1], casas2[1] [2]);
printf("\t--------\n");
printf("\t%c|%c|%c\n", casas2[0] [0], casas2[2] [1], casas2[2] [2]);
}

void forca(int estado){ // estrutura para o jogo, será chamada essa funcção com os comandos dentro do main
if(estado == 0){
printf("\n--------------");
printf("\n| |");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
} else if(estado == 1){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
}else if(estado == 2){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n| |");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
}else if(estado == 3){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n| -|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
}else if(estado == 4){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n| -|-");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
}else if(estado == 5){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n| -|-");
printf("\n| /");
printf("\n|");
printf("\n|");
printf("\n|");
printf("\n-");
}else if(estado == 6){
printf("\n--------------");
printf("\n| |");
printf("\n| O");
printf("\n| -|-");
printf("\n| / \");
printf("\n|");
printf("\n|");
printf("\n| You lose!! :(");
printf("\n-");
}

}

int main (){

  setlocale(LC_ALL, "Portuguese"); // biblioteca locale.h
int menu; // montagem do menu de jogos

do {
printf("\n\n MENU DE JOGOS \n\n");
printf("1. JOGO DE ADIVINHAÇÃO\n");
printf("2. JOGO DA FORCA \n");
printf("3. JOGO DA VELHA \n");
printf("4. SAIR\n");

printf("ESCOLHA UMA OPÇÃO: ");
scanf("%d", &menu);
switch(menu){
case 1: //instruções dentro do case para a montagem do jogo de advinhação
printf("\n VOCÊ ESCOLHEU O JOGO DE ADIVINHAÇÃO\n");

int op; // MENU INICIAL
printf("\tBEM-VINDO AO JOGO \n\n");
printf("ESCOLHA UMA OPÇÃO:\n");
printf("(1) JOGAR\n");
printf("(2) SAIR\n");
printf("OÇÃO: ");
scanf("%d",&op);
int num, nums, tent=0;
char ch;

srand(time(NULL));
nums = (rand() % 100) +1;//função que retorna um numero randomico de 0 a 100 para a variavel nums

do{
tent++;//adiciona mais um ao número de tentativas
printf("\nTENTATIVA DE NÚMERO %d ", tent);
printf("\nTENTE ADVINHAR O NÚMERO SECRETO: ");
scanf("%d", &num);

if(num==nums){//se numero = numero sorteado, vc ganhou
  printf("\nPARABÉNS!! VOCÊ ACERTOU O NÚMERO!!");
  break;
}

if(num<nums){//se numero != numero sorteado, vc perdeu e informa se é menor ou maior que o numero sorteado
  printf("\nPOXA, VOCÊ ERROU! :(");
  printf("\nTENTE UM NÚMERO MAIOR");
} else {
  printf("\nPOXA, VOCÊ ERROU! :(");
  printf("\nTENTE UM NÚMERO MENOR");
}

printf("\nDESEJA TENTAR NOVAMENTE? (S/N) ");
fflush(stdin);//limpa o buffer do teclado para evitar erros com o scanf usado repetidamentre dentro do laço
scanf(" %c", &ch);
}while(ch=='s' || ch=='S' ); // enquanto para o carater "S"(minúsculo/maiúsculo) - se vc usar esse comando vc continua com as tentativas

break; // termina o laço e joga para o próximo jogo

case 2:
printf("\n VOCÊ ESCOLHEU O JOGO DA FORCA\n");

  int erros = 0;
char psec[100]; //palavra secreta com até 100 caracteres, usando vetor de string

printf("PALAVRA SECRETA: ");
scanf("%s", psec); //lê palavras com espaçamento
printf("A PALAVRA SECRETA É: %s", psec);
printf("\nA PALAVRA TEM %lu CARACTERES", strlen(psec));//strlen para saber o tamanho da palavra e o -1 pois ele conta com o enter, assim tirando o caracter inutilizado
for(int i=0; i<50; i++){
printf("\n\n");
}

char ptela[100]; //palavra que aparece na tela
strcpy(ptela, psec); //copia o conteudo da psec para a ptela

for(int i=0; i<strlen(ptela);i++){ //adiciona um até bater a quantidade de caracteres
ptela[i]='_'; //ptela na posição i recebe _
}

while(1){

forca(erros);//imprime a forca com base no número de erros
//chamando a instrução do void no ínicio

printf("\nADIVINHE: ");
for(int i=0; i<strlen(ptela); i++){ //da espaço entre os caracteres do "adivinhe"
  printf("%c ", ptela[i]);
}

printf("\nLETRA: ");
char letra;
scanf(" %c", &letra); //captura a letra
int errou = 1; //1= sim 0= não

for(int i=0; i<strlen(ptela); i++){
  if(letra==psec[i]){ //certo
    ptela[i]=letra;
    errou= 0; // não errou
  }
}
if(errou== 1){ //incrementa erros para avançar a imagem da forca
  erros++;
}

if(strcmp(ptela, psec)== 0){ //se as duas são iguais e encerra no caso da vitória

  printf("\nA PALAVRA SECRETA ERA: ");
for(int i=0; i<strlen(ptela); i++){ //quando eu erro todoas as tentativas ele não retorna com a palavra secreta
  printf("%c", ptela[i]);
}
  printf("\n VOCÊ GANHOU!! :)");
  printf("\nPARABÉNS!!");
  break;
}

if(erros== 6){ //identifica o erro e encerra no caso da derrota
  forca(erros);
  break;
}
}
break;
case 3:
printf("\n VOCÊ ESCOLHEU O JOGO DA VELHA \n");
// estrutura de dados?
int l, c, linha, coluna, jogador, ganhou, jogadas, opcao;
char jogo[3][3];

do{ // deseja jogar novamente?
    jogador = 1;
    ganhou = 0;
    jogadas = 0;
    // como inicializar nossa estrutura de dados?
    for(l = 0; l < 3; l++){
        for(c = 0; c < 3; c++){
            jogo[l][c] = ' ';
        }
    }

    do{ // repete até alguém ganhar ou atingir 9 jogadas
        // imprimir jogo
        printf("\n\n\t 0   1   2\n\n");
        for(l = 0; l < 3; l++){
            for(c = 0; c < 3; c++){
                if(c == 0)
                    printf("\t");
                printf(" %c ", jogo[l][c]);
                if(c < 2)
                    printf("|");
                if(c == 2)
                    printf("  %d", l);
            }
            if(l < 2)
                printf("\n\t-----------");
            printf("\n");
          
        }

        // ler coordenadas
        do{
            printf("\nJOGADOR 1 = O\nJOGADOR 2 = X\n");
            printf("\nJOGADOR %d: Digite a linha e a coluna que deseja jogar: ", jogador);
            scanf("%d%d", &linha, &coluna);
              
        }while(linha < 0 || linha > 2 || coluna < 0 || coluna > 2 || jogo[linha][coluna] != ' ');

        // salvar coordenadas
        if(jogador == 1){
            jogo[linha][coluna] = '0';
            jogador++;
        }
        else{
            jogo[linha][coluna] = 'X';
            jogador = 1;
        }
        jogadas++;

        // alguém ganhou por linha
        if(jogo[0][0] == '0' && jogo[0][1] == '0' && jogo[0][2] == '0' ||
           jogo[1][0] == '0' && jogo[1][1] == '0' && jogo[1][2] == '0' ||
           jogo[2][0] == '0' && jogo[2][1] == '0' && jogo[2][2] == '0'){
            printf("\nParabens! O jogador 1 venceu por linha!\n");
            ganhou = 1;
        }

        if(jogo[0][0] == 'X' && jogo[0][1] == 'X' && jogo[0][2] == 'X' ||
           jogo[1][0] == 'X' && jogo[1][1] == 'X' && jogo[1][2] == 'X' ||
           jogo[2][0] == 'X' && jogo[2][1] == 'X' && jogo[2][2] == 'X'){
            printf("\nParabens! O jogador 2 venceu por linha!\n");
            ganhou = 1;
        }

        // alguém ganhou por coluna
        if(jogo[0][0] == '0' && jogo[1][0] == '0' && jogo[2][0] == '0' ||
           jogo[0][1] == '0' && jogo[1][1] == '0' && jogo[2][1] == '0' ||
           jogo[0][2] == '0' && jogo[1][2] == '0' && jogo[2][2] == '0'){
            printf("\nParabens! O jogador 1 venceu por coluna!\n");
            ganhou = 1;
        }

        if(jogo[0][0] == 'X' && jogo[1][0] == 'X' && jogo[2][0] == 'X' ||
           jogo[0][1] == 'X' && jogo[1][1] == 'X' && jogo[2][1] == 'X' ||
           jogo[0][2] == 'X' && jogo[1][2] == 'X' && jogo[2][2] == 'X'){
            printf("\nParabens! O jogador 2 venceu por coluna!\n");
            ganhou = 1;
        }

        // alguém ganhou na diagonal principal
        if(jogo[0][0] == '0' && jogo[1][1] == '0' && jogo[2][2] == '0'){
            printf("\nParabens! O jogador 1 venceu na diag. principal!\n");
            ganhou = 1;
        }

        if(jogo[0][0] == 'X' && jogo[1][1] == 'X' && jogo[2][2] == 'X'){
            printf("\nParabens! O jogador 2 venceu na diag. principal!\n");
            ganhou = 1;
        }

        // alguém ganhou na diagonal secundária
        if(jogo[0][2] == '0' && jogo[1][1] == '0' && jogo[2][0] == '0'){
            printf("\nParabens! O jogador 1 venceu na diag. secindaria!\n");
            ganhou = 1;
        }

        if(jogo[0][2] == 'X' && jogo[1][1] == 'X' && jogo[2][0] == 'X'){
            printf("\nParabens! O jogador 2 venceu na diag. secundaria!\n");
            ganhou = 1;
        }
    }while(ganhou == 0 && jogadas < 9);

    // imprimir jogo
    printf("\n\n\t 0   1   2\n\n");
    for(l = 0; l < 3; l++){
        for(c = 0; c < 3; c++){
            if(c == 0)
                printf("\t");
            printf(" %c ", jogo[l][c]);
            if(c < 2)
                printf("|");
            if(c == 2)
                printf("  %d", l);
        }
        if(l < 2)
            printf("\n\t-----------");
        printf("\n");
    }

    if(ganhou == 0)
        printf("\nO jogo finalizou sem ganhador!\n");

    printf("\nDigite 1 para jogar novamente: \n");
    scanf("%d", &opcao);

  
}while(opcao == 1);
break;
case 4:
printf("\n VOCÊ SAIU DO JOGO\n");
break;

default:
printf("OPÇÃO INVÁLIDA. ESCOLHA NOVAMENTE!\n"); // se inserir um número inválido no menu ele imprime essa frase e retorna as opções
}
} while (menu != 4); //condição para escolher 4 opcões diferentes dentro do laço de repetição

return 0;
}
