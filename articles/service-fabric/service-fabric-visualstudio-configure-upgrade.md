---
title: "uaktualnienie hello aaaConfigure aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure hello ustawienia dotyczące uaktualniania aplikacji sieci szkieletowej usług za pomocą programu Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Skonfiguruj hello uaktualnienie aplikacji usługi Service Fabric w programie Visual Studio
Visual Studio tools dla sieci szkieletowej usług Azure zapewniają obsługę uaktualnienia publikowania toolocal lub zdalnych klastrów. Istnieją trzy scenariusze, w których chcesz tooupgrade Twojej aplikacji tooa nowsza wersja zamiast zastępowania aplikacji hello podczas testowania i debugowania:

* Dane aplikacji nie będzie utracone podczas uaktualniania hello.
* Dostępności pozostaje wysoka, nie będzie przerw w działaniu usługi podczas uaktualniania hello, jeśli brak wystarczającej liczby wystąpień usługi rozmieszczenie domen uaktualnienia.
* Testy mogą być uruchamiane na aplikacji, podczas gdy jest uaktualniany.

## <a name="parameters-needed-tooupgrade"></a>Parametry wymagane tooupgrade
Są dostępne dwa typy wdrażania: regularne lub uaktualniania. Regularne wdrożenia usuwa wszelkie poprzednie informacje na temat wdrażania i dane w klastrze hello podczas wdrażania uaktualnienia zachowuje on. Podczas uaktualniania aplikacji usługi Service Fabric w programie Visual Studio należy parametry uaktualnienia tooprovide aplikacji i zasad dotyczących kondycji wyboru. Parametry uaktualniania aplikacji pomocy formantu hello uaktualnieniu podczas kondycji Sprawdź zasady określają, czy hello uaktualnienie zakończyło się pomyślnie. Zobacz [uaktualniania aplikacji usługi Service Fabric: parametry uaktualnienia](service-fabric-application-upgrade-parameters.md) więcej szczegółów.

Istnieją trzy tryby uaktualnienia: *monitorowanej*, *UnmonitoredAuto*, i *UnmonitoredManual*.

* Uaktualnienie monitorowanej automatyzuje hello uaktualnienia i aplikacji sprawdzania kondycji.
* Uaktualnienie UnmonitoredAuto automatyzuje hello uaktualnienia, ale pomija hello sprawdzenie kondycji aplikacji.
* Po wykonaniu uaktualnienia UnmonitoredManual należy toomanually każdej z domen uaktualnienia.

Każdy tryb uaktualniania wymaga różnych zestawów parametrów. Zobacz [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) toolearn więcej informacji na temat dostępnych opcji uaktualniania hello.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Uaktualnianie aplikacji usługi Service Fabric w programie Visual Studio
Jeśli używasz hello sieci szkieletowej usług programu Visual Studio tools tooupgrade aplikacji usługi Service Fabric, można określić toobe proces publikowania uaktualnienia zamiast regularnego wdrażania sprawdzając hello **uaktualnienia aplikacji hello** Sprawdź pole.

### <a name="tooconfigure-hello-upgrade-parameters"></a>Parametry uaktualniania hello tooconfigure
1. Kliknij przycisk hello **ustawienia** przycisku Dalej toohello pole wyboru. Witaj **Edytuj parametry uaktualnienia** zostanie wyświetlone okno dialogowe. Witaj **Edytuj parametry uaktualnienia** okno dialogowe obsługuje hello monitorowana, UnmonitoredAuto i UnmonitoredManual tryby uaktualnienia.
2. Wybierz tryb uaktualniania hello mają toouse, a następnie wypełnij hello parametru siatki.

    Każdy parametr ma wartości domyślnej. Witaj opcjonalny parametr *DefaultServiceTypeHealthPolicy* przyjmuje wprowadzania tabeli skrótów. Oto przykład hello skrótu tabeli format wejściowy *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* jest inny opcjonalnym parametrem, który przyjmuje wprowadzania tabeli skrótów hello następującego formatu:

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Oto przykład rzeczywistych:

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. W przypadku wybrania UnmonitoredManual tryb uaktualniania należy ręcznie uruchomić toocontinue konsoli programu PowerShell i Zakończ proces uaktualniania hello. Odwołuje się zbyt[uaktualniania aplikacji sieci szkieletowej usług: Tematy zaawansowane](service-fabric-application-upgrade-advanced.md) toolearn sposób ręcznego uaktualnienia działa.

## <a name="upgrade-an-application-by-using-powershell"></a>Uaktualnianie aplikacji przy użyciu programu PowerShell
Możesz użyć tooupgrade poleceń cmdlet programu PowerShell aplikacji sieci szkieletowej usług. Zobacz [samouczek uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade-tutorial.md) i [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) Aby uzyskać szczegółowe informacje.

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Określ zasady sprawdzania kondycji w pliku manifestu aplikacji hello
Każda usługa w aplikacji platformy Service Fabric może mieć własne parametry zasad kondycji, które zastąpić wartości domyślne hello. Możesz podać te wartości parametrów w pliku manifestu aplikacji hello.

Witaj poniższy przykład przedstawia sposób tooapply unikatowy kondycji Sprawdź zasady dla każdej usługi w manifeście aplikacji hello.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat wdrażania aplikacji, zobacz [wdrażania istniejącej aplikacji w sieci szkieletowej usług Azure](service-fabric-deploy-existing-app.md).