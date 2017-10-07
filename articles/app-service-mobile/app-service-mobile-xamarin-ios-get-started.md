---
title: "aaaGet wprowadzenie do usługi Azure App Service Mobile Apps dla aplikacji Xamarin.iOS | Dokumentacja firmy Microsoft"
description: "Postępuj zgodnie z tego samouczka tooget wprowadzenie używanie Mobile Apps do tworzenia aplikacji platformy Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a>Tworzenie aplikacji platformy Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd wewnętrznej bazy danych opartej na chmurze usługi tooa aplikacji mobilnej platformy Xamarin.iOS przy użyciu zaplecza aplikacji mobilnej Azure.  Utworzysz zaplecze nowej aplikacji mobilnej oraz prostą aplikację platformy Xamarin.iOS typu *Lista czynności do wykonania*, która przechowuje dane aplikacji na platformie Azure.

Wykonanie kroków tego samouczka jest wymaganiem wstępnym dla wszystkich innych samouczków Xamarin.iOS dotyczących używania funkcji Mobile Apps hello w usłudze Azure App Service.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące wymagania wstępne:

* Aktywne konto platformy Azure. Jeśli nie masz konta, należy utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* Visual Studio z programem Xamarin. Instrukcje można znaleźć w temacie [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin).
* Komputer Mac z zainstalowanym środowiskiem Xcode v7.0 lub nowszym i rozwiązaniem Xamarin Studio Community. Zobacz tematy [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin) oraz [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Konfigurowanie, instalowanie oraz weryfikacje dla użytkowników komputerów Mac) (MSDN).

## <a name="create-an-azure-mobile-app-backend"></a>Tworzenie zaplecza Aplikacji mobilnej Azure
Wykonaj te kroki toocreate zaplecza aplikacji mobilnej.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello
W ten sposób zainicjowano obsługę zaplecza Aplikacji mobilnej Azure, które może być używane przez aplikacje mobilne klientów. Następnie należy pobrać Projekt serwera dla prostego "Lista czynności do wykonania" wewnętrznej bazy danych i opublikuj go tooAzure.

Wykonaj następujące kroki tooconfigure powitania serwera projektu toouse hello albo hello zaplecza Node.js lub .NET.

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a>Pobieranie i uruchamianie aplikacji platformy Xamarin.iOS hello
1. Otwórz hello [portalu Azure] w oknie przeglądarki.
2. W bloku ustawień hello aplikacji mobilnej kliknij **wprowadzenie** > **Xamarin.iOS**. W kroku 3 kliknij pozycję **Utwórz nową aplikację**, jeśli nie została jeszcze wybrana.  Następnie kliknij przycisk hello **Pobierz** przycisku.

      Aplikacji klienckiej, która łączy tooyour zaplecze aplikacji mobilnej zostanie pobrana. Zapisz hello skompresowany plik projektu na komputerze lokalnym i Zapamiętaj miejsce jego zapisania.
3. Wyodrębnij pobrany projekt hello, a następnie otwórz go w programie Xamarin Studio (lub programu Visual Studio).

    ![][9]

    ![][8]
4. Naciśnij hello F5 klucza toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello.
5. W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie kliknij przycisk hello ** + ** przycisku.

    ![][10]

    Dane z hello żądania zostaną wstawione do tabeli TodoItem hello. Elementy przechowywane w tabeli hello są zwracane przez zaplecze aplikacji mobilnej hello, a dane są wyświetlane na liście hello.

> [!NOTE]
> Można sprawdzić hello kod, który uzyskuje dostęp do Twojej aplikacji mobilnej tooquery wewnętrznej bazy danych i wstawianie danych w pliku C# QSTodoService.cs hello.
>
>

## <a name="next-steps"></a>Następne kroki
* [Dodaj aplikację tooyour synchronizacji w trybie Offline](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-xamarin-ios-get-started-users.md)
* [Dodawanie aplikacji platformy Xamarin.Android tooyour powiadomień wypychanych](app-service-mobile-xamarin-ios-get-started-push.md)
* [Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[Witryna Azure Portal]: https://portal.azure.com/
