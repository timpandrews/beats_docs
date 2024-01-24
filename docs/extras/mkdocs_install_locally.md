1. Clone the repository:

    ```bash
    git clone [repository_url]
    ```

2. Navigate to the Project directory

    ```bash
    cd beats_docs
    ```

3. Create and activate a virtual environment

    ```bash
    python3 -m venv _env
    source _env/bin/activate
    ```

4. Install dependencies
    ```bash
    pip install -r requirements.txt
    ```

5. Run Server
```bash 
mkdocs serve --dev-addr=127.0.0.1:8001
```
6. Local URL:   
[http://127.0.0.1:8001/](http://127.0.0.1:8001/)
