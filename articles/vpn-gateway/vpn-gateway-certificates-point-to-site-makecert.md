---
title: "Generowanie i eksportowania certyfikatów dla lokacji punktu: MakeCert: Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera kroki toocreate certyfikatu głównego z podpisem własnym, wyeksportować klucz publiczny hello i generowania certyfikatów klientów za pomocą narzędzia MakeCert."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 0b795ccf74f1f97fbd3de8a0dc339f9cb0b48183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-makecert"></a>Generowanie i eksportowania certyfikatów połączeń punkt-lokacja za pomocą narzędzia MakeCert

Połączenia punkt-lokacja używają tooauthenticate certyfikatów. W tym artykule przedstawiono, jak toocreate a podpisem głównego certyfikatu i generowania certyfikatów klientów za pomocą narzędzia MakeCert. Jeśli szukasz punkt-lokacja kroków konfiguracji, takich jak jak listy certyfikatów głównych tooupload, wybierz jedną z artykułów hello "Konfiguruj punkt-lokacja" z powitania po:

> [!div class="op_single_selector"]
> * [Tworzenie certyfikatów z podpisem własnym — PowerShell](vpn-gateway-certificates-point-to-site.md)
> * [Tworzenie certyfikatów z podpisem własnym — MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)
> * [Skonfiguruj punkt-lokacja - Resource Manager - portalu Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [Konfigurowanie programu PowerShell punkt lokacja - Resource Manager —](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Skonfiguruj punkt-lokacja — Classic - portalu Azure](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 

Gdy firma Microsoft zaleca używanie hello [kroki Windows 10 PowerShell](vpn-gateway-certificates-point-to-site.md) toocreate certyfikaty, udostępniamy instrukcje te MakeCert jako opcjonalny metody. Hello certyfikaty, które można wygenerować za pomocą jednej z metod można zainstalować na [dowolnego systemu operacyjnego klienta obsługiwanych](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq). Jednak MakeCert ma hello następujące ograniczenia:

* MakeCert jest przestarzały. Oznacza to, że to narzędzie można usunąć w dowolnym momencie. Wszystkie certyfikaty, które już wygenerowane za pomocą narzędzia MakeCert nie będzie mieć wpływ na podczas MakeCert nie jest już dostępny. MakeCert jest tylko certyfikaty hello toogenerate używane jako mechanizm sprawdzania poprawności.

## <a name="rootcert"></a>Utwórz certyfikat z podpisem własnym głównego

Hello następujące kroki pokazują, jak toocreate a podpisanych certyfikatów za pomocą narzędzia MakeCert. Te kroki nie są właściwe modelu wdrażania. Są one ważne dla usługi Resource Manager i model klasyczny.

1. Pobierz i zainstaluj [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968(v=vs.85).aspx).
2. Po zakończeniu instalacji, zwykle można znaleźć narzędzie makecert.exe hello w tej ścieżce: "C:\Program Files (x86) \Windows Kits\10\bin\<arch >". Niemniej jednak możliwe jest był zainstalowany tooanother lokalizacji. Otwórz wiersz polecenia jako administrator i przejdź do lokalizacji toohello hello narzędzie MakeCert. Program hello poniższy przykład, dostosowanie hello właściwej lokalizacji:

  ```cmd
  cd C:\Program Files (x86)\Windows Kits\10\bin\x64
  ```
3. Utwórz i zainstaluj certyfikat w magazynie certyfikatów osobistych hello na tym komputerze. Witaj poniższy przykład tworzy odpowiadającego *.cer* przekazać tooAzure, konfigurując P2S pliku. Zamień "P2SRootCert" i "P2SRootCert.cer" hello nazwę mają toouse hello certyfikatu. Witaj certyfikat znajduje się w "Certyfikaty — bieżący User\Personal\Certificates".

  ```cmd
  makecert -sky exchange -r -n "CN=P2SRootCert" -pe -a sha256 -len 2048 -ss My
  ```

## <a name="cer"></a>Wyeksportować klucz publiczny hello (.cer)

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

Plik exported.cer Hello musi być przekazana tooAzure. Aby uzyskać instrukcje, zobacz [skonfigurować połączenie punkt-lokacja](vpn-gateway-howto-point-to-site-resource-manager-portal.md#uploadfile). tooadd dodatkowe zaufany certyfikat główny, zobacz [w tej sekcji](vpn-gateway-howto-point-to-site-resource-manager-portal.md#add) hello artykułu.

### <a name="export-hello-self-signed-certificate-and-private-key-toostore-it-optional"></a>Eksportowanie certyfikatu z podpisem własnym hello i toostore klucza prywatnego (opcjonalnie)

Możesz tooexport hello główny certyfikat z podpisem własnym i zapisz go w bezpieczne. Jeśli musisz być później zainstalować ją na innym komputerze i generować więcej certyfikaty klienta lub wyeksportować innego pliku .cer. Witaj tooexport certyfikat z podpisem własnym głównego jako PFX, wybierz hello certyfikatu głównego i użycie hello te same czynności, zgodnie z opisem w [wyeksportować certyfikat klienta](#clientexport).

## <a name="create-and-install-client-certificates"></a>Tworzenie i instalowania certyfikatów klienta

Nie instaluj certyfikatu z podpisem własnym hello bezpośrednio na komputerze klienckim hello. Należy toogenerate certyfikatu klienta z hello certyfikatu z podpisem własnym. Następnie wyeksportować i zainstalować komputer kliencki toohello powitania klienta certyfikatu. Witaj, wykonaj czynności nie są określonego modelu wdrażania. Są one ważne dla usługi Resource Manager i model klasyczny.

### <a name="clientcert"></a>Generuj certyfikat klienta

Każdy komputer kliencki, który łączy tooa sieci wirtualnej za pomocą punkt-lokacja musi mieć zainstalowany certyfikat klienta. Wygeneruj certyfikat klienta z certyfikatem głównym podpisem hello i wyeksportować i zainstalować certyfikat klienta na powitania. Jeśli certyfikat klienta na powitania nie jest zainstalowany, uwierzytelnianie nie powiedzie się. 

Witaj następujących krokach objaśniono sposób generowania certyfikatu klienta z podpisem własnym głównego certyfikatu. Wiele certyfikatów klienta może generować z hello tym samym certyfikatem głównym. Podczas generowania certyfikatów klienta przy użyciu poniższych czynności hello hello certyfikat klienta jest automatycznie zainstalowane w systemie hello użytą toogenerate hello certyfikatu. Jeśli chcesz tooinstall certyfikat klienta na inny komputer kliencki, można wyeksportować certyfikat hello.
 
1. Na powitania tym samym komputerze, że używane toocreate hello certyfikat z podpisem własnym, otwórz wiersz polecenia jako administrator.
2. Zmodyfikuj i uruchom toogenerate próbki hello certyfikat klienta.
  * Zmień *"P2SRootCert"* toohello nazwę hello podpisem głównego, który jest generowany hello certyfikatu klienta z. Upewnij się, że używasz nazwę hello hello głównego certyfikatu, który jest niezależnie od hello "CN =' wartość została określona podczas tworzenia hello podpisem głównego.
  * Zmień *P2SChildCert* toohello nazwę, która ma toogenerate toobe certyfikatu klienta.

  Po uruchomieniu hello poniższy przykład bez modyfikowania jej wynik hello jest certyfikat klienta o nazwie P2SChildcert w magazynie certyfikatów osobistych, który został wygenerowany na podstawie certyfikatu głównego P2SRootCert.

  ```cmd
  makecert.exe -n "CN=P2SChildCert" -pe -sky exchange -m 96 -ss My -in "P2SRootCert" -is my -a sha256
  ```

### <a name="clientexport"></a>Eksportowanie certyfikatu klienta

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

### <a name="install"></a>Zainstaluj certyfikat wyeksportowany klienta

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a>Następne kroki

Kontynuuj konfigurację punkt-lokacja. 

* Dla **Resource Manager** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenie punkt-lokacja sieci wirtualnej](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Dla **klasycznego** kroków modelu wdrażania, zobacz [skonfigurować tooa połączenia sieci VPN typu punkt-lokacja sieci wirtualnej (klasyczne)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).
