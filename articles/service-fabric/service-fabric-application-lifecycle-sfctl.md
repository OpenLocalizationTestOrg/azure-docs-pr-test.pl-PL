---
title: "aaaManage sieć szkieletowa usług Azure aplikacji przy użyciu interfejsu wiersza polecenia Azure Service Fabric"
description: "Dowiedz się, jak toodeploy i usunięcie aplikacji z usługi Azure Service Fabric klastra przy użyciu interfejsu wiersza polecenia Azure Service Fabric"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Zarządzanie aplikacją sieci szkieletowej usług Azure przy użyciu interfejsu wiersza polecenia Azure Service Fabric

Dowiedz się, jak toocreate i usuwania aplikacji, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.

## <a name="prerequisites"></a>Wymagania wstępne

* Instalowanie usługi sieci szkieletowej interfejsu wiersza polecenia. Następnie wybierz klaster sieci szkieletowej usług. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md).

* Ma sieci szkieletowej usług aplikacji pakietu gotowe toobe wdrożone. Aby uzyskać więcej informacji o tym, jak tooauthor i pakietu aplikacji, przeczytaj o hello [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).

## <a name="overview"></a>Omówienie

toodeploy nowej aplikacji, wykonaj następujące kroki:

1. Przekaż pakiet toohello sieci szkieletowej usług obrazu sklepu z aplikacjami.
2. Udostępnianie typu aplikacji.
3. Określ i tworzenia aplikacji.
4. Określ i utworzyć usług.

tooremove istniejącej aplikacji, wykonaj następujące kroki:

1. Usunięcie aplikacji hello.
2. Cofnij aprowizację hello skojarzony typ aplikacji.
3. Usuń zawartość magazynu obraz powitania.

## <a name="deploy-a-new-application"></a>Wdrażanie nowej aplikacji

toodeploy nowej aplikacji hello pełną następujące zadania:

### <a name="upload-a-new-application-package-toohello-image-store"></a>Przekaż nowy magazyn obrazu toohello pakietu aplikacji

Przed utworzeniem aplikacji, należy przekazać magazynu obrazów platformy Service Fabric toohello pakietu aplikacji hello.

Na przykład, jeśli pakiet aplikacji hello `app_package_dir` katalogu, hello Użyj następującego polecenia tooupload hello katalogu:

```azurecli
sfctl application upload --path ~/app_package_dir
```

W przypadku dużych pakietów aplikacji, można określić hello `--show-progress` opcję postęp hello toodisplay hello przekazywania.

### <a name="provision-hello-application-type"></a>Typ aplikacji hello udostępniania

Po zakończeniu przekazywania hello udostępnienia aplikacji hello. Aplikacja hello tooprovision, hello Użyj następującego polecenia:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

Witaj wartość `application-type-build-path` jest nazwą hello hello katalogu, gdzie możesz przekazać pakiet aplikacji.

### <a name="create-an-application-from-an-application-type"></a>Utworzenie aplikacji na podstawie typu aplikacji

Po udostępnieniem aplikacji hello, użyj następującego polecenia tooname hello i utworzyć aplikację:

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`jest nazwą hello mają toouse dla wystąpienia aplikacji hello. W manifeście aplikacji poprzednio udostępnione można uzyskać dodatkowe parametry.

Nazwa aplikacji Hello musi rozpoczynać się od prefiksu powitania `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Tworzenie usługi dla nowej aplikacji hello

Po utworzeniu aplikacji z aplikacji hello należy utworzyć usług. Poniższy przykład hello możemy utworzyć nowej usługi bezstanowej z naszej aplikacji. Hello usług, które można utworzyć na podstawie aplikacji są definiowane w w pakiecie poprzednio obsługiwaną aplikacji hello manifestu usługi.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Sprawdź wdrożenie aplikacji i kondycji

tooverify wszystko jest w dobrej kondycji, należy użyć następującego polecenia kondycji hello:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

podobnych poleceń tooretrieve hello kondycji hello usług i aplikacji, użyj tooverify hello usługi jest w dobrej kondycji:

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.

## <a name="remove-an-existing-application"></a>Usuń istniejącą aplikację

tooremove aplikacji hello pełną następujące zadania:

### <a name="delete-hello-application"></a>Usunięcie aplikacji hello

Aplikacja hello toodelete, hello Użyj następującego polecenia:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Wstrzymał obsługi administracyjnej typ aplikacji hello

Po usunięciu aplikacji hello można anulować udostępnienia typ aplikacji hello, jeśli nie są już potrzebne. Typ aplikacji hello toounprovision, hello Użyj następującego polecenia:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Typ Hello wersja nazwę i typ musi odpowiadać, hello nazwa i wersja w manifeście aplikacji poprzednio obsługiwaną hello.

### <a name="delete-hello-application-package"></a>Usuwanie pakietu aplikacji hello

Po ma anulował udostępnianie typ aplikacji hello, można usunąć pakietu aplikacji hello z magazynu obrazów hello, jeśli nie są już potrzebne. Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku. 

pakiet aplikacji hello toodelete z magazynu obrazów hello, hello Użyj następującego polecenia:

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`musi być nazwą hello hello katalogu, który został przekazany, po utworzeniu aplikacji hello.

## <a name="upgrade-application"></a>Uaktualnianie aplikacji

Po utworzeniu aplikacji, powtórz hello tego samego zestawu tooprovision czynności drugiego wersji aplikacji. Następnie Uaktualnianie aplikacji usługi Service Fabric może przejść toorunning hello druga wersja aplikacji hello. Aby uzyskać więcej informacji, zobacz dokumentację hello [uaktualnień aplikacji usługi sieć szkieletowa](service-fabric-application-upgrade.md).

tooperform uaktualniania pierwszego udostępniania hello następnej wersji przy użyciu aplikacji hello jak poprzednio hello tych samych poleceń:

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

Zalecane jest, a następnie tooperform monitorowanych automatyczne uaktualnianie uruchomienie uaktualnienia hello, uruchamiając następujące polecenie hello:

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

Uaktualnienia zastąpienie istniejących parametrów z dowolnego zestaw jest określony. Parametry aplikacji powinien zostać przekazany jako argumenty polecenia uaktualniania toohello, jeśli to konieczne. Parametry aplikacji powinien być kodowany jako obiekt JSON.

wcześniej określony tooretrieve żadnych parametrów, możesz użyć hello `sfctl application info` polecenia.

Podczas uaktualniania aplikacji jest w toku, stan hello można pobrać przy użyciu `sfctl application upgrade-status` polecenia.

Ponadto jeśli uaktualnianie jest w toku i musi toobe anulowane, można użyć hello `sfctl application upgrade-rollback` tooroll ponownie hello uaktualnienia.

## <a name="next-steps"></a>Następne kroki

* [Podstawy usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)
* [Wprowadzenie do korzystania z usługi Service Fabric w systemie Linux](service-fabric-get-started-linux.md)
* [Uruchamianie uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)
