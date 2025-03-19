What is right and why?

frontend:  
  build:  
    context: .  
    dockerfile: frontend/Dockerfile

backend:  
  build:  
    context: .backend  
    dockerfile: backend/Dockerfile

or

frontend:  
  build:  
    context: ./frontend
    dockerfile: Dockerfile

backend:  
  build:  
    context: ./backend  
    dockerfile: Dockerfile

Структура проекта
```
.
├── docker-compose.yml
├── frontend
│   ├── Dockerfile
│   └── notes.Blazor
└── backend
    ├── Dockerfile
    ├── notes.api
    ├── notes.data
    └── notes.models

```