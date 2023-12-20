```cpp
#include <Arduino.h>

#include <WebServer.h>

  

#include <WiFi.h>

// #include <string>

const char *ssid = "hi";

const char *password = "123456789";

WebServer server(80);

  

String indexHtml = String("") + "<!DOCTYPE html>" +

                   "<html>" +

                   "    <head>" +

                   "        <meta charset=\"utf-8\">" +

                   "        <title>ESP32 WebController</title>" +

                   "    </head>" +

                   "    <body>" +

                   "        <h1>Web Controller</h1>" +

                   "        <button onclick=\"test()\" type=\"button\" style=\"height: 100px;width: 200px;background-color: #1aa6f67d;border: 0px;\">Test</button>" +

                   "    </body>" +

                   "    <script type=\"text/javascript\">" +

                   "        function test() {" +

                   "            var ajax = new XMLHttpRequest();" +

                   "            ajax.open(\'get\', \'/test\');" +

                   "            ajax.send();" +

                   "            ajax.onreadystatechange = function() {" +

                   "                if (ajax.readyState == 4 && ajax.status == 200) {" +

                   "                    console.log(ajax.responseText);" +

                   "                }" +

                   "            }" +

                   "        }" +

                   "    </script>" +

                   "</html>";

  

void indexHandler()

{

  server.send(200, "text/html", indexHtml);

}

  

void testHandler()

{

  server.send(200, "text/html", "test seccess");

  Serial.print("test Controller | Time:");

  Serial.println(millis());

}

  

void setup()

{

  // put your setup code here, to run once:

  Serial.begin(115200);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED)

  {

    delay(2000);

    Serial.println(WiFi.status());

    Serial.println("Connecting to WiFi..");

  }

  Serial.println(WiFi.status());

  Serial.println("Connected.");

  Serial.println(WiFi.localIP().toString());

  

  server.on("/", indexHandler);

  server.on("/test", testHandler);

  server.begin();

}

  

void loop()

{

  // put your main code here, to run repeatedly:

  server.handleClient();

}
```