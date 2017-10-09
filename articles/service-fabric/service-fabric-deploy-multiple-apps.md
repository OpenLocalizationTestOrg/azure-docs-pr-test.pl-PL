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
# <a name="deploy-multiple-guest-executables"></a>Wdrażanie wielu aplikacji wykonywalnych gości
W tym artykule przedstawiono sposób toopackage i wdrożyć wiele gościa tooAzure pliki wykonywalne sieci szkieletowej usług. Dla odczytu sposób za tworzenie i wdrażanie pojedynczego pakietu sieci szkieletowej usług[wdrażanie gościa tooService wykonywalnego sieci szkieletowej](service-fabric-deploy-existing-app.md).

Gdy w tym przewodniku przedstawiono, jak toodeploy aplikacji przy użyciu środowiska Node.js fronton, który używa produktu MongoDB jako hello magazynu danych, można stosować hello kroki tooany aplikacji, która zawiera zależności na inną aplikację.   

Można użyć programu Visual Studio tooproduce hello aplikacji pakiet, który zawiera wiele plików wykonywalnych gościa. Zobacz [toopackage przy użyciu programu Visual Studio istniejącej aplikacji](service-fabric-deploy-existing-app.md). Po dodaniu pliku wykonywalnego gościa pierwszy hello, kliknij prawym przyciskiem myszy projekt aplikacji hello i wybierz hello **Dodaj -> Usługa sieci szkieletowej usług nowe** tooadd hello drugi gościa projekt wykonywalny toohello rozwiązania. Uwaga: Jeśli wybierzesz opcję toolink hello źródła w hello projekt programu Visual Studio, tworzenie hello rozwiązania Visual Studio, będzie upewnij się, że pakiet aplikacji to maksymalnie toodate ze zmianami w źródle hello. 

## <a name="samples"></a>Przykłady
* [Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>Ręcznie pakietu hello wielu aplikacja wykonywalna gościa
Można też ręcznie pakietu pliku wykonywalnego gościa hello. Dla pakietów ręcznego hello, w tym artykule wykorzystano hello sieci szkieletowej usług pakowania narzędzia, które są dostępne pod adresem [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Tworzenie pakietów hello aplikacji Node.js
W tym artykule przyjęto, że Node.js nie jest zainstalowane na powitania węzłów w klastrze usługi sieć szkieletowa hello. W rezultacie należy tooadd Node.exe toohello katalog główny aplikacji węzeł przed opakowania. Hello struktura katalogów aplikacji Node.js hello (przy użyciu aparatu Jade szablonu i platforma sieci web Express) powinien wyglądać podobnie toohello, jeden poniżej:

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

Jako kolejny krok tworzenia pakietu aplikacji dla hello aplikacji Node.js. Poniższy kod Hello tworzy pakiet aplikacji sieci szkieletowej usług, który zawiera hello aplikacji Node.js.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Poniżej znajduje się opis hello parametrów, które są używane:

* **/ source** punktów toohello katalogu aplikacji hello, który powinien być spakowany.
* **/ target** definiuje hello katalogu, w których hello można utworzyć pakietu. Ten katalog zawiera inny niż katalog źródłowy hello toobe.
* **elementów/appname** definiuje nazwę aplikacji hello hello istniejącej aplikacji. Jest ważne toounderstand przekłada toohello nazwy usługi w manifeście hello, a nie toohello Nazwa aplikacji sieci szkieletowej usług.
* **/exe** definiuje hello pliku wykonywalnego, że sieć szkieletowa usług powinien toolaunch, w tym przypadku `node.exe`.
* **/ma** definiuje argumentu hello są używane toolaunch hello pliku wykonywalnego. Ponieważ nie zainstalowano środowiska Node.js, sieci szkieletowej usług wymaga serwera sieci web Node.js hello toolaunch, wykonując `node.exe bin/www`.  `/ma:'bin/www'`Określa, że toouse narzędzia do tworzenia pakietów hello `bin/ma` jako hello argument node.exe.
* **/ Typ aplikacji** definiuje nazwy typu aplikacji hello w sieci szkieletowej usług.

Podczas przeglądania katalogu toohello, który został określony w parametrze/TARGET hello, można zauważyć, że narzędzia hello został utworzony pakiet pełni funkcjonalnej sieci szkieletowej usług, jak pokazano poniżej:

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
Witaj wygenerowanego pliku ServiceManifest.xml ma teraz sekcja, która opisuje, jak serwer sieci web Node.js hello powinna być uruchamiana, jak pokazano w poniższy fragment kodu hello:

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
W tym przykładzie serwer sieci web Node.js hello nasłuchuje tooport 3000, więc należy tooupdate informacje o punkcie końcowym hello w pliku ServiceManifest.xml hello, jak pokazano poniżej.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Tworzenie pakietów hello aplikacji bazy danych MongoDB
Teraz, gdy spakowaniu aplikacji Node.js hello można teraz i pakietu bazy danych MongoDB. Jak wspomniano wcześniej, hello kroki przechodzących przez obecnie nie są określone tooNode.js i bazy danych MongoDB. W rzeczywistości mają one zastosowanie tooall aplikacje, które mają toobe w jednej aplikacji sieci szkieletowej usług.  

toopackage bazy danych MongoDB ma toomake się, że pakiet Mongod.exe i Mongo.exe. Oba pliki binarne znajdują się w hello `bin` katalogu z katalogu instalacji bazy danych MongoDB. Struktura katalogów Hello wygląda podobnie toohello, co poniżej.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Usługi sieć szkieletowa usług musi toostart bazy danych MongoDB z toohello podobne polecenie jedną poniżej, więc należy toouse hello `/ma` parametru podczas tworzenia pakietu bazy danych MongoDB.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> Hello dane nie są są zachowywane w przypadku hello awarii węzła, jeśli katalog danych MongoDB hello zostanie umieszczony na powitania katalogu lokalnego węzła hello. Należy używać magazynu trwałego lub wdrożenie zestawu utratę danych tooprevent kolejności replik bazy danych MongoDB.  
>
>

W powłoce poleceń programu PowerShell lub hello możemy Uruchom narzędzie tworzenia pakietów hello z hello następujące parametry:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

W kolejności tooadd MongoDB tooyour pakiet sieci szkieletowej usług aplikacji, należy się, że parametr/target hello wskazuje toohello toomake tym samym katalogu, który już zawiera manifest aplikacji hello wraz z aplikacji Node.js hello. Należy się upewnić, że używasz toomake hello tej samej nazwy atrybutów ApplicationType.

Umożliwia przeglądanie katalogu toohello i sprawdź, czy narzędzie jakie hello został utworzony.

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
Jak widać, narzędzie hello dodany nowy katalog toohello folder bazy danych MongoDB, zawierający dane binarne bazy danych MongoDB hello. Po otwarciu hello `ApplicationManifest.xml` pliku, zobaczysz tego pakietu hello zawiera teraz hello aplikacji Node.js i bazy danych MongoDB. Witaj poniższy kod hello zawartości hello manifestu aplikacji.

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

### <a name="publishing-hello-application"></a>Publikowanie aplikacji hello
ostatni krok Hello jest toopublish hello aplikacji toohello lokalnego klastra sieci szkieletowej usług za pomocą skryptów środowiska PowerShell hello poniżej:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Gdy aplikacja hello jest klaster lokalny pomyślnie opublikowano toohello, będzie dostępny hello aplikacji Node.js na porcie hello, który mamy wprowadzony w manifeście usługi hello aplikacji Node.js hello — na przykład http://localhost: 3000.

W tym samouczku już wspomniano, jak tooeasily pakiety dwóch istniejących aplikacji jednej aplikacji sieci szkieletowej usług. Przedstawiono również sposób toodeploy on tooService sieci szkieletowej, którą mogą korzystać z niektórych hello funkcji sieci szkieletowej usług, takich jak wysoka dostępność i kondycji systemu integracji.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Dodawanie więcej gościa pliki wykonywalne tooan istniejących aplikacji przy użyciu narzędzia Yeoman w systemie Linux

tooadd inną tooan aplikację usługi już utworzone przy użyciu `yo`, wykonaj następujące kroki hello: 
1. Zmień katalog główny toohello hello istniejącej aplikacji.  Na przykład `cd ~/YeomanSamples/MyApplication`, jeśli `MyApplication` to aplikacja hello utworzone przez narzędzia Yeoman.
2. Uruchom `yo azuresfguest:AddService` oraz hello niezbędne informacje.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o wdrażaniu kontenerów [sieci szkieletowej usług i kontenery — omówienie](service-fabric-containers-overview.md)
* [Przykład dla pakowanie i wdrażanie pliku wykonywalnego gościa](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Przykład dwóch gościa pliki wykonywalne (C# i nodejs) podczas komunikacji za pomocą usługi nazewnictwa hello za pomocą usługi REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
