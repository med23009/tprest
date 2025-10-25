## tprest - API REST (Java / Spring Boot)

Ce projet est une API REST en Java (Spring Boot) exposant des endpoints pour gérer des articles.

## Prérequis
- Java 17 (ou compatible avec le projet)
- Maven
- Postman (ou curl) pour tester les API

## Builder le projet
Depuis la racine du projet, lancez :

```bash
mvn clean package -DskipTests
```

## Lancer l'application
Vous pouvez lancer l'application avec Maven ou en exécutant le jar généré.

Avec Maven :

```bash
mvn spring-boot:run
```

Avec le jar (après `mvn package`) :

```bash
java -jar target/*.jar
```

## Profils et ports
Le projet contient plusieurs fichiers de configuration :

- `src/main/resources/application.properties` (port par défaut : 7777)
- `src/main/resources/application-integ.properties` (port : 6666)
- `src/main/resources/application-prod.properties` (port : 9999)

Pour lancer avec un profil spécifique :

```bash
mvn spring-boot:run -Dspring-boot.run.profiles=integ
# ou
java -jar target/*.jar --spring.profiles.active=prod
```

Si aucun profil n'est spécifié, l'application utilise `application.properties` (port 7777).

## Endpoints disponibles
Base path : `/api/articles`

- GET /api/articles/all
  - Retourne la liste de tous les articles (JSON ou XML).

- GET /api/articles/id/{id}
  - Récupère un article par son identifiant (path variable).
  - Ex : `GET http://localhost:7777/api/articles/id/1`

- GET /api/articles?id={id}
  - Récupère un article par son identifiant (paramètre query).
  - Ex : `GET http://localhost:7777/api/articles?id=1`

- POST /api/articles/create
  - Crée un nouvel article. Corps JSON attendu (exemple ci-dessous).
  - Réponse : 201 Created

- PUT /api/articles/update/{id}
  - Met à jour un article existant (body JSON) et renvoie 200 OK.

- DELETE /api/articles/delete/{id}
  - Supprime l'article et renvoie 200 OK.

## Exemple de body (JSON) pour POST / PUT

```json
{
  "title": "Mon article",
  "content": "Contenu de l'article",
  "author": "Auteur"
}
```

Adaptez les champs selon la classe `ArticleDTO` dans le projet.

## Tester avec Postman
1. Ouvrir Postman.
2. Créer une nouvelle requête.
3. Pour une POST / PUT, sélectionner `Body` → `raw` → `JSON` et coller le JSON d'exemple.
4. Définir l'URL (ex : `http://localhost:7777/api/articles/create`).
5. Envoyer la requête et vérifier la réponse.

Conseils utiles :
- Ajouter un environnement Postman avec la variable `base_url` (ex : `http://localhost:7777`) puis l'utiliser comme `{{base_url}}/api/articles/all`.

## Exemples cURL rapides

# GET all
curl -sS -X GET http://localhost:7777/api/articles/all

# GET by id (path)
curl -sS -X GET http://localhost:7777/api/articles/id/1

# POST create
curl -sS -X POST http://localhost:7777/api/articles/create \
  -H "Content-Type: application/json" \
  -d '{"title":"Titre","content":"Texte","author":"Moi"}'

# PUT update
curl -sS -X PUT http://localhost:7777/api/articles/update/1 \
  -H "Content-Type: application/json" \
  -d '{"title":"Nouveau titre","content":"Nouveau texte","author":"Moi"}'

# DELETE
curl -sS -X DELETE http://localhost:7777/api/articles/delete/1

## Documentation / Swagger
Le projet expose aussi la documentation OpenAPI/Swagger si SpringDoc est configuré :

- API docs : `/api-docs`
- Swagger UI : `/docs-ui`

Ex : `http://localhost:7777/docs-ui`

## Tests
Pour lancer les tests unitaires/integration :

```bash
mvn test
```

## Remarques
- Les exemples supposent que l'application tourne sur le port 7777 (valeur par défaut dans `application.properties`).
- Ajustez les corps JSON selon les contraintes de validation définies sur `ArticleDTO`.

---
Si vous voulez, je peux aussi fournir une collection Postman exportable (.json) contenant toutes les requêtes prêtes à l'emploi.
- Understand the architecture of Rest.
- Understand the 04 methods GET, POST, PUT and DELETE.
- Implement Rest with Spring Boot and Spring Rest.
- Handle exceptions with Spring (@ControllerAdvice) when processing a Rest request.
- Understand how Spring Rest can generate the resource in XML format.
- Develop unit tests and integration tests with Spring, Junit and Mockito.
- Do the tests with postman.
- Understand the principle of “Spring Active Profile”.
- Configure and administer the Apache Tomcat version 10.
- Understand how to create the WAR file with Spring Boot using Maven.
- Deploy the WAR file on the container server.
