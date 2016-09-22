#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(){
char romano[30],opt[0];
int num[10], i, tamanho, soma=0, tmp=0;
do{
system("clear");
printf("Digite um número romano para converter em decimal: ");
scanf("%s",romano);

//Calculando a quantidade de caracteres da string
tamanho = strlen(romano);

//Para cada letra válida assumimos um valor
for (i=0; i<tamanho; i++){

  if (romano[i] == 'i')
    num[i] = 1;
  else if (romano[i] == 'v')
    num[i]=5;
  else if (romano[i] == 'x')
    num[i]=10;
  else if (romano[i] == 'l')
    num[i]=50;
  else if (romano[i] == 'c')
    num[i]=100;
  else if (romano[i] == 'd')
    num[i]=500;
  else if (romano[i] == 'm')
    num[i]=1000;
  else //Para qualquer letra que seja inválida assumimos o valor -1.
  num[i]=-1;    
}

for (i=0; i<tamanho; i++){
	if (num[i] == -1 || (num[i]==num[i-3] && num[i]==num[i-2] && num[i]==num[i-1] && i>=3) || (num[i]==num[i-1] && (num[i]==5 || num[i]==50 || num[i]==500)))
		soma = -1; 
		//A soma será -1 de acordo com pelo menos 1 dos critérios abaixo:
		//Se a letra for inválida.
		//Em nenhum número se pode pôr uma mesma letra mais de três vezes seguidas.
		//A letra "V", "L" e a "D" não podem se duplicar porque outras letras ("X", "C", "M") representam seu valor duplicado.
		
	else{	
		if (num[i-1] >= num[i] && i>0) //Se o primeiro número for maior que o segundo, somamos.
			soma = soma + num[i];
		else if(i==0)
			soma = num[i];
		else if (num[i-1] < num[i]) //Se o primeiro número for menor que o segundo, subtraimos.
			soma = soma + num[i] - 2*num[i-1]; //Subtrai-se duas vezes porque o número menor foi somado anteriormente.
	}
}

printf("%s = %d\n",romano,soma);
printf("Continuar? [s][n]: ");
scanf("%s",opt);
getchar();



}while(opt[0] == 's');

return 0;
}
