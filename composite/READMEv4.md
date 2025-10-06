

L'entité qui consomme de l'electricité se nomme un Site. C'est par exemple : une usine, un bâtiment, une maison...

```mermaid
classDiagram
class Site {
+UUID id
+String numeroPDL
+String segment
+float consommation()
}
```

