---
title: aaaAzure zestawu SDK dla platformy .NET 2.8 informacje o wersji
description: Zestaw Azure SDK dla platformy .NET 2,8 informacje o wersji
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Zestaw Azure SDK dla platformy .NET 2.8, 2.8.1 i 2.8.2
## <a name="overview"></a>Omówienie
Ten artykuł zawiera informacje o wersji hello (które obejmują znane problemy i fundamentalne zmiany) dla hello Azure SDK dla platformy .NET 2.8, 2.8.1 i 2.8.2 zwalnia. 

Aby uzyskać pełną listę nowych funkcji i aktualizacje wprowadzone w tej wersji, zobacz hello [Azure SDK 2.8 dla programu Visual Studio 2013 i Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) anonsu. 

## <a name="azure-sdk-for-net-28"></a>Azure SDK for .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Pobierz zestaw Azure SDK dla platformy .NET 2.8
[Zestaw Azure SDK dla platformy .NET 2.8 dla programu Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Zestaw Azure SDK dla platformy .NET 2.8 dla programu Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Obsługuje platformy .NET w wersji 4.5.2
#### <a name="known-issues"></a>Znane problemy
Azure .NET SDK 2.8 umożliwia możesz toocreate .NET 4.5.2 pakiety usługi w chmurze. Jednak .NET 4.5.2 framework nie zostaną zainstalowane na powitania domyślnej wersji obrazów systemu operacyjnego gościa do stycznia 2016 systemu operacyjnego gościa. Przed, 4.5.2 .NET framework będą dostępne przy użyciu oddzielnych wersji wersji systemu operacyjnego gościa — listopad 2015-02. Zobacz hello [poszczególnych wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack strony, gdy zostaną wydane hello obrazu.  Po zwolnieniu hello listopada 2015-02 obrazu można toouse tego obrazu, aktualizując pliku (cscfg) pliku konfiguracji usługi w chmurze. W konfiguracji usługi hello pliku atrybut hello osVersion hello element ServiceConfiguration elementu toohello ciągu "WA-GOŚCIA-OS-4.26_201511-02". Jeśli wybierzesz pozycję tooopt toouse ten obraz będzie już pobrać toohello aktualizacje automatyczne systemu operacyjnego gościa. tooget hello aktualizacje automatyczne hello osVersion musi być ustawiona zbyt "*" i .NET 4.5.2 będą dostępne tylko za pomocą funkcji Aktualizacje automatyczne w stycznia 2016.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Znane problemy
Podczas **szablon fabryki danych** projektu tworzenia dotyczące przykładowych danych, skrypt powłoki azure power może zakończyć się niepowodzeniem, jeśli jest zainstalowana na komputerze hello wersji powłoki azure power po 0.9.8.

W kolejności toosuccessfully tworzenia tego typu projektu, należy zainstalować [azure power shell wersji 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Narzędzia Menedżera zasobów Azure
#### <a name="breaking-changes"></a>Fundamentalne zmiany
Hello skrypt programu PowerShell dostarczane przez projekt grupy zasobów platformy Azure hello został zaktualizowany w tej wersji toowork hello nowe Azure polecenia cmdlet programu PowerShell w wersji 1.0.  Ten nowy skrypt nie będzie działać z z programem Visual Studio podczas używania wersji too2.8 wcześniejsze hello zestawu SDK.  

Skrypty z projektów utworzonych w starszych wersjach hello zestawu SDK nie będzie uruchamiana z poziomu programu Visual Studio przy użyciu hello 2.8 SDK.  Wszystkie skrypty będą nadal toowork poza Visual Studio z odpowiednią wersję hello hello poleceń cmdlet programu Azure PowerShell.  

Witaj 2,8 zestaw SDK wymaga wersji 1.0 hello poleceń cmdlet programu Azure PowerShell.  Wszystkie wersje hello zestaw SDK wymaga wersji 0.9.8 hello poleceń cmdlet programu Azure PowerShell.  Aby uzyskać więcej informacji, zobacz [to](http://go.microsoft.com/fwlink/?LinkID=623011) blogu.

### <a name="web-tools-extensions"></a>Rozszerzeń narzędzi sieci Web
#### <a name="known-issues"></a>Znane problemy
Witaj następujące znane problemy zostaną rozwiązane w powitania po uwolnieniu.

* Usługi aplikacji związane z chmury i Eksploratora serwera gestu w środowiskach nieprodukcyjnych (na przykład chińskiej wersji platformy Azure lub klienci stosu Azure) nie działają. Dla klientów w tych obszarach wpływ na pobieranie hello publikowania profil z hello portalu Azure zostaną włączone możliwości publikowania. Przyszłych wydaniach naprawi gesty, takie jak "Dołączanie debugera" i "Wyświetl dzienniki przesyłania strumieniowego" dla Chińskiej wersji platformy Azure i klientami stosu. 
* Klienci mogą zostać wyświetlone błędy podczas tworzenia podczas Insights aplikacji hello wystąpienia toowhich, które są wdrażane znajduje się w regionie innym niż wschodnie stany USA usługi aplikacji. W tych scenariuszach tworzenia usługi aplikacji w portalu hello i pobieranie hello profilu publikowania spowoduje włączenie publikowania scenariuszy. 

### <a name="azure-hdinsight-tools"></a>Usługa Azure HDInsight Tools
#### <a name="new-updates"></a>Nowe aktualizacje
* Można wykonać zapytanie Hive w klastrze hello za pośrednictwem serwera HiveServer2 z prawie nie koszty i zobacz dzienniki zadania hello czasie rzeczywistym.
* Przy użyciu hello więcej szczegółów znajduje nowe Hive widok wykonywania zadania mogą odnajdywać do głębiej, zadania i zidentyfikuj potencjalne problemy.

Aby uzyskać informacje, zobacz [Azure SDK 2.8 dla programu Visual Studio 2013 i Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Zestaw Azure SDK dla programu .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Znane problemy dotyczące programu Visual Studio 2013 i Visual Studio 2015
1. Wyzwalane zadania WebJob publikuje będzie tooslots Pokaż i błąd i nie będzie zestaw zgodnie z harmonogramem, ale przeprowadzi wypychanie hello tooAzure zadania WebJob. Klientów, którzy wymagają zadania zaplanowane można następnie używać tooset Azure Portal hello zapasowych harmonogram hello hello zadania WebJob. 
2. Python klientów może zgłaszać problemy z debugera. Zespół usługi wprowadza poprawkę dla tego, ale dotyczy klientów, prosimy Microsoft wiedzą na forach hello lub na blogu anonsu hello lub release notes sekcji komentarzy. 
3. Klienci w pewnych regionach (na przykład Południowa, Indie) może wystąpić błędy udostępniania usługi aplikacji. Jest to zgodne z portalu hello i klientów, którzy ten problem, można użyć hello Azure toorequest portalu dostępu toopublish toothese-regionów geograficznych. Gdy żądają regiony toothese dostępu przy użyciu hello Azure portalu inicjowania obsługi administracyjnej powinny działać. 

## <a name="azure-sdk-for-net-282"></a>Zestaw Azure SDK dla platformy .NET 2.8.2
Po instalacji hello hello 2.8.2 narzędzi mogą wystąpić powitania po problem.         

* Jeśli używasz systemu Windows 10 i nie jest zainstalowany program Internet Explorer, może wystąpić błąd "Nie można odnaleźć programu Internet Explorer".
  tooresolve hello problem, zainstaluj program Internet Explorer przy użyciu hello Dodaj/Usuń składniki systemu Windows w oknie dialogowym.

Jeśli zauważysz ten problem, użyj tooreport funkcji hello wysyłania a uśmiech go.

Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) post.

## <a name="other-updates"></a>Inne aktualizacje
W przypadku innych aktualizacji, zobacz [post anonsu Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Zobacz też
[Azure SDK 2.8 anonsu post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Obsługa i wycofania informacje dotyczące hello zestaw Azure SDK for .NET i interfejsów API](https://msdn.microsoft.com/library/azure/dn479282.aspx)

