---
title: "aaaHosting reverse DNS strefy wyszukiwania w usłudze Azure DNS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak strefy wyszukiwania DNS dla zakresy IP wstecznego hello toohost usługi Azure DNS toouse"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Hosting stref wyszukiwania wstecznego wyszukiwania DNS w usłudze Azure DNS

W tym artykule opisano, jak toohost hello wstecznego strefy wyszukiwania DNS dla przypisanego zakresy IP w usłudze Azure DNS. zakresy adresów IP Hello reprezentowany przez strefy wyszukiwania wstecznego hello musi być przypisany organizacji tooyour zwykle przez Usługodawcę internetowego.

tooconfigure reverse DNS dla tooyour przypisany adres IP należącą do Azure usługi Azure, zobacz [Konfigurowanie wyszukiwania wstecznego hello hello adresy IP przydzielone tooyour usługi Azure](dns-reverse-dns-for-azure-services.md).

Przed przeczytaniem tego artykułu, należy się zapoznać z tym [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md).

W tym artykule przedstawiono hello kroki toocreate z pierwszą strefę DNS wyszukiwania wstecznego i rejestrowanie przy użyciu hello portalu Azure, programu Azure PowerShell, Azure CLI w wersji 1.0 lub 2.0 interfejsu wiersza polecenia platformy Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Utwórz strefę wyszukiwania wstecznego DNS

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com)
1. W menu centralnym hello, kliknij polecenie, a następnie kliknij przycisk **nowy** > **sieci** >, a następnie kliknij przycisk **strefy DNS** tooopen hello **strefy DNS Utwórz**bloku.

   ![Strefa DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. Na powitania **strefy DNS Utwórz** bloku Nazwa strefy DNS. Nazwa Hello strefy hello jest inaczej przystosowana do prefiksy IPv4 i IPv6. Użyj instrukcji albo hello [IPV4](#ipv4) lub [IPv6](#ipv6) tooname strefy. Po zakończeniu kliknij przycisk **Utwórz** toocreate hello strefy.

### <a name="ipv4"></a>IPv4

Nazwa strefy wyszukiwania wstecznego IPv4 Hello opiera się na zakres IP hello, który reprezentuje. Powinien on być zgodny z formatem hello: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Podczas tworzenia classless strefy wyszukiwania wstecznego DNS w usłudze Azure DNS, należy użyć łącznika (`-`) zamiast ukośnika ("/") w nazwie strefy hello.
>
> Na przykład dla hello 192.0.2.128/26 zakres IP, należy użyć `128-26.2.0.192.in-addr.arpa` jako nazwa strefy hello zamiast `128/26.2.0.192.in-addr.arpa`.
>
> Wynika to z faktu, zarówno są obsługiwane przez hello standardy usługi DNS, nazwy zawierające ukośnik hello strefy DNS (`/`) znaków nie są obsługiwane w usłudze Azure DNS.

Witaj poniższy przykład przedstawia sposób toocreate C klasy wstecznego strefę DNS o nazwie `2.0.192.in-addr.arpa` w usłudze Azure DNS za pomocą hello portalu Azure:

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure2.png)

Witaj, "Lokalizacja grupy zasobów" definiuje hello lokalizację dla grupy zasobów hello i nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "global" i nie jest wyświetlany.

Witaj następujące przykłady przedstawiają sposób toocomplete to zadanie z programu Azure PowerShell i hello wiersza polecenia platformy Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>Protokół IPv6

Hello Nazwa strefy wyszukiwania wstecznego IPv6 powinny mieć hello następującej postaci: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Aby uzyskać przykłady, zobacz [omówienie wstecznego DNS i pomocy technicznej na platformie Azure](dns-reverse-dns-overview.md#ipv6).


Witaj poniższy przykład przedstawia sposób toocreate strefy IPv6 wstecznego wyszukiwania DNS o nazwie `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` w usłudze Azure DNS za pomocą hello portalu Azure:

 ![Tworzenie strefy DNS](./media/dns-reverse-dns-hosting/figure3.png)

Witaj, "Lokalizacja grupy zasobów" definiuje hello lokalizację dla grupy zasobów hello i nie ma wpływu na powitania strefy DNS. Lokalizacja strefy DNS Hello jest zawsze "global" i nie jest wyświetlany.

Witaj następujące przykłady przedstawiają sposób toocomplete to zadanie z programu Azure PowerShell i hello wiersza polecenia platformy Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Delegowanie strefy wyszukiwania wstecznego DNS

Wytworzeniu strefy wyszukiwania wstecznego DNS, musisz zapewnić, że tej strefy hello jest delegowane ze strefy nadrzędnej hello. Delegowanie DNS umożliwia hello DNS nazwa rozwiązania procesu toofind hello serwery nazw hostujące strefy wyszukiwania wstecznego DNS. Dzięki temu te nazwy serwerów tooanswer odwrotnej zapytania DNS dotyczące hello adresów IP z zakresu adresów.

Proces hello delegowanie strefy DNS dla strefy wyszukiwania do przodu, opisano w [delegować tooAzure Twojego domeny DNS](dns-delegate-domain-azure-dns.md). Delegowanie dla strefy wyszukiwania wstecznego działa hello tak samo. Jedyną różnicą Hello jest konieczność serwery nazw hello tooconfigure z hello usługodawcy internetowego, która opracowała zakresowi adresów IP, a nie rejestratora nazw domen.

## <a name="create-a-dns-ptr-record"></a>Tworzenie rekordu PTR systemu DNS

### <a name="ipv4"></a>IPv4

Witaj poniższy przykład przeprowadzi Cię przez proces hello tworzenie rekordu PTR w strefy wyszukiwania wstecznego DNS w usłudze Azure DNS. Inne typy rekordów i istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md).

1.  U góry hello hello **strefy DNS** bloku, wybierz opcję **+ zestawu rekordów** tooopen hello **dodać zestaw rekordów** bloku.

 ![Strefa DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. Na powitania **dodać zestaw rekordów** bloku. 
1. Wybierz **PTR** z rekordu hello "**typu**" menu.  
1. Witaj Nazwa zestawu rekordów hello rekordu PTR musi toobe hello reszty hello adres IPv4 w odwrotnej kolejności. W tym przykładzie hello pierwsze trzy oktety są już wypełnione jako część nazwy strefy hello (.2.0.192). W związku z tym tylko hello ostatni oktet jest dostarczany w polu Nazwa hello. Można na przykład, nazwę zestawu rekordów "**15**" dla zasobu, którego adres IP jest 192.0.2.15.  
1. W hello "**nazwy domeny**" Wprowadź hello pełną nazwę domeny (FQDN) przy użyciu protokołu IP hello zasobu hello.
1. Wybierz **OK** u dołu hello hello bloku toocreate hello DNS rekordu.

 ![Dodaj zestaw rekordów](./media/dns-reverse-dns-hosting/figure5.png)

Witaj poniżej przedstawiono przykłady dotyczące toocomplete to zadanie z programu PowerShell i hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>Protokół IPv6

Poniższy przykład Hello przeprowadzi Cię przez proces tworzenia nowego rekordu "PTR" hello. Inne typy rekordów i istniejące rekordy toomodify, zobacz [rekordy DNS, zarządzanie i zestawów rekordów przy użyciu portalu Azure hello](dns-operations-recordsets-portal.md).

1. U góry hello hello **bloku strefy DNS**, wybierz pozycję **+ zestawu rekordów** tooopen hello **dodać zestaw rekordów** bloku.

  ![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. Na powitania **dodać zestaw rekordów** bloku. 
3. Wybierz **PTR** z rekordu hello "**typu**" menu.  
4. Witaj Nazwa zestawu rekordów hello rekordu PTR musi toobe hello reszty hello adres IPv6 w odwrotnej kolejności. Nie może zawierać zero kompresji. W tym przykładzie hello pierwszych 64 bitów hello IPv6 są już wypełnione jako część nazwy strefy hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). W związku z tym hello ostatnie 64 bity są dostarczane w polu Nazwa hello. Hello ostatniego 64-bitowy adres IP hello są wprowadzane w odwrotnej kolejności kropką jako ogranicznik hello między każdą liczbę szesnastkową. Można na przykład, nazwę zestawu rekordów "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" dla zasobu, którego adres IP jest 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. W hello "**nazwy domeny**" Wprowadź hello pełną nazwę domeny (FQDN) przy użyciu protokołu IP hello zasobu hello.
6. Wybierz **OK** u dołu hello hello bloku toocreate hello DNS rekordu.

![Dodawanie bloku zestawu rekordów](./media/dns-reverse-dns-hosting/figure7.png)

Witaj poniżej przedstawiono przykłady dotyczące toocomplete to zadanie z programu PowerShell i hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Wyświetlanie rekordów

tooview hello rekordy, które zostały utworzone, przejdź tooyour strefę DNS w hello portalu Azure. W hello obniżyć część hello **strefy DNS** bloku hello rekordów dla strefy DNS hello jest widoczny. Powinna zostać wyświetlona hello domyślne NS i SOA rekordy, które są tworzone w każdej strefie, oraz nowych rekordów, które zostały utworzone.

### <a name="ipv4"></a>IPv4

Blok strefy DNS, wyświetlanie rekordów IPv4 PTR:

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure8.png)

Witaj następujące przykłady Pokaż jak tooview hello PTR rekordy przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>Protokół IPv6

Blok strefy DNS, wyświetlanie rekordów IPv6 PTR:

![Blok strefy DNS](./media/dns-reverse-dns-hosting/figure9.png)

Witaj poniżej przedstawiono przykłady jak tooview hello rekordy z programu PowerShell i hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>Często zadawane pytania

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Stref wyszukiwania wstecznego wyszukiwania DNS może być obsługiwać Moje bloków IP przypisany usługodawcy internetowego w usłudze Azure DNS?

Tak. Hosting hello stref wyszukiwania wstecznego (ARPA) do własnego zakresów IP w usłudze Azure DNS jest w pełni obsługiwany.

Tworzenie strefy wyszukiwania wstecznego hello w usłudze Azure DNS, jak wyjaśniono w tym artykule, a następnie pracować z Usługodawcą zbyt[delegowanie strefy hello](dns-domain-delegation.md).  Następnie można zarządzać hello rekordów PTR dla każdego wyszukiwania wstecznego w hello sam sposób jak inne typy rekordów.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Jaka jest hosting moich kosztów strefy wstecznego wyszukiwania DNS?

Hosting hello strefy wyszukiwania wstecznego wyszukiwania DNS dla sieci bloku IP przypisany usługodawcy internetowego w usłudze Azure DNS jest rozliczana według [standardowe opłaty za usługę Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Czy można udostępniać stref wyszukiwania wstecznego wyszukiwania DNS dla adresów IPv4 i IPv6 w usłudze Azure DNS?

Tak. W tym artykule opisano sposób toocreate protokołów IPv4 i IPv6 reverse DNS strefy wyszukiwania w usłudze Azure DNS.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Można zaimportować istniejący strefy wyszukiwania wstecznego DNS?

Tak. Można użyć hello Azure CLI tooimport istniejących stref DNS w usłudze Azure DNS. Działa to zarówno dla strefy wyszukiwania do przodu i strefy wyszukiwania wstecznego.

Aby uzyskać więcej informacji, zobacz [importu i eksportu, używając pliku strefy DNS hello Azure CLI](dns-import-export.md).

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących wstecznego DNS, zobacz [istnienia wstecznego wyszukiwania DNS dla Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Dowiedz się, jak za[Zarządzanie odwrotnej rekordy DNS dla usług Azure](dns-reverse-dns-for-azure-services.md).
