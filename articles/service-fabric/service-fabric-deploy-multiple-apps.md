---
title: "aaaDeploy aplikacji Node.js, która używa bazy danych MongoDB | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące toopackage wielu klastra usługi sieć szkieletowa usług Azure tooan toodeploy gościa pliki wykonywalne"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="aaa47-103">Wdrażanie wielu aplikacji wykonywalnych gości</span><span class="sxs-lookup"><span data-stu-id="aaa47-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="aaa47-104">W tym artykule przedstawiono sposób toopackage i wdrożyć wiele gościa tooAzure pliki wykonywalne sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="aaa47-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="aaa47-105">Dla odczytu sposób za tworzenie i wdrażanie pojedynczego pakietu sieci szkieletowej usług[wdrażanie gościa tooService wykonywalnego sieci szkieletowej](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="aaa47-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="aaa47-106">Gdy w tym przewodniku przedstawiono, jak toodeploy aplikacji przy użyciu środowiska Node.js fronton, który używa produktu MongoDB jako hello magazynu danych, można stosować hello kroki tooany aplikacji, która zawiera zależności na inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="aaa47-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="aaa47-107">Można użyć programu Visual Studio tooproduce hello aplikacji pakiet, który zawiera wiele plików wykonywalnych gościa.</span><span class="sxs-lookup"><span data-stu-id="aaa47-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="aaa47-108">Zobacz [toopackage przy użyciu programu Visual Studio istniejącej aplikacji](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="aaa47-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="aaa47-109">Po dodaniu pliku wykonywalnego gościa pierwszy hello, kliknij prawym przyciskiem myszy projekt aplikacji hello i wybierz hello **Dodaj -> Usługa sieci szkieletowej usług nowe** tooadd hello drugi gościa projekt wykonywalny toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="aaa47-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="aaa47-110">Uwaga: Jeśli wybierzesz opcję toolink hello źródła w hello projekt programu Visual Studio, tworzenie hello rozwiązania Visual Studio, będzie upewnij się, że pakiet aplikacji to maksymalnie toodate ze zmianami w źródle hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="aaa47-111">Przykłady</span><span class="sxs-lookup"><span data-stu-id="aaa47-111">Samples</span></span>
* [<span data-ttu-id="aaa47-112">Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa</span><span class="sxs-lookup"><span data-stu-id="aaa47-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="aaa47-113">Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="aaa47-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="aaa47-114">Ręcznie pakietu hello wielu aplikacja wykonywalna gościa</span><span class="sxs-lookup"><span data-stu-id="aaa47-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="aaa47-115">Można też ręcznie pakietu pliku wykonywalnego gościa hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="aaa47-116">Dla pakietów ręcznego hello, w tym artykule wykorzystano hello sieci szkieletowej usług pakowania narzędzia, które są dostępne pod adresem [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="aaa47-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="aaa47-117">Tworzenie pakietów hello aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="aaa47-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="aaa47-118">W tym artykule przyjęto, że Node.js nie jest zainstalowane na powitania węzłów w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="aaa47-119">W rezultacie należy tooadd Node.exe toohello katalog główny aplikacji węzeł przed opakowania.</span><span class="sxs-lookup"><span data-stu-id="aaa47-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="aaa47-120">Hello struktura katalogów aplikacji Node.js hello (przy użyciu aparatu Jade szablonu i platforma sieci web Express) powinien wyglądać podobnie toohello, jeden poniżej:</span><span class="sxs-lookup"><span data-stu-id="aaa47-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="aaa47-121">Jako kolejny krok tworzenia pakietu aplikacji dla hello aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="aaa47-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="aaa47-122">Poniższy kod Hello tworzy pakiet aplikacji sieci szkieletowej usług, który zawiera hello aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="aaa47-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="aaa47-123">Poniżej znajduje się opis hello parametrów, które są używane:</span><span class="sxs-lookup"><span data-stu-id="aaa47-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="aaa47-124">**/ source** punktów toohello katalogu aplikacji hello, który powinien być spakowany.</span><span class="sxs-lookup"><span data-stu-id="aaa47-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="aaa47-125">**/ target** definiuje hello katalogu, w których hello można utworzyć pakietu.</span><span class="sxs-lookup"><span data-stu-id="aaa47-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="aaa47-126">Ten katalog zawiera inny niż katalog źródłowy hello toobe.</span><span class="sxs-lookup"><span data-stu-id="aaa47-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="aaa47-127">**elementów/appname** definiuje nazwę aplikacji hello hello istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaa47-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="aaa47-128">Jest ważne toounderstand przekłada toohello nazwy usługi w manifeście hello, a nie toohello Nazwa aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="aaa47-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="aaa47-129">**/exe** definiuje hello pliku wykonywalnego, że sieć szkieletowa usług powinien toolaunch, w tym przypadku `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="aaa47-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="aaa47-130">**/ma** definiuje argumentu hello są używane toolaunch hello pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="aaa47-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="aaa47-131">Ponieważ nie zainstalowano środowiska Node.js, sieci szkieletowej usług wymaga serwera sieci web Node.js hello toolaunch, wykonując `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="aaa47-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="aaa47-132">`/ma:'bin/www'`Określa, że toouse narzędzia do tworzenia pakietów hello `bin/ma` jako hello argument node.exe.</span><span class="sxs-lookup"><span data-stu-id="aaa47-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="aaa47-133">**/ Typ aplikacji** definiuje nazwy typu aplikacji hello w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="aaa47-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="aaa47-134">Podczas przeglądania katalogu toohello, który został określony w parametrze/TARGET hello, można zauważyć, że narzędzia hello został utworzony pakiet pełni funkcjonalnej sieci szkieletowej usług, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="aaa47-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="aaa47-135">Witaj wygenerowanego pliku ServiceManifest.xml ma teraz sekcja, która opisuje, jak serwer sieci web Node.js hello powinna być uruchamiana, jak pokazano w poniższy fragment kodu hello:</span><span class="sxs-lookup"><span data-stu-id="aaa47-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="aaa47-136">W tym przykładzie serwer sieci web Node.js hello nasłuchuje tooport 3000, więc należy tooupdate informacje o punkcie końcowym hello w pliku ServiceManifest.xml hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="aaa47-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="aaa47-137">Tworzenie pakietów hello aplikacji bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="aaa47-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="aaa47-138">Teraz, gdy spakowaniu aplikacji Node.js hello można teraz i pakietu bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="aaa47-139">Jak wspomniano wcześniej, hello kroki przechodzących przez obecnie nie są określone tooNode.js i bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="aaa47-140">W rzeczywistości mają one zastosowanie tooall aplikacje, które mają toobe w jednej aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="aaa47-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="aaa47-141">toopackage bazy danych MongoDB ma toomake się, że pakiet Mongod.exe i Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="aaa47-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="aaa47-142">Oba pliki binarne znajdują się w hello `bin` katalogu z katalogu instalacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="aaa47-143">Struktura katalogów Hello wygląda podobnie toohello, co poniżej.</span><span class="sxs-lookup"><span data-stu-id="aaa47-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="aaa47-144">Usługi sieć szkieletowa usług musi toostart bazy danych MongoDB z toohello podobne polecenie jedną poniżej, więc należy toouse hello `/ma` parametru podczas tworzenia pakietu bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="aaa47-145">Hello dane nie są są zachowywane w przypadku hello awarii węzła, jeśli katalog danych MongoDB hello zostanie umieszczony na powitania katalogu lokalnego węzła hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="aaa47-146">Należy używać magazynu trwałego lub wdrożenie zestawu utratę danych tooprevent kolejności replik bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="aaa47-147">W powłoce poleceń programu PowerShell lub hello możemy Uruchom narzędzie tworzenia pakietów hello z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="aaa47-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="aaa47-148">W kolejności tooadd MongoDB tooyour pakiet sieci szkieletowej usług aplikacji, należy się, że parametr/target hello wskazuje toohello toomake tym samym katalogu, który już zawiera manifest aplikacji hello wraz z aplikacji Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="aaa47-149">Należy się upewnić, że używasz toomake hello tej samej nazwy atrybutów ApplicationType.</span><span class="sxs-lookup"><span data-stu-id="aaa47-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="aaa47-150">Umożliwia przeglądanie katalogu toohello i sprawdź, czy narzędzie jakie hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="aaa47-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="aaa47-151">Jak widać, narzędzie hello dodany nowy katalog toohello folder bazy danych MongoDB, zawierający dane binarne bazy danych MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="aaa47-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="aaa47-152">Po otwarciu hello `ApplicationManifest.xml` pliku, zobaczysz tego pakietu hello zawiera teraz hello aplikacji Node.js i bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="aaa47-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="aaa47-153">Witaj poniższy kod hello zawartości hello manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaa47-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="aaa47-154">Publikowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="aaa47-154">Publishing hello application</span></span>
<span data-ttu-id="aaa47-155">ostatni krok Hello jest toopublish hello aplikacji toohello lokalnego klastra sieci szkieletowej usług za pomocą skryptów środowiska PowerShell hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="aaa47-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="aaa47-156">Gdy aplikacja hello jest klaster lokalny pomyślnie opublikowano toohello, będzie dostępny hello aplikacji Node.js na porcie hello, który mamy wprowadzony w manifeście usługi hello aplikacji Node.js hello — na przykład http://localhost: 3000.</span><span class="sxs-lookup"><span data-stu-id="aaa47-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="aaa47-157">W tym samouczku już wspomniano, jak tooeasily pakiety dwóch istniejących aplikacji jednej aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="aaa47-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="aaa47-158">Przedstawiono również sposób toodeploy on tooService sieci szkieletowej, którą mogą korzystać z niektórych hello funkcji sieci szkieletowej usług, takich jak wysoka dostępność i kondycji systemu integracji.</span><span class="sxs-lookup"><span data-stu-id="aaa47-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="aaa47-159">Dodawanie więcej gościa pliki wykonywalne tooan istniejących aplikacji przy użyciu narzędzia Yeoman w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="aaa47-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="aaa47-160">tooadd inną tooan aplikację usługi już utworzone przy użyciu `yo`, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="aaa47-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="aaa47-161">Zmień katalog główny toohello hello istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aaa47-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="aaa47-162">Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.</span><span class="sxs-lookup"><span data-stu-id="aaa47-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="aaa47-163">Uruchom `yo azuresfguest:AddService` oraz hello niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="aaa47-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa47-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aaa47-164">Next steps</span></span>
* <span data-ttu-id="aaa47-165">Dowiedz się więcej o wdrażaniu kontenerów [sieci szkieletowej usług i kontenery — omówienie](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="aaa47-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="aaa47-166">Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa</span><span class="sxs-lookup"><span data-stu-id="aaa47-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="aaa47-167">Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST</span><span class="sxs-lookup"><span data-stu-id="aaa47-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
