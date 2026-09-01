# Asset binari

Gli asset binari sono file normali del repository.

Regole:
- non aggiungere filtri o backend di storage esterno in `.gitattributes`;
- non committare file pointer al posto del contenuto reale;
- se un asset manca, recuperare il binario originale e committarlo direttamente;
- prima del push verificare che immagini, font, archivi e PDF siano contenuti reali;
- asset **serviti** dal browser: sotto `public_html/` (vedi [public-path-public-html](./public-path-public-html.md)), mai assumere `laravel/public/`.
