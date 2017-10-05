---
title: "Konfigurowanie niestandardowej nazwy domeny usług w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak udostępnić aplikacji Azure lub dane na domenę niestandardową Konfigurowanie ustawień DNS."
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
ms.openlocfilehash: 9f872fd5119042945356225a80331da18f3a6d99
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="5b9af-103">Konfigurowanie niestandardowej nazwy domeny dla usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="5b9af-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b9af-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b9af-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="5b9af-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b9af-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="5b9af-106">Podczas tworzenia usługi w chmurze Azure przypisuje go do poddomeny cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5b9af-106">When you create a Cloud Service, Azure assigns it to a subdomain of cloudapp.net.</span></span> <span data-ttu-id="5b9af-107">Na przykład jeśli usługi w chmurze ma nazwę "contoso", użytkownikom będzie można uzyskać dostępu do aplikacji przy użyciu adresu URL, takie jak http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5b9af-107">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="5b9af-108">Azure przypisuje wirtualny adres IP.</span><span class="sxs-lookup"><span data-stu-id="5b9af-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="5b9af-109">Można jednak również ujawniać aplikacji na własną nazwę domeny, np. contoso.com. W tym artykule wyjaśniono, jak zarezerwować lub skonfigurowania niestandardowej nazwy domeny dla ról sieci web usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5b9af-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="5b9af-110">Czy można już zrozumieć, jakie CNAME i są?</span><span class="sxs-lookup"><span data-stu-id="5b9af-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="5b9af-111">[Skok poza wyjaśnienie](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="5b9af-111">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="5b9af-112">Pobrać, przechodząc szybciej!</span><span class="sxs-lookup"><span data-stu-id="5b9af-112">Get going faster!</span></span> <span data-ttu-id="5b9af-113">Użyj platformy Azure [z przewodnikiem wskazówki](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="5b9af-113">Use the Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="5b9af-114">Powoduje skojarzenie niestandardowej nazwy domeny i zabezpieczania komunikacji (SSL) z usług Azure Cloud Services lub witryny sieci Web Azure bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="5b9af-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="5b9af-115">Procedury w tym zadaniu mają zastosowanie do usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="5b9af-115">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="5b9af-116">Dla usług aplikacji, zobacz [to](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="5b9af-117">W przypadku kont magazynu, zobacz [to](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="5b9af-118">Zrozumienie rekordów CNAME i A</span><span class="sxs-lookup"><span data-stu-id="5b9af-118">Understand CNAME and A records</span></span>
<span data-ttu-id="5b9af-119">CNAME (lub rekordy aliasu) i rejestruje zarówno pozwalają na nazwę domeny można skojarzyć z określonym serwerem (lub usługi, w tym przypadku) jednak one działać inaczej.</span><span class="sxs-lookup"><span data-stu-id="5b9af-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="5b9af-120">Istnieją także niektóre zagadnień, używając rekordy z usługami w chmurze Azure, które należy wziąć pod uwagę przed podjęciem decyzji, który ma zostać użyty.</span><span class="sxs-lookup"><span data-stu-id="5b9af-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="5b9af-121">Rekord CNAME lub Alias</span><span class="sxs-lookup"><span data-stu-id="5b9af-121">CNAME or Alias record</span></span>
<span data-ttu-id="5b9af-122">Rekord CNAME mapuje *określonych* domeny, takie jak **contoso.com** lub **www.contoso.com**, nazwę kanoniczną domeny.</span><span class="sxs-lookup"><span data-stu-id="5b9af-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="5b9af-123">W takim przypadku nazwa kanoniczna domeny jest **.cloudapp [moja_aplikacja] .net** nazwy domeny platformy Azure hostowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b9af-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="5b9af-124">Po utworzeniu nazwy CNAME tworzy alias dla **.cloudapp [moja_aplikacja] .net**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="5b9af-125">Wpis CNAME rozwiąże adres IP Twojego **.cloudapp [moja_aplikacja] .net** usługi automatycznie, więc jeśli zmieni adres IP usługi w chmurze, nie trzeba podejmować żadnych działań.</span><span class="sxs-lookup"><span data-stu-id="5b9af-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="5b9af-126">Niektóre rejestratorów domeny umożliwiają tylko mapy poddomen przy użyciu rekordu CNAME, np. www.contoso.com i nie nazwy głównych, np. contoso.com. Aby uzyskać więcej informacji na rekordy CNAME, zobacz w dokumentacji dostarczonej przez rejestratora, [wpis Wikipedia rekordu CNAME](http://en.wikipedia.org/wiki/CNAME_record), lub [nazwy domen IETF - wdrażania i specyfikację](http://tools.ietf.org/html/rfc1035) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5b9af-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="5b9af-127">Rekord</span><span class="sxs-lookup"><span data-stu-id="5b9af-127">A record</span></span>
<span data-ttu-id="5b9af-128">Rekord A mapuje domeny, takie jak **contoso.com** lub **www.contoso.com**, *lub domena symboli wieloznacznych* takich jak  **\*. contoso.com**, adres IP.</span><span class="sxs-lookup"><span data-stu-id="5b9af-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="5b9af-129">W przypadku usługi w chmurze Azure, wirtualnego adresu IP usługi.</span><span class="sxs-lookup"><span data-stu-id="5b9af-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="5b9af-130">Dlatego Największą zaletą rekord A za pośrednictwem rekordu CNAME mają jeden wpis, który używa symboli wieloznacznych, takich jak \* **. contoso.com**, który będzie obsługiwać żądania wielu domen podrzędnych takich jak  **mail.contoso.com**, **login.contoso.com**, lub **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="5b9af-131">Ponieważ rekord jest zamapowana na statycznego adresu IP, nie może automatycznie rozwiązać zmian adres IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5b9af-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="5b9af-132">Adres IP używany przez usługi w chmurze jest przydzielony przy pierwszym uruchomieniu wdrożenia do pustego gniazda (produkcyjnego lub przemieszczania.) Po usunięciu wdrożenia gniazda adres IP został wydany przez Azure i wszystkich przyszłych wdrożeń do gniazda, należy podać nowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="5b9af-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="5b9af-133">Wygodnie adres IP miejsca danego wdrożenia (środowisko produkcyjne lub tymczasowe) jest trwały podczas wymiany między przemieszczania i wdrożeń produkcyjnych lub uaktualnianie w miejscu istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5b9af-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="5b9af-134">Aby uzyskać więcej informacji dotyczących wykonywania tych akcji, zobacz [sposobu zarządzania usługami w chmurze](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="5b9af-135">Dodaj rekord CNAME dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="5b9af-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="5b9af-136">Aby utworzyć rekord CNAME, możesz należy dodać nowy wpis w tabeli DNS dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="5b9af-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="5b9af-137">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord CNAME, ale pojęcia są takie same.</span><span class="sxs-lookup"><span data-stu-id="5b9af-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="5b9af-138">Użyj jednej z tych metod, aby znaleźć **. cloudapp.net** nazwy domeny przypisany do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5b9af-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="5b9af-139">Zaloguj się do [klasycznego portalu Azure], wybierz usługi w chmurze, wybierz **pulpitu nawigacyjnego**, a następnie znajdź **adres URL witryny** wpis w **szybkiego dostępu**sekcji.</span><span class="sxs-lookup"><span data-stu-id="5b9af-139">Login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
     
       ![sekcja szybkiego dostępu przedstawiający adres URL witryny][csurl]
     
       <span data-ttu-id="5b9af-141">**LUB**</span><span class="sxs-lookup"><span data-stu-id="5b9af-141">**OR**</span></span>  
   * <span data-ttu-id="5b9af-142">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5b9af-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="5b9af-143">Zapisz nazwę domeny używaną w adresie URL zwrócone przez każdej z metod, ponieważ będzie potrzebny podczas tworzenia rekordu CNAME.</span><span class="sxs-lookup"><span data-stu-id="5b9af-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="5b9af-144">Zaloguj się w witrynie rejestratora DNS i przejdź do strony zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="5b9af-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="5b9af-145">Wyszukaj łącza lub obszarów witryny oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="5b9af-146">Teraz można znaleźć, gdzie wybierz lub wprowadź CNAME w.</span><span class="sxs-lookup"><span data-stu-id="5b9af-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="5b9af-147">Może być konieczne wybierz typ rekordu z listy rozwijanej lub przejdź do strony Ustawienia zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="5b9af-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="5b9af-148">Należy zwrócić uwagę słowa **CNAME**, **Alias**, lub **poddomen**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="5b9af-149">Należy również podać domeny lub poddomeny aliasu CNAME, takich jak **www** Jeśli chcesz utworzyć alias **www.customdomain.com**. Jeśli chcesz utworzyć alias dla domeny głównej, może być wymieniona jako "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="5b9af-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="5b9af-150">Następnie należy podać nazwę kanoniczną hosta, która jest aplikacji **cloudapp.net** domeny w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="5b9af-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="5b9af-151">Na przykład następujący rekord CNAME przekazuje cały ruch z **www.contoso.com** do **contoso.cloudapp.net**, nazwę domeny niestandardowej wdrożonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5b9af-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="5b9af-152">Nazwa aliasu/hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="5b9af-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="5b9af-153">Canonical domeny</span><span class="sxs-lookup"><span data-stu-id="5b9af-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="5b9af-154">www</span><span class="sxs-lookup"><span data-stu-id="5b9af-154">www</span></span> |<span data-ttu-id="5b9af-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="5b9af-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="5b9af-156">Obiekt odwiedzający **www.contoso.com** nie będzie widoczna wartość true, hosta (contoso.cloudapp.net), więc procesu przekazywania jest niewidoczny dla użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="5b9af-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="5b9af-157">W powyższym przykładzie dotyczy tylko ruchu na **www** poddomeny.</span><span class="sxs-lookup"><span data-stu-id="5b9af-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="5b9af-158">Ponieważ rekordy CNAME nie można używać symboli wieloznacznych, należy utworzyć jeden CNAME dla każdej domeny/poddomeny.</span><span class="sxs-lookup"><span data-stu-id="5b9af-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="5b9af-159">Aby skierować ruch z domen podrzędnych, takich jak \*. contoso.com, adres cloudapp.net możesz skonfigurować **adres URL przekierowania** lub **adres URL do przodu** wpis w ustawieniach DNS lub Utwórz rekord A.</span><span class="sxs-lookup"><span data-stu-id="5b9af-159">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="5b9af-160">Dodawanie rekordu A dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="5b9af-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="5b9af-161">Aby utworzyć rekord A, możesz znaleźć wirtualnego adresu IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5b9af-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="5b9af-162">Następnie dodaj nowy wpis w tabeli DNS dla domeny niestandardowej przy użyciu narzędzi dostarczonych przez rejestratora.</span><span class="sxs-lookup"><span data-stu-id="5b9af-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="5b9af-163">Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord A, ale pojęcia są takie same.</span><span class="sxs-lookup"><span data-stu-id="5b9af-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="5b9af-164">Użyj jednej z następujących metod, aby uzyskać adres IP usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5b9af-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="5b9af-165">Zaloguj się do [klasycznego portalu Azure], wybierz usługi w chmurze, wybierz **pulpitu nawigacyjnego**, a następnie znajdź **adres publiczny wirtualnego adresu IP (VIP)** wpis w  **szybkiego dostępu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5b9af-165">login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Public Virtual IP (VIP) address** entry in the **quick glance** section.</span></span>
     
       ![Wyświetlanie adres VIP sekcji szybkiego dostępu][vip]
     
       <span data-ttu-id="5b9af-167">**LUB**</span><span class="sxs-lookup"><span data-stu-id="5b9af-167">**OR**</span></span>  
   * <span data-ttu-id="5b9af-168">Instalowanie i konfigurowanie [programu Azure Powershell](/powershell/azure/overview), a następnie użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="5b9af-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="5b9af-169">Jeśli masz wiele punktów końcowych skojarzonych z usługi w chmurze, otrzymasz wiele wierszy zawierających adres IP, ale wszystkie ten sam adres powinien być wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5b9af-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing the IP address, but all should display the same address.</span></span>
     
     <span data-ttu-id="5b9af-170">Zapisz adres IP, ponieważ będzie potrzebny podczas tworzenia rekordu A.</span><span class="sxs-lookup"><span data-stu-id="5b9af-170">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="5b9af-171">Zaloguj się w witrynie rejestratora DNS i przejdź do strony zarządzania DNS.</span><span class="sxs-lookup"><span data-stu-id="5b9af-171">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="5b9af-172">Wyszukaj łącza lub obszarów witryny oznaczone jako **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-172">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="5b9af-173">Teraz można znaleźć, gdzie wybierz lub wprowadź rekordu.</span><span class="sxs-lookup"><span data-stu-id="5b9af-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="5b9af-174">Może być konieczne wybierz typ rekordu z listy rozwijanej lub przejdź do strony Ustawienia zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="5b9af-174">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="5b9af-175">Wybierz lub wprowadź domenę lub poddomen, który będzie używany przez ten rekord.</span><span class="sxs-lookup"><span data-stu-id="5b9af-175">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="5b9af-176">Na przykład wybierz **www** Jeśli chcesz utworzyć alias **www.customdomain.com**. Jeśli chcesz utworzyć wpis symboli wieloznacznych dla wszystkich domen podrzędnych, wprowadź "__*__".</span><span class="sxs-lookup"><span data-stu-id="5b9af-176">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="5b9af-177">Wszystkich domen podrzędnych będzie on zawierał takie jak **mail.customdomain.com**, **login.customdomain.com**, i **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="5b9af-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="5b9af-178">Jeśli chcesz utworzyć rekordu A dla domeny głównej, może być wymieniona jako "**@**" symbol w narzędziach DNS rejestratora.</span><span class="sxs-lookup"><span data-stu-id="5b9af-178">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="5b9af-179">Wprowadź adres IP usługi w chmurze w polu podana.</span><span class="sxs-lookup"><span data-stu-id="5b9af-179">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="5b9af-180">Skojarzenie wpis domeny używane w rekordzie przy użyciu adresu IP wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="5b9af-180">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="5b9af-181">Na przykład następujące rekord przekazuje cały ruch z **contoso.com** do **137.135.70.239**, adres IP wdrożonej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5b9af-181">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="5b9af-182">Nazwa hosta/domeny podrzędnej</span><span class="sxs-lookup"><span data-stu-id="5b9af-182">Host name/Subdomain</span></span> | <span data-ttu-id="5b9af-183">Adres IP</span><span class="sxs-lookup"><span data-stu-id="5b9af-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="5b9af-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="5b9af-184">137.135.70.239</span></span> |

<span data-ttu-id="5b9af-185">W tym przykładzie pokazano tworzenie rekordu A dla domeny głównej.</span><span class="sxs-lookup"><span data-stu-id="5b9af-185">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="5b9af-186">Jeśli chcesz utworzyć wpis symboli wieloznacznych, aby pokrywał wszystkich domen podrzędnych, należy wprowadzić "__*__" jako poddomeny.</span><span class="sxs-lookup"><span data-stu-id="5b9af-186">If you wish to create a wildcard entry to cover all subdomains, you would enter '__*__' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="5b9af-187">Adresy IP na platformie Azure są dynamiczne domyślnie.</span><span class="sxs-lookup"><span data-stu-id="5b9af-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="5b9af-188">Prawdopodobnie warto użyć [zastrzeżony adres IP](../virtual-network/virtual-networks-reserved-public-ip.md) aby upewnić się, czy adres IP nie ulega zmianie.</span><span class="sxs-lookup"><span data-stu-id="5b9af-188">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5b9af-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b9af-189">Next steps</span></span>
* [<span data-ttu-id="5b9af-190">Jak zarządzać usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="5b9af-190">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="5b9af-191">Jak zamapować zawartość usługi CDN na domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="5b9af-191">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="5b9af-192">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="5b9af-193">Dowiedz się, jak [wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-193">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="5b9af-194">Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="5b9af-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[klasycznego portalu Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
