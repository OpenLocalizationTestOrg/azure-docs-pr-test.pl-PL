---
title: aaaHPC 2016 pakiet klastra na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodeploy HPC Pack 2016 klastra w systemie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Wdrożenie klastra HPC Pack 2016 na platformie Azure

Wykonaj kroki hello w tym artykule toodeploy [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) klastra w maszynach wirtualnych platformy Azure. HPC Pack jest bezpłatna rozwiązania HPC firmy Microsoft, oparty na technologii Microsoft Azure i Windows Server i obsługuje obciążeń szeroki zakres HPC.

Użyj jednej z hello [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 klastra. Można wybrać kilka opcji Topologia klastra z różnymi liczbami głównymi węzłami klastra i z albo systemem Linux lub Windows węzły obliczeniowe.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="pfx-certificate"></a>Certyfikatu PFX

W klastrze Microsoft HPC Pack 2016 wymaga komunikatu hello toosecure certyfikat wymiany informacji osobistych (PFX) między węzłami klastra HPC hello. certyfikat Hello musi spełniać hello następujące wymagania:

* Musi mieć klucz prywatny zdolny do wymiany klucza
* Użycie klucza zawiera podpis cyfrowy i szyfrowanie klucza
* Obejmuje ulepszonego użycia klucza uwierzytelniania serwera i uwierzytelnianie klienta

Jeśli nie masz jeszcze certyfikatu, który spełnia te wymagania, można zażądać hello certyfikatu od urzędu certyfikacji. Alternatywnie można użyć hello następujące polecenia toogenerate hello certyfikatu z podpisem własnym systemem operacyjnym hello, na którym Uruchom polecenie hello i wyeksportuj certyfikat format PFX hello z kluczem prywatnym.

* **Dla systemu Windows 10 lub Windows Server 2016**, uruchom wbudowane hello **SelfSignedCertificate nowy** polecenia cmdlet programu PowerShell w następujący sposób:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **W systemach operacyjnych starszych niż Windows 10 lub Windows Server 2016**, Pobierz hello [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z hello Microsoft Script Center. Wyodrębnij jego zawartość, a następnie uruchom następujące polecenia w wierszu polecenia programu PowerShell hello:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Przekaż certyfikat tooan usługi Azure key vault

Przed wdrożeniem klastra HPC hello, Przekaż hello certyfikatu tooan [usługi Azure key vault](../../key-vault/index.md) jako poufne i rekordów hello, następujących informacji do użycia podczas wdrażania hello: **nazwę magazynu**,  **Grupa zasobów magazynu**, **adres URL certyfikatu**, i **odcisk palca certyfikatu**.

Certyfikat hello tooupload skrypt programu PowerShell próbki jest zgodna. Aby uzyskać więcej informacji na temat przekazywania certyfikatu tooan usługi Azure key vault, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Obsługiwane topologie

Wybierz jedną z hello [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 klastra. Poniżej przedstawiono wysokiego poziomu architektury trzy obsługiwanych topologii klastrów. Topologie wysokiej dostępności obejmują wiele głównymi węzłami klastra.

1. Klastra o wysokiej dostępności z domeną usługi Active Directory

    ![Klastra HA w domenie AD](./media/hpcpack-2016-cluster/haad.png)



2. Wysoka dostępność klastra bez domeny usługi Active Directory

    ![Klastra HA bez domeny usługi AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Klaster z jednym węzłem głównym

   ![Klaster z jednym węzłem głównym](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Wdrażanie klastra

toocreate hello klastra, wybrać szablon i kliknij przycisk **wdrażanie tooAzure**. W hello [portalu Azure](https://portal.azure.com), określ parametry szablonu hello, zgodnie z opisem w hello następujące kroki. Każdy szablon tworzy wszystkich zasobów systemu Azure wymaganych przez infrastruktura klastra HPC hello. Zasoby obejmują sieci wirtualnej platformy Azure, publicznego adresu IP adres usługi równoważenia obciążenia (tylko w przypadku klastra o wysokiej dostępności), interfejsów sieciowych, zestawów dostępności, kont magazynu i maszyn wirtualnych.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Krok 1: Wybierz subskrypcję hello, lokalizacji i grupy zasobów

Witaj **subskrypcji** i hello **lokalizacji** musi być taka sama, określona po przekazaniu certyfikatu PFX (patrz wymagania wstępne). Firma Microsoft zaleca utworzenie **grupy zasobów** hello wdrożenia.

### <a name="step-2-specify-hello-parameter-settings"></a>Krok 2: Określ ustawienia parametru hello

Wprowadź lub zmień wartości parametrów szablonu hello. Kliknij przycisk hello ikona dalej tooeach parametr informacji pomocy. Zobacz też hello wskazówki dotyczące [dostępne rozmiary maszyny Wirtualnej](sizes.md).

Określ wartości hello rejestrowane w hello wymagania wstępne hello następujące parametry: **nazwę magazynu**, **grupy zasobów magazynu**, **adres URL certyfikatu**i **Odcisk palca certyfikatu**.

### <a name="step-3-review-legal-terms-and-create"></a>Krok 3. Przejrzyj postanowienia prawne i utworzyć
Kliknij przycisk **Przejrzyj postanowienia prawne** tooreview hello warunki. Jeśli akceptujesz, kliknij przycisk **zakupu**, a następnie kliknij przycisk **Utwórz** toostart hello wdrożenia.

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra
1. Po wdrożeniu klastra HPC Pack hello Przejdź toohello [portalu Azure](https://portal.azure.com). Kliknij przycisk **grup zasobów**i grupy zasobów hello Znajdź w których hello klastra została wdrożona. Hello można znaleźć węzła głównego maszyn wirtualnych.

    ![Głównymi węzłami klastra w portalu hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. Kliknij przycisk jednego węzła głównego (w klastrze wysokiej dostępności kliknij dowolny z węzłów głównych hello). W **Essentials**, można znaleźć hello publicznego adresu IP lub pełną nazwę DNS hello klastra.

    ![Ustawienia połączenia klastra](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Kliknij przycisk **Connect** toolog na tooany hello węzłów głównych przy użyciu pulpitu zdalnego z nazwą użytkownika administratora. Jeśli klaster hello wdrożono znajduje się w domenie usługi Active Directory, nazwa użytkownika hello ma formę hello <privateDomainName> \<adminUsername > (na przykład hpc.local\hpcadmin).

## <a name="next-steps"></a>Następne kroki
* Przedstawia zadania tooyour klastra. Zobacz [przesłać tooHPC zadań klastra HPC Pack na platformie Azure](hpcpack-cluster-submit-jobs.md) i [Zarządzanie klastra HPC Pack 2016 na platformie Azure przy użyciu usługi Azure Active Directory](hpcpack-cluster-active-directory.md).

