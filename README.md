//1.Faça um programa que gerencie uma agenda de telefones. O
//programa deve ser capaz de armazenar as informações para até 100 pessoas.
//A agenda deve conter o CPF, nome e o telefone de cada pessoa, devendo ser
//possível realizar as seguintes operações: consulta de um telefone, inclusão de
//um novo telefone; alteração do número de um telefone já cadastrado; exclusão
//de um telefone; impressão dos telefones cadastrados; ordenação por CPF;
//consulta a partir do CPF de uma pessoa. A rotina de consulta de um telefone
//obtido o CPF, quando não estiver cadastrado deve perguntar ao usuário se o
//deseja incluir. Faça uma função para cada tarefa que o programa realiza.
#include <stdio.h>
#include <conio.h>
#include <string.h>
#include <ctype.h>
#include <stdlib.h>
#include <locale.h>
#define n 100
typedef struct agenda{
 char nome[30];
double cpf;
 int tel;
 int tel2;
}agenda;
agenda a[n],temp;
int i,fim;
void exclui(int valor){
char op2;
            for(i=0;i<n;i++){
             if(valor==a[i].cpf){
              printf("Deseja Excluir? 's' para sim ou 'n' para não\n");
              fflush(stdin);
              scanf("%c",&op2);
              op2=tolower(op2);
 switch(op2){
               case 's': 
                         memset(a[i].nome, ' ', 30);
                         a[i].cpf = 0;
                         a[i].tel = 0;
                         a[i].tel2 = 0;
                         printf("Exclusão Efetuada!");
                         system("pause");
                         break;
               case 'n': i=100;
                         break;
              }
               break;
             }
             else if((valor!=a[i].cpf)&&(i>=99)){
              printf("CPF não encontrado!");
              system("pause");
             }
            }
}
void pesquisar(double pes){
  for(i=0;i<n;i++){
    if(pes==a[i].cpf){
      system("cls");
	  printf("Nome: %s",a[i].nome);
	  printf("\nCPF: %lf",a[i].cpf);
	  printf("\nTelefone: %d",a[i].tel);
	  printf("\nTelefone 2: %d\n",a[i].tel2);
      system("pause");
      break;
    }
    else if((pes!=a[i].cpf)&&(i>=99)){
      printf("\nCPF não encontrado!\n");
      system("pause");
    }
  }
}
void novo_telefone(double novo2){
  for(i=0;i<n;i++){
    if(novo2==a[i].cpf){
      printf("\nNovo número: ");
      scanf("%d",&a[i].tel2);
      break;
    }
    else if((novo2!=a[i].cpf)&&(i>=99)){
      printf("\nCPF não encontrado!\n");
      system("pause");
    }
  }
}
void alterar(double pesq2){
  for(i=0;i<n;i++){
    if(pesq2==a[i].cpf){
      a[i].tel = 0;
      system("cls");
      printf("Insira os novos dados!");
	  printf("\nTelefone: ");
	  scanf("%d",&a[i].tel);
      break;
    }
    else if((pesq2!=a[i].cpf)&&(i>=99)){
      printf("\nCPF não encontrado!");
      system("pause");
    }
  }
}
void listar(){
  for(fim=n-1; fim>0; fim--){
    for(i=0; i<fim; i++){
      if(a[i].cpf>a[i+1].cpf){
        temp = a[i]; /* troca */
        a[i] = a[i+1];
        a[i+1] = temp;
      }
    }
  }
  for(i=0;i<n;i++){
    if(a[i].cpf!=0){
      printf("\nNome: %s",a[i].nome);
      printf("\nCPF: %0.lf",a[i].cpf);
	  printf("\nTelefone: %d",a[i].tel);
	  printf("\nTelefone: %d\n",a[i].tel2);
  	  system("pause");
    }
    else if((a[i].cpf!=0)&&(n>=100)){
      printf("Não há contato salvo!");
      system("pause");
    }
  }
}
main(){
setlocale(LC_ALL, "Portuguese");
int s,pesq=0,excluir,k=0,op,novo;
  for(i=0;i<n;i++){
    memset(a[i].nome, ' ', 30);
    a[i].cpf = 0;
    a[i].tel = 0;
    a[i].tel2 = 0;
  }
do{
  system("cls");
  printf("\tMenu!\n");
  printf("\n1-Cadastro");
  printf("\n2-Exclusão de telefone");
  printf("\n3-Pesquisa por CPF");
  printf("\n4-Inclusão de um novo telefone");
  printf("\n5-Alterar telefone");
  printf("\n6-Listar");
  printf("\n7-Sair");
  printf("\nescolha uma das opções acima: ");
  scanf("%d",&op);
  switch(op){
   case 1: system("cls");
           do{
              if(k>99){
               printf("Não há espaço na memória para cadastrar!");
               s=0;
              }
              else{
               system("cls");
               printf("Digite seu nome: ");
               fflush(stdin);
               gets(a[k].nome);
               printf("\nDigite seu CPF: ");
               scanf("%lf",&a[k].cpf);
               printf("\nDigite seu telefone: ");
               scanf("%d",&a[k].tel);
               k++;
			   system("cls");
               printf("Cadastro Realizado com sucesso!");
               printf("\nDigite 0 para sair ou qualquer letra/número para continuar o cadastro! ");
               scanf("%d",&s);
              }
             }while(s!=0);
             break;
   case 2: system("cls");
           printf("Digite o CPF do cliente:\n");
           scanf("%d", &excluir);
           exclui(excluir);
		   break;
   case 3: system("cls");
           printf("Para mostrar as infomacoes do contato, insira o CPF do contato:\n");
           scanf("%d",&pesq);
           pesquisar(pesq);
           break;
   case 4: system("cls");
           printf("Digite o CPF: ");
           scanf("%d",&novo);
           novo_telefone(novo);
           break;
   case 5: system("cls");
           printf("Para alterar as infomacoes do contato, insira o CPF do contato:\n");
           scanf("%d",&pesq);
		   alterar(pesq);
           break;
   case 6: system("cls");
           listar();
           break;
  }
}while(op!=7);
}
