---
title: "Tematy dotyczące uaktualniania aplikacji zaawansowanego | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono niektóre tematy zaawansowane dotyczące uaktualniania aplikacji sieci szkieletowej usług."
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
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="bebb3-103">Uaktualnianie aplikacji usługi Service Fabric: Tematy zaawansowane</span><span class="sxs-lookup"><span data-stu-id="bebb3-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="bebb3-104">Dodawanie lub usuwanie usługi podczas uaktualniania aplikacji</span><span class="sxs-lookup"><span data-stu-id="bebb3-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="bebb3-105">Jeśli nowa usługa zostanie dodany do aplikacji, która jest już wdrożony i opublikowane jako uaktualnienie, nowej usługi jest dodawany do wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bebb3-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="bebb3-106">Takie uaktualnienia nie wpływa na usług, które zostały już część aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bebb3-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="bebb3-107">Jednak należy uruchomić wystąpienie usługi, która została dodana dla nowej usługi jest aktywne (przy użyciu `New-ServiceFabricService` polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="bebb3-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="bebb3-108">Usługi może zostać także usunięty z aplikacji w ramach uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="bebb3-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="bebb3-109">Jednak wszystkie bieżącego wystąpienia usługi usunięte być do musi zostać zatrzymana przed kontynuowaniem uaktualniania (przy użyciu `Remove-ServiceFabricService` polecenia cmdlet).</span><span class="sxs-lookup"><span data-stu-id="bebb3-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="bebb3-110">Ręczny tryb uaktualniania</span><span class="sxs-lookup"><span data-stu-id="bebb3-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="bebb3-111">Należy rozważyć niemonitorowane ręczny tryb tylko w przypadku uaktualniania nie powiodło się lub został wstrzymany.</span><span class="sxs-lookup"><span data-stu-id="bebb3-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="bebb3-112">Monitorowane tryb jest zalecany tryb uaktualniania aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="bebb3-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="bebb3-113">Azure Service Fabric zawiera wiele trybów uaktualnienia do obsługi klastrów rozwoju i produkcji.</span><span class="sxs-lookup"><span data-stu-id="bebb3-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="bebb3-114">Wybrane opcje wdrażania może się różnić w różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="bebb3-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="bebb3-115">Uaktualnienie stopniowe aplikacji monitorowanych jest najbardziej typowe uaktualnienie do użycia w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="bebb3-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="bebb3-116">Po określeniu zasad uaktualniania sieci szkieletowej usług gwarantuje, że aplikacja jest w dobrej kondycji przed uaktualnianie będzie kontynuowane.</span><span class="sxs-lookup"><span data-stu-id="bebb3-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="bebb3-117">Administrator aplikacji umożliwia ręczne stopniowego tryb uaktualniania aplikacji ma pełną kontrolę nad postęp uaktualnienia za pośrednictwem różnych domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="bebb3-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="bebb3-118">Ten tryb jest przydatne, gdy wymagane są zasady oceny kondycji dostosowane lub złożonych lub wykonywane jest uaktualnienie nietypowe (na przykład aplikacja jest już utraty danych).</span><span class="sxs-lookup"><span data-stu-id="bebb3-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="bebb3-119">Na koniec automatycznego uaktualnienia stopniowego aplikacji przydaje się do rozwoju lub środowiska testowe w celu zapewnienia szybkiego iteracji cyklu podczas tworzenia usługi.</span><span class="sxs-lookup"><span data-stu-id="bebb3-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="bebb3-120">Zmień na ręczny tryb uaktualniania</span><span class="sxs-lookup"><span data-stu-id="bebb3-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="bebb3-121">**Ręczne**— Zatrzymaj uaktualnienie aplikacji w bieżącym UD i zmienić niemonitorowane ręczny tryb uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="bebb3-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="bebb3-122">Administrator musi ręcznie wywołać **MoveNextApplicationUpgradeDomainAsync** do wyzwalacza wycofanie inicjując nowego uaktualnienia lub kontynuować proces uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="bebb3-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="bebb3-123">Po uaktualnieniu wchodzi w trybie ręcznym, pozostaje w trybie ręcznym do momentu zainicjowania nowego uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="bebb3-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="bebb3-124">**GetApplicationUpgradeProgressAsync** polecenie zwraca sieci SZKIELETOWEJ\_aplikacji\_uaktualnienia\_stanu\_STOPNIOWYCH\_do przodu\_OCZEKUJE.</span><span class="sxs-lookup"><span data-stu-id="bebb3-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="bebb3-125">Uaktualnienie z pakietem różnicowego</span><span class="sxs-lookup"><span data-stu-id="bebb3-125">Upgrade with a diff package</span></span>
<span data-ttu-id="bebb3-126">Można uaktualnić aplikacji usługi Service Fabric przy inicjowania obsługi administracyjnej z pakietem aplikacji pełne, niezależne.</span><span class="sxs-lookup"><span data-stu-id="bebb3-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="bebb3-127">Można również uaktualnić aplikację przy użyciu pakietu różnicowego, który zawiera tylko pliki zaktualizowaną aplikację, manifest aplikacji zaktualizowane i pliki manifestu usługi.</span><span class="sxs-lookup"><span data-stu-id="bebb3-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="bebb3-128">Pakiet aplikacji pełne zawiera wszystkie pliki niezbędne do uruchomienia aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="bebb3-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="bebb3-129">Pakiet różnicowego zawiera tylko te pliki, które zmienione od ostatniego udostępniania i uaktualniania bieżącego oraz manifest aplikacji pełną a usługą pliki manifestu.</span><span class="sxs-lookup"><span data-stu-id="bebb3-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="bebb3-130">Wszystkie odwołania w manifeście aplikacji lub manifestu usługi, której nie można znaleźć w układzie kompilacji jest wyszukiwany w magazynie obrazu.</span><span class="sxs-lookup"><span data-stu-id="bebb3-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="bebb3-131">Pakiety aplikacji pełne są wymagane dla pierwszej instalacji aplikacji do klastra.</span><span class="sxs-lookup"><span data-stu-id="bebb3-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="bebb3-132">Kolejne aktualizacje mogą być pakiet pełnej aplikacji lub pakietu różnic.</span><span class="sxs-lookup"><span data-stu-id="bebb3-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="bebb3-133">Sytuacji, gdy przy użyciu pakietu różnicowego dobrym wyborem będzie:</span><span class="sxs-lookup"><span data-stu-id="bebb3-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="bebb3-134">Pakiet różnicowego jest preferowane w przypadku pakietu dużej aplikacji, który odwołuje się wiele plików manifestu usługi i/lub kilka pakietów kodu, pakiety konfiguracji lub pakietów danych.</span><span class="sxs-lookup"><span data-stu-id="bebb3-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="bebb3-135">Pakiet różnicowego jest preferowane w przypadku systemu wdrożenia, w którym generuje układu kompilacji bezpośrednio w procesie kompilacji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bebb3-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="bebb3-136">W takim przypadku mimo że nie zmieniła się kod, nowo zbudowany zestawy uzyskać różne sumy kontrolnej.</span><span class="sxs-lookup"><span data-stu-id="bebb3-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="bebb3-137">Przy użyciu pakietu pełnej aplikacji należy zaktualizować wersję na wszystkie pakiety kodu.</span><span class="sxs-lookup"><span data-stu-id="bebb3-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="bebb3-138">Przy użyciu pakietu różnicowego, musisz tylko podać zmienionych plików i pliki manifestu, których wersja uległa zmianie.</span><span class="sxs-lookup"><span data-stu-id="bebb3-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="bebb3-139">Po uaktualnieniu aplikacji przy użyciu programu Visual Studio, pakietu różnic jest automatycznie publikowany.</span><span class="sxs-lookup"><span data-stu-id="bebb3-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="bebb3-140">Aby ręcznie utworzyć pakiet różnicowego, manifest aplikacji i manifestów usługi muszą zostać zaktualizowane, ale tylko zmienione pakiety powinny być uwzględnione w pakiet aplikacji końcowego.</span><span class="sxs-lookup"><span data-stu-id="bebb3-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="bebb3-141">Na przykład Zacznijmy następującej aplikacji (dostępne w celu ułatwienia zrozumienia numery wersji):</span><span class="sxs-lookup"><span data-stu-id="bebb3-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="bebb3-142">Teraz załóżmy, że chcesz zaktualizować tylko kod pakietu programu service1 przy użyciu pakietu różnicowego przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bebb3-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="bebb3-143">Teraz zaktualizowane aplikacji ma następującą strukturę folderów:</span><span class="sxs-lookup"><span data-stu-id="bebb3-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="bebb3-144">W takim przypadku należy zaktualizować manifest aplikacji 2.0.0 i manifest usługi service1 w celu uwzględnienia aktualizacji pakietu kodu.</span><span class="sxs-lookup"><span data-stu-id="bebb3-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="bebb3-145">Folder dla pakietu aplikacji może mieć następującą strukturę:</span><span class="sxs-lookup"><span data-stu-id="bebb3-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="bebb3-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bebb3-146">Next steps</span></span>
<span data-ttu-id="bebb3-147">[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bebb3-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="bebb3-148">[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bebb3-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="bebb3-149">Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="bebb3-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="bebb3-150">Uzyskania uaktualnień aplikacji zgodnych przez poznanie [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="bebb3-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="bebb3-151">Rozwiązywania typowych problemów w uaktualnień aplikacji, korzystając z procedury opisanej w [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bebb3-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
