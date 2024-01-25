# monk-opengpts

This repository contains Monk.io template to deploy openGPTs (https://github.com/langchain-ai/opengpts).


## Prerequisites

- Install Monk
- Register and Login Monk
- Add Cloud Provider


## Clone Repository

```bash
git clone https://github.com/monk-io/monk-opengpts
```


## Make public

OpenGPTs requires https to work correctly, so you need to have HTTPS balancer section in your template or configure it in another way
```
balancers:
    opengpts:
      type: HTTPS
      port: <- service-port("opengpts/frontend","frontend")
      frontend-port: 80
      instances:
        - opengpts/frontend
      health-check:
        kind: TCP
        url: /
        interval: 5
        request: ''
        response: ''
      tls-certificate: <- secret("monk-domain-cert")
      tls-key: <- secret("monk-domain-key")
      tls-chain: <- secret("monk-domain-chain") default("")
```


## Load Template

```bash
cd monk-opengpts
monk load MANIFEST
```


## Deploy

```bash
monk run opengpts/stack
? Select tag to run [local/opengpts/stack] on: prod
✔ Starting the run job: local/opengpts/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% redis:latest sergtest10
✔ [================================================] 100% gcr.io/monk-releases/opengpts-backend:latest sergtest10
✔ [================================================] 100% gcr.io/monk-releases/opengpts-frontend:latest sergtest10
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/redis connections graph updating DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/redis connections graph has been updated DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/redis services initialization DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/redis services have been initialized DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/frontend connections graph updating DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/frontend connections graph has been updated DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/frontend services initialization DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/frontend services have been initialized DONE
✔ Host ports have been added to container 5a1195f14cd3f74cb61e38a2de2cd2aa-al-opengpts-redis-redis DONE
✔ New container 5a1195f14cd3f74cb61e38a2de2cd2aa-al-opengpts-redis-redis created DONE
✔ Container 5a1195f14cd3f74cb61e38a2de2cd2aa-al-opengpts-redis-redis network has been configured DONE
✔ Host ports have been added to container 58525f5eb253184deabd279945550e44-ngpts-frontend-frontend DONE
✔ New container 58525f5eb253184deabd279945550e44-ngpts-frontend-frontend created DONE
✔ Container 58525f5eb253184deabd279945550e44-ngpts-frontend-frontend network has been configured DONE
✔ Container 5a1195f14cd3f74cb61e38a2de2cd2aa-al-opengpts-redis-redis has been started DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/backend connections graph updating DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/backend connections graph has been updated DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/backend services initialization DONE
✔ Runnable templates/local/opengpts/stack/runnables/templates/local/opengpts/backend services have been initialized DONE
✔ Container 58525f5eb253184deabd279945550e44-ngpts-frontend-frontend has been started DONE
✔ Host ports have been added to container 84712bcadaa7127cd444841cab36265f-pengpts-backend-backend DONE
✔ New container 84712bcadaa7127cd444841cab36265f-pengpts-backend-backend created DONE
✔ Container 84712bcadaa7127cd444841cab36265f-pengpts-backend-backend network has been configured DONE
✔ Container 84712bcadaa7127cd444841cab36265f-pengpts-backend-backend has been started DONE
✔ Started local/opengpts/stack
🔩 templates/local/opengpts/stack
 └─🧊 Peer sergtest10
    ├─🔩 templates/local/opengpts/frontend 
    │  └─📦 58525f5eb253184deabd279945550e44-ngpts-frontend-frontend running
    │     ├─🧩 gcr.io/monk-releases/opengpts-frontend:latest
    │     └─🔌 open (public) 35.247.67.82:5173 -> 5173
    ├─🔩 templates/local/opengpts/backend  
    │  └─📦 84712bcadaa7127cd444841cab36265f-pengpts-backend-backend running
    │     ├─🧩 gcr.io/monk-releases/opengpts-backend:latest
    │     └─🔌 open 35.247.67.82:8000 -> 8000
    └─🔩 templates/local/opengpts/redis    
       └─📦 5a1195f14cd3f74cb61e38a2de2cd2aa-al-opengpts-redis-redis running
          ├─🧩 redis:latest                          
          ├─💾 /var/lib/monkd/volumes/opengpts/redis -> /data
          └─🔌 open 35.247.67.82:6379 -> 6379

💡 You can inspect and manage your above stack with these commands:
        monk logs (-f) local/opengpts/stack - Inspect logs
        monk shell     local/opengpts/stack - Connect to the container's shell
        monk do        local/opengpts/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Variables

Description of variables: https://github.com/langchain-ai/opengpts