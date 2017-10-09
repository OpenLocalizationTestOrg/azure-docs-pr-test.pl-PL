---
title: "aaaCreate pierwszej aplikacji platformy Azure mikrousług w systemie Linux przy użyciu języka C# | Dokumentacja firmy Microsoft"
description: "Tworzenie i wdrażanie aplikacji usługi Service Fabric przy użyciu platformy C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="10db6-103">Tworzenie pierwszej aplikacji usługi Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="10db6-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10db6-104">C# — Windows</span><span class="sxs-lookup"><span data-stu-id="10db6-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="10db6-105">Java — Linux</span><span class="sxs-lookup"><span data-stu-id="10db6-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="10db6-106">C# — Linux</span><span class="sxs-lookup"><span data-stu-id="10db6-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="10db6-107">Usługa Service Fabric udostępnia zestawy SDK do kompilowania usług w systemie Linux przy użyciu platform .NET Core i Java.</span><span class="sxs-lookup"><span data-stu-id="10db6-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="10db6-108">W tym samouczku opisano, jak toocreate aplikacji dla systemu Linux i kompilacji usługi przy użyciu języka C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="10db6-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10db6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="10db6-109">Prerequisites</span></span>
<span data-ttu-id="10db6-110">Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania systemu Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="10db6-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="10db6-111">Jeśli używasz systemu Mac OS X, możesz [skonfigurować jednopunktowe środowisko systemu Linux na maszynie wirtualnej za pomocą narzędzia Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="10db6-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="10db6-112">Ma również tooinstall hello [usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="10db6-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="10db6-113">Instalowanie i konfigurowanie hello generatory kodu dla języka CSharp</span><span class="sxs-lookup"><span data-stu-id="10db6-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="10db6-114">Usługa Service Fabric udostępnia narzędzia do tworzenia szkieletu, które ułatwiają tworzenie aplikacji CSharp usługi Service Fabric z poziomu terminalu przy użyciu generatora szablonów Yeoman.</span><span class="sxs-lookup"><span data-stu-id="10db6-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="10db6-115">Wykonaj kroki hello poniżej tooensure masz generatora narzędzia yeoman szablonu usługi sieć szkieletowa hello CSharp działa na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="10db6-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="10db6-116">Zainstaluj środowisko NodeJs i menedżera NPM na swojej maszynie</span><span class="sxs-lookup"><span data-stu-id="10db6-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="10db6-117">Zainstaluj generator szablonów [narzędzia Yeoman](http://yeoman.io/) na swoim komputerze z poziomu narzędzia NPM</span><span class="sxs-lookup"><span data-stu-id="10db6-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="10db6-118">Zainstaluj generator aplikacji usługi sieci szkieletowej Yeo Java hello z pakietu NPM</span><span class="sxs-lookup"><span data-stu-id="10db6-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="10db6-119">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="10db6-119">Create hello application</span></span>
<span data-ttu-id="10db6-120">Aplikacja usługi Service Fabric może zawierać jeden lub więcej usług, a każda z określoną rolę w dostarczaniu funkcjonalności aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10db6-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="10db6-121">Witaj sieci szkieletowej usług [narzędzia Yeoman](http://yeoman.io/) generator języka CSharp, które zostaną zainstalowane w ostatnim kroku, umożliwia łatwe toocreate pierwszą usługi i tooadd więcej później.</span><span class="sxs-lookup"><span data-stu-id="10db6-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="10db6-122">Użyjmy toocreate narzędzia Yeoman aplikacji z jedną usługą.</span><span class="sxs-lookup"><span data-stu-id="10db6-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="10db6-123">W terminalu wpisz następujące polecenie toostart tworzenia szkieletów hello hello:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="10db6-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="10db6-124">Nadaj nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10db6-124">Name your application.</span></span>
3. <span data-ttu-id="10db6-125">Wybierz typ hello pierwszej usługi i nadaj jej nazwę.</span><span class="sxs-lookup"><span data-stu-id="10db6-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="10db6-126">Do celów tego samouczka hello wybieramy opcję niezawodnej usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="10db6-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Generator Yeoman usługi Service Fabric dla platformy C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="10db6-128">Aby uzyskać więcej informacji na temat opcji hello, zobacz [usługi sieć szkieletowa omówienie modelu programowania](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="10db6-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="10db6-129">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="10db6-129">Build hello application</span></span>
<span data-ttu-id="10db6-130">Witaj narzędzia usługi sieć szkieletowa Yeoman szablony obejmują skryptu kompilacji, czy można użyć aplikacji hello toobuild z hello terminali (po Nawigacja toohello folderu aplikacji).</span><span class="sxs-lookup"><span data-stu-id="10db6-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="10db6-131">Wdrażanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="10db6-131">Deploy hello application</span></span>

<span data-ttu-id="10db6-132">Po utworzeniu aplikacji hello można wdrożyć klaster lokalny toohello.</span><span class="sxs-lookup"><span data-stu-id="10db6-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="10db6-133">Połącz toohello lokalnego klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="10db6-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="10db6-134">Uruchom skrypt instalacji hello hello szablonu toocopy aplikacji hello pakietu magazynu obrazu klastra toohello, Rejestracja typu aplikacji hello, i Utwórz wystąpienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10db6-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="10db6-135">Wdrażanie aplikacji hello wbudowane jest hello takie same jak innych aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="10db6-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="10db6-136">Zobacz dokumentację hello [Zarządzanie aplikacją sieci szkieletowej usług z hello interfejsu wiersza polecenia usługi sieć szkieletowa](service-fabric-application-lifecycle-sfctl.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="10db6-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="10db6-137">Parametry toothese polecenia można znaleźć w manifestach hello generowane w pakiecie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="10db6-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="10db6-138">Po wdrożeniu aplikacji hello, otwórz przeglądarkę i przejdź do [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) w [http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="10db6-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="10db6-139">Następnie rozwiń hello **aplikacji** węzeł i zwróć uwagę, że istnieją teraz wpis dla danego typu aplikacji i drugi dla hello pierwsze wystąpienie tego typu.</span><span class="sxs-lookup"><span data-stu-id="10db6-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="10db6-140">Uruchomić klienta testowego hello i przejściu w tryb failover</span><span class="sxs-lookup"><span data-stu-id="10db6-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="10db6-141">Projekty aktora nie działają samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="10db6-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="10db6-142">Wymagają one innej usługi lub klienta toosend ich wiadomości.</span><span class="sxs-lookup"><span data-stu-id="10db6-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="10db6-143">Szablon aktora Hello zawiera skrypt prosty test przy użyciu usługi aktora hello można toointeract.</span><span class="sxs-lookup"><span data-stu-id="10db6-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="10db6-144">Uruchom skrypt hello przy użyciu hello czujki narzędzie toosee hello dane wyjściowe hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="10db6-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="10db6-145">W narzędziu Service Fabric Explorer Znajdź węzeł obsługujący replikę podstawową hello hello usługi aktora.</span><span class="sxs-lookup"><span data-stu-id="10db6-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="10db6-146">W poniższym zrzucie ekranu hello jest węzeł 3.</span><span class="sxs-lookup"><span data-stu-id="10db6-146">In hello screenshot below, it is node 3.</span></span>

    ![Znajdowanie hello repliki podstawowej w narzędziu Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="10db6-148">Kliknij węzeł hello można znaleźć w poprzednim kroku hello, a następnie wybierz **Dezaktywuj (ponowne uruchomienie)** z menu Akcje hello.</span><span class="sxs-lookup"><span data-stu-id="10db6-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="10db6-149">Ta akcja powoduje ponowne uruchomienie jednego węzła w klastrze lokalnym wymuszenia pracy awaryjnej tooa replikę pomocniczą uruchomiona w innym węźle.</span><span class="sxs-lookup"><span data-stu-id="10db6-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="10db6-150">Jak to zrobić, należy zwrócić uwagę toohello w danych wyjściowych powitania klienta testowego i Uwaga tego licznika hello nadal tooincrement pomimo hello trybu failover.</span><span class="sxs-lookup"><span data-stu-id="10db6-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="10db6-151">Dodawanie więcej usług tooan istniejącej aplikacji</span><span class="sxs-lookup"><span data-stu-id="10db6-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="10db6-152">tooadd inną tooan aplikację usługi już utworzone przy użyciu `yo`, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="10db6-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="10db6-153">Zmień katalog główny toohello hello istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10db6-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="10db6-154">Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="10db6-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="10db6-155">Uruchom polecenie `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="10db6-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="10db6-156">Migrowanie z project.json too.csproj</span><span class="sxs-lookup"><span data-stu-id="10db6-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="10db6-157">Uruchamianie "dotnet migracji" w katalogu głównym projektu zostanie poddana migracji wszystkich hello project.json toocsproj format.</span><span class="sxs-lookup"><span data-stu-id="10db6-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="10db6-158">Aktualizacja hello projekt zawiera odwołania do odpowiednio toocsproj plików w projekcie.</span><span class="sxs-lookup"><span data-stu-id="10db6-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="10db6-159">Zaktualizuj hello pliki toocsproj nazwy pliku projektu w build.sh.</span><span class="sxs-lookup"><span data-stu-id="10db6-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10db6-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10db6-160">Next steps</span></span>

* [<span data-ttu-id="10db6-161">Dowiedz się więcej o usłudze Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="10db6-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="10db6-162">Interakcja z klastrów sieci szkieletowej usług za pomocą hello usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="10db6-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="10db6-163">Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="10db6-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="10db6-164">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="10db6-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
