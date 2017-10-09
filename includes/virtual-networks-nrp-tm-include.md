## <a name="traffic-manager-profile"></a>Profil Menedżera ruchu
Menedżera ruchu i jego zasobu punktu końcowego podrzędne umożliwiają DNS tooendpoints routingu na platformie Azure i poza platformą Azure. Taki podział ruchu podlega metody zasad routingu. Menedżer ruchu umożliwia także monitorowane toobe kondycji punktu końcowego, a ruch odpowiednio kierowane oparty na powitania kondycji punktu końcowego. 

| Właściwość | Opis |
| --- | --- |
| **trafficRoutingMethod** |Możliwe wartości to *wydajności*, *ważone*, i *priorytet* |
| **dnsConfig** |Nazwa FQDN hello profilu |
| **Protokół** |Protokół monitorowania, możliwe wartości to *HTTP* i *protokołu HTTPS* |
| **Port** |monitorowanie portu |
| **Ścieżka** |Ścieżka monitorowania |
| **Punkty końcowe** |kontener dla punktu końcowego zasobów |

### <a name="endpoint"></a>Endpoint
Punkt końcowy jest zasobem podrzędne profil Menedżera ruchu. Reprezentuje usługę lub ruchu użytkowników toowhich punktu końcowego sieci web jest dystrybuowany na podstawie zasad hello skonfigurowane w hello zasobów profilu usługi Traffic Manager. 

| Właściwość | Opis |
| --- | --- |
| **Typ** |Witaj typ punktu końcowego hello, możliwe wartości to *punktu końcowego usługi Azure*, *zewnętrznego punktu końcowego*, i *zagnieżdżone punktu końcowego* |
| **Element targetResourceId** |publiczny adres IP punktu końcowego usługi lub sieci web. Może to być platformy Azure lub zewnętrznego punktu końcowego. |
| **Waga** |Waga punktu końcowego używane w ruchu zarządzania. |
| **Priorytet** |priorytet punktu końcowego hello, używane toodefine działania trybu failover |

Przykład Traffic Manager w formacie Json: 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Dodatkowe zasoby
Odczyt [dokumentacja interfejsu API REST dla Menedżera ruchu](https://msdn.microsoft.com/library/azure/mt163664.aspx) Aby uzyskać więcej informacji.

