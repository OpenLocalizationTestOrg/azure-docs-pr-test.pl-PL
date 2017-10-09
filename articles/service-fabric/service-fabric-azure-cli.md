---
title: "wprowadzenie do usługi Azure Service Fabric interfejsu wiersza polecenia XPlat aaaGetting"
description: "Wprowadzenie do korzystania z usługi Azure Service Fabric interfejsu wiersza polecenia XPlat"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="44a57-103">Przy użyciu interfejsu wiersza polecenia XPlat toointeract hello z klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="44a57-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="44a57-104">Zakłócają klastra sieci szkieletowej usług z maszyn z systemem Linux przy użyciu interfejsu wiersza polecenia XPlat hello w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="44a57-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="44a57-105">pierwszym krokiem Hello jest pobrać najnowszą wersję hello hello interfejsu wiersza polecenia z hello git rep i zestaw hello go w ścieżce za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a57-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="44a57-106">Dla każdego polecenia obsługuje, można wpisać nazwę hello hello polecenia tooobtain hello pomocy dla tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="44a57-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="44a57-107">Automatyczne uzupełnianie jest obsługiwane w przypadku hello poleceń.</span><span class="sxs-lookup"><span data-stu-id="44a57-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="44a57-108">Na przykład powitania po pomocy dla poleceń aplikacji hello oferuje polecenia.</span><span class="sxs-lookup"><span data-stu-id="44a57-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="44a57-109">Hello pomocy tooa danego polecenia, można dodatkowo filtrować jako powitania po przykładzie:</span><span class="sxs-lookup"><span data-stu-id="44a57-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="44a57-110">tooenable automatycznego uzupełniania w hello interfejsu wiersza polecenia, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="44a57-111">Hello następujących poleceń połączyć toohello klastra i Pokaż hello węzłów w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="44a57-112">toouse nazwanych parametrów i Znajdź, jakie są, można wpisać — pomoc po użyciu polecenia.</span><span class="sxs-lookup"><span data-stu-id="44a57-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="44a57-113">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="44a57-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="44a57-114">Podczas łączenia tooa obsługi wielu komputerów klastra na komputerze **oznacza to nie jest częścią klastra hello**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="44a57-115">Zamień hello PublicIPorFQDN tag hello rzeczywistych adres IP lub nazwa FQDN zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="44a57-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="44a57-116">Podczas łączenia tooa obsługi wielu komputerów klastra na komputerze **będącego częścią klastra hello**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="44a57-117">Można użyć programu PowerShell lub interfejsu wiersza polecenia toointeract z klastra sieci szkieletowej usług z systemem Linux został utworzony za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="44a57-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="44a57-118">Tych klastrów nie są bezpieczne, w związku z tym może być otwierasz się jeden — okno przez dodanie hello publicznego adresu IP w manifeście klastra hello.</span><span class="sxs-lookup"><span data-stu-id="44a57-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="44a57-119">Przy użyciu hello klastra sieci szkieletowej usług tooa tooconnect interfejsu wiersza polecenia XPlat</span><span class="sxs-lookup"><span data-stu-id="44a57-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="44a57-120">Witaj następującego polecenia wiersza polecenia platformy Azure opisano, jak tooconnect tooa zabezpieczyć klastra.</span><span class="sxs-lookup"><span data-stu-id="44a57-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="44a57-121">Szczegóły certyfikatu Hello zgodny z certyfikatem w węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="44a57-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="44a57-122">Jeśli certyfikat ma urzędy certyfikacji (CA), należy tooadd hello — urzędu certyfikacji certyfikatu ścieżki parametru jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="44a57-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="44a57-123">Jeśli masz wiele urzędów certyfikacji, należy użyć przecinka jako ogranicznik hello.</span><span class="sxs-lookup"><span data-stu-id="44a57-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="44a57-124">Jeśli Twoje nazwa pospolita certyfikatu hello jest niezgodny z punktu końcowego połączenia hello, można użyć parametru hello `--strict-ssl-false` toobypass hello weryfikacji, jak pokazano w hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44a57-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="44a57-125">Jeśli chcesz tooskip weryfikacji hello urzędu certyfikacji, można dodać hello — Odrzuć — Dostęp nieautoryzowany — wartość false parametru pokazane na powitania następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44a57-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="44a57-126">Po nawiązaniu połączenia, powinno być możliwe toorun innych toointeract polecenia interfejsu wiersza polecenia z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="44a57-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="44a57-127">Wdrażanie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="44a57-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="44a57-128">Wykonaj następujące polecenia toocopy, zarejestrować i uruchomić aplikacji sieci szkieletowej usług hello hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="44a57-129">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="44a57-129">Upgrading your application</span></span>

<span data-ttu-id="44a57-130">proces Hello jest podobne toohello [procesu w systemie Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="44a57-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="44a57-131">Tworzenie, skopiuj zarejestrować i utworzyć aplikację z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="44a57-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="44a57-132">Jeśli wystąpienie aplikacji ma nazwę `fabric:/MySFApp`i typ hello jest MySFApp, hello poleceń będzie następujące:</span><span class="sxs-lookup"><span data-stu-id="44a57-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="44a57-133">Należy hello zmienić tooyour aplikację i skompiluj ponownie usługi hello zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="44a57-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="44a57-134">Aktualizacja hello zmodyfikowane w pliku manifestu usługi (ServiceManifest.xml) hello zaktualizowane wersje na powitania usługi (i kodu lub konfiguracji lub danych, zależnie od potrzeb).</span><span class="sxs-lookup"><span data-stu-id="44a57-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="44a57-135">Również zmodyfikować manifest aplikacji hello (ApplicationManifest.xml) za pomocą hello zaktualizować numer wersji aplikacji hello i hello modyfikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="44a57-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="44a57-136">Teraz skopiuj i zarejestruj zaktualizowaną aplikację za pomocą hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a57-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="44a57-137">Teraz można rozpocząć uaktualniania aplikacji hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44a57-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="44a57-138">Teraz można monitorować przy użyciu SFX uaktualniania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="44a57-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="44a57-139">W ciągu kilku minut aplikacji hello czy zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="44a57-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="44a57-140">Można również skorzystać z aplikacji zaktualizowane z powodu błędu i sprawdzić funkcję wycofywania automatycznie hello w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="44a57-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="44a57-141">Konwertowanie z PFX tooPEM i na odwrót</span><span class="sxs-lookup"><span data-stu-id="44a57-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="44a57-142">Tooinstall certyfikat może być konieczne w klastrach bezpiecznego tooaccess komputera lokalnego (z systemem Windows lub Linux), które mogą być w innym środowisku.</span><span class="sxs-lookup"><span data-stu-id="44a57-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="44a57-143">Na przykład podczas uzyskiwania dostępu do zabezpieczonych klaster systemu Linux na komputerze z systemem Windows i na odwrót może być konieczne tooconvert certyfikatu PFX tooPEM i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="44a57-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="44a57-144">tooconvert z pliku PFX tooa pliku PEM o hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a57-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="44a57-145">tooconvert z pliku tooa PEM pliku PFX, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a57-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="44a57-146">Odwołuje się zbyt[dokumentacji biblioteki OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="44a57-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="44a57-147">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="44a57-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="44a57-148">Kopiowanie pakietu aplikacji hello nie powiedzie się</span><span class="sxs-lookup"><span data-stu-id="44a57-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="44a57-149">Sprawdź, czy `openssh` jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="44a57-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="44a57-150">Domyślnie Ubuntu pulpitu nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="44a57-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="44a57-151">Zainstaluj za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="44a57-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="44a57-152">Jeśli hello problem będzie nadal występował, spróbuj wyłączyć PAM dla ssh, zmieniając hello `sshd_config` plik przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="44a57-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="44a57-153">Jeśli hello problem będzie nadal występować, spróbuj rosnący numer hello ssh sesji, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="44a57-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="44a57-154">Przy użyciu kluczy ssh uwierzytelniania (w przeciwieństwie toopasswords) nie jest jeszcze obsługiwana (ponieważ platformy hello używa ssh pakiety toocopy), dlatego zamiast tego Użyj uwierzytelniania hasła.</span><span class="sxs-lookup"><span data-stu-id="44a57-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44a57-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44a57-155">Next steps</span></span>

[<span data-ttu-id="44a57-156">Konfigurowanie środowiska deweloperskiego hello i wdrożyć klaster sieci szkieletowej usług aplikacji tooa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="44a57-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="44a57-157">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="44a57-157">Related articles</span></span>

* <span data-ttu-id="44a57-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="44a57-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
