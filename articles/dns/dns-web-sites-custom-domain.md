---
title: "aaaCreate niestandardowych rekordów DNS dla aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Jak toocreate niestandardową domenę DNS rekordów dla aplikacji sieci web przy użyciu usługi Azure DNS."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="9f4b1-103">Utwórz rekordy DNS dla aplikacji sieci web w domenę niestandardową</span><span class="sxs-lookup"><span data-stu-id="9f4b1-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="9f4b1-104">Można użyć usługi Azure DNS toohost domeny niestandardowej dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="9f4b1-105">Na przykład tworzysz aplikację sieci web platformy Azure i mają tooaccess Twojego użytkowników albo jej przy użyciu contoso.com lub www.contoso.com jako nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="9f4b1-106">toodo, ma dwa rekordy toocreate:</span><span class="sxs-lookup"><span data-stu-id="9f4b1-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="9f4b1-107">Główny "A" toocontoso.com wskazujące rekordów</span><span class="sxs-lookup"><span data-stu-id="9f4b1-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="9f4b1-108">"CNAME" rekordu dla hello www nazwę, która wskazuje toohello rekordu</span><span class="sxs-lookup"><span data-stu-id="9f4b1-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="9f4b1-109">Należy pamiętać, że w przypadku utworzenia rekordu A dla aplikacji sieci web na platformie Azure, powitalne rekord należy ręcznie zaktualizować Jeśli hello źródłowy adres IP dla zmian aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f4b1-110">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9f4b1-110">Before you begin</span></span>

<span data-ttu-id="9f4b1-111">Przed rozpoczęciem, najpierw musisz utworzyć strefę DNS w usłudze Azure DNS i delegowanie strefy hello w tooAzure Twojego rejestratora DNS.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="9f4b1-112">toocreate strefy DNS, wykonaj kroki hello w [utworzyć strefę DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="9f4b1-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="9f4b1-113">toodelegate Twojego tooAzure DNS DNS, wykonaj kroki hello w [Delegowanie domeny DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="9f4b1-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="9f4b1-114">Po utworzeniu strefy i delegowanie go tooAzure DNS, następnie możesz utworzyć rekordów dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="9f4b1-115">1. Tworzenie rekordu A dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="9f4b1-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="9f4b1-116">Rekord jest używane toomap adresu IP tooits nazwy.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="9f4b1-117">W hello poniższy przykład przypisze możemy w jako tooan rekord A adres IPv4:</span><span class="sxs-lookup"><span data-stu-id="9f4b1-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="9f4b1-118">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9f4b1-118">Step 1</span></span>

<span data-ttu-id="9f4b1-119">Utwórz rekord a. i przypisz tooa $rs zmiennej</span><span class="sxs-lookup"><span data-stu-id="9f4b1-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="9f4b1-120">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9f4b1-120">Step 2</span></span>

<span data-ttu-id="9f4b1-121">Dodawanie zestawu rekordów hello IPv4 wartość toohello wcześniej utworzony "@" przy użyciu zmiennej hello $rs przypisane.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="9f4b1-122">Witaj przypisaną wartość IPv4 będzie hello adresu IP dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="9f4b1-123">adres IP hello toofind dla aplikacji sieci web, wykonaj kroki hello w [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9f4b1-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="9f4b1-124">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9f4b1-124">Step 3</span></span>

<span data-ttu-id="9f4b1-125">Zatwierdź hello zestawu rekordów toohello zmiany.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="9f4b1-126">Użyj `Set-AzureRMDnsRecordSet` tooupload hello zmienia toohello tooAzure zestawu rekordów DNS:</span><span class="sxs-lookup"><span data-stu-id="9f4b1-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="9f4b1-127">2. Utwórz rekord CNAME dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="9f4b1-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="9f4b1-128">Jeśli domena jest już zarządzany przez usługę Azure DNS (zobacz [Delegowanie domeny DNS](dns-domain-delegation.md), można użyć następującego toocreate przykład hello rekord CNAME dla contoso.azurewebsites.net hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="9f4b1-129">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9f4b1-129">Step 1</span></span>

<span data-ttu-id="9f4b1-130">Otwórz program PowerShell i Utwórz nowy zestaw rekordów CNAME i przypisać tooa $rs zmiennej.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="9f4b1-131">W tym przykładzie spowoduje utworzenie zestawu rekordów typu CNAME "czas toolive" 600 sekund w strefie DNS o nazwie "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="9f4b1-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9f4b1-132">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-132">hello following example is hello response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="9f4b1-133">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9f4b1-133">Step 2</span></span>

<span data-ttu-id="9f4b1-134">Po utworzeniu zestawu rekordów CNAME hello należy toocreate wartość aliasu jest wskazujących toohello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="9f4b1-135">Przy użyciu hello przypisane wcześniej zmiennej "$rs" można użyć aliasu hello toocreate hello poniższe polecenie programu PowerShell dla contoso.azurewebsites.net aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="9f4b1-136">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-136">hello following example is hello response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="9f4b1-137">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9f4b1-137">Step 3</span></span>

<span data-ttu-id="9f4b1-138">Zatwierdź zmiany hello przy użyciu hello `Set-AzureRMDnsRecordSet` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9f4b1-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="9f4b1-139">Możesz to sprawdzić hello rekord został utworzony prawidłowo badając hello "www.contoso.com" za pomocą polecenia nslookup, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="9f4b1-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="9f4b1-140">Utwórz rekord "awverify" dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="9f4b1-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="9f4b1-141">Jeśli zdecydujesz toouse rekordu A dla aplikacji sieci web, można musi przejść przez tooensure procesu weryfikacji można hello własnej domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="9f4b1-142">Ten krok weryfikacji jest realizowane przez utworzenie rekordu CNAME specjalne o nazwie "awverify".</span><span class="sxs-lookup"><span data-stu-id="9f4b1-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="9f4b1-143">Ta sekcja dotyczy tylko tooA rekordy.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="9f4b1-144">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9f4b1-144">Step 1</span></span>

<span data-ttu-id="9f4b1-145">Utwórz rekord "awverify" hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-145">Create hello "awverify" record.</span></span> <span data-ttu-id="9f4b1-146">W poniższym przykładzie hello zostanie utworzony rekord "aweverify" hello własność tooverify contoso.com hello domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="9f4b1-147">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-147">hello following example is hello response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="9f4b1-148">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9f4b1-148">Step 2</span></span>

<span data-ttu-id="9f4b1-149">Po utworzeniu zestawu rekordów hello "awverify" przypisać rekord CNAME hello ustawić alias.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="9f4b1-150">W poniższym przykładzie hello możemy przypisze tooawverify.contoso.azurewebsites.net alias zestawu rekordów CNAMe hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="9f4b1-151">Poniższy przykład Hello jest hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-151">hello following example is hello response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="9f4b1-152">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9f4b1-152">Step 3</span></span>

<span data-ttu-id="9f4b1-153">Zatwierdź zmiany hello przy użyciu hello `Set-AzureRMDnsRecordSet cmdlet`, jak pokazano w poniższym polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="9f4b1-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f4b1-154">Next steps</span></span>

<span data-ttu-id="9f4b1-155">Wykonaj kroki hello w [Konfigurowanie niestandardowej nazwy domeny dla usługi App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure toouse aplikacji sieci web domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9f4b1-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
