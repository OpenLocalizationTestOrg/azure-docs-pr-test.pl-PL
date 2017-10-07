---
title: "aaaCreate Centrum IoT przy użyciu wiersza polecenia platformy Azure (az.py) | Dokumentacja firmy Microsoft"
description: "Jak toocreate Centrum Azure IoT przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure i platform (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a>Tworzenie Centrum IoT przy użyciu hello Azure CLI 2.0

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Wprowadzenie

Można użyć toocreate Azure CLI 2.0 (az.py) i programowe zarządzanie centra Azure IoT. W tym artykule opisano, jak toouse hello Azure CLI 2.0 (az.py) toocreate Centrum IoT.

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* [Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) — hello interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.
* Azure CLI 2.0 (az.py) - hello generacji interfejsu wiersza polecenia dla hello zarządzania model wdrażania zasobów zgodnie z opisem w tym artykule.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Azure CLI 2.0][lnk-CLI-install].

## <a name="sign-in-and-set-your-azure-account"></a>Zaloguj się i ustawić konta platformy Azure

Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.

1. W wierszu polecenia hello Uruchom hello [polecenia logowania][lnk-login-command]:
    
    ```azurecli
    az login
    ```

    Postępuj zgodnie z tooauthenticate instrukcje hello przy użyciu kodu hello i zaloguj się na tooyour konto platformy Azure za pośrednictwem przeglądarki sieci web.

2. Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello Azure konta skojarzone z poświadczeniami użytkownika. Poniższych hello [toolist polecenia hello Azure kont] [ lnk-az-account-command] dostępne dla toouse możesz:
    
    ```azurecli
    az account list 
    ```

    Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello. Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a>Tworzenie Centrum IoT

Przy użyciu hello Azure CLI toocreate grupę zasobów, a następnie dodaj Centrum IoT.

1. Podczas tworzenia Centrum IoT należy utworzyć ją w grupie zasobów. Użyj istniejącej grupy zasobów lub uruchomić następujące hello [toocreate polecenia grupę zasobów][lnk-az-resource-command]:
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > Witaj w poprzednim przykładzie tworzy hello grupy zasobów w hello lokalizacji zachodnie stany USA. Można wyświetlić listę dostępnych lokalizacji, uruchamiając polecenie hello `az account list-locations -o table`.
    >
    >

2. Uruchom następujące hello [toocreate polecenia Centrum IoT] [ lnk-az-iot-command] w grupie zasobów, przy użyciu globalnie unikatowej nazwy Centrum IoT:
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> poprzednie polecenie Hello utworzenie Centrum IoT w hello S1, dla której są rozliczane warstwy cenowej. Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure][lnk-iot-pricing].
>
>

## <a name="remove-an-iot-hub"></a>Usuń Centrum IoT

Można użyć hello Azure CLI zbyt[usunąć pojedynczego zasobu][lnk-az-resource-command], na przykład Centrum IoT lub Usuń grupę zasobów i wszystkie jego zasoby, w tym wszystkie centra IoT.

toodelete Centrum IoT, uruchom następujące polecenie hello:

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

toodelete grupę zasobów i wszystkie jego zasoby, hello uruchom następujące polecenie:

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przy użyciu hello toomanage portalu Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
