
# SceneManager

## Beschreibung

Ein JavaFX-Dienstprogramm zum Verwalten und Wechseln zwischen verschiedenen Szenen in einer Anwendung. Enthält Unterstützung für Popups und anpassbare Funktionen.

---

### Verwendung

Hier ist ein Beispiel, wie mein SceneManager in einem JavaFX-Projekt Szenen "speichert" und "verwaltet":

```java
public enum Scenes {
// use SceneType scenes = SceneType.MAIN_MENU; to get the path of the mainMenu.fxml file

    MAIN_MENU("hello-view.fxml", "Menu")
    ;

    final String fxmlPath;
    final String title;

    Scenes(String fxmlPath, String title) {
        this.fxmlPath = fxmlPath;
        this.title = title;
    }

    public String getPath() {
        return fxmlPath;
    }

    public String getTitle() {
        return title;
    }
}
```

---

### Wechseln von Scenen

```java
public void showScene(Scenes fxml) {
    if (primaryStage == null) {
        primaryStage = new Stage();  // Create primary stage if it doesn't exist
    }
    try {
        FXMLLoader fxmlLoader = new FXMLLoader(Starter.class.getResource(fxml.getPath()));  // Load the FXML file for the scene
        Parent root = fxmlLoader.load();

        Scene scene = new Scene(root);  // Create a new Scene object
        primaryStage.setTitle(fxml.getTitle());  // Set the window title
        sceneStack.push(fxml);  // Add the scene to the stack

        // Handle key press events for the scene
        scene.setOnKeyPressed(keyEvent -> {
            KeyHandler.getInstance().keyPressed(keyEvent);
        });

        primaryStage.setScene(scene);  // Set the scene to the stage
        primaryStage.centerOnScreen();  // Center the stage on the screen
        primaryStage.show();  // Show the stage
    } catch (IOException e) {
        throw new RuntimeException(e);  // Handle any loading errors
    }
}

```