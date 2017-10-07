---
title: "Witaj toouse aaaHow pakietu zawartości usługi Azure Active Directory Power BI | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello pakietu zawartości usługi Azure Active Directory Power BI"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Jak toouse hello pakietu zawartości usługi Azure Active Directory Power BI

Zrozumienie, jak użytkownicy korzystają z funkcji usługi Azure Active Directory, jest bardzo ważne dla Ciebie jako administratora IT. Pozwala ona tooplan Twojego użycia tooincrease infrastruktury i komunikacja IT i tooget najbardziej hello poza funkcji usługi AAD. Power BI Content Pack dla usługi Azure Active Directory zapewnia hello toofurther możliwości analizowanie Twojej toounderstand danych, jak używasz tego danych toogather bardziej rozbudowane wgląd w informacje co się dzieje z ich Azure Active Directory dla hello różnych funkcjach można znacznie zależne.  Dzięki integracji hello interfejsów API usługi Azure Active Directory do usługi Power BI można łatwo pobrać hello wbudowanych pakietów zawartości i Uzyskaj wgląd w działania hello tooall w usłudze Azure Active Directory za pomocą wizualizacji rozbudowane środowisko, oferowanych przez usługę Power BI. Możesz utworzyć własny pulpit nawigacyjny i w prosty sposób udostępnić go innym osobom w organizacji. 

Ten temat zawiera o uzyskać szczegółowe instrukcje dotyczące sposobu tooinstall i użyj hello zawartości pakietu w danym środowisku.

## <a name="installation"></a>Instalacja  

**Witaj tooinstall pakiet zawartości Power BI:**

1. Zaloguj się do [usługi Power BI](https://app.powerbi.com/groups/me/getdata/services) z kontem Power BI (jest to hello tego samego konta jako usługi Office 365 lub konto usługi Azure AD).

2. U dołu okienka nawigacji po lewej stronie powitania hello, wybierz **Pobierz dane**.

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. W hello **usług** kliknij **uzyskać**.
   
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Wyszukaj usługę **Azure Active Directory**.

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Po wyświetleniu monitu wpisz swój identyfikator dzierżawy Azure AD, a następnie kliknij przycisk **Dalej**.

    > [!TIP] 
    > Szybko tooget hello identyfikatora dzierżawy dla dzierżawcy usługi Office 365 / usługi Azure AD jest toohello toologin Portal programu Azure AD, przejść do szczegółów toohello katalogu i skopiuj identyfikator hello z hello następującego adresu URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension lubkatalogu/<tenantid>/directoryQuickStart

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Kliknij przycisk **Zaloguj**. 
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**.
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  W oknie dialogowym zgody aplikacji hello, kliknij przycisk **Akceptuj**.
 
9.  Po utworzeniu pulpitu nawigacyjnego dzienników aktywności usługi Azure Active Directory kliknij go.
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>Co można zrobić z tym pakietem zawartości?

Przed możemy przejść do czynności z tym pakietem zawartości, w tym krótki przegląd hello różne raporty w hello zawartości pakietu. Raport dane Przechodzi wstecz toohello **ostatnich 30 dni**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Raporty zawarte w tej wersji pakietu zawartości usługi Azure Active Directory

**Raport dotyczący użycia aplikacji i Trend**: Uzyskaj wgląd w aplikacje hello używane w organizacji oraz te, które są używane najczęściej hello i kiedy. Można użyć tego raportu toogather wgląd w informacje sposobu używania aplikacji, które niedawno wycofane w organizacji lub sprawdzić, które aplikacje są popularne. W ten sposób można poprawić użycia, jeśli zostanie wyświetlony, jeśli aplikacja hello nie jest używany.

**Logowania według lokalizacji i użytkownicy**: Uzyskaj wgląd w wszystkich hello logowania wykonywane przy użyciu tożsamości Azure i zapewnia wgląd w informacje hello tożsamość hello użytkowników. Dzięki temu możesz zagłębić się w szczegóły poszczególnych logowań i odpowiedzieć na pytania:

- Skąd loguje się dany użytkownik?
- Użytkownika, który ma hello większości logowania i gdzie one logowania z? 
- Powiodła logowania hello?  
 
Możesz przejść do szczegółów, klikając określoną datę lub lokalizację.

**Unique users per app** (Liczba unikatowych użytkowników aplikacji): wyświetla wszystkich unikatowych użytkowników korzystających z danej aplikacji. Dotyczy tylko użytkowników, którzy *pomyślnie* zalogowali się do aplikacji.

**Urządzenie logowania**: wyświetlać hello typ systemu operacyjnego i przeglądarki są używane przez użytkowników w organizacji za pomocą szczegółowe informacje na temat użytkowników hello, w tym:

- Nazwa użytkownika
- Adres IP
- Lokalizacja 
- Stan logowania 

W tym raporcie można zrozumieć hello różnych profilów urządzenia używane w organizacji i ustalić na podstawie co zasady urządzeń

**SSPR Funnel** (Lejek SSPR): pomaga w zrozumieniu procesu resetowania haseł w Twojej organizacji. Pobierz rzut oka na ile hasła resetuje podjęto za pomocą narzędzia SSPR hello i ile z nich zostały pomyślnie. Wyświetlić elementy podrzędne awarii resetuje hasło hello za pomocą lejka SSPR hello i zrozumienie, dlaczego pewnych błędów wystąpił. Ten raport zawiera głębsze zrozumienie sposobu używania narzędzia SSPR hello w danej organizacji, możesz wprowadzić hello prawidłowych decyzji.

## <a name="customizing-azure-ad-activity-content-pack"></a>Dostosowywanie pakietu zawartości usługi Azure AD Activity

**Zmień wizualizacji**: wizualizacji raportu można zmienić, klikając **Edytuj raport** i wybierz wizualizację hello ma.
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Dodatkowe pola**: można dodać raport toohello pola lub usuń go, wybierając hello toowhich visual pole hello tooadd lub Usuń. W poniższym przykładzie hello dodaję widoku tabeli toohello pola "stan logowania". 
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Pulpit nawigacyjny tooyour wizualizacje numeru PIN**: można dostosować pulpit nawigacyjny i zawiera własną raportu toohello wizualizacje i przypiąć go toohello pulpitu nawigacyjnego. W poniższym przykładzie hello I dodaje nowy filtr o nazwie "stan logowania" i objęte hello raportu. I również zmienić wizualizacji hello z wykres liniowy tooa wykresu słupkowego i można przypiąć ten nowy pulpit nawigacyjny visual toohello.

![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Udostępnianie pulpitu nawigacyjnego**: po utworzeniu hello zawartości, która ma można udostępnić pulpit nawigacyjny hello hello użytkowników w organizacji. Należy pamiętać, że po udostępnieniu hello raportu widzą hello wybrane w raporcie hello pola.
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Planowanie codziennego odświeżania raportu usługi Power BI

tooschedule codzienne odświeżanie raportu usługi Power BI, przejdź zbyt**zestawów danych > Ustawienia > Planowanie odświeżania** i ustaw ją, jak pokazano poniżej.
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Aktualizowanie wersji toonewer pakietu zawartości

Jeśli chcesz, aby tooupdate zawartości pakietu tooget nowszej wersji:

- Pobierz nowy pakiet zawartości hello i skonfigurować zgodnie z instrukcjami wymienione w tym artykule.

- Po skonfigurowaniu go, przejdź zbyt**źródło danych > Ustawienia > poświadczenia źródła danych** i ponownie wprowadź swoje poświadczenia, jak pokazano poniżej

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Jak działa nowa wersja pakietu zawartości hello hello, należy usunąć starą wersję hello w razie potrzeby poprzez usunięcie hello podstawowych raportów i zestawów danych skojarzonych z tego pakietu zawartości.

## <a name="still-having-issues"></a>Nadal masz problemy? 

Zapoznaj się z [przewodnikiem rozwiązywania problemów](active-directory-reporting-troubleshoot-content-pack.md). Ogólną pomoc dotyczącą usługi Power BI można znaleźć w następujących [artykułach pomocy](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Następne kroki

Omówienie raportowania patrz hello [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).
