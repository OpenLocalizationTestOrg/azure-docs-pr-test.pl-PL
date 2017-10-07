---
title: "aaaSet niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstaw łączniki serwera Proxy aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Ustaw niestandardową stronę główną dla opublikowanych aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD

W tym artykule omówiono sposób tooconfigure aplikacji toodirect użytkowników tooa niestandardową stronę główną. Podczas publikowania aplikacji przy użyciu serwera Proxy aplikacji ustawić wewnętrzny adres URL, ale czasami nie jest to hello strony, które należy najpierw widzą użytkownicy. Ustawić niestandardową stronę główną, dzięki czemu użytkownicy Przejdź toohello prawej strony, przy uzyskiwaniu dostępu do aplikacji hello hello Azure Panel dostępu usługi Active Directory lub uruchamiania aplikacji hello usługi Office 365.

Gdy użytkownicy uruchomią aplikację hello, są zaleceniami adresu URL domeny katalogu głównego toohello domyślne hello opublikowanych aplikacji. Strona docelowa Hello zwykle jest ustawiony jako adres URL strony głównej hello. Adresy URL niestandardowej strony głównej toodefine hello Azure AD PowerShell modułu należy używać tooland użytkowników aplikacji w konkretnej strony w aplikacji hello. 

Na przykład:
- W sieci firmowej użytkownicy przejść za*https://ExpenseApp/login/login.aspx* toosign w i uzyskiwać dostęp do aplikacji.
- Ponieważ inne zasoby, takie jak obrazy wymagane przez serwer Proxy aplikacji tooaccess na najwyższym poziomie struktury folderów hello hello, publikowania aplikacji hello z *https://ExpenseApp* jako hello wewnętrznego adresu URL.
- Witaj domyślne zewnętrzny adres URL jest *https://ExpenseApp-contoso.msappproxy.net*, która nie przyjmuje swojego konta toohello użytkowników na stronie.  
- Ustaw *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* jako hello toogive adres URL strony głównej użytkowników nie zakłóca pracy. 

>[!NOTE]
>Przyznać dostęp użytkownikom toopublished aplikacji hello aplikacje są wyświetlane w hello [Panel dostępu usługi Azure AD](active-directory-saas-access-panel-introduction.md) i hello [uruchamiania aplikacji usługi Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Przed rozpoczęciem

Aby ustawić adres URL strony głównej hello, należy hello uwzględnić następujące wymagania:

* Upewnij się, że w tej ścieżce hello jest ścieżką poddomeny adresu URL domeny katalogu głównego hello.

  W przypadku adresu URL domeny głównej hello, na przykład https://apps.contoso.com/app1/, hello strony głównej skonfigurowanego adresu URL musi rozpoczynać się od https://apps.contoso.com/app1/.

* Jeśli wprowadzisz zmiany toohello aplikacja opublikowana, zmiany hello może zresetować wartość hello hello adres URL strony głównej. Podczas aktualizacji aplikacji hello w przyszłości hello, należy ponownie sprawdzić i, w razie potrzeby zaktualizuj hello adres URL strony głównej.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Zmień stronę główną hello w hello portalu Azure

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Przejdź za**usługi Azure Active Directory** > **rejestracji aplikacji** i wybierz aplikację z listy hello. 
3. Wybierz **właściwości** z hello ustawień.
4. Aktualizacja hello **adres URL strony głównej** pole z nowej ścieżki. 

   ![Podaj adres URL nowej strony głównej](./media/application-proxy-office365-app-launcher/homepage.png)

5. Wybierz **Zapisz**

## <a name="change-hello-home-page-with-powershell"></a>Zmień stronę główną hello przy użyciu programu PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Zainstaluj moduł programu PowerShell usługi Azure AD hello

Przed zdefiniowaniem adres URL niestandardowej strony głównej przy użyciu programu PowerShell, należy zainstalować moduł programu PowerShell usługi Azure AD hello. Możesz pobrać pakiet hello z hello [galerii programu PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), która używa hello punkt końcowy interfejsu API programu Graph. 

Witaj tooinstall pakiet, wykonaj następujące kroki:

1. Otwórz okno programu PowerShell standard, a następnie uruchom następujące polecenie hello:

    ```
     Install-Module -Name AzureAD
    ```
    Jeśli używasz polecenia hello jako bez uprawnień administratora, użyj hello `-scope currentuser` opcji.
2. Podczas instalacji hello wybierz **Y** tooinstall dwa pakiety z Nuget.org. Oba pakiety są wymagane. 

### <a name="find-hello-objectid-of-hello-app"></a>Znajdź hello ObjectID aplikacji hello

Uzyskaj hello ObjectID aplikacji hello, a następnie wyszukaj aplikacji hello przez jego strony głównej.

1. Otwórz program PowerShell i zaimportować moduł hello Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Zaloguj się toohello modułu Azure AD jako administrator dzierżawy hello.

    ```
    Connect-AzureAD
    ```
3. Znajdź aplikacji hello na podstawie jego adresu URL strony głównej. Adres URL hello można znaleźć w portalu hello przechodząc zbyt**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**. W tym przykładzie użyto *sharepoint iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Należy uzyskać wynik, który jest podobne toohello, co pokazano poniżej. Skopiuj hello toouse ObjectID identyfikator GUID w następnej sekcji hello.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Adres URL strony głównej hello aktualizacji

W hello tego samego modułu PowerShell, który został użyty w kroku 1, wykonaj hello następujące kroki:

1. Upewnij się, że masz hello Popraw aplikacji i Zastąp *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* z hello ObjectID skopiowany w hello poprzedzających krok.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Po potwierdzeniu aplikacji hello, należy się Strona główna hello tooupdate gotowy, w następujący sposób.

2. Utwórz toohold obiektu pusta aplikacja hello zmiany, które mają toomake. Ta zmienna przechowuje hello wartości, które mają tooupdate. Nic nie jest tworzony w tym kroku.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. Ustaw wartość toohello adres URL strony głównej hello, która ma. wartość Hello musi być ścieżką poddomeny hello opublikowanych aplikacji. Na przykład, jeśli zmienisz hello adres URL strony głównej z *https://sharepoint-iddemo.msappproxy.net/* za*https://sharepoint-iddemo.msappproxy.net/hybrid/*, użytkownicy aplikacji bezpośrednio przejść toohello niestandardowe Strona główna.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Upewnij się, hello aktualizacji przy użyciu hello GUID (identyfikator obiektu), który został skopiowany w "krok 1: znajdowanie hello ObjectID aplikacji hello."

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm, że zmiany hello zakończyło się powodzeniem, ponownie uruchomić aplikacji hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Wszelkie zmiany dokonane w aplikacji toohello może zresetować hello adres URL strony głównej. Jeśli adres URL strony głównej resetuje, powtórz krok 2.

## <a name="next-steps"></a>Następne kroki

- [Włącz tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Włącz serwer Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md)
