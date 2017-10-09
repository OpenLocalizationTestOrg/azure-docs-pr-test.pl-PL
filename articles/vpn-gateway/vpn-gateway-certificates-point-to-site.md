---
title: "Generowanie i eksportowania certyfikatów dla lokacji punktu: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera kroki toocreate certyfikatu głównego z podpisem własnym, a następnie wyeksportować klucz publiczny hello i wygenerowania certyfikatów klienta przy użyciu programu PowerShell w systemie Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="0ea8d-103">Generowanie i eksportowania certyfikatów połączeń punkt-lokacja za pomocą programu PowerShell w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="0ea8d-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="0ea8d-104">Połączenia punkt-lokacja używają tooauthenticate certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="0ea8d-105">W tym artykule pokazano, jak toocreate a podpisem główny certyfikat i generować certyfikaty klienta przy użyciu programu PowerShell w systemie Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="0ea8d-106">Jeśli szukasz punkt-lokacja kroków konfiguracji, takich jak jak listy certyfikatów głównych tooupload, wybierz jedną z artykułów hello "Konfiguruj punkt-lokacja" z powitania po:</span><span class="sxs-lookup"><span data-stu-id="0ea8d-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ea8d-107">Tworzenie certyfikatów z podpisem własnym — PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ea8d-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="0ea8d-108">Tworzenie certyfikatów z podpisem własnym — MakeCert</span><span class="sxs-lookup"><span data-stu-id="0ea8d-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="0ea8d-109">Skonfiguruj punkt-lokacja - Resource Manager - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ea8d-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="0ea8d-110">Konfigurowanie programu PowerShell punkt lokacja - Resource Manager —</span><span class="sxs-lookup"><span data-stu-id="0ea8d-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="0ea8d-111">Skonfiguruj punkt-lokacja — Classic - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ea8d-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="0ea8d-112">W tym artykule na komputerze z systemem Windows 10, należy wykonać kroki hello.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="0ea8d-113">Aby używać certyfikatów z toogenerate poleceń cmdlet programu PowerShell Hello są częścią systemu operacyjnego hello systemu Windows 10 i nie działają w innych wersjach systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="0ea8d-114">komputer Hello systemu Windows 10 jest tylko certyfikaty hello toogenerate potrzebne.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="0ea8d-115">Wygenerowany hello certyfikatów można przekazać je lub je zainstalować w dowolnym systemie operacyjnym klienta obsługiwanych.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="0ea8d-116">Jeśli nie masz dostępu do komputera tooa systemu Windows 10, możesz użyć [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="0ea8d-117">Witaj certyfikaty, które można wygenerować za pomocą jednej z metod można zainstalować na dowolnym [obsługiwane](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) kliencki system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="0ea8d-118"><a name="rootcert"></a>Utwórz certyfikat z podpisem własnym głównego</span><span class="sxs-lookup"><span data-stu-id="0ea8d-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="0ea8d-119">Użyj toocreate polecenia cmdlet New-SelfSignedCertificate hello certyfikatu głównego z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="0ea8d-120">Dodatkowy parametr informacji, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="0ea8d-121">Z komputera z systemem Windows 10 Otwórz konsolę programu Windows PowerShell z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="0ea8d-122">Użyj powitania po przykład toocreate hello podpisem głównego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="0ea8d-123">Witaj poniższy przykład tworzy certyfikat główny z podpisem własnym o nazwie P2SRootCert, który jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates".</span><span class="sxs-lookup"><span data-stu-id="0ea8d-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="0ea8d-124">Certyfikat hello można wyświetlić, otwierając *certmgr.msc*, lub *zarządzanie certyfikatami użytkownika*.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="0ea8d-125"><a name="cer"></a>Wyeksportować klucz publiczny hello (.cer)</span><span class="sxs-lookup"><span data-stu-id="0ea8d-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="0ea8d-126">Plik exported.cer Hello musi być przekazana tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="0ea8d-127">Aby uzyskać instrukcje, zobacz [skonfigurować połączenie punkt-lokacja](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="0ea8d-128">tooadd dodatkowe zaufany certyfikat główny, [w tej sekcji](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="0ea8d-129">Wyeksportuj certyfikat główny podpisem hello i toostore klucza publicznego (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="0ea8d-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="0ea8d-130">Możesz tooexport hello główny certyfikat z podpisem własnym i zapisz go w bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="0ea8d-131">Jeśli musisz być później zainstalować ją na innym komputerze i generować więcej certyfikaty klienta lub wyeksportować innego pliku .cer.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="0ea8d-132">Witaj tooexport certyfikat z podpisem własnym głównego jako PFX, wybierz hello certyfikatu głównego i użycie hello te same czynności, zgodnie z opisem w [wyeksportować certyfikat klienta](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="0ea8d-133"><a name="clientcert"></a>Generuj certyfikat klienta</span><span class="sxs-lookup"><span data-stu-id="0ea8d-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="0ea8d-134">Każdy komputer kliencki, który łączy tooa sieci wirtualnej za pomocą punkt-lokacja musi mieć zainstalowany certyfikat klienta.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="0ea8d-135">Wygeneruj certyfikat klienta z certyfikatem głównym podpisem hello i wyeksportować i zainstalować certyfikat klienta na powitania.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="0ea8d-136">Jeśli certyfikat klienta na powitania nie jest zainstalowany, uwierzytelnianie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="0ea8d-137">Witaj następujących krokach objaśniono sposób generowania certyfikatu klienta z podpisem własnym głównego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="0ea8d-138">Wiele certyfikatów klienta może generować z hello tym samym certyfikatem głównym.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="0ea8d-139">Podczas generowania certyfikatów klienta przy użyciu poniższych czynności hello hello certyfikat klienta jest automatycznie zainstalowane w systemie hello użytą toogenerate hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="0ea8d-140">Jeśli chcesz tooinstall certyfikat klienta na inny komputer kliencki, można wyeksportować certyfikat hello.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="0ea8d-141">Przykłady Hello Użyj toogenerate polecenia cmdlet New-SelfSignedCertificate hello certyfikat klienta, która wygaśnie za 1 rok.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="0ea8d-142">Dla parametru dodatkowe informacje, na przykład ustawienie wartości różnych wygaśnięcia certyfikatu klienta hello, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="0ea8d-143">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="0ea8d-143">Example 1</span></span>

<span data-ttu-id="0ea8d-144">W tym przykładzie użyto hello zadeklarować zmiennej "$cert" hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="0ea8d-145">Jeśli konsola programu PowerShell hello został zamknięty, po utworzenie hello certyfikatu głównego z podpisem własnym, lub są dodatkowe klienta certyfikaty w nowej sesji konsoli programu PowerShell, wykonaj kroki hello w [przykład 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="0ea8d-146">Zmodyfikuj i uruchom toogenerate przykład hello certyfikat klienta.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="0ea8d-147">Po uruchomieniu hello poniższy przykład bez modyfikowania jej wynik hello jest certyfikat klienta o nazwie "P2SChildCert".</span><span class="sxs-lookup"><span data-stu-id="0ea8d-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="0ea8d-148">Coś innego certyfikatu podrzędnego hello tooname, zmodyfikuj wartości nazwy Pospolitej hello.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="0ea8d-149">Nie należy zmieniać hello TextExtension, uruchamiając w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="0ea8d-150">certyfikat klienta Hello, generowany jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="0ea8d-151"><a name="ex2"></a>Przykład 2</span><span class="sxs-lookup"><span data-stu-id="0ea8d-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="0ea8d-152">Tworzysz klienta dodatkowe certyfikaty, czy są nie używa hello sam sesji programu PowerShell, który służy toocreate certyfikat główny z podpisem własnym, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ea8d-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="0ea8d-153">Zidentyfikuj certyfikat główny podpisem hello, który jest zainstalowany na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="0ea8d-154">To polecenie cmdlet zwraca listę certyfikatów, które są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="0ea8d-155">Znajdź nazwę podmiotu hello z hello zwrócony, a następnie odcisk palca hello kopiowania, znajduje następny tekst tooa tooit pliku.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="0ea8d-156">Poniższy przykład hello istnieją dwa certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="0ea8d-157">Nazwa CN Hello jest hello hello certyfikatu głównego podpisem, z którego mają zostać toogenerate certyfikatu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="0ea8d-158">W tym przypadku "P2SRootCert".</span><span class="sxs-lookup"><span data-stu-id="0ea8d-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="0ea8d-159">Należy zadeklarować zmienną dla certyfikatu głównego hello za pomocą odcisku palca hello hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="0ea8d-160">Zastąp odcisk PALCA hello odcisk palca certyfikatu głównego hello, z którego mają zostać toogenerate certyfikatu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="0ea8d-161">Na przykład za pomocą odcisku palca powitania dla P2SRootCert w poprzednim kroku hello, zmienna hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="0ea8d-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="0ea8d-162">Zmodyfikuj i uruchom toogenerate przykład hello certyfikat klienta.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="0ea8d-163">Po uruchomieniu hello poniższy przykład bez modyfikowania jej wynik hello jest certyfikat klienta o nazwie "P2SChildCert".</span><span class="sxs-lookup"><span data-stu-id="0ea8d-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="0ea8d-164">Coś innego certyfikatu podrzędnego hello tooname, zmodyfikuj wartości nazwy Pospolitej hello.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="0ea8d-165">Nie należy zmieniać hello TextExtension, uruchamiając w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="0ea8d-166">certyfikat klienta Hello, generowany jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="0ea8d-167"><a name="clientexport"></a>Eksportowanie certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="0ea8d-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="0ea8d-168"><a name="install"></a>Zainstaluj certyfikat wyeksportowany klienta</span><span class="sxs-lookup"><span data-stu-id="0ea8d-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0ea8d-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ea8d-169">Next steps</span></span>

<span data-ttu-id="0ea8d-170">Kontynuuj konfigurację punkt-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0ea8d-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="0ea8d-171">Dla **Resource Manager** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="0ea8d-172">Dla **klasycznego** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenia sieci VPN typu punkt-lokacja sieci wirtualnej (klasyczne)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ea8d-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
