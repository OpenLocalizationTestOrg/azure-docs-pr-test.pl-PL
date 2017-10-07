---
title: aaaOverview Microsoft Azure Data Lake Analytics | Dokumentacja firmy Microsoft
description: "Data Lake Analytics to usługa danych Big Data w Azure, który umożliwia toodrive danych firmy przy użyciu danych uzyskanych z danych w chmurze hello, niezależnie od rozmiaru lub w których jest."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 1e1d443a-48a2-47fb-bc00-bf88274222de
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 15bcd549c5aeb167da1338f253270ad57f8c5123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-microsoft-azure-data-lake-analytics"></a>Omówienie usługi Microsoft Azure Data Lake Analytics
## <a name="what-is-azure-data-lake-analytics"></a>Co to jest usługa Azure Data Lake Analytics?
Azure Data Lake Analytics to analizy danych big data toosimplify usługa na żądanie analizy zadania. Można skoncentrować się na pisaniu i uruchamianiu zadań oraz zarządzaniu nimi, a nie na obsłudze rozproszonej infrastruktury. Zamiast wdrażać, konfigurować i dostrajania sprzętu zapisać tootransform kwerend danych i wyodrębniać wartościowe informacje. Usługa analizy Hello może obsługiwać zadania o dowolnej skali natychmiast przez ustawienie hello wskazujące potrzebną moc należy. Płacisz tylko za uruchomione zadanie, dzięki czemu oszczędzasz pieniądze. Hello usługa analizy obsługuje usługę Azure Active Directory, co pozwala zarządzać dostępem i rolami zintegrowanymi z lokalnego systemu tożsamości. Zawiera także U-SQL, języka, który łączy korzyści hello SQL z wszechstronnymi możliwościami kodu użytkownika hello. Umożliwia skalowalne rozproszone środowisko uruchomieniowe języka U-SQL tooefficiently możesz analizować dane w magazynie hello i na serwerach SQL Azure, baza danych SQL Azure i usługi Azure SQL Data Warehouse.

## <a name="key-capabilities"></a>Najważniejsze możliwości
* **Dynamiczne skalowanie**
  
    Usługa Data Lake Analytics została zaprojektowana z myślą o wydajności i skalowaniu w chmurze.  Umożliwia ona dynamiczną aprowizację zasobów oraz analizowanie terabajtów, a nawet eksabajtów danych. Po ukończeniu zadania hello wyłączane zasobów automatycznie i płacisz tylko za użytą moc przetwarzania hello. Zwiększyć lub zmniejszyć rozmiar hello przechowywanych danych lub hello ilość zasobów obliczeniowych, używany w przypadku braku toorewrite kodu. Można skupić się tylko na logice biznesowej, a nie na sposobie przetwarzania i przechowywania dużych zestawów danych.
* **Szybsze programowanie, debugowanie i bardziej inteligentne optymalizowanie przy użyciu znanych narzędzi**
  
    Data Lake Analytics jest ściśle zintegrowana z programem Visual Studio, dzięki czemu można używać toorun znanych narzędzi, debugować i dostosowywać kod. Wizualizacje zadań U-SQL umożliwiają sprawdzanie sposobu działania kodu w skali. Dzięki temu można łatwo identyfikować wąskie gardła związane z wydajnością i optymalizować koszty.
* **U-SQL: język prosty i znany, zaawansowany i rozszerzalny**
  
    Data Lake Analytics obejmuje język zapytań, rozszerzający hello znanego, prostego, deklaratywnego charakteru SQL z wszechstronnymi możliwościami hello języka C# U-SQL. Hello języka U-SQL jest wbudowany w program hello sam rozproszone środowisko uruchomieniowe, które obsługuje systemy danych big data hello w firmie Microsoft. Miliony deweloperów SQL i .NET mogą teraz przetwarzanie i analizowanie danych z hello umiejętności, które mają.
* **Bezproblemowa integracja z inwestycjami związanymi z infrastrukturą IT**
  
    Usługa Data Lake Analytics może korzystać z istniejących inwestycji w infrastrukturę IT w zakresie obsługi tożsamości, zarządzania, zabezpieczeń i magazynowania danych. W tym nadzór nad danymi i umożliwia łatwe tooextend istniejących aplikacji obsługujących dane. Usługa Data Lake Analytics jest zintegrowana z usługą Active Directory, co umożliwia zarządzanie użytkownikami i udzielanie im uprawnień, oraz zawiera wbudowane funkcje monitorowania i inspekcji.
* **Przystępna cena i niedroga obsługa**
  
    Usługa Data Lake Analytics to ekonomiczne rozwiązanie służące do uruchamiania obciążeń związanych z danymi big data. Opłaty są naliczane za poszczególne zadania wykonywane podczas przetwarzania danych. Sprzęt, licencje ani umowy dotyczące pomocy technicznej w zakresie usługi nie są wymagane. Witaj system jest automatycznie skalowany w górę lub w dół zadania hello rozpoczęciu i zakończeniu tak nigdy płacisz więcej niż trzeba.
* **Współdziałanie z danymi na platformie Azure**
  
    Data Lake Analytics jest zoptymalizowana toowork z usługi Azure Data Lake — zapewnianie hello najwyższy poziom wydajności, przepływności i przetwarzania równoległego na potrzeby obciążeń danych big data.  Usługa Data Lake Analytics może również współdziałać z usługami Azure Blob Storage i Azure SQL Database.

## <a name="next-steps"></a>Następne kroki
 
  * Rozpoczynanie pracy z usługą Data Lake Analytics za pomocą [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI](data-lake-analytics-get-started-cli2.md)
  * Zarządzanie usługą Azure Data Lake Analytics przy użyciu [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) | [Azure .NET SDK](data-lake-analytics-manage-use-dotnet-sdk.md) | [Node.js](data-lake-analytics-manage-use-nodejs.md)
  * [Monitorowanie zadań usługi Azure Data Lake Analytics i rozwiązywanie problemów przy użyciu witryny Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md) 
