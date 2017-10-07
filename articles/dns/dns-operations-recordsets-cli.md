---
title: "Azure CLI 2.0 hello aaaManage rekordy DNS przy użyciu usługi Azure DNS | Dokumentacja firmy Microsoft"
description: "Zarządzanie zestawów rekordów DNS i rekordy w usłudze Azure DNS, gdy hosting domeny w usłudze Azure DNS. Wszystkie polecenia 2.0 interfejsu wiersza polecenia dla operacji na zestawów rekordów i rekordów."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a>Zarządzanie rekordami DNS i zestawy rekordów w usłudze Azure DNS przy użyciu hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Interfejs wiersza polecenia platformy Azure 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

W tym artykule opisano, jak toomanage rekordy DNS dla strefy DNS przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 2.0, który jest dostępny dla systemu Windows, Mac i Linux między platformami. Można również zarządzać rekordami DNS przy użyciu [programu Azure PowerShell](dns-operations-recordsets.md) lub hello [portalu Azure](dns-operations-recordsets-portal.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

* [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modele wdrażania.
* [Azure CLI 2.0](dns-operations-recordsets-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.

Przykłady Hello w tym artykule założono, że masz już [zainstalowane hello Azure CLI 2.0, zalogowany i utworzyć strefę DNS](dns-operations-dnszones-cli.md).

## <a name="introduction"></a>Wprowadzenie

Przed utworzeniem rekordy DNS w usłudze Azure DNS, należy najpierw toounderstand jak usługi Azure DNS organizuje rekordy DNS w zestawach rekordów DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Aby uzyskać więcej informacji na temat rekordów DNS w usłudze Azure DNS, zobacz [Strefy i rekordy DNS](dns-zones-records.md).

## <a name="create-a-dns-record"></a>Tworzenie rekordu DNS

toocreate rekord DNS, użyj hello `az network dns record-set <record-type> set-record` polecenie (gdzie `<record-type>` jest hello typu rekordu, tj , srv txt, itp.) Aby uzyskać pomoc, zobacz `az network dns record-set --help`.

Podczas tworzenia rekordu, potrzebna jest nazwa grupy zasobów toospecify hello, nazwę strefy, nazwę, typ rekordu hello i hello szczegółów rekordu hello Trwa tworzenie zestawu rekordów. Witaj podanej nazwy zestawu rekordów musi być *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy.

Jeśli jeszcze nie istnieje zestaw rekordów hello, to polecenie tworzy go. Jeśli istnieje już zestaw rekordów hello, to polecenie dodaje rekord hello Określ toohello istniejącego zestawu rekordów.

Jeśli jest tworzony nowy rekord, używany jest domyślny czas wygaśnięcia wynoszący 3600. Aby uzyskać instrukcje dotyczące toouse różnych TTLs, zobacz temat [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).

Witaj poniższym przykładzie jest tworzony rekord A o nazwie *www* w strefie hello *contoso.com* w grupie zasobów hello *MyResourceGroup*. Witaj adres IP hello jest rekord *1.2.3.4*.

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

Ustaw toocreate rekord w wierzchołku strefy hello hello (w tym przypadku "contoso.com"), użyj nazwy rekordu hello "@", wraz ze znakami cudzysłowu hello:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a>Tworzenie zestawu rekordów DNS

W hello powyżej przykłady, hello rekord DNS została albo dodano tooan istniejącego zestawu rekordów lub utworzono zestaw rekordów hello *niejawnie*. Można również utworzyć zestaw rekordów hello *jawnie* przed dodaniem rejestruje tooit. Usługa DNS platformy Azure obsługuje "empty" zestawów rekordów, które mogą działać jako tooreserve symbol zastępczy nazwy DNS przed utworzeniem rekordów DNS. Pusty zestawów rekordów są widoczne w hello Azure DNS kontrolować płaszczyzny, ale nie są wyświetlane na serwery hello Azure DNS.

Zestawy rekordów są tworzone przy użyciu hello `az network dns record-set <record-type> create` polecenia. Aby uzyskać pomoc, zobacz `az network dns record-set <record-type> create --help`.

Tworzenie rekordu hello jawnie ustaw umożliwia toospecify właściwości zestawu rekordów, takie jak hello [czasu wygaśnięcia (TTL, Time-To-Live)](dns-zones-records.md#time-to-live) i metadanych. [Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość.

Witaj poniższy przykład tworzy pusty zestaw rekordów typu "A" TTL 60 sekund, przy użyciu hello `--ttl` parametr (forma krótka `-l`):

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

Hello poniższym przykładzie jest tworzony rekord z dwóch wpisów metadanych, "dział = not" i "środowiska produkcji =", za pomocą hello `--metadata` parametru:

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

Posiadanie utworzony pusty zestaw rekordów, można dodawać rekordy przy użyciu `azure network dns record-set <record-type> set-record` zgodnie z opisem w [Utwórz rekord DNS](#create-a-dns-record).

## <a name="create-records-of-other-types"></a>Tworzenie rekordów innych typów

Posiadanie widoczne szczegółowo jak rekordy toocreate "A", hello następujących przykładach pokazano, jak rekord toocreate innych typów rekordów obsługiwane przez usługę Azure DNS.

Parametry Hello używane toospecify hello rekordu danych różnią się w zależności od typu hello hello rekordu. Na przykład dla rekordów typu "A", należy określić adres hello IPv4 z parametrem hello `--ipv4-address <IPv4 address>`. Witaj parametry dla poszczególnych typów rekordów mogą być wyświetlane przy użyciu `az network dns record-set <record-type> set-record --help`.

W każdym przypadku zostanie przedstawiony sposób toocreate pojedynczego rekordu. rekord Hello jest dodany toohello istniejącego zestawu rekordów lub zestawu rekordów utworzone niejawnie. Aby uzyskać więcej informacji na temat tworzenia zestawów rekordów i rekordu definiujący parametr jawnie, zobacz [utworzyć zestaw rekordów DNS](#create-a-dns-record-set).

Firma Microsoft nie dają toocreate przykład zestawu rekordów SOA, ponieważ SOAs są tworzone i usunąć z każdej strefy DNS i nie można utworzyć ani usunąć oddzielnie. Jednak [hello SOA można modyfikować, jak pokazano w przykładzie nowsze](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record"></a>Utwórz rekord AAAA

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a>Utwórz rekord CNAME

> [!NOTE]
> Standardy usługi DNS Hello nie zezwalają na rekordy CNAME w wierzchołku hello strefy (`--Name "@"`), ani akceptują zestawów rekordów zawierających więcej niż jeden rekord.
> 
> Aby uzyskać więcej informacji, zobacz [rekordy CNAME](dns-zones-records.md#cname-records).

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a>Utwórz rekord MX

W tym przykładzie używamy nazwy zestawu rekordów hello "@" hello toocreate rekord MX w wierzchołku strefy hello (w tym przypadku "contoso.com").

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a>Tworzenie rekordów NS

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a>Utwórz rekord PTR

W takim przypadku "Mój-arpa-zone.com" reprezentuje hello strefy ARPA reprezentujący zakresowi adresów IP. Każdy rekord PTR ustawione w tej strefie odpowiada tooan adres IP zakresu tego adresu IP.  Nazwa rekordu Hello "10" jest Witaj oktet ostatniego adresu IP hello tego zakresu IP reprezentowany przez ten rekord.

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a>Tworzenie rekordów SRV

Podczas tworzenia [zestawu rekordów SRV](dns-zones-records.md#srv-records), określ hello  *\_usługi* i  *\_protokołu* w hello nazwy zestawu rekordów. Nie istnieje żadne tooinclude potrzeby "@" w hello nazwy zestawu rekordów podczas tworzenia rekordów SRV zestawu w wierzchołku strefy hello.

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a>Utwórz rekord TXT

Witaj poniższy przykład przedstawia sposób rejestrowania toocreate TXT. Aby uzyskać więcej informacji na temat hello maksymalna długość ciągu obsługiwane w rekordach TXT, zobacz [rekordów TXT](dns-zones-records.md#txt-records).

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a>Pobierz zestaw rekordów

Użyj istniejącego zestawu rekordów, tooretrieve `az network dns record-set <record-type> show`. Aby uzyskać pomoc, zobacz `az network dns record-set <record-type> show --help`.

Podczas tworzenia rekordu lub zestawu rekordów, rekord hello określić nazwy musi być *względną* nazwy, co oznacza należy wykluczyć hello nazwy strefy. Należy również typ rekordu hello toospecify, hello strefie zawierającej rekord hello ustawić i hello grupę zasobów, zawierającą hello strefy.

Witaj poniższy przykład pobiera rekordu hello *www* a typu ze strefy *contoso.com* w grupie zasobów *MyResourceGroup*:

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a>Lista zestawów rekordów

Wyświetl listę wszystkich rekordów w strefie DNS przy użyciu hello `az network dns record-set list` polecenia. Aby uzyskać pomoc, zobacz `az network dns record-set list --help`.

W tym przykładzie zwraca zestawy wszystkich rekordów w strefie hello *contoso.com*, w grupie zasobów *MyResourceGroup*, niezależnie od tego, czy nazwa lub typ rekordu:

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

W tym przykładzie zwraca wszystkie zestawy rekordów zgodne hello danego typu rekordu (w tym przypadku rekordy ""):

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a>Dodawanie rekordów tooan istniejącego zestawu rekordów

Można użyć `az network dns record-set <record-type> set-record` zarówno zestaw rekordów w nowym rekordzie toocreate lub zestaw rekordów istniejącego rekordu tooan tooadd.

Aby uzyskać więcej informacji, zobacz [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.

## <a name="remove-a-record-from-an-existing-record-set"></a>Usuń rekord z istniejącego zestawu rekordów.

tooremove DNS rekordów z istniejącego zestawu rekordów, użyj `az network dns record-set <record-type> remove-record`. Aby uzyskać pomoc, zobacz `az network dns record-set <record-type> remove-record -h`.

To polecenie usuwa rekord DNS z zestawu rekordów. Usunięcie ostatniego rekordu hello w zestawie rekordów samego zestawu rekordów hello są także usuwane. pusty zestaw rekordów tookeep hello Użyj hello `--keep-empty-record-set` opcji.

Należy toospecify hello toobe rekordów usunięte i hello strefy należy ją usunąć, używając hello takich samych parametrach co podczas tworzenia rekordów przy użyciu `az network dns record-set <record-type> set-record`. Te parametry są opisane w [Utwórz rekord DNS](#create-a-dns-record) i [tworzenie rekordów innych typów](#create-records-of-other-types) powyżej.

powitania po usuwaniu przykład Witaj rekord z wartością "1.2.3.4" z rekordu hello ustawić nazwane *www* w strefie hello *contoso.com*, w grupie zasobów hello *MyResourceGroup*.

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a>Modyfikowanie istniejącego zestawu rekordów

Każdy zestaw rekordów zawiera [czas wygaśnięcia (TTL)](dns-zones-records.md#time-to-live), [metadanych](dns-zones-records.md#tags-and-metadata)i rekordów DNS. Witaj poniższe sekcje zawierają opis sposobu toomodify tych właściwości.

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a>toomodify rekord A, AAAA, MX, NS, PTR, SRV i TXT

toomodify istniejący rekord z typu A, AAAA, MX, NS, PTR, SRV i TXT, należy najpierw dodać nowego rekordu, a następnie usuń hello istniejącego rekordu. Aby uzyskać szczegółowe informacje na temat toodelete i dodać rekordy, zobacz hello wcześniejszej części tego artykułu.

Witaj poniższy przykład pokazuje, jak toomodify rekord "A", z tooIP 1.2.3.4 adres IP adresów 5.6.7.8:

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

Nie można dodać, usunąć lub zmodyfikować rekordy hello hello automatycznie utworzyć zestaw w wierzchołku strefy hello rekordów NS (`--Name "@"`, w tym znaki cudzysłowu). Dla tego zestawu rekordów hello zmiany tylko dozwolone są zestawu rekordów hello toomodify TTL i metadanych.

### <a name="toomodify-a-cname-record"></a>toomodify rekord CNAME

W przeciwieństwie do większości innych typów rekordów zestawu rekordów CNAME może zawierać tylko jeden rekord.  W związku z tym nie można zastąpić bieżącą wartość hello, dodawania nowego rekordu i usuwanie istniejącego rekordu hello, podobnie jak w przypadku innych typów rekordów.

Zamiast tego należy użyć toomodify rekord CNAME `az network dns record-set cname set-record`. Aby uzyskać pomoc zobacz`az network dns record-set cname set-record --help`

Witaj przykład modyfikuje zestawu rekordów CNAME hello *www* w strefie hello *contoso.com*, w grupie zasobów *MyResourceGroup*, toopoint za "www.fabrikam.net" zamiast jego Istniejąca wartość:

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a>toomodify rekord SOA

W przeciwieństwie do większości innych typów rekordów zestawu rekordów CNAME może zawierać tylko jeden rekord.  W związku z tym nie można zastąpić bieżącą wartość hello, dodawania nowego rekordu i usuwanie istniejącego rekordu hello, podobnie jak w przypadku innych typów rekordów.

Zamiast tego należy użyć hello toomodify rekord SOA `az network dns record-set soa update`. Aby uzyskać pomoc, zobacz `az network dns record-set soa update --help`.

Witaj poniższy przykład przedstawia sposób rejestrowania właściwość tooset hello "e-mail" hello SOA strefy hello *contoso.com* w grupie zasobów hello *MyResourceGroup*:

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS rekordów w wierzchołku strefy hello

zestaw w wierzchołku strefy hello rekordów NS Hello jest tworzony automatycznie w każdej strefie DNS. Zawiera ona nazwy hello hello Azure DNS nazwy serwerów przypisanej toohello strefy.

Możesz dodać dodatkowe nazwy serwerów toothis NS zestawu rekordów, toosupport wspólnie hosting domeny z więcej niż jednego dostawcy usługi DNS. Można również zmodyfikować hello TTL i metadanych dla tego zestawu rekordów. Jednak nie można usunąć ani zmodyfikować hello wstępnie wypełnione serwerów nazw usługi Azure DNS.

Należy pamiętać, że dotyczy to tylko toohello NS zestawu rekordów w wierzchołku strefy hello. Inne NS zestawów rekordów w strefie (jako stref podrzędnych używane toodelegate) może być modyfikowany bez ograniczeń.

Witaj poniższy przykład przedstawia tooadd rekordów NS toohello dodatkowe nazwy serwera konfiguracji na wierzchołku strefy hello:

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a>Ustaw hello toomodify TTL istniejącego rekordu

Ustaw hello toomodify TTL istniejącego rekordu, użyj `azure network dns record-set <record-type> update`. Aby uzyskać pomoc, zobacz `azure network dns record-set <record-type> update --help`.

Witaj poniższy przykład pokazuje, jak toomodify zestawu rekordów TTL, w tym przypadku too60 sekund:

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a>metadane hello toomodify istniejącego zestawu rekordów

[Metadane zestawu rekordów](dns-zones-records.md#tags-and-metadata) może być tooassociate używane dane specyficzne dla aplikacji z każdego zestawu rekordów jako pary klucz wartość. Ustaw toomodify hello metadane istniejącego rekordu, użyj `az network dns record-set <record-type> update`. Aby uzyskać pomoc, zobacz `az network dns record-set <record-type> update --help`.

Hello poniższy przykład przedstawia sposób toomodify, zestaw rekordów, o dwa wpisy metadanych, "dział = not" i "środowiska produkcyjnego =". Należy zauważyć, że metadane *zastąpione* przez wartości hello podane.

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a>Usuń zestaw rekordów

Zestawy rekordów można usunąć za pomocą hello `az network dns record-set <record-type> delete` polecenia. Aby uzyskać pomoc, zobacz `azure network dns record-set <record-type> delete --help`. Usunięcie zestawu rekordów spowoduje również usunięcie wszystkich rekordów w zestawie rekordów hello.

> [!NOTE]
> Nie można usunąć hello SOA i NS zestawów rekordów w wierzchołku strefy hello (`--name "@"`).  Te są tworzone automatycznie podczas hello strefy został utworzony i są usuwane automatycznie po usunięciu hello strefy.

Witaj poniższy przykład powoduje usunięcie zestawu o nazwie rekordów hello *www* a typu ze strefy hello *contoso.com* w grupie zasobów *MyResourceGroup*:

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

Jesteś operację usuwania hello zostanie wyświetlony monit o tooconfirm. toosuppress ten monit, użyj hello `--yes` przełącznika.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [strefy i rekordy w usłudze Azure DNS](dns-zones-records.md).
<br>
Dowiedz się, jak za[ochrony strefy i rekordy](dns-protect-zones-recordsets.md) przy użyciu usługi Azure DNS.
