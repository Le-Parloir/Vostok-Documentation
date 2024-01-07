# La signalétique dans les locaux

## Les logos lumineux

Ils indiquent les différents états de l'antenne et des studios

### Listing des logos

- Logo n°1 : porte studio 1 : 192.168.1.50 : sn007
- Logo n°2 : porte régie : 192.168.1.51 : sn006
- Logo n°3 : porte studio 2 : 192.168.1.52 : sn002
- Logo n°4 : vitre régie : 192.168.1.53 : sn005
- Logo n°5 : vitre studio 1 : 192.168.1.54 : sn008

### Couleurs des logos

- Boot default: solid yellow (100,100,0)

- AUTOPLAY (USER_10) : logo et onde sont en 'beige'

```
EXEC_SEND_HTTP_GET http://192.168.1.50/w?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.50/v?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.51/w?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.51/v?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.52/w?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.52/v?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.53/w?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.53/v?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.54/w?r=255&g=245&b=214
EXEC_SEND_HTTP_GET http://192.168.1.54/v?r=255&g=245&b=214
```

- REGIE UNMUTE (USER_11) : l'onde  passe en 'bleu Vostok'

```
EXEC_SEND_HTTP_GET http://192.168.1.50/w?r=0&b=75&g=175
EXEC_SEND_HTTP_GET http://192.168.1.51/w?r=0&b=75&g=175
EXEC_SEND_HTTP_GET http://192.168.1.52/w?r=0&b=75&g=175
EXEC_SEND_HTTP_GET http://192.168.1.53/w?r=0&b=75&g=175
EXEC_SEND_HTTP_GET http://192.168.1.54/w?r=0&b=75&g=175
```

- SILENCE SUR POSTE AUTO (USER_12) : l'onde passe en rouge

```
EXEC_SEND_HTTP_GET http://192.168.1.50/w?r=255
EXEC_SEND_HTTP_GET http://192.168.1.51/w?r=255
EXEC_SEND_HTTP_GET http://192.168.1.52/w?r=255
EXEC_SEND_HTTP_GET http://192.168.1.53/w?r=255
EXEC_SEND_HTTP_GET http://192.168.1.54/w?r=255
```


