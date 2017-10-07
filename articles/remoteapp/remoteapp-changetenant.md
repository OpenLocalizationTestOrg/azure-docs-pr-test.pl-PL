---
title: "dzierżawy usługi Azure Active Directory hello aaaChange w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dzierżawy usługi Azure Active Directory hello toochange skojarzony z usługą Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Zmiana dzierżawy usługi Azure Active Directory hello w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp używa dostępu użytkownika tooallow usługi Azure Active Directory (Azure AD). Witaj, co skojarzony z hello subskrypcji platformy Azure jest dostępna dzierżawa Hello tylko usługi Azure AD, używanego w usłudze Azure RemoteApp. Można wyświetlić hello skojarzone subskrypcji na powitania **ustawienia** w portalu hello na stronie. Przyjrzyj się hello **katalogu** kolumny na powitania **subskrypcje** kartę.

> [!NOTE]
> Dla tego toosucceed zmiany należy najpierw usunąć wszystkich użytkowników z istniejącą dzierżawą usługi Azure Active Directory hello ze wszystkich kolekcji usługi Azure RemoteApp. toodo tego toohello Przejdź w portalu Azure, przejdź toohello **usługi Azure RemoteApp** karcie, a następnie otwórz każdej kolekcji usługi Azure RemoteApp. Przejdź toohello **użytkowników** karcie i usuwanie użytkowników, którzy należą tooyour bieżącej dzierżawie usługi Azure Active Directory. Powtórz dla wszystkich istniejących kolekcji usługi Azure RemoteApp. Bez tej czynności nie będzie możliwe toocreate lub kolekcji poprawki.
> 
> 

Jeśli chcesz toouse innej dzierżawy, użyj te kroki toochange hello skojarzenia z subskrypcją:

1. W portalu hello, usuń wszelkie toowhich użytkowników usługi Azure AD został przez Ciebie udzielony dostęp tooAzure kolekcji usługi RemoteApp. (Zobacz Uwaga hello powyżej kroki dotyczące toodo to.)
2. Ustaw konto Microsoft (wcześniej nazywanych Live ID) jako hello administratora usługi. (Nie wiadomo, czy są już Witaj, Administratorze usługi? Można sprawdzić, klikając **Ustawienia -> Administratorzy**.) Teraz Oto jak zmienić który:
   
   1. Kliknij hello użytkownika w prawym górnym rogu hello, a następnie kliknij przycisk **wyświetlić mojego rachunku**.
   2. Kliknij subskrypcję hello. Następnie na nowej stronie powitania, przewiń w dół i kliknij **Edytuj szczegóły subskrypcji** w hello prawo. (Sortowania hello środkowej u dołu po prawej, jeśli pomaga go znaleźć.)
   3. Typ konta Microsoft hello hello użytkownik, który powinien być administratorem hello usługi.
3. Teraz Wyloguj się hello portalu, a następnie zaloguj się ponownie przy użyciu konta Microsoft, które są określone w poprzednim kroku hello hello.
4. Kliknij przycisk **nowy -> Aplikacja usługi -> Active Directory -> Directory -> niestandardowe tworzenie**.
5. W obszarze **katalogu**, wybierz **Użyj istniejącego katalogu**. Zamierzamy toohave toosign poza hello portalu, więc wybierzesz **jestem toobe gotowa, teraz wylogować**.
6. Zaloguj się ponownie do hello portalu jako administrator globalny katalogu hello ma tooadd. (Jeśli już byłeś administratorem globalnym, będzie po zaokrąglona z Zaloguj się, a następnie zaloguj.)
7. Użytkownik zostanie zapytany przy logowaniu w, jeśli chcesz toouse istniejącej dzierżawy AD w ramach subskrypcji. Kliknij przycisk **Kontynuuj**, a następnie kliknij przycisk **Wyloguj się teraz**.
8. Zalogować ponownie, a następnie wróć za**Ustawienia -> Subskrypcje**. Wybierz subskrypcję, a następnie kliknij przycisk **Edytuj katalog**. Wybierz, które mają toouse dzierżawy hello Azure AD.

Można teraz używać hello nowej usługi Azure AD dzierżawy toocontrol dostępu toohello Azure subskrypcji i tooconfigure dostępu użytkowników w usłudze Azure RemoteApp.

