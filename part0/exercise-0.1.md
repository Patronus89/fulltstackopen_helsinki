sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes note in text field and clicks Save button
    
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note right of server: Server saves the new note to notes list
    server-->>browser: HTTP 302 Redirect (Location: /notes)
    deactivate server
    
    Note right of browser: Browser follows redirect and makes new GET request
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    Note right of server: Server returns updated notes list including the new note
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, { "content": "New note content", "date": "2023-1-2" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders all notes including the new one
