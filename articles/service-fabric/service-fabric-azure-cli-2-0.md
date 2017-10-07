---
title: "wprowadzenie do usługi Azure Service Fabric i Azure CLI 2.0 aaaGet"
description: "Dowiedz się, jak toouse hello Azure Service Fabric polecenia moduł w Azure CLI w wersji 2.0. Dowiedz się, jak tooconnect tooa klastra i w jaki sposób toomanage aplikacji."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="6002f-104">Usługa Azure Service Fabric i interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6002f-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="6002f-105">Witaj narzędzia wiersza polecenia platformy Azure (Azure CLI) w wersji 2.0 obejmuje toohelp polecenia Zarządzanie klastrami usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="6002f-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="6002f-106">Dowiedz się, jak tooget pracę z wiersza polecenia platformy Azure i sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6002f-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="6002f-107">Instalowanie interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6002f-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="6002f-108">Można użyć toointeract poleceń Azure CLI 2.0 z i zarządzania klastrami usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="6002f-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="6002f-109">tooget hello najnowszą wersję interfejsu wiersza polecenia Azure, wykonaj hello [Azure CLI 2.0 standardowego procesu instalacji](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6002f-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6002f-110">Aby uzyskać więcej informacji, zobacz hello [omówienie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6002f-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="6002f-111">Składnia interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6002f-111">Azure CLI syntax</span></span>

<span data-ttu-id="6002f-112">W interfejsie wiersza polecenia platformy Azure wszystkie polecenia usługi Service Fabric mają prefiks `az sf`.</span><span class="sxs-lookup"><span data-stu-id="6002f-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="6002f-113">Aby uzyskać ogólne informacje o poleceniach hello można użyć, należy użyć `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="6002f-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="6002f-114">Aby uzyskać pomoc dotyczącą pojedynczego polecenia, użyj polecenia `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="6002f-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="6002f-115">Polecenia usługi Service Fabric w interfejsie wiersza polecenia platformy Azure są zgodne z następującym wzorcem nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="6002f-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="6002f-116">`<object>`element docelowy hello dla `<action>`.</span><span class="sxs-lookup"><span data-stu-id="6002f-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="6002f-117">Wybieranie klastra</span><span class="sxs-lookup"><span data-stu-id="6002f-117">Select a cluster</span></span>

<span data-ttu-id="6002f-118">Przed wykonaniem jakichkolwiek operacji, należy wybrać tooconnect klastra, aby.</span><span class="sxs-lookup"><span data-stu-id="6002f-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="6002f-119">Na przykład zobacz hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="6002f-119">For an example, see hello following code.</span></span> <span data-ttu-id="6002f-120">Kod Hello łączy tooan niezabezpieczona klastra.</span><span class="sxs-lookup"><span data-stu-id="6002f-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="6002f-121">Nie używaj niezabezpieczonych klastrów usługi Service Fabric w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="6002f-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="6002f-122">Witaj punktu końcowego klastra musi być poprzedzony `http` lub `https`.</span><span class="sxs-lookup"><span data-stu-id="6002f-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="6002f-123">Musi on zawierać portu hello hello HTTP bramy.</span><span class="sxs-lookup"><span data-stu-id="6002f-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="6002f-124">adres i Hello port są hello taka sama, jak hello adres URL Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="6002f-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="6002f-125">W przypadku klastrów zabezpieczonych za pomocą certyfikatu można użyć niezaszyfrowanych plików PEM albo plików CRT i KEY.</span><span class="sxs-lookup"><span data-stu-id="6002f-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="6002f-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6002f-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="6002f-127">Aby uzyskać więcej informacji, zobacz [bezpiecznego klastra sieci szkieletowej usług Azure Connect tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6002f-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6002f-128">Witaj `select` polecenia nie działają na wszystkie żądania przed zwróceniem.</span><span class="sxs-lookup"><span data-stu-id="6002f-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="6002f-129">tooverify, że klaster został podany poprawnie, należy użyć wiersza polecenia, takich jak `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="6002f-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="6002f-130">Upewnij się, że polecenie hello nie zwraca żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="6002f-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="6002f-131">Operacje podstawowe</span><span class="sxs-lookup"><span data-stu-id="6002f-131">Basic operations</span></span>

<span data-ttu-id="6002f-132">Informacje o połączeniu klastra są utrwalane w wielu sesjach interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6002f-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="6002f-133">Po wybraniu klastra sieci szkieletowej usług można uruchomić w klastrze hello dowolne polecenie sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="6002f-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="6002f-134">Na przykład hello tooget stan kondycji klastra usługi sieć szkieletowa, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6002f-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="6002f-135">polecenie Hello wyniki hello następujących danych wyjściowych (przy założeniu, że dane wyjściowe JSON jest określona w konfiguracji interfejsu wiersza polecenia Azure hello):</span><span class="sxs-lookup"><span data-stu-id="6002f-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="6002f-136">Porady i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="6002f-136">Tips and troubleshooting</span></span>

<span data-ttu-id="6002f-137">Może się okazać hello następujące informacje przydatne, jeśli wystąpiły problemy podczas używania poleceń usługi Service Fabric w wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6002f-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="6002f-138">Konwertuj certyfikatu z formatu tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="6002f-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="6002f-139">Interfejs wiersza polecenia platformy Azure obsługuje certyfikaty po stronie klienta w postaci plików PEM (rozszerzenie pem).</span><span class="sxs-lookup"><span data-stu-id="6002f-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="6002f-140">Jeśli używasz pliki PFX z systemu Windows, należy przekonwertować format tooPEM tych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="6002f-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="6002f-141">tooconvert pliku PEM tooa pliku PFX, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6002f-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="6002f-142">Aby uzyskać więcej informacji, zobacz hello [dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="6002f-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="6002f-143">Problemy z połączeniem</span><span class="sxs-lookup"><span data-stu-id="6002f-143">Connection issues</span></span>

<span data-ttu-id="6002f-144">Niektóre operacje może generować następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="6002f-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="6002f-145">Sprawdź, czy określona hello tego punktu końcowego klastra jest dostępny i nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="6002f-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="6002f-146">Sprawdź także, że powitalne interfejsu użytkownika Eksploratora sieci szkieletowej usług jest dostępna na hosta i portu.</span><span class="sxs-lookup"><span data-stu-id="6002f-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="6002f-147">punkt końcowy z hello tooupdate, użyj `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="6002f-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="6002f-148">Szczegółowe dzienniki</span><span class="sxs-lookup"><span data-stu-id="6002f-148">Detailed logs</span></span>

<span data-ttu-id="6002f-149">Szczegółowe dzienniki często bywają przydatne w przypadku debugowania lub zgłaszania problemu.</span><span class="sxs-lookup"><span data-stu-id="6002f-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="6002f-150">Interfejs wiersza polecenia platformy Azure oferuje globalnym `--debug` flagi, które zwiększa poziom szczegółowości hello plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="6002f-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="6002f-151">Polecenia — pomoc i składnia</span><span class="sxs-lookup"><span data-stu-id="6002f-151">Command help and syntax</span></span>

<span data-ttu-id="6002f-152">Wykonaj polecenia usługi sieć szkieletowa hello tej samej Konwencji jako wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6002f-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="6002f-153">Aby uzyskać pomoc dotyczącą określonego polecenia lub grupy poleceń, użyj hello `-h` flagi:</span><span class="sxs-lookup"><span data-stu-id="6002f-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="6002f-154">Oto inny przykład:</span><span class="sxs-lookup"><span data-stu-id="6002f-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
