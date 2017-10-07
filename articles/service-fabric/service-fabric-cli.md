---
title: "wprowadzenie do usługi Azure Service Fabric interfejsu wiersza polecenia (sfctl) aaaGet"
description: "Dowiedz się, jak toouse hello interfejsu wiersza polecenia Azure Service Fabric. Dowiedz się, jak tooconnect tooa klastra i w jaki sposób toomanage aplikacji."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="cdda1-104">Wiersz polecenia usługi Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cdda1-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="cdda1-105">Hello Azure Service Fabric interfejsu wiersza polecenia (sfctl) jest narzędziem wiersza polecenia interakcji i zarządzania nimi jednostki sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="cdda1-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="cdda1-106">Interfejs sfctl może być używany z klastrami systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="cdda1-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="cdda1-107">Interfejs sfctl działa na dowolnej platformie, która obsługuje język Python.</span><span class="sxs-lookup"><span data-stu-id="cdda1-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdda1-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cdda1-108">Prerequisites</span></span>

<span data-ttu-id="cdda1-109">Wcześniejsze tooinstallation, upewnij się, że w środowisku ma python oraz narzędzia pip zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="cdda1-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="cdda1-110">Aby uzyskać więcej informacji, zapoznaj się hello [narzędzia pip dokumentacji szybkiego startu](https://pip.pypa.io/en/latest/quickstart/)i oficjalna [python zainstalować dokumentację](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="cdda1-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="cdda1-111">Obsługiwane są zarówno python 2.7 i 3,6, zalecane jest python toouse 3,6.</span><span class="sxs-lookup"><span data-stu-id="cdda1-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="cdda1-112">Instalowanie</span><span class="sxs-lookup"><span data-stu-id="cdda1-112">Install</span></span>

<span data-ttu-id="cdda1-113">Hello Azure Service Fabric interfejsu wiersza polecenia (sfctl) jest dostarczana jako pakiet języka python.</span><span class="sxs-lookup"><span data-stu-id="cdda1-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="cdda1-114">tooinstall hello najnowszej wersji Uruchom:</span><span class="sxs-lookup"><span data-stu-id="cdda1-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="cdda1-115">Po zakończeniu instalacji, uruchom `sfctl -h` tooget informacji o dostępnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="cdda1-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="cdda1-116">Składnia interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="cdda1-116">CLI syntax</span></span>

<span data-ttu-id="cdda1-117">Polecenia mają zawsze prefiks `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="cdda1-118">Aby uzyskać ogólne informacje na temat wszystkich poleceń, z których możesz korzystać, użyj polecenia `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="cdda1-119">Aby uzyskać pomoc dotyczącą pojedynczego polecenia, użyj polecenia `sfctl <command> -h`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="cdda1-120">Wykonaj polecenia powtarzalne struktury, z docelowym hello hello polecenia poprzedniego zlecenie hello lub akcji:</span><span class="sxs-lookup"><span data-stu-id="cdda1-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="cdda1-121">W tym przykładzie `<object>` jest hello celu `<action>`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="cdda1-122">Wybieranie klastra</span><span class="sxs-lookup"><span data-stu-id="cdda1-122">Select a cluster</span></span>

<span data-ttu-id="cdda1-123">Przed wykonaniem jakichkolwiek operacji, należy wybrać tooconnect klastra, aby.</span><span class="sxs-lookup"><span data-stu-id="cdda1-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="cdda1-124">Na przykład uruchom powitania po tooselect i połącz toohello klastra o nazwie hello `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="cdda1-125">Nie używaj niezabezpieczonych klastrów usługi Service Fabric w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="cdda1-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="cdda1-126">Witaj punktu końcowego klastra musi być poprzedzony `http` lub `https`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="cdda1-127">Musi on zawierać portu hello hello HTTP bramy.</span><span class="sxs-lookup"><span data-stu-id="cdda1-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="cdda1-128">adres i Hello port są hello taka sama, jak hello adres URL Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="cdda1-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="cdda1-129">W przypadku klastrów zabezpieczonych certyfikatem możesz określić certyfikat zakodowany w formacie PEM.</span><span class="sxs-lookup"><span data-stu-id="cdda1-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="cdda1-130">certyfikat Hello można określić jako pojedynczy plik lub certyfikat i parę kluczy.</span><span class="sxs-lookup"><span data-stu-id="cdda1-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="cdda1-131">Aby uzyskać więcej informacji, zobacz [bezpiecznego klastra sieci szkieletowej usług Azure Connect tooa](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cdda1-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="cdda1-132">Operacje podstawowe</span><span class="sxs-lookup"><span data-stu-id="cdda1-132">Basic operations</span></span>

<span data-ttu-id="cdda1-133">Informacje o połączeniu z klastrem są utrwalane między sesjami interfejsu sfctl.</span><span class="sxs-lookup"><span data-stu-id="cdda1-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="cdda1-134">Po wybraniu klastra sieci szkieletowej usług można uruchomić w klastrze hello dowolne polecenie sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="cdda1-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="cdda1-135">Na przykład hello tooget stan kondycji klastra usługi sieć szkieletowa, użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cdda1-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="cdda1-136">polecenie Hello wyniki hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="cdda1-136">hello command results in hello following output:</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="cdda1-137">Porady i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="cdda1-137">Tips and troubleshooting</span></span>

<span data-ttu-id="cdda1-138">Kilka sugestii i porad dotyczących rozwiązywania typowych problemów.</span><span class="sxs-lookup"><span data-stu-id="cdda1-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="cdda1-139">Konwertuj certyfikatu z formatu tooPEM PFX</span><span class="sxs-lookup"><span data-stu-id="cdda1-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="cdda1-140">Hello interfejsu wiersza polecenia usługi sieć szkieletowa obsługuje certyfikaty klienta jako pliki PEM (rozszerzenie PEM).</span><span class="sxs-lookup"><span data-stu-id="cdda1-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="cdda1-141">Jeśli używasz pliki PFX z systemu Windows, należy przekonwertować format tooPEM tych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="cdda1-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="cdda1-142">tooconvert pliku PEM tooa pliku PFX, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="cdda1-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="cdda1-143">Aby uzyskać więcej informacji, zobacz hello [dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="cdda1-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="cdda1-144">Problemy z połączeniem</span><span class="sxs-lookup"><span data-stu-id="cdda1-144">Connection issues</span></span>

<span data-ttu-id="cdda1-145">Niektóre operacje może generować następujące wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="cdda1-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="cdda1-146">Sprawdź, czy określona hello tego punktu końcowego klastra jest dostępny i nasłuchuje.</span><span class="sxs-lookup"><span data-stu-id="cdda1-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="cdda1-147">Sprawdź także, że powitalne interfejsu użytkownika Eksploratora sieci szkieletowej usług jest dostępna na hosta i portu.</span><span class="sxs-lookup"><span data-stu-id="cdda1-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="cdda1-148">punkt końcowy z hello tooupdate, użyj `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="cdda1-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="cdda1-149">Szczegółowe dzienniki</span><span class="sxs-lookup"><span data-stu-id="cdda1-149">Detailed logs</span></span>

<span data-ttu-id="cdda1-150">Szczegółowe dzienniki często bywają przydatne w przypadku debugowania lub zgłaszania problemu.</span><span class="sxs-lookup"><span data-stu-id="cdda1-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="cdda1-151">Brak globalnym `--debug` flagi, które zwiększa poziom szczegółowości hello plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="cdda1-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="cdda1-152">Polecenia — pomoc i składnia</span><span class="sxs-lookup"><span data-stu-id="cdda1-152">Command help and syntax</span></span>

<span data-ttu-id="cdda1-153">Aby uzyskać pomoc dotyczącą określonego polecenia lub grupy poleceń, użyj hello `-h` flagi:</span><span class="sxs-lookup"><span data-stu-id="cdda1-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="cdda1-154">Inny przykład:</span><span class="sxs-lookup"><span data-stu-id="cdda1-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="cdda1-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdda1-155">Next steps</span></span>

* [<span data-ttu-id="cdda1-156">Wdrażanie aplikacji przy użyciu interfejsu wiersza polecenia Azure Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="cdda1-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="cdda1-157">Wprowadzenie do usługi Service Fabric w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="cdda1-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
