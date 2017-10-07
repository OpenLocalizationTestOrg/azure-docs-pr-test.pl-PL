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
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="fb816-103">Importowanie i eksportowanie pliku strefy DNS przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="fb816-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="fb816-104">W tym artykule przedstawiono sposób tooimport i eksportowanie plików strefy DNS dla usługi Azure DNS przy użyciu hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="fb816-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="fb816-105">Wprowadzenie tooDNS strefy migracji</span><span class="sxs-lookup"><span data-stu-id="fb816-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="fb816-106">Pliku strefy DNS to plik tekstowy zawierający szczegóły każdego rekordu systemu nazw domen (DNS) w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="fb816-107">Wynika z formatem, dzięki czemu odpowiednie do transferu między systemami DNS rekordów DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="fb816-108">Przy użyciu pliku strefy to szybki i niezawodny i wygodny sposób tootransfer strefę DNS do lub z usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="fb816-109">Usługa DNS platformy Azure obsługuje importowania i eksportowania plików strefy za pomocą hello Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="fb816-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="fb816-110">Importowanie pliku strefy jest **nie** obecnie obsługiwane za pośrednictwem programu Azure PowerShell lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fb816-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="fb816-111">Hello Azure CLI 1.0 jest narzędziem wiersza polecenia i platform, używany do zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="fb816-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="fb816-112">Jest dostępna dla platformy systemu Windows, Mac i Linux z hello hello [Azure pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fb816-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="fb816-113">Obsługa platform jest ważne, aby importować i eksportować pliki stref, ponieważ hello najczęściej używane nazwy oprogramowanie serwera, [POWIĄZAĆ](https://www.isc.org/downloads/bind/), zwykle działa w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="fb816-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="fb816-114">Obecnie są dwie wersje hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fb816-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="fb816-115">CLI1.0 opiera się na Node.js i ma polecenia rozpoczynające się od "azure".</span><span class="sxs-lookup"><span data-stu-id="fb816-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="fb816-116">CLI2.0 jest oparty na języku Python i ma polecenia rozpoczynające się od "az".</span><span class="sxs-lookup"><span data-stu-id="fb816-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="fb816-117">Podczas importowania z pliku strefy jest obsługiwane w obu wersjach, zalecamy użycie poleceń CLI1.0 hello, zgodnie z opisem na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="fb816-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="fb816-118">Uzyskaj do istniejącego pliku strefy DNS</span><span class="sxs-lookup"><span data-stu-id="fb816-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="fb816-119">Przed zaimportowaniem pliku strefy DNS w usłudze Azure DNS należy tooobtain kopię pliku strefy hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="fb816-120">Hello źródłu tego pliku zależy od tego, gdzie jest obecnie hostowany hello strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="fb816-121">Jeśli strefy DNS jest hostowana przez partnera usługi (na przykład rejestratora domen, dedykowane dostawcy hostingu DNS lub dostawcy usług w chmurze alternatywne), czy usługa powinien dostarczyć toodownload możliwości hello hello pliku strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="fb816-122">Jeśli strefy DNS jest obsługiwana w systemie DNS systemu Windows, hello domyślny folder plików strefy hello jest **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="fb816-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="fb816-123">przedstawiono również plik strefy tooeach pełną ścieżkę Hello na powitania **ogólne** kartę hello konsolę DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="fb816-124">Jeżeli strefy DNS znajduje się za pomocą powiązania, hello lokalizację pliku strefy hello w każdej strefie jest określony w pliku konfiguracji powiązania hello **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="fb816-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="fb816-125">Strefy pliki pobierane z GoDaddy ma nieco niestandardowym formacie.</span><span class="sxs-lookup"><span data-stu-id="fb816-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="fb816-126">Należy toocorrect to przed zaimportowaniem plików tych stref w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="fb816-127">Nazwy DNS w hello RDATA każdy rekord DNS są określane jako w pełni kwalifikowane nazwy, ale nie mają kończącym "." Oznacza to, że są interpretowane przez inne systemy DNS jako nazw względnych.</span><span class="sxs-lookup"><span data-stu-id="fb816-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="fb816-128">Konieczne jest zakończenie hello tooedit hello strefy pliku tooappend "." tootheir nazwy, aby zaimportować je do usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="fb816-129">Na przykład hello rekord CNAME "www 3600 CNAME contoso.com" należy zmienić zbyt "www 3600 CNAME w contoso.com".</span><span class="sxs-lookup"><span data-stu-id="fb816-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="fb816-130">(z tokenem ".").</span><span class="sxs-lookup"><span data-stu-id="fb816-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="fb816-131">Importowanie pliku strefy DNS do usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="fb816-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="fb816-132">Importowanie pliku strefy tworzy nową strefę w usłudze Azure DNS, jeśli już nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="fb816-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="fb816-133">Jeśli istnieje już strefa hello, hello zestawów rekordów w pliku strefy hello muszą zostać połączone z zestawami rekordów istniejących hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="fb816-134">Scal zachowanie</span><span class="sxs-lookup"><span data-stu-id="fb816-134">Merge behavior</span></span>

* <span data-ttu-id="fb816-135">Domyślnie są scalane istniejących i nowych zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="fb816-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="fb816-136">Usuń zduplikowane są identyczne rekordy w zestawie rekordów scalone.</span><span class="sxs-lookup"><span data-stu-id="fb816-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="fb816-137">Alternatywnie, określając hello `--force` opcji, hello zastępuje procesu importowania istniejącego rekordu zestawy z nowego zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="fb816-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="fb816-138">Istniejące zestawy rekordów, które nie mają odpowiedni rekord w pliku strefy importowanych hello nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="fb816-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="fb816-139">W przypadku zestawów rekordów scalania, hello toolive (TTL) istniejących zestawów rekordów zostanie użyta godzina.</span><span class="sxs-lookup"><span data-stu-id="fb816-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="fb816-140">Gdy `--force` jest używana, hello TTL nowy zestaw rekordów hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="fb816-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="fb816-141">Początek parametry uwierzytelniania (SOA) (z wyjątkiem `host`) są zawsze pobierane z pliku strefy importowanych hello, niezależnie od tego, czy `--force` jest używany.</span><span class="sxs-lookup"><span data-stu-id="fb816-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="fb816-142">Podobnie dla hello na wierzchołku strefy hello rekord serwera nazw, hello TTL jest zawsze pobierana z hello importowanych stref pliku.</span><span class="sxs-lookup"><span data-stu-id="fb816-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="fb816-143">Importowany rekord CNAME nie zastępuje istniejący CNAME zarejestrować hello takie same nazwy, chyba że hello `--force` parametr jest określony.</span><span class="sxs-lookup"><span data-stu-id="fb816-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="fb816-144">Gdy wystąpi konflikt między rekord CNAME, a inny rekord hello takie same nazwy, ale o różnych wpisz (niezależnie od tego, który jest istniejących lub nowych), jest zachowywana hello istniejącego rekordu.</span><span class="sxs-lookup"><span data-stu-id="fb816-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="fb816-145">To jest niezależna od stosowania hello `--force`.</span><span class="sxs-lookup"><span data-stu-id="fb816-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="fb816-146">Dodatkowe informacje na temat importowania</span><span class="sxs-lookup"><span data-stu-id="fb816-146">Additional information about importing</span></span>

<span data-ttu-id="fb816-147">Witaj poniższe uwagi znajdują się dodatkowe informacje techniczne na temat strefy hello procesu importowania.</span><span class="sxs-lookup"><span data-stu-id="fb816-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="fb816-148">Witaj `$TTL` dyrektywa jest opcjonalna i jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="fb816-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="fb816-149">Gdy nie `$TTL` dyrektywy jest podane, są importowane rekordy bez jawnego TTL Ustaw domyślną tooa TTL 3600 sekund.</span><span class="sxs-lookup"><span data-stu-id="fb816-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="fb816-150">Gdy dwa rekordy w hello tego samego zestawu rekordów Określ inną TTLs, niższą wartość hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="fb816-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="fb816-151">Witaj `$ORIGIN` dyrektywa jest opcjonalna i jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="fb816-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="fb816-152">Gdy nie `$ORIGIN` ustawiono hello domyślna wartość używana jest nazwa strefy hello określonego w wierszu polecenia hello (oraz przerywanie hello ".").</span><span class="sxs-lookup"><span data-stu-id="fb816-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="fb816-153">Witaj `$INCLUDE` i `$GENERATE` dyrektywy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="fb816-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="fb816-154">Obsługiwane są następujące typy rekordów: A, AAAA, CNAME, MX, NS, SOA, SRV i TXT.</span><span class="sxs-lookup"><span data-stu-id="fb816-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="fb816-155">Hello rekord SOA jest tworzona automatycznie przez usługę Azure DNS, gdy tworzona jest strefa.</span><span class="sxs-lookup"><span data-stu-id="fb816-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="fb816-156">Podczas importowania pliku strefy, wszystkie parametry SOA są pobierane z pliku strefy hello *z wyjątkiem* hello `host` parametru.</span><span class="sxs-lookup"><span data-stu-id="fb816-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="fb816-157">Ten parametr używa hello wartości dostarczonej przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="fb816-158">Jest to spowodowane tego parametru musi odwoływać się toohello Nazwa podstawowego serwera dostarczane przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="fb816-159">rekord serwera nazw Hello na wierzchołku strefy hello jest również tworzone automatycznie przez usługę Azure DNS podczas tworzenia strefy hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="fb816-160">Tylko hello TTL tego zestawu rekordów jest importowany.</span><span class="sxs-lookup"><span data-stu-id="fb816-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="fb816-161">Te rekordy zawierają hello nazwy serwerów nazw udostępnionych przez usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="fb816-162">Witaj rejestrowania danych nie zostanie zastąpiona hello wartości zawartych w pliku strefy importowanych hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="fb816-163">W publicznej wersji zapoznawczej usługi DNS platformy Azure obsługuje tylko jeden ciąg rekordów TXT.</span><span class="sxs-lookup"><span data-stu-id="fb816-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="fb816-164">Wielociągu rekordów TXT są jest połączonych i obcięte too255 znaków.</span><span class="sxs-lookup"><span data-stu-id="fb816-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="fb816-165">Format interfejsu wiersza polecenia i wartości</span><span class="sxs-lookup"><span data-stu-id="fb816-165">CLI format and values</span></span>

<span data-ttu-id="fb816-166">format Hello tooimport polecenia interfejsu wiersza polecenia Azure hello strefę DNS jest:</span><span class="sxs-lookup"><span data-stu-id="fb816-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="fb816-167">Wartości:</span><span class="sxs-lookup"><span data-stu-id="fb816-167">Values:</span></span>

* <span data-ttu-id="fb816-168">`<resource group>`jest hello Nazwa grupy zasobów hello strefy hello w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="fb816-169">`<zone name>`jest nazwą hello hello strefy.</span><span class="sxs-lookup"><span data-stu-id="fb816-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="fb816-170">`<zone file name>`jest hello/nazwa ścieżki toobe pliku strefy hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="fb816-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="fb816-171">Jeśli strefa o tej nazwie nie istnieje w grupie zasobów hello, utworzono dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fb816-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="fb816-172">Jeśli hello strefy już istnieje, hello zestawy rekordów importowanych są scalane z istniejących zestawów rekordów.</span><span class="sxs-lookup"><span data-stu-id="fb816-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="fb816-173">toooverwrite hello istniejących zestawów rekordów, użyj hello `--force` opcji.</span><span class="sxs-lookup"><span data-stu-id="fb816-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="fb816-174">format hello tooverify pliku strefy bez faktycznie importowania, użyj hello `--parse-only` opcji.</span><span class="sxs-lookup"><span data-stu-id="fb816-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="fb816-175">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="fb816-175">Step 1.</span></span> <span data-ttu-id="fb816-176">Zaimportuj plik strefy</span><span class="sxs-lookup"><span data-stu-id="fb816-176">Import a zone file</span></span>

<span data-ttu-id="fb816-177">tooimport pliku strefy dla stref hello **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="fb816-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="fb816-178">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="fb816-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="fb816-179">Wybierz subskrypcję hello miejscu toocreate nowej strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="fb816-180">Usługa DNS platformy Azure jest usługą platformy Azure tylko do Menedżera zasobów, więc hello Azure CLI musi mieć tryb Manager tooResource wyłączone.</span><span class="sxs-lookup"><span data-stu-id="fb816-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="fb816-181">Przed użyciem hello usługa Azure DNS, należy zarejestrować dostawcę zasobów Microsoft.Network hello toouse subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fb816-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="fb816-182">(Jest to jednorazowa operacja dla każdej subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="fb816-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="fb816-183">Jeśli nie masz już, należy również toocreate Menedżera zasobów grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fb816-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="fb816-184">strefy hello tooimport **contoso.com** z pliku hello **contoso.com.txt** do nowej strefy DNS w grupie zasobów hello **myresourcegroup**, uruchom polecenie hello `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="fb816-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="fb816-185">To polecenie ładuje plik strefy hello i przeanalizować go.</span><span class="sxs-lookup"><span data-stu-id="fb816-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="fb816-186">polecenie Hello wykonuje szereg poleceń na powitania usługi Azure DNS usługi toocreate hello strefy i ustawia wszystkie hello rekordu w strefie hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="fb816-187">polecenie Hello zgłosi postęp w oknie konsoli hello, wraz z jakiekolwiek błędy i ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="fb816-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="fb816-188">Ponieważ zestawy rekordów są tworzone w serii, może upłynąć kilka minut tooimport pliku dużych strefy.</span><span class="sxs-lookup"><span data-stu-id="fb816-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="fb816-189">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="fb816-189">Step 2.</span></span> <span data-ttu-id="fb816-190">Sprawdź hello strefy</span><span class="sxs-lookup"><span data-stu-id="fb816-190">Verify hello zone</span></span>

<span data-ttu-id="fb816-191">tooverify hello strefy DNS po zaimportowaniu plików hello, można użyć jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="fb816-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="fb816-192">Można wyświetlić listę rekordów hello za pomocą następującego polecenia wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="fb816-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="fb816-193">Wyświetl listę rekordów hello za pomocą polecenia cmdlet programu PowerShell hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="fb816-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="fb816-194">Można użyć `nslookup` tooverify rozpoznawania nazw dla hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="fb816-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="fb816-195">Ponieważ hello strefy nie jest jeszcze delegowana, wystarczy toospecify hello poprawne serwerów nazw usługi Azure DNS jawnie.</span><span class="sxs-lookup"><span data-stu-id="fb816-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="fb816-196">Witaj poniższy przykład przedstawia sposób tooretrieve hello nazw serwerów nazw przypisanych toohello strefy.</span><span class="sxs-lookup"><span data-stu-id="fb816-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="fb816-197">IT przedstawiono również sposób zarejestrować tooquery hello "www" za pomocą `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="fb816-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="fb816-198">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="fb816-198">Step 3.</span></span> <span data-ttu-id="fb816-199">Zaktualizuj Delegowanie DNS</span><span class="sxs-lookup"><span data-stu-id="fb816-199">Update DNS delegation</span></span>

<span data-ttu-id="fb816-200">Po upewnieniu się, że strefa hello zostały zaimportowane prawidłowo, należy tooupdate hello DNS delegowania toopoint toohello serwerów nazw usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="fb816-201">Aby uzyskać więcej informacji, zobacz artykuł hello [zaktualizowania delegowania DNS hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="fb816-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="fb816-202">Eksportowanie pliku strefy DNS z usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="fb816-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="fb816-203">format Hello tooimport polecenia interfejsu wiersza polecenia Azure hello strefę DNS jest:</span><span class="sxs-lookup"><span data-stu-id="fb816-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="fb816-204">Wartości:</span><span class="sxs-lookup"><span data-stu-id="fb816-204">Values:</span></span>

* <span data-ttu-id="fb816-205">`<resource group>`jest hello Nazwa grupy zasobów hello strefy hello w usłudze Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="fb816-206">`<zone name>`jest nazwą hello hello strefy.</span><span class="sxs-lookup"><span data-stu-id="fb816-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="fb816-207">`<zone file name>`jest hello/nazwa ścieżki toobe pliku strefy hello wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="fb816-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="fb816-208">Hello strefy importowania, potrzebne są najpierw toosign w, wybierz subskrypcję i skonfiguruj tryb usługi Resource Manager toouse interfejsu wiersza polecenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fb816-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="fb816-209">tooexport pliku strefy</span><span class="sxs-lookup"><span data-stu-id="fb816-209">tooexport a zone file</span></span>

1. <span data-ttu-id="fb816-210">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fb816-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="fb816-211">Wybierz subskrypcję hello miejscu toocreate strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="fb816-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="fb816-212">Usługa DNS platformy Azure jest usługą platformy Azure tylko do Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="fb816-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="fb816-213">Hello Azure CLI musi być wyłączone tooResource menedżera trybu.</span><span class="sxs-lookup"><span data-stu-id="fb816-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="fb816-214">istniejąca strefa DNS platformy Azure hello tooexport **contoso.com** w grupie zasobów **myresourcegroup** pliku toohello **contoso.com.txt** (w hello bieżącym folderze), uruchom `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="fb816-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="fb816-215">Tego polecenia, które wywołuje hello tooenumerate usługi Azure DNS zestawów rekordów w strefie hello i eksportowanie pliku strefy hello wyniki tooa POWIĄZANIE zgodne.</span><span class="sxs-lookup"><span data-stu-id="fb816-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
