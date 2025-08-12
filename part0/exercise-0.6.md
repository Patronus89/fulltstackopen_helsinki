sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes note in text field and clicks Save button

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note right of server: Server saves the new note and responds with JSON
    server-->>browser: {"message": "note created"}
    deactivate server

    Note right of browser: JavaScript updates the notes list on the page without reload
    Note right of browser: JavaScript clears the input field
    Note right of browser: New note appears immediately in the list
