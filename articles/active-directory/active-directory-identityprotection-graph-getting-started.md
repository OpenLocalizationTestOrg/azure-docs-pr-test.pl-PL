---
title: "aaaGet wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph | Dokumentacja firmy Microsoft"
description: "Zawiera wprowadzenie tooquery Microsoft Graph listę zdarzeń o podwyższonym ryzyku i skojarzonych informacji z usługi Azure Active Directory."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, zdarzenie ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph
Program Microsoft Graph jest hello Microsoft unified punkt końcowy interfejsu API i hello macierzystego z [Azure Active Directory Identity Protection](active-directory-identityprotection.md) interfejsów API. pierwszy interfejsu API Hello **identityRiskEvents**, pozwala tooquery Microsoft Graph, aby uzyskać listę z [ryzyka zdarzenia](active-directory-identityprotection-risk-events-types.md) i skojarzone z nimi informacje. W tym artykule pobiera pracę podczas badania tego interfejsu API. Szczegółowe wprowadzenie, pełną dokumentację i toohello dostępu Explorer wykresu, zobacz hello [witryny Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

Istnieją trzy kroki tooaccessing tożsamości ochrony danych za pomocą programu Microsoft Graph:

1. Dodawanie aplikacji przy użyciu klucza tajnego klienta. 
2. Użyj tego klucza tajnego i kilka innych części informacji tooauthenticate tooMicrosoft wykresu służący do otrzymywania tokenu uwierzytelniania. 
3. Użyj tego punktu końcowego tokenu toomake żądań toohello interfejsu API i wrócić tożsamości ochrony danych.

Przed rozpoczęciem pracy należy:

* Aplikacji hello toocreate uprawnień administratora w usłudze Azure AD
* Witaj nazwy domeny Twojej dzierżawy (np. contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Dodawanie aplikacji z klucz tajny klienta
1. [Zaloguj się](https://manage.windowsazure.com) tooyour klasycznego portalu Azure jako administrator. 
2. W okienku nawigacji po lewej stronie powitania polecenie **usługi Active Directory**. 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.
4. W menu hello na górze hello, kliknij przycisk **aplikacji**.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Kliknij przycisk **Dodaj** u dołu hello hello strony.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Na powitania **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. W hello **nazwa** tekstowym, wpisz nazwę dla aplikacji (np.: Aplikacja interfejsu API zdarzenia ryzyka AADIP).
   
    b. Jako **typu**, wybierz pozycję **aplikacji sieci Web i / lub interfejs API sieci Web**.
   
    c. Kliknij przycisk **Dalej**.
8. Na powitania **właściwości aplikacji** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. W hello **adres URL logowania** pole tekstowe, typ `http://localhost`.
   
    b. W hello **identyfikator URI aplikacji** pole tekstowe, typ `http://localhost`.
   
    c. Kliknij przycisk **Complete** (Zakończ).

Możesz teraz skonfigurować aplikacji.

![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Przyznaj hello toouse uprawnień z aplikacji interfejsu API
1. Na stronie aplikacji hello menu u góry hello kliknij **Konfiguruj**. 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. W hello **uprawnienia aplikacji tooother** kliknij **Dodaj aplikację**.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Na powitania **uprawnienia aplikacji tooother** okna dialogowego, wykonaj następujące kroki hello:
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Wybierz **Microsoft Graph**.
   
    b. Kliknij przycisk **Complete** (Zakończ).
4. Kliknij przycisk **uprawnienia aplikacji: 0**, a następnie wybierz **odczytać wszystkie informacje dotyczące zdarzenia ryzyka tożsamości**.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Kliknij przycisk **zapisać** u dołu hello hello strony.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Uzyskiwanie klucza dostępu
1. Na stronie aplikacji hello **klucze** wybierz 1 rok jako czas trwania.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Kliknij przycisk **zapisać** u dołu hello hello strony.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. w sekcji klucze hello skopiuj wartość hello nowo utworzony klucz i wklej go w bezpiecznym miejscu.
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > W przypadku utraty tego klucza, będzie zawierać sekcję toothis tooreturn i Utwórz nowy klucz. Zachowaj ten klucz tajny: każdy użytkownik, który można uzyskać dostęp do danych.
   > 
   > 
4. W hello **właściwości** hello kopiowania, sekcji **identyfikator klienta**, a następnie wklej go w bezpiecznym miejscu. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Uwierzytelnianie tooMicrosoft wykres i hello zapytania interfejsu API zdarzenia ryzyka tożsamości
W tym momencie powinny mieć:

* Identyfikator klienta Hello skopiowane powyżej
* klucz Hello, skopiowane powyżej
* Witaj nazwy domeny Twojej dzierżawy

tooauthenticate, wysyłania post żądania zbyt`https://login.microsoft.com` z następujących parametrów w treści hello hello:

* Typ grant_type: "**client_credentials**"
* Zasób: "**https://graph.microsoft.com**"
* client_id:<your client ID>
* client_secret:<your key>

> [!NOTE]
> Wymagane wartości tooprovide dla hello **client_id** i hello **client_secret** parametru.
> 
> 

Jeśli to się powiedzie, to zwraca token uwierzytelniania.  
Witaj toocall interfejsu API, Utwórz nagłówek z hello następującego parametru:

    `Authorization`=”<token_type> <access_token>"


Podczas uwierzytelniania, można znaleźć typu tokenu hello i token dostępu w hello zwrócił token.

Wyślij ten nagłówek jako toohello żądania, po adresem URL interfejsu API:`https://graph.microsoft.com/beta/identityRiskEvents`

odpowiedź Hello w przypadku powodzenia jest kolekcją tożsamości zdarzenia o podwyższonym ryzyku i skojarzone dane w formacie OData JSON, który może być analizowana i obsługiwane zgodnie z własnymi potrzebami hello.

Oto przykładowy kod do uwierzytelniania i wywoływanie interfejsu API hello przy użyciu programu Powershell.  
Wystarczy dodać Identyfikatora klienta, a dla klucza dzierżawy domeny.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Następne kroki
Gratulacje, właśnie utworzony pierwszy tooMicrosoft wywołania wykresu!  
Teraz można zbadać zdarzenia o podwyższonym ryzyku tożsamości i użyć hello danych, jednak użytkownik mieści się w temacie.

toolearn więcej informacji na temat programu Microsoft Graph i jak toobuild aplikacji przy użyciu hello interfejsu API programu Graph, zobacz hello [dokumentacji](https://graph.microsoft.io/docs) i znacznie więcej informacji na temat hello [witryny Microsoft Graph](https://graph.microsoft.io/). Ponadto upewnij się, że hello toobookmark [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) strony, która zawiera listę wszystkich hello tożsamości ochrony interfejsami API dostępnymi w wykresie. Jak możemy dodać nowe sposoby toowork z ochrony tożsamości za pomocą interfejsu API, zobaczysz je na tej stronie.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md)
* [Rodzaje zdarzeń o podwyższonym ryzyku wykrywanych przez Azure Active Directory Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Omówienie programu Microsoft Graph](https://graph.microsoft.io/docs)
* [Katalogu głównego usługi programu Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

