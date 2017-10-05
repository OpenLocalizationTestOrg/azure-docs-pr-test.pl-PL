---
title: "Usługa Azure DNS przewodnik rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Sposoby rozwiązywania typowych problemów z usługą Azure DNS"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="5a55f-103">Usługa Azure DNS przewodnik rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="5a55f-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="5a55f-104">Ta strona zawiera informacje dotyczące rozwiązywania problemów dla często zadawane pytania usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="5a55f-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="5a55f-105">Jeśli te kroki nie rozwiążą problemu, możesz również wyszukać lub post problemu na naszych [forum pomocy technicznej społeczności w witrynie MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="5a55f-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="5a55f-106">Alternatywnie Otwórz żądanie pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5a55f-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="5a55f-107">Nie można utworzyć strefy DNS</span><span class="sxs-lookup"><span data-stu-id="5a55f-107">I can't create a DNS zone</span></span>

<span data-ttu-id="5a55f-108">Aby rozwiązać typowe problemy, spróbuj wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5a55f-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="5a55f-109">Przejrzyj dzienniki inspekcji usługi Azure DNS, aby ustalić przyczynę niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="5a55f-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="5a55f-110">Każda nazwa strefy DNS musi być unikatowa w obrębie swojej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="5a55f-111">To znaczy, że dwie strefy DNS o takiej samej nazwie nie mogą współużytkować grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="5a55f-112">Spróbuj użyć innej nazwy strefy lub innej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="5a55f-113">Możesz zobaczyć błąd „Osiągnięto lub przekroczono maksymalną liczbę stref w subskrypcji {identyfikator subskrypcji}”.</span><span class="sxs-lookup"><span data-stu-id="5a55f-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="5a55f-114">Użyj innej subskrypcji platformy Azure, usuń kilka stref lub skontaktuj się z pomocą techniczną platformy Azure w celu podniesienia limitu dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5a55f-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="5a55f-115">Możesz zobaczyć błąd „Strefa {nazwa strefy} jest niedostępna”.</span><span class="sxs-lookup"><span data-stu-id="5a55f-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="5a55f-116">Ten błąd oznacza, że usługa DNS platformy Azure nie mogła przydzielić serwerów nazw dla tej strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="5a55f-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="5a55f-117">Spróbuj użyć innej nazwy strefy.</span><span class="sxs-lookup"><span data-stu-id="5a55f-117">Try using a different zone name.</span></span> <span data-ttu-id="5a55f-118">Jeśli jesteś właścicielem nazwy domeny, możesz zamiast tego skontaktować się z działem pomocy technicznej platformy Azure, który może przydzielić odpowiednie serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="5a55f-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="5a55f-119">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="5a55f-119">**Recommended documents**</span></span>

<span data-ttu-id="5a55f-120">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="5a55f-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5a55f-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)</span><span class="sxs-lookup"><span data-stu-id="5a55f-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="5a55f-122">Nie można utworzyć nowego rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="5a55f-122">I can't create a DNS record</span></span>

<span data-ttu-id="5a55f-123">Aby rozwiązać typowe problemy, spróbuj wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5a55f-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="5a55f-124">Przejrzyj dzienniki inspekcji usługi Azure DNS, aby ustalić przyczynę niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="5a55f-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="5a55f-125">Czy zestaw rekordów już istnieje?</span><span class="sxs-lookup"><span data-stu-id="5a55f-125">Does the record set exist already?</span></span>  <span data-ttu-id="5a55f-126">Usługa DNS platformy Azure zarządza rekordami za pomocą *zestawów*, czyli kolekcji rekordów o tej samej nazwie i typie.</span><span class="sxs-lookup"><span data-stu-id="5a55f-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="5a55f-127">Jeśli już istnieje rekord o tej danej nazwie i typie, to w celu dodania kolejnego takiego rekordu trzeba poddać edycji istniejący zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="5a55f-128">Czy próbujesz utworzyć rekord w wierzchołku strefy DNS (w „katalogu głównym” strefy)?</span><span class="sxs-lookup"><span data-stu-id="5a55f-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="5a55f-129">Jeśli tak, to konwencja systemu DNS wymaga użycia znaku „@” jako nazwy rekordu.</span><span class="sxs-lookup"><span data-stu-id="5a55f-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="5a55f-130">Standardy systemu DNS nie umożliwiają także używania rekordów CNAME w wierzchołku strefy.</span><span class="sxs-lookup"><span data-stu-id="5a55f-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="5a55f-131">Czy występuje konflikt dotyczący rekordu CNAME?</span><span class="sxs-lookup"><span data-stu-id="5a55f-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="5a55f-132">Standardy systemu DNS nie umożliwiają używania rekordu CNAME o takiej samej nazwie jak nazwa rekordu innego typu.</span><span class="sxs-lookup"><span data-stu-id="5a55f-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="5a55f-133">Jeśli istnieje już rekord CNAME, utworzenie innego typu rekordu o takiej samej nazwie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5a55f-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="5a55f-134">Analogicznie, utworzenie rekordu CNAME zakończy się niepowodzeniem, jeśli jego nazwa jest taka sama jak nazwa istniejącego rekordu innego typu.</span><span class="sxs-lookup"><span data-stu-id="5a55f-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="5a55f-135">Rozwiąż ten konflikt, usuwając drugi rekord lub wybierając inną nazwę rekordu.</span><span class="sxs-lookup"><span data-stu-id="5a55f-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="5a55f-136">Czy osiągnięto limit liczby zestawów rekordów w strefie DNS?</span><span class="sxs-lookup"><span data-stu-id="5a55f-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="5a55f-137">Bieżąca liczba zestawów rekordów oraz najwyższa możliwa liczba zestawów rekordów są pokazane w witrynie Azure Portal w obszarze „Właściwości” danej strefy.</span><span class="sxs-lookup"><span data-stu-id="5a55f-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="5a55f-138">Jeśli osiągnięto ten limit, usuń niektóre zestawy rekordów lub skontaktuj się z działem pomocy technicznej platformy Azure, aby zwiększyć limit liczby zestawów rekordów dla tej strefy. Następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="5a55f-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="5a55f-139">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="5a55f-139">**Recommended documents**</span></span>

<span data-ttu-id="5a55f-140">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="5a55f-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5a55f-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)</span><span class="sxs-lookup"><span data-stu-id="5a55f-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="5a55f-142">Nie mogę rozpoznać mojego rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="5a55f-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="5a55f-143">Rozpoznawanie nazw DNS to wieloetapowy proces, który może się nie powieść z wielu powodów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="5a55f-144">Następujące kroki zawierają informacje pomocne w badaniu przyczyn nieudanego rozpoznawania nazw DNS w przypadku rekordu DNS w strefie hostowanej w usłudze DNS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5a55f-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="5a55f-145">Sprawdź, czy rekordy DNS zostały prawidłowo skonfigurowane w usłudze DNS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5a55f-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="5a55f-146">Przejrzyj rekordy DNS w witrynie Azure Portal, sprawdzając, czy nazwa strefy, nazwa rekordu i typ rekordu są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="5a55f-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="5a55f-147">Sprawdź, czy rekordy DNS są rozpoznawane prawidłowo na serwerach nazw usługi DNS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5a55f-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="5a55f-148">Jeśli zapytania DNS są wysyłane z komputera lokalnego, mogą być wyświetlane wyniki z pamięci podręcznej. Nie odzwierciedlają one aktualnego stanu serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="5a55f-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="5a55f-149">Ponadto w sieciach firmowych często są używane serwery proxy usługi DNS, które uniemożliwiają kierowanie zapytań DNS do określonych serwerów nazw.</span><span class="sxs-lookup"><span data-stu-id="5a55f-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="5a55f-150">Aby uniknąć tych problemów, skorzystaj z usługi rozpoznawania nazw opartej na sieci Web, np. [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="5a55f-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="5a55f-151">Pamiętaj, aby określić poprawne serwery nazw dla strefy DNS zgodnie z informacjami w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5a55f-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="5a55f-152">Sprawdź, czy nazwa DNS jest poprawna (należy określić w pełni kwalifikowaną nazwę, z uwzględnieniem nazwy strefy) i czy typ rekordu jest poprawny</span><span class="sxs-lookup"><span data-stu-id="5a55f-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="5a55f-153">Zobaczy, czy nazwa domeny DNS została prawidłowo [oddelegowana na serwery nazw usługi DNS platformy Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5a55f-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="5a55f-154">Istnieje [wiele witryn innych firm umożliwiających weryfikowanie delegowania DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="5a55f-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="5a55f-155">Ten test jest testem delegowania *strefy*, więc należy podać tylko nazwę strefy DNS, a nie w pełni kwalifikowaną nazwę rekordu.</span><span class="sxs-lookup"><span data-stu-id="5a55f-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="5a55f-156">Po ukończeniu powyższych działań rozpoznawanie rekordu DNS powinno już przebiegać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="5a55f-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="5a55f-157">Do weryfikacji można ponownie skorzystać z usługi [digwebinterface](http://digwebinterface.com), tym razem stosując domyślne ustawienia serwera nazw.</span><span class="sxs-lookup"><span data-stu-id="5a55f-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="5a55f-158">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="5a55f-158">**Recommended documents**</span></span>

[<span data-ttu-id="5a55f-159">Delegowanie domeny do usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="5a55f-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="5a55f-160">Jak określić „usługę” i „protokół” dla rekordu SRV?</span><span class="sxs-lookup"><span data-stu-id="5a55f-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="5a55f-161">Usługa DNS platformy Azure zarządza rekordami DBS za pomocą zestawów, czyli kolekcji rekordów o tej samej nazwie i typie.</span><span class="sxs-lookup"><span data-stu-id="5a55f-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="5a55f-162">W przypadku zestawu rekordów SRV „usługa” i „protokół” muszą być określone jako część nazwy zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="5a55f-163">Inne parametry rekordów SRV („priorytet”, „waga”, „port” i „miejsce docelowe”) są określane osobno dla każdego rekordu w zestawie rekordów.</span><span class="sxs-lookup"><span data-stu-id="5a55f-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="5a55f-164">Przykładowe nazwy rekordów SRV (nazwa usługi „sip”, protokół „tcp”):</span><span class="sxs-lookup"><span data-stu-id="5a55f-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="5a55f-165">\_sip.\_tcp (tworzy zestaw rekordów w wierzchołku strefy)</span><span class="sxs-lookup"><span data-stu-id="5a55f-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="5a55f-166">\_sip.\_tcp.sipservice (tworzy zestaw rekordów o nazwie „sipservice”)</span><span class="sxs-lookup"><span data-stu-id="5a55f-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="5a55f-167">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="5a55f-167">**Recommended documents**</span></span>

<span data-ttu-id="5a55f-168">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="5a55f-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="5a55f-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
 (Tworzenie zestawów rekordów i rekordów DNS przy użyciu witryny Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="5a55f-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="5a55f-170">
[Typ rekordu SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="5a55f-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a55f-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a55f-171">Next steps</span></span>

* <span data-ttu-id="5a55f-172">Dowiedz się więcej o [strefy DNS platformy Azure i rekordów](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="5a55f-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="5a55f-173">Aby rozpocząć korzystanie z usługi Azure DNS, Dowiedz się, jak [utworzyć strefę DNS](dns-getstarted-create-dnszone-portal.md) i [utworzyć rekordy DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a55f-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="5a55f-174">Aby przeprowadzić migrację istniejącej strefy DNS, Dowiedz się, jak [importowanie i eksportowanie pliku strefy DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="5a55f-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

