---
title: "aaaAuthenticate z Mobile Engagement REST API - instalacji ręcznej"
description: "W tym artykule opisano, jak toomanually Instalator uwierzytelniania dla interfejsów API REST, Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Uwierzytelniania w usłudze Mobile Engagement REST API - instalacji ręcznej
To jest zbyt dokumentacji dodatku[Uwierzytelnij z interfejsów API REST usługi Engagement Mobile](mobile-engagement-api-authentication.md). Upewnij się, że odczytu pierwszego tooget hello kontekstu. Opisuje to alternatywny sposób toodo hello jednorazowej konfiguracji konfigurowania uwierzytelniania przy użyciu interfejsów API REST usługi Engagement Mobile hello hello portalu Azure. 

> [!NOTE]
> Poniższe instrukcje Hello są oparte na tym [przewodnik usługi Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) i dostosowywać do co to jest wymagany do uwierzytelniania dla mobilnych interfejsów API usługi Engagement. Aby zapoznać tooit, jeśli chcesz, aby toounderstand hello poniższe kroki szczegółowo. 
> 
> 

1. Tooyour logowania konta Azure za pośrednictwem hello [klasyczny portal](https://manage.windowsazure.com/).
2. Wybierz **usługi Active Directory** w okienku po lewej stronie powitania.
   
     ![Wybierz usługi Active Directory][1]
3. Wybierz hello **domyślne usługi Active Directory** w portalu Azure. 
   
     ![Wybierz katalog][2]
   
   > [!IMPORTANT]
   > Ta metoda działa tylko wtedy, gdy pracujesz w domyślnej hello usługi Active Directory dla konta i nie będzie działać, jeśli robią to w usłudze Active Directory utworzonego w ramach Twojego konta. 
   > 
   > 
4. tooview aplikacji hello w katalogu, kliknij na **aplikacji**.
   
     ![Wyświetl aplikacje][3]
5. Polecenie **dodać**. 
   
     ![Dodawanie aplikacji][4]
6. Polecenie **Dodaj aplikację moją organizację**
   
     ![Nowa aplikacja][5]
7. Wprowadź nazwę aplikacji hello i hello wybierz typ aplikacji jako **interfejsu API sieci WEB i/lub aplikacji sieci WEB** i kliknij przycisk Dalej hello.
   
     ![Nazwa aplikacji][6]
8. Możesz podać wszelkie fikcyjny adresy URL dla **adres URL logowania** i **identyfikator URI aplikacji**. Nie są one używane do naszego scenariusza i adresy URL hello, same nie są weryfikowane.  
   
     ![Właściwości aplikacji][7]
9. Na końcu hello tego będziesz mieć aplikację AAD o nazwie hello, podane wcześniej podobnie następującej hello. Jest to Twoje **AD\_aplikacji\_nazwa** i zapisz go.  
   
     ![Nazwa aplikacji][8]
10. Kliknij nazwę aplikacji hello i wybierz polecenie **Konfiguruj**.
    
      ![Konfigurowanie aplikacji][9]
11. Zanotuj hello Identyfikatora klienta, która będzie służyć jako **klienta\_identyfikator** do interfejsu API wywołania. 
    
     ![Konfigurowanie aplikacji][10]
12. Przewiń w dół toohello **klucze** i Dodaj klucz o najlepiej czas trwania 2 lata (wygaśnięcia) i kliknij pozycję **zapisać**. 
    
     ![Konfigurowanie aplikacji][11]
13. Skopiuj natychmiast hello wartość, która jest wyświetlana dla klucza hello jest wyświetlana tylko teraz, a nie są przechowywane, więc nie zostanie nigdy ponownie wyświetlone. W przypadku utraty następnie konieczne będzie toogenerate nowy klucz. Są to hello **CLIENT_SECRET** do interfejsu API wywołania. 
    
     ![Konfigurowanie aplikacji][12]
    
    > [!IMPORTANT]
    > Ten klucz wygaśnie o hello końca czasu trwania hello określenia tak toorenew się upewnij, który go, gdy czas hello w przeciwnym razie uwierzytelnianie interfejsu API nie będzie już działać. Można również usunąć i ponownie utwórz ten klucz, jeśli uważasz, że został złamany.
    > 
    > 
14. Polecenie **WYŚWIETL punkty końcowe** przycisk teraz który spowoduje to otwarcie hello **punkty końcowe aplikacji** okno dialogowe. 
    
    ![][13]
15. Okno dialogowe punkty końcowe aplikacji hello, skopiuj hello **KOŃCOWYM TOKENÓW OAUTH 2.0**. 
    
    ![][14]
16. Ten punkt końcowy będzie powitania po formularza, gdzie jest hello identyfikatora GUID w adresie URL hello Twojej **TENANT_ID** tak zanotuj go: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Obecnie firma Microsoft będzie kontynuowana tooconfigure hello uprawnienia do tej aplikacji. Dla tego trzeba będzie tooopen się hello [portalu Azure](https://portal.azure.com). 
18. Polecenie **grup zasobów** i Znajdź hello **Mobile Engagement** grupy zasobów.  
    
    ![][15]
19. Kliknij przycisk hello **Mobile Engagement** zasobów grupy i przejdź toohello **ustawienia** bloku, w tym miejscu. 
    
    ![][16]
20. Polecenie **użytkowników** w hello bloku ustawienia, a następnie kliknij polecenie **Dodaj** tooadd użytkownika. 
    
    ![][17]
21. Polecenie **wybierz rolę**
    
    ![][18]
22. Polecenie **właściciela**
    
    ![][19]
23. Wyszukaj nazwę aplikacji hello **AD\_aplikacji\_nazwa** hello pola wyszukiwania. Domyślnie w tym miejscu nie będą widzieć to. Po znalezieniu go, zaznacz go i kliknij na **wybierz** u dołu hello hello bloku. 
    
    ![][20]
24. Na powitania **dostępu Dodaj** bloku, zostanie wyświetlona jako **użytkownika 1, 0 grupy**. Kliknij przycisk **OK** na temat tej zmiany hello tooconfirm bloku. 
    
    ![][21]

Ukończono hello wymaganych konfiguracji usługi AAD i są wszystkie hello toocall zestaw interfejsów API. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



