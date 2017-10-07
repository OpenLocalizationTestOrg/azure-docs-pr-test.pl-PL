---
title: "komunikaty o błędach protokołu RDP aaaSpecific dla maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Zrozumienie określone komunikaty o błędach, które można napotkać podczas próby użycia maszyny wirtualnej systemu Windows tooa połączenia pulpitu zdalnego w systemie Azure"
keywords: "Błąd pulpitu zdalnego, błąd połączeń usług pulpitu zdalnego nie może połączyć się z tooVM, rozwiązywania problemów pulpitu zdalnego"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Rozwiązywanie problemów z określonych RDP błąd wiadomości tooa maszyny Wirtualnej systemu Windows na platformie Azure
W trakcie używania maszyny wirtualnej systemu Windows tooa połączenia pulpitu zdalnego (VM) na platformie Azure może zostać wyświetlony komunikat o błędzie. Szczegółów tego artykułu hello niektóre z najczęściej komunikaty o błędach napotkano oraz rozwiązywanie problemów z tooresolve kroki je. Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej za pomocą protokołu RDP ale czy nie występują komunikat o błędzie, zobacz hello [Podręcznik rozwiązywania problemów dotyczących usług pulpitu zdalnego](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Aby uzyskać informacje na określone komunikaty o błędach zobacz następujące hello:

* [Witaj, sesja zdalna została rozłączona, ponieważ nie ma żadnych tooprovide dostępne serwery licencji usług pulpitu zdalnego licencji](#rdplicense).
* [Pulpit zdalny nie może odnaleźć hello komputera "name"](#rdpname).
* [Wystąpił błąd uwierzytelniania. Witaj urzędu zabezpieczeń lokalnych nie można skontaktować się z](#rdpauth).
* [Błąd zabezpieczeń systemu Windows: Twoje poświadczenia nie działają](#wincred).
* [Ten komputer nie może połączyć z komputerem zdalnym toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>Witaj, sesja zdalna została rozłączona, ponieważ nie ma żadnych tooprovide serwery licencji usług pulpitu zdalnego dostępnych licencji.
Przyczyna: hello 120-dniowego okresu prolongaty licencjonowania roli serwera usług pulpitu zdalnego hello utracił ważność i należy tooinstall licencji.

Jako obejście zapisać lokalną kopię pliku RDP hello z portalu hello i uruchomić to polecenie tooconnect wiersza polecenia programu PowerShell. Ten krok powoduje wyłączenie Licencjonowanie tylko tego połączenia:

        mstsc <File name>.RDP /admin

Jeśli nie potrzebujesz faktycznie więcej niż dwóch jednoczesnych toohello połączeń usług pulpitu zdalnego maszyny Wirtualnej, można użyć roli serwera usług pulpitu zdalnego hello tooremove Menedżera serwera.

Aby uzyskać więcej informacji, zobacz hello blogu [maszyny Wirtualnej platformy Azure nie powiodło się "Nie serwerów usług pulpitu zdalnego licencji dostępnych"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Pulpit zdalny nie może odnaleźć komputera hello "name".
Przyczyna: powitania klienta pulpitu zdalnego na tym komputerze nie można rozpoznać nazwy hello hello komputera w ustawieniach hello hello pliku RDP.

Możliwe rozwiązania:

* Jeśli jesteś w intranecie firmy, upewnij się, czy komputer ma serwera proxy toohello dostępu i wysłać tooit ruchu HTTPS.
* Jeśli korzystasz z lokalnie przechowywanego pliku RDP, spróbuj użyć hello jedną generowany przez hello portal. Ten krok zapewnia hello poprawna nazwa DNS dla maszyny wirtualnej hello, lub usługi w chmurze hello i port punktu końcowego hello hello maszyny Wirtualnej. Oto przykładowy plik RDP, generowane przez hello portal:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

ma adres Hello część tego pliku RDP:

* Witaj w pełni kwalifikowana nazwa domeny usługi w chmurze hello zawierający hello maszyny Wirtualnej ("tailspin-azdatatier.cloudapp.net" w tym przykładzie).
* Hello TCP portu zewnętrznego punktu końcowego hello transmisji pulpitu zdalnego (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Wystąpił błąd uwierzytelniania. Nie można skontaktować się z Hello urzędu zabezpieczeń lokalnych.
Przyczyna: hello docelowej maszyny Wirtualnej nie może zlokalizować urzędu zabezpieczeń hello w części zawierającej nazwę użytkownika hello poświadczeń.

Gdy nazwa użytkownika jest w formie hello *SecurityAuthority*\\*UserName* (przykład: CORP\User1), hello *SecurityAuthority* fragment jest albo hello maszyny Wirtualnej w Nazwa komputera (dla urzędu zabezpieczeń lokalnych hello) lub nazwę domeny usługi Active Directory.

Możliwe rozwiązania:

* Jeśli konto hello jest toohello lokalnej maszyny Wirtualnej, upewnij się, że nazwa wirtualna tego hello jest poprawna.
* Jeśli konto hello znajduje się w domenie usługi Active Directory, Sprawdź pisownię hello hello nazwy domeny.
* Jeśli konto domeny usługi Active Directory i hello nazwa domeny została wpisana poprawnie, sprawdź, czy kontroler domeny jest dostępny w tej domenie. Jest typowym problemem w sieci wirtualnych platformy Azure, zawierających kontrolery domeny, że kontroler domeny jest niedostępna, ponieważ nie została uruchomiona. Jako rozwiązanie alternatywne można użyć konta administratora lokalnego zamiast konta domeny.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Błąd zabezpieczeń systemu Windows: Twoje poświadczenia nie działają.
Przyczyna: hello docelowej maszyny Wirtualnej nie może zweryfikować nazwę konta i hasło.

Komputer z systemem Windows można zweryfikować poświadczeń hello konta lokalnego lub konta domeny.

* Dla kont lokalnych, użyj hello *ComputerName*\\*UserName* składni (przykład: SQL1\Admin4798).
* Dla kont domeny, użyj hello *DomainName*\\*UserName* składni (przykład: CONTOSO\peterodman).

Jeśli ma podwyższenia poziomu kontrolera domeny tooa maszyny Wirtualnej w nowym lesie usługi Active Directory, zostanie przekonwertowany hello konta administratora lokalnego, który podpisał z tooan równoważne konta hello same hasło w hello nowego lasu i domeny. Konto lokalne powitania jest usuwany.

Na przykład jeśli zalogowany za pomocą konta lokalnego hello DC1\DCAdmin, a następnie podwyższony hello maszynę wirtualną jako kontroler domeny w nowym lesie dla domeny corp.contoso.com hello hello DC1\DCAdmin lokalnego konta zostaje usunięta i nowe konto domeny (CORP\DCAdmin ) jest tworzony z hello samo hasło.

Upewnij się, czy nazwa konta hello jest nazwa maszyny wirtualnej hello można sprawdzić jako prawidłowe konto, czy hasło hello jest poprawna.

Jeśli potrzebujesz toochange hello hasło konta administratora lokalnego hello zobacz [jak tooreset hasła lub hello pulpitu zdalnego usługi dla maszyn wirtualnych systemu Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Ten komputer nie może połączyć toohello komputera zdalnego.
Przyczyna: konto hello, który został użyty tooconnect nie ma pulpitu zdalnego logowania praw.

Każdy komputer z systemem Windows ma pulpitu zdalnego użytkownicy grupą lokalną, zawierającą hello kont i grup, które można zdalnie Zaloguj się do niego. Członkowie grupy Administratorzy lokalni hello mają także dostęp, nawet jeśli te konta nie są wymienione w hello grupy lokalnej Użytkownicy pulpitu zdalnego. W przypadku komputerów przyłączonych do domeny grupy administratorów lokalnych hello zawiera hello Administratorzy domeny dla domeny hello.

Upewnij się, że konta hello, którego używasz tooconnect z uprawnieniami pulpitu zdalnego logowania. Jako obejście za pomocą tooconnect konta administratora lokalnego lub domeny za pośrednictwem pulpitu zdalnego. tooadd hello grupy lokalnej Użytkownicy pulpitu zdalnego toohello odpowiednie konto, za pomocą przystawki programu Microsoft Management Console hello (**Narzędzia systemowe > Użytkownicy i grupy lokalne > grupy > Użytkownicy pulpitu zdalnego**).

## <a name="next-steps"></a>Następne kroki
Jeśli żaden z tych błędów wystąpił nieznany problem z łączeniem z za pomocą protokołu RDP, zobacz hello [Podręcznik rozwiązywania problemów dotyczących usług pulpitu zdalnego](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Kroki podczas uzyskiwania dostępu do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów dotyczących dostępu tooan aplikacja była uruchomiona na maszynie Wirtualnej platformy Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Jeśli występują problemy przy użyciu protokołu Secure Shell (SSH) tooconnect tooa maszyny Wirtualnej systemu Linux na platformie Azure, zobacz [Rozwiązywanie problemów z SSH połączeń tooa maszyny Wirtualnej systemu Linux na platformie Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

