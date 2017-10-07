---
title: "błędy wdrożenia usługi Azure aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toolearn o błędach wdrożenia usługi Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Błąd wdrażania, wdrożenia usługi azure wdrażanie tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a>Zrozumienie błędy wdrożenia usługi Azure
W tym temacie opisano błędy wdrożenia i jak mogą odnajdować więcej informacji o błędzie. Błędy wdrożenia toocommon rozwiązania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="two-types-of-errors"></a>Dwa typy błędów
Istnieją dwa typy błędów, które mogą odbierać:

* Błędy sprawdzania poprawności
* Błędy wdrożenia

powitania po obraz zawiera dziennik aktywności hello subskrypcji. Reprezentuje dwa wdrożenia. W przypadku wdrożenia jednego szablonu hello nie przeszedł sprawdzania poprawności (**weryfikacji**) i nie kontynuować. W hello inne wdrożenia, szablon hello przeszły sprawdzanie poprawności, ale nie powiodło się podczas tworzenia zasobów hello (**zapisu wdrożeń**). 

![Pokaż kod błędu:](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

Błędy sprawdzania poprawności wynikają z scenariusze, które można określić przed przystąpieniem do wdrożenia. Obejmują one błędy składniowe w szablonie lub w trakcie zasobów toodeploy przekraczające przydziałami subskrypcji. Błędy wdrożenia wynikają z warunki, jakie występują podczas procesu wdrażania hello. Obejmują one próby tooaccess z zasobem, który jest wdrażany jednocześnie.

Oba typy błędy zwracany błąd o kodzie użycie tootroubleshoot hello wdrożenia. Oba typy błędy są wyświetlane w hello [dziennik aktywności](resource-group-audit.md). Błędy sprawdzania poprawności nie pojawiają się jednak w historii wdrożenia, ponieważ wdrożenie hello nigdy nie jest uruchomiony.

## <a name="determine-error-code"></a>Określić kod błędu:

Informacje na temat błędu analizując komunikat o błędzie hello i hello kod błędu. Witaj [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md) artykule wymieniono rozwiązania przez kod błędu. W tym temacie przedstawiono sposób toouse hello kod błędu hello toodiscover portalu Azure.

### <a name="validation-errors"></a>Błędy sprawdzania poprawności

W przypadku wdrażania za pośrednictwem portalu hello, zobaczysz błąd sprawdzania poprawności po przesłaniu wartości.

![Pokaż błąd sprawdzania poprawności portalu](./media/resource-manager-troubleshoot-tips/validation-error.png)

Wybierz wiadomość hello więcej szczegółów. W hello po obrazu, zobacz **InvalidTemplateDeployment** błąd i komunikat informujący zasad zablokowane wdrożenia.

![Pokaż szczegóły sprawdzania poprawności](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>Błędy wdrożenia

Podczas operacji hello pozytywnej weryfikacji, ale nie powiodło się podczas wdrażania, zostanie wyświetlony błąd hello w powiadomieniach hello. Wybierz powiadomienie hello.

![Błąd powiadomienia](./media/resource-manager-troubleshoot-tips/notification.png)

Możesz dowiedzieć się więcej o wdrażaniu hello. Wybierz więcej informacji o błędzie hello hello toofind opcji.

![Wdrażanie nie powiodło się](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

Zostanie wyświetlony kody błędów hello wiadomości i błędów. Należy zauważyć, że istnieją dwa kody błędów. Witaj pierwszy kod błędu (**niepowodzenia wdrożenia**) jest błąd ogólny, który nie zapewnia hello szczegółowe informacje możesz potrzeby toosolve hello błąd. Witaj drugi kod błędu (**StorageAccountNotFound**) zawiera szczegóły hello potrzebne. 

![Szczegóły błędu](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>Włączenie rejestrowania debugowania
Czasami uzyskać więcej informacji dotyczących toodiscover żądań i odpowiedzi hello co poszło źle. Przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure, mogą żądać, aby uzyskać dodatkowe informacje jest rejestrowane podczas wdrażania.

- PowerShell

   W programie PowerShell, należy ustawić hello **DeploymentDebugLogLevel** tooAll parametru, obiektu ResponseContent lub RequestContent.

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   Sprawdź zawartość żądania hello z hello następującego polecenia cmdlet:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   Lub hello zawartości z odpowiedzi:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   Te informacje mogą pomóc w określeniu, czy wartość w szablonie hello jest są ustawione niepoprawnie.

- Interfejs wiersza polecenia platformy Azure

   Sprawdź operacje wdrażania hello z hello następujące polecenie:

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- Szablon zagnieżdżony

   toolog informacji debugowania dla zagnieżdżony szablon, użyj hello **debugSetting** elementu.

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a>Tworzenie szablonu rozwiązywania problemów
W niektórych przypadkach hello Najprostszym sposobem tootroubleshoot szablon jest tootest jej części. Można utworzyć szablon uproszczony, umożliwiającą toofocus na części hello uważasz, że przyczyną jest błąd hello. Na przykład załóżmy, że otrzymujesz błąd podczas odwoływania się do zasobu. Zamiast dotyczącą całą szablonu, utworzyć szablon, który zwraca część hello, który może być przyczyną tego problemu. Możesz określić, czy jest przekazywany hello prawo parametrów, przy użyciu funkcji szablonu prawidłowo, i pobieranie zasobu hello oczekiwać może pomóc.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

Lub Załóżmy, że pojawiły się błędy wdrożenia, które Twoim zdaniem są powiązane zestawu tooincorrectly zależności. Przetestuj szablonu przez podzielenie go na uproszczonej szablonów. Najpierw Utwórz szablon, który wdraża jednego zasobu (np. programu SQL Server). Podczas pracy upewnić się, że ten zasób zdefiniowany prawidłowo, Dodaj zasób zależy od niego (na przykład baza danych SQL). Jeśli te dwa zasoby zdefiniowany prawidłowo, należy dodać inne zasoby zależne (na przykład zasady inspekcji). Between każdego wdrożenia testu Usuń hello grupy toomake się, że należy odpowiednio testowania hello zależności między zasobami. 

## <a name="check-deployment-sequence"></a>Sprawdź wdrożenie sekwencji

Wiele błędów wdrażania się tak zdarzyć, gdy zasoby są wdrożone w nieoczekiwany sekwencji. Te błędy wystąpić, gdy zależności nie są poprawnie ustawione. Jeśli brakuje wymaganych zależności, jeden zasób prób toouse wartość innego zasobu, ale hello innych jeszcze nie istnieje. Otrzymasz komunikat o błędzie informujący, że zasób nie został znaleziony. Mogą wystąpić błędy tego typu sporadycznie hello czasu wdrożenia dla każdego zasobu może się różnić. Na przykład Twojego pierwszego toodeploy próba zasobami powiedzie się, ponieważ wymagany zasób jest przeprowadzany losowo w czasie. Jednak z druga próba nie powiedzie się z powodu hello wymaganych zasobów nie została ukończona w czasie. 

Ale ma tooavoid Ustawianie zależności, które nie są wymagane. Gdy niepotrzebne zależności, można przedłużyć czas trwania hello hello wdrożenia, zapobiegając zasoby, które nie są wzajemnie zależne od wdrażany równolegle. Ponadto można utworzyć zależności cykliczne, które blokują hello wdrożenia. Witaj [odwołania](resource-group-template-functions-resource.md#reference) funkcja tworzy niejawne zależności hello odwołuje się do zasobu, gdy zasób jest wdrażany w hello tego samego szablonu. W związku z tym może mieć zależności więcej niż określona w hello zależności hello **dependsOn** właściwości. Witaj [resourceId](resource-group-template-functions-resource.md#resourceid) funkcji nie utworzyć niejawnego zależności lub zweryfikować, że istnieje zasób hello.

W przypadku wystąpienia problemów zależności, należy toogain wgląd w kolejności hello wdrożenia zasobów. kolejność hello tooview operacji wdrażania:

1. Wybierz hello historii wdrożenia dla grupy zasobów.

   ![Wybierz Historia wdrażania](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. Wybierz wdrożenie z historii hello, a następnie wybierz **zdarzenia**.

   ![Wybierz zdarzenia wdrożenia](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. Sprawdź, czy hello sekwencji zdarzeń dla każdego zasobu. Należy zwrócić uwagę toohello stan każdej operacji. Na przykład hello poniższej ilustracji przedstawiono trzy konta magazynu, które wdrożone równolegle. Należy zauważyć, że hello trzy konta magazynu są uruchamiane na powitania tym samym czasie.

   ![Wdrożenie równoległe](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   Następny obraz powitania zawiera trzy konta magazynu, które nie są wdrażane równolegle. Hello drugiego konta magazynu zależy od hello pierwsze konto magazynu, a trzeci konta magazynu hello zależy hello drugiego konta magazynu. W związku z tym hello pierwsze konto magazynu jest uruchomiona, zaakceptowane i zakończona, zanim hello obok została uruchomiona.

   ![kolejne wdrożenia](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

Nawet w przypadku bardziej złożonych zadań, można użyć tego samego toodiscover technika Witaj, podczas wdrażania zostanie rozpoczęte i zakończone dla każdego zasobu. Przejrzyj toosee zdarzenia z wdrożenia, jeśli sekwencja hello jest inny niż oczekiwany. Jeśli tak, można obliczyć ponownie hello zależności dla tego zasobu.

Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu. Zwraca się, że istnieje komunikat o błędzie stwierdzający, w szczególności zależność cykliczną. toosolve zależność cykliczną:

1. W szablonie należy znaleźć zasobu hello objęci hello zależność cykliczną. 
2. Dla tego zasobu, sprawdź hello **dependsOn** właściwości i wszelkie używa hello **odwołania** toosee zasobów, do których ona zależy od funkcji. 
3. Sprawdź, czy toosee tych zasobów, zasobów, do których one zależą od. Wykonaj zależności hello dopóki zauważysz z zasobem, który jest zależny od zasobu oryginalnego hello.
5. Dla zasobów hello objętego hello zależność cykliczną, należy dokładnie zbadać wszystkich zastosowań hello **dependsOn** tooidentify właściwości wszelkie zależności, które nie są wymagane. Usuń te zależności. Jeśli nie wiesz, czy zależność jest potrzebny, spróbuj go usunąć. 
6. Należy ponownie wdrożyć szablon hello.

Usuwanie wartości z hello **dependsOn** właściwości, które mogą powodować błędy podczas wdrażania szablonu hello. Jeśli wystąpi błąd, należy dodać zależności hello do hello szablonu. 

Jeśli takie podejście nie rozwiązuje hello zależność cykliczną, rozważ migrację część logiki wdrażania zasobów podrzędnych (na przykład rozszerzenia lub ustawienia konfiguracji). Po hello zasoby związane z hello zależność cykliczną, należy skonfigurować te toodeploy zasoby podrzędne. Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się toohello innych właściwości. Można je wdrożyć w hello w następującej kolejności:

1. vm1
2. maszyny vm2
3. Rozszerzenie na vm1 zależy od vm1 i maszyny vm2. rozszerzenie Hello ustawia wartości vm1, który otrzymuje od maszyny vm2.
4. Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2. rozszerzenie Hello ustawia wartości maszyny vm2, który otrzymuje od vm1.

Witaj, które same podejście działa w przypadku aplikacji usługi App Service. Rozważ przeniesienie do zasobu podrzędnego zasób aplikacji hello wartości konfiguracji. Można wdrożyć dwie aplikacje sieci web w hello w następującej kolejności:

1. webapp1
2. webapp2
3. Konfiguracja webapp1 zależy od webapp1 i webapp2. Zawiera ustawienia aplikacji wartościami z webapp2.
4. Konfiguracja webapp2 zależy od webapp1 i webapp2. Zawiera ustawienia aplikacji wartościami z webapp1.


## <a name="next-steps"></a>Następne kroki
* Błędy wdrożenia toocommon rozwiązania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn o inspekcji akcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).
* toolearn o błędach hello toodetermine akcje podczas wdrażania, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
