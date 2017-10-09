---
title: "aaaRun dowolnej aplikacji systemu Windows na dowolnym urządzeniu za pomocą usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooshare dowolnej aplikacji systemu Windows z użytkownikami przy użyciu usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Uruchamianie dowolnej aplikacji systemu Windows na dowolnym urządzeniu za pomocą usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Możesz uruchomić aplikację systemu Windows w dowolnym miejscu na dowolnym urządzeniu w tej chwili, korzystając z usługi Azure RemoteApp. Czy chodzi o niestandardową aplikację napisaną 10 lat temu lub aplikacji pakietu Office, użytkownicy nie muszą już powiązane toobe tooa określonym systemem operacyjnym (np. Windows XP) w przypadku kilku aplikacji.

Z usługą Azure RemoteApp z użytkownicy mogą również używać własnych Android lub urządzeń firmy Apple i Pobierz hello tym samym środowisku, jaki zapewnia system Windows (lub z systemem Windows Phone). Jest to możliwe dzięki temu, że aplikacje systemu Windows są hostowane w kolekcji maszyn wirtualnych z systemem Windows na platformie Azure — użytkownicy mogą uzyskiwać do nich dostęp z dowolnego miejsca, jeśli mają połączenie z Internetem. 

Dowiedz się przykładem dokładnie tak jak toodo to.

W tym artykule zamierzamy tooshare Access wszystkim naszym użytkownikom. Można jednak użyć do tego celu dowolnej aplikacji. Tak długo, jak aplikację można zainstalować na komputerze z systemem Windows Server 2012 R2, można udostępnić go przy użyciu hello poniższe kroki. Możesz przejrzeć hello [wymagania dotyczące aplikacji](remoteapp-appreqs.md) toomake się, że aplikacja będzie działać.

Uzyskaj należy pamiętać, że ponieważ dostęp jest bazą danych, a chcemy toobe tej bazy danych przydatne, wykonamy kilka dodatkowych czynności użytkowników toolet dostęp hello dostępu do udziału danych. Jeśli aplikacja nie jest bazą danych lub nie ma potrzeby Twojego użytkowników toobe stanie tooaccess udziału plików, można pominąć te kroki w tym samouczku

> [!NOTE]
> <a name="note"></a>Należy toocomplete konto platformy Azure w tym samouczku:
> 
> * Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): otrzymasz kredyt płatnej usług platformy Azure można użyć tootry wychodzących, a nawet po wyczerpaniu kredytu możesz zachować konto hello i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web. Karty kredytowej nigdy nie zostanie obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.
> * Możesz [aktywować korzyści subskrybenta MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) — w ramach subskrypcji MSDN co miesiąc otrzymasz kredyt, który można przeznaczyć na płatne usługi platformy Azure.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Tworzenie kolekcji w usłudze RemoteApp
Rozpocznij od utworzenia kolekcji. Kolekcja Hello służy jako kontener dla aplikacji i użytkowników. Każdy kolekcja jest oparta na obrazie — można utworzyć własny obraz lub użyć obrazu dostarczonego w ramach subskrypcji. W tym samouczku używamy obraz wersji próbnej pakietu Office 2013 hello — zawiera aplikacji hello czy chcemy tooshare.

1. W portalu Azure hello przewiń w dół w drzewie nawigacji po lewej stronie powitania do momentu ukazania się pozycji RemoteApp. Otwórz tę stronę.
2. Kliknij przycisk **Create a RemoteApp collection** (Utwórz kolekcję RemoteApp).
3. Kliknij pozycję **Szybkie tworzenie** i wprowadź nazwę kolekcji.
4. Wybierz region hello ma toouse toocreate kolekcji. Aby hello najlepsze wyniki, wybierz hello region najbliższy geograficznie lokalizacji toohello, w której użytkownicy będą uzyskiwać dostęp do aplikacji hello. Na przykład w tym samouczku hello użytkowników będzie znajdować się w Redmond, Washington. najbliższy region platformy Azure Hello jest **zachodnie stany USA**.
5. Wybierz plan rozliczeniowy hello, które chcesz toouse. podstawowy plan rozliczeniowy Hello umieszcza 16 użytkowników na dużej maszynie Wirtualnej Azure, natomiast standardowy plan rozliczeniowy hello obejmuje 10 użytkowników na dużej maszynie Wirtualnej Azure. Generalnie, hello plan podstawowy świetnie sprawdza przepływu pracy typ wpisu danych. W przypadku aplikacji biurowych, takich jak pakiet Office odpowiedni będzie plan standardowy hello.
6. Na koniec wybierz obraz pakietu Office 2013 Professional hello. Ten obraz zawiera aplikacje pakietu Office 2013. Dla przypomnienia — ten obraz nadaje się tylko do wersji próbnych kolekcji i weryfikacji koncepcji. Nie można używać tego obrazu w kolekcji przeznaczonej dla systemów produkcyjnych.
7. Teraz kliknij pozycję **Create a RemoteApp collection** (Utwórz kolekcję RemoteApp).

![Tworzenie kolekcji w chmurze w usłudze RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Spowoduje to uruchomienie tworzenia kolekcji, ale może potrwać godzinę tooan.

Teraz wszystko gotowe tooadd użytkowników.

## <a name="share-hello-app-with-users"></a>Aplikacja hello udziału z użytkownikami
Po kolekcji został utworzony pomyślnie, jest toousers dostępu toopublish czasu i dodać użytkowników hello, którzy powinni mieć dostęp do tooit.

Po przejściu od hello Azure RemoteApp węzła podczas tworzenia kolekcji hello, Rozpocznij teraz tworzyć kopie tooit z hello strony głównej systemu Azure.

1. Kliknij utworzoną wcześniej tooaccess dodatkowe opcje kolekcję hello i skonfiguruj hello kolekcji.
   ![Nowa kolekcja usługi RemoteApp w chmurze](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Na powitania **publikowania** , kliknij pozycję **publikowania** u dołu hello hello ekranu, a następnie kliknij przycisk **programy menu Start publikowania**.
   ![Publikowanie programu usługi RemoteApp](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Wybierz aplikacje hello ma toopublish z listy hello. W tym przypadku wybierz program Access. Kliknij przycisk **Complete** (Zakończ). Poczekaj na publikowanie toofinish aplikacji hello.
   ![Publikowanie programu Access w usłudze RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Po zakończeniu publikowania aplikacji hello Przejdź toohello **dostępu użytkownika** karcie tooadd wszyscy użytkownicy hello, które muszą uzyskiwać dostęp do aplikacji tooyour. Wprowadź odpowiednie nazwy użytkowników (adresy e-mail), a następnie kliknij przycisk **Save** (Zapisz).

![Dodaj użytkowników tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. Nadszedł czas tootell użytkowników o nowych aplikacjach i w jaki sposób tooaccess je. toodo, Wyślij e-mail ze wskazaniem adresu URL pobierania klienta pulpitu zdalnego toohello użytkowników.
   ![adres URL pobierania powitania klienta usługi RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Konfigurowanie tooAccess dostępu
Niektóre aplikacje wymagają dodatkowej konfiguracji po wdrożeniu za pośrednictwem usługi RemoteApp. W szczególności aby uzyskać dostęp, jesteśmy toocreate będzie udostępniania plików na platformie Azure, z których każdy użytkownik może uzyskać dostęp. (Jeśli nie chcesz toodo, który można utworzyć [kolekcji hybrydowej](remoteapp-create-hybrid-deployment.md) [zamiast kolekcji w chmurze], która umożliwia użytkownikom dostęp do plików i informacji w sieci lokalnej.) Następnie potrzebujemy tootell toomap naszych użytkowników dysk lokalny na ich toohello komputera systemu plików na platformę Azure.

Witaj pierwszej części, które jako Witaj, Administratorze wykonać. Następnie niektóre kroki zostaną wykonane przez użytkowników.

1. Rozpocznij od publikowania hello interfejsu wiersza polecenia (cmd.exe). W hello **publikowania** wybierz opcję **cmd**, a następnie kliknij przycisk **Publikuj > Publikuj program przy użyciu ścieżki**.
2. Wprowadź nazwę hello aplikacji hello i hello ścieżki. W tym przypadku "File Explorer" jako nazwę hello i "% SYSTEMDRIVE%\windows\explorer.exe" jako użyć hello ścieżki.
   ![Opublikuj plik cmd.exe hello.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Teraz należy toocreate Azure [konta magazynu](../storage/common/storage-create-storage-account.md). Nasze konto nazywa się "accessstorage", "wybrać nazwę, która jest łatwy do rozpoznania tooyou. (toomisquote Highlander, może istnieć tylko jeden "accessstorage".) ![Nasze konto magazynu Azure](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Teraz wróć tooyour pulpitu nawigacyjnego, aby hello ścieżki tooyour magazynu (lokalizacji punktu końcowego). Będzie za chwilę potrzebna, dlatego skopiuj ją w poręczne miejsce.
   ![Ścieżka konta magazynu Hello](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Następnie po utworzeniu konta magazynu hello należy hello podstawowy klucz dostępu. Kliknij przycisk **Zarządzaj kluczami dostępu**, a następnie kopiowania hello podstawowy klucz dostępu.
6. Teraz Ustaw kontekst hello hello konta magazynu i tworzenia nowego udziału plików do dostępu. Uruchom następujące polecenia cmdlet w oknie programu Windows PowerShell z podniesionymi uprawnieniami hello:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Dlatego dla naszego udziału są hello poleceń cmdlet, Uruchamiamy:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

Tego teraz, Włącz hello użytkownika. Najpierw użytkownicy powinni zainstalować [klienta usługi RemoteApp](remoteapp-clients.md). Następnie użytkownicy hello muszą toomap dysku z ich toothat konta Azure pliku udziału utworzonego i dodać swoje pliki programu Access. Należy to wykonać w następujący sposób:

1. W kliencie usługi RemoteApp hello hello dostępu opublikowane aplikacje. Uruchom hello cmd.exe program.
2. Uruchom następujące polecenie toomap hello dysku z udziału plików toohello komputera:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Jeśli ustawisz hello **/ persistent** tooyes parametru hello mapowanie dysku będzie zachowywane między sesjami.
3. Teraz uruchom aplikację Eksploratora plików hello RemoteApp. Skopiuj wszystkie pliki programu Access ma toouse w udziale plików toohello udostępnionej aplikacji hello.
   ![Umieszczanie plików programu Access w udziale na platformie Azure](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Na koniec Otwórz program Access, a następnie otwórz hello bazy danych, udostępnioną. Powinny pojawić się dane w programie Access działającym hello chmury.
   ![Rzeczywiste bazy danych programu Access uruchomiona z hello chmury](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Teraz można używać programu Access na dowolnych urządzeniach — wystarczy zainstalować na nich klienta usługi RemoteApp.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
Po opanowaniu tworzenia kolekcji spróbuj utworzyć [kolekcję korzystającą z usługi Office 365](remoteapp-tutorial-o365anywhere.md). Możesz też utworzyć [kolekcję hybrydową](remoteapp-create-hybrid-deployment.md) z dostępem do sieci lokalnej.

<!--Image references-->

