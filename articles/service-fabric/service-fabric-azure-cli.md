---
title: "Wprowadzenie do korzystania z usługi Azure Service Fabric interfejsu wiersza polecenia XPlat"
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a><span data-ttu-id="8ddba-103">Przy użyciu wiersza polecenia XPlat wchodzić w interakcje z klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8ddba-103">Using the XPlat CLI to interact with a Service Fabric cluster</span></span>

<span data-ttu-id="8ddba-104">Zakłócają klastra sieci szkieletowej usług z maszyn z systemem Linux przy użyciu wiersza polecenia XPlat w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="8ddba-104">You can interact with Service Fabric cluster from Linux machines using the XPlat CLI on Linux.</span></span>

<span data-ttu-id="8ddba-105">Pierwszym krokiem jest Pobierz najnowszą wersję interfejsu wiersza polecenia z git rep i skonfigurować ją w ścieżce przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="8ddba-105">The first step is get the latest version of the CLI from the git rep and set it up in your path using the following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="8ddba-106">Dla każdego polecenia obsługuje, można wpisać nazwę polecenia, aby uzyskać pomoc dotyczącą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="8ddba-106">For each command, it supports, you can type the name of the command to obtain the help for that command.</span></span>
<span data-ttu-id="8ddba-107">Automatyczne uzupełnianie jest obsługiwana dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="8ddba-107">Auto-completion is supported for the commands.</span></span> <span data-ttu-id="8ddba-108">Na przykład następujące polecenie zapewnia pomoc dla poleceń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ddba-108">For example, the following command gives you help for all the application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="8ddba-109">Można dokładniej przefiltrować ułatwiają danego polecenia, jak przedstawiono na poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8ddba-109">You can further filter the help to a specific command, as the following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="8ddba-110">Aby włączyć automatyczne uzupełnianie w interfejsu wiersza polecenia, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-110">To enable auto-completion in the CLI, run the following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="8ddba-111">Poniższe polecenia, połącz się z klastrem i wyświetlić węzły w klastrze:</span><span class="sxs-lookup"><span data-stu-id="8ddba-111">The following commands connect to the cluster and show you the nodes in the cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="8ddba-112">Parametry nazwane i Znajdź, jakie są, możesz wpisać — pomoc po użyciu polecenia.</span><span class="sxs-lookup"><span data-stu-id="8ddba-112">To use named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="8ddba-113">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="8ddba-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="8ddba-114">Podczas nawiązywania połączenia z maszyną klastrze z wieloma maszynami **oznacza to nie jest częścią klastra**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-114">When connecting to a multi-machine cluster from a machine **that is not part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="8ddba-115">Zamień PublicIPorFQDN tag rzeczywistych adres IP lub nazwa FQDN zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="8ddba-115">Replace the PublicIPorFQDN tag with the real IP or FQDN as appropriate.</span></span> <span data-ttu-id="8ddba-116">Podczas nawiązywania połączenia z maszyną klastrze z wieloma maszynami **będącego częścią klastra**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-116">When connecting to a multi-machine cluster from a machine **that is part of the cluster**, use the following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="8ddba-117">Możesz użyć programu PowerShell lub interfejsu wiersza polecenia do interakcji z klastra sieci szkieletowej usług z systemem Linux został utworzony za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ddba-117">You can use PowerShell or CLI to interact with your Linux Service Fabric Cluster created through the Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="8ddba-118">Tych klastrów nie są bezpieczne, w związku z tym można może być otwarcia jednego — okno przez dodanie publicznego adresu IP w manifeście klastra.</span><span class="sxs-lookup"><span data-stu-id="8ddba-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding the public IP address in the cluster manifest.</span></span>

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a><span data-ttu-id="8ddba-119">Przy użyciu wiersza polecenia XPlat do nawiązania połączenia klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8ddba-119">Using the XPlat CLI to connect to a Service Fabric cluster</span></span>

<span data-ttu-id="8ddba-120">Następujące polecenia interfejsu wiersza polecenia Azure opisują sposób podłączania do bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="8ddba-120">The following Azure CLI commands describe how to connect to a secure cluster.</span></span> <span data-ttu-id="8ddba-121">Szczegóły certyfikatu musi odpowiadać certyfikatu w węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="8ddba-121">The certificate details must match a certificate on the cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="8ddba-122">Jeśli certyfikat ma urzędy certyfikacji (CA), należy dodać parametr — urzędu certyfikacji certyfikatu ścieżki, jak w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8ddba-122">If your certificate has Certificate Authorities (CAs), you need to add the --ca-cert-path parameter like the following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="8ddba-123">Jeśli masz wiele urzędów certyfikacji, należy użyć przecinka jako ogranicznik.</span><span class="sxs-lookup"><span data-stu-id="8ddba-123">If you have multiple CAs, use a comma as the delimiter.</span></span>

<span data-ttu-id="8ddba-124">Jeśli Twoje nazwa pospolita w certyfikacie nie odpowiada punktu końcowego połączenia, można użyć parametru `--strict-ssl-false` do pominięcia weryfikacji, jak pokazano w poniższym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="8ddba-124">If your Common Name in the certificate does not match the connection endpoint, you could use the parameter `--strict-ssl-false` to bypass the verification as shown in the following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="8ddba-125">Jeśli chcesz pominąć weryfikacji urzędu certyfikacji, można dodać parametr Odrzuć — Dostęp nieautoryzowany — wartość false, jak pokazano w poniższym poleceniu:</span><span class="sxs-lookup"><span data-stu-id="8ddba-125">If you would like to skip the CA verification, you could add the --reject-unauthorized-false parameter as shown in the following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="8ddba-126">Po nawiązaniu połączenia można innych poleceń interfejsu wiersza polecenia w celu wchodzenia w interakcje z klastrem.</span><span class="sxs-lookup"><span data-stu-id="8ddba-126">After you connect, you should be able to run other CLI commands to interact with the cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="8ddba-127">Wdrażanie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8ddba-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="8ddba-128">Wykonaj następujące polecenia, aby skopiować, zarejestrować i uruchomić aplikacji sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="8ddba-128">Execute the following commands to copy, register, and start the service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="8ddba-129">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="8ddba-129">Upgrading your application</span></span>

<span data-ttu-id="8ddba-130">Proces jest podobny do [procesu w systemie Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="8ddba-130">The process is similar to the [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="8ddba-131">Tworzenie, skopiuj zarejestrować i utworzyć aplikację z katalogu głównego projektu.</span><span class="sxs-lookup"><span data-stu-id="8ddba-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="8ddba-132">Jeśli wystąpienie aplikacji ma nazwę `fabric:/MySFApp`, a typ to MySFApp, polecenia zostaną wyświetlone następujące:</span><span class="sxs-lookup"><span data-stu-id="8ddba-132">If your application instance is named `fabric:/MySFApp`, and the type is MySFApp, the commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="8ddba-133">Wprowadź zmiany w aplikacji i skompiluj ponownie zmodyfikowaną usługę.</span><span class="sxs-lookup"><span data-stu-id="8ddba-133">Make the change to your application and rebuild the modified service.</span></span>  <span data-ttu-id="8ddba-134">Zaktualizuj usługę zmodyfikowanego pliku manifestu (ServiceManifest.xml) z zaktualizowane wersje usługi (i kodu ani konfiguracji lub danych, zależnie od potrzeb).</span><span class="sxs-lookup"><span data-stu-id="8ddba-134">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="8ddba-135">Numer zaktualizowaną wersję aplikacji i modyfikacji usługi również zmodyfikować manifest aplikacji (pliku ApplicationManifest.xml).</span><span class="sxs-lookup"><span data-stu-id="8ddba-135">Also modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application, and the modified service.</span></span>  <span data-ttu-id="8ddba-136">Teraz skopiuj i zarejestruj zaktualizowaną aplikację za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="8ddba-136">Now, copy and register your updated application using the following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="8ddba-137">Teraz można rozpocząć uaktualniania aplikacji przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-137">Now, you can start the application upgrade with the following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="8ddba-138">Teraz można monitorować przy użyciu SFX uaktualnienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ddba-138">You can now monitor the application upgrade using SFX.</span></span> <span data-ttu-id="8ddba-139">W ciągu kilku minut aplikacja zostanie zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="8ddba-139">In a few minutes, the application would have been updated.</span></span> <span data-ttu-id="8ddba-140">Można również skorzystać z aplikacji zaktualizowane z powodu błędu i sprawdzić funkcji automatycznego wycofania w sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="8ddba-140">You can also try an updated app with an error and check the auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a><span data-ttu-id="8ddba-141">Konwertowanie z PFX PEM i na odwrót</span><span class="sxs-lookup"><span data-stu-id="8ddba-141">Converting from PFX to PEM and vice versa</span></span>

<span data-ttu-id="8ddba-142">Może być konieczne do bezpiecznych klastrów, które mogą być w innym środowisku należy zainstalować certyfikat w komputerze lokalnym (z systemem Windows lub Linux).</span><span class="sxs-lookup"><span data-stu-id="8ddba-142">You might need to install a certificate in your local machine (with Windows or Linux) to access secure clusters that may be in a different environment.</span></span> <span data-ttu-id="8ddba-143">Na przykład podczas uzyskiwania dostępu do zabezpieczonych klaster systemu Linux na komputerze z systemem Windows i na odwrót może być konieczne konwertowanie certyfikatu PFX do PEM i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="8ddba-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need to convert your certificate from PFX to PEM and vice versa.</span></span> 

<span data-ttu-id="8ddba-144">Aby dokonać konwersji pliku PEM, do pliku PFX, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-144">To convert from a PEM file to a PFX file, use the following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="8ddba-145">Aby przekonwertować plik PFX na plik PEM, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-145">To convert from a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="8ddba-146">Aby uzyskać szczegółowe informacje, zapoznaj się z [dokumentacją rozwiązania OpenSSL](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html).</span><span class="sxs-lookup"><span data-stu-id="8ddba-146">Refer to [OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="8ddba-147">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="8ddba-147">Troubleshooting</span></span>


### <a name="copying-of-the-application-package-does-not-succeed"></a><span data-ttu-id="8ddba-148">Kopiowanie pakietu aplikacji nie powiedzie się</span><span class="sxs-lookup"><span data-stu-id="8ddba-148">Copying of the application package does not succeed</span></span>

<span data-ttu-id="8ddba-149">Sprawdź, czy `openssh` jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="8ddba-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="8ddba-150">Domyślnie Ubuntu pulpitu nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="8ddba-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="8ddba-151">Zainstaluj za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-151">Install it using the following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="8ddba-152">Jeśli problem będzie się powtarzał, spróbuj wyłączyć PAM dla ssh, zmieniając `sshd_config` plik za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="8ddba-152">If the problem persists, try disabling PAM for ssh by changing the `sshd_config` file using the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="8ddba-153">Jeśli problem będzie nadal występować, spróbuj zwiększyć liczbę ssh sesji, wykonując następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="8ddba-153">If the problem still persists, try increasing the number of ssh sessions by executing the following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="8ddba-154">Przy użyciu kluczy dla ssh uwierzytelniania (w przeciwieństwie do hasła) nie jest jeszcze obsługiwana (ponieważ platformy używa ssh można kopiować pakiety), dlatego zamiast tego Użyj uwierzytelniania hasła.</span><span class="sxs-lookup"><span data-stu-id="8ddba-154">Using keys for ssh authentication (as opposed to passwords) isn't yet supported (since the platform uses ssh to copy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ddba-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ddba-155">Next steps</span></span>

[<span data-ttu-id="8ddba-156">Konfigurowanie środowiska projektowego i wdrażanie aplikacji sieci szkieletowej usług do klastra z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="8ddba-156">Set up the development environment and deploy a Service Fabric application to a Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="8ddba-157">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="8ddba-157">Related articles</span></span>

* <span data-ttu-id="8ddba-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md) (Wprowadzenie do usługi Service Fabric i interfejsu wiersza polecenia platformy Azure 2.0)</span><span class="sxs-lookup"><span data-stu-id="8ddba-158">[Getting started with Service Fabric and Azure CLI 2.0](service-fabric-azure-cli-2-0.md)</span></span>
