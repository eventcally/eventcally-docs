---
title: API Authorization
lang: de
redirect_from: /goto/dev-api-auth/
---
Um auf die API zuzugreifen, müssen Anfragen authorisiert werden. Die möglichen Authorisierungstypen werden im Folgenden beschrieben.

Bitte beachte die Informationen zum [Rate Limit]({% post_url /developer/2025-05-21-api-rate-limit %}).

## API Schlüssel

Anfragen können per API Schlüssel authorisiert werden. **Mit dieser Methode kann ausschließlich auf öffentliche Daten ohne Nutzer-Kontext zugegriffen werden**.

### API Schlüssel erstellen

Gehe auf dein Profil und wähle im Bereich "Entwickler" den Punkt "API Schlüssel". *Alternativ kann man auch für Organisationen API Schlüssel erstellen (Menü > Organisation > Api Schlüssel)*. Klicke auf "API Schlüssel erstellen". Wähle einen Namen und klicke auf "Erstellen". Auf der folgenden Seite wird der API Schlüssel angezeigt.

### API aufrufen

Um auf die API zuzugreifen, muss der erhaltene API Schlüssel im Header `x-api-key` des HTTP Requests übergeben werden.

```bash
curl --request GET \
  --url https://{DOMAIN}/api/v1/events \
  --header 'x-api-key: {API_KEY}' \
  --header 'content-type: application/json'
```

## OAuth2/OpenID

Die Authorisierung kann mittels OAuth2/OpenID realisiert werden: [Mehr Informationen zu OAuth2](https://auth0.com/de/intro-to-iam/what-is-oauth-2).

Es werden die OAuth Grants `authorization_code` und `client_credentials` unterstützt. Um Zugriffsdaten zu erhalten, muss eine OAuth Client Definition erstellt werden. Gehe dazu auf dein Profil und wähle im Bereich "Entwickler" den Punkt "OAuth2 Clients".

### Öffentlicher Lese-Zugriff

Dieser Abschnitt beschreibt den Zugriff auf öffentliche Daten ohne Nutzer-Kontext. Dafür wird der OAuth Grant `client_credentials` verwendet: [Mehr Informationen zum Flow](https://auth0.com/docs/get-started/authentication-and-authorization-flow/call-your-api-using-the-client-credentials-flow).

#### Client erstellen

Gehe auf dein Profil und wähle im Bereich "Entwickler" den Punkt "OAuth2 Clients". Klicke auf "OAuth2 Client hinzufügen". Wähle einen Namen und lasse die übrigen Eingabefelder leer. Klicke auf "Speichern". Auf der folgenden Seite stehen die erforderlichen Informationen "Client ID" und "Client Secret".

#### Access token anfragen

Um auf die API zuzugreifen, muss ein Access Token angefordert werden. Dafür muss eine POST-Anfrage an die Token URL gesendet werden.

```bash
curl  --request POST \
  --url 'https://{DOMAIN}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data client_id={YOUR_CLIENT_ID} \
  --data client_secret={YOUR_CLIENT_SECRET}
```

#### Antwort verarbeiten

Die Antwort erhält Informationen wie den Access Token im JSON-Format.

```javascript
{
  "access_token":"{ACCESS_TOKEN}",
  "token_type":"Bearer",
  "expires_in":86400
}
```

#### API aufrufen

Um auf die API zuzugreifen, muss der erhaltene Access Token as Bearer Token im Authorization Header des HTTP Requests übergeben werden.

```bash
curl --request GET \
  --url https://{DOMAIN}/api/v1/events \
  --header 'authorization: Bearer {ACCESS_TOKEN}' \
  --header 'content-type: application/json'
```
