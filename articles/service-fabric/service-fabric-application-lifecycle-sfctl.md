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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="d5577-103">Zarządzanie aplikacją sieci szkieletowej usług Azure przy użyciu interfejsu wiersza polecenia Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d5577-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="d5577-104">Dowiedz się, jak toocreate i usuwania aplikacji, które są uruchomione w klastrze usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="d5577-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5577-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d5577-105">Prerequisites</span></span>

* <span data-ttu-id="d5577-106">Instalowanie usługi sieci szkieletowej interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5577-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="d5577-107">Następnie wybierz klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="d5577-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="d5577-108">Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d5577-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="d5577-109">Ma sieci szkieletowej usług aplikacji pakietu gotowe toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="d5577-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="d5577-110">Aby uzyskać więcej informacji o tym, jak tooauthor i pakietu aplikacji, przeczytaj o hello [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="d5577-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d5577-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d5577-111">Overview</span></span>

<span data-ttu-id="d5577-112">toodeploy nowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d5577-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="d5577-113">Przekaż pakiet toohello sieci szkieletowej usług obrazu sklepu z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="d5577-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="d5577-114">Udostępnianie typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-114">Provision an application type.</span></span>
3. <span data-ttu-id="d5577-115">Określ i tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-115">Specify and create an application.</span></span>
4. <span data-ttu-id="d5577-116">Określ i utworzyć usług.</span><span class="sxs-lookup"><span data-stu-id="d5577-116">Specify and create services.</span></span>

<span data-ttu-id="d5577-117">tooremove istniejącej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d5577-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="d5577-118">Usunięcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-118">Delete hello application.</span></span>
2. <span data-ttu-id="d5577-119">Cofnij aprowizację hello skojarzony typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="d5577-120">Usuń zawartość magazynu obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="d5577-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="d5577-121">Wdrażanie nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5577-121">Deploy a new application</span></span>

<span data-ttu-id="d5577-122">toodeploy nowej aplikacji hello pełną następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d5577-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="d5577-123">Przekaż nowy magazyn obrazu toohello pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5577-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="d5577-124">Przed utworzeniem aplikacji, należy przekazać magazynu obrazów platformy Service Fabric toohello pakietu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="d5577-125">Na przykład, jeśli pakiet aplikacji hello `app_package_dir` katalogu, hello Użyj następującego polecenia tooupload hello katalogu:</span><span class="sxs-lookup"><span data-stu-id="d5577-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="d5577-126">W przypadku dużych pakietów aplikacji, można określić hello `--show-progress` opcję postęp hello toodisplay hello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="d5577-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="d5577-127">Typ aplikacji hello udostępniania</span><span class="sxs-lookup"><span data-stu-id="d5577-127">Provision hello application type</span></span>

<span data-ttu-id="d5577-128">Po zakończeniu przekazywania hello udostępnienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="d5577-129">Aplikacja hello tooprovision, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5577-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="d5577-130">Witaj wartość `application-type-build-path` jest nazwą hello hello katalogu, gdzie możesz przekazać pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="d5577-131">Utworzenie aplikacji na podstawie typu aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5577-131">Create an application from an application type</span></span>

<span data-ttu-id="d5577-132">Po udostępnieniem aplikacji hello, użyj następującego polecenia tooname hello i utworzyć aplikację:</span><span class="sxs-lookup"><span data-stu-id="d5577-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="d5577-133">`app-name`jest nazwą hello mają toouse dla wystąpienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="d5577-134">W manifeście aplikacji poprzednio udostępnione można uzyskać dodatkowe parametry.</span><span class="sxs-lookup"><span data-stu-id="d5577-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="d5577-135">Nazwa aplikacji Hello musi rozpoczynać się od prefiksu powitania `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="d5577-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="d5577-136">Tworzenie usługi dla nowej aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5577-136">Create services for hello new application</span></span>

<span data-ttu-id="d5577-137">Po utworzeniu aplikacji z aplikacji hello należy utworzyć usług.</span><span class="sxs-lookup"><span data-stu-id="d5577-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="d5577-138">Poniższy przykład hello możemy utworzyć nowej usługi bezstanowej z naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="d5577-139">Hello usług, które można utworzyć na podstawie aplikacji są definiowane w w pakiecie poprzednio obsługiwaną aplikacji hello manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="d5577-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="d5577-140">Sprawdź wdrożenie aplikacji i kondycji</span><span class="sxs-lookup"><span data-stu-id="d5577-140">Verify application deployment and health</span></span>

<span data-ttu-id="d5577-141">tooverify wszystko jest w dobrej kondycji, należy użyć następującego polecenia kondycji hello:</span><span class="sxs-lookup"><span data-stu-id="d5577-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="d5577-142">podobnych poleceń tooretrieve hello kondycji hello usług i aplikacji, użyj tooverify hello usługi jest w dobrej kondycji:</span><span class="sxs-lookup"><span data-stu-id="d5577-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="d5577-143">Dobrej kondycji usługi i aplikacje mają `HealthState` wartość `Ok`.</span><span class="sxs-lookup"><span data-stu-id="d5577-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="d5577-144">Usuń istniejącą aplikację</span><span class="sxs-lookup"><span data-stu-id="d5577-144">Remove an existing application</span></span>

<span data-ttu-id="d5577-145">tooremove aplikacji hello pełną następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d5577-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="d5577-146">Usunięcie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5577-146">Delete hello application</span></span>

<span data-ttu-id="d5577-147">Aplikacja hello toodelete, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5577-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="d5577-148">Wstrzymał obsługi administracyjnej typ aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5577-148">Unprovision hello application type</span></span>

<span data-ttu-id="d5577-149">Po usunięciu aplikacji hello można anulować udostępnienia typ aplikacji hello, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d5577-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="d5577-150">Typ aplikacji hello toounprovision, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5577-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="d5577-151">Typ Hello wersja nazwę i typ musi odpowiadać, hello nazwa i wersja w manifeście aplikacji poprzednio obsługiwaną hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="d5577-152">Usuwanie pakietu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5577-152">Delete hello application package</span></span>

<span data-ttu-id="d5577-153">Po ma anulował udostępnianie typ aplikacji hello, można usunąć pakietu aplikacji hello z magazynu obrazów hello, jeśli nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d5577-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="d5577-154">Usunięcie pakietów aplikacji ułatwia odzyskiwanie miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="d5577-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="d5577-155">pakiet aplikacji hello toodelete z magazynu obrazów hello, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5577-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="d5577-156">`content-path`musi być nazwą hello hello katalogu, który został przekazany, po utworzeniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="d5577-157">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d5577-157">Upgrade application</span></span>

<span data-ttu-id="d5577-158">Po utworzeniu aplikacji, powtórz hello tego samego zestawu tooprovision czynności drugiego wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5577-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="d5577-159">Następnie Uaktualnianie aplikacji usługi Service Fabric może przejść toorunning hello druga wersja aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d5577-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="d5577-160">Aby uzyskać więcej informacji, zobacz dokumentację hello [uaktualnień aplikacji usługi sieć szkieletowa](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d5577-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="d5577-161">tooperform uaktualniania pierwszego udostępniania hello następnej wersji przy użyciu aplikacji hello jak poprzednio hello tych samych poleceń:</span><span class="sxs-lookup"><span data-stu-id="d5577-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="d5577-162">Zalecane jest, a następnie tooperform monitorowanych automatyczne uaktualnianie uruchomienie uaktualnienia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d5577-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="d5577-163">Uaktualnienia zastąpienie istniejących parametrów z dowolnego zestaw jest określony.</span><span class="sxs-lookup"><span data-stu-id="d5577-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="d5577-164">Parametry aplikacji powinien zostać przekazany jako argumenty polecenia uaktualniania toohello, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d5577-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="d5577-165">Parametry aplikacji powinien być kodowany jako obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="d5577-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="d5577-166">wcześniej określony tooretrieve żadnych parametrów, możesz użyć hello `sfctl application info` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5577-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="d5577-167">Podczas uaktualniania aplikacji jest w toku, stan hello można pobrać przy użyciu `sfctl application upgrade-status` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5577-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="d5577-168">Ponadto jeśli uaktualnianie jest w toku i musi toobe anulowane, można użyć hello `sfctl application upgrade-rollback` tooroll ponownie hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="d5577-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5577-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5577-169">Next steps</span></span>

* [<span data-ttu-id="d5577-170">Podstawy usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d5577-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="d5577-171">Wprowadzenie do korzystania z usługi Service Fabric w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="d5577-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="d5577-172">Uruchamianie uaktualniania aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="d5577-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
