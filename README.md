# flow5
Este repositorio adquiere la información directamente de OpenWeather.Map

Primero entramos al siguiente link; https://openweathermap.org/, en e dónde nos registramos.

Segundo creamos una API Key (https://home.openweathermap.org/api_keys)

Tercero API CALL

Forma general
https://api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={API key}

Nota: La forma general se consiguió directamente en la página mencionada.

Forma personal
https://api.openweathermap.org/data/2.5/weather?lat=19.44519163299204&lon=-99.20614630492445&appid=520c194bdaaacfb92a1c81ca67c668b6&units=metric

Estas cordeandas se obtuvieron con Google Maps de acuerdo a la ubicación deseada, y esa URl se pone en el nodo http request.

&units=metric   : Son las unidades.

En Node RED, Tendremos lo siguiente:
--------------------------------------------------------------------------------------------------------------------------------
Para informacion personal

Nodo Function Temperatura

msg.payload = msg.payload.main.temp;

global.set ("tempFlow5",msg.payload);

return msg;

Nodo Function Humedad

msg.payload = msg.payload.main.humidity;

global.set ("humFlow5",msg.payload);

return msg;

--------------------------------------------------------------------------------------------------------------------------------
Para informacion general

codigoIoT/g7/mosquitto/flow5

Nodo function Temperatura

msg.topic = msg.payload.id;

msg.payload = msg.payload.temp;

return msg;

Nodo function Humedad

msg.topic = msg.payload.id;

msg.payload = msg.payload.hum;

return msg;

--------------------------------------------------------------------------------------------------------------------------------

Enviador

msg.payload = '{"id":"Zuriel","temp":'+global.get ("tempFlow5")+',"hum":'+global.get ("humFlow5")+'}';
return msg;

[![Nodos-para-el-flow5.png](https://i.postimg.cc/85Z34GqB/Nodos-para-el-flow5.png)](https://postimg.cc/ygSv6M6k)


Finalmente, tenemos la siguiente interfaz:

[![Interfaz-Flow5.png](https://i.postimg.cc/t49MKYpt/Interfaz-Flow5.png)](https://postimg.cc/ykrj96Jk)


Interfaz desde un dispositivo movil:

[![Interfaz-desde-un-Movil.jpg](https://i.postimg.cc/4xZxjbYL/Interfaz-desde-un-Movil.jpg)](https://postimg.cc/vcqyVnLf)
