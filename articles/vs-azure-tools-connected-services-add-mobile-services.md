---
title: "aaaAdding usług Mobile Services przy użyciu usług połączonych w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Dodawanie usługi Mobile Services przy użyciu programu Visual Studio Dodaj połączone usługi hello — okno dialogowe"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Dodawanie usługi Mobile Services przy użyciu programu Visual Studio usług połączonych
Za pomocą programu Visual Studio 2015, można połączyć tooAzure Mobile Services przy użyciu hello **dodać podłączonej usługi** okna dialogowego. Możesz połączyć się z wszystkich aplikacji klienckich C#, dowolnej aplikacji JavaScript lub aplikacji Cordova i platform. Po nawiązaniu połączenia można utworzyć i uzyskać dostęp do danych, tworzenie niestandardowych interfejsów API i zaplanowanych zadań lub dodać obsługę powiadomień wypychanych.  Hello operacji usług połączonych dodaje wszystkie odpowiednie odwołania i kod połączenia. Mogą również czerpać korzyści z wbudowaną obsługę uwierzytelniania przy użyciu różnych popularnych tożsamości systemów, takich jak Azure AD, Facebook, Twitter i Accounts firmy Microsoft.

## <a name="supported-project-types"></a>Typy obsługiwane projektów
> [!NOTE]
> W programie Visual Studio 2015 dodawanie projektów uniwersalnych systemu Windows (Windows 10) tooa usług Azure Mobile Services przy użyciu okna dialogowego Dodawanie usług połączonych hello nie jest obsługiwane. Możesz dodać usług Azure Mobile Services przez zainstalowanie odpowiednich pakietów hello przy użyciu hello Menedżera pakietów NuGet dla projektu.
> 
> 

Możesz użyć hello usług połączonych okna dialogowego tooconnect tooAzure usług Mobile Services w hello następujące typy projektu.

* Projekty Sklepu Windows 8.1 .NET, Phone i aplikacji uniwersalnych
* Projekty Sklepu Windows 8.1 JavaScript, Phone i aplikacji uniwersalnych
* Projektów utworzonych za pomocą narzędzi Visual Studio Tools for Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Połączenie usług Mobile tooAzure za pomocą okna dialogowego Dodawanie usług połączonych hello
1. Upewnij się, że masz konta platformy Azure. Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Otwórz hello **dodać usług połączonych** okno dialogowe.
   
   * Dla aplikacji .NET Otwórz projekt w programie Visual Studio, hello Otwórz menu kontekstowe dla hello **odwołania** węzła w Eksploratorze rozwiązań, a następnie wybierz pozycję **dodać podłączonej usługi**
     
        ![Łączenie tooAzure usługi mobilnej](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * W przypadku projektów aplikacji oprogramowania Apache Cordova, otwórz projekt w programie Visual Studio, hello Otwórz menu kontekstowe dla węzła projektu hello w Eksploratorze rozwiązań, a następnie wybierz pozycję **dodać podłączonej usługi**.
3. W hello **dodać podłączonej usługi** okna dialogowego wybierz **usług Azure Mobile Services**, a następnie wybierz pozycję hello **Konfiguruj** przycisk. Jeśli jeszcze tego nie zrobiono, może być zostanie wyświetlony monit o toolog na platformie Azure.
   
    ![Dodawanie usługi mobilnej Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. W hello **usług Azure Mobile Services** oknie dialogowym Wybierz istniejącą usługę mobilną, jeśli istnieje. Jeśli potrzebujesz toocreate nowej usługi mobilnej Azure, procedura hello poniżej toodo tak. W przeciwnym razie Pomiń toohello następnego kroku.
   
    toocreate nowe konto usługi mobilnej:
   
   1. Wybierz hello ** Utwórz usługę ** łącze umieszczone u dołu hello hello — okno dialogowe.
       ![Dodawanie nowej podłączonej usługi mobilnej](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Na powitania **Tworzenie usługi mobilnej** okno dialogowe, są dostępne usługi mobilnej zaplecze JavaScript lub usługi mobilnej zaplecza .NET hello **środowiska uruchomieniowego** listy rozwijanej. 
      
       ![Tworzenie usługi mobilnej](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Usługi zaplecza JavaScript jest prosta i skuteczna. Po utworzeniu usługi mobilnej zaplecze JavaScript kod JavaScript po stronie serwera hello są przechowywane w chmurze hello, ale skrypty serwera można edytować za pomocą Eksploratora serwera lub hello portalu zarządzania Azure. 
      
       Usługi mobilnej zaplecza .NET zapewnia pełną moc hello i elastyczność interfejsu API sieci Web oraz Entity Framework. Po utworzeniu usługi mobilnej zaplecza .NET projekt zostanie utworzony i dodać tooyour rozwiązania. 
   3. Wybierz hello **Region** której mają hello usługi mobilnej, a następnie wprowadź nazwę użytkownika i hasło dla serwera hello.
   4. Po wprowadzeniu wszystkich informacji wymaganych hello wybierz hello **Utwórz** przycisk usługi mobilnej hello toocreate.
   5. Nowa Usługa mobilna Hello powinien są wyświetlane na liście usługi hello na powitania **usług Azure Mobile Services** okno dialogowe. Wybierz nową usługę mobilną hello hello listy, a następnie wybierz pozycję hello **Dodaj** przycisk tooadd hello usługi tooyour projektu.
5. Przejrzyj wprowadzenie hello sieciowego strona, która pojawia się i dowiedzieć się, jak projekt został zmodyfikowany. Po dodaniu podłączonej usługi, w przeglądarce zostanie wyświetlona strona wprowadzenie. Możesz przejrzeć hello sugerowane kolejne kroki i przykłady kodu lub przełącz toosee strony co się stało toohello, jakie odwołania zostały dodane tooyour projektu, i jak zostały zmodyfikowane pliki kodu i konfiguracji.
6. Za pomocą hello przykłady kodu przedstawiono wskazówki Uruchom, pisania kodu tooaccess usługi mobilnej!

## <a name="how-your-project-is-modified"></a>Jak zmienić jest projektu
Jak Visual Studio modyfikuje projekt zależy od typu projektu hello. C# aplikacji klienta, zobacz [co się stało — projektów C#](http://go.microsoft.com/fwlink/p/?LinkId=513119). W przypadku aplikacji klienckich JavaScript, zobacz [co się stało — projekty JavaScript](http://go.microsoft.com/fwlink/p/?LinkId=513120). Dla aplikacji Cordova zobacz [co się stało — projektów Cordova](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Następne kroki
Zadawaj pytania i uzyskiwanie pomocy: 

* [MSDN Forum: Usług Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure Mobile Services na powitania Blog zespołu usługi Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure Mobile Services w witrynie azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Dokumentacja usług Azure Mobile Services w witrynie azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

