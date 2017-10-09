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
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="a6212-104">Obsługa aplikacji Redaguj docker w sieci szkieletowej usług Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a6212-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="a6212-105">Docker używa hello [docker-compose.yml](https://docs.docker.com/compose) pliku do definiowania wielu kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6212-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="a6212-106">toomake go łatwo klientów zapoznać się z Docker tooorchestrate istniejące aplikacje kontenera na sieć szkieletowa usług Azure, jest dostępna obsługa podglądu rozwiązania Docker Compose natywnie hello platformy.</span><span class="sxs-lookup"><span data-stu-id="a6212-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="a6212-107">Sieć szkieletowa usług może zaakceptować wersji 3 lub nowszej `docker-compose.yml` plików.</span><span class="sxs-lookup"><span data-stu-id="a6212-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="a6212-108">Ponieważ ta obsługa jest dostępna w wersji zapoznawczej, jest obsługiwana tylko podzestaw Redaguj dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="a6212-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="a6212-109">Na przykład nie są obsługiwane uaktualnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6212-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="a6212-110">Można zawsze usunąć i wdrażania aplikacji, a nie jej uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="a6212-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="a6212-111">toouse to podglądu, tworzenia klastra w wersji 5.7 lub nowszej środowiska uruchomieniowego platformy Service Fabric hello za pośrednictwem portalu Azure oraz hello odpowiadającego SDK hello.</span><span class="sxs-lookup"><span data-stu-id="a6212-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6212-112">Ta funkcja jest w wersji zapoznawczej i nie jest obsługiwana w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a6212-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="a6212-113">Wdrażanie rozwiązania Docker Compose pliku w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="a6212-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="a6212-114">Hello następujące polecenia Tworzenie aplikacji usługi Service Fabric (o nazwie `fabric:/TestContainerApp` w hello poprzedzających przykładzie), które można monitorować i zarządzać, takich jak innych aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="a6212-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="a6212-115">Można użyć nazwy określonej aplikacji hello dla zapytań o kondycję.</span><span class="sxs-lookup"><span data-stu-id="a6212-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="a6212-116">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6212-116">Use PowerShell</span></span>

<span data-ttu-id="a6212-117">Tworzenie aplikacji usługi sieci szkieletowej tworzą z plik docker-compose.yml, uruchamiając następujące polecenie w programie PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="a6212-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="a6212-118">`RegistryUserName`i `RegistryPassword` można znaleźć toohello kontenera rejestru użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="a6212-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="a6212-119">Po zakończeniu aplikacji hello jej stan można sprawdzić za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a6212-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="a6212-120">Witaj toodelete tworzenia aplikacji za pomocą programu PowerShell, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a6212-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="a6212-121">Użyj usługi sieci szkieletowej interfejsu wiersza polecenia Azure (sfctl)</span><span class="sxs-lookup"><span data-stu-id="a6212-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="a6212-122">Alternatywnie można użyć hello następujące polecenia interfejsu wiersza polecenia usługi sieci szkieletowej:</span><span class="sxs-lookup"><span data-stu-id="a6212-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="a6212-123">Po utworzeniu aplikacji hello jej stan można sprawdzić za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="a6212-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="a6212-124">Witaj toodelete tworzenia aplikacji, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a6212-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="a6212-125">Obsługiwane dyrektywy tworzenia</span><span class="sxs-lookup"><span data-stu-id="a6212-125">Supported Compose directives</span></span>

<span data-ttu-id="a6212-126">Ta wersja zapoznawcza obsługuje podzbiór hello opcji konfiguracji z formatu w wersji 3 Redaguj hello, w tym powitania po nim elementów podstawowych:</span><span class="sxs-lookup"><span data-stu-id="a6212-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="a6212-127">Usługi > Wdrażanie > repliki</span><span class="sxs-lookup"><span data-stu-id="a6212-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="a6212-128">Usługi > Wdrażanie > umieszczania > ograniczenia</span><span class="sxs-lookup"><span data-stu-id="a6212-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="a6212-129">Usługi > Wdrażanie > Zasoby > limity</span><span class="sxs-lookup"><span data-stu-id="a6212-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="a6212-130">udziały procesorów</span><span class="sxs-lookup"><span data-stu-id="a6212-130">-cpu-shares</span></span>
    * <span data-ttu-id="a6212-131">-pamięci</span><span class="sxs-lookup"><span data-stu-id="a6212-131">-memory</span></span>
    * <span data-ttu-id="a6212-132">-pamięci-wymiany</span><span class="sxs-lookup"><span data-stu-id="a6212-132">-memory-swap</span></span>
* <span data-ttu-id="a6212-133">Usługi > poleceń</span><span class="sxs-lookup"><span data-stu-id="a6212-133">Services > Commands</span></span>
* <span data-ttu-id="a6212-134">Usługi > środowiska</span><span class="sxs-lookup"><span data-stu-id="a6212-134">Services > Environment</span></span>
* <span data-ttu-id="a6212-135">Usługi > portów</span><span class="sxs-lookup"><span data-stu-id="a6212-135">Services > Ports</span></span>
* <span data-ttu-id="a6212-136">Usługi > obrazu</span><span class="sxs-lookup"><span data-stu-id="a6212-136">Services > Image</span></span>
* <span data-ttu-id="a6212-137">Usługi > izolację (tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="a6212-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="a6212-138">Usługi > Rejestrowanie > sterownika</span><span class="sxs-lookup"><span data-stu-id="a6212-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="a6212-139">Usługi > Rejestrowanie > sterownika > Opcje</span><span class="sxs-lookup"><span data-stu-id="a6212-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="a6212-140">Wolumin & wdrażanie > woluminu</span><span class="sxs-lookup"><span data-stu-id="a6212-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="a6212-141">Konfigurowanie klastra hello wymuszania ograniczenia zasobów, zgodnie z opisem w [ładu zasobów sieci szkieletowej usług](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a6212-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="a6212-142">Inne rozwiązania Docker Compose dyrektywy nie są obsługiwane dla tej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a6212-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="a6212-143">ServiceDnsName obliczeń</span><span class="sxs-lookup"><span data-stu-id="a6212-143">ServiceDnsName computation</span></span>

<span data-ttu-id="a6212-144">Jeśli nazwa usługi hello, określona w pliku tworzenia jest w pełni kwalifikowaną nazwą domeny (to znaczy zawiera kropkę [.]), nazwa DNS hello zarejestrowany przez sieć szkieletowa usług to `<ServiceName>` (w tym hello kropkę).</span><span class="sxs-lookup"><span data-stu-id="a6212-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="a6212-145">Jeśli nie, każdy z segmentów ścieżki w nazwie aplikacji hello staje się etykietę domeny w hello nazwę DNS usługi, z hello pierwszy segment ścieżki staje się hello etykieta domeny najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a6212-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="a6212-146">Na przykład jeśli hello określona nazwa aplikacji jest `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` byłoby hello zarejestrowanej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="a6212-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="a6212-147">Różnice między Redaguj (wystąpienie definicji) i sieci szkieletowej usług modelu aplikacji (definicja typu)</span><span class="sxs-lookup"><span data-stu-id="a6212-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="a6212-148">Plik docker-compose.yml opisuje zestaw możliwych do wdrożenia kontenerów, łącznie z ich właściwości i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6212-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="a6212-149">Na przykład plik hello może zawierać zmienne środowiskowe i portów.</span><span class="sxs-lookup"><span data-stu-id="a6212-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="a6212-150">Można również określić parametry wdrażania, takie jak ograniczenia dotyczące umieszczania, limity zasobów i nazwy DNS w plik docker-compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="a6212-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="a6212-151">Witaj [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md) używa typów usługi oraz typy aplikacji, gdzie masz wiele wystąpień aplikacji hello tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="a6212-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="a6212-152">Na przykład można mieć jedno wystąpienie aplikacji na klienta.</span><span class="sxs-lookup"><span data-stu-id="a6212-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="a6212-153">Ten model na podstawie typu obsługuje wiele wersji hello tego samego typu aplikacji zarejestrowanej hello w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a6212-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="a6212-154">Na przykład klienta A może mieć utworzyć wystąpienia typu 1.0 AppTypeA aplikacji, a klient B może mieć inna aplikacja hello utworzono wystąpienie tego samego typu i wersji.</span><span class="sxs-lookup"><span data-stu-id="a6212-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="a6212-155">Zdefiniuj typy aplikacji hello w manifestach aplikacji hello oraz określić parametry nazwy i wdrażania aplikacji hello podczas tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a6212-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="a6212-156">Chociaż ten model zapewnia elastyczność, firma Microsoft są także planowania toosupport gdy typy są niejawne z pliku manifestu hello model wdrożenia prostszy, na podstawie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="a6212-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="a6212-157">W tym modelu każda aplikacja uzyskuje niezależne manifeście.</span><span class="sxs-lookup"><span data-stu-id="a6212-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="a6212-158">Firma Microsoft przeglądania tym wysiłku przez dodanie obsługi docker-compose.yml, który jest formatem wdrożenia na podstawie wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="a6212-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6212-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6212-159">Next steps</span></span>

* <span data-ttu-id="a6212-160">Przeczytana hello [modelu aplikacji sieci szkieletowej usług](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="a6212-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* <span data-ttu-id="a6212-161">[Get started with Service Fabric CLI](service-fabric-cli.md) (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="a6212-161">[Get started with Service Fabric CLI](service-fabric-cli.md)</span></span>
