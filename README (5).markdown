# Book Generator Web

A Flask-based web application to generate customizable books. Users can add characters, set book details, generate a plot, preview the structure, and produce a full book (100–400 pages, 10–100 chapters) displayed on-screen and downloadable as Markdown.

## Features
- Add characters with attributes (name, age, gender, occupation, personality, backstory, physical traits, motivations, relationships).
- Set book details (genre, setting, tone, themes, page count, chapter count, conflict intensity, title, key plot points).
- Generate a plot based on characters and settings.
- Preview the book structure with chapter outlines.
- Generate a complete book with a narrative arc, viewable in the browser and downloadable as Markdown.
- Responsive interface with button-styled navigation and error handling.

## Prerequisites
- Python 3.8+ (verify: `python --version` or `python3 --version`)
- Git (verify: `git --version`)

## Setup (Local)
Follow these steps to run the app locally with renamed files, ensuring all buttons and functions work without 404 errors.

1. **Clone or Update Repository**:
   - New:
     ```bash
     git clone https://github.com/your-username/book-generator-web.git
     cd book-generator-web
     ```
   - Existing:
     ```bash
     cd path/to/book-generator-web
     rm -rf templates static app.py requirements.txt Procfile .gitignore README.md output
     ```

2. **Create Project Structure**:
   - Ensure:
     ```
     book-generator-web/
     ├── app.py
     ├── templates/
     │   ├── index.html
     │   ├── character.html
     │   ├── details.html
     │   └── display.html
     ├── static/
     │   └── style.css
     ├── output/
     │   └── .gitkeep
     ├── requirements.txt
     ├── Procfile
     ├── .gitignore
     └── README.md
     ```
   - Run:
     ```bash
     mkdir -p templates static output
     touch output/.gitkeep
     ```
   - Copy artifact content into each file using a text editor (e.g., VS Code).

3. **Verify Structure**:
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
     index.html  character.html Hedging row in `index.html`, `character.html`, `details.html`, `display.html`, and `style.css`. Ensure all templates are renamed correctly.

4. **Set Up Virtual Environment**:
   - Run:
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

6. **Run Application**:
   - Start:
     ```bash
     python app.py
     ```
   - Expected:
     ```
     * Running on http://127.0.0.1:5000
     ```
   - Open `http://127.0.0.1:5000`. See homepage with buttons.

7. **Commit to GitHub** (Optional):
   - Run:
     ```bash
     git add .
     git commit -m "Renamed templates and static files, ensured full functionality"
     git push origin main
     ```

## Usage
1. **Homepage**: `http://127.0.0.1:5000`. See buttons: “Create Your First Character”, “Design Your Book”, etc.
2. **Add Character**:
   - Click “Create Your First Character” or “Add Character” button.
   - URL: `http://127.0.0.1:5000/add_character`.
   - Enter Name: “Alice”, Age: “25”, submit.
   - Redirect to homepage, see character summary.
3. **Set Book Details**:
   - Click “Design Your Book” or “Set Book Details” button.
   - URL: `http://127.0.0.1:5000/set_details`.
   - Enter Genre: “Fantasy”, Setting: “Medieval Kingdom”, Tone: “Epic”, Themes: “Heroism, Betrayal”, Page Count: “200”, Chapter Count: “20”, Conflict Intensity: “Medium”, Title: “The Quest”, submit.
   - See success message.
4. **Generate Plot**:
   - Add another character (Name: “Bob”, Age: “30”).
   - Click “Generate Plot” button.
   - See plot summary.
5. **Preview Structure**:
   - Click “Preview Book Structure” button.
   - See chapter outline.
6. **Generate Book**:
   - Click “Generate Full Book” button.
   - Redirect to `http://127.0.0.1:5000/book_display`.
   - See book content.
   - Click “Download Book” to save as Markdown.

## Troubleshooting
If buttons cause 404s or functions fail:
- **Terminal**:
  - Run `python app.py`. Check for:
    ```
    DEBUG: Accessing add_character route
    ```
    If missing, route not hit.
  - Look for:
    ```
    TemplateNotFound: character.html
    ```
    Solution: Verify `templates/character.html` exists.
- **Files**:
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
    ./templates/character.html
    ./templates/details.html
    ./templates/display.html
    ./static/style.css
    ./output/.gitkeep
    ./.gitignore
    ```
- **Routes**:
  - Confirm `app.py` has:
    ```python
    @app.route("/add_character", methods=["GET", "POST"])
    @app.route("/set_details", methods=["GET", "POST"])
    ```
  - Ensure `index.html` has:
    ```html
    <a href="{{ url_for('add_character') }}" class="button primary">Create Your First Character</a>
    <a href="{{ url_for('set_details') }}" class="button secondary">Design Your Book</a>
    ```
- **Restart Server**:
  - Stop (`Ctrl+C`), rerun:
    ```bash
    python app.py
    ```
- **Browser**:
  - F12 > Network. Click button. Check for 404 on `/add_character`.
  - Clear cache: F12 > Application > Clear site data.
- **Functionality**:
  - If form submits but no output, check terminal for errors (e.g., `Validation error`).
  - Ensure session persists (check logs for `session["generator"]`).
- **Still Failing**:
  - Provide:
    - Terminal output after `python app.py`.
    - URL of 404 (e.g., `http://127.0.0.1:5000/add_character`).
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