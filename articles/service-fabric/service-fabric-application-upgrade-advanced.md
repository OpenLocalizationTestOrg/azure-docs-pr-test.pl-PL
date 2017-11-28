---
title: aaaAdvanced tematy uaktualniania aplikacji | Dokumentacja firmy Microsoft
description: "W tym artykule omówiono niektóre tematy zaawansowane dotyczące tooupgrading aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="623c2-103">Uaktualnianie aplikacji usługi Service Fabric: Tematy zaawansowane</span><span class="sxs-lookup"><span data-stu-id="623c2-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="623c2-104">Dodawanie lub usuwanie usługi podczas uaktualniania aplikacji</span><span class="sxs-lookup"><span data-stu-id="623c2-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="623c2-105">Jeśli nowa usługa zostanie dodany tooan aplikacji, która jest już wdrożony i opublikowane jako uaktualnienie, hello nowej usługi jest dodany toohello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="623c2-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="623c2-106">Takie uaktualnienia nie wpływa na powitania usług, które były częścią aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="623c2-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="623c2-107">Jednak wystąpienia usługi hello, która została dodana musi być uruchomiona hello nowej usługi toobe active (przy użyciu hello `New-ServiceFabricService` polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="623c2-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="623c2-108">Usługi może zostać także usunięty z aplikacji w ramach uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="623c2-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="623c2-109">Jednak wszystkie bieżącego wystąpienia usługi usunięte być do hello musi zostać zatrzymana przed kontynuacją uaktualniania hello (przy użyciu hello `Remove-ServiceFabricService` polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="623c2-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="623c2-110">Ręczny tryb uaktualniania</span><span class="sxs-lookup"><span data-stu-id="623c2-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="623c2-111">należy rozważyć Hello niemonitorowane ręczny tryb tylko w przypadku uaktualniania nie powiodło się lub został wstrzymany.</span><span class="sxs-lookup"><span data-stu-id="623c2-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="623c2-112">Tryb monitorowanych Hello jest hello zalecane tryb uaktualniania aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="623c2-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="623c2-113">Azure Service Fabric zawiera wielu trybów uaktualnienia klastrów toosupport rozwoju i produkcji.</span><span class="sxs-lookup"><span data-stu-id="623c2-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="623c2-114">Wybrane opcje wdrażania może się różnić w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="623c2-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="623c2-115">uaktualnienie stopniowe aplikacji Hello monitorowane jest hello najczęstszych toouse uaktualnienia w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="623c2-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="623c2-116">Podczas uaktualniania hello określić zasady, zapewnia sieć szkieletowa usług aplikacji hello jest dobrej kondycji, aby mogła być kontynuowana hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="623c2-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="623c2-117">administrator aplikacji Hello służy hello ręczne wprowadzanie aplikacji tryb uaktualniania toohave całkowitą kontrolę nad hello postęp uaktualnienia za pośrednictwem hello różnych domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="623c2-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="623c2-118">Ten tryb jest przydatne, gdy wymagane są zasady oceny kondycji dostosowane lub złożonych lub wykonywane jest uaktualnienie nietypowe (na przykład aplikacja hello jest już utraty danych).</span><span class="sxs-lookup"><span data-stu-id="623c2-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="623c2-119">Na koniec hello automatycznego uaktualnienia stopniowego aplikacji przydaje się do rozwoju lub testowania tooprovide środowisk cykl iteracji szybkiego podczas tworzenia usługi.</span><span class="sxs-lookup"><span data-stu-id="623c2-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="623c2-120">Zmień tryb uaktualniania toomanual</span><span class="sxs-lookup"><span data-stu-id="623c2-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="623c2-121">**Ręczne**— uaktualnienie aplikacji hello Stop w hello bieżącego hello UD i zmień uaktualnienia tooUnmonitored tryb ręczny.</span><span class="sxs-lookup"><span data-stu-id="623c2-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="623c2-122">Witaj administrator musi wywołania toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed z hello wyzwalacza wycofanie inicjując nowego uaktualnienia lub uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="623c2-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="623c2-123">Po uaktualnieniu hello wejścia ręczny tryb hello, pozostaje w trybie ręcznym hello do momentu zainicjowania nowego uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="623c2-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="623c2-124">Witaj **GetApplicationUpgradeProgressAsync** polecenie zwraca sieci SZKIELETOWEJ\_aplikacji\_uaktualnienia\_stanu\_STOPNIOWYCH\_do przodu\_OCZEKUJE.</span><span class="sxs-lookup"><span data-stu-id="623c2-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="623c2-125">Uaktualnienie z pakietem różnicowego</span><span class="sxs-lookup"><span data-stu-id="623c2-125">Upgrade with a diff package</span></span>
<span data-ttu-id="623c2-126">Można uaktualnić aplikacji usługi Service Fabric przy inicjowania obsługi administracyjnej z pakietem aplikacji pełne, niezależne.</span><span class="sxs-lookup"><span data-stu-id="623c2-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="623c2-127">Aplikację można również uaktualnić przy użyciu pakietu różnicowego, który zawiera tylko pliki aplikacji hello zaktualizowane, hello zaktualizowane manifest aplikacji i pliki manifestu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="623c2-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="623c2-128">Pakiet aplikacji pełne zawiera wszystkie toostart niezbędne pliki hello i uruchomienia aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="623c2-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="623c2-129">Pakiet różnicowego zawiera hello tylko te pliki, które w klientach hello ostatniego udostępniania i uaktualniania bieżące hello oraz manifest pełnej aplikacji hello i usługa hello pliki manifestu.</span><span class="sxs-lookup"><span data-stu-id="623c2-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="623c2-130">Wszystkie odwołania w manifeście aplikacji hello lub manifestu usługi, której nie można znaleźć w układzie kompilacji hello jest wyszukiwany w hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="623c2-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="623c2-131">Pakiety aplikacji pełne są wymagane dla pierwszej instalacji klastra toohello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="623c2-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="623c2-132">Kolejne aktualizacje mogą być pakiet pełnej aplikacji lub pakietu różnic.</span><span class="sxs-lookup"><span data-stu-id="623c2-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="623c2-133">Sytuacji, gdy przy użyciu pakietu różnicowego dobrym wyborem będzie:</span><span class="sxs-lookup"><span data-stu-id="623c2-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="623c2-134">Pakiet różnicowego jest preferowane w przypadku pakietu dużej aplikacji, który odwołuje się wiele plików manifestu usługi i/lub kilka pakietów kodu, pakiety konfiguracji lub pakietów danych.</span><span class="sxs-lookup"><span data-stu-id="623c2-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="623c2-135">Pakiet różnicowego jest preferowane w przypadku systemu wdrożenia, w którym generuje układu kompilacji hello bezpośrednio w procesie kompilacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="623c2-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="623c2-136">W takim przypadku mimo że nie zmieniła się hello kodu, nowo zbudowany zestawy uzyskać różne sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="623c2-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="623c2-137">Przy użyciu pakietu pełnej aplikacji wymaga możesz tooupdate hello wersji na wszystkie pakiety kodu.</span><span class="sxs-lookup"><span data-stu-id="623c2-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="623c2-138">Przy użyciu pakietu różnicowego, tylko podanie hello zmienione pliki oraz pliki manifestu hello, gdzie hello wersja została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="623c2-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="623c2-139">Po uaktualnieniu aplikacji przy użyciu programu Visual Studio, hello różnicowego pakietu jest automatycznie publikowany.</span><span class="sxs-lookup"><span data-stu-id="623c2-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="623c2-140">toocreate pakietu różnicowego ręcznie, hello manifest aplikacji i hello usługi manifesty muszą zostać zaktualizowane, ale tylko pakietów hello zmienione powinny być uwzględnione w pakiet końcowego aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="623c2-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="623c2-141">Na przykład Zacznijmy powitania po aplikacji (dostępne w celu ułatwienia zrozumienia numery wersji):</span><span class="sxs-lookup"><span data-stu-id="623c2-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="623c2-142">Teraz załóżmy, że żądana tooupdate tylko hello pakietu kodu z service1 przy użyciu pakietu różnicowego przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="623c2-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="623c2-143">Zaktualizowano aplikacji ma teraz, hello następujące struktury folderów:</span><span class="sxs-lookup"><span data-stu-id="623c2-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="623c2-144">W takim przypadku należy zaktualizować too2.0.0 manifestu aplikacji hello i hello manifestu usługi service1 tooreflect hello kod pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="623c2-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="623c2-145">folder Hello pakietu aplikacji musi hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="623c2-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="623c2-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="623c2-146">Next steps</span></span>
<span data-ttu-id="623c2-147">[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="623c2-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="623c2-148">[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="623c2-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="623c2-149">Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="623c2-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="623c2-150">Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="623c2-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="623c2-151">Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="623c2-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
