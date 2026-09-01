# One.Metal 1.2.0

Version corrigée du projet One.Metal.

## Architecture
- Mobile Flutter dans `mobile/`
- API FastAPI dans `backend/`
- SQLite par défaut pour le développement
- PostgreSQL recommandé pour la production
- Ollama pour le chat IA auto-hébergé

## Développement backend
```bash
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

## Docker
Copier `backend/.env.example` vers `backend/.env`, remplacer obligatoirement les secrets et paramètres de production, puis :
```bash
docker compose up --build -d
```
Le volume Docker ne masque que `storage/`, afin de ne pas cacher le code de l'API. FastAPI documente cette approche de conteneurisation et le lancement via Uvicorn/FastAPI.

## Ollama
Installer Ollama sur le serveur IA et définir `OLLAMA_URL` et `OLLAMA_MODEL`. Le chat renvoie HTTP 503 si le moteur n'est pas disponible plutôt que de simuler une réponse.

## Mobile
```bash
cd mobile
flutter pub get
flutter run --dart-define=API_BASE_URL=https://votre-api.example/api
```
Pour Android émulateur, la valeur par défaut utilise `10.0.2.2:8000`.

## Premium
- Prix: 10 000 XOF / 30 jours
- WhatsApp administrateur: +225 02 08 94 36
- Activation via endpoint administrateur ou contact WhatsApp
- Le statut Premium est vérifié côté serveur.

## Sécurité
En production, utiliser HTTPS, une clé JWT aléatoire longue, un mot de passe admin fort, des origines CORS explicites, une base PostgreSQL et des sauvegardes. Ne jamais mettre de secrets dans l'application mobile.

## Limite importante
Les moteurs image/vidéo/voix sont des adaptateurs et nécessitent leurs propres modèles auto-hébergés et ressources GPU. Le projet ne simule pas leur fonctionnement.
