---
title: "aaaImport i eksportowanie strefa domeny pliku tooAzure DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooimport i eksportowanie DNS strefy tooAzure pliku DNS przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importowanie i eksportowanie pliku strefy DNS przy użyciu hello Azure CLI w wersji 1.0 

W tym artykule przedstawiono sposób tooimport i eksportowanie plików strefy DNS dla usługi Azure DNS przy użyciu hello Azure CLI w wersji 1.0.

## <a name="introduction-toodns-zone-migration"></a>Wprowadzenie tooDNS strefy migracji

Pliku strefy DNS to plik tekstowy zawierający szczegóły każdego rekordu systemu nazw domen (DNS) w strefie hello. Wynika z formatem, dzięki czemu odpowiednie do transferu między systemami DNS rekordów DNS. Przy użyciu pliku strefy to szybki i niezawodny i wygodny sposób tootransfer strefę DNS do lub z usługi Azure DNS.

Usługa DNS platformy Azure obsługuje importowania i eksportowania plików strefy za pomocą hello Azure interfejsu wiersza polecenia (CLI). Importowanie pliku strefy jest **nie** obecnie obsługiwane za pośrednictwem programu Azure PowerShell lub hello portalu Azure.

Hello Azure CLI 1.0 jest narzędziem wiersza polecenia i platform, używany do zarządzania usługami Azure. Jest dostępna dla platformy systemu Windows, Mac i Linux z hello hello [Azure pliki do pobrania](https://azure.microsoft.com/downloads/). Obsługa platform jest ważne, aby importować i eksportować pliki stref, ponieważ hello najczęściej używane nazwy oprogramowanie serwera, [POWIĄZAĆ](https://www.isc.org/downloads/bind/), zwykle działa w systemie Linux.

> [!NOTE]
> Obecnie są dwie wersje hello wiersza polecenia platformy Azure. CLI1.0 opiera się na Node.js i ma polecenia rozpoczynające się od "azure".
> CLI2.0 jest oparty na języku Python i ma polecenia rozpoczynające się od "az". Podczas importowania z pliku strefy jest obsługiwane w obu wersjach, zalecamy użycie poleceń CLI1.0 hello, zgodnie z opisem na tej stronie.

## <a name="obtain-your-existing-dns-zone-file"></a>Uzyskaj do istniejącego pliku strefy DNS

Przed zaimportowaniem pliku strefy DNS w usłudze Azure DNS należy tooobtain kopię pliku strefy hello. Hello źródłu tego pliku zależy od tego, gdzie jest obecnie hostowany hello strefy DNS.

* Jeśli strefy DNS jest hostowana przez partnera usługi (na przykład rejestratora domen, dedykowane dostawcy hostingu DNS lub dostawcy usług w chmurze alternatywne), czy usługa powinien dostarczyć toodownload możliwości hello hello pliku strefy DNS.
* Jeśli strefy DNS jest obsługiwana w systemie DNS systemu Windows, hello domyślny folder plików strefy hello jest **%systemroot%\system32\dns**. przedstawiono również plik strefy tooeach pełną ścieżkę Hello na powitania **ogólne** kartę hello konsolę DNS.
* Jeżeli strefy DNS znajduje się za pomocą powiązania, hello lokalizację pliku strefy hello w każdej strefie jest określony w pliku konfiguracji powiązania hello **named.conf**.

> [!NOTE]
> Strefy pliki pobierane z GoDaddy ma nieco niestandardowym formacie. Należy toocorrect to przed zaimportowaniem plików tych stref w usłudze Azure DNS.
>
> Nazwy DNS w hello RDATA każdy rekord DNS są określane jako w pełni kwalifikowane nazwy, ale nie mają kończącym "." Oznacza to, że są interpretowane przez inne systemy DNS jako nazw względnych. Konieczne jest zakończenie hello tooedit hello strefy pliku tooappend "." tootheir nazwy, aby zaimportować je do usługi Azure DNS.
>
> Na przykład hello rekord CNAME "www 3600 CNAME contoso.com" należy zmienić zbyt "www 3600 CNAME w contoso.com".
> (z tokenem ".").

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importowanie pliku strefy DNS do usługi Azure DNS

Importowanie pliku strefy tworzy nową strefę w usłudze Azure DNS, jeśli już nie istnieje. Jeśli istnieje już strefa hello, hello zestawów rekordów w pliku strefy hello muszą zostać połączone z zestawami rekordów istniejących hello.

### <a name="merge-behavior"></a>Scal zachowanie

* Domyślnie są scalane istniejących i nowych zestawów rekordów. Usuń zduplikowane są identyczne rekordy w zestawie rekordów scalone.
* Alternatywnie, określając hello `--force` opcji, hello zastępuje procesu importowania istniejącego rekordu zestawy z nowego zestawów rekordów. Istniejące zestawy rekordów, które nie mają odpowiedni rekord w pliku strefy importowanych hello nie zostaną usunięte.
* W przypadku zestawów rekordów scalania, hello toolive (TTL) istniejących zestawów rekordów zostanie użyta godzina. Gdy `--force` jest używana, hello TTL nowy zestaw rekordów hello jest używany.
* Początek parametry uwierzytelniania (SOA) (z wyjątkiem `host`) są zawsze pobierane z pliku strefy importowanych hello, niezależnie od tego, czy `--force` jest używany. Podobnie dla hello na wierzchołku strefy hello rekord serwera nazw, hello TTL jest zawsze pobierana z hello importowanych stref pliku.
* Importowany rekord CNAME nie zastępuje istniejący CNAME zarejestrować hello takie same nazwy, chyba że hello `--force` parametr jest określony.
* Gdy wystąpi konflikt między rekord CNAME, a inny rekord hello takie same nazwy, ale o różnych wpisz (niezależnie od tego, który jest istniejących lub nowych), jest zachowywana hello istniejącego rekordu. To jest niezależna od stosowania hello `--force`.

### <a name="additional-information-about-importing"></a>Dodatkowe informacje na temat importowania

Witaj poniższe uwagi znajdują się dodatkowe informacje techniczne na temat strefy hello procesu importowania.

* Witaj `$TTL` dyrektywa jest opcjonalna i jest obsługiwana. Gdy nie `$TTL` dyrektywy jest podane, są importowane rekordy bez jawnego TTL Ustaw domyślną tooa TTL 3600 sekund. Gdy dwa rekordy w hello tego samego zestawu rekordów Określ inną TTLs, niższą wartość hello jest używany.
* Witaj `$ORIGIN` dyrektywa jest opcjonalna i jest obsługiwana. Gdy nie `$ORIGIN` ustawiono hello domyślna wartość używana jest nazwa strefy hello określonego w wierszu polecenia hello (oraz przerywanie hello ".").
* Witaj `$INCLUDE` i `$GENERATE` dyrektywy nie są obsługiwane.
* Obsługiwane są następujące typy rekordów: A, AAAA, CNAME, MX, NS, SOA, SRV i TXT.
* Hello rekord SOA jest tworzona automatycznie przez usługę Azure DNS, gdy tworzona jest strefa. Podczas importowania pliku strefy, wszystkie parametry SOA są pobierane z pliku strefy hello *z wyjątkiem* hello `host` parametru. Ten parametr używa hello wartości dostarczonej przez usługę Azure DNS. Jest to spowodowane tego parametru musi odwoływać się toohello Nazwa podstawowego serwera dostarczane przez usługę Azure DNS.
* rekord serwera nazw Hello na wierzchołku strefy hello jest również tworzone automatycznie przez usługę Azure DNS podczas tworzenia strefy hello. Tylko hello TTL tego zestawu rekordów jest importowany. Te rekordy zawierają hello nazwy serwerów nazw udostępnionych przez usługę Azure DNS. Witaj rejestrowania danych nie zostanie zastąpiona hello wartości zawartych w pliku strefy importowanych hello.
* W publicznej wersji zapoznawczej usługi DNS platformy Azure obsługuje tylko jeden ciąg rekordów TXT. Wielociągu rekordów TXT są jest połączonych i obcięte too255 znaków.

### <a name="cli-format-and-values"></a>Format interfejsu wiersza polecenia i wartości

format Hello tooimport polecenia interfejsu wiersza polecenia Azure hello strefę DNS jest:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Wartości:

* `<resource group>`jest hello Nazwa grupy zasobów hello strefy hello w usłudze Azure DNS.
* `<zone name>`jest nazwą hello hello strefy.
* `<zone file name>`jest hello/nazwa ścieżki toobe pliku strefy hello zaimportowane.

Jeśli strefa o tej nazwie nie istnieje w grupie zasobów hello, utworzono dla Ciebie. Jeśli hello strefy już istnieje, hello zestawy rekordów importowanych są scalane z istniejących zestawów rekordów. toooverwrite hello istniejących zestawów rekordów, użyj hello `--force` opcji.

format hello tooverify pliku strefy bez faktycznie importowania, użyj hello `--parse-only` opcji.

### <a name="step-1-import-a-zone-file"></a>Krok 1. Zaimportuj plik strefy

tooimport pliku strefy dla stref hello **contoso.com**.

1. Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello Azure CLI w wersji 1.0.

    ```azurecli
    azure login
    ```

2. Wybierz subskrypcję hello miejscu toocreate nowej strefy DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. Usługa DNS platformy Azure jest usługą platformy Azure tylko do Menedżera zasobów, więc hello Azure CLI musi mieć tryb Manager tooResource wyłączone.

    ```azurecli
    azure config mode arm
    ```

4. Przed użyciem hello usługa Azure DNS, należy zarejestrować dostawcę zasobów Microsoft.Network hello toouse subskrypcji. (Jest to jednorazowa operacja dla każdej subskrypcji).

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Jeśli nie masz już, należy również toocreate Menedżera zasobów grupy zasobów.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. strefy hello tooimport **contoso.com** z pliku hello **contoso.com.txt** do nowej strefy DNS w grupie zasobów hello **myresourcegroup**, uruchom polecenie hello `azure network dns zone import`.<BR>To polecenie ładuje plik strefy hello i przeanalizować go. polecenie Hello wykonuje szereg poleceń na powitania usługi Azure DNS usługi toocreate hello strefy i ustawia wszystkie hello rekordu w strefie hello. polecenie Hello zgłosi postęp w oknie konsoli hello, wraz z jakiekolwiek błędy i ostrzeżenia. Ponieważ zestawy rekordów są tworzone w serii, może upłynąć kilka minut tooimport pliku dużych strefy.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Krok 2. Sprawdź hello strefy

tooverify hello strefy DNS po zaimportowaniu plików hello, można użyć jednej z następujących metod hello:

* Można wyświetlić listę rekordów hello za pomocą następującego polecenia wiersza polecenia platformy Azure hello:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Wyświetl listę rekordów hello za pomocą polecenia cmdlet programu PowerShell hello `Get-AzureRmDnsRecordSet`.
* Można użyć `nslookup` tooverify rozpoznawania nazw dla hello rekordów. Ponieważ hello strefy nie jest jeszcze delegowana, wystarczy toospecify hello poprawne serwerów nazw usługi Azure DNS jawnie. Witaj poniższy przykład przedstawia sposób tooretrieve hello nazw serwerów nazw przypisanych toohello strefy. IT przedstawiono również sposób zarejestrować tooquery hello "www" za pomocą `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Krok 3. Zaktualizuj Delegowanie DNS

Po upewnieniu się, że strefa hello zostały zaimportowane prawidłowo, należy tooupdate hello DNS delegowania toopoint toohello serwerów nazw usługi Azure DNS. Aby uzyskać więcej informacji, zobacz artykuł hello [zaktualizowania delegowania DNS hello](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Eksportowanie pliku strefy DNS z usługi Azure DNS

format Hello tooimport polecenia interfejsu wiersza polecenia Azure hello strefę DNS jest:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Wartości:

* `<resource group>`jest hello Nazwa grupy zasobów hello strefy hello w usłudze Azure DNS.
* `<zone name>`jest nazwą hello hello strefy.
* `<zone file name>`jest hello/nazwa ścieżki toobe pliku strefy hello wyeksportowane.

Hello strefy importowania, potrzebne są najpierw toosign w, wybierz subskrypcję i skonfiguruj tryb usługi Resource Manager toouse interfejsu wiersza polecenia Azure hello.

### <a name="tooexport-a-zone-file"></a>tooexport pliku strefy

1. Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello wiersza polecenia platformy Azure.

    ```azurecli
    azure login
    ```

2. Wybierz subskrypcję hello miejscu toocreate strefy DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. Usługa DNS platformy Azure jest usługą platformy Azure tylko do Menedżera zasobów. Hello Azure CLI musi być wyłączone tooResource menedżera trybu.

    ```azurecli
    azure config mode arm
    ```

4. istniejąca strefa DNS platformy Azure hello tooexport **contoso.com** w grupie zasobów **myresourcegroup** pliku toohello **contoso.com.txt** (w hello bieżącym folderze), uruchom `azure network dns zone export`. Tego polecenia, które wywołuje hello tooenumerate usługi Azure DNS zestawów rekordów w strefie hello i eksportowanie pliku strefy hello wyniki tooa POWIĄZANIE zgodne.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
