---
title: "aaaGet pracę z usługą Mobile Apps za pomocą platformy Xamarin.Forms"
description: "Postępuj zgodnie z tego samouczka toostart używanie Mobile Apps do tworzenia aplikacji platformy Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Tworzenie aplikacji platformy Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak tooadd oparte na chmurze usługi zaplecza tooa aplikacji mobilnej platformy Xamarin.Forms przy użyciu hello funkcji Mobile Apps Azure App Service jako hello zaplecza. Tworzysz nowe zaplecze funkcji Mobile Apps oraz prostą aplikację platformy Xamarin.Forms typu Lista czynności do wykonania, która przechowuje dane aplikacji na platformie Azure.

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Apps dotyczących aplikacji platformy Xamarin.Forms.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli nie masz konta, możesz utworzyć konto wersji próbnej platformy Azure i Uzyskaj too10 bezpłatnych aplikacji mobilnych, które możesz korzystać nawet po próbnej. Aby uzyskać więcej informacji, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* Visual Studio z programem Xamarin. Aby uzyskać informacje, zobacz hello [ustawić Konfigurowanie i instalowanie programu Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) strony.

* Komputer Mac z zainstalowanym środowiskiem Xcode v7.0 lub nowszym i rozwiązaniem Xamarin Studio Community. Aby uzyskać informacje, zobacz tematy [Set up and install for Visual Studio and Xamarin (Konfigurowanie i instalowanie dla programów Visual Studio i Xamarin)](https://msdn.microsoft.com/library/mt613162.aspx) oraz [Set up, install, and verify for Mac users (Konfigurowanie, instalowanie i weryfikowanie dla użytkowników komputerów Mac)](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).

## <a name="create-a-new-mobile-apps-back-end"></a>Tworzenie nowego zaplecza funkcji Mobile Apps

toocreate zakończyć nowych aplikacji mobilnych w Wstecz, hello następujące:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Masz teraz zdefiniowane zaplecze funkcji Mobile Apps, którego mogą używać mobilne aplikacje klienckie. Następnie należy pobrać Projekt serwera dla wewnętrznej listy zadań do wykonania prostego, a następnie opublikuj go tooAzure.

## <a name="configure-hello-server-project"></a>Konfigurowanie projektu serwera hello

tooconfigure powitania serwera projektu toouse hello zaplecza Node.js lub .NET, hello następujące:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Pobierz i uruchom hello rozwiązania platformy Xamarin.Forms

Możesz pobrać rozwiązanie hello na dwa sposoby. Pobrać tooa Mac i otworzyć go w programie Xamarin Studio lub pobrać tooa komputer z systemem Windows i otworzyć go w programie Visual Studio za pomocą sieci Mac do tworzenia aplikacji dla systemu iOS hello. Aby uzyskać więcej informacji, zobacz stronę [Set up and install Visual Studio and Xamarin (Konfigurowanie i instalowanie programów Visual Studio i Xamarin)](https://msdn.microsoft.com/library/mt613162.aspx).

Na komputerze Mac lub Windows hello następujące:

1. Przejdź toohello [portalu Azure].

2. Na powitania **ustawienia** bloku dla aplikacji mobilnej, w obszarze **Mobile**, wybierz pozycję **wprowadzenie** > **platformy Xamarin.Forms**. W **kroku 3** wybierz pozycję **Utwórz nową aplikację**, a następnie wybierz pozycję **Pobierz**.

   Ta akcja spowoduje pobranie projektu, który zawiera aplikację klienta, który jest połączony tooyour aplikacji mobilnej. Zapisz komputera lokalnego tooyour hello projektu skompresowany plik i zanotuj miejsce jego zapisania.

3. Wyodrębnij pobrany projekt hello, a następnie otwórz go w programie Xamarin Studio (Mac) lub programu Visual Studio (z systemem Windows).

   ![Projekt wyodrębniony w programie Xamarin Studio][9]

   ![Projekt wyodrębniony w programie Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Opcjonalnie) Uruchom projekt dla systemu iOS hello
W tej sekcji możesz uruchomić projektu hello Xamarin iOS dla urządzeń z systemem iOS. Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.

#### <a name="in-xamarin-studio"></a>W programie Xamarin Studio
1. Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie wybierz **Ustaw jako projekt startowy**.

2. Na powitania **Uruchom** menu, wybierz opcję **Rozpocznij debugowanie** toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello.

#### <a name="in-visual-studio"></a>W programie Visual Studio
1. Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie wybierz **Ustaw jako projekt startowy**.

2. Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.

3. W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** projektu iOS toohello dalej pola wyboru.

4. toobuild hello projekt i uruchomić aplikacji hello w emulatorze urządzenia iPhone hello, wybierz hello **F5** klucza.

   > [!NOTE]
   > Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów. Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.    
   >
   >

5. W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).

    ![][10]

    Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure. Dane z hello żądania zostaną wstawione do tabeli TodoItem hello. Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.

    > [!NOTE]
    > Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Opcjonalnie) Uruchom projekt dla systemu Android hello
W tej sekcji możesz uruchomić hello Xamarin droid projektu dla systemu Android. Jeśli nie pracujesz z urządzeniami z systemem Android, możesz pominąć tę sekcję.

#### <a name="in-xamarin-studio"></a>W programie Xamarin Studio

1. Kliknij prawym przyciskiem myszy projekt Android hello, a następnie wybierz **Ustaw jako projekt startowy**.

2. toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Android, na powitania **Uruchom** menu, wybierz opcję **Rozpocznij debugowanie**.

#### <a name="in-visual-studio"></a>W programie Visual Studio

1. Kliknij prawym przyciskiem myszy projekt Android (Droid) hello, a następnie wybierz **Ustaw jako projekt startowy**.

2. Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.

3. W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** pola wyboru dalej toohello projekt systemu Android.

4. toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Android wybierz opcję hello **F5** klucza.

   > [!NOTE]
   > Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów. Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.    
   >
   >

5. W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).

    ![][11]
    
    Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure. Dane z hello żądania zostaną wstawione do tabeli TodoItem hello. Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.
    
    > [!NOTE]
    > Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Opcjonalnie) Uruchom projekt dla systemu Windows hello

W tej sekcji służy do uruchamiania projektu Xamarin WinApp dla urządzeń z systemem Windows hello. Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.

#### <a name="in-visual-studio"></a>W programie Visual Studio

1. Kliknij prawym przyciskiem myszy projekty systemu Windows hello, a następnie wybierz **Ustaw jako projekt startowy**.

2. Na powitania **kompilacji** menu, wybierz opcję **programu Configuration Manager**.

3. W hello **programu Configuration Manager** okno dialogowe, wybierz opcję hello **kompilacji** i **Wdróż** pola wyboru dalej toohello Windows wybranego projektu.

4. toobuild hello projekt i uruchomić aplikacji hello w emulatorze systemu Windows, wybierz opcję hello **F5** klucza.

   > [!NOTE]
   > Jeśli masz problemy z kompilacją hello projektu, uruchom hello NuGet pakietu manager i aktualizacji toohello najnowszą wersję hello Xamarin obsługi pakietów. Projekty Szybki Start może być wolne tooupdate toohello najnowszych wersji.    
   >
   >

5. W aplikacji hello wpisz znaczący tekst, na przykład *Poznaj program Xamarin*, a następnie wybierz hello znak plus (**+**).

    Ta akcja wysyła toohello żądania post, nowe aplikacje mobilne zaplecza, która jest hostowana na platformie Azure. Dane z hello żądania zostaną wstawione do tabeli TodoItem hello. Elementy, które są przechowywane w tabeli hello są zwracane przez hello Mobile Apps ponownie zakończyć i hello się, że dane są wyświetlane na liście hello.
    
    ![][12]
    
    > [!NOTE]
    > Znajdziesz hello kodu, który uzyskuje dostęp do Twojego Mobile Apps zaplecza w hello pliku C# TodoItemManager.cs projektu biblioteki klas przenośnych hello rozwiązania.
    >
    >

## <a name="next-steps"></a>Następne kroki

* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-xamarin-forms-get-started-users.md)  
  Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.

* [Dodaj aplikację tooyour powiadomień wypychanych](app-service-mobile-xamarin-forms-get-started-push.md)  
  Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych Mobile Apps zaplecza toouse usługi Azure Notification Hubs toosend hello.

* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Dowiedz się, jak zaplecza tooadd obsługi w trybie offline dla aplikacji przy użyciu aplikacji mobilnej. Synchronizacja w trybie offline umożliwia wyświetlanie, dodawanie lub modyfikowanie danych aplikacji mobilnej, nawet w przypadku braku połączenia sieciowego.

* [Użyj hello zarządzanego klienta dla aplikacji mobilnych](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Dowiedz się, jak toowork z hello zarządzanego klienta SDK w aplikacji platformy Xamarin.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portalu Azure]: https://portal.azure.com/
