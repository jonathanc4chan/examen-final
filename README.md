# examen-final

import java.sql.Connection;

import java.sql.DriverManager;

import java.sql.PreparedStatement;

import java.sql.SQLException;

public class examenfinal {
    public static void main(String[] args) {
        // Datos del estudiante a insertar
        int carnet = 12345;
        String nombre = "Juan";
        int edad = 20;

        // Detalles de la conexión a la base de datos
        String url = "jdbc:mysql://localhost:3306/estudiantes"; 
        String usuario = "root";
        String contraseña = "2004";

        try {
            
            Connection conexion = DriverManager.getConnection("jdbc:mysql://localhost:3306/estudiantes", "root", "2004");

           
            String consulta = "INSERT INTO estudiante (carnet, nombre, edad) VALUES (?, ?, ?)";

           
            PreparedStatement declaracion = conexion.prepareStatement(consulta);
            declaracion.setInt(1, carnet);
            declaracion.setString(2, nombre);
            declaracion.setInt(3, edad);

            
            int filasInsertadas = declaracion.executeUpdate();

            if (filasInsertadas > 0) {
                System.out.println("Inserción exitosa");
            } else {
                System.out.println("Fallo al insertar el estudiante");
            }

            // Cerrar la conexión y la declaración
            declaracion.close();
            conexion.close();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
