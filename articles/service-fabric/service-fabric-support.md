---
title: "Więcej informacji na temat opcji obsługi sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Bilety obsługi platformy Azure obsługiwane wersje klastra sieci szkieletowej usług i łącza do pliku"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 78e68cff3a757cbbcd8dc6f53120e6a4af54591a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-service-fabric-support-options"></a>Opcje pomocy technicznej usługi Azure Service Fabric

Aby zapewnić odpowiednią obsługę Twoje obciążenie pracą aplikacji uruchomionych na klastrów sieci szkieletowej usług, firma Microsoft zainstalować różne opcje. W zależności od poziomu wsparcia potrzebne i ważność problemu, Pobierz wybierz opcje prawego. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Raport środowisko produkcyjne lub problemów z witryną na żywo lub zażądać płatnej pomocy technicznej platformy Azure

Do raportowania problemów z witryną na żywo w klastrze usługi sieć szkieletowa wdrożonego na platformie Azure, otwórz bilet pomocy technicznej professional [w portalu Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) lub [portalu pomocy technicznej firmy Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Dowiedz się więcej o:
 
- [Pomoc techniczna Professional firmy Microsoft dla systemu Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Premier pomocy technicznej firmy Microsoft](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Raport środowisko produkcyjne lub problemów z witryną na żywo lub zażądać płatnej pomocy technicznej dla autonomicznego klastrów sieci szkieletowej usług

Raportowanie problemów z witryną na żywo w klastrze usługi sieć szkieletowa wdrożonych lokalnie lub w innych chmur, otwórz bilet pomocy technicznej professional na [portalu pomocy technicznej firmy Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Dowiedz się więcej o:

- [Pomoc techniczna Professional firmy Microsoft dla lokalnego](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Premier pomocy technicznej firmy Microsoft](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Generuje raport sieć szkieletowa usług Azure 
Firma Microsoft skonfigurowano repozytorium GitHub, problemy z sieci szkieletowej usług raportowania.  Firma Microsoft są także aktywnie monitoruje następujące forach.

### <a name="github-repo"></a>Repozytorium GitHub 
Zgłoś problemy sieci szkieletowej usług Azure na [repozytorium git problemów dotyczących sieci szkieletowej usługi](https://github.com/Azure/service-fabric-issues). Tym repozytorium jest przeznaczony dla raportowania i śledzenia problemów z sieci szkieletowej usług Azure i wykonywania żądania małych funkcji. **Nie używaj to do raportu na żywo lokacji problemów**.

### <a name="stackoverflow-and-msdn-forums"></a>Fora StackOverflow i MSDN

[Tagu sieci szkieletowej usług w witrynie StackOverflow] [ stackoverflow] i [forum usługi Service Fabric w witrynie MSDN] [ msdn-forum] służą najlepsze zadać pytania dotyczące sposobu działania platformy i jak może wykonywać określone zadania z nim.

### <a name="azure-feedback-forum"></a>Azure forum opinii

[Forum opinii Azure dla platformy Service Fabric] [ uservoice-forum] najlepiej składania pomysły big funkcji ma produktu, jak firma Microsoft analizuje najpopularniejszych żądania są częścią naszego średnich planowanie długoterminowej. Firma Microsoft zachęca do rally obsługę sugestii w ramach społeczności.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Obsługiwane wersje usługi sieć szkieletowa usług.

Upewnij się, że klastra zawsze działa obsługiwana wersja usługi Service Fabric. Gdy firma Microsoft ogłaszamy wydanie programu nowa wersja usługi Service Fabric, poprzednia wersja jest oznaczony do zakończenia wsparcia po co najmniej 60 dni. Nowe wersje są ogłaszane [na blogu zespołu usługi sieć szkieletowa](https://blogs.msdn.microsoft.com/azureservicefabric/).

Można znaleźć w następujących dokumentach na więcej informacji na temat zachowania klastra uruchomiona obsługiwana wersja usługi Service Fabric.

- [Uaktualnienie wersji platformy Service Fabric w klastrze platformy Azure](service-fabric-cluster-upgrade.md)
- [Uaktualnienie wersji platformy Service Fabric w klastrze serwerów autonomicznych systemu windows](service-fabric-cluster-upgrade-windows-server.md)
 
Poniżej przedstawiono listę wersji platformy Service Fabric, które są obsługiwane i ich daty zakończenia wsparcia.

| **Klaster środowisko uruchomieniowe sieci szkieletowej usług** | **Zestaw SDK zgodne / wersje pakietu NuGet** | **Obsługa Data zakończenia** |
| --- | --- | --- |
| Wszystkie wersje klastra przed 5.3.121 |Mniejsze niż w wersji 2.3 |20 stycznia 2017 r. |
| 5.3.* |Mniejsze niż w wersji 2.3 |24 lutego 2017 r. |
| 5.4.* |Mniejsze niż lub równa wersji 2.4 |Może 10,2017     |
| 5.5.* |Mniejsze niż wersja 2.5 |Sierpnia 10,2017    |
| 5.6.* |Mniejsze niż w wersji 2.6 |Październik 13,2017    |
| 5.7.* |Mniejsze niż w wersji 2.7 |Bieżąca wersja i dlatego bez daty zakończenia

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Usługi sieci szkieletowej Podgląd wersje — nieobsługiwany do użytku produkcyjnego.
Od czasu do czasu firma Microsoft wersji mających znaczących funkcji, którą chcemy udostępnić opinię, które są wydawane jako podglądów. Te wersje preview należy używać tylko do celów testowych. Klastra produkcyjnego zawsze powinna działać obsługiwanych, stabilna wersja sieci szkieletowej usług. Wersja zapoznawcza zawsze zaczyna się od numeru wersji głównej i pomocniczej 255. Na przykład jeśli widzisz usługi sieć szkieletowa wersji 255.255.5703.949 tej wersji jest tylko do użycia w klastrach testu i jest w wersji zapoznawczej. Te wersje zapoznawcze również są ogłaszane na [blog zespołu usługi sieć szkieletowa](https://blogs.msdn.microsoft.com/azureservicefabric) i będą zawierały wszystkie szczegółowe informacje o funkcjach dostępnych.

Nie ma żadnych opcji płatnej pomocy technicznej dla tych wersji zapoznawczej. Użyj jednej z opcji wymienionych w obszarze [wystawia sieć szkieletowa usług Azure raport](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) aby zadać pytania lub wyrazić swoją opinię.

## <a name="next-steps"></a>Następne kroki

- [Uaktualnienie wersji sieci szkieletowej usług w klastrze platformy Azure](service-fabric-cluster-upgrade.md)
- [Uaktualnienie wersji platformy Service Fabric w klastrze serwerów autonomicznych systemu windows](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
