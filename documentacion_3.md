# Tree.h

```c++
#ifndef TREE_H
#define TREE_H

#include <iostream>

template <typename T>
class Node {
public:
    T data;
    Node* firstChild;
    Node* nextSibling;

    explicit Node(T data);
};

template <typename T>
class Tree {
public:
    Node<T>* root;

    Tree();

    Node<T>* addNode(T data, Node<T>* parent = nullptr);

    void printTree(Node<T>* node, int level = 0);
};

#include "Tree.cpp"

#endif //TREE_H
```

###### el siguiente pedaso de codigo sirve para 

```c++
template <typename T>
class Node {//clase
public:
    T data;//dato almacenado
    Node* firstChild;//puntero al hijo del nodo
    Node* nextSibling;//puntero al siguiente nodo 

    explicit Node(T data);//crea nodo data
};
```

###### En esta parte del código se tiene la clase node que tiene una plantilla data T tiene un puntero al primer hijo del nodo. permite crear relaciones del árbol padre hijo y un puntero al siguiente nodo tenemos un constructor que toma un dato como argumento e inicializar sin hijos ni hermanos por defecto.

```c++
template <typename T>
class Tree {//clase
public:
    Node<T>* root;puntero raiz del arbol

    Tree();//crear un arbol vacio

    Node<T>* addNode(T data, Node<T>* parent = nullptr);//añadir un nodo con el dtao al arbol 

    void printTree(Node<T>* node, int level = 0);//imprime el arbol
};

#include "Tree.cpp"//icluye archivo Tree.cpp
```

###### En este código tenemos la clase Tree que usa plantilla, tenemos un puntero a la raíz del árbol que representa el nodo principal del árbol donde se desarrollan todas las relaciones padre hijo, se inicializa un árbol vacío el puntero a la raíz root  y se establece como nullptr, tenemos un método que agrega un nuevo nodo árbol con el valor data si parent no se le proporciona  el nuevo nodo se convierte en la raiz del arbol y si se proporciona parent en nuevo nodo se agrega como hijo del nodo parent y tiene otro método que es para imprimir el árbol comenzando en el nodo que se le de. 

# Tree.cpp

```c++
#include "Tree.h"


template <typename T>
Node<T>::Node(T data) : data(data), firstChild(nullptr), nextSibling(nullptr) {}

template <typename T>
Tree<T>::Tree() : root(nullptr) {}

template <typename T>
Node<T>* Tree<T>::addNode(T data, Node<T>* parent) {
    Node<T>* newNode = new Node<T>(data);

    if(parent) {
        if(parent->firstChild) {
            Node<T>* sibling = parent->firstChild;
            while(sibling->nextSibling) {
                sibling = sibling->nextSibling;
            }
            sibling->nextSibling = newNode;
        } else {
            parent->firstChild = newNode;
        }
    } else {
        root = newNode;
    }

    return newNode;
}

template <typename T>
void Tree<T>::printTree(Node<T>* node, int level) {
    if(!node) return;

    for(int i = 0; i < level; i++) std::cout << "--";
    std::cout << node->data << '\n';

    printTree(node->firstChild, level + 1);
    printTree(node->nextSibling, level);
}
```

```c++
#include "Tree.h" //incluye archivo Tree.h

template <typename T>
Node<T>::Node(T data) : data(data), firstChild(nullptr), nextSibling(nullptr) {}

```

###### es el constructor de Node toma un dato data y lo asigna al atributo data del nodo sae inicializa los punteros firstchild y nextchild  como nullptr para dejar claro que no hay hijos ni hermanos al crear un nuevo nodo.

```c++
template <typename T>
Tree<T>::Tree() : root(nullptr) {}
```

###### es el constructor de Tree inicializa la raíz como nullptr para crear el arbol vacio

```c++
template <typename T>
Node<T>* Tree<T>::addNode(T data, Node<T>* parent) {
    Node<T>* newNode = new Node<T>(data);
```

###### esto es un método que crea un nuevo nodo con el dato usando el constructor de Node se asigna el puntero a new Node

```c++
   if(parent) {
        if(parent->firstChild) {
            Node<T>* sibling = parent->firstChild;
            while(sibling->nextSibling) {
                sibling = sibling->nextSibling;
            }
            sibling->nextSibling = newNode;
        } else {
            parent->firstChild = newNode;
        }
    } else {
        root = newNode;
    }

    return newNode;
}
```

###### Si parent no es nullptr Si parent tiene un primer hijo firstChild, el código busca el último hermano en la lista de hijos de parent y añade el nuevo nodo newNode como hermano al final de la lista. Si parent no tiene ningún hijo, el nuevo nodo se convierte en el primer hijo de parent. Si el parent es nullptr el nuevo nodo se convierte en la raíz  del árbol.  el método devuelve el puntero al nuevo nodo (return newNode;).

```c++
template <typename T>
void Tree<T>::printTree(Node<T>* node, int level) {
    if(!node) return;
```

###### el método anterior imprime el árbol a partir de un nodo que se le de 

```c++
    for(int i = 0; i < level; i++) std::cout << "--";
    std::cout << node->data << '\n';

```

###### se imprime el nivel de profundidad y luego se imprime el dato del nodo 

```c++
    printTree(node->firstChild, level + 1);
    printTree(node->nextSibling, level);
}

```

###### se llama así misma printTree para imprimir el hijo del nodo actual con un nivel de profundidad que se incrementa se vuelve a llamar recursivamente a printTree  para imprimir al siguiente hermano del nodo actual 

