# Quadbeat: Graph-Based Music Recommendation System

Quadbeat is a Java Spring Boot web application that provides music recommendations using graph-based algorithms. It allows users to search for songs, get recommendations based on songs, artists, or mood, and create a temporary playlist—all through a modern web interface.

---

## Features

- **Song Search:** Search for songs by title or artist.
- **Mood-Based Recommendations:** Get song recommendations based on selected moods (Energetic, Neutral, Melancholy).
- **Graph-Based Recommendations:** Uses BFS and Dijkstra algorithms on song, artist, and mood graphs for recommendations.
- **Duplicate Filtering:** Smart filtering to avoid duplicate or overly similar songs in recommendations.
- **Temporary Playlist:** Add recommended songs to a session-based playlist (no database required).
- **Modern UI:** Responsive and user-friendly web interface.

---

## Tech Stack

- **Backend:** Java 21, Spring Boot 3.2.2, Maven
- **Frontend:** HTML, CSS, JavaScript (vanilla)
- **Data:** CSV dataset of songs (with fields like title, artist, genre, mood, tempo, popularity, etc.)

---

## Project Structure

```
Quadbeat/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── Quadbeat/
│   │   │   │   ├── RecommendationService.java
│   │   │   │   ├── RecommendationController.java
│   │   │   │   ├── RecommendationDto.java
│   │   │   ├── model/
│   │   │   │   ├── GraphBuilder.java
│   │   │   │   ├── Song.java
│   │   │   │   ├── Edge.java
│   │   │   ├── resources/
│   │   │   │   ├── static/
│   │   │   │   │   ├── index.html
│   │   │   │   │   ├── script.js
│   │   │   │   │   ├── styles.css
│   │   │   ├── application.properties
├── pom.xml
```

---

## How It Works

### Data Loading

- Songs are loaded from a CSV file at startup.
- Each song has attributes: `songId`, `title`, `artist`, `language`, `genre`, `releaseYear`, `mood`, `tempo`, `popularity`.

### Graph Construction

- **Song-Based Graph:** Connects songs with similar genre, tempo, mood, and popularity.
- **Artist-Based Graph:** Connects songs by the same artist, genre, mood, and tempo.
- **Mood-Based Graph:** Connects songs with similar mood, tempo, and genre.

### Recommendation Algorithms

- **BFS (Quick Match):** Finds songs closely related to the seed song.
- **Dijkstra (Best Match):** Finds best matches based on edge weights (similarity).

### Duplicate Filtering

- Recommendations are filtered to avoid:
  - Exact duplicates (same title and artist)
  - Remixes/covers (very similar titles and artists)
  - Duplicates within the recommendation list (keeps the highest score)

### REST API Endpoints

- `GET /search?query=...` — Search for songs by title or artist.
- `GET /recommend?songId=...&graphType=...&algorithm=...` — Get recommendations.
  - `graphType`: `SONG_BASED`, `ARTIST_BASED`, `MOOD_BASED`
  - `algorithm`: `BFS`, `DIJKSTRA`

### Frontend

- **index.html:** Main UI with search, mood buttons, recommendations, and playlist.
- **script.js:** Handles user interactions, API calls, and dynamic UI updates.
- **styles.css:** Modern, responsive styling.

---

## How to Run

### Prerequisites

- Java 21 JDK
- Maven (or use the included Maven wrapper)

### Steps

1. **Clone the repository and navigate to the project:**
   ```bash
   cd Quadbeat
   ```

2. **Run the application:**
   - Using Maven Wrapper:
     ```bash
     ./mvnw spring-boot:run
     ```
   - Or with Maven:
     ```bash
     mvn spring-boot:run
     ```

3. **Open your browser and go to:**
   ```
   http://localhost:8080
   ```

---

## Usage

- **Search:** Enter a song or artist and click "Search".
- **Mood Recommendations:** Click a mood button to get recommendations.
- **Add to Playlist:** Click "Add to Playlist" on any recommended song.
- **View Playlist:** See your current playlist in the UI.
- **Remove/Clear Playlist:** Remove individual songs or clear the entire playlist.

---

## Customization

- **Dataset:** Replace or update the CSV file in `Dataset/` to use your own songs.
- **Recommendation Logic:** Modify `GraphBuilder.java` and `RecommendationService.java` for custom recommendation strategies.
- **UI:** Edit `index.html`, `script.js`, and `styles.css` for frontend changes.

---

## License

This project is for educational and demonstration purposes.

---

## Authors

- [Your Name Here]

---

## Acknowledgements

- Built with Spring Boot, Java, and open web technologies. 