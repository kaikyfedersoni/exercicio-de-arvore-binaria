#include <stdio.h>

#include <stdlib.h>

#include <string.h>



// Estrutura do nó da árvore binária

typedef struct Node {

    char* data;

    struct Node* left;

    struct Node* right;

} Node;



// Função para criar um novo nó

Node* createNode(char* data) {

    Node* newNode = (Node*)malloc(sizeof(Node));

    newNode->data = data;

    newNode->left = NULL;

    newNode->right = NULL;

    return newNode;

}



// Função auxiliar para verificar se um caractere é um operador

int isOperator(char c) {

    return (c == '+' || c == '-' || c == '*' || c == '/');

}



// Função para construir a árvore binária a partir da equação ou atribuição

Node* buildExpressionTree(char* input) {

    // Verifica se é uma atribuição

    char* assignPos = strchr(input, '=');

    if (assignPos != NULL) {

        // Cria um novo nó com o operador de atribuição

        Node* newNode = createNode("=");



        // Obtém o lado esquerdo da atribuição (variável)

        int varLength = assignPos - input;

        char* variable = (char*)malloc((varLength + 1) * sizeof(char));

        strncpy(variable, input, varLength);

        variable[varLength] = '\0';



        // Cria um novo nó para a variável

        Node* leftNode = createNode(variable);



        // Obtém o lado direito da atribuição (expressão)

        Node* rightNode = buildExpressionTree(assignPos + 1);



        // Define os nós esquerdo e direito no nó de atribuição

        newNode->left = leftNode;

        newNode->right = rightNode;



        return newNode;

    }



    // Se não for uma atribuição, constrói a árvore binária como antes



    int len = strlen(input);

    // Remove o caractere de nova linha

    if (len > 0 && input[len - 1] == '\n') {

        input[len - 1] = '\0';

        len--;

    }



    // Encontra o operador com a menor precedência

    int i;

    int operatorPos = -1;

    int brackets = 0;

    for (i = len - 1; i >= 0; i--) {

        if (input[i] == ')')

            brackets++;

        else if (input[i] == '(')

            brackets--;

        else if (brackets == 0 && isOperator(input[i])) {

            operatorPos = i;

            break;

        }

    }



    // Se não há operadores, é um número ou uma variável

    if (operatorPos == -1) {

        // Verifica se é um número

        int isNumber = 1;

        for (i = 0; i < len; i++) {

            if (!(input[i] >= '0' && input[i] <= '9')) {

                isNumber = 0;

                break;

            }

        }



        if (isNumber) {

            // Cria um novo nó para o número

            char* number = (char*)malloc((len + 1) * sizeof(char));

            strcpy(number, input);

            number[len] = '\0';



            return createNode(number);

        } else {

            // É uma variável

            char* variable = (char*)malloc((len + 1) * sizeof(char));

            strcpy(variable, input);

            variable[len] = '\0';



            return createNode(variable);

        }

    }



    // Cria um novo nó com o operador

    char* operator = (char*)malloc(2 * sizeof(char));

    operator[0] = input[operatorPos];

    operator[1] = '\0';



    // Cria um novo nó para o operador

    Node* newNode = createNode(operator);



    // Obtém o lado esquerdo do operador

    char* leftOperand = (char*)malloc((operatorPos + 1) * sizeof(char));

    strncpy(leftOperand, input, operatorPos);

    leftOperand[operatorPos] = '\0';



    // Obtém o lado direito do operador

    char* rightOperand = (char*)malloc((len - operatorPos - 1) * sizeof(char));

    strncpy(rightOperand, input + operatorPos + 1, len - operatorPos - 1);

    rightOperand[len - operatorPos - 1] = '\0';



    // Constrói as subárvores recursivamente

    newNode->left = buildExpressionTree(leftOperand);

    newNode->right = buildExpressionTree(rightOperand);



    return newNode;

}



// Função para imprimir a árvore binária no formato especificado

void printTree(Node* root) {

    if (root == NULL)

        return;



    printf("<%s", root->data);

    printTree(root->left);

    printTree(root->right);

    printf(">");

}



// Função para liberar a memória alocada pela árvore binária

void freeTree(Node* root) {

    if (root == NULL)

        return;



    freeTree(root->left);

    freeTree(root->right);

    free(root->data);

    free(root);

}



int main() {

    char input[100];



    printf("Digite a equação ou atribuição: ");

    fgets(input, sizeof(input), stdin);



    // Constrói a árvore binária a partir da entrada

    Node* root = buildExpressionTree(input);



    // Imprime a árvore binária no formato especificado

    printf("Árvore binária: ");

    printTree(root);

    printf("\n");



    // Libera a memória alocada pela árvore binária

    freeTree(root);



    return 0;

}
