---
title: Rejestry organizacji kontenera Docker aaaPrivate na platformie Azure | Dokumentacja firmy Microsoft
description: "Zarządzane toohello wprowadzenie usługa Rejestr kontenera platformy Azure, zapewniając oparte na chmurze prywatnej rejestrów Docker."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Rejestry organizacji IANA wprowadzenie tooprivate Docker kontenera


Rejestru kontenera platformy Azure jest zarządzanego [rejestru Docker](https://docs.docker.com/registry/) usługi na podstawie hello 2.0 rejestru Docker open source. Tworzenie i obsługa toostore rejestrów kontenera platformy Azure i zarządzanie nimi sieci prywatnej [kontenera Docker](https://www.docker.com/what-docker) obrazów. Kontener rejestrów na platformie Azure za pomocą istniejącego kontenera projektowania i wdrażania potoki i rysowanie w treści hello specjalizacji społeczności Docker.

Aby uzyskać ogólne informacje o platformie Docker i kontenerach, zobacz:

* [Docker user guide](https://docs.docker.com/engine/userguide/) (Podręcznik użytkownika platformy Docker)




## <a name="use-cases"></a>Przypadki zastosowań
Ściąganie obrazów z kontenera Azure celów wdrożenia toovarious rejestru:

* **Skalowalne systemy organizowania** zarządzające konteneryzowanymi aplikacjami w klastrach hostów, włączając w to rozwiązania [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) i [Kubernetes](http://kubernetes.io/docs/).
* **Usługi platformy Azure** obsługujące kompilowanie i uruchamianie aplikacji na dużą skalę, w tym usługi [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) i inne.

Deweloperzy mogą również push tooa kontenera rejestru jako część przepływu pracy tworzenia kontenera. Na przykład mogą kierować dane do rejestru kontenerów z poziomu narzędzia integracji ciągłej lub narzędzia do wdrażania, takiego jak usługa [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) lub [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Kluczowe pojęcia
* **Rejestr** — utwórz przynajmniej jeden rejestr kontenerów w subskrypcji platformy Azure. Każdy rejestru nie jest obsługiwana przez standardowe Azure [konta magazynu](../storage/common/storage-introduction.md) w hello tej samej lokalizacji. Korzystać z magazynu lokalnego, zamknij sieci obrazów kontenera przez utworzenie rejestru w hello tej samej lokalizacji platformy Azure jako wdrożeń. Nazwa FQDN rejestru ma formy hello `myregistry.azurecr.io`.

  Możesz [kontroli dostępu](container-registry-authentication.md) tooa kontenera rejestru za pomocą usługi Azure Active Directory kopią zapasową [nazwy głównej usługi](../active-directory/active-directory-application-objects.md) lub konto administratora podana. Uruchom hello standardowe `docker login` tooauthenticate polecenie z rejestru.

* **Rejestr zarządzany** — warstwa, która oferuje dodatkowe możliwości dla rejestrów w ramach trzech jednostek SKU — Podstawowej, Standardowej i Premium. obrazy Hello w tych jednostki SKU są przechowywane na kontach magazynu zarządzanych przez hello usługi rejestrów kontenera platformy Azure, co zwiększa niezawodność i umożliwia korzystanie z nowych funkcji. Nowe możliwości obejmują integrację elementów webhook, uwierzytelnianie repozytorium za pomocą usługi Azure Active Directory oraz obsługę funkcji usuwania. Użytkownicy mają toochoose opcji hello między rejestrów zarządzanych lub toocreate rejestru obsługiwanej przez swoje własne konta magazynu podczas tworzenia rejestrów.

* **Repozytorium** — rejestr zawiera przynajmniej jedno repozytorium stanowiące grupę obrazów kontenerów. Usługa Azure Container Registry obsługuje wielopoziomowe przestrzenie nazw repozytoriów. Ta funkcja umożliwia możesz toogroup kolekcje tooa powiązanych obrazy specyficzne dla aplikacji, lub zbiór aplikacji toospecific rozwoju lub zespołów operacyjnych. Na przykład:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` reprezentuje obraz całej firmy
  * `myregistry.azurecr.io/warrantydept/dotnet-build`reprezentuje obraz używany aplikacji .NET toobuild, współużytkowana przez dział gwarancji hello
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`reprezentuje obraz sieci web są pogrupowane w powitania klienta przesyłanie aplikacji, należących do działu gwarancji hello

* **Obraz** — każdy obraz jest przechowywany w repozytorium i jest migawką tylko do odczytu kontenera platformy Docker. Rejestry kontenerów platformy Azure mogą obejmować zarówno obrazy systemu Windows, jak i Linux. Możesz kontrolować nazwy obrazów wszystkich wdrożeń kontenera. Użyj standardowego [polecenia Docker](https://docs.docker.com/engine/reference/commandline/) toopush obrazów do repozytorium lub ściągania obrazu z repozytorium.

* **Kontener** — mianem kontenera określa się aplikację wraz z jej zależnościami, opakowaną w kompletny system plików, włączając w to kod, środowisko uruchomieniowe, narzędzia systemowe i biblioteki. Uruchom kontenery platformy Docker w oparciu o obrazy systemu Windows lub Linux, które zostały ściągnięte z rejestru kontenerów. Kontenery uruchomione na jednym komputerze udostępnianie hello jądra systemu operacyjnego. Kontenery docker są tooall pełni dostosowane głównych dystrybucjach systemu Linux, Mac i systemu Windows.




## <a name="next-steps"></a>Następne kroki
* [Tworzenie kontenera rejestru przy użyciu hello portalu Azure](container-registry-get-started-portal.md)
* [Tworzenie kontenera rejestru przy użyciu hello Azure CLI](container-registry-get-started-azure-cli.md)
* [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
* toobuild ciągłej integracji i przepływ pracy wdrażania przy użyciu programu Visual Studio Team Services, usługi kontenera platformy Azure i rejestru kontenera platformy Azure, zobacz [w tym samouczku](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Tooset zapasową własne Docker prywatnej rejestru na platformie Azure (bez publicznego punktu końcowego), zobacz [wdrażanie swój własny prywatnej Docker rejestru na platformie Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
