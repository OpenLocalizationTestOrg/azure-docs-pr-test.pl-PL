## <a name="route-tables"></a>Tabele tras
Zasoby tabeli tras zawiera toodefine tras jak przepływa ruch w ramach infrastruktury platformy Azure. Można użyć zdefiniowanych przez użytkownika tras (przez) toosend cały ruch z jednej podsieci tooa urządzenie wirtualne, takie jak system wykrywania zapory lub nieautoryzowanego dostępu (ID). Możesz skojarzyć toosubnets tabeli tras. 

Tabele tras zawierają hello następujące właściwości.

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **trasy** |Trasy definiowane przez kolekcję użytkownika w tabeli tras hello |zobacz [trasy zdefiniowane przez użytkownika](#User-defined-routes) |
| **podsieci** |Kolekcja tabeli tras podsieci hello jest stosowany zbyt|zobacz [podsieci](#Subnets) |

### <a name="user-defined-routes"></a>Trasy zdefiniowane przez użytkownika
Toospecify Udr wysyłania ruchu sieciowego, można utworzyć na podstawie jego adresu docelowego. Trasa można traktować jako definicji bramy domyślnej hello na podstawie adresu docelowego hello pakietów sieciowych.

Udr zawierają hello następujące właściwości. 

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **addressPrefix** |Prefiks adresu lub pełny adres IP dla miejsca docelowego hello |192.168.1.0/24, 192.168.1.101 |
| **Typ następnego przeskoku** |Typu ruchu hello urządzenie zostanie wysłany|Internet VirtualAppliance, Brama sieci VPN |
| **adres IP następnego przeskoku** |Adres IP następnego przeskoku hello |192.168.1.4 |

Przykładowa tabela tras w formacie JSON:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Dodatkowe zasoby
* Uzyskaj więcej informacji [Udr](../articles/virtual-network/virtual-networks-udr-overview.md).
* Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) dla tabel tras.
* Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) dla użytkownika zdefiniowanych tras (Udr).

