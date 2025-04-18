# DSA-Project

*Autocomplete feature and spelling checker*

## Smart Search - README


### Overview

Smart Search is a lightweight, responsive autocomplete system that delivers intelligent word suggestions based on prefix, infix, and suffix patterns. It uses a combination of Trie and Suffix Trie data structures to offer efficient real-time search capabilities. The system consists of a C++ backend server that handles fast query processing and word addition, and a modern frontend interface built with HTML, CSS, and JavaScript. Users can interact with the system through an intuitive UI or programmatically via REST-style endpoints, making it a flexible and extensible platform for enhancing search experiences.


## Features

1. **Autocomplete**: Suggests words matching the input's prefix, infix, or suffix.  
2. **Word Addition**: Users can add custom words to the dictionary with persistent storage.  
3. **Search Timing**: Displays backend search time in microseconds for each query.  
4. **REST API**:  
   - `POST /add-word?word=<word>`: Add a new word.  
   - `GET /suggestions?query=<pattern>`: Get autocomplete suggestions.  
5. **Responsive UI**: Responsive search interface with real-time dropdown suggestions and background video for aesthetics.


## Project Structure

- **`trie.h`**: Implements `Trie` and `SuffixTrie` with methods for inserting, searching, and retrieving matches.  
- **`server.cpp`**: A minimal C++ HTTP server that handles requests for word suggestions and dictionary updates.  
- **`dictionary.txt`**: A plain text word list used to populate the Trie on startup.  
- **Frontend Files**:  
  - `index.html`: Main HTML interface with search and word addition inputs.  
  - `styles.css`: Styling and animation for a modern and clean UI.  
  - `script.js`: Handles user interactions and communicates with the server.  
  - `bgvideo.mp4`: Background video that loops on the homepage.


## Code Structure and Implementation

### Trie Data Structure

- **`Trie` Class**:
  - `insert(word, freq)`: Adds a word to the Trie and increases its frequency.  
  - `autocomplete(pattern)`: Retrieves words based on prefix, infix, and suffix matches.  
  - `isWord(word)`: Checks if the word exists in the Trie.  
  - `findWordsWithInfix(infix)`: Returns all words containing the given infix.

- **`SuffixTrie` Class**:
  - `buildsuffixTrie(word)`: Adds all suffixes of the word for quick suffix matching.  
  - `searchsuffix(suffix)`: Checks if any word ends with the given suffix.


### Server-Side Code

- **`handle_request(client_socket)`**:
  - Handles:
    - `POST /add-word`: Adds new words and updates both file and Trie.
    - `GET /suggestions`: Fetches suggestions from Trie and returns a JSON response.
  - Tracks and returns backend search time in microseconds.

- **Persistent Storage**:
  - On startup, words are loaded from `dictionary.txt`.  
  - New entries are appended to ensure persistence.


### Client-Side Code

- **JavaScript (`script.js`)**:
  - Fetches suggestions from the server in real-time as users type.  
  - Adds new words to the backend via `POST` request.  
  - Displays backend search time and supports keyboard navigation.

- **HTML/CSS**:
  - Typing animation for the title.  
  - Clean form-based UI for search and dictionary updates.  
  - Responsive layout with a full-screen background video.


## Running the Project

### Prerequisites

- C++11 or higher  
- A modern web browser (Chrome, Firefox, etc.)

   ### Setup Instructions
   
1. **Compile the Server**:
   ```bash
   g++ server.cpp -o server -std=c++11
   ```
2. **Run the Server**:
   
   ```bash
   ./server
   ```
4. **Access the Application**:
   Open `http://localhost:8080` in a web browser to access the Smart Search interface.



## Usage

1. **Autocomplete**:
    - Start typing in the search box.
    - Suggestions appear for prefixes, infixes, and suffixes.
    - Select suggestions via mouse or keyboard.

2. **Add New Word**:
    - Type a word in the “Add Word” field and click "Add Word".
    - Word is instantly saved and usable.

3. **Search Time**:
    - Below suggestions, the time taken for backend Trie search is displayed.


## Technologies

- C++: Trie and SuffixTrie implementation for fast word search and dictionary updates
- HTML/CSS: Responsive web interface and layout styling
- JavaScript: Handles user input, dynamic rendering, and fetch API communication
- HTTP: Custom protocol over TCP for request/response between client and server


## Notes

- **Performance**:  
  Trie provides O(L) search where L is the length of the pattern.  
  Infix and suffix search is supported without redundant traversal.

- **Error Handling**:  
  Handles missing or malformed input, file write issues, and invalid HTTP requests.

- **Extensibility**:  
  Can be expanded to support ranking, typo tolerance, or user-specific dictionaries.

   
