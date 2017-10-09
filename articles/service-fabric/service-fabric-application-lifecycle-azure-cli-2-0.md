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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="6291f-103">Zarządzanie aplikacją usługi sieć szkieletowa usług Azure przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="6291f-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="6291f-104">Dowiedz się, jak toocreate i usuwania aplikacji, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="6291f-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6291f-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6291f-105">Prerequisites</span></span>

* <span data-ttu-id="6291f-106">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="6291f-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="6291f-107">Następnie wybierz klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6291f-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="6291f-108">Aby uzyskać więcej informacji, zobacz [wprowadzenie Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="6291f-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="6291f-109">Ma sieci szkieletowej usług aplikacji pakietu gotowe toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6291f-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="6291f-110">Aby uzyskać więcej informacji o tym, jak tooauthor i pakietu aplikacji, przeczytaj o hello [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="6291f-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="6291f-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6291f-111">Overview</span></span>

<span data-ttu-id="6291f-112">toodeploy nowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6291f-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="6291f-113">Przekaż pakiet toohello sieci szkieletowej usług obrazu sklepu z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="6291f-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="6291f-114">Udostępnianie typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6291f-114">Provision an application type.</span></span>
3. <span data-ttu-id="6291f-115">Określ i tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6291f-115">Specify and create an application.</span></span>
4. <span data-ttu-id="6291f-116">Określ i utworzyć usług.</span><span class="sxs-lookup"><span data-stu-id="6291f-116">Specify and create services.</span></span>

<span data-ttu-id="6291f-117">tooremove istniejącej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6291f-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="6291f-118">Usunięcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-118">Delete hello application.</span></span>
2. <span data-ttu-id="6291f-119">Cofnij aprowizację hello skojarzony typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6291f-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="6291f-120">Usuń zawartość magazynu obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="6291f-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="6291f-121">Wdrażanie nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6291f-121">Deploy a new application</span></span>

<span data-ttu-id="6291f-122">toodeploy nowej aplikacji hello pełną następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="6291f-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="6291f-123">Przekaż nowy magazyn obrazu toohello pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="6291f-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="6291f-124">Przed utworzeniem aplikacji, należy przekazać magazynu obrazów platformy Service Fabric toohello pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="6291f-125">Na przykład, jeśli pakiet aplikacji hello `app_package_dir` katalogu, hello Użyj następującego polecenia tooupload hello katalogu:</span><span class="sxs-lookup"><span data-stu-id="6291f-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="6291f-126">W przypadku dużych pakietów aplikacji, można określić hello `--show-progress` opcję postęp hello toodisplay hello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="6291f-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="6291f-127">Typ aplikacji hello udostępniania</span><span class="sxs-lookup"><span data-stu-id="6291f-127">Provision hello application type</span></span>

<span data-ttu-id="6291f-128">Po zakończeniu przekazywania hello udostępnienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="6291f-129">Aplikacja hello tooprovision, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6291f-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="6291f-130">Witaj wartość `application-type-build-path` jest nazwą hello hello katalogu, gdzie możesz przekazać pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6291f-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="6291f-131">Utworzenie aplikacji na podstawie typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="6291f-131">Create an application from an application type</span></span>

<span data-ttu-id="6291f-132">Po udostępnieniem aplikacji hello, użyj następującego polecenia tooname hello i utworzyć aplikację:</span><span class="sxs-lookup"><span data-stu-id="6291f-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="6291f-133">`app-name`jest nazwą hello mają toouse dla wystąpienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="6291f-134">Możesz pobrać ze strony manifest aplikacji poprzednio obsługiwaną hello dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="6291f-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="6291f-135">Nazwa aplikacji Hello musi rozpoczynać się od prefiksu powitania `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="6291f-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="6291f-136">Tworzenie usługi dla nowej aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6291f-136">Create services for hello new application</span></span>

<span data-ttu-id="6291f-137">Po utworzeniu aplikacji z aplikacji hello należy utworzyć usług.</span><span class="sxs-lookup"><span data-stu-id="6291f-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="6291f-138">Poniższy przykład hello możemy utworzyć nowej usługi bezstanowej z naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6291f-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="6291f-139">Hello usług, które można utworzyć na podstawie aplikacji są definiowane w w pakiecie poprzednio obsługiwaną aplikacji hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="6291f-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="6291f-140">Sprawdź wdrożenie aplikacji i kondycji</span><span class="sxs-lookup"><span data-stu-id="6291f-140">Verify application deployment and health</span></span>

<span data-ttu-id="6291f-141">tooverify, że aplikacja i usługi zostały pomyślnie wdrożone, sprawdź, czy aplikacji hello i usługi są wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="6291f-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="6291f-142">podobnych poleceń tooretrieve hello kondycji hello usług i aplikacji hello należy użyć tooverify hello usługi jest w dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="6291f-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="6291f-143">Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.</span><span class="sxs-lookup"><span data-stu-id="6291f-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="6291f-144">Usuń istniejącą aplikację</span><span class="sxs-lookup"><span data-stu-id="6291f-144">Remove an existing application</span></span>

<span data-ttu-id="6291f-145">tooremove aplikacji hello pełną następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="6291f-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="6291f-146">Usunięcie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6291f-146">Delete hello application</span></span>

<span data-ttu-id="6291f-147">Aplikacja hello toodelete, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6291f-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="6291f-148">Wstrzymał obsługi administracyjnej typ aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6291f-148">Unprovision hello application type</span></span>

<span data-ttu-id="6291f-149">Po usunięciu aplikacji hello można anulować udostępnienia typ aplikacji hello, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="6291f-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="6291f-150">Typ aplikacji hello toounprovision, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6291f-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="6291f-151">Typ Hello wersja nazwę i typ musi odpowiadać, hello nazwa i wersja w manifeście aplikacji poprzednio obsługiwaną hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="6291f-152">Usuwanie pakietu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6291f-152">Delete hello application package</span></span>

<span data-ttu-id="6291f-153">Po ma anulował udostępnianie typ aplikacji hello, można usunąć pakietu aplikacji hello z magazynu obrazów hello, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="6291f-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="6291f-154">Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="6291f-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="6291f-155">pakiet aplikacji hello toodelete z magazynu obrazów hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6291f-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="6291f-156">`content-path`musi być nazwą hello hello katalogu, który został przekazany, po utworzeniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6291f-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="6291f-157">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="6291f-157">Related articles</span></span>

* [<span data-ttu-id="6291f-158">Usługa Service Fabric i interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6291f-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* <span data-ttu-id="6291f-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md) (Wprowadzenie do interfejsu wiersza polecenia XPlat usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="6291f-159">[Get started with Service Fabric XPlat CLI](service-fabric-azure-cli.md)</span></span>
