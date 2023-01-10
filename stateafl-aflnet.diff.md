# Seulement dans aflnet: afl-clang-fast
# Seulement dans aflnet: afl-clang-fast++


# Les fichiers stateafl/afl-fuzz.c et aflnet/afl-fuzz.c sont différents
Many differences ..


# Les fichiers stateafl/aflnet-replay.c et aflnet/aflnet-replay.c sont différents
```
71c71
<   if ((!strcmp(argv[2], "DTLS12")) || (!strcmp(argv[2], "SIP"))) {
---
>   if ((!strcmp(argv[2], "DTLS12")) || (!strcmp(argv[2], "DNS")) || (!strcmp(argv[2], "SIP"))) {
96,114d95
<   
< #ifdef LOCAL_PORT
<     struct sockaddr_in local_serv_addr;
< 
<     int optval = 1;
<     setsockopt(sockfd, SOL_SOCKET, SO_REUSEPORT, &optval, sizeof(optval));
< 
<     local_serv_addr.sin_family = AF_INET;
<     local_serv_addr.sin_addr.s_addr = INADDR_ANY;
<     local_serv_addr.sin_port = htons(LOCAL_PORT);
< 
<     local_serv_addr.sin_addr.s_addr = inet_addr("127.0.0.1");
<     if (bind(sockfd, (struct sockaddr*) &local_serv_addr, sizeof(struct sockaddr_in)))  {
<       FATAL("Unable to bind socket on local source port");
<     }
< #endif
<   
< 
< 
131,135d111
< 
< #ifdef SEND_DELAY
<     usleep(SEND_DELAY); // send delay
< #endif
< 
```


# Seulement dans stateafl: aflnet-to-plain.c
Not used?


# Les fichiers stateafl/afl-replay.c et aflnet/afl-replay.c sont différents
```
79c79
<   if ((!strcmp(argv[2], "DTLS12")) || (!strcmp(argv[2], "SIP"))) {
---
>   if ((!strcmp(argv[2], "DTLS12")) || (!strcmp(argv[2], "DNS")) || (!strcmp(argv[2], "SIP"))) {
```


# Les fichiers stateafl/config.h et aflnet/config.h sont différents
```
331c331
< #define STATE_STR_LEN 16
---
> #define STATE_STR_LEN 12
```


# Seulement dans stateafl: convert-pcap-replay-format.py


# Les fichiers stateafl/Makefile et aflnet/Makefile sont différents
```
36c36
<   LDFLAGS  += -ldl -lgvc -lcgraph -lm
---
>   LDFLAGS  += -ldl -lgvc -lcgraph -lm -lcap
```


# Seulement dans stateafl: README-AFLnet.md
Probably an old version of the README of aflnet


# Les fichiers stateafl/README.md et aflnet/README.md sont différents
Completely different (no surprise)

