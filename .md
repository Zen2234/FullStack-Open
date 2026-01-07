sequenceDiagram
    participant browser
    participant server

    Note right of browser: Käyttäjä kirjoittaa tekstin lomakkeeseen ja painaa "Save"

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note left of server: Palvelin vastaanottaa lomakedatan (content)
    Note left of server: Palvelin tallentaa uuden muistiinpanon
    server-->>browser: HTTP 302 Redirect (/exampleapp/notes)
    deactivate server

    Note right of browser: Selain seuraa uudelleenohjausta ja lataa sivun uudelleen

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET main.css
    browser->>server: GET main.js

    Note right of browser: JavaScript hakee muistiinpanot palvelimelta

    browser->>server: GET data.json
    activate server
    server-->>browser: JSON, jossa myös uusi muistiinpano
    deactivate server

    Note right of browser: Selain renderöi muistiinpanot näkyviin
