---
title: "Przykłady raportu interfejsu API działania aaaAzure logowania usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooget pracę z hello Azure Active Directory interfejsu API raportowania"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Przykłady interfejsu API raport aktywności logowania w usłudze Azure Active Directory
Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.  
Raportowania usługi Azure AD zapewnia interfejs API, który umożliwia tooaccess działań logowania dane za pomocą kodu lub narzędzia pokrewne.  
Witaj zakres tego tematu jest tooprovide o przykładowy kod hello **logowania działanie interfejsu API**.

Zobacz:

* [Dzienniki inspekcji](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach
* [Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.


## <a name="prerequisites"></a>Wymagania wstępne
Zanim użyjesz hello przykłady w tym temacie, należy toocomplete hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>Skrypt programu PowerShell
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a>Wykonywanie skryptu hello
Po Zakończ edycję skryptu hello, uruchom go i sprawdź, czy tego hello oczekiwanych dane z hello raportu dzienniki inspekcji są zwracane.

Witaj skrypt zwraca dane wyjściowe z hello logowania raportu w formacie JSON. Tworzy również `SigninActivities.json` pliku z hello same dane wyjściowe. Możesz eksperymentować, modyfikując hello skryptu tooreturn danych z innych raportów ujmij w komentarz hello formatów wyjściowych, które nie muszą.

## <a name="next-steps"></a>Następne kroki
* Czy chcesz, aby toocustomize hello przykłady w tym temacie? Zapoznaj się z hello [działania usługi Azure Active Directory logowania dokumentacja interfejsu API](active-directory-reporting-api-sign-in-activity-reference.md). 
* Jeśli chcesz toosee pełny przegląd przy użyciu hello interfejsem API raportowania usługi Azure Active Directory, zobacz [wprowadzenie hello interfejsem API raportowania usługi Azure Active Directory](active-directory-reporting-api-getting-started.md).
* Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).  

