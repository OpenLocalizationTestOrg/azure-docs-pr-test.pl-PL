---
title: aaaCreate Windows platformy Uniwersalnej na Mobile Apps | Dokumentacja firmy Microsoft
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie używanie zapleczy aplikacji mobilnych Azure do tworzenia aplikacji uniwersalnych platformy systemu Windows (UWP) w języku C#, Visual Basic lub JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Tworzenie aplikacji systemu Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooa Windows platformy Uniwersalnej aplikacji. Aby uzyskać więcej informacji, zobacz artykuł [Co to jest usługa Mobile Apps](app-service-mobile-value-prop.md). następujące Hello to przechwytywaniu zawartości ekranu aplikacji hello zakończone:

![Ukończona aplikacja klasyczna](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Uruchamianie na komputerze

![Ukończona aplikacja na telefon](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Uruchamianie na telefonie

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków Aplikacji mobilnych dotyczących aplikacji platformy uniwersalnej systemu Windows.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli nie masz konta, możesz utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Program [Visual Studio Community 2015] lub nowszy.

## <a name="create-a-new-azure-mobile-app-backend"></a>Tworzenie zaplecza nowej Aplikacji mobilnej Azure
Wykonaj te kroki toocreate nowego zaplecza aplikacji mobilnej.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów. Następnie pobierzesz Projekt serwera dla prostego "Lista czynności do wykonania" wewnętrznej bazy danych i opublikuj go tooAzure.

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Pobieranie i uruchamianie projektu klienta hello
Po skonfigurowaniu zaplecza aplikacji mobilnej, możesz utworzyć nową aplikację klienta lub zmodyfikować istniejącą tooAzure tooconnect aplikacji. W tej sekcji możesz pobrać projekt szablonu aplikacji platformy uniwersalnej systemu Windows jest zaplecza aplikacji mobilnej tooyour tooconnect dostosowane.

1. Po powrocie do hello **szybki start** bloku dla zaplecza aplikacji mobilnej, kliknij przycisk **Utwórz nową aplikację** > **Pobierz**, następnie wyodrębnić hello skompresowane pliki projektu tooyour komputera lokalnego.

    ![Pobieranie projektu Szybki start systemu Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Opcjonalnie) Dodaj toohello projekt aplikacji platformy uniwersalnej systemu Windows hello samego rozwiązania co projekt serwera hello. To ułatwia toodebug testu zarówno hello wewnętrznej bazy danych i aplikacji hello w hello tym samym rozwiązaniu Visual Studio, jeśli wybierzesz toodo, dlatego. tooadd rozwiązania toohello projekt aplikacji platformy uniwersalnej systemu Windows, musisz korzystać z programu Visual Studio 2015 lub nowsza wersja.
3. Z aplikacją platformy uniwersalnej systemu Windows hello jako projekt startowy hello naciśnij klawisz toodeploy klucza F5 hello i hello uruchomienia aplikacji.
4. W aplikacji hello wpisz znaczący tekst, na przykład *hello ukończenia samouczka*, w hello **Wstaw czynność do wykonania** polu tekstowym, a następnie kliknij przycisk **zapisać**.

    ![Kompletna aplikacja systemu Windows typu Szybki start na komputerze](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    To wysyła POST żądania toohello nowe zaplecze aplikacji mobilnej hostowanej na platformie Azure.
5. (Opcjonalnie) Zatrzymaj aplikacji hello i uruchom go ponownie na innym urządzeniu lub emulatorze przenośnym.

    ![Kompletna aplikacja systemu Windows typu Szybki start na telefonie](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Zwróć uwagę, że dane zapisane hello w poprzednim kroku są ładowane z platformy Azure, po uruchomieniu aplikacji platformy uniwersalnej systemu Windows hello.

## <a name="next-steps"></a>Następne kroki
* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.
* [Dodaj aplikację tooyour powiadomień wypychanych](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.
* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej. Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
