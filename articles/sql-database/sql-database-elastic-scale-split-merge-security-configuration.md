---
title: "Konfiguracja zabezpieczeń scalania aaaSplit | Dokumentacja firmy Microsoft"
description: Konfigurowanie x409 certyfikaty szyfrowania
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="d5aec-103">Konfiguracja zabezpieczeń scalania podziału</span><span class="sxs-lookup"><span data-stu-id="d5aec-103">Split-merge security configuration</span></span>
<span data-ttu-id="d5aec-104">toouse hello podziału/Merge usługi, należy poprawnie skonfigurować zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d5aec-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="d5aec-105">Usługa Hello jest częścią hello funkcji elastycznego skalowania bazy danych SQL Azure firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d5aec-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="d5aec-106">Aby uzyskać więcej informacji, zobacz [elastycznej podziału skali i scal samouczek usługi](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="d5aec-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="d5aec-107">Konfigurowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-107">Configuring certificates</span></span>
<span data-ttu-id="d5aec-108">Certyfikaty są skonfigurowane na dwa sposoby.</span><span class="sxs-lookup"><span data-stu-id="d5aec-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="d5aec-109">Witaj tooConfigure certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="d5aec-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="d5aec-110">tooConfigure certyfikaty klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="d5aec-111">Certyfikaty tooobtain</span><span class="sxs-lookup"><span data-stu-id="d5aec-111">tooobtain certificates</span></span>
<span data-ttu-id="d5aec-112">Certyfikaty można uzyskać z publicznych urzędów certyfikacji (CA) lub hello [usługi certyfikatów systemu Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5aec-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="d5aec-113">Są to hello preferowanych metod tooobtain certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="d5aec-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="d5aec-114">Jeśli te opcje nie są dostępne, można wygenerować **certyfikaty z podpisem własnym**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="d5aec-115">Narzędzia toogenerate certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="d5aec-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="d5aec-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="d5aec-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="d5aec-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="d5aec-118">narzędzia hello toorun</span><span class="sxs-lookup"><span data-stu-id="d5aec-118">toorun hello tools</span></span>
* <span data-ttu-id="d5aec-119">Z wiersz polecenia dla deweloperów programu Visual Studio, zobacz [wiersz polecenia programu Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="d5aec-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="d5aec-120">Jeśli zainstalowany, przejdź do:</span><span class="sxs-lookup"><span data-stu-id="d5aec-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="d5aec-121">Pobierz hello WDK z [Windows 8.1: Pobieranie zestawów i narzędzi](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="d5aec-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="d5aec-122">certyfikat SSL hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d5aec-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="d5aec-123">Certyfikat SSL jest wymagany tooencrypt hello komunikacji i uwierzytelniania serwera hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="d5aec-124">Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:</span><span class="sxs-lookup"><span data-stu-id="d5aec-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="d5aec-125">Utwórz nowy certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="d5aec-126">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="d5aec-127">Utwórz plik PFX dla certyfikatu SSL z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="d5aec-128">Przekaż certyfikat SSL tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="d5aec-129">Aktualizuj certyfikat SSL w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="d5aec-130">Urząd certyfikacji SSL importu</span><span class="sxs-lookup"><span data-stu-id="d5aec-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="d5aec-131">przechowywanie istniejącego certyfikatu z certyfikatu hello toouse</span><span class="sxs-lookup"><span data-stu-id="d5aec-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="d5aec-132">Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="d5aec-133">Przekaż certyfikat SSL tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="d5aec-134">Aktualizuj certyfikat SSL w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="d5aec-135">toouse istniejącego certyfikatu w pliku PFX</span><span class="sxs-lookup"><span data-stu-id="d5aec-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="d5aec-136">Przekaż certyfikat SSL tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="d5aec-137">Aktualizuj certyfikat SSL w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="d5aec-138">certyfikaty klienta tooconfigure</span><span class="sxs-lookup"><span data-stu-id="d5aec-138">tooconfigure client certificates</span></span>
<span data-ttu-id="d5aec-139">Certyfikaty klienta są wymagane w kolejności tooauthenticate żądań toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="d5aec-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="d5aec-140">Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:</span><span class="sxs-lookup"><span data-stu-id="d5aec-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="d5aec-141">Wyłącz certyfikaty klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="d5aec-142">Wyłącz uwierzytelnianie oparte na certyfikatach</span><span class="sxs-lookup"><span data-stu-id="d5aec-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="d5aec-143">Wydać nowe certyfikaty klienta z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="d5aec-144">Tworzenie urzędu certyfikacji z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="d5aec-145">Przekaż certyfikat urzędu certyfikacji tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="d5aec-146">Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="d5aec-147">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="d5aec-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="d5aec-148">Tworzenie plików PFX certyfikatów klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="d5aec-149">Importowanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="d5aec-150">Skopiuj odciski palców certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="d5aec-151">Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="d5aec-152">Użyj istniejących certyfikatów klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="d5aec-153">Znajdowanie klucza publicznego urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="d5aec-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="d5aec-154">Przekaż certyfikat urzędu certyfikacji tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="d5aec-155">Aktualizuj certyfikat urzędu certyfikacji w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="d5aec-156">Skopiuj odciski palców certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="d5aec-157">Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="d5aec-158">Skonfiguruj sprawdzanie odwołania certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="d5aec-159">Dozwolonych adresów IP</span><span class="sxs-lookup"><span data-stu-id="d5aec-159">Allowed IP addresses</span></span>
<span data-ttu-id="d5aec-160">Punkty końcowe usługi toohello dostępu może być ograniczony toospecific zakresów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d5aec-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="d5aec-161">szyfrowanie tooconfigure hello magazynu</span><span class="sxs-lookup"><span data-stu-id="d5aec-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="d5aec-162">Certyfikat jest wymagany tooencrypt hello poświadczenia, które są przechowywane w magazynie metadanych hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="d5aec-163">Wybierz hello najbardziej odpowiednią hello trzech scenariuszy poniżej, a wykonywanie wszystkich jej kroków:</span><span class="sxs-lookup"><span data-stu-id="d5aec-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="d5aec-164">Użyj nowego certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="d5aec-165">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="d5aec-166">Tworzenie pliku PFX certyfikatu szyfrowania z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="d5aec-167">Przekaż certyfikat szyfrowania tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="d5aec-168">Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="d5aec-169">Użyj istniejącego certyfikatu z magazynu certyfikatów hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="d5aec-170">Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="d5aec-171">Przekaż certyfikat szyfrowania tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="d5aec-172">Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="d5aec-173">Użyj istniejącego certyfikatu w pliku PFX</span><span class="sxs-lookup"><span data-stu-id="d5aec-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="d5aec-174">Przekaż certyfikat szyfrowania tooCloud usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="d5aec-175">Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="d5aec-176">Witaj domyślnej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d5aec-176">hello default configuration</span></span>
<span data-ttu-id="d5aec-177">Hello domyślnej konfiguracji odrzuca wszystkie punkt końcowy HTTP toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="d5aec-178">Jest to hello zalecane ustawienia, ponieważ punkty końcowe toothese żądań hello może posiadać poufne informacje, takie jak poświadczenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d5aec-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="d5aec-179">Konfiguracja domyślna Hello zezwala wszystkich punkt końcowy HTTPS toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="d5aec-180">To ustawienie może być ograniczony dalej.</span><span class="sxs-lookup"><span data-stu-id="d5aec-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="d5aec-181">Zmiana hello konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d5aec-181">Changing hello Configuration</span></span>
<span data-ttu-id="d5aec-182">Witaj grupy regułami kontroli dostępu stosowane tooand punktu końcowego są konfigurowane w hello  **<EndpointAcls>**  części hello **pliku konfiguracji usługi**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="d5aec-183">reguły Hello w grupie kontroli dostępu są skonfigurowane w <AccessControl name=""> sekcji pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="d5aec-184">Hello format opisanej w dokumentacji list kontroli dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="d5aec-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="d5aec-185">Na przykład tooallow tylko adresy IP w zakresie 100.100.0.0 hello too100.100.255.255 hello tooaccess HTTPS punkt końcowy, reguły hello będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d5aec-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="d5aec-186">Odmowa usługi zapobiegania</span><span class="sxs-lookup"><span data-stu-id="d5aec-186">Denial of service prevention</span></span>
<span data-ttu-id="d5aec-187">Istnieją dwa różne mechanizmy obsługiwane toodetect i zapobieganie atakom "odmowa usługi":</span><span class="sxs-lookup"><span data-stu-id="d5aec-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="d5aec-188">Ogranicz liczbę równoczesnych żądań na hosta zdalnego (domyślnie wyłączone)</span><span class="sxs-lookup"><span data-stu-id="d5aec-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="d5aec-189">Ogranicz szybkość dostępu do jednego hosta zdalnego (na domyślne)</span><span class="sxs-lookup"><span data-stu-id="d5aec-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="d5aec-190">Są one oparte na funkcji hello opisano w dynamicznej zabezpieczeń IP w programie IIS.</span><span class="sxs-lookup"><span data-stu-id="d5aec-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="d5aec-191">Jeśli zmiana tej konfiguracji należy wziąć pod hello następujące czynniki:</span><span class="sxs-lookup"><span data-stu-id="d5aec-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="d5aec-192">zachowanie Hello urządzeń translatora adresów sieciowych za pośrednictwem hello informacji hosta zdalnego i serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="d5aec-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="d5aec-193">Każdy zasób tooany żądania w roli sieci web hello jest uznawany za (np. ładowanie skryptów, obrazy, itp.)</span><span class="sxs-lookup"><span data-stu-id="d5aec-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="d5aec-194">Ograniczenie liczby równoczesnych dostępów</span><span class="sxs-lookup"><span data-stu-id="d5aec-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="d5aec-195">dostępne są następujące ustawienia Hello, które skonfigurowania tego zachowania:</span><span class="sxs-lookup"><span data-stu-id="d5aec-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="d5aec-196">Zmień DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable tę ochronę.</span><span class="sxs-lookup"><span data-stu-id="d5aec-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="d5aec-197">Ograniczanie szybkość dostępu</span><span class="sxs-lookup"><span data-stu-id="d5aec-197">Restricting rate of access</span></span>
<span data-ttu-id="d5aec-198">dostępne są następujące ustawienia Hello, które skonfigurowania tego zachowania:</span><span class="sxs-lookup"><span data-stu-id="d5aec-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="d5aec-199">Konfigurowanie tooa odpowiedzi hello odrzucił żądanie</span><span class="sxs-lookup"><span data-stu-id="d5aec-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="d5aec-200">Witaj następujące ustawienie konfiguruje tooa odpowiedzi hello odrzucił żądanie:</span><span class="sxs-lookup"><span data-stu-id="d5aec-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="d5aec-201">Zapoznaj się z toohello dokumentacją dla dynamicznych zabezpieczeń protokołu IP w usługach IIS dla innych obsługiwanych wartości.</span><span class="sxs-lookup"><span data-stu-id="d5aec-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="d5aec-202">Operacje dotyczące konfigurowania certyfikatów usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="d5aec-203">Ten temat dotyczy tylko w celach informacyjnych.</span><span class="sxs-lookup"><span data-stu-id="d5aec-203">This topic is for reference only.</span></span> <span data-ttu-id="d5aec-204">Wykonaj kroki konfiguracji hello opisane w temacie:</span><span class="sxs-lookup"><span data-stu-id="d5aec-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="d5aec-205">Konfigurowanie certyfikatu SSL hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="d5aec-206">Skonfiguruj certyfikaty klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d5aec-207">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-207">Create a self-signed certificate</span></span>
<span data-ttu-id="d5aec-208">Wykonaj:</span><span class="sxs-lookup"><span data-stu-id="d5aec-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="d5aec-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="d5aec-209">toocustomize:</span></span>

* <span data-ttu-id="d5aec-210">-n z hello adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="d5aec-210">-n with hello service URL.</span></span> <span data-ttu-id="d5aec-211">Symbole wieloznaczne ("CN = * .cloudapp .net") i alternatywnych nazw ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d5aec-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="d5aec-212">-e z datą wygaśnięcia certyfikatu hello Utwórz silne hasło i określ go po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="d5aec-213">Utwórz plik PFX dla certyfikatu SSL z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="d5aec-214">Wykonaj:</span><span class="sxs-lookup"><span data-stu-id="d5aec-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="d5aec-215">Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="d5aec-216">Tak, Eksportuj klucz prywatny hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-216">Yes, export hello private key</span></span>
* <span data-ttu-id="d5aec-217">Eksportuj wszystkie właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d5aec-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="d5aec-218">Wyeksportuj certyfikat protokołu SSL z magazynu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="d5aec-219">Znajdowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-219">Find certificate</span></span>
* <span data-ttu-id="d5aec-220">Kliknij przycisk Akcje -> Wszystkie zadania -> Export...</span><span class="sxs-lookup"><span data-stu-id="d5aec-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="d5aec-221">Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="d5aec-222">Tak, Eksportuj klucz prywatny hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="d5aec-223">Jeśli to możliwe, Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello * Wyeksportuj wszystkie rozszerzone właściwości</span><span class="sxs-lookup"><span data-stu-id="d5aec-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="d5aec-224">Przekaż usługi toocloud certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="d5aec-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="d5aec-225">Przekaż certyfikat z hello istniejące lub wygenerować. Plik PFX o hello pary kluczy SSL:</span><span class="sxs-lookup"><span data-stu-id="d5aec-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="d5aec-226">Wprowadź hasło hello ochrona powitalnych informacji o kluczu prywatnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="d5aec-227">Aktualizuj certyfikat SSL w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="d5aec-228">Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:</span><span class="sxs-lookup"><span data-stu-id="d5aec-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="d5aec-229">Urząd certyfikacji SSL importu</span><span class="sxs-lookup"><span data-stu-id="d5aec-229">Import SSL certification authority</span></span>
<span data-ttu-id="d5aec-230">Wykonaj następujące kroki w wszystkie konta/maszyny, które będą komunikować się z usługą hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="d5aec-231">Kliknij dwukrotnie hello. Plik CER w Eksploratorze Windows</span><span class="sxs-lookup"><span data-stu-id="d5aec-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="d5aec-232">W oknie dialogowym certyfikat hello kliknij przycisk Zainstaluj certyfikat...</span><span class="sxs-lookup"><span data-stu-id="d5aec-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="d5aec-233">Zaimportuj certyfikat w magazynie zaufanych głównych urzędów certyfikacji powitalne</span><span class="sxs-lookup"><span data-stu-id="d5aec-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="d5aec-234">Wyłącz uwierzytelnianie oparte na certyfikatach</span><span class="sxs-lookup"><span data-stu-id="d5aec-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="d5aec-235">Obsługiwane jest tylko uwierzytelnianie oparte na certyfikatach klienta i wyłączenie go spowoduje umożliwiają punktów końcowych usługi toohello dostępu publicznego, innych mechanizmów znajdują się w miejscu (np. Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="d5aec-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="d5aec-236">Zmienić te ustawienia toofalse w funkcji hello tooturn plików w konfiguracji usługi hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="d5aec-237">Następnie skopiuj hello certyfikatu w tym samym odciskiem palca jako hello SSL w ustawieniu certyfikatu hello urzędu certyfikacji:</span><span class="sxs-lookup"><span data-stu-id="d5aec-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="d5aec-238">Tworzenie urzędu certyfikacji z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="d5aec-239">Wykonaj hello następujące kroki toocreate tooact certyfikatu z podpisem własnym, jako urząd certyfikacji:</span><span class="sxs-lookup"><span data-stu-id="d5aec-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="d5aec-240">toocustomize go</span><span class="sxs-lookup"><span data-stu-id="d5aec-240">toocustomize it</span></span>

* <span data-ttu-id="d5aec-241">-e z datą wygaśnięcia certyfikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="d5aec-242">Znajdowanie klucza publicznego urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="d5aec-242">Find CA public key</span></span>
<span data-ttu-id="d5aec-243">Wszystkie certyfikaty klienta musi został wystawiony przez urząd certyfikacji zaufany przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="d5aec-244">Znajdź hello toohello klucza publicznego urzędu certyfikacji, który wystawił certyfikaty klienta hello, które mają toobe używany do uwierzytelniania w kolejności tooupload on toohello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d5aec-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="d5aec-245">Jeśli plik hello kluczem publicznym hello jest niedostępny, eksportować go z magazynu certyfikatów hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="d5aec-246">Znajdowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-246">Find certificate</span></span>
  * <span data-ttu-id="d5aec-247">Wyszukaj certyfikat klienta wystawiony przez hello tego samego urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="d5aec-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="d5aec-248">Kliknij dwukrotnie certyfikat hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="d5aec-249">Wybierz kartę ścieżki certyfikacji hello w oknie dialogowym certyfikat hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="d5aec-250">Kliknij dwukrotnie wpis urzędu certyfikacji hello w ścieżce hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="d5aec-251">Zanotować hello właściwości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="d5aec-252">Zamknij hello **certyfikatu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d5aec-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="d5aec-253">Znajdowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-253">Find certificate</span></span>
  * <span data-ttu-id="d5aec-254">Wyszukiwanie hello opisanymi powyżej urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="d5aec-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="d5aec-255">Kliknij przycisk Akcje -> Wszystkie zadania -> Export...</span><span class="sxs-lookup"><span data-stu-id="d5aec-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="d5aec-256">Wyeksportuj certyfikat do. CER z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="d5aec-257">**Nie eksportuj klucza prywatnego hello**</span><span class="sxs-lookup"><span data-stu-id="d5aec-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="d5aec-258">Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello Jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="d5aec-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="d5aec-259">Eksportuj wszystkie właściwości rozszerzone.</span><span class="sxs-lookup"><span data-stu-id="d5aec-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="d5aec-260">Przekaż usługi toocloud certyfikatu urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="d5aec-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="d5aec-261">Przekaż certyfikat z hello istniejące lub wygenerować. Plik CER kluczem publicznym hello urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="d5aec-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="d5aec-262">Certyfikat urzędu certyfikacji aktualizacji w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="d5aec-263">Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:</span><span class="sxs-lookup"><span data-stu-id="d5aec-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="d5aec-264">Zaktualizuj wartość hello hello następujące ustawienie hello sam odcisk palca:</span><span class="sxs-lookup"><span data-stu-id="d5aec-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="d5aec-265">Certyfikaty</span><span class="sxs-lookup"><span data-stu-id="d5aec-265">Issue client certificates</span></span>
<span data-ttu-id="d5aec-266">Każda usługa hello poszczególnych tooaccess autoryzowanych powinien mieć klienta certyfikat wystawiony dla his/hers wyłącznego użycia i należy wybrać, czy his/hers właścicielem tooprotect silne hasło jego klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="d5aec-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="d5aec-267">Witaj, wykonaj czynności należy wykonać w hello na tym samym komputerze, na którym hello certyfikat z podpisem własnym urzędu certyfikacji został wygenerowany i przechowywane:</span><span class="sxs-lookup"><span data-stu-id="d5aec-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="d5aec-268">Dostosowywanie:</span><span class="sxs-lookup"><span data-stu-id="d5aec-268">Customizing:</span></span>

* <span data-ttu-id="d5aec-269">n - o identyfikatorze klienta toohello będą uwierzytelniane z tym certyfikatem</span><span class="sxs-lookup"><span data-stu-id="d5aec-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="d5aec-270">-e z datą wygaśnięcia certyfikatu hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="d5aec-271">MyID.pvk i MyID.cer z unikatowych nazw plików dla tego certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="d5aec-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="d5aec-272">To polecenie wyświetli monit o podanie toobe hasło utworzone, a następnie użyty raz.</span><span class="sxs-lookup"><span data-stu-id="d5aec-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="d5aec-273">Należy używać silnych haseł.</span><span class="sxs-lookup"><span data-stu-id="d5aec-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="d5aec-274">Tworzenie plików PFX dla klienta certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="d5aec-275">Dla każdego certyfikatu wygenerowanego klienta należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="d5aec-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="d5aec-276">Dostosowywanie:</span><span class="sxs-lookup"><span data-stu-id="d5aec-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="d5aec-277">Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="d5aec-278">Tak, Eksportuj klucz prywatny hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-278">Yes, export hello private key</span></span>
* <span data-ttu-id="d5aec-279">Eksportuj wszystkie właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d5aec-279">Export all extended properties</span></span>
* <span data-ttu-id="d5aec-280">toowhom poszczególnych Hello, które ten certyfikat jest wystawiane należy wybrać hello hasło eksportu</span><span class="sxs-lookup"><span data-stu-id="d5aec-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="d5aec-281">Importowanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-281">Import client certificate</span></span>
<span data-ttu-id="d5aec-282">Każda osoba, dla którego został wystawiony certyfikat klienta należy importować pary kluczy hello na maszynach hello on użyje toocommunicate z usługą hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="d5aec-283">Kliknij dwukrotnie hello. Plik PFX w Eksploratorze Windows</span><span class="sxs-lookup"><span data-stu-id="d5aec-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="d5aec-284">Zaimportuj certyfikat do hello Magazyn osobisty z co najmniej tej opcji:</span><span class="sxs-lookup"><span data-stu-id="d5aec-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="d5aec-285">Dołącz wszystkie właściwości rozszerzone zaznaczone</span><span class="sxs-lookup"><span data-stu-id="d5aec-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="d5aec-286">Skopiuj odciski palców certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="d5aec-287">Każda osoba, dla którego został wystawiony certyfikat klienta, należy wykonać następujące kroki w kolejności tooobtain hello odcisk palca his/hers certyfikatu, który zostanie dodany plik konfiguracji usługi toohello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="d5aec-288">Uruchom certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="d5aec-288">Run certmgr.exe</span></span>
* <span data-ttu-id="d5aec-289">Wybierz kartę osobistych powitalne</span><span class="sxs-lookup"><span data-stu-id="d5aec-289">Select hello Personal tab</span></span>
* <span data-ttu-id="d5aec-290">Kliknij dwukrotnie certyfikat klienta hello toobe używany do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="d5aec-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="d5aec-291">Hello certyfikat zostanie otwarte okno dialogowe Wybierz kartę szczegółów hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="d5aec-292">Upewnij się, że Pokaż są wyświetlane wszystkie</span><span class="sxs-lookup"><span data-stu-id="d5aec-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="d5aec-293">Wybierz hello pola o nazwie odcisk palca liście hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="d5aec-294">Kopiuj wartość hello odcisk palca hello ** usunąć niewidoczne znaków Unicode, przed pierwszą cyfrą hello ** usunięcia wszystkich spacji</span><span class="sxs-lookup"><span data-stu-id="d5aec-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="d5aec-295">Konfigurowanie klientów dozwolone w pliku konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="d5aec-296">Zaktualizuj wartość hello hello następujące ustawienia w pliku konfiguracji usługi hello rozdzielaną przecinkami listę hello odciski palców certyfikatów klienta hello dozwolone usługi toohello dostęp:</span><span class="sxs-lookup"><span data-stu-id="d5aec-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="d5aec-297">Skonfiguruj sprawdzanie odwołania certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="d5aec-298">ustawienie domyślne Hello nie skontaktuj się z hello urzędu certyfikacji dla stanu odwołania certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="d5aec-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="d5aec-299">tooturn na powitania sprawdza, czy hello urzędu certyfikacji, który wystawił certyfikaty klienta hello obsługuje kontrole, Zmień następujące ustawienia z jedną z wartości hello zdefiniowanych w hello wyliczenie X509RevocationMode hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="d5aec-300">Utwórz plik PFX certyfikatów z podpisem szyfrowania</span><span class="sxs-lookup"><span data-stu-id="d5aec-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="d5aec-301">Aby uzyskać certyfikat szyfrowania należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="d5aec-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="d5aec-302">Dostosowywanie:</span><span class="sxs-lookup"><span data-stu-id="d5aec-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="d5aec-303">Wprowadź hasło, a następnie wyeksportować certyfikat z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="d5aec-304">Tak, Eksportuj klucz prywatny hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-304">Yes, export hello private key</span></span>
* <span data-ttu-id="d5aec-305">Eksportuj wszystkie właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d5aec-305">Export all extended properties</span></span>
* <span data-ttu-id="d5aec-306">Konieczne będzie hello hasła podczas przekazywania hello usługi w chmurze toohello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="d5aec-307">Wyeksportuj certyfikat szyfrowania z magazynu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="d5aec-308">Znajdowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-308">Find certificate</span></span>
* <span data-ttu-id="d5aec-309">Kliknij przycisk Akcje -> Wszystkie zadania -> Export...</span><span class="sxs-lookup"><span data-stu-id="d5aec-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="d5aec-310">Wyeksportuj certyfikat do. Plik PFX z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="d5aec-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="d5aec-311">Tak, Eksportuj klucz prywatny hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="d5aec-312">Jeśli to możliwe, Dołącz wszystkie certyfikaty w ścieżce certyfikacji hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="d5aec-313">Eksportuj wszystkie właściwości rozszerzone</span><span class="sxs-lookup"><span data-stu-id="d5aec-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="d5aec-314">Przekaż usługi toocloud certyfikatu szyfrowania</span><span class="sxs-lookup"><span data-stu-id="d5aec-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="d5aec-315">Przekaż certyfikat z hello istniejące lub wygenerować. Plik PFX o pary kluczy szyfrowania hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="d5aec-316">Wprowadź hasło hello ochrona powitalnych informacji o kluczu prywatnym</span><span class="sxs-lookup"><span data-stu-id="d5aec-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="d5aec-317">Aktualizuj certyfikat szyfrowania w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5aec-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="d5aec-318">Zaktualizuj wartości odcisku palca hello hello następujące ustawienia w pliku konfiguracji usługi hello z odciskiem palca hello hello usługi w chmurze toohello przekazać certyfikat:</span><span class="sxs-lookup"><span data-stu-id="d5aec-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="d5aec-319">Typowe operacje certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d5aec-319">Common certificate operations</span></span>
* <span data-ttu-id="d5aec-320">Konfigurowanie certyfikatu SSL hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="d5aec-321">Skonfiguruj certyfikaty klienta</span><span class="sxs-lookup"><span data-stu-id="d5aec-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="d5aec-322">Znajdowanie certyfikatów</span><span class="sxs-lookup"><span data-stu-id="d5aec-322">Find certificate</span></span>
<span data-ttu-id="d5aec-323">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d5aec-323">Follow these steps:</span></span>

1. <span data-ttu-id="d5aec-324">Uruchom mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="d5aec-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="d5aec-325">Plik -> Dodaj/Usuń przystawkę...</span><span class="sxs-lookup"><span data-stu-id="d5aec-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="d5aec-326">Wybierz **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="d5aec-327">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-327">Click **Add**.</span></span>
5. <span data-ttu-id="d5aec-328">Wybierz lokalizację magazynu certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="d5aec-329">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-329">Click **Finish**.</span></span>
7. <span data-ttu-id="d5aec-330">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-330">Click **OK**.</span></span>
8. <span data-ttu-id="d5aec-331">Rozwiń węzeł **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="d5aec-332">Rozwiń węzeł magazynu certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="d5aec-333">Rozwiń węzeł podrzędny hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d5aec-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="d5aec-334">Wybierz certyfikat hello listy.</span><span class="sxs-lookup"><span data-stu-id="d5aec-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="d5aec-335">Eksportowanie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d5aec-335">Export certificate</span></span>
<span data-ttu-id="d5aec-336">W hello **Kreatora eksportu certyfikatów**:</span><span class="sxs-lookup"><span data-stu-id="d5aec-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="d5aec-337">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-337">Click **Next**.</span></span>
2. <span data-ttu-id="d5aec-338">Wybierz **tak**, następnie **klucza prywatnego hello eksportu**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="d5aec-339">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-339">Click **Next**.</span></span>
4. <span data-ttu-id="d5aec-340">Wybierz format pliku żądanego wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="d5aec-341">Witaj wyboru żądane opcje.</span><span class="sxs-lookup"><span data-stu-id="d5aec-341">Check hello desired options.</span></span>
6. <span data-ttu-id="d5aec-342">Sprawdź **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-342">Check **Password**.</span></span>
7. <span data-ttu-id="d5aec-343">Wpisz silne hasło i potwierdź je.</span><span class="sxs-lookup"><span data-stu-id="d5aec-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="d5aec-344">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-344">Click **Next**.</span></span>
9. <span data-ttu-id="d5aec-345">Wpisz lub wyszukaj nazwę pliku, gdzie toostore hello certyfikatu (Użyj. Rozszerzenie PFX).</span><span class="sxs-lookup"><span data-stu-id="d5aec-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="d5aec-346">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-346">Click **Next**.</span></span>
11. <span data-ttu-id="d5aec-347">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-347">Click **Finish**.</span></span>
12. <span data-ttu-id="d5aec-348">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="d5aec-349">Importowanie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d5aec-349">Import certificate</span></span>
<span data-ttu-id="d5aec-350">W Kreatorze importu certyfikatów hello:</span><span class="sxs-lookup"><span data-stu-id="d5aec-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="d5aec-351">Wybierz lokalizację magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="d5aec-352">Wybierz **bieżącego użytkownika** jeśli tylko procesów uruchomionych w obszarze bieżący użytkownik będą uzyskiwać dostęp do usługi hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="d5aec-353">Wybierz **komputera lokalnego** Jeśli inne procesy w tym komputerze będą uzyskiwać dostęp do usługi hello</span><span class="sxs-lookup"><span data-stu-id="d5aec-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="d5aec-354">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-354">Click **Next**.</span></span>
3. <span data-ttu-id="d5aec-355">W przypadku importowania z pliku Potwierdź hello ścieżkę pliku.</span><span class="sxs-lookup"><span data-stu-id="d5aec-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="d5aec-356">Jeśli import. Plik PFX:</span><span class="sxs-lookup"><span data-stu-id="d5aec-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="d5aec-357">Wprowadź hasło hello ochrona powitalnych klucza prywatnego</span><span class="sxs-lookup"><span data-stu-id="d5aec-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="d5aec-358">Wybierz opcje importowania</span><span class="sxs-lookup"><span data-stu-id="d5aec-358">Select import options</span></span>
5. <span data-ttu-id="d5aec-359">Wybierz certyfikaty "W miejscu" hello po magazynu</span><span class="sxs-lookup"><span data-stu-id="d5aec-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="d5aec-360">Kliknij pozycję **Browse (Przeglądaj)**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-360">Click **Browse**.</span></span>
7. <span data-ttu-id="d5aec-361">Wybierz żądaną magazyn hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-361">Select hello desired store.</span></span>
8. <span data-ttu-id="d5aec-362">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="d5aec-363">Jeśli wybrano hello magazynu zaufanego głównego urzędu certyfikacji, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="d5aec-364">Kliknij przycisk **OK** na wszystkie okna dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d5aec-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="d5aec-365">Przekazywanie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d5aec-365">Upload certificate</span></span>
<span data-ttu-id="d5aec-366">W hello [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="d5aec-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="d5aec-367">Wybierz **usługi w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="d5aec-368">Wybierz usługę w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="d5aec-369">W menu u góry hello, kliknij polecenie **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="d5aec-370">Na pasku dolnej powitania kliknij **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="d5aec-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="d5aec-371">Wybierz plik certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="d5aec-372">Jeśli istnieje. PFX, wprowadź hasło hello hello klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="d5aec-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="d5aec-373">Po zakończeniu skopiuj odcisk palca certyfikatu hello z hello nowy wpis na liście hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="d5aec-374">Inne zagadnienia dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="d5aec-374">Other security considerations</span></span>
<span data-ttu-id="d5aec-375">w tym dokumencie opisano ustawienia protokołu SSL Hello szyfrowania komunikacji między hello service i jej klientów, gdy punkt końcowy HTTPS hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="d5aec-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="d5aec-376">Jest to ważne, ponieważ poświadczenia dostępu do bazy danych i inne poufne informacje znajdują się w komunikacie hello.</span><span class="sxs-lookup"><span data-stu-id="d5aec-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="d5aec-377">Należy jednak pamiętać, że usługa hello będzie się powtarzał wewnętrzny stan, w tym poświadczenia, w jego wewnętrznego tabele w bazie danych Microsoft Azure SQL hello dostarczoną do przechowywania metadanych w subskrypcji platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d5aec-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="d5aec-378">Tej bazy danych został zdefiniowany jako część hello następujące ustawienia w pliku konfiguracji usługi (. Plik CSCFG):</span><span class="sxs-lookup"><span data-stu-id="d5aec-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="d5aec-379">Poświadczenia przechowywane w tej bazie danych są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="d5aec-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="d5aec-380">Jednak najlepszym rozwiązaniem, sprawdź, czy role sieć web i proces roboczy wdrożeń usługi są przechowywane w górę toodate i bezpieczne, ponieważ mają dostęp toohello metadanych bazy danych i hello certyfikat używany do szyfrowania i odszyfrowywania przechowywanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d5aec-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

