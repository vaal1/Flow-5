# Flow-5
Intercambiar información por API con todo el grupo

Instrucciones 

1. Iniciar Node-Red
2. Agregar al flow un enviador de infromación
- Enviar la Información por JSON
3. Agregar al flow un escuchador de información
4. Agregar umn broker publico
- nslookup broker.hivemq.com
- 35.156.177.225
- codigoIoT/flow5/mqtt/clima

### Nodo function Temperatura API
global.set ("tempAPI", msg.payload.main.temp);
msg.payload = msg.payload.main.temp;
msg.topic = "Temperatura";
return msg;

### Nodo function Humedad API
msg.payload = msg.payload.main.humidity;
global.set ("humAPI", msg.payload);
msg.topic = "Humedad";
return msg;

### Variables para el Broker Publico
- id
- temp
- hum

### Nodo function JSON Publico
msg.payload = '{"id":"Hugo Vargas. Col Doctores, CDMX","temp":' + global.get("tempAPI")+',"hum":' + global.get ("humAPI") +'}';
return msg;

### Nodo function Temperatura Publica API
msg.topic = msg.payload.id;
msg.payload = msg.payload.temp;
return msg;


### Nodo function Humedad Publica API
msg.topic = msg.payload.id;
msg.payload = msg.payload.hum;
return msg;
