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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="50252-103">Zarządzanie aplikacją usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="50252-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="50252-104">Dowiedz się, jak tworzyć i usuwać aplikacje, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="50252-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50252-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="50252-105">Prerequisites</span></span>

* <span data-ttu-id="50252-106">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="50252-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="50252-107">Następnie wybierz klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="50252-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="50252-108">Aby uzyskać więcej informacji, zobacz [wprowadzenie Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="50252-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="50252-109">Ma gotowa do wdrożenia pakietu aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="50252-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="50252-110">Aby uzyskać więcej informacji o sposobie pakiet aplikacji i autor, przeczytaj o [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="50252-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="50252-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="50252-111">Overview</span></span>

<span data-ttu-id="50252-112">Aby wdrożyć nową aplikację, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="50252-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="50252-113">Przekaż pakiet aplikacji do magazynu obrazów platformy Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="50252-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="50252-114">Udostępnianie typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-114">Provision an application type.</span></span>
3. <span data-ttu-id="50252-115">Określ i tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-115">Specify and create an application.</span></span>
4. <span data-ttu-id="50252-116">Określ i utworzyć usług.</span><span class="sxs-lookup"><span data-stu-id="50252-116">Specify and create services.</span></span>

<span data-ttu-id="50252-117">Aby usunąć istniejącą aplikację, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="50252-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="50252-118">Usuń aplikację.</span><span class="sxs-lookup"><span data-stu-id="50252-118">Delete the application.</span></span>
2. <span data-ttu-id="50252-119">Typ aplikacji skojarzone wstrzymał obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="50252-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="50252-120">Usuń zawartość magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="50252-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="50252-121">Wdrażanie nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="50252-121">Deploy a new application</span></span>

<span data-ttu-id="50252-122">Aby wdrożyć nową aplikację, należy wykonać następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="50252-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="50252-123">Przekaż nowy pakiet aplikacji do magazynu obrazów</span><span class="sxs-lookup"><span data-stu-id="50252-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="50252-124">Przed utworzeniem aplikacji, przekaż pakiet aplikacji do magazynu obrazów platformy Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="50252-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="50252-125">Na przykład, jeśli pakiet aplikacji jest w `app_package_dir` katalogu, użyj następujących poleceń do przekazania katalogu:</span><span class="sxs-lookup"><span data-stu-id="50252-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="50252-126">W przypadku dużych pakietów aplikacji, można określić `--show-progress` opcję, aby wyświetlić postęp przekazywania.</span><span class="sxs-lookup"><span data-stu-id="50252-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="50252-127">Typ aplikacji do udostępniania</span><span class="sxs-lookup"><span data-stu-id="50252-127">Provision the application type</span></span>

<span data-ttu-id="50252-128">Po zakończeniu przekazywania udostępnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="50252-129">Aby zainicjować obsługę aplikacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="50252-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="50252-130">Wartość `application-type-build-path` jest nazwę katalogu, w którym przekazać pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="50252-131">Utworzenie aplikacji na podstawie typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="50252-131">Create an application from an application type</span></span>

<span data-ttu-id="50252-132">Po udostępnieniem aplikacji użyj następującego polecenia, aby utworzyć aplikację:</span><span class="sxs-lookup"><span data-stu-id="50252-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="50252-133">`app-name`jest to nazwa, który ma być używany dla danego wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="50252-134">W manifeście aplikacji poprzednio udostępnione można uzyskać dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="50252-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="50252-135">Nazwa aplikacji musi rozpoczynać się od prefiksu `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="50252-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="50252-136">Tworzenie usługi dla nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="50252-136">Create services for the new application</span></span>

<span data-ttu-id="50252-137">Po utworzeniu aplikacji, należy utworzyć usług z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="50252-138">W poniższym przykładzie utworzymy nowe usługi bezstanowej z naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="50252-139">Usługi, które można utworzyć na podstawie aplikacji są definiowane w manifestu usługi, w pakiecie aplikacji wcześniej zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="50252-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="50252-140">Sprawdź wdrożenie aplikacji i kondycji</span><span class="sxs-lookup"><span data-stu-id="50252-140">Verify application deployment and health</span></span>

<span data-ttu-id="50252-141">Aby potwierdzić, że aplikacja i usługi zostały pomyślnie wdrożone, sprawdź, czy wymienione są aplikacji i usług:</span><span class="sxs-lookup"><span data-stu-id="50252-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="50252-142">Aby sprawdzić, czy usługa jest w dobrej kondycji, należy użyć poleceń podobne do pobrania kondycji usługi i aplikacji:</span><span class="sxs-lookup"><span data-stu-id="50252-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="50252-143">Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.</span><span class="sxs-lookup"><span data-stu-id="50252-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="50252-144">Usuń istniejącą aplikację</span><span class="sxs-lookup"><span data-stu-id="50252-144">Remove an existing application</span></span>

<span data-ttu-id="50252-145">Aby usunąć aplikację, należy wykonać następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="50252-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="50252-146">Usuń aplikację</span><span class="sxs-lookup"><span data-stu-id="50252-146">Delete the application</span></span>

<span data-ttu-id="50252-147">Aby usunąć aplikację, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="50252-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="50252-148">Cofnij aprowizację typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="50252-148">Unprovision the application type</span></span>

<span data-ttu-id="50252-149">Po usunięciu aplikacji można anulować udostępnienia typ aplikacji, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="50252-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="50252-150">Wstrzymał obsługi administracyjnej typ aplikacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="50252-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="50252-151">Nazwa typu i wersji typu muszą być zgodne, nazwa i wersja w manifeście aplikacji wcześniej zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="50252-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="50252-152">Usuwanie pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="50252-152">Delete the application package</span></span>

<span data-ttu-id="50252-153">Po ma anulował udostępnianie typ aplikacji, można usunąć pakiet aplikacji w magazynie obrazów, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="50252-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="50252-154">Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="50252-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="50252-155">Aby usunąć pakiet aplikacji w sklepie obrazu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="50252-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="50252-156">`content-path`musi być nazwą katalogu, który został przekazany podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50252-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="50252-157">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="50252-157">Related articles</span></span>

* [<span data-ttu-id="50252-158">Usługa Service Fabric i interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="50252-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* <span data-ttu-id="50252-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="50252-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
