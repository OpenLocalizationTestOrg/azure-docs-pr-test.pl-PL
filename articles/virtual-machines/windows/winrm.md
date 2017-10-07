---
title: "aaaSet WinRM dostępu dla maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Konfiguracja dostępu do usługi WinRM do użytku z maszyny wirtualnej platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Konfigurowanie usługi WinRM dostępu dla maszyn wirtualnych w usłudze Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>Usługa WinRM w programie vs zarządzania usługą Azure usługi Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Omówienie hello Azure Resource Manager, zobacz to [artykułu](../../azure-resource-manager/resource-group-overview.md)
* Różnice między zarządzania usługą Azure i usługi Azure Resource Manager, zobacz to [artykułu](../../resource-manager-deployment-model.md)

Witaj klucza różnica w Określanie konfiguracji usługi WinRM między dwa stosy hello jest jak hello certyfikatu są instalowane na powitania maszyny Wirtualnej. W stosie usługi Azure Resource Manager hello certyfikaty hello są modelowane jako zasobów zarządzanych przez hello dostawcy zasobów magazynu kluczy. W związku z tym hello użytkownika wymaga tooprovide własnych certyfikatów i przekaż go tooa Key Vault przed jego użyciem w maszynie Wirtualnej.

Poniżej przedstawiono kroki hello należy tooset tootake w górę Maszynę wirtualną z połączeniem WinRM

1. Tworzenie magazynu kluczy
2. Utwórz certyfikat z podpisem własnym
3. Przekaż tooKey Twojego certyfikatu z podpisem własnym magazynie
4. Uzyskać adres URL hello z certyfikatu z podpisem własnym w hello magazyn kluczy
5. Odwołanie adres URL certyfikaty z podpisem własnym podczas tworzenia maszyny Wirtualnej

## <a name="step-1-create-a-key-vault"></a>Krok 1: Tworzenie magazynu kluczy
Można użyć hello poniżej polecenia toocreate hello magazyn kluczy

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Krok 2: Tworzenie certyfikatu z podpisem własnym
Można utworzyć certyfikatu z podpisem własnym za pomocą tego skryptu PowerShell

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Krok 3: Przekaż toohello Twojego certyfikatu z podpisem własnym magazyn kluczy
Przed przekazywania hello toohello certyfikatu usługi Key Vault utworzonego w kroku 1, musi on tooconverted w formacie hello będzie zrozumiałe dostawcy zasobów Microsoft.Compute. zezwala na powitania poniższego skryptu programu PowerShell można to zrobić

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Krok 4: Uzyskać adres URL hello z certyfikatu z podpisem własnym w hello magazyn kluczy
dostawcy zasobów Microsoft.Compute Hello musi mieć klucz tajny toohello adres URL wewnątrz hello Key Vault podczas inicjowania obsługi administracyjnej hello maszyny Wirtualnej. To umożliwia Microsoft.Compute hello zasobów toodownload dostawcy hello klucz tajny i utworzyć certyfikat równoważne hello na powitania maszyny Wirtualnej.

> [!NOTE]
> adres URL Hello hello klucz tajny musi również tooinclude hello wersji. Przykładowy adres URL wygląda jak poniżej https://contosovault.vault.azure.net:443/klucze tajne/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Szablony
Adres URL toohello łącza hello można uzyskać w szablonie hello przy użyciu hello poniższego kodu

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Możesz uzyskać ten adres URL przy użyciu hello poniżej polecenia programu PowerShell

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Krok 5: Odwołanie adres URL certyfikaty z podpisem własnym podczas tworzenia maszyny Wirtualnej
#### <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager
Podczas tworzenia maszyny Wirtualnej za pomocą szablonów, certyfikat hello pobiera odwołanie do w hello kluczy tajnych i hello winRM sekcji zgodnie z poniższymi instrukcjami:

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

Przykładowy szablon dla hello powyżej można znaleźć tutaj na [201 vm-winrm-keyvault — windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

Kod źródłowy dla tego szablonu można znaleźć w [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Krok 6: Łączenie toohello maszyny Wirtualnej
Zanim będzie można połączyć toohello maszyny Wirtualnej należy toomake się, że komputer jest skonfigurowany do zdalnego zarządzania usługi WinRM. Uruchom program PowerShell jako administrator, a następnie wykonaj hello poniżej polecenia toomake się, że jest skonfigurowane.

    Enable-PSRemoting -Force

> [!NOTE]
> Może być konieczne toomake się, że hello Usługa WinRM jest uruchomiona, jeśli hello powyżej nie działa. Możesz zrobić tego za pomocą`Get-Service WinRM`
> 
> 

Po zakończeniu instalacji hello możesz połączyć toohello maszyny Wirtualnej przy użyciu hello poniżej polecenia

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
