---
title: "Usługa Azure sieci szkieletowej z rozwiązania Docker Compose podglądu"
description: "Sieć szkieletowa usług Azure akceptuje rozwiązania Docker Compose format, aby ułatwić organizowania istniejących kontenerów przy użyciu sieci szkieletowej usług. Ta obsługa jest obecnie w przeglądzie."
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
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Obsługa aplikacji Redaguj docker w sieci szkieletowej usług Azure (wersja zapoznawcza)

Używa docker [docker-compose.yml](https://docs.docker.com/compose) pliku do definiowania wielu kontenera aplikacji. Aby ułatwić klientom zapoznać się z rozwiązaniem Docker do organizowania istniejących aplikacji kontenera na sieć szkieletowa usług Azure, firma Microsoft wprowadzono obsługę podglądu rozwiązania Docker Compose natywnie przez platformę. Sieć szkieletowa usług może zaakceptować wersji 3 lub nowszej `docker-compose.yml` plików. 

Ponieważ ta obsługa jest dostępna w wersji zapoznawczej, jest obsługiwana tylko podzestaw Redaguj dyrektywy. Na przykład nie są obsługiwane uaktualnienia aplikacji. Można zawsze usunąć i wdrażania aplikacji, a nie jej uaktualnienie.

Aby korzystać z tej wersji zapoznawczej, tworzenia klastra w wersji 5.7 lub nowszej środowiska uruchomieniowego platformy Service Fabric za pośrednictwem portalu Azure oraz odpowiedniego zestawu SDK. 

> [!NOTE]
> Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Wdrażanie rozwiązania Docker Compose pliku w sieci szkieletowej usług

Następujące polecenia Utwórz aplikację usługi sieć szkieletowa (o nazwie `fabric:/TestContainerApp` w poprzednim przykładzie), które można monitorować i zarządzać, takich jak innych aplikacji sieci szkieletowej usług. Określona nazwa aplikacji dla zapytań o kondycję można użyć.

### <a name="use-powershell"></a>Korzystanie z programu PowerShell

Tworzenie aplikacji usługi sieci szkieletowej tworzą z plik docker-compose.yml, uruchamiając następujące polecenie w programie PowerShell:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`i `RegistryPassword` odwoływać się do kontenera rejestru nazwy i hasła użytkownika. Po zakończeniu aplikacji jej stan można sprawdzić za pomocą następującego polecenia:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

Aby usunąć tworzenia aplikacji za pomocą programu PowerShell, użyj następującego polecenia:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Użyj usługi sieci szkieletowej interfejsu wiersza polecenia Azure (sfctl)

Można również można użyć następującego polecenia interfejsu wiersza polecenia usługi sieci szkieletowej:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Po utworzeniu aplikacji jej stan można sprawdzić za pomocą następującego polecenia:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Aby usunąć tworzenia aplikacji, użyj następującego polecenia:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Obsługiwane dyrektywy tworzenia

Ta wersja zapoznawcza obsługuje podzbiór z formatu Redaguj w wersji 3, w tym następujące elementy podstawowe opcje konfiguracji:

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

Konfigurowanie klastra na potrzeby wymuszania ograniczenia zasobów, zgodnie z opisem w [ładu zasobów sieci szkieletowej usług](service-fabric-resource-governance.md). Inne rozwiązania Docker Compose dyrektywy nie są obsługiwane dla tej wersji zapoznawczej.

## <a name="servicednsname-computation"></a>ServiceDnsName obliczeń

Jeśli nazwa usługi określona w pliku tworzenia jest w pełni kwalifikowaną nazwą domeny (to znaczy zawiera kropkę [.]), nazwa DNS zarejestrowane przez sieć szkieletowa usług to `<ServiceName>` (w tym kropki (.)). Jeśli nie, każdy z segmentów ścieżki w nazwie aplikacji staje się etykieta domeny, w polu Nazwa DNS usługi z pierwszy segment ścieżki, staje się etykieta domeny najwyższego poziomu.

Na przykład, jeśli określona nazwa aplikacji jest `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` byłoby zarejestrowanej nazwy DNS.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Różnice między Redaguj (wystąpienie definicji) i sieci szkieletowej usług modelu aplikacji (definicja typu)

Plik docker-compose.yml opisuje zestaw możliwych do wdrożenia kontenerów, łącznie z ich właściwości i konfiguracji.
Na przykład plik może zawierać zmienne środowiskowe i portów. Można również określić parametry wdrażania, takie jak ograniczenia dotyczące umieszczania, limity zasobów i nazwy DNS w plik docker-compose.yml.

[Model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) używa usługi typy i aplikacji, gdzie masz wiele wystąpień aplikacji tego samego typu. Na przykład można mieć jedno wystąpienie aplikacji na klienta. Ten model na podstawie typu obsługuje wiele wersji tego samego typu aplikacji, który został zarejestrowany za pomocą środowiska uruchomieniowego.

Na przykład klient A może mieć utworzyć wystąpienia typu 1.0 AppTypeA aplikacji, a klient B może mieć inną aplikację utworzone z tego samego typu i wersji. Definiowanie typów aplikacji w manifestach aplikacji i określić parametry nazwy i wdrażania aplikacji, podczas tworzenia aplikacji.

Chociaż ten model zapewnia elastyczność, będziemy również planowania obsługi modelu wdrażania prostszy, na podstawie wystąpienia, których typy są niejawne z pliku manifestu. W tym modelu każda aplikacja uzyskuje niezależne manifeście. Firma Microsoft przeglądania tym wysiłku przez dodanie obsługi docker-compose.yml, który jest formatem wdrożenia na podstawie wystąpienia.

## <a name="next-steps"></a>Następne kroki

* Przeczytaj na [modelu aplikacji sieci szkieletowej usług](service-fabric-application-model.md)
* [Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)
