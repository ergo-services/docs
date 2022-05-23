---
description: Web API Gateway behavior implementation
---

# Web

The _Web API Gateway_ pattern is also sometimes known as the "_Backend For Frontend_" (BFF)  because you build it while thinking about the needs of the client app. Therefore, BFF sits between the client apps and the microservices. It acts as a reverse proxy, routing requests from clients to services.

This implementation is inspired by the popular library [https://github.com/gorilla/mux](https://github.com/gorilla/mux)

