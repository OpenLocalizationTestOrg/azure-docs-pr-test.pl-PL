---
title: "aaaAzure diagnostyki wersji schematu konfiguracji rozszerzenie i historię | Dokumentacja firmy Microsoft"
description: "Toocollecting odpowiednich liczników wydajności w maszynach wirtualnych platformy Azure, zestawy skalowania maszyny Wirtualnej, sieci szkieletowej usług i usługi w chmurze."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Azure wersji schematu konfiguracji rozszerzenie diagnostyki i historii
Indeksy tej strony wersji schematu rozszerzenia diagnostyki Azure dostarczana jako część programu hello zestawu SDK usługi Microsoft Azure.  

> [!NOTE]
> Hello rozszerzenie Azure Diagnostics jest składnik hello używany toocollect liczniki wydajności i innych danych statystycznych z:
> - Azure Virtual Machines 
> - Zestawy skali maszyn wirtualnych
> - Service Fabric 
> - Cloud Services 
> - Grupy zabezpieczeń sieci
> 
> Ta strona jest tylko istotne, jeśli używasz tych usług.

Witaj rozszerzenie Azure Diagnostics jest używany z innymi produktami firmy Microsoft diagnostyki, takich jak Azure monitora, usługi Application Insights i analizy dzienników. Aby uzyskać więcej informacji, zobacz [omówienie narzędzi monitorowania Microsoft](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Azure wersji zestawu SDK i informacji diagnostycznych wysyłania wykresu  

|Wersja zestawu SDK platformy Azure | Wersja rozszerzenia diagnostyki | Model|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |wtyczki|  
|2.0 - 2.4         |1.0                            |wtyczki|  
|2.5               |1.2                            |Rozszerzenia|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2.9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Diagnostyka Azure w wersji 1.0 najpierw dostarczoną w wtyczki model — co oznacza, czy zainstalowany hello Azure SDK, masz wersji hello diagnostyki Azure zostały wydane z nim.  

 Począwszy od zestawu SDK, 2.5 (Diagnostyka w wersji 1.2), Diagnostyka Azure poszło tooan rozszerzenia modelu. nowe funkcje tooutilize narzędzia Hello tylko były dostępne w nowszej Azure SDK, ale usługi za pomocą diagnostyki Azure czy odebrania hello najnowszej wersji wysyłki bezpośrednio z platformy Azure. Na przykład każdy użytkownik nadal przy użyciu zestawu SDK, 2.5 będzie można ładowania najnowszej wersji hello pokazano w poprzedniej tabeli hello, niezależnie od tego, jeśli używają hello nowsze funkcje.  

## <a name="schemas-index"></a>Indeks schematów  
Różne wersje diagnostyki Azure używają schematy innej konfiguracji. 

[Schemat konfiguracji diagnostyki 1.0](azure-diagnostics-schema-1dot0.md)  

[Schemat konfiguracji diagnostyki 1.2](azure-diagnostics-schema-1dot2.md)  

[Diagnostyka 1.3 i nowszym schemat konfiguracji](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Historia wersji


### <a name="diagnostics-extension-19"></a>Diagnostyka rozszerzenia 1.9 
Dodano obsługę Docker.


### <a name="diagnostics-extension-181"></a>Diagnostyka rozszerzenia 1.8.1 
Można określić tokenu sygnatury dostępu Współdzielonego, zamiast klucz konta magazynu w konfiguracji prywatnej hello. Jeśli zostanie podany SAS token, klucz konta magazynu hello jest ignorowana.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Diagnostyka rozszerzenia 1.8 
Dodano tooPublicConfig typu magazynu. Może być StorageType *tabeli*, *obiektu Blob*, *TableAndBlob*. *Tabela* jest domyślnym hello.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Diagnostyka rozszerzenia 1.7 
Dodano hello tooEventHub tooroute możliwości.

### <a name="diagnostics-extension-15"></a>Rozszerzenia diagnostyki w wersji 1.5
Dodaje hello wychwytywanie elementu i hello dane diagnostyczne toosend możliwości zbyt[usługi Application Insights](../application-insights/app-insights-cloudservices.md) co ułatwia problemów toodiagnose w Twojej aplikacji, a także hello poziom systemu i infrastruktury.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>2.6 zestawu SDK i informacji diagnostycznych rozszerzenie Azure 1.3 
Usługi w chmurze projektów programu Visual Studio hello następujące zmiany zostały wprowadzone. (Te zmiany mają zastosowanie również toolater wersji zestawu SDK platformy Azure.)

* emulator lokalne powitania obsługuje teraz diagnostyki. Oznacza to, można zbierać dane diagnostyczne i upewnij się, że aplikacja tworzy hello prawo śladów podczas tworzenia i testowania w programie Visual Studio. Witaj parametry połączenia `UseDevelopmentStorage=true` umożliwia zbieranie danych diagnostycznych, gdy używasz projekt usługi w chmurze w programie Visual Studio przy użyciu emulatora magazynu Azure hello. Wszystkie dane diagnostyczne są zbierane na koncie magazynu hello (Programowanie magazynu).
* Parametry połączenia konta magazynu diagnostyki Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) znajduje się jeszcze raz w pliku konfiguracji (cscfg) hello usługi. W systemie Azure SDK 2.5 konto magazynu diagnostyki hello została określona w pliku diagnostics.wadcfgx hello.

Istnieją pewne ważne różnice między jak parametry połączenia hello działał w 2.4 zestawu SDK platformy Azure i starszych i jak działa w Azure SDK w wersji 2.6 lub nowszej.

* W 2.4 zestawu SDK platformy Azure i starszych parametry połączenia hello był używany jako środowisko uruchomieniowe w hello diagnostyki wtyczki tooget hello informacji o koncie magazynu przesyłania dzienników diagnostycznych.
* W Azure SDK w wersji 2.6 lub nowszej ciąg połączenia diagnostyki hello jest używany przez rozszerzenie Diagnostyka programu Visual Studio tooconfigure hello hello magazynu odpowiednie informacje o koncie podczas publikowania. Parametry połączenia Hello umożliwia definiowanie różnych kont magazynu dla konfiguracji innej usługi, które Visual Studio będzie korzystać w przypadku publikowania. Jednak ponieważ hello diagnostyki wtyczki nie jest już dostępny (po 2.5 zestawu SDK platformy Azure), plik .cscfg hello samodzielnie nie można włączyć hello rozszerzenia diagnostyki. Masz rozszerzenia hello tooenable z osobna za pomocą narzędzi, takich jak Visual Studio lub programu PowerShell.
* proces hello toosimplify konfigurowania rozszerzenia diagnostyki hello przy użyciu programu PowerShell, hello pakietu wyjście z programu Visual Studio zawiera także hello publicznej konfiguracji XML hello diagnostyki rozszerzenia dla poszczególnych ról. Visual Studio będzie korzystać hello diagnostyki połączenia ciąg toopopulate hello informacji o koncie magazynu w konfiguracji publicznego hello. pliki konfiguracji publicznego Hello są tworzone w folderze rozszerzenia hello i wykonaj wzorzec hello PaaSDiagnostics. <RoleName>. PubConfig.xml. Wszystkie wdrożenia programu PowerShell na podstawie można użyć tego wzorca toomap każdego tooa konfiguracji roli.
* Witaj parametry połączenia w pliku .cscfg hello jest już używana przez hello dane diagnostyczne hello tooaccess portalu Azure, może występować w hello **monitorowanie** parametry połączenia hello kartę są potrzebne tooconfigure hello usługi tooshow pełne dane w portalu hello monitorowania.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrowanie projektów tooAzure SDK 2.6 lub nowszej
Podczas migrowania z tooAzure Azure SDK 2.5 SDK w wersji 2.6 lub nowszej, jeśli masz konto magazynu diagnostyki określone w pliku .wadcfgx hello, następnie pozostanie on istnieje. Zaletą tootake hello elastyczność za pomocą innego magazynu kont do innego magazynu konfiguracji, należy dodać projekt tooyour ciąg połączenia hello toomanually. W przypadku migrowania projektu z Azure SDK 2.4 lub starszych tooAzure 2.6 zestawu SDK, następnie hello diagnostyki parametry połączenia zostaną zachowane. Pamiętaj jednak zmiany hello jak parametry połączenia są traktowane w Azure SDK w wersji 2.6 określone w poprzedniej sekcji hello.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Jak określa konto magazynu diagnostyki hello w Visual Studio
* Jeśli parametry połączenia diagnostyki jest określone w pliku .cscfg hello, Visual Studio używa on tooconfigure hello diagnostyki rozszerzenia podczas publikowania i podczas generowania pliki xml konfiguracji publicznego hello podczas pakowania.
* Jeśli ciąg połączenia diagnostyki nie została określona w pliku .cscfg hello, następnie Visual Studio w języku konta magazynu hello toousing określonego w hello .wadcfgx tooconfigure hello diagnostyki rozszerzenie pliku podczas publikowania i generowania hello publicznego pliki xml konfiguracji podczas pakowania.
* Parametry połączenia diagnostyki Hello w pliku .cscfg hello mają pierwszeństwo przed hello konta magazynu w pliku .wadcfgx hello. Jeśli parametry połączenia diagnostyki jest określona w pliku .cscfg hello, następnie Visual Studio użyty i ignoruje hello konta magazynu w .wadcfgx.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Co to Witaj, "Aktualizuj parametry połączenia magazynu programowanie..." czy pole wyboru?
Witaj wyboru **zaktualizować parametry połączenia magazynu programowanie dla diagnostyki i buforowanie z poświadczeniami konta magazynu Microsoft Azure podczas publikowania tooMicrosoft Azure** daje żadnych tooupdate wygodny sposób Programowanie parametry połączenia konta magazynu z kontem magazynu platformy Azure hello określony podczas publikowania.

Załóżmy na przykład, zaznacz to pole wyboru i określa parametry połączenia diagnostyki hello `UseDevelopmentStorage=true`. Podczas publikowania hello tooAzure projektu programu Visual Studio będzie automatycznie zaktualizować parametry połączenia diagnostyki hello z kontem magazynu hello określone w Kreatorze publikowania hello. Jednak jeśli konto magazynu rzeczywista określono jako parametry połączenia diagnostyki hello, następnie to konto jest używana zamiast tego.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostyka funkcji różnice między 2.4 zestawu SDK platformy Azure i wcześniej i Azure SDK, 2.5 lub nowszej
Jeśli uaktualniasz projektu z tooAzure Azure SDK 2.4 SDK, 2.5 lub nowszej, powinna zawierać się w hello uwadze następujące różnice funkcji diagnostyki.

* **Konfiguracyjne interfejsy API są przestarzałe** — trybu diagnostyki jest dostępna w 2.4 zestawu SDK platformy Azure i jego wcześniejsze wersje, ale jest przestarzała w wersji 2.5 zestawu SDK platformy Azure i nowszych. Jeśli aktualnie zdefiniowano konfigurację diagnostyki w kodzie, konieczne będzie tooreconfigure tych ustawień od podstaw w projekcie migrowanych hello aby pracy tookeep diagnostyki. plik konfiguracji diagnostyki Hello Azure SDK 2.4 jest diagnostics.wadcfg i diagnostics.wadcfgx dla 2.5 zestawu SDK platformy Azure i nowszych.
* **Można skonfigurować tylko na poziomie roli hello, nie na poziomie wystąpienia hello diagnostyki dla aplikacji usługi w chmurze.**
* **Za każdym razem, gdy wdrażanie aplikacji, zaktualizowano konfigurację diagnostyki hello** — może to powodować problemy z parzystością, jeśli zmiana konfiguracji diagnostyki z Eksploratora serwera, a następnie ponowne wdrożenie aplikacji.
* **W wersji 2.5 zestawu SDK platformy Azure i nowszych, zrzuty awaryjne są konfigurowane w pliku konfiguracji diagnostyki hello, nie w kodzie** — Jeśli masz zrzuty awaryjne skonfigurowane w kodzie, będziesz mieć toomanually transfer hello konfiguracji z pliku konfiguracji toohello kodu, Ponieważ zrzuty awaryjne hello nie są przenoszone podczas tooAzure migracji hello 2.6 zestawu SDK.

