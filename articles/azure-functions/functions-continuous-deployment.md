---
title: "wdrożenie usługi Azure Functions aaaContinuous | Dokumentacja firmy Microsoft"
description: "Użyj ciągłego wdrażania urządzenia z usługi aplikacji Azure toopublish funkcji platformy Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Ciągłe wdrażanie dla usługi Azure Functions
Azure Functions umożliwia łatwe toodeploy aplikacji funkcji przy użyciu ciągłej integracji usługi aplikacji. Funkcje integruje się z BitBucket, Dropbox, GitHub i Visual Studio Team Services (VSTS). Dzięki temu przepływu pracy gdzie kod funkcji aktualizacji przy użyciu jednej z tych usług zintegrowanych wyzwalacza wdrożenia tooAzure. W przypadku nowych funkcji tooAzure rozpoczynać [Azure Functions — omówienie](functions-overview.md).

Ciągłe wdrażanie to doskonałe rozwiązanie dla projektów, w których ma miejsce częste współtworzenie wielu treści. Umożliwia on również Obsługa kontroli źródła na kodzie funkcji. następujące źródła wdrożenia Hello są obecnie obsługiwane:

* [Bitbucket](https://bitbucket.org/)
* [Skrzynki](https://www.dropbox.com/)
* Repozytorium zewnętrznego (Git lub Mercurial)
* [Lokalne repozytorium Git](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [Usługi OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Wdrożenia są konfigurowane na poszczególnych funkcji aplikacji. Po włączeniu ciągłe wdrażanie kodu toofunction dostępu w portalu hello ustawiono zbyt*tylko do odczytu*.

## <a name="continuous-deployment-requirements"></a>Wymagania dotyczące ciągłe wdrażanie

Musi mieć źródła wdrożenia skonfigurowane i kod funkcji hello źródła wdrożenia przed skonfigurowaniem ciągłego wdrażania. We wdrożeniu aplikacji daną funkcję każdej funkcji znajduje się w podkatalogu o nazwie, gdzie nazwa katalogu hello jest nazwą hello hello funkcji.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Konfigurowanie ciągłego wdrażania
Użyj tej procedury tooconfigure ciągłego wdrażania dla istniejącej aplikacji funkcji. Te kroki prezentują integracji z repozytorium GitHub, ale podobne kroki zastosować Visual Studio Team Services lub innych usługach wdrożenia.

1. W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**. 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Następnie w hello **wdrożeń** kliknij bloku **Instalatora**.
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. W hello **źródło wdrożenia** bloku, kliknij przycisk **wybierz źródło**, a następnie wypełnij informacje hello źródła wdrożenia wybranej i kliknij przycisk **OK**.
   
    ![Wybierz źródło wdrożenia](./media/functions-continuous-deployment/choose-deployment-source.png)

Po skonfigurowaniu ciągłego wdrażania, wszystkie zmiany pliku źródła wdrożenia zostaną skopiowane toohello funkcji aplikacji i wdrożenia witrynę w trybie pełnym zostanie wywołany. witryny Hello jest wdrożone podczas aktualizacji plików hello źródła.

## <a name="deployment-options"></a>Opcje wdrażania

Witaj poniżej przedstawiono niektóre typowe wdrożeń:

- [Tworzenie tymczasowych wdrożenia](#staging)
- [Przenieś istniejące wdrożenie toocontinuous funkcji](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Tworzenie tymczasowych wdrożenia

Funkcja aplikacji jeszcze nie obsługuje miejsc wdrożenia. Można jednak nadal zarządzać oddzielnych wdrożeń tymczasowych i produkcyjnych przy użyciu ciągłej integracji.

Hello tooconfigure procesu i pracy z wdrożeniem przemieszczania wygląda zazwyczaj następująco:

1. Utwórz dwie aplikacje funkcji w subskrypcji, jeden dla kodu produkcyjnego hello i jeden dla przemieszczania. 

2. Utwórz źródło wdrożenia, jeśli nie został wcześniej. W tym przykładzie użyto [GitHub].

3. Dla aplikacji funkcja produkcji, pełną hello poprzednie kroki **skonfigurowano ciągłe wdrażanie** i zestaw hello wdrożenia gałęzi toohello głównej gałęzi repozytorium GitHub.
   
    ![Wybierz gałąź wdrożenia](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Powtórz ten krok dla hello przemieszczania funkcji aplikacji, ale wybierz hello przemieszczania gałęzi zamiast tego w Twojego repozytorium GitHub. Jeśli źródło wdrożenia nie obsługuje tworzenia rozgałęzień, należy użyć innego folderu.
    
5. Wprowadzić kod tooyour aktualizacje w hello przemieszczania gałęzi lub folderu, a następnie sprawdź, czy te zmiany zostaną odzwierciedlone w hello przemieszczania wdrożenia.

6. Po zakończeniu testowania, Scal zmiany z gałęzi przemieszczania hello hello gałęzi głównej. Tę operację scalania wyzwala wdrożenie toohello produkcji funkcji aplikacji. Jeśli źródło wdrożenia nie obsługuje gałęzie, Zastąp hello pliki w folderze produkcji hello hello pliki z folderu przemieszczania hello.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Przenieś istniejące wdrożenie toocontinuous funkcji
Jeśli masz istniejące funkcje, które utworzono i obsługiwane w portalu hello należy toodownload istniejącą funkcji plików kodu przy użyciu FTP lub hello lokalnego repozytorium Git, zanim można skonfigurować ciągłego wdrażania, jak opisano powyżej. Można to zrobić w hello ustawień usługi aplikacji — dla aplikacji funkcja. Po pobraniu plików, możesz przekazać je tooyour wybrane źródło ciągłego wdrażania.

> [!NOTE]
> Po skonfigurowaniu ciągłej integracji będzie już możliwe tooedit źródła plików hello funkcje portalu.

- [Porady: Konfigurowanie poświadczeń wdrożenia](#credentials)
- [Porady: pobieranie plików przy użyciu FTP](#downftp)
- [Porady: pobieranie plików przy użyciu hello lokalnego repozytorium Git](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Porady: Konfigurowanie poświadczeń wdrożenia
Przed pobraniem plików z aplikacji funkcji za pomocą protokołu FTP lub lokalnego repozytorium Git, należy skonfigurować witryny hello tooaccess poświadczeń. Poświadczenia są ustawione na poziomie aplikacji hello funkcji. Użyj hello następujące poświadczenia wdrażania tooset kroki w portalu Azure hello:

1. W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **poświadczenia wdrażania**.
   
    ![Konfigurowanie poświadczeń wdrożenia lokalnego](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Wpisz nazwę użytkownika i hasło, a następnie kliknij przycisk **zapisać**. Tooaccess te poświadczenia można teraz używać aplikacji funkcji z FTP lub hello wbudowanych repozytorium Git.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Porady: pobieranie plików przy użyciu FTP

1. W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **właściwości**, następnie skopiować wartości hello **użytkownika serwera FTP/wdrożenia**, **Nazwa hosta FTP**, i **nazwy hosta FTPS**.  

    **Użytkownika serwera FTP/wdrożenia** należy podać wyświetlaną w portalu hello, łącznie z nazwą aplikacji hello, tooprovide prawidłowego kontekstu serwera hello FTP.
   
    ![Uzyskaj informacje wdrożenia](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. Z tego klienta FTP Użyj hello połączenia zebranych informacji tooconnect tooyour aplikacji i Pobierz pliki źródłowe hello funkcji.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Porady: pobieranie plików przy użyciu lokalnego repozytorium Git

1. W aplikacji funkcji w hello [portalu Azure](https://portal.azure.com), kliknij przycisk **funkcji platformy** i **opcje wdrażania**. 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Następnie w hello **wdrożeń** kliknij bloku **Instalatora**.
 
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. W hello **źródło wdrożenia** bloku, kliknij przycisk **repozytorium Git lokalnego** , a następnie kliknij przycisk **OK**.

3. W **funkcji platformy**, kliknij przycisk **właściwości** i zanotuj wartość hello Git adresu URL. 
   
    ![Instalator ciągłe wdrażanie](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Klonuj repozytorium hello na komputerze lokalnym przy użyciu wiersza polecenia programu Git-aware lub ulubionego narzędzia Git. polecenie klonowania Git Hello wygląda następująco:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Pobieranie plików z klonu toohello aplikacji z funkcji na komputerze lokalnym, tak jak hello poniższy przykład:
   
        git pull origin master
   
    Jeśli jest to wymagane, podaj użytkownika [skonfigurowane poświadczenia wdrażania](#credentials).  

[GitHub]: https://github.com/
