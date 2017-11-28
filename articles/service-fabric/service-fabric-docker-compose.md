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
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="9496b-104">Obsługa aplikacji Redaguj docker w sieci szkieletowej usług Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="9496b-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="9496b-105">Używa docker [docker-compose.yml](https://docs.docker.com/compose) pliku do definiowania wielu kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9496b-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="9496b-106">Aby ułatwić klientom zapoznać się z rozwiązaniem Docker do organizowania istniejących aplikacji kontenera na sieć szkieletowa usług Azure, firma Microsoft wprowadzono obsługę podglądu rozwiązania Docker Compose natywnie przez platformę.</span><span class="sxs-lookup"><span data-stu-id="9496b-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="9496b-107">Sieć szkieletowa usług może zaakceptować wersji 3 lub nowszej `docker-compose.yml` plików.</span><span class="sxs-lookup"><span data-stu-id="9496b-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="9496b-108">Ponieważ ta obsługa jest dostępna w wersji zapoznawczej, jest obsługiwana tylko podzestaw Redaguj dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="9496b-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="9496b-109">Na przykład nie są obsługiwane uaktualnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9496b-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="9496b-110">Można zawsze usunąć i wdrażania aplikacji, a nie jej uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="9496b-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="9496b-111">Aby korzystać z tej wersji zapoznawczej, tworzenia klastra w wersji 5.7 lub nowszej środowiska uruchomieniowego platformy Service Fabric za pośrednictwem portalu Azure oraz odpowiedniego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9496b-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="9496b-112">Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9496b-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="9496b-113">Wdrażanie rozwiązania Docker Compose pliku w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="9496b-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="9496b-114">Następujące polecenia Utwórz aplikację usługi sieć szkieletowa (o nazwie `fabric:/TestContainerApp` w poprzednim przykładzie), które można monitorować i zarządzać, takich jak innych aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="9496b-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="9496b-115">Określona nazwa aplikacji dla zapytań o kondycję można użyć.</span><span class="sxs-lookup"><span data-stu-id="9496b-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="9496b-116">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9496b-116">Use PowerShell</span></span>

<span data-ttu-id="9496b-117">Tworzenie aplikacji usługi sieci szkieletowej tworzą z plik docker-compose.yml, uruchamiając następujące polecenie w programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9496b-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="9496b-118">`RegistryUserName`i `RegistryPassword` odwoływać się do kontenera rejestru nazwy i hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9496b-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="9496b-119">Po zakończeniu aplikacji jej stan można sprawdzić za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9496b-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="9496b-120">Aby usunąć tworzenia aplikacji za pomocą programu PowerShell, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9496b-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="9496b-121">Użyj usługi sieci szkieletowej interfejsu wiersza polecenia Azure (sfctl)</span><span class="sxs-lookup"><span data-stu-id="9496b-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="9496b-122">Można również można użyć następującego polecenia interfejsu wiersza polecenia usługi sieci szkieletowej:</span><span class="sxs-lookup"><span data-stu-id="9496b-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="9496b-123">Po utworzeniu aplikacji jej stan można sprawdzić za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9496b-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="9496b-124">Aby usunąć tworzenia aplikacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9496b-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="9496b-125">Obsługiwane dyrektywy tworzenia</span><span class="sxs-lookup"><span data-stu-id="9496b-125">Supported Compose directives</span></span>

<span data-ttu-id="9496b-126">Ta wersja zapoznawcza obsługuje podzbiór z formatu Redaguj w wersji 3, w tym następujące elementy podstawowe opcje konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="9496b-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="9496b-127">Usługi > Wdrażanie > repliki</span><span class="sxs-lookup"><span data-stu-id="9496b-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="9496b-128">Usługi > Wdrażanie > umieszczania > ograniczenia</span><span class="sxs-lookup"><span data-stu-id="9496b-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="9496b-129">Usługi > Wdrażanie > Zasoby > limity</span><span class="sxs-lookup"><span data-stu-id="9496b-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="9496b-130">udziały procesorów</span><span class="sxs-lookup"><span data-stu-id="9496b-130">-cpu-shares</span></span>
    * <span data-ttu-id="9496b-131">-pamięci</span><span class="sxs-lookup"><span data-stu-id="9496b-131">-memory</span></span>
    * <span data-ttu-id="9496b-132">-pamięci-wymiany</span><span class="sxs-lookup"><span data-stu-id="9496b-132">-memory-swap</span></span>
* <span data-ttu-id="9496b-133">Usługi > poleceń</span><span class="sxs-lookup"><span data-stu-id="9496b-133">Services > Commands</span></span>
* <span data-ttu-id="9496b-134">Usługi > środowiska</span><span class="sxs-lookup"><span data-stu-id="9496b-134">Services > Environment</span></span>
* <span data-ttu-id="9496b-135">Usługi > portów</span><span class="sxs-lookup"><span data-stu-id="9496b-135">Services > Ports</span></span>
* <span data-ttu-id="9496b-136">Usługi > obrazu</span><span class="sxs-lookup"><span data-stu-id="9496b-136">Services > Image</span></span>
* <span data-ttu-id="9496b-137">Usługi > izolację (tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="9496b-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="9496b-138">Usługi > Rejestrowanie > sterownika</span><span class="sxs-lookup"><span data-stu-id="9496b-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="9496b-139">Usługi > Rejestrowanie > sterownika > Opcje</span><span class="sxs-lookup"><span data-stu-id="9496b-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="9496b-140">Wolumin & wdrażanie > woluminu</span><span class="sxs-lookup"><span data-stu-id="9496b-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="9496b-141">Konfigurowanie klastra na potrzeby wymuszania ograniczenia zasobów, zgodnie z opisem w [ładu zasobów sieci szkieletowej usług](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9496b-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="9496b-142">Inne rozwiązania Docker Compose dyrektywy nie są obsługiwane dla tej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="9496b-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="9496b-143">ServiceDnsName obliczeń</span><span class="sxs-lookup"><span data-stu-id="9496b-143">ServiceDnsName computation</span></span>

<span data-ttu-id="9496b-144">Jeśli nazwa usługi określona w pliku tworzenia jest w pełni kwalifikowaną nazwą domeny (to znaczy zawiera kropkę [.]), nazwa DNS zarejestrowane przez sieć szkieletowa usług to `<ServiceName>` (w tym kropki (.)).</span><span class="sxs-lookup"><span data-stu-id="9496b-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="9496b-145">Jeśli nie, każdy z segmentów ścieżki w nazwie aplikacji staje się etykieta domeny, w polu Nazwa DNS usługi z pierwszy segment ścieżki, staje się etykieta domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="9496b-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="9496b-146">Na przykład, jeśli określona nazwa aplikacji jest `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` byłoby zarejestrowanej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="9496b-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="9496b-147">Różnice między Redaguj (wystąpienie definicji) i sieci szkieletowej usług modelu aplikacji (definicja typu)</span><span class="sxs-lookup"><span data-stu-id="9496b-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="9496b-148">Plik docker-compose.yml opisuje zestaw możliwych do wdrożenia kontenerów, łącznie z ich właściwości i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9496b-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="9496b-149">Na przykład plik może zawierać zmienne środowiskowe i portów.</span><span class="sxs-lookup"><span data-stu-id="9496b-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="9496b-150">Można również określić parametry wdrażania, takie jak ograniczenia dotyczące umieszczania, limity zasobów i nazwy DNS w plik docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="9496b-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="9496b-151">[Model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) używa usługi typy i aplikacji, gdzie masz wiele wystąpień aplikacji tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="9496b-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="9496b-152">Na przykład można mieć jedno wystąpienie aplikacji na klienta.</span><span class="sxs-lookup"><span data-stu-id="9496b-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="9496b-153">Ten model na podstawie typu obsługuje wiele wersji tego samego typu aplikacji, który został zarejestrowany za pomocą środowiska uruchomieniowego.</span><span class="sxs-lookup"><span data-stu-id="9496b-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="9496b-154">Na przykład klient A może mieć utworzyć wystąpienia typu 1.0 AppTypeA aplikacji, a klient B może mieć inną aplikację utworzone z tego samego typu i wersji.</span><span class="sxs-lookup"><span data-stu-id="9496b-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="9496b-155">Definiowanie typów aplikacji w manifestach aplikacji i określić parametry nazwy i wdrażania aplikacji, podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9496b-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="9496b-156">Chociaż ten model zapewnia elastyczność, będziemy również planowania obsługi modelu wdrażania prostszy, na podstawie wystąpienia, których typy są niejawne z pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="9496b-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="9496b-157">W tym modelu każda aplikacja uzyskuje niezależne manifeście.</span><span class="sxs-lookup"><span data-stu-id="9496b-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="9496b-158">Firma Microsoft przeglądania tym wysiłku przez dodanie obsługi docker-compose.yml, który jest formatem wdrożenia na podstawie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="9496b-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9496b-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9496b-159">Next steps</span></span>

* <span data-ttu-id="9496b-160">Przeczytaj na [modelu aplikacji sieci szkieletowej usług](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="9496b-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* <span data-ttu-id="9496b-161">[Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="9496b-161">[Get started with Service Fabric CLI](service-fabric-cli.md)</span></span>
