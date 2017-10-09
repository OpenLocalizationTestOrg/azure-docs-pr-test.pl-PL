---
title: "aaaGet hello tym samym środowisku usługi Office 365 na dowolnym urządzeniu za pomocą usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooshare dowolną aplikację Office 365 z użytkownikami przy użyciu usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello sam środowisku usługi Office 365 na dowolnym urządzeniu za pomocą usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

W tym artykule opisano sposób toodeploy usługi Office 365 na dowolnym urządzeniu w firmie. Użytkowników można uzyskać hello takie same możliwości i interfejsu użytkownika występuje w systemach Android, firmy Apple i systemu Windows.

Osiągniemy ten cel dzięki usłudze Azure RemoteApp, obsługując usługę Office 365 na skalowalnych maszynach wirtualnych platformy Azure, z którymi użytkownicy mogą nawiązywać połączenie. Ten zestaw maszyn wirtualnych nazywamy „kolekcją w chmurze”.

## <a name="create-a-cloud-collection"></a>Tworzenie kolekcji w chmurze
Najpierw po utworzeniu konta platformy Azure, przejdź zbyt**RemoteApp** , klikając łącze hello na powitania po lewej stronie.
![Wyświetlanie usługi Azure RemoteApp na powitania portalu Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Kontynuuj, klikając **nowe** na dole hello i "szybko tworząc" kolekcję. Podaj nazwę, hello region, hello subskrypcji, hello plan i obraz powitania "Office Proffesional 2013", który firma Microsoft udostępnia.
![Okno dialogowe tworzenia](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Po zakończeniu należy uruchomić proces tworzenia kolekcji hello formularza hello. To może potrwać godzinę tooan.

![Oczekiwanie](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Po zakończeniu procesu hello ekran będzie wyglądać następująco. Po kliknięciu pozycji **Publikowanie** zobaczysz, że większość aplikacji pakietu Office została już opublikowana.
![Utworzona kolekcja](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Opublikowane aplikacje](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

W tym momencie można również dodać więcej użytkowników, którzy mają dostęp toothis kolekcji, klikając **dostępu użytkownika**.
![Konfigurowanie dostępu użytkowników](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Teraz spróbujmy łączenie tooOffice 365!

## <a name="connect-toooffice-365"></a>Połącz tooOffice 365
Przejdź przez zbyt[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), przewiń w dół i kliknij przycisk **klientów pobrać** tooinstall hello Azure RemoteApp klienta na powitania urządzenia możesz teraz. Witaj poniższe zrzuty ekranu dotyczą systemu Windows.

Po uruchomieniu aplikacji hello użytkownik zostanie zapytany toosign przy użyciu swojego konta Microsoft (nazywanych wcześniej "Live ID"), użyj hello używanego jako konto platformy Azure dla teraz. Po zalogowaniu zobaczysz powiadomienia o nowych zaproszeniach. Kliknij w tym miejscu, aby wyświetlić listę podobną do poniższej. Zaakceptuj zaproszenie hello, odpowiadające adresowi e-mail właściciela konta platformy Azure.

![Nowe zaproszenie](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Ekran z nowymi zaproszeniami wygląda następująco:

![Akceptowanie zaproszenia](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Po zaakceptowaniu zaproszenia hello powinny być widoczne wszystkie aplikacje pakietu Office hello powitania klienta usługi Azure RemoteApp.

![Lista aplikacji](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Po kliknięciu na żadnym z tych aplikacji hello należy uruchomić na powitania maszyny wirtualnej platformy Azure i powinno być wszystko gotowe! Owocnej pracy.

![uruchamianie](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

