## <a name="network-security-group"></a>Grupy zabezpieczeń sieci
Zasób NSG umożliwia tworzenie hello granicy zabezpieczeń obciążeń, implementując zezwalania i odmowy reguły. Te zasady mogą być stosowane tooa maszyny Wirtualnej karty Sieciowej i podsieci.

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **podsieci** |Lista hello identyfikatorów podsieci grupa NSG jest stosowana do. |/Subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/TestRG/Providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd |
| **securityRules** |Lista reguł zabezpieczeń, które tworzą hello NSG |Zobacz [reguły zabezpieczeń](#Security-rule) poniżej |
| **defaultSecurityRules** |Lista domyślnych reguł zabezpieczeń w każdej grupy NSG |Zobacz [domyślne reguły zabezpieczeń](#Default-security-rules) poniżej |

* **Reguła zabezpieczeń** -grupa NSG może mieć zdefiniowano wiele reguł zabezpieczeń. Każda reguła może akceptować lub odrzucać różnego rodzaju ruchu.

### <a name="security-rule"></a>Reguły zabezpieczeń
Reguła zabezpieczeń jest zasobem podrzędne grupy NSG zawierający właściwości hello poniżej.

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **Opis elementu** |Opis reguły hello |Zezwalaj na ruch przychodzący dla wszystkich maszyn wirtualnych w podsieci X |
| **Protokół** |Protokół toomatch hello reguły |TCP, UDP lub * |
| **sourcePortRange** |Toomatch zakres portu źródłowego hello reguły |80, 100-200, * |
| **destinationPortRange** |Docelowy port zakresu toomatch hello reguły |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch prefiks adresu źródłowego dla reguły hello |10.10.10.1, 10.10.10.0/24, sieć wirtualną |
| **destinationAddressPrefix** |Toomatch prefiks adresu docelowego hello reguły |10.10.10.1, 10.10.10.0/24, sieć wirtualną |
| **Kierunek** |Kierunek ruchu toomatch hello reguły |ruch przychodzący lub wychodzący |
| **priorytet** |Priorytet reguły hello. Reguły są sprawdzane według ważności, gdy reguła ma zastosowanie, żadne inne reguły są sprawdzane pod kątem dopasowania. |10, 100, 65000 |
| **dostęp** |Typ tooapply dostęp, czy reguła hello |zezwolenie lub zablokowanie |

Przykład grupy NSG w formacie JSON:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Domyślne reguły zabezpieczeń

Reguły domyślne zabezpieczenia mają hello takie same właściwości dostępne w zasadach zabezpieczeń. Istnieją one tooprovide podstawowej łączności między zasoby, które mają toothem zastosować grupy NSG. Upewnij się, że wiesz, jakiego [domyślne reguły zabezpieczeń](../articles/virtual-network/virtual-networks-nsg.md#default-rules) istnieje.

### <a name="additional-resources"></a>Dodatkowe zasoby
* Uzyskaj więcej informacji [grup NSG](../articles/virtual-network/virtual-networks-nsg.md).
* Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) dla grup NSG.
* Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) dla reguł zabezpieczeń.
