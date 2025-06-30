# NoteVault Notes Database (`notes_database`)

This service provides the MongoDB instance required by the NoteVault Notes API backend. All note data is persisted here.

---

## 🛠️ Purpose

- Stores users' notes: title, content, tags, categories
- Must be accessible by the Notes API backend service before the backend can start

---

## 🚀 How to Run

### Using Docker (standalone)

```sh
docker run --rm -p 27017:27017 --name notes_db mongo
```

- Exposes MongoDB on default port `27017`
- Data will be ephemeral unless using a volume; adjust per your needs

### With Docker Compose or Orchestration

If using a `docker-compose.yml` or similar, the service name should match `notes_database`:
```yaml
services:
  notes_database:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - ./data:/data/db  # Optional, for persistence
```

### Configuration

| Variable        | Description                         | Example                   |
| --------------- | ----------------------------------- | ------------------------- |
| `MONGODB_URL`   | MongoDB connection URI              | `mongodb://notes_database:27017` |
| `MONGODB_DB`    | Database name for notes             | `notesdb`                 |

These should be set in the backend container/environment.

---

## 🧩 Integration Example

- Database URL from backend:  
  `MONGODB_URL=mongodb://notes_database:27017`
- Database name from backend:  
  `MONGODB_DB=notesdb`

---

## 📦 Data Storage

By default, no authentication or volumes are configured. For persistence, add a volume; for production, configure users/passwords as needed.

---

## 🔄 Usage Order

> **Start this MongoDB service _before_ starting the Notes API backend.**

---

## 📚 Resources

- [MongoDB Docker Hub](https://hub.docker.com/_/mongo)
- [MongoDB Documentation](https://www.mongodb.com/docs/manual/)
