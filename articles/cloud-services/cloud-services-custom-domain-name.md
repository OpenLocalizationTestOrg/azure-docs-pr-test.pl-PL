---
title: "aaaConfigure niestandardowej nazwy domeny usług w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooexpose aplikacji Azure lub dane na domenę niestandardową, konfigurując ustawienia DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="d11cd-103">Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="d11cd-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d11cd-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d11cd-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="d11cd-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d11cd-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="d11cd-106">Podczas tworzenia usługi w chmurze Azure przypisuje go poddomeną tooa cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d11cd-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="d11cd-107">Na przykład, jeśli usługi w chmurze ma nazwę "contoso", użytkownicy będą się mogli tooaccess aplikacji przy użyciu adresu URL, takie jak http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d11cd-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="d11cd-108">Azure przypisuje wirtualny adres IP.</span><span class="sxs-lookup"><span data-stu-id="d11cd-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="d11cd-109">Można jednak również ujawniać aplikacji na własną nazwę domeny, np. contoso.com. W tym artykule opisano sposób tooreserve lub skonfigurować niestandardową nazwę domeny dla ról sieci web usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d11cd-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="d11cd-110">Czy można już zrozumieć, jakie CNAME i są?</span><span class="sxs-lookup"><span data-stu-id="d11cd-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="d11cd-111">[Skok poza wyjaśnienie hello](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="d11cd-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="d11cd-112">Pobrać, przechodząc szybciej!</span><span class="sxs-lookup"><span data-stu-id="d11cd-112">Get going faster!</span></span> <span data-ttu-id="d11cd-113">Użyj hello Azure [z przewodnikiem wskazówki](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="d11cd-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="d11cd-114">Powoduje skojarzenie niestandardowej nazwy domeny i zabezpieczania komunikacji (SSL) z usług Azure Cloud Services lub witryny sieci Web Azure bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="d11cd-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="d11cd-115">Witaj procedury w tym zadaniu mają zastosowanie tooAzure usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d11cd-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="d11cd-116">Dla usług aplikacji, zobacz [to](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="d11cd-117">W przypadku kont magazynu, zobacz [to](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="d11cd-118">Zrozumienie rekordów CNAME i A</span><span class="sxs-lookup"><span data-stu-id="d11cd-118">Understand CNAME and A records</span></span>
<span data-ttu-id="d11cd-119">CNAME (lub rekordy aliasu) i rekordy zarówno pozwalają tooassociate nazwy domeny z określonego serwera (lub usługi, w tym przypadku) jednak one działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="d11cd-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="d11cd-120">Istnieją również kilka zagadnień, podczas korzystania z usługi w chmurze Azure, które należy wziąć pod uwagę przed podjęciem decyzji, które toouse rekordów.</span><span class="sxs-lookup"><span data-stu-id="d11cd-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="d11cd-121">Rekord CNAME lub Alias</span><span class="sxs-lookup"><span data-stu-id="d11cd-121">CNAME or Alias record</span></span>
<span data-ttu-id="d11cd-122">Rekord CNAME mapuje *określonych* domeny, takie jak **contoso.com** lub **www.contoso.com**, tooa nazwa kanoniczna domeny.</span><span class="sxs-lookup"><span data-stu-id="d11cd-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="d11cd-123">W takim przypadku nazwa kanoniczna domeny hello jest hello **.cloudapp [moja_aplikacja] .net** nazwy domeny platformy Azure hostowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d11cd-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="d11cd-124">Po utworzeniu hello CNAME tworzy alias dla hello **.cloudapp [moja_aplikacja] .net**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="d11cd-125">Hello wpis CNAME rozwiąże adres IP toohello Twojego **.cloudapp [moja_aplikacja] .net** usługi automatycznie, więc jeśli zmieni adres IP hello hello usługi w chmurze, nie masz tootake żadnych działań.</span><span class="sxs-lookup"><span data-stu-id="d11cd-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="d11cd-126">Niektóre domeny rejestratorów tylko pozwalają poddomen toomap przy użyciu rekordu CNAME, np. www.contoso.com i nie nazwy głównych, np. contoso.com. Więcej informacji o rekordy CNAME, można znaleźć w dokumentacji hello przez rejestratora, [hello wpis Wikipedia rekordu CNAME](http://en.wikipedia.org/wiki/CNAME_record), lub hello [nazwy domen IETF - wdrażania i specyfikację](http://tools.ietf.org/html/rfc1035) dokument.</span><span class="sxs-lookup"><span data-stu-id="d11cd-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="d11cd-127">Rekord</span><span class="sxs-lookup"><span data-stu-id="d11cd-127">A record</span></span>
<span data-ttu-id="d11cd-128">Rekord A mapuje domeny, takie jak **contoso.com** lub **www.contoso.com**, *lub domena symboli wieloznacznych* takich jak  **\*. contoso.com**, tooan adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d11cd-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="d11cd-129">W przypadku hello usługi w chmurze platformy Azure hello wirtualnego adresu IP hello usługi.</span><span class="sxs-lookup"><span data-stu-id="d11cd-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="d11cd-130">Dlatego hello Największą zaletą rekord A za pośrednictwem rekordu CNAME jest, że może mieć jeden wpis, który używa symboli wieloznacznych, takich jak \* **. contoso.com**, który będzie obsługiwać żądania wielu domen podrzędnych takich jak  **mail.contoso.com**, **login.contoso.com**, lub **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="d11cd-131">Ponieważ rekord jest mapowany tooa statyczny adres IP, nie może automatycznie rozwiązać zmian adresu IP toohello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d11cd-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="d11cd-132">Witaj adres IP używany przez usługi w chmurze jest przydzielony hello po raz pierwszy wdrażanie tooan pustego gniazda (produkcyjnego lub przemieszczania.) Po usunięciu wdrożenia hello gniazda hello hello adres IP został wydany przez Azure i dowolnego miejsca toohello przyszłych wdrożeniach. należy podać nowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="d11cd-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="d11cd-133">Wygodnie hello adres IP miejsca danego wdrożenia (środowisko produkcyjne lub tymczasowe) jest trwały podczas wymiany między przemieszczania i wdrożeń produkcyjnych lub uaktualnianie w miejscu istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d11cd-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="d11cd-134">Aby uzyskać więcej informacji dotyczących wykonywania tych akcji, zobacz [jak usługi w chmurze toomanage](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="d11cd-135">Dodaj rekord CNAME dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="d11cd-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="d11cd-136">toocreate rekord CNAME, należy dodać nowy wpis w tabeli DNS powitania dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="d11cd-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="d11cd-137">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord CNAME, ale hello są pojęcia hello takie same.</span><span class="sxs-lookup"><span data-stu-id="d11cd-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="d11cd-138">Użyj jednej z tych metod hello toofind **. cloudapp.net** przypisaną usługi w chmurze tooyour nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="d11cd-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="d11cd-139">Toohello logowania [klasycznego portalu Azure], wybierz usługi w chmurze, wybierz **pulpitu nawigacyjnego**, a następnie znajdź hello **adres URL witryny** wpisu w hello **szybkiego dostępu**  sekcji.</span><span class="sxs-lookup"><span data-stu-id="d11cd-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![adres URL witryny hello przedstawiający sekcji szybkiego dostępu][csurl]
     
       <span data-ttu-id="d11cd-141">**LUB**</span><span class="sxs-lookup"><span data-stu-id="d11cd-141">**OR**</span></span>  
   * <span data-ttu-id="d11cd-142">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d11cd-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="d11cd-143">Zapisz nazwę domeny hello używane w hello adres URL zwracany przez metodę albo, jak będą one potrzebne podczas tworzenia rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="d11cd-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="d11cd-144">Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="d11cd-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="d11cd-145">Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="d11cd-146">Teraz można znaleźć, gdzie wybierz lub wprowadź CNAME w.</span><span class="sxs-lookup"><span data-stu-id="d11cd-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="d11cd-147">Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="d11cd-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="d11cd-148">Należy szukać słowa hello **CNAME**, **Alias**, lub **poddomen**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="d11cd-149">Należy również podać hello domeny lub poddomeny aliasu dla hello CNAME, takich jak **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Jeśli chcesz toocreate aliasu dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="d11cd-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="d11cd-150">Następnie należy podać nazwę kanoniczną hosta, która jest aplikacji **cloudapp.net** domeny w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="d11cd-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="d11cd-151">Na przykład po rekord CNAME hello przekazuje cały ruch z **www.contoso.com** za**contoso.cloudapp.net**, hello niestandardowej nazwy domeny wdrożonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="d11cd-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="d11cd-152">Nazwa aliasu/hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="d11cd-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="d11cd-153">Canonical domeny</span><span class="sxs-lookup"><span data-stu-id="d11cd-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="d11cd-154">www</span><span class="sxs-lookup"><span data-stu-id="d11cd-154">www</span></span> |<span data-ttu-id="d11cd-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="d11cd-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="d11cd-156">Obiekt odwiedzający **www.contoso.com** nigdy nie zobaczą hello true hosta (contoso.cloudapp.net), więc hello proces przesyłania jest niewidoczne toothe użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="d11cd-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="d11cd-157">Witaj w powyższym przykładzie dotyczy tylko tootraffic na powitania **www** poddomeny.</span><span class="sxs-lookup"><span data-stu-id="d11cd-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="d11cd-158">Ponieważ rekordy CNAME nie można używać symboli wieloznacznych, należy utworzyć jeden CNAME dla każdej domeny/poddomeny.</span><span class="sxs-lookup"><span data-stu-id="d11cd-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="d11cd-159">Jeśli chcesz, ruch toodirect z poddomenami, takich jak \*. contoso.com, adres cloudapp.net tooyour, można skonfigurować **adres URL przekierowania** lub **adres URL do przodu** wpis w ustawieniach DNS lub Utwórz rekord A.</span><span class="sxs-lookup"><span data-stu-id="d11cd-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="d11cd-160">Dodawanie rekordu A dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="d11cd-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="d11cd-161">rekord A toocreate, musi najpierw odnaleźć hello wirtualnego adresu IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d11cd-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="d11cd-162">Następnie dodaj nowy wpis hello tabeli DNS dla domeny niestandardowej przy użyciu narzędzi hello dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="d11cd-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="d11cd-163">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord A, ale hello są pojęcia hello takie same.</span><span class="sxs-lookup"><span data-stu-id="d11cd-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="d11cd-164">Użyj jednej z hello następujące metody tooget hello adres IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d11cd-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="d11cd-165">toohello logowania [klasycznego portalu Azure], wybierz usługi w chmurze, wybierz **pulpitu nawigacyjnego**, a następnie znajdź hello **adres publiczny wirtualnego adresu IP (VIP)** wpisu w hello **szybkiego dostępu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d11cd-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![Wyświetlanie hello VIP sekcji szybkiego dostępu][vip]
     
       <span data-ttu-id="d11cd-167">**LUB**</span><span class="sxs-lookup"><span data-stu-id="d11cd-167">**OR**</span></span>  
   * <span data-ttu-id="d11cd-168">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d11cd-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="d11cd-169">Jeśli masz wiele punktów końcowych skojarzonych z usługi w chmurze, otrzymasz wiele wierszy zawierających hello adresu IP, ale wszystkie powinien być wyświetlany hello sam adres.</span><span class="sxs-lookup"><span data-stu-id="d11cd-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="d11cd-170">Zapisz hello adresu IP, ponieważ będzie potrzebny podczas tworzenia rekordu A.</span><span class="sxs-lookup"><span data-stu-id="d11cd-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="d11cd-171">Zaloguj się na tooyour DNS rejestratora witryny sieci Web i przejdź do strony toohello zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="d11cd-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="d11cd-172">Znajdź łącza lub obszarów witryny hello oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="d11cd-173">Teraz można znaleźć, gdzie wybierz lub wprowadź rekordu.</span><span class="sxs-lookup"><span data-stu-id="d11cd-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="d11cd-174">Może być tooselect hello rekord typu z listy rozwijanej lub przejdź tooan Zaawansowane ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="d11cd-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="d11cd-175">Wybierz lub wprowadź domenę hello lub poddomeny, który będzie używany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="d11cd-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="d11cd-176">Na przykład wybierz **www** Jeśli chcesz toocreate aliasu dla **www.customdomain.com**. Toocreate wpis symboli wieloznacznych dla wszystkich domen podrzędnych, należy wprowadzić "__*__".</span><span class="sxs-lookup"><span data-stu-id="d11cd-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="d11cd-177">Wszystkich domen podrzędnych będzie on zawierał takie jak **mail.customdomain.com**, **login.customdomain.com**, i **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="d11cd-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="d11cd-178">Jeśli rekord A toocreate dla domeny głównej hello, może być wymieniona jako hello "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="d11cd-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="d11cd-179">Wprowadź adres IP hello usługi w chmurze w hello podane pole.</span><span class="sxs-lookup"><span data-stu-id="d11cd-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="d11cd-180">Skojarzenie wpis domeny hello hello rekordu A o adresie IP hello wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="d11cd-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="d11cd-181">Na przykład po rekord hello przekazuje cały ruch z **contoso.com** za**137.135.70.239**, adres IP wdrożonej aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="d11cd-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="d11cd-182">Nazwa hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="d11cd-182">Host name/Subdomain</span></span> | <span data-ttu-id="d11cd-183">Adres IP</span><span class="sxs-lookup"><span data-stu-id="d11cd-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="d11cd-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="d11cd-184">137.135.70.239</span></span> |

<span data-ttu-id="d11cd-185">W tym przykładzie przedstawiono tworzenie rekordu A dla domeny głównej hello.</span><span class="sxs-lookup"><span data-stu-id="d11cd-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="d11cd-186">W razie potrzeby toocreate toocover wpis symbolu wieloznacznego wszystkich domen podrzędnych, należy wprowadzić "__*__" jako hello poddomeny.</span><span class="sxs-lookup"><span data-stu-id="d11cd-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="d11cd-187">Adresy IP na platformie Azure są dynamiczne domyślnie.</span><span class="sxs-lookup"><span data-stu-id="d11cd-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="d11cd-188">Prawdopodobnie zechcesz toouse [zastrzeżony adres IP](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure, który nie ulega zmianie adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d11cd-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d11cd-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d11cd-189">Next steps</span></span>
* [<span data-ttu-id="d11cd-190">W jaki sposób tooManage usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="d11cd-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="d11cd-191">Jak tooa CDN zawartości tooMap domeny niestandardowe</span><span class="sxs-lookup"><span data-stu-id="d11cd-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="d11cd-192">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="d11cd-193">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="d11cd-194">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="d11cd-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[klasycznego portalu Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
