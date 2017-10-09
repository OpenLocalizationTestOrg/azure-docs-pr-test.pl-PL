---
title: "aaaAzure sieci szkieletowej usług wstecznego bezpiecznej komunikacji serwera proxy | Dokumentacja firmy Microsoft"
description: Konfigurowanie komunikacji zabezpieczonej end-to-end tooenable zwrotnego serwera proxy.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Usługa bezpiecznego tooa Uzyskuj dostęp do hello zwrotnego serwera proxy

W tym artykule opisano, jak tooestablish bezpiecznego połączenia między hello zwrotnego serwera proxy i usług, umożliwiając w ten sposób zakończenia tooend bezpiecznego kanału.

Połączenie usług toosecure jest obsługiwana tylko wtedy, gdy zwrotnego serwera proxy skonfigurowanego toolisten HTTPS. Pozostałej części dokumentu hello przyjęto założenie, że w przypadku hello.
Odwołuje się zbyt[odwrotny serwer proxy w sieci szkieletowej usług Azure](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello zwrotnego serwera proxy w sieci szkieletowej usług.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Ustanawianie bezpiecznego połączenia między hello zwrotnego serwera proxy i usługami 

### <a name="reverse-proxy-authenticating-tooservices"></a>Odwrotny serwer proxy uwierzytelniania tooservices:
Hello zwrotny serwer proxy identyfikowany przy użyciu jego certyfikat określony tooservices ***reverseProxyCertificate*** właściwości w hello **klastra** [sekcji Typ zasobu](../azure-resource-manager/resource-group-authoring-templates.md). Usługi można zaimplementować hello logiki tooverify hello certyfikat przedstawiony przez zwrotny serwer proxy hello. Hello usługi można określić ustawienia konfiguracji w pakiecie konfiguracji hello szczegóły certyfikatu klienta hello akceptowane. Mogą być odczytywane w czasie wykonywania, a używane toovalidate hello certyfikat przedstawiony przez zwrotny serwer proxy hello. Odwołuje się zbyt[Zarządzanie parametry aplikacji](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello konfiguracji ustawień. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Odwrotny serwer proxy weryfikowania tożsamości usługi hello za pośrednictwem hello certyfikat przedstawiony przez usługę hello:
tooperform weryfikacji certyfikatu serwera certyfikatów hello przedstawianych przez usługi hello, zwrotny serwer proxy obsługuje jeden hello następujące opcje: None, ServiceCommonNameAndIssuer i ServiceCertificateThumbprints.
tooselect jedną z tych trzech opcji Określ hello **ApplicationCertificateValidationPolicy** w sekcji parametrów hello elementu bramy aplikacji/Http w obszarze [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Aby uzyskać szczegółowe informacje o dodatkowych konfiguracji dla każdego z tych opcji można znaleźć toohello następnej sekcji.

### <a name="service-certificate-validation-options"></a>Opcje sprawdzania poprawności certyfikatu usługi 

- **Brak**: zwrotny serwer proxy Pomija weryfikację certyfikatu usługi proxy hello i ustanawia hello bezpiecznego połączenia. Jest to zachowanie domyślne hello.
Określ hello **ApplicationCertificateValidationPolicy** z wartością **Brak** w sekcji parametrów hello elementu bramy aplikacji/Http.

- **ServiceCommonNameAndIssuer**: zwrotny serwer proxy sprawdza hello certyfikat przedstawiony przez usługę hello na podstawie nazwa pospolita certyfikatu i odcisk palca wystawcy natychmiastowego: Określ hello **ApplicationCertificateValidationPolicy**  z wartością **ServiceCommonNameAndIssuer** w sekcji parametrów hello elementu bramy aplikacji/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

Dodawanie listy hello toospecify wspólnej nazwy usługi oraz odciski palców wystawcy, **bramy aplikacji/Http/ServiceCommonNameAndIssuer** elementu w obszarze fabricSettings, jak pokazano poniżej. W elemencie tablicy parametrów hello można dodawać wiele par odcisk palca wystawcy i nazwa pospolita certyfikatu. 

Jeśli zwrotnego serwera proxy punktu końcowego hello jest połączenie toopresents certyfikatu, który jest wspólny nazwy i wystawców odcisk palca zgodny z dowolnym hello wartości określone w tym miejscu, kanału SSL. Po awarii toomatch hello szczegóły certyfikatu zwrotnego serwera proxy nie powiedzie się żądanie powitania klienta z kodem stanu 502 (zły bramy). Witaj wiersza stanu HTTP będzie również zawierać hello frazy "Nieprawidłowy certyfikat SSL." 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: zwrotny serwer proxy zweryfikuje hello serwerem proxy usługi certyfikatu opartego na jego odcisk palca. Można wybrać toogo tej trasy podczas hello usługi są skonfigurowane przy użyciu certyfikatów z podpisem własnym: Określ hello **ApplicationCertificateValidationPolicy** z wartością **ServiceCertificateThumbprints**w sekcji parametrów hello elementu bramy aplikacji/Http.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Również określić odciski palców hello z **ServiceCertificateThumbprints** wpis w sekcji parametrów elementu bramy aplikacji/Http. Można określić wiele odciski palców jako listę rozdzielaną przecinkami, w polu wartość hello, jak pokazano poniżej:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Jeśli hello odcisk palca certyfikatu serwera hello jest wyświetlana na tej pozycji konfiguracji, zwrotny serwer proxy zakończy się pomyślnie hello połączenia SSL. W przeciwnym razie zostaje zakończone hello połączenia i kończy się niepowodzeniem hello żądanie klienta z 502 (zły bramy). Witaj wiersza stanu HTTP będzie również zawierać hello frazy "Nieprawidłowy certyfikat SSL."

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Punkt końcowy zaznaczenia logiki podczas usług ekspozycji punktów końcowych, bezpieczne, jak również niezabezpieczona
Sieć szkieletowa usług obsługuje konfigurowanie wiele punktów końcowych dla usługi. Zobacz [Określanie zasobów w manifeście usługi](service-fabric-service-manifest-resources.md).

Zwrotny serwer proxy wybierze jeden z hello punkty końcowe tooforward hello żądania oparte na powitania **ListenerName** parametr zapytania. Jeśli nie zostanie określony, ją wybrać dowolnego punktu końcowego z listy punktów końcowych hello. Teraz, może to być punkt końcowy HTTP lub HTTPS. Mogą istnieć scenariusze/wymagania miejscu hello toooperate zwrotnego serwera proxy w "tylko tryb bezpieczny", tj nie ma punktów końcowych hello bezpiecznego zwrotnego serwera proxy tooforward żądań toounsecured. Można to osiągnąć, określając hello **SecureOnlyMode** pozycji konfiguracji z wartością **true** w sekcji parametrów hello elementu bramy aplikacji/Http.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> Podczas działania w **SecureOnlyMode**, jeśli określono klienta **ListenerName** odpowiadającego punktu końcowego HTTP(unsecured) tooan, zwrotnego serwera proxy nie powiedzie się Żądanie hello 404 kod stanu HTTP (nie znaleziono).

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Konfigurowanie uwierzytelniania certyfikatu klienta za pośrednictwem hello zwrotnego serwera proxy
Kończenie żądań SSL odbywa się na powitania zwrotnego serwera proxy i wszystkie powitania klienta certyfikatu dane zostaną utracone. Uwierzytelnianie certyfikatu hello usług tooperform klienta, ustaw hello **ForwardClientCertificate** ustawienia w sekcji parametrów hello elementu bramy aplikacji/Http.

1. Gdy **ForwardClientCertificate** ustawiono zbyt**false**, odwrócić serwera proxy nie będą wymagane dla certyfikatu klienta hello podczas jego uzgadniania protokołu SSL z powitania klienta.
Jest to zachowanie domyślne hello.

2. Gdy **ForwardClientCertificate** ustawiono zbyt**true**, żądań serwera proxy dla certyfikatu klienta hello wstecznego podczas jego uzgadniania protokołu SSL z powitania klienta.
Następnie prześle je powitania klienta danych certyfikatu w niestandardowy nagłówek HTTP o nazwie **certyfikat klienta X**. wartość nagłówka Hello jest ciąg formatu PEM hello kodowanie base64 certyfikatu powitania klienta. usługi Hello można powiodło się/niepowodzenie hello żądania z kodem stanu odpowiednie po sprawdzeniu danych certyfikatu hello.
Jeżeli powitania klienta nie przedstawić certyfikat, zwrotny serwer proxy przekazuje pusty nagłówek i powiadom hello usługi dojścia hello case.

> Zwrotny serwer proxy jest tylko usługa przesyłania dalej. Nie będzie wykonywać żadnych weryfikacji certyfikatu powitania klienta.


## <a name="next-steps"></a>Następne kroki
* Odwołuje się zbyt[Konfigurowanie usług toosecure tooconnect zwrotnego serwera proxy](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) dla usługi Azure Resource Manager szablonu przykłady tooconfigure bezpiecznego zwrotny serwer proxy przy użyciu opcji weryfikacji certyfikatu hello w innej usługi.
* Zobacz przykład protokołu HTTP do komunikacji między usługami w [przykładowy projekt w witrynie GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Zdalne wywołania procedur z usług zdalnych niezawodne usługi](service-fabric-reliable-services-communication-remoting.md)
* [Interfejs API, który używa OWIN w niezawodnej usługi sieci Web](service-fabric-reliable-services-communication-webapi.md)
* [Zarządzanie certyfikatami klastra](service-fabric-cluster-security-update-certs-azure.md)
