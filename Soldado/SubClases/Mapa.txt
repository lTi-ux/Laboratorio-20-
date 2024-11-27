//KENNEDY CHIRINOS ROJAS
//LABORATORIO 20
import java.util.*;

class Mapa {
    public static final int TAMANO_MAPA = 10;
    private Soldado[][] tablero;

    public Mapa() {
        tablero = new Soldado[TAMANO_MAPA][TAMANO_MAPA];
    }

    public void posicionarEjercitos(Ejercito ejercito1, Ejercito ejercito2) {
        posicionarSoldados(ejercito1.getSoldados(), "E1");
        posicionarSoldados(ejercito2.getSoldados(), "E2");
    }

    private void posicionarSoldados(List<Soldado> soldados, String etiquetaEjercito) {
        for (Soldado soldado : soldados) {
            int fila = soldado.getFila();
            int columna = soldado.getColumna();
            if (fila >= 0 && fila < TAMANO_MAPA && columna >= 0 && columna < TAMANO_MAPA) {
                if (tablero[fila][columna] == null) {
                    tablero[fila][columna] = soldado;
                    tablero[fila][columna].nombre = etiquetaEjercito + "-" + soldado.getNombre();
                } else {
                    System.out.println("La posición (" + fila + ", " + columna + ") ya está ocupada.");
                }
            } else {
                System.out.println("Posición (" + fila + ", " + columna + ") fuera de los límites del mapa.");
            }
        }
    }

    public void mostrarMapa() {
        System.out.println("=======================================================");
    
        System.out.print("  ");
        for (int j = 0; j < TAMANO_MAPA; j++) {
            System.out.print("    " + j + "    ");
        }
        System.out.println();

        for (int i = 0; i < TAMANO_MAPA; i++) {
            System.out.print(i + " ");
            for (int j = 0; j < TAMANO_MAPA; j++) {
                if (tablero[i][j] == null) {
                    System.out.print("[      ] ");
                } else {
                    Soldado soldado = tablero[i][j];
                    String tipoSoldado = soldado.tipoDeSoldado().substring(0, 2).toUpperCase();
                    String etiquetaEjercito = soldado.getNombre().substring(0, 2).toUpperCase(); // Obtener etiqueta del ejército
                    System.out.print("[" + etiquetaEjercito + "-" + tipoSoldado + soldado.getNivelVida() + "] ");
                }
            }
            System.out.println();
        }
        System.out.println("=======================================================");
    }
}
