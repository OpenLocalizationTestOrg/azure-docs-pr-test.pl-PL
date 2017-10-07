---
title: "aaaCreate pierwszej funkcji platformy Azure przy użyciu programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Tworzenie i publikowanie proste tooAzure funkcja wyzwalana HTTP przy użyciu narzędzi funkcji Azure dla programu Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, funkcje, przetwarzanie zdarzeń, obliczenia, architektura bez serwera"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>Tworzenie pierwszej funkcji przy użyciu programu Visual Studio

Środowisko Azure Functions umożliwia wykonywanie kodu w środowisku bez serwera bez konieczności toofirst tworzenie maszyny Wirtualnej lub opublikować aplikację sieci web.

W tym temacie dowiesz się, jak toouse hello 2017 usługi Visual Studio tools dla usługi Azure Functions toocreate i przetestować funkcję "hello world", który jest lokalnie. Następnie będzie publikować tooAzure kodu funkcji hello. Te narzędzia są dostępne jako część hello obciążenia Azure Programowanie w Visual Studio 2017 wersji 15 ustęp 3 lub nowszym.

![Kod usługi Azure Functions w projekcie programu Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka, instalacji:

* [Visual Studio 2017 wersji 15 ustęp 3](https://www.visualstudio.com/vs/preview/), łącznie z hello **Azure programowanie** obciążenia.

    ![Instalowanie programu Visual Studio 2017 przy użyciu hello Azure programowanie obciążenia](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    Po instalacji lub uaktualnienia tooVisual Studio 2017 wersji 15 ustęp 3, może być również konieczne toomanually aktualizacji hello 2017 usługi Visual Studio tools dla usługi Azure Functions. Można aktualizować hello narzędzi z hello **narzędzia** menu w obszarze **rozszerzenia i aktualizacje...**   >  **Aktualizacje** > **programu Visual Studio Marketplace** > **sieci Web i usługę Azure Functions zadania narzędzia**  >  **Aktualizacji**. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>Tworzenie projektu usługi Azure Functions w programie Visual Studio

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

Teraz, po utworzeniu projektu hello, można utworzyć swoją pierwszą funkcję.

## <a name="create-hello-function"></a>Utwórz hello — funkcja

1. W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Dodaj** > **Nowy element**. Wybierz pozycję **Funkcja platformy Azure** i kliknij pozycję **Dodaj**.

2. Wybierz pozycję **HttpTrigger**, wpisz **nazwę funkcji**, wybierz opcję **Anonimowe** w polu **Prawa dostępu** i kliknij pozycję **Utwórz**. Funkcja Hello tworzone jest dostępny przez żądania HTTP za pomocą dowolnego klienta. 

    ![Tworzenie nowej funkcji platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    Projekt tooyour, który zawiera klasę implementującą kodu funkcji zostanie dodany plik kodu. Ten kod opiera się na szablonie, który odbiera wartość nazwy i tłumiące echo go. Witaj **FunctionName** atrybut ustawia hello nazwę funkcji. Witaj **HttpTrigger** atrybut wskazuje wiadomość hello wyzwala hello funkcji. 

    ![Plik kodu — funkcja](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

Po utworzeniu funkcji wyzwalanej przez protokół HTTP można ją przetestować na komputerze lokalnym.

## <a name="test-hello-function-locally"></a>Testowanie funkcji hello lokalnie

Podstawowe narzędzia usługi Azure Functions umożliwiają uruchamianie projektu usługi Azure Functions na lokalnym komputerze deweloperskim. Jesteś zostanie wyświetlony monit o tooinstall, które te narzędzia hello podczas pierwszego uruchomienia funkcji w programie Visual Studio.  

1. tootest funkcji, naciśnij klawisz F5. Po wyświetleniu monitu Zaakceptuj Żądanie hello z toodownload programu Visual Studio i zainstalować narzędzia do podstawowych funkcji platformy Azure (CLI).  Możesz także tooenable wyjątek zapory, aby narzędzia hello mogły obsługiwać żądania HTTP.

2. Adres URL hello kopiowania funkcji ze środowiska uruchomieniowego usługi Azure Functions hello wyjściowej.  

    ![Lokalne środowisko uruchomieniowe platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. Wklej adres URL żądania HTTP hello hello do paska adresu przeglądarki. Dołącz ciągu zapytania hello `&name=<yourname>` toothis adresu URL i wykonać hello żądania. Hello poniżej przedstawiono odpowiedzi hello w hello przeglądarki toohello lokalne żądania GET zwracane przez funkcję hello: 

    ![Funkcja localhost odpowiedzi w przeglądarce hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. toostop debugowanie, kliknij przycisk hello **zatrzymać** przycisk na powitania narzędzi Visual Studio.

Po sprawdzeniu, czy funkcja hello działa poprawnie na komputerze lokalnym, jest tooAzure projektu hello toopublish czasu.

## <a name="publish-hello-project-tooazure"></a>Publikowanie hello tooAzure projektu

Aby opublikować projekt, musisz mieć aplikację funkcji w swojej subskrypcji platformy Azure. Aplikację funkcji możesz utworzyć bezpośrednio w programie Visual Studio.

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Testowanie funkcji na platformie Azure

1. Skopiuj hello podstawowy adres URL aplikacji funkcji hello ze strony profilu publikowania hello. Zastąp hello `localhost:port` część adresu URL hello używane podczas testowania funkcji hello lokalnie z hello nowego podstawowego adresu URL. Jak wcześniej, upewnij się, że ciąg zapytania hello tooappend `&name=<yourname>` toothis adresu URL i wykonać hello żądania.

    adres URL Hello, która wywołuje HTTP wyzwalane funkcja wygląda następująco:

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. Wklej nowy adres URL dla żądania hello HTTP w pasku adresu przeglądarki. Hello poniżej przedstawiono odpowiedzi hello w hello przeglądarki toohello zdalnego żądania GET zwracane przez funkcję hello: 

    ![Funkcja odpowiedzi w przeglądarce hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>Następne kroki

Użyto aplikacji funkcji toocreate C# dla programu Visual Studio przy użyciu prostych funkcji HTTP wyzwolone. 

+ toolearn jak tooconfigure toosupport Twojego projektu inne rodzaje wyzwalaczy i powiązań, zobacz hello [Konfiguruj hello projektu dla rozwoju lokalnych](functions-develop-vs.md#configure-the-project-for-local-development) sekcji [narzędzi funkcji Azure dla programu Visual Studio](functions-develop-vs.md).
+ toolearn więcej informacji na temat lokalnych testowanie i debugowanie przy użyciu hello Azure funkcje podstawowe narzędzia, zobacz [kodu oraz testów usługi Azure Functions lokalnie](functions-run-local.md). 
+ toolearn więcej informacji na temat tworzenia funkcji jako biblioteki klas .NET, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md). 

