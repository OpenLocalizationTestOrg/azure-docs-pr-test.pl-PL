---
title: "aplikacje sieci szkieletowej usług Azure aaaManage używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
description: "Dowiedz się, jak toodeploy i usunięcie aplikacji z usługi Azure Service Fabric klastra przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Zarządzanie aplikacją usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0

Dowiedz się, jak toocreate i usuwania aplikacji, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.

## <a name="prerequisites"></a>Wymagania wstępne

* Zainstaluj interfejs wiersza polecenia platformy Azure 2.0. Następnie wybierz klaster sieci szkieletowej usług. Aby uzyskać więcej informacji, zobacz [wprowadzenie Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

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

toodeploy nowej aplikacji hello pełną następujące zadania.

### <a name="upload-a-new-application-package-toohello-image-store"></a>Przekaż nowy magazyn obrazu toohello pakietu aplikacji

Przed utworzeniem aplikacji, należy przekazać magazynu obrazów platformy Service Fabric toohello pakietu aplikacji hello. 

Na przykład, jeśli pakiet aplikacji hello `app_package_dir` katalogu, hello Użyj następującego polecenia tooupload hello katalogu:

```azurecli
az sf application upload --path ~/app_package_dir
```

W przypadku dużych pakietów aplikacji, można określić hello `--show-progress` opcję postęp hello toodisplay hello przekazywania.

### <a name="provision-hello-application-type"></a>Typ aplikacji hello udostępniania

Po zakończeniu przekazywania hello udostępnienia aplikacji hello. Aplikacja hello tooprovision, hello Użyj następującego polecenia:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Witaj wartość `application-type-build-path` jest nazwą hello hello katalogu, gdzie możesz przekazać pakiet aplikacji.

### <a name="create-an-application-from-an-application-type"></a>Utworzenie aplikacji na podstawie typu aplikacji

Po udostępnieniem aplikacji hello, użyj następującego polecenia tooname hello i utworzyć aplikację:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`jest nazwą hello mają toouse dla wystąpienia aplikacji hello. Możesz pobrać ze strony manifest aplikacji poprzednio obsługiwaną hello dodatkowe parametry.

Nazwa aplikacji Hello musi rozpoczynać się od prefiksu powitania `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Tworzenie usługi dla nowej aplikacji hello

Po utworzeniu aplikacji z aplikacji hello należy utworzyć usług. Poniższy przykład hello możemy utworzyć nowej usługi bezstanowej z naszej aplikacji. Hello usług, które można utworzyć na podstawie aplikacji są definiowane w w pakiecie poprzednio obsługiwaną aplikacji hello manifestu usługi.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Sprawdź wdrożenie aplikacji i kondycji

tooverify, że aplikacja i usługi zostały pomyślnie wdrożone, sprawdź, czy aplikacji hello i usługi są wyświetlane:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

podobnych poleceń tooretrieve hello kondycji hello usług i aplikacji hello należy użyć tooverify hello usługi jest w dobrej kondycji:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.

## <a name="remove-an-existing-application"></a>Usuń istniejącą aplikację

tooremove aplikacji hello pełną następujące zadania.

### <a name="delete-hello-application"></a>Usunięcie aplikacji hello

Aplikacja hello toodelete, hello Użyj następującego polecenia:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Wstrzymał obsługi administracyjnej typ aplikacji hello

Po usunięciu aplikacji hello można anulować udostępnienia typ aplikacji hello, jeśli nie są już potrzebne. Typ aplikacji hello toounprovision, hello Użyj następującego polecenia:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Typ Hello wersja nazwę i typ musi odpowiadać, hello nazwa i wersja w manifeście aplikacji poprzednio obsługiwaną hello.

### <a name="delete-hello-application-package"></a>Usuwanie pakietu aplikacji hello

Po ma anulował udostępnianie typ aplikacji hello, można usunąć pakietu aplikacji hello z magazynu obrazów hello, jeśli nie są już potrzebne. Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku. 

pakiet aplikacji hello toodelete z magazynu obrazów hello, hello Użyj następującego polecenia:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`musi być nazwą hello hello katalogu, który został przekazany, po utworzeniu aplikacji hello.

## <a name="related-articles"></a>Pokrewne artykuły:

* [Usługa Service Fabric i interfejs wiersza polecenia platformy Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)
