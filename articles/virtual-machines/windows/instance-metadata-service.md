---
title: "aaaAzure wystąpienia metadane usługi dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Interfejs rESTful tooget informacje o obliczeniowych, sieci i zdarzeń planowanych konserwacji systemu Windows maszyny Wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a>Usługa Azure wystąpienie metadanych dla maszyn wirtualnych systemu Windows


Hello Azure wystąpienie metadanych usługi dostarcza informacji o uruchomionych wystąpień maszyn wirtualnych, które można toomanage używane i skonfigurować maszyny wirtualne.
Dotyczy to również informacje, takie jak jednostka SKU, konfiguracji sieci i zdarzeń planowanych konserwacji. Aby uzyskać więcej informacji na jakie rodzaje informacji jest dostępnych w temacie [kategorie metadanych](#instance-metadata-data-categories).

Usługa metadanych wystąpienia platformy Azure jest punkt końcowy REST tooall dostępne maszyny wirtualne IaaS utworzony za pośrednictwem hello [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). punkt końcowy Hello jest dostępny w dobrze znanego adresu IP bez obsługi routingu (`169.254.169.254`) który jest możliwy tylko z wewnątrz hello maszyny Wirtualnej.



> [!IMPORTANT]
> Ta usługa jest **ogólnie dostępna** w globalnej regiony platformy Azure. Znajduje się w publicznej wersji zapoznawczej dla instytucji rządowych, Chin i chmury Azure niemiecki. Regularnie odbiera aktualizacje tooexpose nowe informacje o wystąpieniu maszyny wirtualnej. Ta strona odzwierciedla hello aktualne [kategorii danych](#instance-metadata-data-categories) dostępne.



## <a name="service-availability"></a>Dostępność usługi
Usługa Hello jest dostępna we wszystkich regionach globalne Azure ogólnie dostępna. Usługa Hello znajduje się w publicznej wersji zapoznawczej w regionach dla instytucji rządowych, Chiny lub Niemcy hello.

Regiony                                        | Dostępność?
-----------------------------------------------|-----------------------------------------------
[Wszystkie ogólnie dostępna globalne regiony platformy Azure](https://azure.microsoft.com/regions/)     | Ogólnie dostępna 
[Azure dla instytucji rządowych](https://azure.microsoft.com/overview/clouds/government/)              | W wersji zapoznawczej 
[Chin Azure](https://www.azure.cn/)                                                           | W wersji zapoznawczej
[Niemcy Azure](https://azure.microsoft.com/overview/clouds/germany/)                    | W wersji zapoznawczej

Ta tabela jest aktualizowany, gdy usługa hello staje się dostępna w innych chmur Azure.

tootry limit hello wystąpienia usługi metadanych, utwórz maszynę Wirtualną z [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) lub hello [portalu Azure](http://portal.azure.com) w hello powyżej regiony i wykonaj hello przykłady poniżej.

## <a name="usage"></a>Sposób użycia

### <a name="versioning"></a>Przechowywanie wersji
Witaj wystąpienia usługi metadanych jest kontrolą wersji. Wersje są obowiązkowe i hello bieżąca wersja to `2017-04-02`.

> [!NOTE] 
> Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api hello. Ten format jest już obsługiwane i zostaną wycofane w przyszłości hello.

Przy wdrażaniu nowsze wersje, starsze wersje nadal będą dostępne dla zgodności czy skrypty są zależne formatów określonych danych. Jednak należy pamiętać, że bieżący version(2017-03-01) podglądu tego hello mogą nie być dostępne po usługi hello jest ogólnie dostępna.

### <a name="using-headers"></a>Korzystanie z nagłówków
Zapytania hello wystąpienia usługi metadanych, należy określić nagłówek hello `Metadata: true` tooensure hello żądania nie został przypadkowo przekierowany.

### <a name="retrieving-metadata"></a>Pobieranie metadanych

Wystąpienie metadanych jest dostępna do uruchamiania maszyny wirtualne utworzone/zarządzane przy użyciu [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Dostęp do wszystkich kategorii danych dla wystąpienia maszyny wirtualnej przy użyciu hello następujące żądania:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Wszystkie wystąpienia zapytania metadanych jest rozróżniana wielkość liter.

### <a name="data-output"></a>Dane wyjściowe
Domyślnie program hello wystąpienia usługi metadanych zwraca dane w formacie JSON (`Content-Type: application/json`). Jednak różnych interfejsów API może zwracać dane w różnych formatach, jeśli jest to wymagane.
Witaj poniższej tabeli jest odwołaniem innych formatów danych, który może obsługiwać interfejsy API.

Interfejs API | Domyślny Format danych | W innych formatach
--------|---------------------|--------------
/instance | JSON | Tekst
/scheduledevents | JSON | Brak

tooaccess format odpowiedzi z systemem innym niż domyślny, określ żądany format hello jako parametr querystring w żądaniu hello. Na przykład:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Bezpieczeństwo
punkt końcowy usługi metadanych wystąpienia Hello jest dostępny tylko w obrębie hello uruchomione wystąpienie maszyny wirtualnej bez obsługi routingu adresu IP. Ponadto wszelkie żądania z `X-Forwarded-For` nagłówek został odrzucony przez usługę hello.
Wymagamy toocontain żądań `Metadata: true` tooensure nagłówek, który hello rzeczywistego żądania bezpośrednio był zamierzony i nie jest częścią niezamierzonych przekierowania. 

### <a name="error"></a>Błąd
Jeśli istnieje element danych nie można odnaleźć lub źle sformułowane żądanie, hello wystąpienia usługi metadanych zwraca standardowe komunikaty o błędach HTTP. Na przykład:

Kod stanu HTTP | Przyczyna
----------------|-------
200 OK |
400 Niewłaściwe żądanie | Brak `Metadata: true` nagłówka
404 — Nie odnaleziono | Witaj does't żądany element istnieje 
405 — metoda nie jest dozwolone | Tylko `GET` i `POST` żądania są obsługiwane.
429 zbyt wiele żądań | Interfejs API Hello obecnie obsługuje maksymalnie 5 zapytania na sekundę
Błąd usługi 500     | Spróbuj ponownie za jakiś czas

### <a name="examples"></a>Przykłady

> [!NOTE] 
> Wszystkie odpowiedzi interfejsu API są ciągami formatu JSON. Wszystkie odpowiedzi na przykład następujące są drukowane pretty dla czytelności.

#### <a name="retrieving-network-information"></a>Trwa pobieranie informacji o sieci

**Żądanie**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Odpowiedź**

> [!NOTE] 
> odpowiedź Hello jest ciągu JSON. powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Trwa pobieranie publicznego adresu IP

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Pobieranie wszystkich metadanych dla wystąpienia

**Żądanie**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Odpowiedź**

> [!NOTE] 
> odpowiedź Hello jest ciągu JSON. powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Pobieranie metadanych maszyny wirtualnej systemu Windows

**Żądanie**

W systemie Windows można pobrać wystąpienia metadanych za pośrednictwem hello programu PowerShell narzędzia `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Lub za pośrednictwem hello `Invoke-RestMethod` polecenia cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Odpowiedź**

> [!NOTE] 
> odpowiedź Hello jest ciągu JSON. powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Kategorie danych metadanych wystąpienia
Witaj następujące kategorie danych są dostępne za pośrednictwem hello wystąpienia usługi metadanych:

Dane | Opis
-----|------------
location | Witaj regionu Azure wirtualna jest uruchomiona
name | Nazwa hello maszyny Wirtualnej 
Oferta | Zapewniają informacje o hello obrazu maszyny Wirtualnej. Ta wartość ma tylko obrazy wdrożone z galerii Azure obrazu.
Wydawcy | Wydawca hello obrazu maszyny Wirtualnej
Jednostka SKU | Określonej jednostki SKU dla obrazu maszyny Wirtualnej hello  
Wersja | Wersja obrazu maszyny Wirtualnej hello 
osType | Linux lub Windows 
platformUpdateDomain |  [Domeny aktualizacji](manage-availability.md) hello wirtualna jest uruchomiona w
platformFaultDomain | [Domena błędów](manage-availability.md) hello wirtualna jest uruchomiona w
vmId | [Unikatowy identyfikator](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) dla hello maszyny Wirtualnej
vmSize | [Rozmiar maszyny Wirtualnej](sizes.md)
IPv4/elementu privateIpAddress | Lokalny adres IPv4 hello maszyny Wirtualnej 
IPv4/publicznego adresu IP | Publiczny adres IPv4 hello maszyny Wirtualnej
podsieć lub adres. | Adres podsieci hello maszyny Wirtualnej
prefiks podsieci / | Prefiks podsieci, przykład 24
adres IPv6/IP | Lokalny adres IPv6 hello maszyny Wirtualnej
MacAddress | Adres mac dla maszyny Wirtualnej 
scheduledevents | Obecnie w publicznej wersji zapoznawczej zobacz [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Przykładowe scenariusze użycia  

### <a name="tracking-vm-running-on-azure"></a>Śledzenie maszyn wirtualnych działających na platformie Azure

Jako dostawcę usług mogą wymagać tootrack hello liczbę maszyn wirtualnych z oprogramowaniem lub agentami, którzy muszą tootrack unikatowość hello maszyny Wirtualnej. toobe stanie tooget Unikatowy identyfikator dla maszyny Wirtualnej, użyj hello `vmId` pola wystąpienia metadanych usługi.

**Żądanie**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Odpowiedź**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Umieszczania kontenery, partycje danych na podstawie domen błędów lub zaktualizowania 

Dla niektórych scenariuszy, umieszczania repliki danych różnych znaczenie ma. Na przykład [umieszczania repliki systemu plików HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) lub położenia kontenera za pomocą [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) może wymagać tooknow hello `platformFaultDomain` i `platformUpdateDomain` hello maszyna wirtualna jest uruchomiona na.
Umożliwia wysyłanie zapytań tych danych bezpośrednio za pomocą hello wystąpienie metadanych usługi.

**Żądanie**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Odpowiedź**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Więcej informacji na temat hello maszyny Wirtualnej podczas do sprawę pomocy technicznej 

Jako dostawcę usług mogą wystąpić pomocy technicznej miejsce chcesz tooknow więcej informacji na temat hello maszyny Wirtualnej. Pytania powitania klienta tooshare hello obliczeń metadane zapewniają podstawowe informacje dotyczące hello pomocy technicznej professional tooknow o rodzaju hello maszyny wirtualnej na platformie Azure. 

**Żądanie**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Odpowiedź**

> [!NOTE] 
> odpowiedź Hello jest ciągu JSON. powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Przykłady wywoływania usługi metadanych przy użyciu różnych języków wewnątrz hello maszyny Wirtualnej 

Język | Przykład 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.RB
Przejdź do sieci Lan   | https://github.com/Microsoft/azureimds/blob/Master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.PY
C++      | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample-Windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.CS
Javascript | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.sh
    

## <a name="faq"></a>Często zadawane pytania
1. Pojawia się błąd hello `400 Bad Request, Required metadata header not specified`. Co to znaczy?
   * Hello usługi metadanych wystąpienia wymaga nagłówka hello `Metadata: true` toobe przekazano hello żądania. Przekazywanie tego nagłówka w wywołaniu REST hello umożliwia dostęp toohello wystąpienie metadanych usługi. 
2. Dlaczego nie występują obliczeniowe informacji Moje maszyny wirtualnej?
   * Obecnie hello wystąpienie metadanych usługi obsługuje tylko wystąpienia utworzone za pomocą Menedżera zasobów Azure. W przyszłości hello może dodać obsługę maszyn wirtualnych usługi w chmurze.
3. Napisany wcześniej utworzony Moje maszyny wirtualnej za pomocą usługi Azure Resource Manager. Dlaczego mam nie zawiera compute metadane?
   * Wszystkie maszyny wirtualne utworzone po wrz 2016, można dodać [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart oglądanie obliczeń metadanych. Dla starszych maszyn wirtualnych (utworzone przed 2016 wrz) Dodaj/Usuń rozszerzenia lub danych dysków toohello wirtualna toorefresh metadanych.
4. Dlaczego otrzymuję błąd hello `500 Internal Server Error`?
   * Ponów żądanie w oparciu wykładniczego wycofywania systemu. Jeśli hello problem będzie się powtarzał skontaktuj się z pomocą techniczną platformy Azure.
5. Gdzie udostępniać dodatkowe pytania/komentarze?
   * Wyślij komentarze dotyczące http://feedback.azure.com.
7. Czy to pomoże dla wystąpienia ustawić skali maszyny wirtualnej?
   * Tak, usługa metadanych jest dostępna dla wystąpień ustawić skali. 
6. Jak uzyskać pomoc techniczną dla usługi hello?
   * tooget obsługę usługi hello Utwórz problem pomocy technicznej w portalu Azure, aby hello maszyny Wirtualnej, jeśli nie jesteś odpowiedzi metadanych stanie tooget mimo ponownych prób długa 

   ![Obsługa metadanych wystąpienia](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o hello [zaplanowane zdarzenia](scheduled-events.md) interfejsu API **w publicznej wersji zapoznawczej** podał hello metadanych wystąpienia usługi.
