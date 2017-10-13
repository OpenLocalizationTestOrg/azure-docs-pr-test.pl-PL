---
title: "Wprowadzenie do usługi Azure Mobile Apps dla aplikacji platformy Xamarin.Android"
description: "Wykonaj czynności opisane w tym samouczku, aby rozpocząć używanie usługi Azure Mobile Apps do tworzenia aplikacji platformy Xamarin Android."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-xamarinandroid-app"></a>Tworzenie aplikacji platformy Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
W tym samouczku przedstawiono sposób dodawania usługi zaplecza opartej na chmurze do aplikacji platformy Xamarin.Android. Aby uzyskać więcej informacji, zobacz artykuł [Co to jest usługa Mobile Apps](app-service-mobile-value-prop.md).

Zrzut ekranu gotowej aplikacji znajduje się poniżej:

![][0]

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Apps dotyczących aplikacji platformy Xamarin.Android.

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków tego samouczka niezbędne jest spełnienie następujących wymagań wstępnych:

* Aktywne konto platformy Azure. Jeśli nie masz konta, skorzystaj z bezpłatnej wersji próbnej platformy Azure i uzyskaj maksymalnie 10 bezpłatnych aplikacji mobilnych. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio z programem Xamarin. Instrukcje można znaleźć w temacie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin).

## <a name="create-an-azure-mobile-app-backend"></a>Tworzenie zaplecza Aplikacji mobilnej Azure
Wykonaj te kroki, aby utworzyć zaplecze aplikacji mobilnej.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów. Następnie należy pobrać projekt serwera dla prostego zaplecza typu „lista czynności do wykonania” i opublikować go na platformie Azure.

## <a name="configure-the-server-project"></a>Konfigurowanie projektu serwera
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a>Pobieranie i uruchamianie aplikacji platformy Xamarin.Android
1. W obszarze **Pobierz i uruchom projekt platformy Xamarin.Android** kliknij przycisk **Pobierz**.

      Zapisz skompresowany plik projektu na komputerze lokalnym i zapamiętaj, gdzie został on zapisany.
2. Naciśnij klawisz **F5**, aby skompilować projekt i uruchomić aplikację.
3. W aplikacji wpisz znaczący tekst, na przykład *Ukończ samouczek*, a następnie kliknij przycisk **Dodaj**.

    ![][10]

    Dane z żądania zostaną wstawione do tabeli TodoItem. Elementy przechowywane w tabeli są zwracane przez zaplecze aplikacji mobilnej, a dane są wyświetlane na liście.

   > [!NOTE]
   > Możesz przejrzeć kod uzyskujący dostęp do zaplecza aplikacji mobilnej w celu wyszukiwania i wstawiania danych. Znajduje się on w pliku C# ToDoActivity.cs.
   >
   >

## <a name="next-steps"></a>Następne kroki
* [Dodawanie synchronizacji offline do aplikacji](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Dodawanie uwierzytelniania do aplikacji](app-service-mobile-xamarin-android-get-started-users.md)
* [Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md)
* [Jak używać zarządzanego klienta usługi Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
