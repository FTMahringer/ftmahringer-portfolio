# QuizApp

<img src="../../../ftmahringer-portfolio/docs/markdowns/images/quizAppStartpage.png" alt="Snake Game" width="600">

---

## Beschreibung
Eine interaktive Anwendung zum Erstellen und Absolvieren von Quizzen. Zu den Funktionen gehören anpassbare Fragen, Bewertung und benutzerfreundliche Navigation.

#### Als Ideen-Vorlage wurde Kahoot genommen.

---

## Features
- Erstellen Sie benutzerdefinierte Quizze
- Wählen sie die richtigen Antworten aus
- Verfolgen Sie den Fortschritt und die Ergebnisse
- Teilen Sie Quizze mit Freunden
- Selbst erstellter Sound-Player für die Quiz-App

---

## Sound-Player

```java
public class SoundPlayer {

    static String correctSoundPath = "src/main/resources/at/htl/quizapp/sounds/correct.mp3";
    static String wrongSoundPath = "src/main/resources/at/htl/quizapp/sounds/wrong.mp3";

    public static void playMP3(String sound) {
        if (sound == null || sound.isEmpty()) {
            throw new IllegalArgumentException("Sound cannot be null or empty");
        } else if (sound.equals("correct")) {
            sound = correctSoundPath;
        } else if (sound.equals("wrong")) {
            sound = wrongSoundPath;
        }

        // Create a separate thread for audio playback
        String finalSound = sound;
        Thread audioThread = new Thread(() -> {
            try {
                FileInputStream fis = new FileInputStream(finalSound);
                Player player = new Player(fis);
                player.play();
            } catch (FileNotFoundException | JavaLayerException e) {
                e.printStackTrace();
            }
        });

        // Start the audio thread
        audioThread.start();
    }
}
```

---

## Darstellung des Quiz-Editors

<img src="../../../ftmahringer-portfolio/docs/markdowns/images/quizAppCreator-Editor.png" alt="Quiz Editor" width="600">

