---
title: "aaaGet Started with Azure Mobile Apps dotyczących aplikacji platformy Xamarin.Android"
description: "Postępuj zgodnie z tego samouczka tooget uruchomiony przy użyciu usługi Azure Mobile Apps do tworzenia aplikacji dla systemu Xamarin Android"
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a>Tworzenie aplikacji platformy Xamarin.Android
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooa aplikacji platformy Xamarin.Android. Aby uzyskać więcej informacji, zobacz artykuł [Co to jest usługa Mobile Apps](app-service-mobile-value-prop.md).

Zrzut ekranu aplikacji hello ukończone znajduje się poniżej:

![][0]

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Apps dotyczących aplikacji platformy Xamarin.Android.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące wymagania wstępne:

* Aktywne konto platformy Azure. Jeśli nie masz konta, należy utworzyć konto wersji próbnej platformy Azure i Uzyskaj bezpłatne aplikacje mobilne too10. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio z programem Xamarin. Instrukcje można znaleźć w temacie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin).

## <a name="create-an-azure-mobile-app-backend"></a>Tworzenie zaplecza Aplikacji mobilnej Azure
Wykonaj te kroki toocreate zaplecza aplikacji mobilnej.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów. Następnie należy pobrać Projekt serwera dla prostego "Lista czynności do wykonania" wewnętrznej bazy danych i opublikuj go tooAzure.

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a>Pobieranie i uruchamianie aplikacji platformy Xamarin.Android hello
1. W obszarze **Pobierz i uruchom projekt platformy Xamarin.Android**, kliknij przycisk hello **Pobierz** przycisku.

      Zapisz komputera lokalnego tooyour hello projektu skompresowany plik i zanotuj miejsce jego zapisania.
2. Naciśnij klawisz hello **F5** klucza toobuild hello projekt i uruchomić aplikacji hello.
3. W aplikacji hello wpisz znaczący tekst, na przykład *hello ukończenia samouczka* , a następnie kliknij przycisk hello **Dodaj** przycisku.

    ![][10]

    Dane z hello żądania zostaną wstawione do tabeli TodoItem hello. Elementy przechowywane w tabeli hello są zwracane przez zaplecze aplikacji mobilnej hello, a dane są wyświetlane na liście hello.

   > [!NOTE]
   > Możesz przejrzeć kod hello, który uzyskuje dostęp do Twojej aplikacji mobilnej tooquery wewnętrznej bazy danych i wstawiania danych, który znajduje się w hello plik o nazwie ToDoActivity.cs C#.
   >
   >

## <a name="next-steps"></a>Następne kroki
* [Dodaj aplikację tooyour synchronizacji w trybie Offline](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-xamarin-android-get-started-users.md)
* [Dodawanie aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych](app-service-mobile-xamarin-android-get-started-push.md)
* [Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
