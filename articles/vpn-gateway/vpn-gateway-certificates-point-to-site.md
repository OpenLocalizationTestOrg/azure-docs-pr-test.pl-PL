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
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a>Generowanie i eksportowania certyfikatów połączeń punkt-lokacja za pomocą programu PowerShell w systemie Windows 10

Połączenia punkt-lokacja używają tooauthenticate certyfikatów. W tym artykule pokazano, jak toocreate a podpisem główny certyfikat i generować certyfikaty klienta przy użyciu programu PowerShell w systemie Windows 10. Jeśli szukasz punkt-lokacja kroków konfiguracji, takich jak jak listy certyfikatów głównych tooupload, wybierz jedną z artykułów hello "Konfiguruj punkt-lokacja" z powitania po:

> [!div class="op_single_selector"]
> * [Tworzenie certyfikatów z podpisem własnym — PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Tworzenie certyfikatów z podpisem własnym — MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Skonfiguruj punkt-lokacja - Resource Manager - portalu Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Konfigurowanie programu PowerShell punkt lokacja - Resource Manager —](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Skonfiguruj punkt-lokacja — Classic - portalu Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


W tym artykule na komputerze z systemem Windows 10, należy wykonać kroki hello. Aby używać certyfikatów z toogenerate poleceń cmdlet programu PowerShell Hello są częścią systemu operacyjnego hello systemu Windows 10 i nie działają w innych wersjach systemu Windows. komputer Hello systemu Windows 10 jest tylko certyfikaty hello toogenerate potrzebne. Wygenerowany hello certyfikatów można przekazać je lub je zainstalować w dowolnym systemie operacyjnym klienta obsługiwanych. 

Jeśli nie masz dostępu do komputera tooa systemu Windows 10, możesz użyć [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certyfikatów. Witaj certyfikaty, które można wygenerować za pomocą jednej z metod można zainstalować na dowolnym [obsługiwane](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) kliencki system operacyjny.

## <a name="rootcert"></a>Utwórz certyfikat z podpisem własnym głównego

Użyj toocreate polecenia cmdlet New-SelfSignedCertificate hello certyfikatu głównego z podpisem własnym. Dodatkowy parametr informacji, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

1. Z komputera z systemem Windows 10 Otwórz konsolę programu Windows PowerShell z podwyższonym poziomem uprawnień.
2. Użyj powitania po przykład toocreate hello podpisem głównego certyfikatu. Witaj poniższy przykład tworzy certyfikat główny z podpisem własnym o nazwie P2SRootCert, który jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates". Certyfikat hello można wyświetlić, otwierając *certmgr.msc*, lub *zarządzanie certyfikatami użytkownika*.

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <a name="cer"></a>Wyeksportować klucz publiczny hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Plik exported.cer Hello musi być przekazana tooAzure. Aby uzyskać instrukcje, zobacz [skonfigurować połączenie punkt-lokacja](vpn-gateway-howto-point-to-site-rm-ps.md#upload). tooadd dodatkowe zaufany certyfikat główny, [w tej sekcji](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) hello artykułu.

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a>Wyeksportuj certyfikat główny podpisem hello i toostore klucza publicznego (opcjonalnie)

Możesz tooexport hello główny certyfikat z podpisem własnym i zapisz go w bezpieczne. Jeśli musisz być później zainstalować ją na innym komputerze i generować więcej certyfikaty klienta lub wyeksportować innego pliku .cer. Witaj tooexport certyfikat z podpisem własnym głównego jako PFX, wybierz hello certyfikatu głównego i użycie hello te same czynności, zgodnie z opisem w [wyeksportować certyfikat klienta](#clientexport).

## <a name="clientcert"></a>Generuj certyfikat klienta

Każdy komputer kliencki, który łączy tooa sieci wirtualnej za pomocą punkt-lokacja musi mieć zainstalowany certyfikat klienta. Wygeneruj certyfikat klienta z certyfikatem głównym podpisem hello i wyeksportować i zainstalować certyfikat klienta na powitania. Jeśli certyfikat klienta na powitania nie jest zainstalowany, uwierzytelnianie nie powiedzie się. 

Witaj następujących krokach objaśniono sposób generowania certyfikatu klienta z podpisem własnym głównego certyfikatu. Wiele certyfikatów klienta może generować z hello tym samym certyfikatem głównym. Podczas generowania certyfikatów klienta przy użyciu poniższych czynności hello hello certyfikat klienta jest automatycznie zainstalowane w systemie hello użytą toogenerate hello certyfikatu. Jeśli chcesz tooinstall certyfikat klienta na inny komputer kliencki, można wyeksportować certyfikat hello.

Przykłady Hello Użyj toogenerate polecenia cmdlet New-SelfSignedCertificate hello certyfikat klienta, która wygaśnie za 1 rok. Dla parametru dodatkowe informacje, na przykład ustawienie wartości różnych wygaśnięcia certyfikatu klienta hello, zobacz [SelfSignedCertificate nowy](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

### <a name="example-1"></a>Przykład 1

W tym przykładzie użyto hello zadeklarować zmiennej "$cert" hello w poprzedniej sekcji. Jeśli konsola programu PowerShell hello został zamknięty, po utworzenie hello certyfikatu głównego z podpisem własnym, lub są dodatkowe klienta certyfikaty w nowej sesji konsoli programu PowerShell, wykonaj kroki hello w [przykład 2](#ex2).

Zmodyfikuj i uruchom toogenerate przykład hello certyfikat klienta. Po uruchomieniu hello poniższy przykład bez modyfikowania jej wynik hello jest certyfikat klienta o nazwie "P2SChildCert".  Coś innego certyfikatu podrzędnego hello tooname, zmodyfikuj wartości nazwy Pospolitej hello. Nie należy zmieniać hello TextExtension, uruchamiając w tym przykładzie. certyfikat klienta Hello, generowany jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <a name="ex2"></a>Przykład 2

Tworzysz klienta dodatkowe certyfikaty, czy są nie używa hello sam sesji programu PowerShell, który służy toocreate certyfikat główny z podpisem własnym, użyj hello następujące kroki:

1. Zidentyfikuj certyfikat główny podpisem hello, który jest zainstalowany na komputerze hello. To polecenie cmdlet zwraca listę certyfikatów, które są zainstalowane na komputerze.

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. Znajdź nazwę podmiotu hello z hello zwrócony, a następnie odcisk palca hello kopiowania, znajduje następny tekst tooa tooit pliku. Poniższy przykład hello istnieją dwa certyfikaty. Nazwa CN Hello jest hello hello certyfikatu głównego podpisem, z którego mają zostać toogenerate certyfikatu podrzędnego. W tym przypadku "P2SRootCert".

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. Należy zadeklarować zmienną dla certyfikatu głównego hello za pomocą odcisku palca hello hello w poprzednim kroku. Zastąp odcisk PALCA hello odcisk palca certyfikatu głównego hello, z którego mają zostać toogenerate certyfikatu podrzędnego.

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  Na przykład za pomocą odcisku palca powitania dla P2SRootCert w poprzednim kroku hello, zmienna hello wygląda następująco:

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  Zmodyfikuj i uruchom toogenerate przykład hello certyfikat klienta. Po uruchomieniu hello poniższy przykład bez modyfikowania jej wynik hello jest certyfikat klienta o nazwie "P2SChildCert". Coś innego certyfikatu podrzędnego hello tooname, zmodyfikuj wartości nazwy Pospolitej hello. Nie należy zmieniać hello TextExtension, uruchamiając w tym przykładzie. certyfikat klienta Hello, generowany jest automatycznie instalowany w "Certyfikaty — bieżący User\Personal\Certificates" na komputerze.

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

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Następne kroki

Kontynuuj konfigurację punkt-lokacja. 

* Dla **Resource Manager** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej](vpn-gateway-howto-point-to-site-resource-manager-portal.md). 
* Dla **klasycznego** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenia sieci VPN typu punkt-lokacja sieci wirtualnej (klasyczne)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
