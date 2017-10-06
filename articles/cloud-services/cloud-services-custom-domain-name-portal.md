---
title: "aaaConfigure niestandardowej nazwy domeny usług w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooexpose Twojego Azure toohello aplikacji lub danych internet na domenę niestandardową, konfigurując ustawienia DNS.  Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="7b0ba-104">Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="7b0ba-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b0ba-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b0ba-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="7b0ba-106">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7b0ba-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="7b0ba-107">Podczas tworzenia usługi w chmurze Azure przypisuje go poddomeną tooa **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-107">When you create a Cloud Service, Azure assigns it tooa subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="7b0ba-108">Na przykład, jeśli usługi w chmurze ma nazwę "contoso", użytkownicy będą się mogli tooaccess aplikacji przy użyciu adresu URL, takie jak http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-108">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="7b0ba-109">Azure przypisuje wirtualny adres IP.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="7b0ba-110">Jednak pozwala również udostępnić aplikacji na własną nazwę domeny, takie jak **contoso.com**. W tym artykule opisano sposób tooreserve lub skonfigurować niestandardową nazwę domeny dla ról sieci web usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="7b0ba-111">Czy można już zrozumieć, jakie CNAME i są?</span><span class="sxs-lookup"><span data-stu-id="7b0ba-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="7b0ba-112">[Skok poza wyjaśnienie hello](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-112">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="7b0ba-113">Witaj procedury w tym zadaniu mają zastosowanie tooAzure usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-113">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="7b0ba-114">Dla usług aplikacji, zobacz [to](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="7b0ba-115">W przypadku kont magazynu, zobacz [to](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="7b0ba-116">Pracuj szybciej--Użyj hello Azure nowe [z przewodnikiem wskazówki](http://support.microsoft.com/kb/2990804)!</span><span class="sxs-lookup"><span data-stu-id="7b0ba-116">Get going faster--use hello NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="7b0ba-117">Powoduje skojarzenie niestandardowej nazwy domeny i zabezpieczania komunikacji (SSL) z usług Azure Cloud Services lub witryny sieci Web Azure bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="7b0ba-118">Zrozumienie rekordów CNAME i A</span><span class="sxs-lookup"><span data-stu-id="7b0ba-118">Understand CNAME and A records</span></span>
<span data-ttu-id="7b0ba-119">CNAME (lub rekordy aliasu) i rekordy zarówno pozwalają tooassociate nazwy domeny z określonego serwera (lub usługi, w tym przypadku) jednak one działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="7b0ba-120">Istnieją również kilka zagadnień, podczas korzystania z usługi w chmurze Azure, które należy wziąć pod uwagę przed podjęciem decyzji, które toouse rekordów.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="7b0ba-121">Rekord CNAME lub Alias</span><span class="sxs-lookup"><span data-stu-id="7b0ba-121">CNAME or Alias record</span></span>
<span data-ttu-id="7b0ba-122">Rekord CNAME mapuje *określonych* domeny, takie jak **contoso.com** lub **www.contoso.com**, tooa nazwa kanoniczna domeny.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="7b0ba-123">W takim przypadku nazwa kanoniczna domeny hello jest hello **.cloudapp [moja_aplikacja] .net** nazwy domeny platformy Azure hostowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="7b0ba-124">Po utworzeniu hello CNAME tworzy alias dla hello **.cloudapp [moja_aplikacja] .net**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="7b0ba-125">Hello wpis CNAME rozwiąże adres IP toohello Twojego **.cloudapp [moja_aplikacja] .net** usługi automatycznie, więc jeśli zmieni adres IP hello hello usługi w chmurze, nie masz tootake żadnych działań.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="7b0ba-126">Niektóre domeny rejestratorów tylko pozwalają poddomen toomap przy użyciu rekordu CNAME, np. www.contoso.com i nie nazwy głównych, np. contoso.com. Więcej informacji o rekordy CNAME, można znaleźć w dokumentacji hello przez rejestratora, [hello wpis Wikipedia rekordu CNAME](http://en.wikipedia.org/wiki/CNAME_record), lub hello [nazwy domen IETF - wdrażania i specyfikację](http://tools.ietf.org/html/rfc1035) dokument.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="7b0ba-127">Rekord</span><span class="sxs-lookup"><span data-stu-id="7b0ba-127">A record</span></span>
<span data-ttu-id="7b0ba-128">*A* rekord mapuje domeny, takie jak **contoso.com** lub **www.contoso.com**, *lub domena symboli wieloznacznych* takich jak  **\*. contoso.com**, tooan adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="7b0ba-129">W przypadku hello usługi w chmurze platformy Azure hello wirtualnego adresu IP hello usługi.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="7b0ba-130">Dlatego hello Największą zaletą rekord A za pośrednictwem rekordu CNAME jest, że może mieć jeden wpis, który używa symboli wieloznacznych, takich jak \* **. contoso.com**, który będzie obsługiwać żądania wielu domen podrzędnych takich jak  **mail.contoso.com**, **login.contoso.com**, lub **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="7b0ba-131">Ponieważ rekord jest mapowany tooa statyczny adres IP, nie może automatycznie rozwiązać zmian adresu IP toohello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="7b0ba-132">Witaj adres IP używany przez usługi w chmurze jest przydzielony hello po raz pierwszy wdrażanie tooan pustego gniazda (produkcyjnego lub przemieszczania.) Po usunięciu wdrożenia hello gniazda hello hello adres IP został wydany przez Azure i dowolnego miejsca toohello przyszłych wdrożeniach. należy podać nowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="7b0ba-133">Wygodnie hello adres IP miejsca danego wdrożenia (środowisko produkcyjne lub tymczasowe) jest trwały podczas wymiany między przemieszczania i wdrożeń produkcyjnych lub uaktualnianie w miejscu istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="7b0ba-134">Aby uzyskać więcej informacji dotyczących wykonywania tych akcji, zobacz [jak usługi w chmurze toomanage](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="7b0ba-135">Dodaj rekord CNAME dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="7b0ba-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="7b0ba-136">toocreate rekord CNAME, należy dodać nowy wpis w tabeli DNS powitania dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="7b0ba-137">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord CNAME, ale hello są pojęcia hello takie same.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="7b0ba-138">Użyj jednej z tych metod hello toofind **. cloudapp.net** przypisaną usługi w chmurze tooyour nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="7b0ba-139">Toohello logowania [portalu Azure], wybierz usługi w chmurze, obejrzyj hello **Essentials** sekcji, a następnie znajdź hello **adres URL witryny** wpisu.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-139">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Site URL** entry.</span></span>
     
       ![adres URL witryny hello przedstawiający sekcji szybkiego dostępu][csurl]
     
       <span data-ttu-id="7b0ba-141">**LUB**</span><span class="sxs-lookup"><span data-stu-id="7b0ba-141">**OR**</span></span>
   * <span data-ttu-id="7b0ba-142">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7b0ba-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="7b0ba-143">Zapisz nazwę domeny hello używane w hello adres URL zwracany przez metodę albo, jak będą one potrzebne podczas tworzenia rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="7b0ba-144">Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="7b0ba-145">Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="7b0ba-146">Teraz można znaleźć, gdzie wybierz lub wprowadź CNAME w.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="7b0ba-147">Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="7b0ba-148">Należy szukać słowa hello **CNAME**, **Alias**, lub **poddomen**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="7b0ba-149">Należy również podać hello domeny lub poddomeny aliasu dla hello CNAME, takich jak **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Jeśli chcesz toocreate aliasu dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="7b0ba-150">Następnie należy podać nazwę kanoniczną hosta, która jest aplikacji **cloudapp.net** domeny w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="7b0ba-151">Na przykład po rekord CNAME hello przekazuje cały ruch z **www.contoso.com** za**contoso.cloudapp.net**, hello niestandardowej nazwy domeny wdrożonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7b0ba-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="7b0ba-152">Nazwa aliasu/hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="7b0ba-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="7b0ba-153">Canonical domeny</span><span class="sxs-lookup"><span data-stu-id="7b0ba-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="7b0ba-154">www</span><span class="sxs-lookup"><span data-stu-id="7b0ba-154">www</span></span> |<span data-ttu-id="7b0ba-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="7b0ba-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="7b0ba-156">Obiekt odwiedzający **www.contoso.com** nigdy nie zobaczą hello true hosta (contoso.cloudapp.net), więc hello proces przesyłania jest niewidoczne toothe użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>
> 
> <span data-ttu-id="7b0ba-157">Witaj w powyższym przykładzie dotyczy tylko tootraffic na powitania **www** poddomeny.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="7b0ba-158">Ponieważ rekordy CNAME nie można używać symboli wieloznacznych, należy utworzyć jeden CNAME dla każdej domeny/poddomeny.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="7b0ba-159">Jeśli chcesz, ruch toodirect z poddomenami, takich jak *. contoso.com, adres cloudapp.net tooyour, można skonfigurować **adres URL przekierowania** lub **adres URL do przodu** wpis w ustawieniach DNS lub Utwórz rekord a..</span><span class="sxs-lookup"><span data-stu-id="7b0ba-159">If you want toodirect  traffic from subdomains, such as *.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="7b0ba-160">Dodawanie rekordu A dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="7b0ba-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="7b0ba-161">rekord A toocreate, musi najpierw odnaleźć hello wirtualnego adresu IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="7b0ba-162">Następnie dodaj nowy wpis hello tabeli DNS dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="7b0ba-163">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord A, ale hello są pojęcia hello takie same.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="7b0ba-164">Użyj jednej z hello następujące metody tooget hello adres IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="7b0ba-165">Toohello logowania [portalu Azure], wybierz usługi w chmurze, obejrzyj hello **Essentials** sekcji, a następnie znajdź hello **publicznego adresu IP, adresy** wpisu.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-165">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Public IP addresses** entry.</span></span>
     
       ![Wyświetlanie hello VIP sekcji szybkiego dostępu][vip]
     
       <span data-ttu-id="7b0ba-167">**LUB**</span><span class="sxs-lookup"><span data-stu-id="7b0ba-167">**OR**</span></span>
   * <span data-ttu-id="7b0ba-168">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7b0ba-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="7b0ba-169">Zapisz hello adresu IP, ponieważ będzie potrzebny podczas tworzenia rekordu A.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-169">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="7b0ba-170">Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-170">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="7b0ba-171">Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-171">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="7b0ba-172">Teraz można znaleźć, gdzie wybierz lub wprowadź rekordu.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="7b0ba-173">Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-173">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="7b0ba-174">Wybierz lub wprowadź domenę hello lub poddomeny, który będzie używany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-174">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="7b0ba-175">Na przykład wybierz **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Toocreate wpis symboli wieloznacznych dla wszystkich domen podrzędnych, należy wprowadzić "***".</span><span class="sxs-lookup"><span data-stu-id="7b0ba-175">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="7b0ba-176">Wszystkich domen podrzędnych będzie on zawierał takie jak **mail.customdomain.com**, **login.customdomain.com**, i **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="7b0ba-177">Jeśli rekord A toocreate dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-177">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="7b0ba-178">Wprowadź adres IP hello usługi w chmurze w hello podane pole.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-178">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="7b0ba-179">Skojarzenie wpis domeny hello hello rekordu A o adresie IP hello wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-179">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="7b0ba-180">Na przykład po rekord hello przekazuje cały ruch z **contoso.com** za**137.135.70.239**, adres IP wdrożonej aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="7b0ba-180">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="7b0ba-181">Nazwa hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="7b0ba-181">Host name/Subdomain</span></span> | <span data-ttu-id="7b0ba-182">Adres IP</span><span class="sxs-lookup"><span data-stu-id="7b0ba-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="7b0ba-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="7b0ba-183">137.135.70.239</span></span> |

<span data-ttu-id="7b0ba-184">W tym przykładzie przedstawiono tworzenie rekordu A dla domeny głównej hello.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-184">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="7b0ba-185">W razie potrzeby toocreate toocover wpis symbolu wieloznacznego wszystkich domen podrzędnych, należy wprowadzić "***" jako hello poddomeny.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-185">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '*****' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="7b0ba-186">Adresy IP na platformie Azure są dynamiczne domyślnie.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="7b0ba-187">Prawdopodobnie zechcesz toouse [zastrzeżony adres IP](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, który nie ulega zmianie adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7b0ba-187">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7b0ba-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b0ba-188">Next steps</span></span>
* [<span data-ttu-id="7b0ba-189">W jaki sposób tooManage usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="7b0ba-189">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="7b0ba-190">Jak tooa CDN zawartości tooMap domeny niestandardowe</span><span class="sxs-lookup"><span data-stu-id="7b0ba-190">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="7b0ba-191">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="7b0ba-192">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-192">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="7b0ba-193">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7b0ba-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portalu Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
