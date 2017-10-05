---
title: What's New in Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o najnowszych funkcji w zestawie narzędzi programu Azure for IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 23714856f0f778be04cf321e0726b53ade430f57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>What's New in Azure Toolkit for IntelliJ
## <a name="azure-toolkit-for-intellij-releases"></a>Azure narzędzi dla wersji IntelliJ
Ten artykuł zawiera informacje o różnych wersjach i najnowsze aktualizacje do zestawu narzędzi Azure for IntelliJ.

> [!NOTE]
> Dostępna jest również zestaw narzędzi platformy Azure dla programu Eclipse IDE. Aby uzyskać więcej informacji, zobacz [zestawu narzędzi platformy Azure dla programu Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 kwietnia 2017 r.
Zestaw narzędzi platformy Azure dla IntelliJ - wersji z kwietnia 2017 zawiera następujące udoskonalenia:

* **Udoskonalone środowisko w znak Azure**: narzędzi Azure dla IntelliJ obsługuje teraz dwie metody logowania do konta platformy Azure: *Interactive* i *automatycznego*. Aby uzyskać więcej informacji, zobacz [Azure znak w instrukcje dotyczące narzędzi Azure dla IntelliJ].
* **Publikowanie za pomocą kontenerów Docker**: teraz można publikować aplikacje sieci web jako kontenery Docker for IntelliJ przy użyciu zestawu narzędzi platformy Azure. Aby uzyskać więcej informacji, zobacz [sposób publikowania aplikacji sieci Web jako kontener Docker przy użyciu zestawu narzędzi Azure for IntelliJ].
* **Zarządzanie kontem magazynu**: narzędzi Azure dla IntelliJ obsługuje teraz Zarządzanie kont magazynu z widoku Eksploratora Azure. Aby uzyskać więcej informacji, zobacz [Zarządzanie kontami magazynu przy użyciu Eksploratora Azure for IntelliJ].
* **Zarządzanie maszynami wirtualnymi**: narzędzi Azure dla IntelliJ obsługuje teraz Zarządzanie maszyn wirtualnych z okna narzędzia Eksplorator Azure. Aby uzyskać więcej informacji, zobacz [Zarządzanie maszyn wirtualnych za pomocą Eksploratora Azure for IntelliJ].
* **Usunięcie zdalne debugowanie Obsługa**. Zdalne debugowanie aplikacji sieci web Java w usłudze Azure App Service została usunięta z zestawu narzędzi Azure for IntelliJ; jest to niezbędne do rozwiązania niektórych problemów, których klienci zgłaszali problemy przy użyciu zestawu narzędzi.

### <a name="august-26-2016"></a>26 sierpnia 2016 r.
Zestaw narzędzi platformy Azure dla IntelliJ - wersji sierpnia 2016 zawiera następujące udoskonalenia:

* **Dystrybucje niestandardowych JDK**. Zestaw narzędzi platformy Azure dla IntelliJ obsługuje teraz określanie i wdrażanie dowolnego wersji JDK do kontenera Twojej aplikacji sieci Web platformy Azure:
  * Oprócz JDKs dostarczany przez platformę Azure można również wybrać z szeroką gamę wersji Zulu OpenJDK udostępniane na platformie Azure przez systemy Azul.
  * Można również określić dystrybucji JDK podczas przesyłania go jako plik ZIP do konta magazynu.
* **Ulepszenia w widoku Eksploratora Azure**:
  * Obsługa zarządzania maszynami wirtualnymi przy użyciu nowego modelu Menedżera zasobów systemu Azure: można listy, tworzyć i usuwać maszyn wirtualnych na podstawie Menedżera zasobów bez opuszczania IDE.
  * Obsługa konta magazynu obiektów blob zarządzania za pomocą Menedżera zasobów systemu Azure, które uzupełnia istniejące funkcje do zarządzania kontami magazynu "klasycznym".
* **Sterownik JDBC firmy Microsoft w wersji 6.0 dla programu SQL Server**. Ta aktualizacja zawiera najnowsze sterownik JDBC dla programu Microsoft SQL Server (6.0), który jest teraz włączone jako biblioteki, który można łatwo dodać do projektów języka Java, a tym samym zastępowanie starszej wersji.

### <a name="june-29-2016"></a>29 czerwca 2016 r.
Zestaw narzędzi platformy Azure dla IntelliJ - wersji z czerwca 2016 zawiera następujące udoskonalenia:

* **Wymaganie Java 8**. Zestaw narzędzi platformy Azure dla IntelliJ wymaga teraz Java 8, mimo że to wymaganie dotyczy tylko w zestawie narzędzi programu, — aplikacje mogą w dalszym ciągu używać wszystkich wersji programu Java, które są obsługiwane przez platformę Azure.
* **Obsługa najnowsze JDKs Java**. Najnowsze wersje Java JDKs są teraz obsługiwane przez zestaw narzędzi platformy Azure dla IntelliJ.
* **Obsługa v2.9.1 Azure SDK**. Najnowszą wersję zestawu SDK platformy Azure jest teraz minimalna warunków wstępnych dla narzędzi Azure dla IntelliJ.
* **Zintegrowane przykłady**. Zestaw narzędzi platformy Azure dla IntelliJ obejmuje teraz kilka przykładowych aplikacji, aby pomóc deweloperom rozpocząć pracę.
* **Integracja narzędzia HDInsight**. Narzędzia HDInsight platformy Azure są teraz powiązane narzędzi Azure for IntelliJ. Aby uzyskać więcej informacji, zobacz [HDInsight Tools Plugin for IntelliJ].
* **Zdalne debugowanie aplikacji sieci Web Java**. Zestaw narzędzi platformy Azure dla IntelliJ obsługuje teraz zdalne debugowanie aplikacji sieci web Java w usłudze Azure App Service.

### <a name="april-12-2016"></a>12 kwietnia 2016 r.
Zestaw narzędzi platformy Azure dla IntelliJ - wersji z kwietnia 2016 zawiera następujące udoskonalenia:

* **Obsługa v2.9.0 Azure SDK**. Najnowszą wersję zestawu SDK platformy Azure jest teraz minimalna warunków wstępnych dla narzędzi Azure dla IntelliJ.
* **Inne ulepszenia użyteczność, czas odpowiedzi i wydajności powiązane z obsługi aplikacji sieci Web Azure**. Liczba optymalizacji wydajności w jak zestawu narzędzi komunikuje się z wynikiem Azure w lepsze reakcje interfejsu użytkownika.
* **Możliwość usunięcia istniejącego kontenera aplikacji sieci Web na platformie Azure z wewnątrz IntelliJ**. Zestaw narzędzi platformy Azure dla IntelliJ umożliwia teraz usunąć istniejącego kontenera sieci Web platformy Azure bez opuszczania IntelliJ.

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji o zestawach narzędzi platformy Azure dla środowisk IDE języka Java, skorzystaj z następujących linków:

* [zestawu narzędzi platformy Azure dla programu Eclipse]
  * [What's New in the Azure Toolkit for Eclipse] (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
  * [Sign In Instructions for the Azure Toolkit for Eclipse] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * *What's New in Azure Toolkit for IntelliJ (w tym artykule)*
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Sign In Instructions for the Azure Toolkit for IntelliJ] (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o używaniu platformy Azure z językiem Java, zobacz [Azure Java Developer Center].

<!-- URL List -->

[zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[Sign In Instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md (Co nowego w zestawie narzędzi platformy Azure dla środowiska Eclipse)
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure znak w instrukcje dotyczące narzędzi Azure dla IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[sposób publikowania aplikacji sieci Web jako kontener Docker przy użyciu zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Zarządzanie kontami magazynu przy użyciu Eksploratora Azure for IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Zarządzanie maszyn wirtualnych za pomocą Eksploratora Azure for IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547

[HDInsight Tools Plugin for IntelliJ]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
