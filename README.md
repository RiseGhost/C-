# C++


# C++ How to acess a private atributes in class 🔐

## Introdução:

Uma classe em C++ pode ter atributos (variáveis) **public** ou **private**. Sendo que o **public** pode ser utilizado pela classe e por outras estruturas externas a classe. Enquanto que o **private** só pode ser utilizado dentro da própria classe. Algo semelhante ao que acontece com as classes em Java.

A “única maneira correta” de ter acesso a esses atributos é utilizando métodos gets e sets. No entanto neste capitulo irei mostra uma maneira alternativa de conseguir manipular os atributos **private** de uma classe.

## Implementação:

Comecei por definir uma class Pessoa 🧍🏻 com os seguintes atributos private:

- int ID;
- int Peso;
- float IMC.

Nos métodos public só definir o construtor vazio da classe.

```cpp
class Pessoa{
  private:
    int ID;
    int Peso;
    float IMC;
  public:
    Pessoa(){
      this->ID = 0;
      this->Peso = 80;
      this->IMC = 25;
    }
};
```

Criei um objeto do tipo Pessoa chamado Ana.

```cpp
Pessoa Ana;
```

Para obter o endereço de memória onde esta guardado o objeto “Ana” posso utilizar o **&**. Ficando:

```cpp
&Ana
```

O endereço de memória de &Ana = &1º atributo, ou seja &Ana = &Ana.ID. Como sei que o ID é do tipo int é só fazer o cast de &Ana.ID para int. Como &Ana.ID é um apontador o cast fica:

```cpp
((int*) &Ana)
```

E assim consigo obter o valor do ID da Ana. 

Para conseguir obter os próximo atributos basta fazer: **((DataType*) &Ana)[index]**. Onde index corresponde ao index do atributo que pretendo aceder.

Como por exemplo:

- [Ana.ID](http://Ana.ID) → ((int*) &Ana)[0];
- Ana.Peso → ((int*) &Ana)[1];
- Ana.IMC → ((float*) &Ana)[2];

Código:

```cpp
#include <iostream>
#include <stdio.h>
class Pessoa{
  private:
    int ID;
    int Peso;
    float IMC;
  public:
    Pessoa(){
      this->ID = 0;
      this->Peso = 80;
      this->IMC = 25;
    }
};

int main(void){
  Pessoa Ana;
  printf("GETS -------------------\n");
  printf("%i\n", ((int*) (&Ana))[0]);
  printf("%i\n", ((int*) (&Ana))[1]);
  printf("%f\n", ((float*) (&Ana))[2]);

  printf("SETS -------------------\n");
  ((int*) &Ana)[0] = 90;
  ((int*) &Ana)[1] = 110;
  ((float*) &Ana)[2] = -90;
  printf("%i\n", ((int*) (&Ana))[0]);
  printf("%i\n", ((int*) (&Ana))[1]);
  printf("%f\n", ((float*) (&Ana))[2]);
  return 0;
}
```

Output:

![](https://user-images.githubusercontent.com/91985039/213273514-d16e2af9-8177-4a51-b54f-f5b4165e7c11.svg)

