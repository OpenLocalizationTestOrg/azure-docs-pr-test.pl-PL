---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Podręcznik publikowania danych usługi dla hello Azure Marketplace
> [!IMPORTANT]
> **W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.** Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners). Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Po ukończeniu hello w kroku 1, [tworzenia kont i rejestracji](marketplace-publishing-accounts-creation-registration.md), możemy przewodnikiem za pośrednictwem hello [ogólne nietechnicznej](marketplace-publishing-pre-requisites.md) i [wymagania techniczne](marketplace-publishing-data-service-creation-prerequisites.md) usługi danych oferty w portalu Azure Marketplace. Obecnie firma Microsoft przeprowadzi Cię przez kroki hello tworzenia oferty usługi danych na powitania [Portal publikowania] [ link-pubportal] dla hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Toohello logowania Portal publikowania.
Przejdź do zbyt[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Dla pierwszego czasu tooPublishing logowania portalu Użyj tego samego konta, z którą profil sprzedawcy firmy zarejestrowano w Centrum deweloperów powitalne.**  (Później możesz dodać każdy pracownik firmy jako współadministrator w hello publikowania portalu).

Polecenie hello **publikowania usług danych** kafelka, jeśli jest to hello pierwszego logowania do portalu publikowania hello.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Wybierz **usług danych** w menu nawigacji hello na powitania po lewej stronie.
  ![Rysowanie](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Tworzenie nowej usługi danych
Wypełnij hello tytuł dla Twojej nowych danych usługi oferty i kliknij na "+" na powitania prawo.

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Przejrzyj hello podmenu w obszarze hello nowo utworzona Usługa danych w menu nawigacji hello.
Polecenie hello **wskazówki** i przejrzyj wszelkie niezbędne kroki potrzebne toopublish prawidłowo hello Usługa danych na hello Azure Marketplace.

> [!TIP]
> Należy zawsze kliknij hello łączy na stronie "Wskazówki" hello lub użyj karty w podmenu oferty usługi danych powitania po lewej stronie powitania.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Utwórz nowy Plan.
### <a name="offers-plans-transactions"></a>Oferuje planów, transakcje.
Każda oferta może mieć wiele planów, ale musi mieć co najmniej jednego (1) planu. Użytkownicy końcowi subskrypcji oferta tooyour one subskrypcji dla jednego planu hello oferty. Każdy plan określa, jak użytkownicy końcowi będą się mogli toouse usługi.

Obecnie portalu Azure Marketplace obsługuje tylko miesięczne transakcji subskrypcji na podstawie modelu usług danych, tj. użytkownicy końcowi będą zwrócić miesięczna zgodnie z toohello ceny hello specjalnego planu subskrybowanego one tooand będą mogli tooconsume numer każdego miesiąca zdefiniowane przez hello plan transakcji.

Każdą transakcję zazwyczaj definiowane jako liczba rekordów, który zwróci dane usługi na podstawie hello zapytania wysyłane toohello usługi. Witaj domyślna to 100. Liczba transakcji zwrócił tooeach zapytanie zostanie liczba rekordów podzielona przez 100 i zostać zaokrąglona w górę do najbliższej liczby całkowitej toohello.

Jest usługę Azure Marketplace warstwy odpowiedzialność toomonitor (licznik) liczba transakcji używane przez każdego zapytania.

> [!IMPORTANT]
> Użytkowników końcowych, które osiągnęła limit transakcji hello w miesiącu hello zostanie zablokowane przed kontynuowaniem toouse hello usługi do końca ich miesięcznego cyklu subskrypcji.
> 
> Hello planu lub jeden z planów hello może ale nie musi zawierać nieograniczoną liczbę transakcji.
> 
> 

### <a name="create-a-plan"></a>Tworzenie planu.
1. Polecenie **"+"** dalej toohello "Dodaj nowy plan".
2. Wybierz jedną z opcji hello: **nieograniczone** lub **ograniczone** użycia tego planu.  Jeśli Limited następnie podaj numer hello planu hello transakcji umożliwia tooconsume w ciągu miesiąca.
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Publikowanie portalu będzie również sugerować "Identyfikator planu", który będzie używany toocommunicate toohello użytkowników końcowych hello Nazwa planu hello hello interfejsu użytkownika i również używane przez hello usługi rynek tooidentify hello planu. Witaj "Identyfikator planu" można zmienić, jeśli chcesz.
   
   > [!NOTE]
   > Witaj "Identyfikator planu" musi być unikatowa w zakresie hello każdego oferty. Jak użyć innych identyfikatorów w hello identyfikator zostanie zablokowane po hello pierwszy tooproduction publikowania i nie będzie możliwe toochange publikowania planowanie portalu tego identyfikatora.
   > 
   > 
3. Kliknij przycisk tooaccept wybór.
4. Następnie użytkownik zostanie poproszony kilka dodatkowych pytań dotyczących nowo utworzony Plan.
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Zapytania | Istotności. |
| --- | --- |
| **Ten Plan jest wolne i dostępne na całym świecie?** |Można utworzyć planu całkowicie wolne z — bezpłatnie. Jego hello tylko plan dla tej oferty — oznacza, że w przypadku publikowania "Oferty bezpłatnej" w hello Marketplace. Jeśli jest tylko dla jednego (z kilku) planu, hello umożliwia toolearn użytkownicy końcowi toooffer opcję więcej informacji na temat usługi z stosunkowo małej liczby transakcji w miesiącu.  W przypadku odpowiedzi hello "Tak", nie dalsze pytania będzie monitowany. |

> [!NOTE]
> Użytkownicy końcowi zawsze można uaktualnić toohello płatnej planów.
> 
> 

| Zapytania | Istotności. |
| --- | --- |
| **Bezpłatna wersja próbna jest dostępny?** |Można wybrać między słowo "Trial nr" na wszystkich lub podać toouse opcji Plan "Miesiąc". Wydawcy, takich jak toouse tej opcji tooprovide użytkownicy końcowi hello możliwości toounderstand hello zalet hello oferuje bezpłatnie przez jeden miesiąc. |

> [!IMPORTANT]
> Użytkownicy końcowi będą tylko stanie toopurchase bezpłatnej wersji próbnej, jeśli ustanowionego instrumentem płatniczym np. karty kredytowej, umowy enterprise agreement.
> 
> Po upływie miesiąca hello bezpłatnej wersji próbnej portalu Azure Marketplace spowoduje uruchomienie ładowania klientów cen hello dzień hello hello subskrypcji, chyba że powitania klienta inicjowane hello anulowania subskrypcji. Nie specjalne powiadomienia będą dostarczane toohello użytkowników końcowych.
> 
> 

| Zapytania | Istotności. |
| --- | --- |
| **Ten plan wymaga toopurchase kod promocji?** |Wydawcy ma tootheir dostępu toolimit opcji plany usługi podając specjalne kodu, o nazwie "A Promocode" toospecific klientów. Tylko użytkownicy końcowi, których ten Promocode będą mogli toosubscribe toohello planu. Jeśli wybierzesz opcję "Nie", potwierdzam, że wszyscy z regionu hello gdzie oferują hello są dostępne (zobacz [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) więcej szczegółów) będą mogli toosubscribe toothis planu. Nie dalsze pytania pojawi się monit. |
| **Również ukryć ten plan z każdego, kto nie ma kod promocyjny prawidłowy?** |Jeśli hello odpowiedzi toohello poprzedniego pytania "Tak" hello wydawcy ma toocompletely opcja Usuń ten plan z znajdujących się w hello UI hello Marketplace. Oznacza to, klienci nie będą widzieć tego planu, na stronie Szczegóły hello oferty. Użytkownicy końcowi, które otrzymają promocode toopurchase, będzie on tooit toosubscribe możliwe przy użyciu tego promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Tworzenie z witryny Marketplace marketingu zawartości
Dla jak tooprovide informacje wymagane w **Marketing, cennik, pomocy technicznej i kategorie** karty odwiedź [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) co jest typowe artefakty tooall opublikowane w hello Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Połącz z tooyour oferty usługi (na podstawie usług SQL Azure lub usługi sieci Web na podstawie).
Polecenie hello **usług danych** podmenu.

W górnej części strony hello hello użytkownik zostanie zapytany oferta hello tooprovide **Namespace**.  

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.png)

Hello poniżej pytanie definiują sposób hello wydawcy będzie tooexpose nowo utworzony tooAzure oferta portalu Marketplace. (Więcej informacji można znaleźć hello [podręcznik techniczny wymagań wstępnych usług danych](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Publikowanie hello na podstawie bazy danych usługi**

Polecenie **bazy danych**. pojawi się Hello następujące strony:

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate mapowanie CSDL hello zestawu danych oparte na powitania bazy danych SQL Azure:

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.4.png)

A następnie dla każdej tabeli

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.6.png)

Jeśli usługa sieci Web

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Odczyt [mapowania istniejące sieci web tooOData usługi za pośrednictwem CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) Aby uzyskać szczegółowe instrukcje i przykłady dotyczące tworzenia CSDL usługi sieci Web.
> 
> 

## <a name="next-steps"></a>Następne kroki
Teraz, po utworzeniu tej oferty usługi danych, upewnij się, że ukończeniu instrukcjami hello hello [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed przejściem do przodu zbyt[testowania w przejściowymusługidanych](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: Jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)
* Jeśli interesuje Cię w uzgodnieniu hello ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definicje, struktur i instrukcje.
* Jeśli interesuje Cię learning oraz opis hello określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.
* Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee przykładowy kod i zrozumienie Składnia kodu i kontekstu.

[link-pubportal]:https://publish.windowsazure.com
