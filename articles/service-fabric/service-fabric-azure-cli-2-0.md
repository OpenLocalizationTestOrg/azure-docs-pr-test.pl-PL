---
title: "Wprowadzenie do usługi Azure Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0"
description: "Dowiedz się, jak korzystać z modułu poleceń usługi Azure Service Fabric w interfejsie wiersza polecenia platformy Azure w wersji 2.0. Dowiedz się, jak nawiązać połączenie z klastrem i zarządzać aplikacjami."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="d2bb1-104">Usługa Azure Service Fabric i interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d2bb1-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="d2bb1-105">Narzędzie wiersza polecenia platformy Azure w wersji 2.0 zawiera polecenia, które ułatwiają zarządzanie klastrami usługi Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="d2bb1-106">Dowiedz się, jak rozpocząć pracę z interfejsem wiersza polecenia platformy Azure i usługą Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="d2bb1-107">Instalowanie interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d2bb1-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="d2bb1-108">Polecenia interfejsu wiersza polecenia platformy Azure 2.0 umożliwiają interakcję z klastrami usługi Service Fabric oraz zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="d2bb1-109">Aby uzyskać najnowszą wersję interfejsu wiersza polecenia platformy Azure, wykonaj kroki [standardowego procesu instalacji interfejsu wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d2bb1-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="d2bb1-110">Aby uzyskać więcej informacji, zobacz temat [Omówienie interfejsu wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2bb1-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="d2bb1-111">Składnia interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d2bb1-111">Azure CLI syntax</span></span>

<span data-ttu-id="d2bb1-112">W interfejsie wiersza polecenia platformy Azure wszystkie polecenia usługi Service Fabric mają prefiks `az sf`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="d2bb1-113">Aby uzyskać ogólne informacje na temat używanych poleceń, z których możesz korzystać, użyj polecenia `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="d2bb1-114">Aby uzyskać pomoc dotyczącą pojedynczego polecenia, użyj polecenia `az sf <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="d2bb1-115">Polecenia usługi Service Fabric w interfejsie wiersza polecenia platformy Azure są zgodne z następującym wzorcem nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="d2bb1-116">Element `<object>` jest obiektem docelowym elementu `<action>`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="d2bb1-117">Wybieranie klastra</span><span class="sxs-lookup"><span data-stu-id="d2bb1-117">Select a cluster</span></span>

<span data-ttu-id="d2bb1-118">Przed wykonaniem jakiejkolwiek operacji musisz wybrać klaster, z którym chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="d2bb1-119">Jako przykład zobacz następujący kod.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-119">For an example, see the following code.</span></span> <span data-ttu-id="d2bb1-120">Kod umożliwia nawiązanie połączenia z niezabezpieczonym klastrem.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="d2bb1-121">Nie używaj niezabezpieczonych klastrów usługi Service Fabric w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="d2bb1-122">Punkt końcowy klastra musi mieć prefiks `http` lub `https`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="d2bb1-123">Musi on zawierać port bramy HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="d2bb1-124">Port i adres są takie same jak adres URL programu Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="d2bb1-125">W przypadku klastrów zabezpieczonych za pomocą certyfikatu można użyć niezaszyfrowanych plików PEM albo plików CRT i KEY.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="d2bb1-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="d2bb1-127">Aby uzyskać więcej informacji, zobacz temat [Nawiązywanie połączenia z zabezpieczonym klastrem usługi Azure Service Fabric](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d2bb1-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d2bb1-128">Przed zwróceniem wartości polecenie `select` nie reaguje na żadne żądania.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="d2bb1-129">Aby sprawdzić, czy klaster został określony poprawnie, użyj polecenia, takiego jak `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="d2bb1-130">Upewnij się, że polecenie nie zwraca żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="d2bb1-131">Operacje podstawowe</span><span class="sxs-lookup"><span data-stu-id="d2bb1-131">Basic operations</span></span>

<span data-ttu-id="d2bb1-132">Informacje o połączeniu klastra są utrwalane w wielu sesjach interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="d2bb1-133">Po wybraniu klastra usługi Service Fabric można uruchomić dowolne polecenie usługi Service Fabric w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="d2bb1-134">Aby na przykład uzyskać informacje o kondycji klastra usługi Service Fabric, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="d2bb1-135">Polecenie zwróci następujące dane wyjściowe (przy założeniu, że dane wyjściowe JSON zostały określone w konfiguracji interfejsu wiersza polecenia platformy Azure):</span><span class="sxs-lookup"><span data-stu-id="d2bb1-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="d2bb1-136">Porady i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d2bb1-136">Tips and troubleshooting</span></span>

<span data-ttu-id="d2bb1-137">Poniższe informacje mogą być pomocne, jeśli wystąpiły problemy podczas korzystania z poleceń usługi Service Fabric w interfejsie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="d2bb1-138">Konwertowanie certyfikatu z formatu PFX na PEM</span><span class="sxs-lookup"><span data-stu-id="d2bb1-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="d2bb1-139">Interfejs wiersza polecenia platformy Azure obsługuje certyfikaty po stronie klienta w postaci plików PEM (rozszerzenie pem).</span><span class="sxs-lookup"><span data-stu-id="d2bb1-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="d2bb1-140">Jeśli używasz plików PFX z systemu Windows, musisz konwertować te certyfikaty na format PEM.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="d2bb1-141">Aby konwertować plik PFX na plik PEM, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="d2bb1-142">Aby uzyskać więcej informacji, zapoznaj się z [dokumentacją dotyczącą protokołu OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="d2bb1-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="d2bb1-143">Problemy z połączeniem</span><span class="sxs-lookup"><span data-stu-id="d2bb1-143">Connection issues</span></span>

<span data-ttu-id="d2bb1-144">Niektóre operacje mogą generować następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="d2bb1-145">Sprawdź, czy punkt końcowy określonego klastra jest dostępny i przeprowadza nasłuchiwanie.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="d2bb1-146">Sprawdź również, czy interfejs użytkownika programu Service Fabric Explorer jest dostępny na tym hoście i porcie.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="d2bb1-147">Aby zaktualizować punkt końcowy, użyj polecenia `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="d2bb1-148">Szczegółowe dzienniki</span><span class="sxs-lookup"><span data-stu-id="d2bb1-148">Detailed logs</span></span>

<span data-ttu-id="d2bb1-149">Szczegółowe dzienniki często bywają przydatne w przypadku debugowania lub zgłaszania problemu.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="d2bb1-150">Interfejs wiersza polecenia platformy Azure zawiera globalną flagę `--debug`, która zwiększa poziom szczegółowości plików dzienników.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="d2bb1-151">Polecenia — pomoc i składnia</span><span class="sxs-lookup"><span data-stu-id="d2bb1-151">Command help and syntax</span></span>

<span data-ttu-id="d2bb1-152">Polecenia usługi Service Fabric korzystają z tej samej konwencji, co interfejs wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2bb1-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="d2bb1-153">Aby uzyskać pomoc dotyczącą określonego polecenia lub grupy poleceń, użyj flagi `-h`:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="d2bb1-154">Oto inny przykład:</span><span class="sxs-lookup"><span data-stu-id="d2bb1-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
