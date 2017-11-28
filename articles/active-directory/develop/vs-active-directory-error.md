---
title: "błędy toodiagnose aaaHow hello Kreator połączenia usługi Azure Active Directory"
description: "Kreator połączenia usługi active directory Hello wykryto typ uwierzytelniania niezgodne"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="e5311-103">Diagnozowanie błędów przy użyciu hello Kreator połączenia usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5311-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="e5311-104">Podczas wykrywania poprzedni kod uwierzytelniania, Kreator hello wykrył typ uwierzytelniania niezgodne.</span><span class="sxs-lookup"><span data-stu-id="e5311-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="e5311-105">Co to jest sprawdzany?</span><span class="sxs-lookup"><span data-stu-id="e5311-105">What is being checked?</span></span>
<span data-ttu-id="e5311-106">**Uwaga:** toocorrectly wykryć poprzedni kod uwierzytelniania w projekcie, hello projektu muszą zostać skompilowane.</span><span class="sxs-lookup"><span data-stu-id="e5311-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="e5311-107">Jeśli wystąpił błąd i nie masz poprzedni kod uwierzytelniania w projekcie, skompiluj ponownie i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="e5311-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="e5311-108">Typy projektów</span><span class="sxs-lookup"><span data-stu-id="e5311-108">Project Types</span></span>
<span data-ttu-id="e5311-109">Witaj, Kreator sprawdza, czy hello typ projektu, który projektujesz tak go wstrzyknąć hello logika uwierzytelniania prawo do projektu hello.</span><span class="sxs-lookup"><span data-stu-id="e5311-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="e5311-110">W przypadku dowolnego kontrolera, która jest pochodną `ApiController` w projekcie hello projektu hello jest uznawany za WebAPI projektu.</span><span class="sxs-lookup"><span data-stu-id="e5311-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="e5311-111">Jeśli występują tylko te kontrolery, które pochodzą z `MVC.Controller` w projekcie hello projektu hello jest uznawany za projekt platformy MVC.</span><span class="sxs-lookup"><span data-stu-id="e5311-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="e5311-112">Cokolwiek innego nie jest obsługiwana przez kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="e5311-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="e5311-113">Kod uwierzytelniania zgodne</span><span class="sxs-lookup"><span data-stu-id="e5311-113">Compatible Authentication Code</span></span>
<span data-ttu-id="e5311-114">Kreator Hello również sprawdza, czy ustawienia uwierzytelniania, które zostały wcześniej skonfigurowane przy użyciu Kreatora hello lub są zgodne z hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="e5311-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="e5311-115">Jeśli wszystkie ustawienia są obecne, jest on uznawany za przypadek wielobieżnej otworzy się Kreator hello hello ustawienia i.</span><span class="sxs-lookup"><span data-stu-id="e5311-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="e5311-116">Jeśli tylko niektóre ustawienia hello są obecne, jest uznawane za przypadek błędu.</span><span class="sxs-lookup"><span data-stu-id="e5311-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="e5311-117">W projekcie MVC hello Kreator sprawdza jakichkolwiek hello następujące ustawienia, które w wyniku poprzedniego użycia kreatora hello:</span><span class="sxs-lookup"><span data-stu-id="e5311-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="e5311-118">Ponadto Kreator hello sprawdza dla żadnego z następujących ustawień w projekcie interfejsu API sieci Web, wynikające z poprzedniego użycia kreatora hello hello:</span><span class="sxs-lookup"><span data-stu-id="e5311-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="e5311-119">Kod uwierzytelniania niezgodne</span><span class="sxs-lookup"><span data-stu-id="e5311-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="e5311-120">Ponadto Kreator hello prób toodetect wersji kodu uwierzytelniania, które zostały skonfigurowane z poprzednich wersji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e5311-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="e5311-121">Jeśli wystąpił ten błąd, oznacza to, że projekt zawiera typ uwierzytelniania niezgodne.</span><span class="sxs-lookup"><span data-stu-id="e5311-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="e5311-122">Kreator Hello wykrywa hello następujące typy uwierzytelniania z poprzednich wersji programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e5311-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="e5311-123">Uwierzytelnianie systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e5311-123">Windows Authentication</span></span> 
* <span data-ttu-id="e5311-124">Indywidualne konta użytkowników</span><span class="sxs-lookup"><span data-stu-id="e5311-124">Individual User Accounts</span></span> 
* <span data-ttu-id="e5311-125">Konta organizacyjne</span><span class="sxs-lookup"><span data-stu-id="e5311-125">Organizational Accounts</span></span> 

<span data-ttu-id="e5311-126">toodetect uwierzytelniania systemu Windows w projekcie programu MVC, Kreator hello szuka hello `authentication` element na podstawie Twojej **web.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="e5311-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="e5311-127">toodetect uwierzytelniania systemu Windows w projekcie interfejsu API sieci Web, Kreator hello szuka hello `IISExpressWindowsAuthentication` element z projektu **.csproj** pliku:</span><span class="sxs-lookup"><span data-stu-id="e5311-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="e5311-128">toodetect uwierzytelniania indywidualnych kont użytkowników, Kreator hello wygląda hello elementu pakietu z sieci **Packages.config** pliku.</span><span class="sxs-lookup"><span data-stu-id="e5311-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="e5311-129">toodetect stare formy uwierzytelniania konto organizacyjne, Kreator hello szuka hello następującego elementu z **web.config**:</span><span class="sxs-lookup"><span data-stu-id="e5311-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="e5311-130">Typ uwierzytelniania hello toochange, Usuń typ uwierzytelniania niezgodne hello i uruchom ponownie kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="e5311-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="e5311-131">Aby uzyskać więcej informacji, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="e5311-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="e5311-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5311-132">Next steps</span></span>
- [<span data-ttu-id="e5311-133">Scenariusze uwierzytelniania dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e5311-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)