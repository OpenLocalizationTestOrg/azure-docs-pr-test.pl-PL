---
title: aaaUsing hostnames tooregister dynamicznych DNS
description: "Ta strona przedstawia szczegóły na temat tooset się nazwy hostów tooregister dynamicznych DNS w serwerach DNS."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="37c00-103">Przy użyciu nazwy hostów tooregister dynamicznych DNS na serwerze DNS</span><span class="sxs-lookup"><span data-stu-id="37c00-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="37c00-104">[Platforma Azure udostępnia rozpoznawanie nazw](virtual-networks-name-resolution-for-vms-and-role-instances.md) na maszynach wirtualnych (VM) i wystąpień ról.</span><span class="sxs-lookup"><span data-stu-id="37c00-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="37c00-105">Jednak gdy programu rozpoznawania nazw musi wykracza poza udostępnianych przez platformę Azure, musisz podać serwery DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="37c00-106">Dzięki temu hello zasilania tootailor Twojego toosuit rozwiązania DNS określonych potrzeb.</span><span class="sxs-lookup"><span data-stu-id="37c00-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="37c00-107">Na przykład może być konieczne tooaccess zasobów lokalnych za pomocą kontrolera domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37c00-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="37c00-108">Jeśli niestandardowe serwery DNS są hostowane jako maszyny wirtualne Azure może przekazywać nazwy hosta kwerendy o hello takie same nazwy hostów tooresolve tooAzure sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="37c00-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="37c00-109">Jeśli nie chcesz, aby toouse tej trasy, możesz zarejestrować Twojej nazwy hostów maszyny Wirtualnej na serwerze DNS przy użyciu dynamicznych DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="37c00-110">Azure nie ma toodirectly możliwości (np. poświadczenia) hello utworzyć rekordy w serwerach DNS, potrzebne są często alternatywne uzgodnienia.</span><span class="sxs-lookup"><span data-stu-id="37c00-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="37c00-111">Poniżej przedstawiono kilka typowych scenariuszy z alternatyw.</span><span class="sxs-lookup"><span data-stu-id="37c00-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="37c00-112">Klienci systemu Windows</span><span class="sxs-lookup"><span data-stu-id="37c00-112">Windows clients</span></span>
<span data-ttu-id="37c00-113">Klienci z systemem Windows przyłączonych do domeny inne niż podejmować niezabezpieczona aktualizacji dynamicznych DNS (DDNS), po uruchomieniu lub zmianie ich adresów IP.</span><span class="sxs-lookup"><span data-stu-id="37c00-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="37c00-114">Nazwa DNS Hello jest hello hostname plus sufiks podstawowej domeny DNS hello.</span><span class="sxs-lookup"><span data-stu-id="37c00-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="37c00-115">Azure pozostawia sufiks podstawowej domeny DNS hello puste, ale możesz ustawić w hello maszyny Wirtualnej, za pośrednictwem hello [interfejsu użytkownika](https://technet.microsoft.com/library/cc794784.aspx) lub [przy użyciu automatyzacji](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="37c00-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="37c00-116">Klienci z systemem Windows przyłączonych do domeny rejestrują swoje adresy IP z kontrolerem domeny hello przy użyciu bezpiecznych dynamicznych DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="37c00-117">proces przyłączania do domeny Hello ustawia sufiks podstawowej domeny DNS hello na powitania klienta i tworzy i obsługuje hello relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="37c00-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="37c00-118">Klienci systemu Linux</span><span class="sxs-lookup"><span data-stu-id="37c00-118">Linux clients</span></span>
<span data-ttu-id="37c00-119">Klienci systemu Linux zazwyczaj nie rejestrują się z serwerem DNS hello podczas uruchamiania, one przyjęto założenie, że jest powitania serwera DHCP.</span><span class="sxs-lookup"><span data-stu-id="37c00-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="37c00-120">Serwery DHCP w usłudze Azure ma zdolność hello lub poświadczenia tooregister rekordów w serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="37c00-121">Można użyć narzędzia o nazwie *nsupdate*, będące częścią pakietu Bind hello, aktualizacji dynamicznych DNS toosend.</span><span class="sxs-lookup"><span data-stu-id="37c00-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="37c00-122">Ponieważ hello protokół dynamicznej DNS jest standardowym, można użyć *nsupdate* nawet jeśli nie używasz Bind na powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="37c00-123">Można użyć punkty zaczepienia hello, udostępnianych przez toocreate klienta DHCP hello i obsługa hello wpis nazwy hosta w powitania serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="37c00-124">Cyklu DHCP hello powitania klienta wykonuje hello skryptów w */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="37c00-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="37c00-125">Może to być używane przy użyciu nowego adresu IP tooregister hello *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="37c00-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="37c00-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="37c00-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="37c00-127">Można również użyć hello *nsupdate* tooperform polecenia aktualizacji bezpiecznych dynamicznych DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="37c00-128">Na przykład podczas korzystania z serwera Bind DNS, to pary kluczy publiczno prywatnych [wygenerowany](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="37c00-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="37c00-129">Serwer DNS Hello jest [skonfigurowane](http://linux.yyz.us/dns/ddns-server.html) z hello publicznej części klucza hello, którego nie można zweryfikować podpisu hello na powitania żądania.</span><span class="sxs-lookup"><span data-stu-id="37c00-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="37c00-130">Należy użyć hello *-k* tooprovide opcji hello para klucz zbyt*nsupdate* aby hello toobe żądania podpisany aktualizacji dynamicznych DNS.</span><span class="sxs-lookup"><span data-stu-id="37c00-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="37c00-131">Podczas korzystania z serwera DNS systemu Windows, za pomocą uwierzytelniania Kerberos hello *-g* parametru w *nsupdate* (niedostępne w wersji Windows hello *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="37c00-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="37c00-132">toodo, użyj *kinit* tooload hello poświadczenia (np. z [pliku keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="37c00-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="37c00-133">Następnie *nsupdate -g* przejmą hello poświadczenia z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="37c00-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="37c00-134">W razie potrzeby można dodać tooyour sufiks wyszukiwania DNS maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="37c00-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="37c00-135">określono sufiks DNS Hello w hello */etc/resolv.conf* pliku.</span><span class="sxs-lookup"><span data-stu-id="37c00-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="37c00-136">Większość dystrybucjach systemu Linux automatycznie zarządzać hello zawartość tego pliku, dlatego zazwyczaj nie można edytować go.</span><span class="sxs-lookup"><span data-stu-id="37c00-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="37c00-137">Jednak można zastąpić sufiks hello przy użyciu klienta DHCP hello *zastępują* polecenia.</span><span class="sxs-lookup"><span data-stu-id="37c00-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="37c00-138">toodo to w */etc/dhcp/dhclient.conf*, dodać:</span><span class="sxs-lookup"><span data-stu-id="37c00-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

