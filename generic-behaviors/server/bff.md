---
description: Backend for Frontend
---

# BFF

The "backend for frontend" (BFF) pattern is also sometimes known as the API Gateway because you build it while thinking about the needs of the client app. Therefore, BFF sits between the client apps and the microservices. It acts as a reverse proxy, routing requests from clients to services.

This implementation is inspired by popular library [https://github.com/gorilla/mux](https://github.com/gorilla/mux)

