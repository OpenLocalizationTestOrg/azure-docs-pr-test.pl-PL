---
title: "aaaCreate Centrum IoT przy użyciu wiersza polecenia platformy Azure (azure.js) | Dokumentacja firmy Microsoft"
description: "Jak toocreate Centrum Azure IoT przy użyciu hello wiersza polecenia platformy Azure i platform (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a>Tworzenie Centrum IoT przy użyciu hello wiersza polecenia platformy Azure

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Wprowadzenie

Można użyć wiersza polecenia platformy Azure (azure.js) toocreate i programowe zarządzanie centra Azure IoT. W tym artykule opisano, jak toouse hello Azure CLI (azure.js) toocreate Centrum IoT.

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* Azure CLI (azure.js) — Witaj interfejsu wiersza polecenia dla hello klasycznego i modeli wdrażania, zarządzania zasobów zgodnie z opisem w tym artykule.
* [Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) — Witaj generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Azure CLI 0.10.4] [ lnk-CLI-install] lub nowszym. Jeśli masz już hello Azure CLI zainstalowana, można sprawdzić poprawność hello bieżącej wersji w wierszu polecenia hello z hello następujące polecenie:

```azurecli
azure --version
```

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Hello Azure CLI musi być w trybie Azure Resource Manager:
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a>Ustawianie konta i subskrypcji platformy Azure

1. W wierszu polecenia hello hello logowania, wpisując następujące polecenie:

   ```azurecli
    azure login
   ```

   Za pomocą przeglądarki sieci web sugerowane hello i tooauthenticate kodu.
1. Jeśli masz wiele subskrypcji Azure, łączenie tooAzure udziela dostępu tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika. Możesz wyświetlić hello subskrypcji platformy Azure i określenie, który jest domyślnym hello, za pomocą polecenia hello:

   ```azurecli
    azure account list
   ```

   kontekst subskrypcji hello tooset pod którym ma zostać toorun hello reszty hello, użyj polecenia:

   ```azurecli
    azure account set <subscription name>
   ```

1. Jeśli nie masz grupy zasobów, można utworzyć jedną o nazwie **exampleResourceGroup**:

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> Artykuł Hello [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów] [ lnk-CLI-arm] zawiera więcej informacji na temat sposobu toouse hello Azure CLI toomanage Azure zasobów.

## <a name="create-an-iot-hub"></a>Tworzenie Centrum IoT

Wymagane parametry:

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* **Grupa zasobów**. Nazwa grupy zasobów Hello. Hello format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, długość 1-64.
* **name**. Nazwa Hello toobe Centrum IoT hello utworzony. Hello format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, 3 – 50 długości.
* **Lokalizacja**. Witaj lokalizacji (region/centrum danych azure) tooprovision hello Centrum IoT.
* **Nazwa jednostki SKU**. Nazwa Hello sku hello, jeden z: [F1, S1, S2, S3]. Hello najnowsze pełną listę można znaleźć toohello stronie dotyczącej cen Centrum IoT.
* **jednostki**. Liczba Hello elastycznie jednostki. Zakres: F1 [1-1]: S1, S2 [1 – 200]: [1 – 10] S3. Jednostki Centrum IoT bazują na całkowita wiadomość hello i liczba liczby urządzeń ma tooconnect.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

toosee hello wszystkie dostępne na potrzeby tworzenia parametrów, możesz użyć polecenia pomocy hello w wierszu polecenia:

```azurecli
azure iothub create -h
```

Prosty przykład: toocreate Centrum IoT o nazwie **exampleIoTHubName** w grupie zasobów hello **exampleResourceGroup**Uruchom hello następujące polecenie:

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> To polecenie interfejsu wiersza polecenia Azure umożliwia utworzenie Centrum IoT standardowe S1 dla której są rozliczane. Można usunąć Centrum IoT hello **exampleIoTHubName** za pomocą następujących poleceń:
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a>Następne kroki

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello poniższego artykułu:

* [Zestawy SDK IoT][lnk-sdks]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przy użyciu hello toomanage portalu Azure IoT Hub][lnk-portal]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
