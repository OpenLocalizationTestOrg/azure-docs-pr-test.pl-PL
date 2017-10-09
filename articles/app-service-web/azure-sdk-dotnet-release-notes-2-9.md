---
title: aaaAzure zestawu SDK dla platformy .NET 2.9 informacje o wersji
description: Informacje o wersji zestawu Azure SDK dla platformy .NET 2.9
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Informacje o wersji zestawu Azure SDK dla programu .NET 2.9

Ten temat zawiera informacje o wersji dla wersji 2.9 i 2.9.6 zestawu Azure SDK dla platformy .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Podsumowanie wersji zestawu Azure SDK dla platformy .NET 2.9.6

Data wydania: 2016-11-16
 
Nie istotne zmiany toohello zestaw Azure SDK 2.9 zostały wprowadzone w tej wersji. Nie jest również nie tooleverage procesu uaktualniania wymagane tego zestawu SDK z istniejącymi projektami usługi w chmurze.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 Release Candidate

- W programie Visual Studio RC 2017 tej wersji programu hello Azure SDK dla platformy .NET jest wbudowany w hello Azure obciążenia. Wszystkie narzędzia hello należy toodo rozwoju platformy Azure będzie częścią programu Visual Studio RC 2017 idąc dalej. Dla programu Visual Studio 2015 i Visual Studio 2013 hello zestawu SDK będą nadal dostępne za pośrednictwem WebPI. Firma Microsoft będzie roku zestawu Azure SDK dla wersji platformy .NET dla programu Visual Studio 2013, gdy program Visual Studio 2017 zwalnia jako produktu końcowego. Wykonaj ten link toodownload programu Visual Studio RC 2017: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Diagnostyka Azure

- Zmienione hello zachowanie tooonly przechowywać parametry połączenia z częściowa kluczem hello zastępuje token dla parametrów połączenia magazynu diagnostyki usługi w chmurze. Klucz magazynu rzeczywista Hello są obecnie przechowywane w folderze profilu użytkownika hello, można kontrolować dostęp do niej. Visual Studio odczyta hello klucza magazynu z folderu profilu użytkownika dla debugowania lokalnego i proces publikowania. 
- W przypadku zmiany toohello odpowiedzi opisane powyżej Visual Studio Online zespołu rozszerzone hello szablon zadania wdrożenia usługi w chmurze Azure, użytkownicy można określić klucz magazynu hello do ustawiania rozszerzenia diagnostyki podczas publikowania tooAzure w ciągłej integracji i wdrażania.
- Ułatwiliśmy ciągu bezpiecznego połączenia możliwe toostore i tokenizacji dla Azure Diagnostics (WAD), toohelp rozwiązuje problemy związane z konfiguracją w environements.
 
### <a name="windows-server-2016-virtual-machines"></a>Maszyny wirtualne systemu Windows Server 2016

- Program Visual Studio teraz obsługuje wdrażanie usługi w chmurze tooOS rodziny 5 (z systemem Windows Server 2016), maszynach wirtualnych. Istniejące usługi w chmurze, można zmienić Twojego tootarget ustawienia hello nowej rodziny systemów operacyjnych. Podczas tworzenia nowych usług w chmurze, jeśli wybierzesz toocreate hello usługi przy użyciu platformy .net 4.6 lub nowszej, będzie on domyślnej hello usługi toouse 5 rodziny systemu operacyjnego.  Aby uzyskać więcej informacji, możesz przejrzeć hello [rodziny systemów operacyjnych gościa obsługuje tabeli](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Znane problemy

- Azure .NET SDK 2.9.6 wprowadzone ograniczeń, która blokuje wdrożenie projektów przy użyciu nieobsługiwanego .NET tooany platform (np. .NET 4.6) rodziny systemów operacyjnych < 5. Udostępniono obejście [tutaj](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Pamięć podręczna na roli Azure 

- Obsługa kończy się na roli Azure w pamięci podręcznej w dniu 30 listopada 2016 r. Aby uzyskać więcej informacji, kliknij przycisk [tutaj](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Stack — szablony usługi Azure Resource Manager dla platformy Azure

- Dodaliśmy stosu Azure jako cel wdrożenia szablonów usługi Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Zestaw Azure SDK dla platformy .NET 2.9 podsumowanie

## <a name="overview"></a>Omówienie
Ten dokument zawiera informacje o wersji hello hello Azure SDK dla platformy .NET 2.9 wydania. 

Aby uzyskać szczegółowe informacje na temat aktualizacji w tej wersji, zobacz hello [post anonsu zestaw Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Zestaw Azure SDK 2.9 dla programu Visual Studio 2015 Update 2 do programu Visual Studio "15" Preview
Ta aktualizacja obejmuje hello następujące poprawki:

* Wystawiać pokrewne tooREST Generowanie klienta interfejsu API w w ciągu których hello "Nieznany typ" zostanie wyświetlony jako nazwa hello hello generacji kodu folderu i/lub nazwę hello nazw hello upuścić na powitania wygenerowany kod.
* Należy wystawić tooScheduled powiązanych zadań Webjob w których hello informacje dotyczące uwierzytelniania sprawdzano toobe przekazany procesu inicjowania obsługi administracyjnej toohello harmonogramu.

Ta aktualizacja obejmuje powitania po nowej funkcji:

* Obsługa dodatkowej usługi aplikacji na karcie "Usługi" hello powitalne okno dialogowe udostępniania usługi aplikacji. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Narzędzia usługi Azure Data Lake Tools dla Visual Studio 2015 Update 2
Tej aktualizacji obejmuje następujące hello:

* **Azure Data Lake Tools** dla programu Visual Studio teraz jest scalany hello Azure SDK dla wersji platformy .NET. Narzędzie Hello jest automatycznie instalowany podczas instalowania zestawu Azure SDK. 
  
    Narzędzie Hello jest często aktualizowana, przejdź [tutaj](http://aka.ms/datalaketool) tooget hello aktualizacji.
* **W Eksploratorze serwera** teraz pozwala tooview wszystkich i utworzyć niektóre jednostki metadanych U-SQL. Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.

## <a name="hdinsight-tools"></a>Narzędzia HDInsight Tools
**Narzędzia HDInsight Tools** dla programu Visual Studio teraz obsługuje HDInsight wersji 3.3, łącznie z wykazem wykresach Tez i inny język poprawki.

## <a name="azure-resource-manager"></a>Azure Resource Manager
Ta wersja dodaje [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) obsługę szablony Menedżera zasobów.

## <a name="see-also"></a>Zobacz też
[Azure SDK 2.9 anonsu post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

