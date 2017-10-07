---
title: "certyfikaty usług i zarządzania aaaCloud | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i używanie certyfikatów przy użyciu systemu Microsoft Azure"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a>Omówienie certyfikatów dla usług w chmurze Azure
Certyfikaty są używane na platformie Azure do usługi w chmurze ([usługi certyfikatów](#what-are-service-certificates)) i do uwierzytelniania z interfejsem API zarządzania hello ([certyfikaty zarządzania](#what-are-management-certificates) po hello przy użyciu klasycznego portalu Azure i nie Witaj z systemem innym niż Klasyczny portal Azure). Ten temat zawiera ogólne omówienie obu typów certyfikatów, jak za[utworzyć](#create) i [wdrażanie](#deploy) ich tooAzure.

Certyfikaty używane na platformie Azure są x.509 v3 certyfikatów i może być podpisany przez inny zaufanego certyfikatu lub można je podpisem. Certyfikatu z podpisem własnym jest podpisany przez jego własnej twórcy, w związku z tym nie jest zaufany domyślnie. W większości przeglądarek, można zignorować ten problem. Należy używać tylko certyfikaty z podpisem własnym podczas tworzenia i testowania usługi w chmurze. 

Certyfikaty używane przez usługę Azure może zawierać prywatnej lub klucza publicznego. Certyfikaty mają odcisku palca, która zapewnia tooidentify oznacza, że ich w sposób jednoznaczny. Taki odcisk palca jest używany w hello Azure [pliku konfiguracyjnego](cloud-services-configure-ssl-certificate.md) tooidentify, który certyfikat usługi w chmurze, należy użyć. 

## <a name="what-are-service-certificates"></a>Co to są certyfikaty usługi?
Usługi certyfikatów są dołączone toocloud usług i Włącz tooand bezpiecznej komunikacji z usługą hello. Na przykład jeśli wdrożono rolę sieci web mają toosupply certyfikatu, który może uwierzytelniać narażonych punkt końcowy HTTPS. Certyfikaty usługi, określone w definicji usługi, są automatycznie wdrożone toohello maszyny wirtualnej, która jest uruchomione wystąpienie roli użytkownika. 

Możesz przekazać classic tooAzure certyfikaty usługi portalu przy użyciu hello Azure classic portal lub za pomocą hello klasycznego modelu wdrażania. Usługi certyfikatów skojarzonych z usługą w chmurze określonych. Wdrażanie tooa w pliku definicji usługi hello są przypisane.

Usługi certyfikatów mogą być zarządzana oddzielnie od usługi i mogą być zarządzane przez różne osoby. Na przykład deweloper może przekazać pakietu usługi, który odwołuje się tooa certyfikatu jest Menedżer poprzednio przekazał tooAzure. Menedżer można zarządzać i odnawiania certyfikatu (zmiana konfiguracji hello hello usługi) bez konieczności tooupload nowego pakietu usług. Aktualizowanie bez nowego pakietu usługi jest możliwe, ponieważ nazwy logicznej hello, nazwa magazynu i lokalizacja certyfikatu hello znajduje się w pliku definicji usługi hello i gdy hello odcisk palca certyfikatu jest określony w pliku konfiguracji usługi hello. tooupdate hello certyfikat, jest tylko niezbędne tooupload nowego certyfikatu i odcisk palca hello Zmień wartość w pliku konfiguracji usługi hello.

>[!Note]
>Witaj [usługi w chmurze — często zadawane pytania](cloud-services-faq.md) artykuł zawiera niektóre przydatne informacje na temat certyfikatów.

## <a name="what-are-management-certificates"></a>Co to są certyfikaty zarządzania?
Certyfikaty zarządzania pozwalają tooauthenticate z hello klasycznego modelu wdrażania. Wiele programów i narzędzia (np. programu Visual Studio lub hello Azure SDK) należy użyć tych certyfikatów tooautomate Konfiguracja i wdrożenie różnych usług platformy Azure. Nie są naprawdę pokrewne toocloud usług. 

> [!WARNING]
> Ostrożnie! Zezwalaj tych typów certyfikatów, każdy, kto jest uwierzytelniany w usłudze ich toomanage hello subskrypcji skojarzonych z nimi. 
> 
> 

### <a name="limitations"></a>Ograniczenia
Istnieje limit 100 certyfikatów zarządzania dla subskrypcji. Istnieje również limit 100 certyfikatów zarządzania dla wszystkich subskrypcji w obszarze Nazwa użytkownika administratora określonej usługi. Hello identyfikator użytkownika dla administratora konta hello został już certyfikaty zarządzania używanych tooadd 100, jeśli ma potrzeby więcej certyfikatów, możesz dodać administratora współpracującego tooadd hello dodatkowych certyfikatów. 

Przed dodaniem więcej niż 100 certyfikatów, zobacz, czy można ponownie użyć istniejącego certyfikatu. Przy użyciu współadministratorów dodaje procesu zarządzania certyfikatu tooyour potencjalnie niepotrzebnych złożoności.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Utwórz nowy certyfikat z podpisem własnym
Można użyć dowolnego toocreate dostępne narzędzia certyfikatu z podpisem własnym, tak długo, jak będą one zgodne z ustawieniami toothese:

* Certyfikat X.509.
* Zawiera klucz prywatny.
* Utworzone dla wymiany kluczy (pfx).
* Nazwa podmiotu musi odpowiadać usługi hello tooaccess hello domeny użytej w chmurze.

    > Nie można pobrać certyfikatu SSL dla hello cloudapp.net (lub jakichkolwiek związanych z platformy Azure) domeny; Nazwa podmiotu certyfikatu Hello musi odpowiadać hello domenę niestandardową nazwę używaną tooaccess aplikacji. Na przykład **contoso.net**, a nie **contoso.cloudapp.net**.

* Co najmniej 2048-bitowego szyfrowania.
* **Usługi certyfikatów tylko**: po stronie klienta, certyfikat musi znajdować się w hello *osobistych* magazynu certyfikatów.

Istnieją dwa sposoby łatwe toocreate certyfikatu w systemie Windows hello `makecert.exe` narzędzia lub usług IIS.

### <a name="makecertexe"></a>MakeCert.exe
Narzędzie to jest przestarzała i nie jest już opisanych tutaj. Aby uzyskać więcej informacji, zobacz [ten artykuł w witrynie MSDN](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Jeśli chcesz toouse hello certyfikatu za pomocą adresu IP, a nie do domeny, należy użyć adresu IP hello w parametrze - DnsName hello.


Jeśli chcesz toouse to [certyfikatu za pomocą portalu zarządzania hello](../azure-api-management-certs.md), eksportowania ich tooa **.cer** pliku:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internetowe usługi informacyjne (IIS)
Istnieje wiele stron na powitania Internetu pokrywał jak toodo to z usługami IIS. [W tym miejscu](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) jest doskonałym udało mi się znaleźć traktować go wyjaśniono również. 

### <a name="java"></a>Java
Można użyć języka Java za[utworzyć certyfikat](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[To](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykule opisano, jak toocreate certyfikatów przy użyciu protokołu SSH.

## <a name="next-steps"></a>Następne kroki
[Przekaż toohello certyfikatu z usługi klasycznego portalu Azure](cloud-services-configure-ssl-certificate.md) (lub hello [portalu Azure](cloud-services-configure-ssl-certificate-portal.md)).

Przekaż [certyfikat interfejsu API zarządzania](../azure-api-management-certs.md) toohello klasycznego portalu Azure. Witaj portalu Azure do uwierzytelniania nie korzysta z certyfikatów zarządzania.

