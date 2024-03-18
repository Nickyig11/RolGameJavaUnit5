# RolGameJavaUnit5

## Introducción
RolCombat es un juego de rol simple donde el jugador controla a un personaje que debe luchar contra enemigos para avanzar y ganar experiencia. El juego está desarrollado en Java y utiliza la consola como interfaz de usuario.

## Instrucciones de Uso

1. Abre el proyecto en tu IDE preferido (vscode en mi caso.).
2. Ejecuta la clase `Main` para iniciar el juego.
3. Sigue las instrucciones que se muestran en la consola para interactuar con el juego.

## Clases Utilizadas
- `Main`: Clase principal que ejecuta el juego.
- `Jugador`: Representa al jugador y contiene métodos para manejar su inventario y estadísticas.
- `Enemigo`: Representa a los diferentes enemigos con los que el jugador debe luchar.
- `Item`: Clase que define los elementos que el jugador puede equipar en su inventario.

![Alt text](image.png)



## Items Disponibles
1. **Espada**:
   - Descripción: Esta espada proporciona un daño medio en combate.
   - Índice de Esquiva: Bajo

2. **Hacha**:
   - Descripción: Un arma potente que causa un daño alto en combate.
   - Índice de Esquiva: Medio

3. **Daga**:
   - Descripción: Una daga ágil que inflige daño rápidamente.
   - Índice de Esquiva: Alto

## Enemigos
- El juego cuenta con diferentes tipos de enemigos, cada uno con sus propias habilidades y características.

## Codigo del Main
```java
import java.util.Random;
import java.util.Scanner;
import java.util.Random;
import java.util.Scanner;

public class Main {
    final static Scanner scanner = new Scanner(System.in);
    final static Random random = new Random();
    final static Jugador primerJugador = new Jugador("", "personaje invencible que "
            + "elimina a cualquier Enemigo de one shot", 10, 20);

    final static Item espada = new Item("espada", "esta bien fuelte este arma");
    final static Item hacha = new Item("hacha", "esta bien pa cortar madera y cabezas");
    final static Item daga = new Item("daga", "pa meter apuñalaitas");

    final static Enemigo primerEnemigo = new Enemigo("pepe", 25, random.nextInt(6) + 1);

    public static void main(String[] args) {
        System.out.println("Cual es tu nombre");
        String nombre = scanner.next();
        primerJugador.addNombre(nombre);

        primerJugador.addItemAlInventario(espada, 0);
        primerJugador.addItemAlInventario(hacha, 1);
        primerJugador.addItemAlInventario(daga, 2);

        boolean continuar = true;
        String accion = "";
        while (continuar) {
            System.out
                    .println("que quieres hacer ahora: \"Continuar\" partida, \"Equipar\" item, \"Terminar\" partida");
            accion = scanner.next();
            switch (accion.toLowerCase()) {
                case "continuar":
                    continuar();
                    break;

                case "equipar":
                    System.out.println("que arma quieres equipar");
                    primerJugador.listarInventario();

                    String itemSeleccionado = scanner.next();
                    /*
                     * Esto lo que hace es que lista toda la lista y compara el nombre para equipar
                     * ese item
                     */
                    for (int i = 0; i < primerJugador.getInventario().length; i++) {
                        if (primerJugador.getInventario()[i] != null) {
                            if (itemSeleccionado.equals(primerJugador.getInventario()[i].getName())) {
                                primerJugador.addItemEquipado(primerJugador.getInventario()[i]);
                            }
                        }
                    }

                    break;

                case "terminar":
                    System.out.println("se acabo");
                    continuar = false;
                    break;

            }
        }

    }

    public static void continuar() {

        while (primerEnemigo.getEstadoDeVida() == true && primerJugador.getEstadoDeVida() == true) {
            int dañoEnemigo = random.nextInt(3) + 1;
            int dañoJugador = 0;

            if (primerJugador.getItemEquipado() == hacha) {
                dañoJugador = random.nextInt(6) + 1;
            } else if (primerJugador.getItemEquipado() == daga) {
                dañoJugador = random.nextInt(2) + 1;
            } else if (primerJugador.getItemEquipado() == espada) {
                dañoJugador = random.nextInt(4) + 1;
            }

            primerJugador.luchar(primerEnemigo, dañoEnemigo, dañoJugador);

            System.out.printf("El jugador le quita %d puntos de vida al enemigo y el jugador recibe %d pundo de daño\n",
                    dañoJugador, dañoEnemigo);
        }
        primerJugador.getNivel();
        if (primerJugador.getEstadoDeVida() == false) {
            System.out.printf("Has muerto el ganador es el enemigo %s \n\n", primerEnemigo.getName());
        } else if (primerEnemigo.getEstadoDeVida() == false) {
            System.out.printf("El enemigo %s a muerto has ganado %s\n", primerEnemigo.getName(),
                    primerJugador.getNombre());
        }

    }

}

public class Main {
    final static Scanner scanner = new Scanner(System.in);
    final static Random random = new Random();
    final static Jugador primerJugador = new Jugador("", "personaje invencible que "
            + "elimina a cualquier Enemigo de one shot", 10, 20);

    final static Item espada = new Item("espada", "esta bien fuelte este arma");
    final static Item hacha = new Item("hacha", "esta bien pa cortar madera y cabezas");
    final static Item daga = new Item("daga", "pa meter apuñalaitas");

    final static Enemigo primerEnemigo = new Enemigo("pepe", 25, random.nextInt(6) + 1);

    public static void main(String[] args) {
        System.out.println("Cual es tu nombre");
        String nombre = scanner.next();
        primerJugador.addNombre(nombre);

        primerJugador.addItemAlInventario(espada, 0);
        primerJugador.addItemAlInventario(hacha, 1);
        primerJugador.addItemAlInventario(daga, 2);

        boolean continuar = true;
        String accion = "";
        while (continuar) {
            System.out
                    .println("que quieres hacer ahora: \"Continuar\" partida, \"Equipar\" item, \"Terminar\" partida");
            accion = scanner.next();
            switch (accion.toLowerCase()) {
                case "continuar":
                    continuar();
                    break;

                case "equipar":
                    System.out.println("que arma quieres equipar");
                    primerJugador.listarInventario();

                    String itemSeleccionado = scanner.next();
                    /*
                     * Esto lo que hace es que lista toda la lista y compara el nombre para equipar
                     * ese item
                     */
                    for (int i = 0; i < primerJugador.getInventario().length; i++) {
                        if (primerJugador.getInventario()[i] != null) {
                            if (itemSeleccionado.equals(primerJugador.getInventario()[i].getName())) {
                                primerJugador.addItemEquipado(primerJugador.getInventario()[i]);
                            }
                        }
                    }

                    break;

                case "terminar":
                    System.out.println("se acabo");
                    continuar = false;
                    break;

            }
        }

    }

    public static void continuar() {

        while (primerEnemigo.getEstadoDeVida() == true && primerJugador.getEstadoDeVida() == true) {
            int dañoEnemigo = random.nextInt(3) + 1;
            int dañoJugador = 0;

            if (primerJugador.getItemEquipado() == hacha) {
                dañoJugador = random.nextInt(6) + 1;
            } else if (primerJugador.getItemEquipado() == daga) {
                dañoJugador = random.nextInt(2) + 1;
            } else if (primerJugador.getItemEquipado() == espada) {
                dañoJugador = random.nextInt(4) + 1;
            }

            primerJugador.luchar(primerEnemigo, dañoEnemigo, dañoJugador);

            System.out.printf("El jugador le quita %d puntos de vida al enemigo y el jugador recibe %d pundo de daño\n",
                    dañoJugador, dañoEnemigo);
        }
        primerJugador.getNivel();
        if (primerJugador.getEstadoDeVida() == false) {
            System.out.printf("Has muerto el ganador es el enemigo %s \n\n", primerEnemigo.getName());
        } else if (primerEnemigo.getEstadoDeVida() == false) {
            System.out.printf("El enemigo %s a muerto has ganado %s\n", primerEnemigo.getName(),
                    primerJugador.getNombre());
        }

    }

}


```