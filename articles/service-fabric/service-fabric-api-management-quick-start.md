---
title: "aaaAzure sieci szkieletowej usług z interfejsu API zarządzania szybki start | Dokumentacja firmy Microsoft"
description: "Ten przewodnik przedstawia, jak tooquickly wprowadzenie do usługi Azure API Management i sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Sieć szkieletowa usług z usługi Azure API Management Szybki Start

W tym przewodniku przedstawiono jak tooset Konfigurowanie usługi Azure API Management z sieci szkieletowej usług i skonfigurować pierwszy interfejsu API operacji toosend ruchu tooback-end usług w sieci szkieletowej usług. toolearn więcej informacji na temat usługi Azure API Management scenariuszy z sieci szkieletowej usług, zobacz hello [omówienie](service-fabric-api-management-overview.md) artykułu. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Wdrażanie tooAzure API Management i sieci szkieletowej usług

Witaj pierwszym krokiem jest toodeploy API Management i tooAzure klastra sieci szkieletowej usług w udostępnionym sieci wirtualnej. Dzięki temu zarządzanie interfejsami API toocommunicate bezpośrednio z usługi Service Fabric, który może wykonywać odnajdywania usługi, rozdzielczość partycji usługi i przekazywać ruch bezpośrednio tooany wewnętrznej bazy danych usługi w sieci szkieletowej usług.

### <a name="topology"></a>Topologia

Ten przewodnik wdrażania następujących hello tooAzure topologii, w którym interfejs API zarządzania i sieci szkieletowej usług znajdują się w podsieci hello tej samej sieci wirtualnej:

 ![Podpis obrazu][sf-apim-topology-overview]

tooget szybko rozpocząć pracę, szablony usługi Resource Manager są dostępne dla każdego kroku wdrożenia:

 - Topologia sieci:
    - [Network.JSON][network-arm]
    - [Network.parameters.JSON][network-parameters-arm]
 - Klaster sieci szkieletowej usług:
    - [cluster.JSON][cluster-arm]
    - [cluster.parameters.JSON][cluster-parameters-arm]
 - Zarządzanie interfejsami API:
    - [APIM.JSON][apim-arm]
    - [APIM.parameters.JSON][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Zaloguj się tooAzure i wybierz subskrypcję

Ten przewodnik po używa [programu Azure PowerShell][azure-powershell]. Po ponownym uruchomieniu nowej sesji programu PowerShell, zaloguj się tooyour konto platformy Azure i wybierz subskrypcję, przed wykonaniem polecenia platformy Azure.
 
Zaloguj się tooyour konto platformy Azure:

```powershell
PS > Login-AzureRmAccount
```

Wybierz subskrypcję:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz nową grupę zasobów dla danego wdrożenia. Nadaj nazwę i lokalizację.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Wdrażanie hello topologii sieci

Hello pierwszym krokiem jest tooset się toowhich topologii sieci hello interfejsu API zarządzania i zostanie wdrożony hello klastra sieci szkieletowej usług. Witaj [network.json] [ network-arm] szablonu usługi Resource Manager jest skonfigurowany toocreate wirtualnych sieci (sieć Wirtualną) z dwoma podsieciami i dwie grupy zabezpieczeń sieci (NSG). 

Witaj [network.parameters.json] [ network-parameters-arm] plik parametrów zawiera nazwy hello hello podsieci i grup NSG, które interfejs API zarządzania i sieci szkieletowej usług zostaną wdrożone do. Ten przewodnik wartości parametrów hello nie ma potrzeby toobe zmienione. Szablony API Management i Menedżer zasobów sieci szkieletowej usług Hello użyć tych wartości, jeśli zostaną zmodyfikowane w tym miejscu, należy zmodyfikować je w związku z tym hello innych szablonów usługi Resource Manager. 

 1. Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:

    - [Network.JSON][network-arm]
    - [Network.parameters.JSON][network-parameters-arm]

 2. Użyj hello następujące PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki instalacji sieciowej hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Wdrażanie klastra usługi sieć szkieletowa hello

Po zasobów sieciowych hello zostało ukończone, wdrażanie, hello następnym krokiem jest toodeploy toohello klastra sieci szkieletowej usług sieci Wirtualnej w podsieci hello i NSG przeznaczone dla klastra usługi sieć szkieletowa hello. W tym samouczku nazw hello toouse wstępnie skonfigurowane hello sieci Wirtualnej, podsieci i NSG, skonfigurowanym w poprzednim kroku hello jest hello szablon Menedżera zasobów sieci szkieletowej usług. 

Szablon usługi Resource Manager klastra usługi sieć szkieletowa Hello jest skonfigurowany toocreate bezpiecznego klastra z certyfikatu zabezpieczeń. certyfikat Hello jest komunikacji między węzłami toosecure używane dla klastra i klaster sieci szkieletowej usług tooyour toomanage użytkownika dostępu. Zarządzanie interfejsami API używa tego certyfikatu tooaccess hello Usługa nazewnictwa sieci szkieletowej dla potrzeb odnajdywania usług.

Ten krok wymaga mające certyfikat w magazynie kluczy dla zabezpieczeń klastra. Aby uzyskać więcej informacji na temat konfigurowania bezpiecznej klastra z Key Vault, zobacz [ten przewodnik na temat tworzenia klastra na platformie Azure przy użyciu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md)

> [!NOTE]
> Można dodać uwierzytelniania usługi Azure Active Directory w dodanie toohello certyfikatu używanego na potrzeby dostępu do klastra. Azure Active Directory jest hello zalecane klastra sieci szkieletowej usług tooyour dostępu sposób toomanage użytkownika, ale jest toocomplete nie jest konieczna w tym samouczku. Certyfikat jest wymagany niezależnie od sposobu zabezpieczenia węzła do węzła klastra, a do uwierzytelniania usługi Azure API Management, który obecnie nie obsługuje uwierzytelniania w usłudze Azure Active Directory dla usługi Service Fabric w wewnętrznej bazie danych.

 1. Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:
 
    - [cluster.JSON][cluster-arm]
    - [cluster.parameters.JSON][cluster-parameters-arm]

 2. Wypełnij puste parametry hello w hello `cluster.parameters.json` plików dla danego wdrożenia, w tym hello [informacje magazynie klucza](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) dla certyfikatu klastra.

 3. Użyj hello następującego środowiska PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki toocreate hello klastra sieci szkieletowej usług:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Wdrażanie usługi API Management

Ponadto należy wdrożyć toohello interfejsu API zarządzania sieciami Wirtualnymi w podsieci hello i NSG przeznaczone dla interfejsu API zarządzania. Nie trzeba toowait dla toofinish wdrażania klastra usługi sieć szkieletowa hello przed wdrożeniem usługi API Management. 

W tym samouczku nazw hello toouse wstępnie skonfigurowane hello sieci Wirtualnej, podsieci i NSG, skonfigurowanym w poprzednim kroku hello jest hello szablonu interfejsu API zarządzania Resource Manager. 

 1. Pobierz hello następującego pliku szablonu i parametry Menedżera zasobów:
 
    - [APIM.JSON][apim-arm]
    - [APIM.parameters.JSON][apim-parameters-arm]

 2. Wypełnij puste parametry hello w hello `apim.parameters.json` dla danego wdrożenia.

 3. Użyj hello następujące PowerShell polecenie toodeploy hello Menedżera zasobów szablonu i parametr pliki dla interfejsu API zarządzania:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Skonfiguruj zarządzanie interfejsami API

Po są wdrażane w klastrze API Management i sieci szkieletowej usług, można skonfigurować sieci szkieletowej usług w wewnętrznej bazie danych w usłudze API Management. Dzięki temu toocreate zasadę usługi wewnętrznej bazy danych, która wysyła klastra sieci szkieletowej usług tooyour ruchu.

### <a name="api-management-security"></a>Zabezpieczenia Management API

tooconfigure hello sieci szkieletowej usług wewnętrznej bazy danych, należy najpierw ustawienia zabezpieczeń interfejsu API zarządzania tooconfigure. ustawienia zabezpieczeń tooconfigure, przejdź tooyour interfejsu API usługi zarządzania w hello portalu Azure.

#### <a name="enable-hello-api-management-rest-api"></a>Włącz hello interfejsu API REST zarządzania interfejsu API

Witaj interfejsu API REST zarządzania interfejsu API jest obecnie hello tylko sposób tooconfigure usługi wewnętrznej bazy danych. pierwszym krokiem Hello jest hello tooenable interfejsu API REST zarządzania interfejsu API i zabezpieczyć.

 1. Hello usługi API Management, wybierz **API Management — wersja ZAPOZNAWCZA** w obszarze **zabezpieczeń**.
 2. Sprawdź hello **Włącz interfejs API zarządzania interfejsu API REST** wyboru.
 3. Uwaga hello adres URL interfejsu API zarządzania — to jest adres URL hello użyjemy nowsze tooset się hello sieci szkieletowej usług zaplecza
 4. Generuj **tokenu dostępu** wybierając datę wygaśnięcia oraz klucz, następnie kliknij przycisk hello **Generuj** przycisku w kierunku hello u dołu strony hello.
 5. Kopiuj hello **token dostępu** i zapisać go — użyjemy w hello następujące kroki. Należy zauważyć, że ta różni się od hello klucza podstawowego i pomocniczego klucza.

#### <a name="upload-a-service-fabric-client-certificate"></a>Przekaż certyfikat klienta sieci szkieletowej usług

Zarządzanie interfejsami API musi uwierzytelniać się z klastrem usługi sieć szkieletowa usług dla potrzeb odnajdywania usług za pomocą certyfikatu klienta, który ma dostęp tooyour klastra. Dla uproszczenia ten samouczek używa hello sam certyfikat określony podczas tworzenia klastra usługi sieć szkieletowa hello, które domyślnie mogą być używane tooaccess klastra.

 1. Hello usługi API Management, wybierz **certyfikatów klienta — w wersji ZAPOZNAWCZEJ** w obszarze **zabezpieczeń**.
 2. Kliknij przycisk hello **+ Dodaj** przycisku
 2. Wybierz hello pliku klucza prywatnego (pfx) hello klastra certyfikatu, który określone podczas tworzenia klastra usługi sieć szkieletowa, nadaj mu nazwę, a następnie podaj hasło klucza prywatnego hello.

> [!NOTE]
> Ten samouczek używa hello sam certyfikat bezpieczeństwa węzła do węzła klienta uwierzytelniania i klastra. Certyfikat klienta w osobnym można używać, jeśli masz jeden tooaccess skonfigurowany klaster sieci szkieletowej usług.

### <a name="configure-hello-backend"></a>Skonfiguruj hello wewnętrznej bazy danych

Teraz, gdy zabezpieczeń interfejsu API zarządzania jest skonfigurowany, można skonfigurować hello sieci szkieletowej usług zaplecza. W przypadku zapleczy sieci szkieletowej usług klastra sieci szkieletowej usług hello jest hello wewnętrznej bazy danych, a nie dla określonej usługi sieć szkieletowa usług. Dzięki temu toomore tooroute w ramach jednych zasad, niż jedna usługa hello klastra.

Ten krok wymaga tokenu dostępu hello wcześniej wygenerowania i hello odcisk palca dla certyfikatu klastra się, że przekazano tooAPI zarządzania hello poprzedniego kroku.

> [!NOTE]
> Jeśli używasz certyfikatu klienta w osobnym w poprzednim kroku powitania dla interfejsu API zarządzania należy hello odcisk palca dla certyfikatu klienta hello w dodanie toohello klastra odcisk palca certyfikatu w tym kroku.

Wyślij powitania po toohello żądanie HTTP PUT URL interfejsu API zarządzania interfejsu API zanotowaną wcześniej podczas włączania usługi wewnętrznej bazy danych usługi Service Fabric hello tooconfigure hello interfejsu API REST zarządzania interfejsu API. Powinny pojawić się `HTTP 201 Created` odpowiedzi, gdy polecenia hello zakończy się pomyślnie. Aby uzyskać więcej informacji na każde pole, zobacz hello zarządzanie interfejsami API [dokumentacji zaplecza interfejsu API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Polecenia HTTP i adres URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Nagłówki żądania:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Treść żądania:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Witaj **adres url** parametru w tym miejscu jest usługi w pełni kwalifikowaną nazwę usługi w klastrze, które są wszystkie żądania kierowane tooby domyślne, jeśli nazwa usługi, nie jest określona w zasadzie wewnętrznej bazy danych. Może używać nazw fałszywych usług, takich jak "fabric: fałszywych/service" Jeśli nie chcesz, aby toohave usługę rezerwowy.

Zobacz toohello zarządzanie interfejsami API [interfejs API zaplecza dokumentacji](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) uzyskać więcej informacji dotyczących każdego pola.

#### <a name="example"></a>Przykład

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Wdrażanie usługi zaplecza sieci szkieletowej usług

Teraz, gdy masz powitalne sieci szkieletowej usług skonfigurowany jako tooAPI wewnętrznej bazy danych zarządzania można tworzyć zasady wewnętrznej bazy danych dla interfejsów API, które przesyłają tooyour usługi sieć szkieletowa usług. Ale najpierw należy w usłudze działającej w żądaniach tooaccept sieci szkieletowej usług.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Tworzenie usługi sieć szkieletowa usług za pomocą punktu końcowego HTTP

W tym samouczku utworzymy podstawowe bezstanowej platformy ASP.NET Core niezawodnej usługi za pomocą hello domyślny szablon projektu interfejsu API sieci Web. Spowoduje to utworzenie punktu końcowego HTTP dla usługi, która będzie udostępnić za pośrednictwem usługi Azure API Management:

```
/api/values
```

Rozpocznij od [Konfigurowanie środowiska programowania do tworzenia aplikacji platformy ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Po skonfigurowaniu środowiska projektowego, uruchom program Visual Studio jako Administrator i Utwórz usługę platformy ASP.NET Core:

 1. W programie Visual Studio wybierz Plik -> Nowy projekt.
 2. Wybierz hello szablonu aplikacji sieci szkieletowej usług w chmurze i nadaj mu nazwę **"ApiApplication"**.
 3. Wybierz hello platformy ASP.NET Core szablonu usługi i nazwę projektu hello **"WebApiService"**.
 4. Wybierz szablon projektu hello Web API platformy ASP.NET Core 1.1.
 5. Po utworzeniu projektu hello Otwórz `PackageRoot\ServiceManifest.xml` i Usuń hello `Port` atrybut z konfiguracji zasobu punktu końcowego hello:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Dzięki temu usługi sieć szkieletowa toospecify port dynamicznie z zakresu portów aplikacji hello, którego możemy otworzyć za pomocą hello sieciowej grupy zabezpieczeń w szablonie usługi Resource Manager klastra hello, dzięki czemu ruch tooflow tooit z interfejsu API zarządzania.
 
 6. Naciśnij klawisz F5 w programie Visual Studio tooverify hello interfejsu API sieci web jest dostępna lokalnie. 

    Otwórz Eksploratora usługi sieć szkieletowa i przechodzenie do szczegółów tooa konkretne wystąpienie hello platformy ASP.NET Core toosee hello adres podstawowy hello usługa nasłuchuje. Dodaj `/api/values` toohello adresem podstawowym i otwórz go w przeglądarce. Wywołuje to hello metody Get na powitania ValuesController hello szablonu interfejsu API sieci Web. Zwraca odpowiedź domyślna hello dostarczone przez szablon hello, tablicy JSON, który zawiera dwa ciągi:

    ```json
    ["value1", "value2"]`
    ```

    To jest punkt końcowy hello, który będzie udostępnić za pośrednictwem interfejsu API zarządzania na platformie Azure.

 7. Ponadto wdrożyć klaster tooyour aplikacji hello na platformie Azure. [Za pomocą programu Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), kliknij prawym przyciskiem myszy projekt aplikacji hello i wybierz **publikowania**. Podaj punkt końcowy klastra (na przykład `mycluster.westus.cloudapp.azure.com:19000`) tooyour aplikacji hello toodeploy sieci szkieletowej usług klastra na platformie Azure.

Usługi bezstanowej platformy ASP.NET Core o nazwie `fabric:/ApiApplication/WebApiService` teraz powinna być uruchomiona w klastrze usługi sieć szkieletowa na platformie Azure.

## <a name="create-an-api-operation"></a>Tworzenie operacji interfejsu API

Teraz jest gotowy toocreate operacji w usłudze API Management tego toocommunicate używany przez klientów zewnętrznych z hello uruchamiania w klastrze usługi sieć szkieletowa hello usługi bezstanowej platformy ASP.NET Core.

 1. Zaloguj się za toohello portalu Azure i przejdź do wdrożenia usługi Zarządzanie interfejsami API tooyour.
 2. W bloku usługi Zarządzanie interfejsami API hello, wybierz **interfejsów API — wersja zapoznawcza**
 3. Dodaj nowy interfejs API, klikając hello **puste API** pole i wypełniania okno dialogowe hello:

     - **Adres URL usługi sieci Web**: dla sieci szkieletowej usług zapleczy, ta wartość adresu URL nie jest używany. Tutaj możesz umieścić żadnej wartości. W tym samouczku, użyj: `http://servicefabric`.
     - **Nazwa**: Podaj dowolną nazwę interfejsu API. W tym samouczku, użyj `Service Fabric App`.
     - **Schemat adresu URL**: Wybierz HTTP, HTTPS lub obu. W tym samouczku, użyj `both`.
     - **Sufiks adresu URL interfejsu API**: Podaj sufiks na interfejsie API. W tym samouczku, użyj `myapp`.
 
 4. Po utworzeniu hello interfejsu API, kliknij przycisk **+ Dodaj operację** operacji tooadd frontonu interfejsu API. Wypełnianie hello wartości:
    
     - **Adres URL**: Wybierz `GET` i podaj ścieżkę adresu URL dla hello interfejsu API. W tym samouczku, użyj `/api/values`.
     
       Domyślnie program hello ścieżki adresu URL określone w tym miejscu są wysyłane hello ścieżki adresu URL usługi sieci szkieletowej usług zaplecza toohello. Jeśli używasz hello tej samej ścieżki adresu URL w tym miejscu używanego z usługą, w tym przypadku `/api/values`, następnie hello działa bez dalszej modyfikacji. Może również określić ścieżki adresu URL w tym miejscu, który różni się od ścieżki adresu URL hello korzystali z wewnętrzną bazą danych usługi Service Fabric, w którym to przypadku będą również toospecify należy ścieżką przepisywania w zasadach operację później.
     - **Nazwa wyświetlana**: Podaj nazwę dowolnego hello interfejsu API. W tym samouczku, użyj `Values`.

## <a name="configure-a-backend-policy"></a>Skonfiguruj zasady wewnętrznej bazy danych

zasady zaplecza Hello wiąże co wszystko. Jest to, gdzie skonfigurować hello wewnętrznej bazy danych są kierowane żądania toowhich usługi sieć szkieletowa usług. Można zastosować operacji interfejsu API tooany tej zasady. Witaj [wewnętrznej bazy danych konfiguracji sieci szkieletowej usług](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) zapewnia następujące hello żądania routingu formantów: 
 - Usługa Wybór wystąpienia, określając nazwę wystąpienia usługi Service Fabric, albo zapisane na stałe (na przykład `"fabric:/myapp/myservice"`) lub generowane na podstawie żądania hello HTTP (na przykład `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Rozdzielczość partycji przez generowanie klucza partycji przy użyciu dowolnego schemat partycjonowania sieci szkieletowej usług.
 - Wybór repliki dla stanowych usług.
 - Rozdzielczość ponów warunki, które należy spełnić warunki hello toospecify ponowne rozpoznanie lokalizację usługi i wysłać żądanie.

W tym samouczku Utwórz zasadę wewnętrznej bazy danych trasy żądań bezpośrednio toohello platformy ASP.NET Core usługi bezstanowej wdrożonej wcześniej:

 1. Wybierz i edytować hello **przychodzących zasad** dla hello `Values` operacji, klikając ikonę edycji hello, a następnie wybierając **widoku kodu**.
 2. W edytorze kodu hello zasad, Dodaj `set-backend-service` zasad w obszarze zasady ruchu przychodzącego, jak pokazano poniżej i kliknij przycisk hello **zapisać** przycisk:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Pełny zestaw atrybutów wewnętrznych zasad sieci szkieletowej usług można znaleźć w temacie toohello [dokumentacji zaplecza interfejsu API zarządzania](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Dodaj hello interfejsu API tooa produktu. 

Przed wywołaniem interfejsu API hello, należy dodać go tooa produktu, którym udzielasz dostępu toousers. 

 1. Hello usługi API Management, wybierz **produktów - PREVIEW**.
 2. Domyślnie produkty przeznaczone do interfejsu API zarządzania dwóch dostawców: Starter i bez ograniczeń. Wybierz hello nieograniczone produktu.
 3. Wybierz interfejsy API.
 4. Kliknij przycisk hello **+ Dodaj** przycisku.
 5. Wybierz hello `Service Fabric App` interfejsu API utworzone w poprzednich krokach hello i kliknij przycisk hello **wybierz** przycisku.

### <a name="test-it"></a>należy przeprowadzić test

Teraz możesz spróbować wysyła żądanie usługi zaplecza tooyour w sieci szkieletowej usług za pośrednictwem interfejsu API zarządzania bezpośrednio z hello portalu Azure.

 1. Hello usługi API Management, wybierz **interfejsu API — wersja ZAPOZNAWCZA**.
 2. W hello `Service Fabric App` interfejsu API utworzone w poprzednich krokach hello, wybierz hello **testu** kartę.
 3. Kliknij przycisk hello **wysyłania** toosend przycisk test żądania toohello wewnętrznej bazy danych usługi.

## <a name="next-steps"></a>Następne kroki

W tym momencie powinny mieć podstawowe ustawienia z interfejsu API zarządzania i sieci szkieletowej usług.

W tym samouczku korzysta z uwierzytelniania opartego na certyfikatach użytkownika podstawowego dla Twojego tooget klastra sieci szkieletowej usług, który można szybko skonfigurować. Bardziej zaawansowanego uwierzytelniania użytkownika dla klastra usługi sieć szkieletowa jest preferowana w [uwierzytelniania usługi Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Następnie [utworzyć i skonfigurować ustawienia zaawansowane produktu w usłudze Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare aplikacji dla ruchu w świecie rzeczywistym.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
