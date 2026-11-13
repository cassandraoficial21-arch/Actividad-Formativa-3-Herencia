# Actividad-Formativa-3-Herencia
Aplicación Java de registro de estudiantes utilizando herencia.

import java.util.Scanner;

// Clase base: contiene los datos generales del estudiante.
class Estudiante {
    protected String nombre;
    protected String matricula;
    protected double promedio;

    // Constructor de la clase base.
    public Estudiante(String nombre, String matricula, double promedio) {
        this.nombre = nombre;
        this.matricula = matricula;
        this.promedio = promedio;
    }

    // Metodo para mostrar los datos del estudiante.
    public void mostrarDatos() {
        System.out.println("Nombre: " + nombre);
        System.out.println("Matricula: " + matricula);
        System.out.println("Promedio: " + promedio);
    }

    // Metodo para actualizar el promedio.
    public void actualizarPromedio(double nuevoPromedio) {
        promedio = nuevoPromedio;
        System.out.println("Promedio actualizado.");
    }

    // Metodo que sera sobrescrito por las clases derivadas.
    public void mostrarTipo() {
        System.out.println("Estudiante general");
    }
}

// Clase derivada que hereda de Estudiante.
class EstudiantePresencial extends Estudiante {
    private String salon;

    public EstudiantePresencial(String nombre, String matricula,
                                double promedio, String salon) {
        super(nombre, matricula, promedio);
        this.salon = salon;
    }

    // Sobrescritura del metodo de la clase base.
    @Override
    public void mostrarTipo() {
        System.out.println("Estudiante presencial");
    }

    // Metodo exclusivo de esta subclase.
    public void mostrarSalon() {
        System.out.println("Salon: " + salon);
    }
}

// Segunda clase derivada.
class EstudianteEnLinea extends Estudiante {
    private String plataforma;

    public EstudianteEnLinea(String nombre, String matricula,
                              double promedio, String plataforma) {
        super(nombre, matricula, promedio);
        this.plataforma = plataforma;
    }

    // Sobrescritura del metodo de la clase base.
    @Override
    public void mostrarTipo() {
        System.out.println("Estudiante en linea");
    }

    // Metodo exclusivo de esta subclase.
    public void mostrarPlataforma() {
        System.out.println("Plataforma: " + plataforma);
    }
}

// Programa principal.
public class Main {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        Estudiante estudiante = null;
        int opcion;

        do {
            System.out.println("\n--- SISTEMA DE ESTUDIANTES ---");
            System.out.println("1. Registrar presencial");
            System.out.println("2. Registrar en linea");
            System.out.println("3. Mostrar datos");
            System.out.println("4. Actualizar promedio");
            System.out.println("5. Mostrar tipo");
            System.out.println("6. Salir");
            System.out.print("Elige una opcion: ");
            opcion = entrada.nextInt();
            entrada.nextLine();

            switch (opcion) {
                case 1:
                    System.out.print("Nombre: ");
                    String nombre = entrada.nextLine();
                    System.out.print("Matricula: ");
                    String matricula = entrada.nextLine();
                    System.out.print("Promedio: ");
                    double promedio = entrada.nextDouble();
                    entrada.nextLine();
                    System.out.print("Salon: ");
                    String salon = entrada.nextLine();

                    estudiante = new EstudiantePresencial(
                        nombre, matricula, promedio, salon);
                    System.out.println("Registro presencial realizado.");
                    break;

                case 2:
                    System.out.print("Nombre: ");
                    nombre = entrada.nextLine();
                    System.out.print("Matricula: ");
                    matricula = entrada.nextLine();
                    System.out.print("Promedio: ");
                    promedio = entrada.nextDouble();
                    entrada.nextLine();
                    System.out.print("Plataforma: ");
                    String plataforma = entrada.nextLine();

                    estudiante = new EstudianteEnLinea(
                        nombre, matricula, promedio, plataforma);
                    System.out.println("Registro en linea realizado.");
                    break;

                case 3:
                    if (estudiante != null) {
                        estudiante.mostrarDatos();

                        if (estudiante instanceof EstudiantePresencial) {
                            ((EstudiantePresencial) estudiante).mostrarSalon();
                        } else if (estudiante instanceof EstudianteEnLinea) {
                            ((EstudianteEnLinea) estudiante).mostrarPlataforma();
                        }
                    } else {
                        System.out.println("Primero registra un estudiante.");
                    }
                    break;

                case 4:
                    if (estudiante != null) {
                        System.out.print("Nuevo promedio: ");
                        double nuevo = entrada.nextDouble();
                        estudiante.actualizarPromedio(nuevo);
                    } else {
                        System.out.println("Primero registra un estudiante.");
                    }
                    break;

                case 5:
                    if (estudiante != null) {
                        estudiante.mostrarTipo();
                    } else {
                        System.out.println("Primero registra un estudiante.");
                    }
                    break;

                case 6:
                    System.out.println("Programa finalizado.");
                    break;

                default:
                    System.out.println("Opcion no valida.");
            }

        } while (opcion != 6);

        entrada.close();
    }
}
