---
title: "aaaDeploy tooAzure wystąpień kontenera z hello rejestru kontenera platformy Azure | Dokumentacja platformy Azure"
description: "Wdrażanie wystąpień kontenera tooAzure z hello rejestru kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Wdrażanie wystąpień kontenera tooAzure z hello rejestru kontenera platformy Azure

Witaj rejestru kontenera Azure jest rejestru Azure, prywatnego obrazów kontenera Docker. W tym artykule opisano, jak toodeploy kontenera obrazy przechowywane w hello Azure kontenera rejestru tooAzure wystąpień kontenera.

## <a name="using-hello-azure-cli"></a>Przy użyciu hello wiersza polecenia platformy Azure

Witaj interfejsu wiersza polecenia Azure zawiera polecenia do tworzenia i zarządzania kontenerami w wystąpień kontenera platformy Azure. Jeśli określisz prywatnej obraz powitania `create` polecenia, można również określić hello obrazu rejestru wymagane jest hasło tooauthenticate z rejestru kontenera hello.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Witaj `create` polecenia również obsługuje określanie hello `registry-login-server` i `registry-username`. Jednak serwer logowania hello hello rejestru kontenera Azure jest zawsze *registryname*. azurecr.io i hello domyślna nazwa użytkownika to *registryname*, więc te wartości są wywnioskować na podstawie nazwy obraz powitania, jeśli nie zostało podane.

## <a name="using-an-azure-resource-manager-template"></a>Przy użyciu szablonu usługi Azure Resource Manager

Możesz określić właściwości hello rejestracji kontenera Azure w szablonie usługi Azure Resource Manager, umieszczając w niej hello `imageRegistryCredentials` właściwości w definicji grupy kontenera hello:

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid przechowywania hasła rejestru kontenera bezpośrednio w szablonie hello, firma Microsoft zaleca, zapisz go jako klucza tajnego w [usługi Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) i odwołaj się w szablonie hello przy użyciu hello [natywna integracja pomiędzy usługą Witaj usługi Azure Resource Manager i usługi Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>Przy użyciu hello portalu Azure

Jeśli obsługa obrazów kontenera w hello rejestru kontenera platformy Azure, można łatwo utworzyć kontener w wystąpień kontenera Azure za pomocą hello portalu Azure.

1. W hello portalu Azure Przejdź tooyour kontenera rejestru.

2. Wybierz repozytoriów.

    ![menu rejestru kontenera Azure Hello hello portalu Azure][acr-menu]

3. Wybierz hello repozytorium, który ma toodeploy z.

4. Kliknij prawym przyciskiem myszy hello tag obrazu kontenera hello ma toodeploy.

    ![Menu kontekstowe dla uruchamiania kontener z wystąpień kontenera platformy Azure][acr-runinstance-contextmenu]

5. Wprowadź nazwę kontenera hello i nazwę grupy zasobów hello. W razie potrzeby można również zmienić hello wartości domyślne.

    ![Tworzenie menu dla wystąpień kontenera platformy Azure][acr-create-deeplink]

6. Po zakończeniu wdrażania hello można przechodzić toohello kontenera grupy z toofind okienko powiadomień hello adresu IP i inne właściwości.

    ![Widok szczegółów grupy kontener wystąpień kontenera platformy Azure][aci-detailsview]

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak kontenery toobuild wypchniesz tooa Kontener prywatny rejestru i wdrażać je wystąpień kontenera tooAzure przez [Ukończenie samouczka hello](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
