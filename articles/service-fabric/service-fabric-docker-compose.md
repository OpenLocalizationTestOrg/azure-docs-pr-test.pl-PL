---
title: "Usługa sieci szkieletowej rozwiązania Docker Compose Podgląd aaaAzure"
description: "Sieć szkieletowa usług Azure akceptuje rozwiązania Docker Compose toomake format go łatwiejsze kontenery istniejących tooorchestrate przy użyciu sieci szkieletowej usług. Ta obsługa jest obecnie w przeglądzie."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Obsługa aplikacji Redaguj docker w sieci szkieletowej usług Azure (wersja zapoznawcza)

Docker używa hello [docker-compose.yml](https://docs.docker.com/compose) pliku do definiowania wielu kontenera aplikacji. toomake go łatwo klientów zapoznać się z Docker tooorchestrate istniejące aplikacje kontenera na sieć szkieletowa usług Azure, jest dostępna obsługa podglądu rozwiązania Docker Compose natywnie hello platformy. Sieć szkieletowa usług może zaakceptować wersji 3 lub nowszej `docker-compose.yml` plików. 

Ponieważ ta obsługa jest dostępna w wersji zapoznawczej, jest obsługiwana tylko podzestaw Redaguj dyrektywy. Na przykład nie są obsługiwane uaktualnienia aplikacji. Można zawsze usunąć i wdrażania aplikacji, a nie jej uaktualnienie.

toouse to podglądu, tworzenia klastra w wersji 5.7 lub nowszej środowiska uruchomieniowego platformy Service Fabric hello za pośrednictwem portalu Azure oraz hello odpowiadającego SDK hello. 

> [!NOTE]
> Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Wdrażanie rozwiązania Docker Compose pliku w sieci szkieletowej usług

Hello następujące polecenia Tworzenie aplikacji usługi Service Fabric (o nazwie `fabric:/TestContainerApp` w hello poprzedzających przykładzie), które można monitorować i zarządzać, takich jak innych aplikacji sieci szkieletowej usług. Można użyć nazwy określonej aplikacji hello dla zapytań o kondycję.

### <a name="use-powershell"></a>Korzystanie z programu PowerShell

Tworzenie aplikacji usługi sieci szkieletowej tworzą z plik docker-compose.yml, uruchamiając następujące polecenie w programie PowerShell hello:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`i `RegistryPassword` można znaleźć toohello kontenera rejestru użytkownika i hasło. Po zakończeniu aplikacji hello jej stan można sprawdzić za pomocą następującego polecenia hello:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

Witaj toodelete tworzenia aplikacji za pomocą programu PowerShell, hello Użyj następującego polecenia:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Użyj usługi sieci szkieletowej interfejsu wiersza polecenia Azure (sfctl)

Alternatywnie można użyć hello następujące polecenia interfejsu wiersza polecenia usługi sieci szkieletowej:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Po utworzeniu aplikacji hello jej stan można sprawdzić za pomocą następującego polecenia hello:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Witaj toodelete tworzenia aplikacji, należy użyć hello następujące polecenie:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Obsługiwane dyrektywy tworzenia

Ta wersja zapoznawcza obsługuje podzbiór hello opcji konfiguracji z formatu w wersji 3 Redaguj hello, w tym powitania po nim elementów podstawowych:

* Usługi > Wdrażanie > repliki
* Usługi > Wdrażanie > umieszczania > ograniczenia
* Usługi > Wdrażanie > Zasoby > limity
    * udziały procesorów
    * -pamięci
    * -pamięci-wymiany
* Usługi > poleceń
* Usługi > środowiska
* Usługi > portów
* Usługi > obrazu
* Usługi > izolację (tylko system Windows)
* Usługi > Rejestrowanie > sterownika
* Usługi > Rejestrowanie > sterownika > Opcje
* Wolumin & wdrażanie > woluminu

Konfigurowanie klastra hello wymuszania ograniczenia zasobów, zgodnie z opisem w [ładu zasobów sieci szkieletowej usług](service-fabric-resource-governance.md). Inne rozwiązania Docker Compose dyrektywy nie są obsługiwane dla tej wersji zapoznawczej.

## <a name="servicednsname-computation"></a>ServiceDnsName obliczeń

Jeśli nazwa usługi hello, określona w pliku tworzenia jest w pełni kwalifikowaną nazwą domeny (to znaczy zawiera kropkę [.]), nazwa DNS hello zarejestrowany przez sieć szkieletowa usług to `<ServiceName>` (w tym hello kropkę). Jeśli nie, każdy z segmentów ścieżki w nazwie aplikacji hello staje się etykietę domeny w hello nazwę DNS usługi, z hello pierwszy segment ścieżki staje się hello etykieta domeny najwyższego poziomu.

Na przykład jeśli hello określona nazwa aplikacji jest `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` byłoby hello zarejestrowanej nazwy DNS.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Różnice między Redaguj (wystąpienie definicji) i sieci szkieletowej usług modelu aplikacji (definicja typu)

Plik docker-compose.yml opisuje zestaw możliwych do wdrożenia kontenerów, łącznie z ich właściwości i konfiguracji.
Na przykład plik hello może zawierać zmienne środowiskowe i portów. Można również określić parametry wdrażania, takie jak ograniczenia dotyczące umieszczania, limity zasobów i nazwy DNS w plik docker-compose.yml hello.

Witaj [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) używa typów usługi oraz typy aplikacji, gdzie masz wiele wystąpień aplikacji hello tego samego typu. Na przykład można mieć jedno wystąpienie aplikacji na klienta. Ten model na podstawie typu obsługuje wiele wersji hello tego samego typu aplikacji zarejestrowanej hello w czasie wykonywania.

Na przykład klienta A może mieć utworzyć wystąpienia typu 1.0 AppTypeA aplikacji, a klient B może mieć inna aplikacja hello utworzono wystąpienie tego samego typu i wersji. Zdefiniuj typy aplikacji hello w manifestach aplikacji hello oraz określić parametry nazwy i wdrażania aplikacji hello podczas tworzenia aplikacji hello.

Chociaż ten model zapewnia elastyczność, firma Microsoft są także planowania toosupport gdy typy są niejawne z pliku manifestu hello model wdrożenia prostszy, na podstawie wystąpienia. W tym modelu każda aplikacja uzyskuje niezależne manifeście. Firma Microsoft przeglądania tym wysiłku przez dodanie obsługi docker-compose.yml, który jest formatem wdrożenia na podstawie wystąpienia.

## <a name="next-steps"></a>Następne kroki

* Przeczytana hello [modelu aplikacji sieci szkieletowej usług](service-fabric-application-model.md)
* [Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)
