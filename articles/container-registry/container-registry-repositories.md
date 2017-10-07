---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repozytoria rejestru kontenera platformy Azure

Rejestru kontenera platformy Azure pozwala toostore kontener obrazów w repozytoriów. Dzięki przechowywaniu obrazów w repozytoriów, może mieć grup obrazów (lub wersji obrazów) w izolowanym środowisku. Po naciśnięciu rejestru tooyour obrazów, można określić te repozytoriów.


## <a name="prerequisites"></a>Wymagania wstępne
* **Usługa Azure Container Registry** — Tworzy rejestr kontenera w subskrypcji platformy Azure. Na przykład użyć hello [portalu Azure](container-registry-get-started-portal.md) lub hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).
* **Interfejs wiersza polecenia docker** -tooset komputera lokalnego jako Docker dostępu i host hello Docker polecenia interfejsu wiersza polecenia, zainstaluj [aparatem platformy Docker](https://docs.docker.com/engine/installation/).
* **Ściąganie obrazu** — ściąganie obrazu z publicznego rejestru Centrum Docker hello tagu go i wypchnąć go tooyour rejestru. Aby uzyskać wskazówki dotyczące wypychania i ściągania obrazów, zobacz [Docker wypychania obrazu tooAzure prywatnej rejestru](container-registry-get-started-docker-cli.md).


## <a name="viewing-repositories-in-hello-portal"></a>Wyświetlanie repozytoria w hello portalu

Po ma przypisany rejestru kontenera tooyour obrazów, można wyświetlić listę repozytoria hello hosting hello obrazów w hello portalu Azure.

Po wykonaniu kroków hello hello [Push Docker obrazu tooAzure prywatnej rejestru](container-registry-get-started-docker-cli.md) artykułu, po wykonaniu obrazu Nginx w rejestrze kontenera. W ramach instrukcji hello należy określić przestrzeń nazw dla obrazu hello. W poniższym przykładzie hello polecenie hello wypchnięcia hello NGinx obrazu toohello "Przykłady" repozytorium:

```
docker push myregistry.azurecr.io/samples/nginx
```
 Usługa Azure Container Registry obsługuje wielopoziomowe przestrzenie nazw repozytoriów. Ta funkcja umożliwia możesz toogroup kolekcje tooa powiązanych obrazy specyficzne dla aplikacji, lub zbiór aplikacji toospecific rozwoju lub zespołów operacyjnych. Zobacz tooread więcej informacji na temat repozytoria w rejestrach kontenera [rejestrów kontenera prywatnego Docker na platformie Azure](container-registry-intro.md).

repozytoria tooview hello kontenera rejestru:

1. Zaloguj się za toohello portalu Azure
2. Na powitania **rejestru kontenera Azure** bloku, wybierz hello rejestru chcesz tooinspect
3. W bloku rejestru powitania kliknij **repozytoria** toosee listę wszystkich repozytoriów hello i obrazów
4. (Opcjonalnie) Wybierz tagi toosee określonego obrazu

![Repozytoria w portalu hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a>Następne kroki
Teraz znasz podstawy hello, wszystko jest gotowe toostart za pomocą rejestru! Na przykład rozpocząć wdrażanie kontenera obrazy tooan [usługi kontenera platformy Azure](https://azure.microsoft.com/documentation/services/container-service/) klastra.
