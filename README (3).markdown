# Book Generator Web

A Flask-based web application to generate customizable books. Users can add characters, set book details, generate a plot, preview the structure, and produce a full book (100–400 pages, 10–100 chapters) displayed on-screen and downloadable as Markdown.

## Features
- Add characters with attributes (name, age, gender, occupation, personality, backstory, physical traits, motivations, relationships).
- Set book details (genre, setting, tone, themes, page count, chapter count, conflict intensity, title, key plot points).
- Generate a plot based on characters and settings.
- Preview the book structure with chapter outlines.
- Generate a complete book with a narrative arc, viewable in the browser and downloadable as Markdown.
- Responsive interface with error handling.

## Prerequisites
- Python 3.8+ (verify with `python --version` or `python3 --version`)
- Git (verify with `git --version`)

## Setup (Local)
Follow these steps to run the app locally and fix 404 errors when clicking links.

1. **Clone or Update the Repository**:
   - New repository:
     ```bash
     git clone https://github.com/your-username/book-generator-web.git
     cd book-generator-web
     ```
   - Existing repository:
     ```bash
     cd path/to/book-generator-web
     rm -rf templates static app.py requirements.txt Procfile .gitignore README.md output
     ```

2. **Create the Project Structure**:
   - Ensure:
     ```
     book-generator-web/
     ├── app.py
     ├── templates/
     │   ├── index.html
     │   ├── add_character.html
     │   ├── set_details.html
     │   └── book_display.html
     ├── static/
     │   └── style.css
     ├── output/
     │   └── .gitkeep
     ├── requirements.txt
     ├── Procfile
     ├── .gitignore
     └── README.md
     ```
   - Create directories:
     ```bash
     mkdir -p templates static output
     touch output/.gitkeep
     ```
   - Copy artifact content into each file using a text editor (e.g., VS Code).

3. **Verify File Structure**:
   - Run:
     ```bash
     ls -R
     ```
     Expected:
     ```
     .:
     app.py  output  Procfile  README.md  requirements.txt  static  templates  .gitignore

     ./output:
     .gitkeep

     ./static:
     style.css

     ./templates:
     add_character.html  book_display.html  index.html  set_details.html
     ```

4. **Set Up Virtual Environment**:
   - Create and activate:
     ```bash
     python -m venv venv
     source venv/bin/activate  # Windows: venv\Scripts\activate
     ```

5. **Install Dependencies**:
   - Run:
     ```bash
     pip install -r requirements.txt
     ```
   - Verify Flask:
     ```bash
     pip show flask
     ```

6. **Run the Application**:
   - Start:
     ```bash
     python app.py
     ```
   - Expected:
     ```
     * Serving Flask app 'app'
     * Debug mode: on
     * Running on http://127.0.0.1:5000
     ```
   - Open `http://127.0.0.1:5000`. See homepage with “Welcome to Book Generator” and navigation.

7. **Commit to GitHub** (Optional):
   - Run:
     ```bash
     git add .
     git commit -m "Fix 404 errors and ensure functionality"
     git push origin main
     ```

## Usage
1. **Homepage**: `http://127.0.0.1:5000`.
2. **Add Character**:
   - Click “Create Your First Character” (`/add_character`).
   - Enter Name: “Alice”, Age: “25”, submit.
   - See summary on homepage.
3. **Set Book Details**:
   - Click “Design Your Book” (`/set_details`).
   - Enter Genre: “Fantasy”, Setting: “Medieval Kingdom”, Tone: “Epic”, Themes: “Heroism, Betrayal”, Page Count: “200”, Chapter Count: “20”, Conflict Intensity: “Medium”, Title: “The Quest”, submit.
   - See success message.
4. **Generate Plot**:
   - Add another character (Name: “Bob”, Age: “30”).
   - Click “Generate Plot”.
   - See plot summary.
5. **Preview Structure**:
   - Click “Preview Book Structure”.
   - See chapter outline.
6. **Generate Book**:
   - Click “Generate Full Book”.
   - View book on `/book_display`.
   - Download via “Download Book”.

## Troubleshooting 404 Errors
If links give 404 errors:
- **Check Terminal**:
  - Run `python app.py`. Look for:
    ```
    DEBUG: Accessing add_character route
    ```
    If missing, routes aren’t hit.
  - Look for:
    ```
    TemplateNotFound: add_character.html
    ```
    Solution: Verify `templates/add_character.html` exists.
- **Verify Files**:
  - Run:
    ```bash
    find . -type f
    ```
    Expected:
    ```
    ./app.py
    ./requirements.txt
    ./Procfile
    ./README.md
    ./templates/index.html
    ./templates/add_character.html
    ./templates/set_details.html
    ./templates/book_display.html
    ./static/style.css
    ./output/.gitkeep
    ./.gitignore
    ```
- **Check Routes**:
  - Confirm `app.py` has:
    ```python
    @app.route("/add_character", methods=["GET", "POST"])
    @app.route("/set_details", methods=["GET", "POST"])
    ```
  - Ensure `index.html` has:
    ```html
    <a href="{{ url_for('add_character') }}">Create Your First Character</a>
    <a href="{{ url_for('set_details') }}">Design Your Book</a>
    ```
- **Restart Server**:
  - Stop (`Ctrl+C`) and rerun:
    ```bash
    python app.py
    ```
- **Browser**:
  - Open F12 > Network. Click a link. Check for 404 on `/add_character` or `/set_details`.
  - Clear cache: F12 > Application > Clear site data.
- **Still Failing**:
  - Provide:
    - Terminal output after `python app.py`.
    - URL of the 404 (e.g., `http://127.0.0.1:5000/add_character`).
    - `ls -R` output.
    - OS and Python version.

## Optional: Deploy to Heroku
1. Install Heroku CLI:
   ```bash
   brew tap heroku/brew && brew install heroku  # macOS
   ```
2. Deploy:
   ```bash
   heroku login
   heroku create book-generator-web
   git push heroku main
   heroku open
   ```

## Alternative Hosting
- **Render**: `https://render.com`, Build: `pip install -r requirements.txt`, Start: `gunicorn app:app`.
- **ngrok**:
  ```bash
  pip install pyngrok
  ngrok http 5000
  ```

## License
MIT License.

## Contributing
Fork, modify, submit pull request.