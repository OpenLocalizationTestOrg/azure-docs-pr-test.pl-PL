---
title: "aaaAzure ciągu połączenia magazynu obrazów platformy Service Fabric | Dokumentacja firmy Microsoft"
description: "Zrozumienie parametry połączenia magazynu obraz powitania"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Zrozumienie hello element ImageStoreConnectionString ustawienie

W niektórych części dokumentacji firma Microsoft krótko wspomina hello istnienie parametrem "Element ImageStoreConnectionString" bez opisujące naprawdę to. I po przejściu przez artykułu, takich jak [Wdróż i usunąć aplikacje przy użyciu programu PowerShell][10], prawdopodobnie wszystkie zrobisz jest kopiowania i wklejania hello wartość wyświetlaną w manifeście klastra hello hello docelowego klaster. Dlatego ustawienie hello muszą być można skonfigurować dla klastra, ale po utworzeniu klastra za pośrednictwem hello [portalu Azure][11], nie tooconfigure opcja to ustawienie i jego zawsze "fabric: magazynu ImageStore" nie istnieje. Co to jest celem hello następnie to ustawienie?

![Manifest klastra][img_cm]

Sieć szkieletowa usług uruchomiona jako platformę na potrzeby wewnętrzne firmy Microsoft przez wiele różnych zespołów, więc w dużym stopniu dostosowywane niektórych aspektów — Witaj "Image Store" jest jednym z aspektów. Zasadniczo hello Image Store jest podłączany repozytorium do przechowywania pakietów aplikacji. Gdy aplikacja jest wdrożony tooa węzła w klastrze hello, ten węzeł pobiera zawartość pakietu aplikacji hello z hello magazynu obrazów. Element ImageStoreConnectionString Hello to ustawienie obejmuje wszystkie informacje niezbędne powitania dla klientów i węzłów toofind hello poprawne Image Store dla danego klastra.

Obecnie istnieją trzy możliwe typy dostawców magazynu obrazów i ich odpowiednie parametry połączenia są następujące:

1. Usługa składnika Image Store: "fabric: magazynu ImageStore"

2. System plików: "Ścieżka systemu file:[file]"

3. Magazyn Azure: "xstore: defaultendpointsprotocol = https; AccountName = [...]; AccountKey = [...]; Kontener = [...] "

Witaj dostawcy typu używane w środowisku produkcyjnym są hello usługi magazynu obrazu, usługa systemowa utrwalonego stanowe widać w narzędziu Service Fabric Explorer. 

![Usługi magazynu obrazów][img_is]

Witaj hostingu magazynu obrazów w usłudze system w obrębie samego klastra hello eliminuje zależności zewnętrznych dla repozytorium pakietów hello i daje większą kontrolę nad hello lokalizacji magazynu. Przyszłe ulepszenia wokół hello magazynu obrazów są prawdopodobnie tootarget hello Image Store dostawcy po raz pierwszy, jeśli nie wyłącznie. Hello parametry połączenia dla dostawcy usługi magazynu obraz powitania nie ma żadnych unikatowych informacji, że powitania klienta jest już połączony toohello klastra docelowego. powitania klienta musi tylko tooknow protokołów przeznaczonych dla usługi systemowej hello powinien być używany.

Hello dostawcy systemu plików jest używany zamiast hello obrazu usługi magazynu lokalnego klastrów jeden pole podczas rozwoju toobootstrap hello klastra nieco szybciej. Różnica Hello jest zwykle mały, ale jest przydatne optymalizacji dla większość osób podczas tworzenia. Jego możliwe toodeploy lokalnego pole jeden klaster z hello również inne dostawcy magazynu, ale zwykle nie istnieje przyczyna toodo tak, ponieważ przepływ pracy Tworzenie i testowanie hello hello sama niezależnie od dostawcy. Innych niż to użycie dostawcy systemu plików i usługi Azure Storage hello istnieje tylko do obsługi starszych wersji.

Dlatego podczas hello element ImageStoreConnectionString jest konfigurowany, zazwyczaj użycia hello domyślne ustawienie. Podczas publikowania tooAzure za pośrednictwem [programu Visual Studio][12], parametr hello jest ustawiane automatycznie odpowiednio. Tooclusters wdrażaniem programowym hostowana na platformie Azure ciąg połączenia hello jest zawsze "fabric: magazynu ImageStore". Chociaż w razie wątpliwości, jego wartość zawsze można sprawdzić przez pobranie hello manifestu klastra przez [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), lub [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Testowanie lokalnie i klastrów produkcyjnych zawsze powinna być również dostawcy usługi magazynu obrazu hello toouse skonfigurowany.

### <a name="next-steps"></a>Następne kroki
[Wdrażanie i usunąć aplikacje przy użyciu programu PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
