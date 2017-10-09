## <a name="public-ip-address"></a>Publiczny adres IP
Zasób publicznego adresu IP zawiera albo zastrzeżonego lub dynamiczny internetowy adres IP. Mimo że można utworzyć publiczny adres IP, jako autonomiczny obiekt, należy tooassociate go tooactually obiektu tooanother Użyj adresu hello. Można skojarzyć publicznego równoważenia obciążenia tooa adres IP, brama aplikacji lub kart tooprovide dostępu toothose zasobów w Internecie.  

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **publicIPAllocationMethod** |Określa, czy adres IP hello jest *statycznych* lub *dynamiczne*. |statyczna, dynamiczne |
| **idleTimeoutInMinutes** |Definiuje hello bezczynności limit czasu, wartość domyślna wynosi 4 minut. Jeśli w tej chwili nie zostanie odebrana nie więcej pakietów dla danej sesji, sesja hello jest zakończona. |dowolna wartość od 4 do 30 |
| **adres IP** |Tooobject przypisany adres IP. Jest to właściwość tylko do odczytu. |104.42.233.77 |

### <a name="dns-settings"></a>Ustawienia DNS
Publiczne adresy IP mieć obiektu podrzędnego o nazwie **dnsSettings** zawierający hello następujące właściwości:

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **domainNameLabel** |Hosta o nazwie używany do rozpoznawania nazw. |WWW, ftp, vm1 |
| **Nazwa FQDN** |Pełna nazwa hello publicznego adresu IP. |www.westus.cloudapp.Azure.com |
| **reverseFqdn** |Nazwy FQDN, który jest rozpoznawany jako adres IP toohello i jest zarejestrowana w systemie DNS jako rekord PTR. |www.contoso.com. |

Przykładowe publicznego adresu IP w formacie JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Dodatkowe zasoby
* Uzyskaj więcej informacji [publiczne adresy IP](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Dowiedz się więcej o [wystąpienie poziomu publiczne adresy IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) publicznego adresu IP adresów.

