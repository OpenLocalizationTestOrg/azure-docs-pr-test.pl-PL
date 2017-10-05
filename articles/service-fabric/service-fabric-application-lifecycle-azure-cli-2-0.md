---
title: "Zarządzanie aplikacjami sieć szkieletowa usług Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0"
description: "Dowiedz się, jak wdrożyć i usuwać aplikacje z klastra usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>Zarządzanie aplikacją usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0

Dowiedz się, jak tworzyć i usuwać aplikacje, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.

## <a name="prerequisites"></a>Wymagania wstępne

* Zainstaluj interfejs wiersza polecenia platformy Azure 2.0. Następnie wybierz klaster sieci szkieletowej usług. Aby uzyskać więcej informacji, zobacz [wprowadzenie Azure CLI 2.0](service-fabric-azure-cli-2-0.md).

* Ma gotowa do wdrożenia pakietu aplikacji sieci szkieletowej usług. Aby uzyskać więcej informacji o sposobie pakiet aplikacji i autor, przeczytaj o [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).

## <a name="overview"></a>Omówienie

Aby wdrożyć nową aplikację, wykonaj następujące kroki:

1. Przekaż pakiet aplikacji do magazynu obrazów platformy Service Fabric.
2. Udostępnianie typu aplikacji.
3. Określ i tworzenia aplikacji.
4. Określ i utworzyć usług.

Aby usunąć istniejącą aplikację, wykonaj następujące kroki:

1. Usuń aplikację.
2. Typ aplikacji skojarzone wstrzymał obsługi administracyjnej.
3. Usuń zawartość magazynu obrazów.

## <a name="deploy-a-new-application"></a>Wdrażanie nowej aplikacji

Aby wdrożyć nową aplikację, należy wykonać następujące zadania.

### <a name="upload-a-new-application-package-to-the-image-store"></a>Przekaż nowy pakiet aplikacji do magazynu obrazów

Przed utworzeniem aplikacji, przekaż pakiet aplikacji do magazynu obrazów platformy Service Fabric. 

Na przykład, jeśli pakiet aplikacji jest w `app_package_dir` katalogu, użyj następujących poleceń do przekazania katalogu:

```azurecli
az sf application upload --path ~/app_package_dir
```

W przypadku dużych pakietów aplikacji, można określić `--show-progress` opcję, aby wyświetlić postęp przekazywania.

### <a name="provision-the-application-type"></a>Typ aplikacji do udostępniania

Po zakończeniu przekazywania udostępnienia aplikacji. Aby zainicjować obsługę aplikacji, użyj następującego polecenia:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

Wartość `application-type-build-path` jest nazwę katalogu, w którym przekazać pakiet aplikacji.

### <a name="create-an-application-from-an-application-type"></a>Utworzenie aplikacji na podstawie typu aplikacji

Po udostępnieniem aplikacji użyj następującego polecenia, aby utworzyć aplikację:

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`jest to nazwa, który ma być używany dla danego wystąpienia aplikacji. W manifeście aplikacji poprzednio udostępnione można uzyskać dodatkowe parametry.

Nazwa aplikacji musi rozpoczynać się od prefiksu `fabric:/`.

### <a name="create-services-for-the-new-application"></a>Tworzenie usługi dla nowej aplikacji

Po utworzeniu aplikacji, należy utworzyć usług z aplikacji. W poniższym przykładzie utworzymy nowe usługi bezstanowej z naszej aplikacji. Usługi, które można utworzyć na podstawie aplikacji są definiowane w manifestu usługi, w pakiecie aplikacji wcześniej zainicjowana.

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Sprawdź wdrożenie aplikacji i kondycji

Aby potwierdzić, że aplikacja i usługi zostały pomyślnie wdrożone, sprawdź, czy wymienione są aplikacji i usług:

```azurecli
az sf application list
az sf service list --application-list TestApp
```

Aby sprawdzić, czy usługa jest w dobrej kondycji, należy użyć poleceń podobne do pobrania kondycji usługi i aplikacji:

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.

## <a name="remove-an-existing-application"></a>Usuń istniejącą aplikację

Aby usunąć aplikację, należy wykonać następujące zadania.

### <a name="delete-the-application"></a>Usuń aplikację

Aby usunąć aplikację, użyj następującego polecenia:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a>Cofnij aprowizację typu aplikacji

Po usunięciu aplikacji można anulować udostępnienia typ aplikacji, jeśli nie są już potrzebne. Wstrzymał obsługi administracyjnej typ aplikacji, użyj następującego polecenia:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Nazwa typu i wersji typu muszą być zgodne, nazwa i wersja w manifeście aplikacji wcześniej zainicjowana.

### <a name="delete-the-application-package"></a>Usuwanie pakietu aplikacji

Po ma anulował udostępnianie typ aplikacji, można usunąć pakiet aplikacji w magazynie obrazów, jeśli nie są już potrzebne. Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku. 

Aby usunąć pakiet aplikacji w sklepie obrazu, użyj następującego polecenia:

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`musi być nazwą katalogu, który został przekazany podczas tworzenia aplikacji.

## <a name="related-articles"></a>Pokrewne artykuły:

* [Usługa Service Fabric i interfejs wiersza polecenia platformy Azure 2.0](service-fabric-azure-cli-2-0.md)
* [Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)
