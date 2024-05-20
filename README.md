# ajedrez
//librerias
#include <iostream>
#include <cmath>

using namespace std;

// Función de estructura para tener una posición en el tablero
struct tablero {
    int fila, columna;
};

// Función para ver si dos reinas se atacan 
bool sAta(tablero reina1, tablero reina2) {
    
    //Se compara la  isma fila, columna o diagonal
    return (reina1.fila == reina2.fila || reina1.columna == reina2.columna || 
            abs(reina1.fila - reina2.fila) == abs(reina1.columna - reina2.columna));
}

// Se utiliza la función de backtracking para contar las posiciones de las reinas
void ccaminos(int n, int fila, int &contador, tablero reina1, bool cReina1) {
    if (fila == n) {
        return;
    }

    for (int columna = 0; columna < n; columna++) {
        if (!cReina1) {
            
            // función para poner a la primera reina 
            tablero nReina1 = {fila, columna};
            ccaminos(n, fila + 1, contador, nReina1, true);
        
            
        } else {
            
            // función para poner a la segunda reina 
            tablero reina2 = {fila, columna};
            if (!sAta(reina1, reina2)) {
                contador++;
            }
        }
    }

    ccaminos(n, fila + 1, contador, reina1, cReina1);
}

int main() {
    
    int n;
    
    //Texto que se imprimira en panrtalla  para pedir el tamañodel tablero
    cout << "Ingresa el tamaño del tablero deseado (n*n): ";
    cin >> n;

    
    int contador = 0;
    
     // se inicializa con una posición inválida
    tablero reina1 = {-1, -1}; 
    ccaminos(n, 0, contador, reina1, false);
    
    //Texto que se imprimirá en pantalla para dar respuesta final 
    cout << "Los caminos que toman las dos reinas es: " << contador << endl;
    return 0;
} 

