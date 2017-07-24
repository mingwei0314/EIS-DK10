EIS-DK10 kit running Windows 10
===
---

# Table of Contents

-   EIS-DK10 kit
-   Connect the sensors
-   Build and Run the sample
-   Send Device Events to IoT Hub
-   Receive messages from IoT Hub
-   Next steps

# EIS-DK10 kit

The EIS-DK10 kit includes:

-   EIS-DK10 device.

# Build and Run the sample

Use Node-RED import flow (Send data to IoT Hub)

[{"id":"e78f478a.ce1a78","type":"inject","z":"95f2b93b.1f9df8","name":"Inject Capability","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":false,"x":120,"y":100,"wires":[["8cde2996.095c78"]]},{"id":"8cde2996.095c78","type":"SUSIIoT-Info","z":"95f2b93b.1f9df8","name":"","topic":"SUSIIoT Info","feature":"All","featuretype":"","x":290,"y":100,"wires":[["10decba4.f7f1b4"]]},{"id":"f0e782b8.a815f","type":"SUSIIoT-Data","z":"95f2b93b.1f9df8","name":"","topic":"SUSIIoT Data","feature":"All","featuretype":"","x":295,"y":136,"wires":[["d11a233a.f65d2"]]},{"id":"b24de484.412328","type":"inject","z":"95f2b93b.1f9df8","name":"Inject Data","topic":"","payload":"","payloadType":"date","repeat":"5","crontab":"","once":false,"x":116,"y":136,"wires":[["f0e782b8.a815f"]]},{"id":"ef4adb07.61b0d8","type":"debug","z":"95f2b93b.1f9df8","name":"","active":true,"console":"false","complete":"payload","x":990,"y":180,"wires":[]},{"id":"10decba4.f7f1b4","type":"function","z":"95f2b93b.1f9df8","name":"parse info","func":"const is_cap = true;\nvar parse_ipso = function(root, path, this_items) {\n    if(\"e\" in root && Array.isArray(root.e)) {\n        var this_path = path.substr(0, path.length - 1);\n        this_items[this_path] = {};\n        for(var idx in root.e) {\n            var item = {\n                \"name\": root.e[idx].n\n            };\n\n            if(is_cap) {\n                item[\"min\"]      = (\"min\" in root.e[idx])? root.e[idx].min : null;\n                item[\"max\"]      = (\"max\" in root.e[idx])? root.e[idx].max : null;\n                item[\"unit\"]     = (\"u\"   in root.e[idx])? root.e[idx].u : null;\n                item[\"type\"]     = (\"v\"   in root.e[idx])? \"v\" : ((\"bv\" in root.e[idx])? \"bv\" : \"sv\");\n                item[\"editable\"] = (\"asm\" in root.e[idx])? (root.e[idx].asm.indexOf('w') !== -1) : false;\n            } else {\n                if(\"v\" in root.e[idx]) {\n                    item.value = root.e[idx].v;\n                } else if(\"bv\" in root.e[idx]) {\n                    item.value = root.e[idx].bv;\n                } else {\n                    item.value = root.e[idx].sv;\n                }\n            }\n\n            this_items[this_path][root.e[idx].id] = item;\n        }\n    } else {\n        for( var k in root) {\n            var child = root[k];\n            if(typeof child === \"object\" && !(Array.isArray(child)))\n                parse_ipso(child, path + k + \"-\", this_items);\n        }\n    }\n};\n\nvar s = msg.payload;\nvar cap = JSON.parse(s);\nvar cap_items = {\"is_cap\": is_cap};\nparse_ipso(cap, \"\", cap_items);\nmsg.payload = JSON.stringify(cap_items);\nreturn msg;\n","outputs":1,"noerr":0,"x":480,"y":100,"wires":[["2a812a08.72f1a6"]]},{"id":"d11a233a.f65d2","type":"function","z":"95f2b93b.1f9df8","name":"parse data","func":"const is_cap = false;\nvar parse_ipso = function(root, path, this_items) {\n    if(\"e\" in root && Array.isArray(root.e)) {\n        var this_path = path.substr(0, path.length - 1);\n        this_items[this_path] = {};\n        for(var idx in root.e) {\n            var item = {\n                \"name\": root.e[idx].n\n            };\n\n            if(is_cap) {\n                item[\"min\"]      = (\"min\" in root.e[idx])? root.e[idx].min : null;\n                item[\"max\"]      = (\"max\" in root.e[idx])? root.e[idx].max : null;\n                item[\"unit\"]     = (\"u\"   in root.e[idx])? root.e[idx].u : null;\n                item[\"type\"]     = (\"v\"   in root.e[idx])? \"v\" : ((\"bv\" in root.e[idx])? \"bv\" : \"sv\");\n                item[\"editable\"] = (\"asm\" in root.e[idx])? (root.e[idx].asm.indexOf('w') !== -1) : false;\n            } else {\n                if(\"v\" in root.e[idx]) {\n                    item.value = root.e[idx].v;\n                } else if(\"bv\" in root.e[idx]) {\n                    item.value = root.e[idx].bv;\n                } else {\n                    item.value = root.e[idx].sv;\n                }\n            }\n\n            this_items[this_path][root.e[idx].id] = item;\n        }\n    } else {\n        for( var k in root) {\n            var child = root[k];\n            if(typeof child === \"object\" && !(Array.isArray(child)))\n                parse_ipso(child, path + k + \"-\", this_items);\n        }\n    }\n};\n\nvar s = msg.payload;\nvar cap = JSON.parse(s);\nvar cap_items = {\"is_cap\": is_cap};\nparse_ipso(cap, \"\", cap_items);\nmsg.payload = JSON.stringify(cap_items);\nreturn msg;\n","outputs":1,"noerr":0,"x":479,"y":136,"wires":[["2a812a08.72f1a6"]]},{"id":"2a812a08.72f1a6","type":"azureiothub","z":"95f2b93b.1f9df8","name":"Azure IoT Hub","protocol":"http","x":680,"y":120,"wires":[["344cd4f6.efed3c"]]},{"id":"344cd4f6.efed3c","type":"SUSIIoT-Control","z":"95f2b93b.1f9df8","name":"","topic":"SUSIIoT Control","x":809,"y":180,"wires":[["ef4adb07.61b0d8"]]}]

# Send Device Events to IoT Hub

Node-RED will auto send platform sensor data per 5 seconds.

# Receive messages from IoT Hub

Refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.

# Next steps

-   [Manage message exchanges between your device and IoT Hub using
    iothub-explorer](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
-   [Store data in Azure Storage](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
-   [Visualize data using PowerBI](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
-   [Visualize data using Web Apps](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
-   Use Machine Learning to predict upcoming data
-   Integrate with Logic Apps to email user about data anomalies