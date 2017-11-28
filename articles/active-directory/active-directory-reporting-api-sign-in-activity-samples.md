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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="6b687-103">Przykłady interfejsu API raport aktywności logowania w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b687-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="6b687-104">Ten temat jest częścią zbiór tematów dotyczących usługi Azure Active Directory hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b687-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="6b687-105">Raportowania usługi Azure AD zapewnia interfejs API, który umożliwia tooaccess działań logowania dane za pomocą kodu lub narzędzia pokrewne.</span><span class="sxs-lookup"><span data-stu-id="6b687-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="6b687-106">Witaj zakres tego tematu jest tooprovide o przykładowy kod hello **logowania działanie interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="6b687-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="6b687-107">Zobacz:</span><span class="sxs-lookup"><span data-stu-id="6b687-107">See:</span></span>

* <span data-ttu-id="6b687-108">[Dzienniki inspekcji](active-directory-reporting-azure-portal.md#activity-reports) Aby uzyskać więcej informacji o pojęciach</span><span class="sxs-lookup"><span data-stu-id="6b687-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="6b687-109">[Wprowadzenie do korzystania z usługi Azure Active Directory interfejsu API raportowania hello](active-directory-reporting-api-getting-started.md) uzyskać więcej informacji o hello raportowania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6b687-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="6b687-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b687-110">Prerequisites</span></span>
<span data-ttu-id="6b687-111">Zanim użyjesz hello przykłady w tym temacie, należy toocomplete hello [interfejsu API raportowania hello Azure AD tooaccess wymagania wstępne](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6b687-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="6b687-112">Skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b687-112">PowerShell script</span></span>
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




## <a name="executing-hello-script"></a><span data-ttu-id="6b687-113">Wykonywanie skryptu hello</span><span class="sxs-lookup"><span data-stu-id="6b687-113">Executing hello script</span></span>
<span data-ttu-id="6b687-114">Po Zakończ edycję skryptu hello, uruchom go i sprawdź, czy tego hello oczekiwanych dane z hello raportu dzienniki inspekcji są zwracane.</span><span class="sxs-lookup"><span data-stu-id="6b687-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="6b687-115">Witaj skrypt zwraca dane wyjściowe z hello logowania raportu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="6b687-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="6b687-116">Tworzy również `SigninActivities.json` pliku z hello same dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="6b687-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="6b687-117">Możesz eksperymentować, modyfikując hello skryptu tooreturn danych z innych raportów ujmij w komentarz hello formatów wyjściowych, które nie muszą.</span><span class="sxs-lookup"><span data-stu-id="6b687-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b687-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b687-118">Next Steps</span></span>
* <span data-ttu-id="6b687-119">Czy chcesz, aby toocustomize hello przykłady w tym temacie?</span><span class="sxs-lookup"><span data-stu-id="6b687-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="6b687-120">Zapoznaj się z hello [działania usługi Azure Active Directory logowania dokumentacja interfejsu API](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6b687-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="6b687-121">Jeśli chcesz toosee pełny przegląd przy użyciu hello interfejsem API raportowania usługi Azure Active Directory, zobacz [wprowadzenie hello interfejsem API raportowania usługi Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6b687-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="6b687-122">Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6b687-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

