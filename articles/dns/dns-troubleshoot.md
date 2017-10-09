---
title: "Przewodnik rozwiązywania problemów DNS aaaAzure | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot typowe problemy związane z usługi Azure DNS"
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
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="852bb-103">Usługa Azure DNS przewodnik rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="852bb-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="852bb-104">Ta strona zawiera informacje dotyczące rozwiązywania problemów dla często zadawane pytania usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="852bb-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="852bb-105">Jeśli te kroki nie rozwiążą problemu, możesz również wyszukać lub post problemu na naszych [forum pomocy technicznej społeczności w witrynie MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="852bb-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="852bb-106">Alternatywnie Otwórz żądanie pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="852bb-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="852bb-107">Nie można utworzyć strefy DNS</span><span class="sxs-lookup"><span data-stu-id="852bb-107">I can't create a DNS zone</span></span>

<span data-ttu-id="852bb-108">tooresolve typowe problemy, wypróbuj co najmniej jeden z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="852bb-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="852bb-109">Przejrzyj powitalne inspekcji usługi Azure DNS rejestruje Przyczyna niepowodzenia hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="852bb-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="852bb-110">Każda nazwa strefy DNS musi być unikatowa w obrębie swojej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="852bb-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="852bb-111">Oznacza to, że dwie strefy DNS z hello takie same nazwy nie mogą współużytkować grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="852bb-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="852bb-112">Spróbuj użyć innej nazwy strefy lub innej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="852bb-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="852bb-113">Może zostać wyświetlony błąd "Osiągnięto lub przekroczono maksymalną liczbę stref w subskrypcji {identyfikator subskrypcji} hello."</span><span class="sxs-lookup"><span data-stu-id="852bb-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="852bb-114">Użyj innej subskrypcji platformy Azure, usuń niektóre strefy lub skontaktuj się z pomocą techniczną platformy Azure tooraise limit subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="852bb-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="852bb-115">Może zostać wyświetlony błąd "hello strefa"{Nazwa strefy}"nie jest dostępny."</span><span class="sxs-lookup"><span data-stu-id="852bb-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="852bb-116">Ten błąd oznacza, że usługi Azure DNS tooallocate serwerów nazw dla tej strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="852bb-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="852bb-117">Spróbuj użyć innej nazwy strefy.</span><span class="sxs-lookup"><span data-stu-id="852bb-117">Try using a different zone name.</span></span> <span data-ttu-id="852bb-118">Alternatywnie Jeśli jesteś właścicielem nazwy domeny hello, skontaktuj się z pomocy technicznej platformy Azure, który można przydzielić serwery nazw dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="852bb-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="852bb-119">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="852bb-119">**Recommended documents**</span></span>

<span data-ttu-id="852bb-120">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="852bb-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="852bb-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)</span><span class="sxs-lookup"><span data-stu-id="852bb-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="852bb-122">Nie można utworzyć nowego rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="852bb-122">I can't create a DNS record</span></span>

<span data-ttu-id="852bb-123">tooresolve typowe problemy, wypróbuj co najmniej jeden z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="852bb-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="852bb-124">Przejrzyj powitalne inspekcji usługi Azure DNS rejestruje Przyczyna niepowodzenia hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="852bb-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="852bb-125">Zestaw rekordów hello istnieje już?</span><span class="sxs-lookup"><span data-stu-id="852bb-125">Does hello record set exist already?</span></span>  <span data-ttu-id="852bb-126">Usługa DNS platformy Azure zarządza rekordami przy użyciu rekordu *ustawia*, hello kolekcji rekordów hello takie same nazwy i hello takie same, które są typu.</span><span class="sxs-lookup"><span data-stu-id="852bb-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="852bb-127">Jeśli rekord z hello takie same nazwy i typ już istnieje, następnie tooadd innego takie należy edytować hello istniejącego rekordu zestawu rekordów.</span><span class="sxs-lookup"><span data-stu-id="852bb-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="852bb-128">Czy próbujesz toocreate rekord w wierzchołku strefy DNS hello (hello "główny" hello strefy)?</span><span class="sxs-lookup"><span data-stu-id="852bb-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="852bb-129">Jeśli tak, hello Konwencja DNS jest toouse hello "@" jako nazwa rekordu hello znak.</span><span class="sxs-lookup"><span data-stu-id="852bb-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="852bb-130">Należy również zauważyć, że hello standardy usługi DNS nie zezwalają na rekordy CNAME w wierzchołku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="852bb-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="852bb-131">Czy występuje konflikt dotyczący rekordu CNAME?</span><span class="sxs-lookup"><span data-stu-id="852bb-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="852bb-132">Standardy usługi DNS Hello nie zezwalają na rekordu CNAME o hello takie same nazwy jako rekord innego typu.</span><span class="sxs-lookup"><span data-stu-id="852bb-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="852bb-133">Jeśli masz istniejące CNAME, tworzenie rekordu z hello nie powiedzie się w tej samej nazwy innego typu.</span><span class="sxs-lookup"><span data-stu-id="852bb-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="852bb-134">Podobnie utworzenie rekordu CNAME kończy się niepowodzeniem, jeśli nazwa hello odpowiada istniejącego rekordu innego typu.</span><span class="sxs-lookup"><span data-stu-id="852bb-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="852bb-135">Usuń konflikt hello przez usunięcie hello inny rekord lub wybrać nazwę innego rekordu.</span><span class="sxs-lookup"><span data-stu-id="852bb-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="852bb-136">Czy osiągnięto limit hello hello liczby zestawów rekordów w strefie DNS? Witaj bieżąca liczba zestawów rekordów i hello maksymalną liczbę zestawów rekordów są wyświetlane w portalu Azure, w obszarze hello 'właściwości' strefy hello hello.</span><span class="sxs-lookup"><span data-stu-id="852bb-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="852bb-137">Jeśli zostanie osiągnięty limit, następnie usuń niektóre zestawy rekordów lub skontaktuj się z pomocą techniczną platformy Azure tooraise limitu zestaw rekordów dla tej strefy, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="852bb-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="852bb-138">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="852bb-138">**Recommended documents**</span></span>

<span data-ttu-id="852bb-139">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="852bb-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="852bb-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md) (Tworzenie strefy DNS)</span><span class="sxs-lookup"><span data-stu-id="852bb-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="852bb-141">Nie mogę rozpoznać mojego rekordu DNS</span><span class="sxs-lookup"><span data-stu-id="852bb-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="852bb-142">Rozpoznawanie nazw DNS to wieloetapowy proces, który może się nie powieść z wielu powodów.</span><span class="sxs-lookup"><span data-stu-id="852bb-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="852bb-143">Witaj Poniższe etapy ułatwiają zbadać, dlaczego niepowodzenie rozpoznawania nazw DNS dla rekordu DNS w strefie hostowanych w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="852bb-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="852bb-144">Upewnij się, że rekordy DNS hello ma poprawnie skonfigurowany w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="852bb-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="852bb-145">Przejrzyj hello rekordów DNS w hello portalu Azure, sprawdzanie, czy hello nazwę strefy, nazwę rekordu i typ rekordu są poprawne.</span><span class="sxs-lookup"><span data-stu-id="852bb-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="852bb-146">Upewnij się, rekordy DNS hello rozpoznawane poprawnie na serwery hello Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="852bb-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="852bb-147">Jeśli wprowadzisz zapytania DNS z komputera lokalnego, mogą pojawić się buforowane wyniki, które nie odzwierciedlają hello bieżący stan serwerów nazw hello.</span><span class="sxs-lookup"><span data-stu-id="852bb-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="852bb-148">Ponadto sieciach firmowych często używają serwerów proxy DNS, które uniemożliwiają zapytania DNS skierowane toospecific serwery nazw.</span><span class="sxs-lookup"><span data-stu-id="852bb-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="852bb-149">tooavoid usługa rozpoznawania nazw oparte na sieci web takich jak używać tych problemów [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="852bb-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="852bb-150">Hello serwerami poprawną nazwę dla swojej strefy DNS, jak pokazano w portalu Azure hello być toospecify się, że.</span><span class="sxs-lookup"><span data-stu-id="852bb-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="852bb-151">Sprawdź, czy nazwa DNS hello jest poprawna, (masz toospecify hello w pełni kwalifikowana nazwa, łącznie z nazwą strefy hello) i typ rekordu hello jest prawidłowa</span><span class="sxs-lookup"><span data-stu-id="852bb-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="852bb-152">Potwierdź tej nazwy domeny DNS hello została prawidłowo [delegowane serwerów nazw usługi Azure DNS toohello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="852bb-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="852bb-153">Istnieje [wiele witryn innych firm umożliwiających weryfikowanie delegowania DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="852bb-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="852bb-154">Ten test jest *strefy* delegowania testu, dlatego należy wprowadzić tylko nazwę strefy DNS hello i nie hello pełni kwalifikowaną nazwę rekordu.</span><span class="sxs-lookup"><span data-stu-id="852bb-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="852bb-155">Po zakończeniu hello powyżej, Twoje rekord DNS powinien teraz prowadzić poprawnie.</span><span class="sxs-lookup"><span data-stu-id="852bb-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="852bb-156">tooverify, można ponownie użyć [digwebinterface](http://digwebinterface.com), przy użyciu hello domyślne nazwy ustawienia serwera.</span><span class="sxs-lookup"><span data-stu-id="852bb-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="852bb-157">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="852bb-157">**Recommended documents**</span></span>

[<span data-ttu-id="852bb-158">Delegat tooAzure domeny DNS</span><span class="sxs-lookup"><span data-stu-id="852bb-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="852bb-159">Jak określić hello "Usługa" i "Protokół" dla rekordu SRV?</span><span class="sxs-lookup"><span data-stu-id="852bb-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="852bb-160">Usługa DNS platformy Azure zarządza rekordami DNS jako zestawów rekordów — Witaj kolekcji rekordów z hello takie same nazwy i hello sam typu.</span><span class="sxs-lookup"><span data-stu-id="852bb-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="852bb-161">Dla zestawu rekordów SRV toobe określony jako część nazwy zestawu rekordów hello należy hello "Usługa" i "Protokół".</span><span class="sxs-lookup"><span data-stu-id="852bb-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="852bb-162">Witaj inne parametry SRV ("priority", "weight", "port" i "target") są określane oddzielnie dla każdego rekordu w zestawie rekordów hello.</span><span class="sxs-lookup"><span data-stu-id="852bb-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="852bb-163">Przykładowe nazwy rekordów SRV (nazwa usługi „sip”, protokół „tcp”):</span><span class="sxs-lookup"><span data-stu-id="852bb-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="852bb-164">\_SIP. \_tcp (tworzy rekord w wierzchołku strefy hello)</span><span class="sxs-lookup"><span data-stu-id="852bb-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="852bb-165">\_sip.\_tcp.sipservice (tworzy zestaw rekordów o nazwie „sipservice”)</span><span class="sxs-lookup"><span data-stu-id="852bb-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="852bb-166">**Zalecane dokumenty**</span><span class="sxs-lookup"><span data-stu-id="852bb-166">**Recommended documents**</span></span>

<span data-ttu-id="852bb-167">[DNS zones and records](dns-zones-records.md)
 (Strefy i rekordy DNS)</span><span class="sxs-lookup"><span data-stu-id="852bb-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="852bb-168">
[Tworzenie zestawów rekordów DNS i rekordów przy użyciu hello portalu Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="852bb-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="852bb-169">
[Typ rekordu SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="852bb-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="852bb-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="852bb-170">Next steps</span></span>

* <span data-ttu-id="852bb-171">Dowiedz się więcej o [strefy DNS platformy Azure i rekordów](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="852bb-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="852bb-172">toostart przy użyciu usługi Azure DNS, Dowiedz się, jak za[utworzyć strefę DNS](dns-getstarted-create-dnszone-portal.md) i [utworzyć rekordy DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="852bb-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="852bb-173">toomigrate istniejącej strefy DNS, Dowiedz się, jak za[importowanie i eksportowanie pliku strefy DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="852bb-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

