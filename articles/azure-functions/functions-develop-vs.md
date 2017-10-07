---
title: "aaaDevelop funkcji platformy Azure przy użyciu programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Functions toodevelop i testowania przy użyciu narzędzi funkcji Azure dla programu Visual Studio 2017 r."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a>Środowisko Azure Functions Tools for Visual Studio  

Narzędzi funkcji platformy Azure dla programu Visual Studio 2017 to rozszerzenie dla programu Visual Studio, który pozwala tworzyć, testować i wdrażać tooAzure funkcje C#. Jeśli jest to usprawnić pierwszej funkcji platformy Azure, możesz dowiedzieć się więcej, zobacz [tooAzure wprowadzenie funkcji](functions-overview.md).

Witaj narzędzi funkcji Azure udostępnia hello następujące korzyści: 

* Edytowania, tworzenia i uruchamiania funkcji na komputerze deweloperskim lokalnego. 
* Publikowanie z usługi Azure Functions projektu bezpośrednio tooAzure. 
* Użyj powiązania funkcji toodeclare atrybuty zadań Webjob bezpośrednio w hello kodu C# zamiast utrzymywania osobnych function.json dla powiązania definicje.
* Tworzenie i wdrażanie wstępnie skompilowanym funkcje C#. Wstępnie skompilowane funkcje umożliwiać wydajności zimnego lepiej niż C# opartych na skryptach funkcji. 
* Kod funkcji w języku C# przy jednoczesnym zachowaniu wszystkich zalet hello tworzenia Visual Studio. 

W tym temacie pokazano, jak toouse hello Azure funkcje narzędzi dla programu Visual Studio 2017 toodevelop funkcji w języku C#. Możesz także dowiedzieć się, jak toopublish tooAzure Twojego projektu jako zestaw .NET.

## <a name="prerequisites"></a>Wymagania wstępne

Narzędzia funkcji platformy Azure jest uwzględniona w hello Azure programowanie obciążenie [programu Visual Studio 2017 wersji 15 ustęp 3](https://www.visualstudio.com/vs/), lub jego nowsza wersja. Upewnij się, że zawierają hello **Azure programowanie** obciążenia w instalacji programu Visual Studio 2017 wersji 15 ustęp 3:

![Instalowanie programu Visual Studio 2017 przy użyciu hello Azure programowanie obciążenia](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

toocreate i wdrażania funkcji, należy również:

* Aktywna subskrypcja platformy Azure. Jeśli nie masz subskrypcji platformy Azure, [wolnego konta](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) są dostępne.

* Konto magazynu Azure. toocreate konta magazynu, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).  
## <a name="create-an-azure-functions-project"></a>Tworzenie projektu usługi Azure Functions 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a>Konfigurowanie hello projektu dla rozwoju lokalnych

Podczas tworzenia nowego projektu przy użyciu szablonu usługi Azure Functions hello otrzymasz pusty C# projekt zawierający hello następujące pliki:

* **Host.JSON**: umożliwia skonfigurowanie hello funkcji hosta. Te ustawienia dotyczą zarówno podczas uruchamiania lokalnie i na platformie Azure. Aby uzyskać więcej informacji, zobacz [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) artykule.
    
* **Local.Settings.JSON**: przechowuje ustawienia używane podczas uruchamiania lokalnego funkcji. Te ustawienia nie są używane przez platformę Azure, są one używane przez hello [Azure funkcje podstawowe narzędzia](functions-run-local.md). Użyj tego ustawienia toospecify plików, takie jak tooother ciągów połączenia Azure usługi. Dodaj nowy toohello klucza **wartości** tablicy dla każdego połączenia wymagany przez funkcje w projekcie. Aby uzyskać więcej informacji, zobacz [pliku ustawień lokalnych](functions-run-local.md#local-settings-file) w hello Azure funkcje podstawowe narzędzia tematu.

środowisko uruchomieniowe Functions Hello wewnętrznie używa konta usługi Azure Storage. W przypadku wyzwolenia wszystkich typów innych niż HTTP i elementów webhook, należy skonfigurować hello **Values.AzureWebJobsStorage** klucza tooa parametry połączenia w prawidłowe konto magazynu Azure.

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 Parametry połączenia tooset hello magazynu konta:

1. W programie Visual Studio Otwórz **Eksplorator chmury**, rozwiń węzeł **konta magazynu** > **Twoje konto magazynu**, a następnie wybierz pozycję **właściwości**i kopiowania hello **parametry połączenia podstawowej** wartość.   

2. W projekcie, otwórz plik projektu local.settings.json hello i ustaw wartość hello hello **AzureWebJobsStorage** klucza toohello parametry połączenia skopiowane.

3. Powtórz hello poprzedniego kroku tooadd unikatowy kluczy toohello **wartości** tablicy dla innych połączeń wymagany przez funkcje.  

## <a name="create-a-function"></a>Tworzenie funkcji

W przypadku funkcji wstępnie skompilowanym powiązania hello używane przez funkcję hello są definiowane przez stosowanie atrybutów w kodzie hello. Korzystając z toocreate narzędzi funkcji Azure hello funkcji z szablonów hello pod warunkiem, te atrybuty są stosowane dla Ciebie. 

1. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Dodaj** > **Nowy element**. Wybierz **funkcji platformy Azure**, wpisz **nazwa** hello klasy, a następnie kliknij przycisk **Dodaj**.

2. Wybierz wyzwalacz, ustaw hello powiązania właściwości, a następnie kliknij przycisk **Utwórz**. Witaj poniższy przykład przedstawia ustawienia hello wyzwolenia tworzenia magazynu kolejek funkcji. 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    Klucz ciąg połączenia o nazwie **QueueStorage** zostanie podany, która jest zdefiniowana w pliku local.settings.json hello. 
 
3. Sprawdź hello nowo dodanych klasy. Zobacz statycznego **Uruchom** — metoda, która ma atrybut hello **FunctionName** atrybutu. Ten atrybut wskazuje, że metoda hello jest hello punkt wejścia dla funkcji hello. 

    Na przykład hello następujące klasy C# reprezentuje podstawowych funkcji magazynu wyzwalane kolejki:

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    Atrybut specyficzne dla powiązania jest podany parametr wiązania zastosowane tooeach toohello metoda punktu wejścia. Atrybut Hello przyjmuje jako parametry, informacje o powiązaniu hello. W poprzednim przykładzie hello hello pierwszy parametr ma **QueueTrigger** atrybut, wskazujący funkcję kolejki wyzwolone. Nazwa kolejki Hello i nazwa ustawienie parametrów połączenia są przekazywane jako parametry.  

## <a name="testing-functions"></a>Testowanie funkcji

Podstawowe narzędzia usługi Azure Functions umożliwiają uruchamianie projektu usługi Azure Functions na lokalnym komputerze deweloperskim. Jesteś zostanie wyświetlony monit o tooinstall, które te narzędzia hello podczas pierwszego uruchomienia funkcji w programie Visual Studio.  

tootest funkcji, naciśnij klawisz F5. Po wyświetleniu monitu Zaakceptuj Żądanie hello z toodownload programu Visual Studio i zainstalować narzędzia do podstawowych funkcji platformy Azure (CLI).  Możesz także tooenable wyjątek zapory, aby narzędzia hello mogły obsługiwać żądania HTTP.

Z projektem hello uruchomiona można przetestować kodu jako może przetestować wdrożonej funkcji. Aby uzyskać więcej informacji, zobacz [strategii do testowania kodu w usługi Azure Functions](functions-test-a-function.md). Podczas uruchamiania w trybie debugowania, punkty przerwania są osiągane w programie Visual Studio, zgodnie z oczekiwaniami. 

Przykład sposobu tootest kolejki wyzwalane funkcji, zobacz hello [samouczek Szybki Start — funkcja kolejki wyzwalane](functions-create-storage-queue-triggered-function.md#test-the-function).  

toolearn więcej informacji o użyciu hello Azure funkcje podstawowe narzędzia, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md).

## <a name="publish-tooazure"></a>Publikowanie tooAzure

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
>Wszystkie ustawienia dodanego w hello local.settings.json należy również dodać toohello funkcji aplikacji na platformie Azure. Te ustawienia nie są automatycznie dodawane. Możesz dodać wymagane ustawienia tooyour funkcji aplikacji w jeden z następujących sposobów:
>
>* [Przy użyciu hello portalu Azure](functions-how-to-use-azure-function-app-settings.md#settings).
>* [Przy użyciu hello `--publish-local-settings` opcja publikowania w hello Azure funkcje podstawowe narzędzia](functions-run-local.md#publish).
>* [Przy użyciu hello Azure CLI](/cli/azure/functionapp/config/appsettings#set). 

## <a name="next-steps"></a>Następne kroki

Uzyskać więcej informacji na temat narzędzia funkcji platformy Azure, zobacz typowe pytania części hello hello [2017 Visual Studio Tools dla usługi Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) wpis w blogu.

toolearn więcej informacji na temat hello Azure funkcje podstawowe narzędzia, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md).  
toolearn więcej informacji na temat tworzenia funkcji jako biblioteki klas .NET, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md). Ten temat zawiera również przykłady sposobu toodeclare atrybuty toouse hello różnego typu powiązania Azure Functions obsługiwane.    
