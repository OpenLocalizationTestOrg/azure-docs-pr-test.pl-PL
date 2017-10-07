---
title: aaaAzure zestawu SDK dla platformy .NET 2.6 informacje o wersji
description: Informacje o wersji zestawu Azure SDK dla platformy .NET w wersji 2.6
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Informacje o wersji zestawu Azure SDK dla platformy .NET w wersji 2.6
Ten dokument zawiera informacje o wersji hello hello Azure SDK w wersji .NET 2.6. 

2.6 zestawu SDK platformy Azure mogą programować aplikacje usługi chmury (PaaS) przeznaczonych dla platformy .NET w wersji 4.5.2 i .NET 4.6 pod warunkiem, że ręczne zainstalowanie hello docelowej platformy .NET Framework na powitania roli usługi w chmurze. Zobacz [zainstalować program .NET dla roli usługi chmury](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Aktualizacje usługi Service Bus
* Centra zdarzeń: 
  
  * Kontrola dostępu docelowej umożliwia teraz podczas wysyłania zdarzeń w przypadku wystawianego dodatkowej wydawcę punktu końcowego usługi Event hubs.
  * Dodatkowe stabilność i poprawy dodać tooEvent koncentratory funkcji.
  * Dodawanie obsługi protokołu Amqp za pośrednictwem protokołu WebSocket do obsługi wiadomości i usługi Event Hubs.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Narzędzia HDInsight Tools for Visual Studio aktualizacji
* **Rozszerzenie IntelliSense**: sugestię zdalnych metadanych
  
    Narzędzia HDInsight Tools for Visual Studio obsługuje obecnie pobierania zdalnych metadanych podczas edycji skryptu Hive. Na przykład możesz wpisać **wybierz * FROM** i zostaną wyświetlone wszystkie hello nazwy tabeli. Ponadto nazwy kolumn hello będzie wyświetlana po określeniu tabeli.
* **Obsługa emulatora usługi HDInsight**
  
    Obecnie narzędzia HDInsight Tools for łączenie tooHDInsight emulatora, więc można utworzyć skrypty programu Hive lokalnie bez wprowadzania jakichkolwiek kosztów obsługi programu Visual Studio wykonujących te skrypty przed klastrów usługi HDInsight. 
  
    Aby uzyskać więcej informacji, zobacz zbyt[tego podręcznika](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Narzędzia HDInsight Tools for Visual Studio obsługują ogólnego klastrów platformy Hadoop** (wersja zapoznawcza)
  
    Narzędzia HDInsight Tools for Visual Studio obsługują teraz ogólnego klastrów platformy Hadoop, dzięki czemu można użyć narzędzia HDInsight Tools dla Visual Studio toodo hello poniżej:
  
  * Połącz klaster tooyour 
  * Pisanie zapytań Hive z rozszerzoną obsługę funkcji IntelliSense — autouzupełniania, 
  * Wyświetl wszystkie zadania hello w klastra za pomocą intuicyjnego interfejsu użytkownika. 
    
    Aby uzyskać więcej informacji, zobacz zbyt[tego podręcznika](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Operacji aktualizacji pamięci podręcznej w roli
* **Pamięć podręczna w roli** został zaktualizowany toouse **zestawu SDK usługi Magazyn Microsoft Azure** wersji 4.3. Do tej pory hello **pamięci podręcznej w roli** został przy użyciu zestawu SDK usługi Magazyn Azure w wersji 1.7.
  
    Klientów przy użyciu 2.5 zestawu SDK platformy Azure lub poniżej należy zaktualizować tooAzure 2.6 zestawu SDK i Przenieś toohello nowej wersji zestawu SDK usługi Magazyn Azure. 
  
    W tej wersji usługi Azure Storage czasu 2011-08-18 jest zaplanowane toobe 1 sierpnia 2016 roku usunięta. Wszelkie migracji pamięci podręcznej w roli z 2.5 zestawu SDK platformy Azure lub poniżej too2.6 musi być ukończenia tego czasu. Aby uzyskać więcej informacji na wycofanie hello Azure Storage wersji 2011-08-18, zobacz [aktualizację usuwania wersji magazynu usługi Microsoft Azure: rozszerzenie too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Możemy Cię o hello 30 listopada 2016 r. wycofania dla usługi zarządzana pamięć podręczna Azure i pamięci podręcznej na roli Azure. Zaleca się przeprowadzenie migracji tooAzure pamięci podręcznej Redis w ramach przygotowań do tego wycofania. Aby uzyskać więcej informacji na daty i wskazówki dotyczące migracji, zobacz [oferty które pamięć podręczna Azure jest dla mnie odpowiednia?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Narzędzia usługi aplikacji Azure
Witaj, następujące elementy zostały zaktualizowane w wersji hello Azure SDK w wersji 2.6.

* Publikowanie Azure rozszerzone aplikacje interfejsu API Azure tooinclude jako cel wdrożenia.
* Aplikacje interfejsu API i Inicjowanie obsługi funkcji udostępniania funkcji tooenable użytkownikom tworzenie aplikacji interfejsu API.
* Serwer Explorer zmienić tooreflect nowego węzła usługi aplikacji, przy użyciu aplikacji interfejsu API, mobilne i sieci Web pogrupowany według grupy zasobów.
* Dodaj klienta aplikacji interfejsu API Azure gestu dodane projektów toomost C#, który spowoduje włączenie automatycznego generowania włączone Swagger interfejsu API aplikacji działających w subskrypcji platformy Azure przez użytkownika.
* Aplikacje interfejsu API narzędzi i węzły usługi App Service w Eksploratorze serwera są dostępne w programie Visual Studio 2013 tylko. 

## <a name="azure-resource-manager-tools-updates"></a>Aktualizacje narzędzia Menedżera zasobów Azure
Narzędzia Menedżera zasobów Azure Hello zostały zaktualizowane tooinclude szablonów dla maszyn wirtualnych, sieci i magazynu. Proces edycji JSON Hello został zaktualizowany tooinclude nowy widok konspektu szablony i hello możliwości tooedit hello korzystania z wstawek JSON. Szablony wdrożone w programie Visual Studio za pomocą skryptu programu PowerShell dostarczane z hello projektu, więc zmiany wprowadzone toohello skrypt będzie używany przez Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Ulepszenia diagnostyki dla usług w chmurze
2.6 zestawu SDK platformy Azure oferuje ponownie obsługę zbierania dzienników diagnostycznych w emulatorze obliczeń platformy Azure hello i przekazywanie ich toodevelopment magazynu. Rejestruje wszystkie diagnostyki (w tym aplikacji śledzenia dzienników, śledzenie dzienniki systemu Windows (ETW), liczników wydajności, infrastruktury dzienniki zdarzeń dzienników i windows zdarzeń) generowane podczas aplikacja hello działa w emulatorze hello może być przeniesione toodevelopment tooverify magazynu, czy Twoje rejestrowania diagnostyki działa na komputerze lokalnym. 

Teraz można określić Hello konto magazynu diagnostyki w pliku konfiguracji (cscfg) usługi hello dzięki czemu można łatwiej toouse diagnostyki różnych kont magazynu dla różnych środowisk. Brak niektórych istotnych różnic między jak parametry połączenia hello działał 2.4 zestawu SDK platformy Azure i 2.6 zestawu SDK platformy Azure. Aby uzyskać więcej informacji na jak parametry połączenia magazynu diagnostyki hello toouse i jak wpływa na swoje projekty zobacz [Konfigurowanie diagnostyki dla usług w chmurze Azure](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Fundamentalne zmiany
### <a name="azure-resource-manager-tools"></a>Narzędzia Menedżera zasobów Azure
* Witaj **projekty wdrażania chmury** typu dostępne w hello 2.5 zestawu SDK platformy Azure została zmieniona zbyt projektu**grupy zasobów platformy Azure**.
* **Projekty wdrażania w chmurze** typu projektów utworzonych w hello 2.5 zestawu SDK platformy Azure mogą być używane w wersji 2.6, ale wdrażanie hello szablonu z programu Visual Studio zakończy się niepowodzeniem. Jednak wdrażania z hello skrypt programu PowerShell będą nadal działać tak jak poprzednio.  Aby uzyskać informacje na temat toouse **projekty wdrażania chmury** w wersji 2.6 przeczytać ten tekst [post](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Znane problemy
* Zbierania dzienników diagnostycznych w emulatorze hello wymaga 64-bitowym systemie operacyjnym. Dzienniki diagnostyczne nie będą zbierane podczas uruchamiania na 32-bitowym systemie operacyjnym. Nie ma to wpływu na innych funkcji emulatora. 
* Azure 2.6 SDK wydanej w dniu 2015-4-29 ma dwa problemy: 
  
  * Nie można załadować uniwersalnej aplikacji w programie Visual Studio 2015, po zainstalowaniu na komputerze hello Azure SDK w wersji 2.6.
  * Debugowanie projektu usługi w chmurze nie powiedzie się w programie Visual Studio 2013 i Visual Studio 2015, gdy przestanie odpowiadać Visual Studio i ulega awarii podczas wyświetlania okna dialogowego z wiadomości powitania "Konfigurowanie diagnostyki dla emulatora".
    
    Aktualizacja tooAzure zestawu SDK w wersji 2.6 został wydany 2015-5-18. Wersja aktualizacji Hello jest 2.6.30508.1601; go rozwiązuje dwa problemy opisane powyżej. Można zidentyfikować hello kompilacji hello SDK Panel sterowania -> programy i funkcje -> Microsoft Azure Tools dla programu Microsoft Visual Studio 2013 – v 2.6. w kolumnie wersja Hello wyświetli hello numer kompilacji.
    
    Jeśli nadal są ukierunkowane hello powyżej problemy, zainstaluj hello najnowszej wersji hello Azure SDK 2.6 dla [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) lub [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Zobacz też
[Obsługa i wycofania informacje dotyczące hello zestaw Azure SDK for .NET i interfejsów API](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

