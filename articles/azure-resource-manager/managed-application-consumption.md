---
title: "zarządzana aplikacja — aaaConsume platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak klient tworzy platformy Azure zarządzanych aplikacji z plików publikowanych."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Korzystanie z wewnętrznej zarządzanej aplikacji

Będzie można korzystać z usługi Azure [zarządzane aplikacje](managed-application-overview.md) które są przeznaczone do członków organizacji. Na przykład można wybrać aplikacje zarządzane przez dział IT, która zapewnić zgodność ze standardami w organizacji. Te aplikacje zarządzane są dostępne za pośrednictwem hello katalogu usług, hello Azure Marketplace.

Przed kontynuowaniem w tym artykule, musi mieć zarządzanej aplikacji dostępne w katalogu usług powitania dla Twojej subskrypcji. Jeśli ktoś w organizacji nie już utworzony zarządzanej aplikacji, zobacz [publikowania aplikacji zarządzanej na użytek wewnętrzny](managed-application-publishing.md).

Obecnie można użyć wiersza polecenia platformy Azure lub hello Azure tooconsume portalu zarządzanej aplikacji.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Tworzenie aplikacji hello zarządzane przy użyciu portalu hello

toodeploy zarządzanych aplikacji za pośrednictwem portalu hello, wykonaj następujące kroki:

1. Przejdź toohello portalu Azure. Wyszukaj **katalogu usług zarządzanych aplikacji**.

   ![Katalog usług zarządzanych aplikacji](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Wybierz hello zarządzana aplikacja ma toocreate z listy hello dostępnych rozwiązań. Wybierz pozycję **Utwórz**.

   ![Wybór aplikacji zarządzanej](./media/managed-application-consumption/select-offer.png)

1. Podaj wartości parametrów hello, które są wymagane tooprovision hello zasobów. Wybierz **zachodnie centralnej nam** dla lokalizacji. Kliknij przycisk **OK**.

   ![Parametry aplikacji zarządzanych](./media/managed-application-consumption/input-parameters.png)

1. Szablon Hello sprawdza poprawność wartości hello, podane. Jeśli weryfikacja zakończy się powodzeniem, wybierz **OK** toostart hello wdrożenia.

   ![Sprawdzanie poprawności zarządzanej aplikacji](./media/managed-application-consumption/validation.png)

Po zakończeniu wdrożenia hello hello odpowiednie zasoby zdefiniowane w szablonie hello są udostępniane w grupie zasobów zarządzanych hello, podane.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Tworzenie aplikacji hello zarządzane przy użyciu wiersza polecenia platformy Azure

Istnieją dwa sposoby toocreate zarządzaną aplikację za pomocą wiersza polecenia platformy Azure:

* Polecenie hello do tworzenia aplikacji zarządzanych.
* Polecenie wdrożenia szablonu regularne hello.

### <a name="use-hello-template-deployment-command"></a>Polecenie wdrożenia szablonu hello

Wdróż plik applianceMainTemplate.json hello hello dostawcy utworzone.

Następnie należy utworzyć dwie grupy zasobów. Witaj pierwszej grupy zasobów jest gdzie hello aplikacji zarządzanej jest utworzony zasób: Microsoft.Solutions/appliances. Witaj drugi zawiera wszystkie hello zasoby zdefiniowane w mainTemplate.json. Ta grupa zasobów jest zarządzana przez hello niezależnego dostawcy oprogramowania.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Użyj `westcentralus` jako lokalizacji hello hello grupy zasobów.
>

applianceMainTemplate.json toodeploy w mainResourceGroup, hello Użyj następującego polecenia:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Po hello szablonu przebiegów poprzedzających monituje o podanie wartości hello hello parametrów, które są zdefiniowane w szablonie hello. Ponadto toohello parametrów, które są potrzebne zasoby tooprovision w szablonie, należy dwóch wartości parametrów klucza:

- **managedResourceGroupId**: hello identyfikator hello zasobów grupy zawierające hello zasoby zdefiniowane w applianceMainTemplate.json. Identyfikator Hello ma formę hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. W hello poprzedzających przykładzie, tego Identyfikatora hello `managedResourceGroup`.
- **applianceDefinitionId**: hello identyfikator hello zarządzanych zasobów definicji aplikacji. Ta wartość jest dostarczana przez hello niezależnego dostawcy oprogramowania.

> [!NOTE]
> Wydawca Hello musi udzielić dostępu toohello zasobów grupy, która zawiera definicję aplikacji hello zarządzane. w subskrypcji wydawcy hello zostanie utworzona Hello definicji zasobu. W związku z tym użytkownika, grupy użytkowników lub aplikacji w dzierżawie klienta hello musi zasobów toothis dostęp do odczytu.

Po hello wdrożenie zakończy się pomyślnie, zobacz hello zarządzane w mainResourceGroup tworzenia aplikacji. Witaj storageAccount zasób został utworzony w managedResourceGroup.

### <a name="use-hello-create-command"></a>Użyj hello Utwórz polecenie

Można użyć hello `az managedapp create` toocreate polecenia zarządzanej aplikacji z hello zarządzane definicji aplikacji.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Identyfikator urządzenia definicji**: identyfikator zasobu hello hello zarządzane utworzone w hello poprzedzających krok definicji aplikacji. tooobtain ten identyfikator, uruchom następujące polecenie hello:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  To polecenie zwraca definicji aplikacji hello zarządzane. Należy wartość hello hello identyfikator właściwości.

* **zarządzane-zarządcy zasobów id**: Nazwa hello hello zasobów grupy zawierające hello zasoby zdefiniowane w applianceMainTemplate.json. Ta grupa zasobów to grupa zasobów zarządzanych hello. Zarządza hello wydawcy. Jeśli nie istnieje, jest tworzony automatycznie.
* **Grupa zasobów**: utworzono hello grupy zasobów, której hello zarządzanych zasobów aplikacji. Witaj Microsoft.Solutions/appliance zasobów znajduje się w tej grupie zasobów.
* **Parametry**: hello parametrów, które są wymagane przez hello zasoby zdefiniowane w applianceMainTemplate.json.

## <a name="known-issues"></a>Znane problemy

Ta wersja zapoznawcza zawiera hello następujące problemy:

* Podczas tworzenia hello hello zarządzanych aplikacji zostanie wyświetlony 500 Wewnętrzny błąd serwera. Jeśli napotkasz problem jest prawdopodobnie toobe tymczasowymi. Ponów operację hello.
* Nowa grupa zasobów jest wymagany dla grupy zasobów zarządzanych hello. Jeśli używasz istniejącej grupy zasobów, hello wdrożenie zakończy się niepowodzeniem.
* Witaj grupę zasobów zawierającą hello Microsoft.Solutions/appliances zasobów muszą być tworzone w hello **westcentralus** lokalizacji.

## <a name="next-steps"></a>Następne kroki

* Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).
* Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
* Aby informacji na temat publikowania aplikacji zarządzanych toohello portalu Azure Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).
