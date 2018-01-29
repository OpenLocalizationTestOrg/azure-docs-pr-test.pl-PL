---
title: "Generowanie i eksportowania certyfikatów dla lokacji punktu: środowiska PowerShell: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera kroki, aby utworzyć certyfikat z podpisem własnym głównego, wyeksportować klucz publiczny i generować certyfikaty klienta przy użyciu programu PowerShell w systemie Windows 10."
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
ms.openlocfilehash: be2e8fe12dee88ccf81faaa114056a29e03881bd
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Generowanie i eksportowania certyfikatów połączeń punkt-lokacja za pomocą programu PowerShell w systemie Windows 10

Połączenia punkt-lokacja używa certyfikatów w celu uwierzytelniania. W tym artykule pokazano, jak utworzyć certyfikat z podpisem własnym głównego i generować certyfikaty klienta przy użyciu programu PowerShell w systemie Windows 10. Jeśli szukasz punkt-lokacja kroków konfiguracji, takich jak sposób przekazywania certyfikatów głównych, wybierz jedną z artykułów "Konfiguruj punkt-lokacja" z następującej listy:

> [!div class="op_single_selector"]
> * [Tworzenie certyfikatów z podpisem własnym — PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Tworzenie certyfikatów z podpisem własnym — MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Skonfiguruj punkt-lokacja - Resource Manager - portalu Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Konfigurowanie programu PowerShell punkt lokacja - Resource Manager —](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Skonfiguruj punkt-lokacja — Classic - portalu Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


Należy wykonać kroki opisane w tym artykule na komputerze z systemem Windows 10. Polecenia cmdlet programu PowerShell, które służy do generowania certyfikatów są częścią systemu operacyjnego Windows 10 i nie działają w innych wersjach systemu Windows. Komputer z systemem Windows 10 wymagana jest tylko do wygenerowania certyfikatów. Po wygenerowaniu certyfikaty, można przekazać je lub je zainstalować w dowolnym systemie operacyjnym klienta obsługiwanych. 

Jeśli nie masz dostępu do komputera z systemem Windows 10, możesz użyć [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) do generowania certyfikatów. Certyfikaty, które można wygenerować za pomocą jednej z metod można instalować na żadnym [obsługiwane](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) kliencki system operacyjny.

## <a name="rootcert"></a>Utwórz certyfikat z podpisem własnym głównego

Utwórz certyfikat z podpisem własnym głównego za pomocą polecenia cmdlet New-SelfSignedCertificate. Dodatkowy parametr informacji, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Z komputera z systemem Windows 10 Otwórz konsolę programu Windows PowerShell z podwyższonym poziomem uprawnień.
2. Skorzystaj z następującego przykładu, można utworzyć certyfikatu z podpisem własnym głównego. Poniższy przykład tworzy certyfikat główny z podpisem własnym o nazwie P2SRootCert, który jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates". Certyfikat można wyświetlić, otwierając *certmgr.msc*, lub *zarządzanie certyfikatami użytkownika*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Wyeksportuj klucz publiczny (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Plik exported.cer, należy przekazać do platformy Azure. Aby uzyskać instrukcje, zobacz [skonfigurować połączenie punkt-lokacja](vpn-gateway-howto-point-to-site-rm-ps.md#upload). Aby dodać dodatkowe zaufany certyfikat główny, [w tej sekcji](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) artykułu.

### <a name="export-the-self-signed-root-certificate-and-public-key-to-store-it-optional"></a>Wyeksportuj certyfikat główny z podpisem własnym i klucz publiczny, zapisz go (opcjonalnie)

Można wyeksportować certyfikat główny z podpisem własnym i zapisze go w bezpieczne. Jeśli musisz być później zainstalować ją na innym komputerze i generować więcej certyfikaty klienta lub wyeksportować innego pliku .cer. Aby wyeksportować certyfikat główny z podpisem własnym jako pliku PFX, wybierz certyfikat główny i Zastosuj te same kroki, zgodnie z opisem w [wyeksportować certyfikat klienta](#clientexport).

## <a name="clientcert"></a>Generuj certyfikat klienta

Na każdym komputerze klienckim nawiązującym połączenie z siecią wirtualną za pomocą połączenia typu punkt-lokacja musi być zainstalowany certyfikat klienta w celu uwierzytelniania. Wygeneruj certyfikat klienta z certyfikatu głównego z podpisem własnym i wyeksportować i instalowania certyfikatu klienta. Jeśli certyfikat klienta nie jest zainstalowany, uwierzytelnianie nie powiedzie się. 

W poniższych krokach objaśniono za pośrednictwem generowania certyfikatu klienta z podpisem własnym głównego certyfikatu. Wiele certyfikatów klienta może generować z tym samym certyfikatem głównym. Podczas generowania certyfikatów klienta, wykonaj kroki opisane poniżej certyfikat klienta jest automatycznie zainstalowane na komputerze, który został użyty do wygenerowania certyfikatu. Jeśli chcesz zainstalować certyfikat klienta na inny komputer kliencki, można wyeksportować certyfikat.

W przykładach użyto polecenia cmdlet New-SelfSignedCertificate, aby wygenerować certyfikat klienta, która wygaśnie za 1 rok. Dla parametru dodatkowe informacje, na przykład ustawienie wartości różnych wygaśnięcia certyfikatu klienta, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Przykład 1

W tym przykładzie używane zadeklarowanej zmiennej "$cert" z poprzedniej sekcji. Jeśli zamknięte konsoli programu PowerShell po utworzeniu certyfikatu głównego z podpisem własnym lub tworzenia klienta dodatkowe certyfikaty w nowej sesji konsoli programu PowerShell, wykonaj kroki w [przykład 2](#ex2).

Zmodyfikuj i uruchom przykład, aby wygenerować certyfikat klienta. Po uruchomieniu poniższy przykład bez modyfikowania jej wynikiem jest certyfikat klienta o nazwie "P2SChildCert".  Jeśli chcesz nazwać certyfikatu podrzędnego czegoś innego, zmodyfikuj wartość CN. Nie należy zmieniać TextExtension, uruchamiając w tym przykładzie. Możesz wygenerować certyfikat klienta jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Przykład 2

Jeśli tworzysz dodatkowych certyfikatów lub nie korzystają z tej samej sesji programu PowerShell, który został użyty do utworzenia certyfikatu z podpisem własnym głównego, wykonaj następujące kroki:

1. Zidentyfikuj certyfikat główny podpisem własnym, który jest zainstalowany na komputerze. To polecenie cmdlet zwraca listę certyfikatów, które są zainstalowane na komputerze.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Znajdź nazwę podmiotu na liście zwrócony, a następnie skopiuj odcisk palca, który znajduje się obok niej do pliku tekstowego. W poniższym przykładzie są dwa certyfikaty. Nazwa Pospolita jest nazwą certyfikatu głównego podpisem, z którego chcesz wygenerować certyfikat podrzędnego. W tym przypadku "P2SRootCert".

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Należy zadeklarować zmienną dla certyfikatu głównego, za pomocą odcisku palca z poprzedniego kroku. Zastąp odcisk PALCA odcisk palca certyfikatu głównego, z którego chcesz wygenerować certyfikat podrzędnego.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Na przykład za pomocą odcisku palca dla P2SRootCert w poprzednim kroku, zmienna wygląda następująco:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Zmodyfikuj i uruchom przykład, aby wygenerować certyfikat klienta. Po uruchomieniu poniższy przykład bez modyfikowania jej wynikiem jest certyfikat klienta o nazwie "P2SChildCert". Jeśli chcesz nazwać certyfikatu podrzędnego czegoś innego, zmodyfikuj wartość CN. Nie należy zmieniać TextExtension, uruchamiając w tym przykładzie. Możesz wygenerować certyfikat klienta jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <a name="clientexport"></a>Eksportowanie certyfikatu klienta   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <a name="install"></a>Zainstaluj certyfikat wyeksportowany klienta

Aby zainstalować certyfikat klienta, zobacz [zainstalować certyfikat klienta na potrzeby połączenia punkt-lokacja](point-to-site-how-to-vpn-client-install-azure-cert.md).

## <a name="next-steps"></a>Kolejne kroki

Kontynuuj konfigurację punkt-lokacja.

* Dla **Resource Manager** kroków modelu wdrażania, zobacz [P2S skonfigurować przy użyciu uwierzytelniania certyfikatu Azure natywnego](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Dla **klasycznego** kroków modelu wdrażania, zobacz [skonfigurować połączenie sieci VPN typu punkt-lokacja sieci wirtualnej (klasyczne)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).