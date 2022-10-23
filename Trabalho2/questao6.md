## Vetores declarados estaticamente, na pilha e no monte
Compilado no [OnlineGDB](https://www.onlinegdb.com/).

A linguagem escolhida para realizar essa função foi o C++.

No C++, por padrão, todas as variáveis definidas em métodos são dinâmicas da pilha, por isso, para a declaração estática não poderia ser separara em uma terceira função, então, ela foi realizada no próprio main.

Os vetores possuem tamanho de 10 mil, e os métodos foram chamados 100 mil vezes. Usou-se a função rand() para preencher todos os vetor com números aleatórios e, em todos os casos, logo após criar e preencher o vetor, ele é imprimido.

```C++
#include <iostream>
#include <time.h>

#define tam 10000

using namespace std;

void pilha()
{
    cout<<endl<<endl<<"Declaração pilha:"<<endl;
    int vetor[tam];
    
    srand(time(NULL));
    
    for(int i = 0; i < tam; i++)
        vetor[i]= rand() % 100;
            
    for(int i = 0; i < tam; i++)
        cout<< vetor[i] << " ";
    
}


void monte()
{
    cout<<endl<<endl<<"Declaração no monte:"<<endl;
    
    int *vetor=new int; ///alocando

    srand(time(NULL));

    if(vetor){
        cout<<"Memoria alocada com sucesso!"<<endl;
        for(int i = 0; i < tam; i++)
            *(vetor + i) = rand() % 100;

        for(int i = 0; i < tam; i++)
            cout<< *(vetor + i)<< " ";
    }
    else{
        cout<<"Erro ao alocar memoria!"<<endl;
    }
    
    delete(vetor); ///desalocando
}


int main()
{
    for(int j=0;j<100000;j++)
    {
        ////Estática
        cout<<endl<<"Declaração estática:"<<endl;
        
        int vetor[tam];
        
        srand(time(NULL));
        
        for(int i = 0; i < tam; i++)
            vetor[i]= rand() % 100;
                
        for(int i = 0; i < tam; i++)
            cout<< vetor[i] << " ";
    
        
        pilha();
        monte();
    }
    return 0;
}

```

O programa compilou normalmente, mas a impressão é demorada.Isso já era de se esperar, pois ele repete os processos de declarações 100 mil vezes e em cada processo é criado um vetor de 10 mil posições.