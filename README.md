Mostrar la tabla de resultados de conductores en un TablaView

#capturas


![Captura de pantalla 2024-07-09 171351](https://github.com/Ivanmurillojr30/tabla-de-resultados-de-conductores/assets/168851753/dd0dd86d-a938-4e47-86c6-cc1a479816b6)


![Captura de pantalla 2024-07-09 135110](https://github.com/Ivanmurillojr30/tabla-de-resultados-de-conductores/assets/168851753/7fab6ce9-8aab-4ab9-b3c4-b4ba39069270)


![Captura de pantalla 2024-07-09 171342](https://github.com/Ivanmurillojr30/tabla-de-resultados-de-conductores/assets/168851753/31f14251-3e93-4fe6-a2ae-a6f38b7254db)


# explicacion 

Este programa es una aplicación JavaFX que muestra estadísticas de pilotos de carreras para los años 2016 a 2020. La interfaz gráfica permite seleccionar el año desde un ComboBox y ver las estadísticas de los pilotos en una tabla. Además, hay un botón que imprime los datos de todos los años en la consola.

Componentes Principales
ComboBox: Permite seleccionar el año para ver las estadísticas correspondientes.
TableView: Muestra los datos de los pilotos en columnas: nombre, equipo, victorias, puntos totales y clasificación.
Button (Print Data): Imprime los datos de todos los años en la consola.
Funcionamiento
start(Stage primaryStage): Configura la ventana principal, crea los componentes (ComboBox, TableView, Button), añade listeners y define el layout.
updateTable(String year): Actualiza la tabla con los datos del año seleccionado.
printTableData(): Imprime en la consola los datos de todos los años.
Datos de Ejemplo
Los datos de ejemplo están definidos en un HashMap<String, ObservableList<Driver>>, donde la clave es el año y el valor es una lista observable de objetos Driver. Cada Driver tiene nombre, equipo, victorias, puntos y clasificación.

# Driver Stats Application

This is a JavaFX application that displays driver statistics for the years 2016 to 2020. The interface allows users to select a year from a ComboBox and view the statistics in a TableView. There is also a button to print all data to the console.

## Features

- View driver statistics by year.
- Table view displays driver name, team, wins, total points, and rank.
- Print all driver data to the console.

## Technologies Used

- Java
- JavaFX

## How to Run


3. Navigate to the project directory:
    ```bash
    cd driver-stats-app
    ```
4. Compile and run the application:
    ```bash
    javac -d bin src/application/Main.java
    java -cp bin application.Main
    ```

## Code Explanation

### Main.java

```java
package application;

import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.control.ComboBox;
import javafx.scene.control.TableColumn;
import javafx.scene.control.TableView;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

import java.util.HashMap;
import java.util.Map;

public class Main extends Application {

    private TableView<Driver> table;
    private Map<String, ObservableList<Driver>> data;

    @SuppressWarnings("unchecked")
    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Driver Stats");

        // Create the ComboBox
        ComboBox<String> comboBox = new ComboBox<>();
        comboBox.getItems().addAll("2016", "2017", "2018", "2019", "2020");
        comboBox.setValue("2016");

        // Create the table
        table = new TableView<>();
        TableColumn<Driver, String> nameColumn = new TableColumn<>("Driver Name");
        nameColumn.setCellValueFactory(new PropertyValueFactory<>("name"));

        TableColumn<Driver, String> teamColumn = new TableColumn<>("Team");
        teamColumn.setCellValueFactory(new PropertyValueFactory<>("team"));

        TableColumn<Driver, Integer> winsColumn = new TableColumn<>("Wins");
        winsColumn.setCellValueFactory(new PropertyValueFactory<>("wins"));

        TableColumn<Driver, Integer> pointsColumn = new TableColumn<>("Total Points");
        pointsColumn.setCellValueFactory(new PropertyValueFactory<>("points"));

        TableColumn<Driver, Integer> rankColumn = new TableColumn<>("Rank");
        rankColumn.setCellValueFactory(new PropertyValueFactory<>("rank"));

        table.getColumns().addAll(nameColumn, teamColumn, winsColumn, pointsColumn, rankColumn);

        // Example data
        data = new HashMap<>();
        data.put("2016", FXCollections.observableArrayList(
                new Driver("Lewis Hamilton", "Mercedes", 10, 250, 1),
                new Driver("Valtteri Bottas", "Mercedes", 5, 180, 2),
                new Driver("Max Verstappen", "Red Bull", 3, 150, 3),
                new Driver("Charles Leclerc", "Ferrari", 2, 120, 4),
                new Driver("Sebastian Vettel", "Ferrari", 1, 100, 5)
        ));
        data.put("2017", FXCollections.observableArrayList(
                new Driver("Sebastian Vettel", "Ferrari", 9, 240, 1),
                new Driver("Lewis Hamilton", "Mercedes", 8, 230, 2),
                new Driver("Daniel Ricciardo", "Red Bull", 4, 170, 3),
                new Driver("Kimi Raikkonen", "Ferrari", 3, 130, 4),
                new Driver("Max Verstappen", "Red Bull", 2, 110, 5)
        ));
        data.put("2018", FXCollections.observableArrayList(
                new Driver("Lewis Hamilton", "Mercedes", 11, 260, 1),
                new Driver("Sebastian Vettel", "Ferrari", 6, 200, 2),
                new Driver("Valtteri Bottas", "Mercedes", 4, 160, 3),
                new Driver("Max Verstappen", "Red Bull", 3, 140, 4),
                new Driver("Daniel Ricciardo", "Red Bull", 2, 120, 5)
        ));
        data.put("2019", FXCollections.observableArrayList(
                new Driver("Lewis Hamilton", "Mercedes", 12, 270, 1),
                new Driver("Valtteri Bottas", "Mercedes", 7, 220, 2),
                new Driver("Charles Leclerc", "Ferrari", 5, 180, 3),
                new Driver("Max Verstappen", "Red Bull", 4, 150, 4),
                new Driver("Sebastian Vettel", "Ferrari", 3, 130, 5)
        ));
        data.put("2020", FXCollections.observableArrayList(
                new Driver("Lewis Hamilton", "Mercedes", 13, 280, 1),
                new Driver("Valtteri Bottas", "Mercedes", 8, 230, 2),
                new Driver("Max Verstappen", "Red Bull", 6, 190, 3),
                new Driver("Sergio Perez", "Racing Point", 2, 140, 4),
                new Driver("Charles Leclerc", "Ferrari", 1, 120, 5)
        ));

        // Add Listener for ComboBox
        comboBox.setOnAction(e -> updateTable(comboBox.getValue()));

        // Create the Print Button
        Button printButton = new Button("Print Data");
        printButton.setOnAction(e -> printTableData());

        // Layout
        VBox vbox = new VBox(comboBox, table, printButton);
        Scene scene = new Scene(vbox, 600, 400);

        primaryStage.setScene(scene);
        primaryStage.show();

        // Initialize table with data from the default selected year
        updateTable(comboBox.getValue());
    }

    private void updateTable(String year) {
        table.setItems(data.get(year));
    }

    private void printTableData() {
        for (String year : data.keySet()) {
            System.out.println("Year: " + year);
            for (Driver driver : data.get(year)) {
                System.out.println(driver);
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        launch(args);
    }
}
