---
title: "Usługi domenowe Azure AD: Kontrolery domeny tooDIY usług porównania domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Porównywanie kontrolery domeny usług domenowych Azure Active Directory tooDIY"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>Jak toodecide Jeśli usług domenowych Azure AD jest odpowiednia dla przypadek użycia
Z usług domenowych Azure AD można wdrażać obciążeń w usługi infrastruktury platformy Azure, bez konieczności tooworry związane z konserwacją infrastruktury tożsamości na platformie Azure. Ta usługa zarządzanych różni się od typowe wdrożenie usługi Active Directory systemu Windows Server, wdrażania i administrowania samodzielnie. Usługa Hello jest łatwe toodeploy i zapewnia monitorowanie kondycji automatycznych i korygowania. Firma Microsoft stale ewoluuje hello usługi tooadd obsługę typowych scenariuszy wdrożeń.

toodecide czy usługi domenowe Azure AD toouse zalecamy następujące materiałów hello:

* Lista hello [funkcje oferowane przez usługi domenowe Azure AD](active-directory-ds-features.md).
* Przejrzyj typowe [scenariusze wdrażania usług domenowych Azure AD](active-directory-ds-scenarios.md).
* Na koniec [porównanie opcji tooa Zrób AD usługi domenowe Azure AD](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure).

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>Porównanie usług domenowych Azure AD tooDIY AD domeny na platformie Azure
Witaj Poniższa tabela ułatwia wybór między przy użyciu usług domenowych Azure AD i zarządzanie nimi własną infrastrukturę AD na platformie Azure.

| **Funkcja** | **Usługi domenowe Azure AD** | **"Zrób" AD na maszynach wirtualnych platformy Azure** |
| --- |:---:|:---:|
| [**Zarządzana usługa**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**& #x 2715;** |
| [**Zabezpieczanie wdrożenia**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |Administrator musi toosecure hello wdrożenia. |
| [**Serwer DNS**](active-directory-ds-comparison.md#dns-server) |**& #x 2713;**  (usługa zarządzane) |**&#x2713;** |
| [**Uprawnienia administratora domeny lub Enterprise**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**& #x 2715;** |**&#x2713;** |
| [**Przyłączanie do domeny**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**Uwierzytelnianie domeny przy użyciu protokołu NTLM i Kerberos**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Ograniczone delegowanie protokołu Kerberos**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|oparte na zasobach|oparte na zasobach & na podstawie konta|
| [**Niestandardowe struktury jednostek organizacyjnych**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**Rozszerzenia schematu**](active-directory-ds-comparison.md#schema-extensions) |**& #x 2715;** |**&#x2713;** |
| [**Relacje zaufania lasu domeny usługi AD**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**& #x 2715;** |**&#x2713;** |
| [**LDAP do odczytu**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**Bezpieczny protokół LDAP (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**Zapis LDAP**](active-directory-ds-comparison.md#ldap-write) |**& #x 2715;** |**&#x2713;** |
| [**Zasady grupy**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**Rozproszona geograficznie wdrożenia**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**& #x 2715;** |**&#x2713;** |

#### <a name="managed-service"></a>Zarządzana usługa
Azure domeny usług domenowych AD są zarządzane przez firmę Microsoft. Nie masz tooworry o poprawki, aktualizacje, monitorowanie kopii zapasowych i zapewnienie dostępności domeny. Te zadania zarządzania są oferowane jako usługa przez Microsoft Azure w domenach zarządzanych.

#### <a name="secure-deployments"></a>Zabezpieczanie wdrożenia
bezpieczne domeny zarządzanej Hello jest zablokowana zgodnie z harmonogramem zalecenia dotyczące zabezpieczeń firmy Microsoft dla wdrożeń usługi AD. Te zalecenia wynika z zespołu produktu hello AD dekad doświadczenia inżynierii i obsługi wdrożenia usługi AD. W przypadku wdrożeń Zrób należy tootake określonego wdrożenia toolock kroki w dół/zabezpieczania wdrożenia.

#### <a name="dns-server"></a>Serwer DNS
Domeny zarządzanej usług domenowych Azure AD zawiera zarządzanych usług DNS. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello, można zarządzać DNS w domenie hello zarządzane. Członkowie tej grupy są podane pełne uprawnienia do administrowania systemem DNS dla domeny zarządzanej hello. Zarządzanie systemem DNS mogą być wykonywane przy użyciu hello "Konsoli administracyjnej DNS" zawarte w pakiecie narzędzia administracji zdalnej serwera (RSAT) hello.
[Więcej informacji](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>Uprawnienia do domeny lub administratora przedsiębiorstwa
Te podniesione uprawnienia nie są dostępne w domenie zarządzanej usługi AAD DS. Domen zarządzanych aplikacji, które wymagają tych podniesione uprawnienia nie można wdrożyć przed DS usługi AAD. Mniejszego podzestawu uprawnień administracyjnych jest dostępne toomembers hello administracji delegowanej grupy o nazwie "Administratorzy usługi AAD kontrolera domeny". Te uprawnienia obejmują uprawnienia tooconfigure DNS, skonfigurować zasady grupy, uzyskanie uprawnień administratora na komputerach przyłączonych do domeny itp.

#### <a name="domain-join"></a>Przyłączanie do domeny
Możesz także dołączyć do maszyn wirtualnych toohello zarządzane domeny toohow podobne dołączeniu do domeny tooan AD komputerów.

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>Uwierzytelnianie domeny przy użyciu protokołu NTLM i Kerberos
Z usług domenowych Azure AD można użyć tooauthenticate Twojego poświadczeń firmowych z hello domeny zarządzanej. Poświadczenia są zsynchronizowane z dzierżawą usługi Azure AD. Dla zsynchronizowane dzierżawy Azure AD Connect zapewnia, że zmiany wprowadzone toocredentials lokalnych są synchronizowane tooAzure AD. Z konfiguracją Zrób domeny, może być konieczne tooset zapasową domeny AD relację zaufania z lokalnej usługi AD dotyczącego tooauthenticate użytkowników przy użyciu poświadczeń firmowych. Alternatywnie może być konieczne tooset górę aby haseł użytkowników synchronizować maszyn wirtualnych kontrolerów domeny Azure tooyour tooensure replikacji usługi AD.

#### <a name="kerberos-constrained-delegation"></a>Ograniczone delegowanie protokołu Kerberos
Nie masz uprawnień administratora domeny w domenie zarządzanej usług domenowych w usłudze Active Directory. W związku z tym nie można skonfigurować na podstawie konta (tradycyjny) ograniczone delegowanie protokołu Kerberos. Można jednak skonfigurować hello bezpieczniejsze oparte na zasobach ograniczonego delegowania.
[Więcej informacji](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>Niestandardowe struktury jednostek organizacyjnych
Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello można tworzyć niestandardowe jednostek organizacyjnych w domenie hello zarządzane. Użytkownicy, którzy tworzą niestandardowej jednostki organizacyjne są przyznawane pełne uprawnienia administracyjne na powitania jednostki Organizacyjnej.
[Więcej informacji](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>Rozszerzenia schematu
Nie można rozszerzyć schematu podstawowego hello domeny zarządzanej usług domenowych Azure AD. W związku z tym aplikacje korzystające z rozszerzenia schematu tooAD (na przykład nowych atrybutów obiektu użytkownika hello) nie może zostać cofnięte i przesunięte domen tooAAD DS.

#### <a name="ad-domain-or-forest-trusts"></a>AD domeny lub zaufanie lasu
Domen zarządzanych nie może być skonfigurowany tooset się relacje zaufania (przychodzącego/wychodzącego) z innymi domenami. W związku z tym scenariuszy wdrażania lasu zasobów nie można użyć usług domenowych Azure AD. Podobnie wdrożeń, gdzie wolisz nie toosynchronize tooAzure haseł usługi AD nie można użyć usług domenowych Azure AD.

#### <a name="ldap-read"></a>Odczyt LDAP
Witaj zarządzane obciążeń odczytu LDAP obsługuje domeny. W związku z tym można wdrożyć aplikacji, które wykonują operacje względem domeny zarządzanej hello odczytu LDAP.

#### <a name="secure-ldap"></a>Bezpieczny protokół LDAP
Można skonfigurować usługi domenowe Azure AD tooprovide bezpiecznego LDAP dostępu tooyour zarządzane domeny, w tym nad hello internet.
[Więcej informacji](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>Zapis LDAP
domeny zarządzanej Hello jest tylko do odczytu obiektów użytkownika. W związku z tym aplikacje, które wykonują operacje zapisu LDAP atrybutów obiektu użytkownika hello nie działają w domeny zarządzanej. Ponadto haseł użytkowników nie można zmienić z wewnątrz hello domeny zarządzanej. Innym przykładem może być zmiana członkostwa grupy lub grupy atrybutów w obrębie domeny zarządzanej hello, co jest niedozwolone. Jednak wszystkie dokonane zmiany atrybutów toouser lub hasła w usłudze Azure AD (za pośrednictwem portalu programu PowerShell/Azure) lub lokalnej usługi AD są synchronizowane toohello AAD DS zarządzane domeny.

#### <a name="group-policy"></a>Zasady grupy
Brak wbudowanego obiektu zasad grupy poszczególnych kontenerów "AADDC komputery" i "Użytkownicy AADDC" hello. Można dostosować te zasady grupy wbudowane tooconfigure obiektów zasad grupy. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello można utworzyć niestandardowe obiekty zasad grupy i połączyć je tooexisting jednostek organizacyjnych (w tym niestandardowe jednostek organizacyjnych).
[Więcej informacji](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>Rozproszone geograficznie wdrożenia
Azure domen zarządzanych w usługach domenowych AD są dostępne w jednej sieci wirtualnych na platformie Azure. Scenariusze, które wymagają domeny kontrolery toobe dostępne w wielu regionach platformy Azure przez Witaj świecie, w przypadku konfigurowania kontrolerów domeny w maszynach wirtualnych Azure IaaS może być lepszym hello.


## <a name="do-it-yourself-diy-ad-deployment-options"></a>Opcje wdrażania (DIY) AD "Zrób"
Przypadki użycia wdrożenia może być konieczne niektóre hello możliwości oferowane przez instalację systemu Windows Server AD. W takich sytuacjach należy wziąć pod uwagę jedną hello następujące Zrób opcje (DIY):

* **Domeny chmury autonomicznej:** można skonfigurować autonomiczny "domenę chmury" przy użyciu maszyn wirtualnych platformy Azure, które zostały skonfigurowane jako kontrolery domeny. Ta infrastruktura nie jest zintegrowana z lokalnej usługi AD środowiska. Ta opcja wymaga innego zestawu "poświadczeń w chmurze" toologin/administrowania maszynami wirtualnymi w chmurze hello.
* **Wdrażanie lasu zasobu:** można skonfigurować w domenie w hello topologią lasu zasobów, przy użyciu maszyn wirtualnych platformy Azure skonfigurowane jako kontrolery domeny. Następnie należy skonfigurować relację zaufania usługi AD z lokalnej usługi AD środowiska. Możesz lasu zasobów toothis przyłączenie do domeny komputerów (maszynach wirtualnych platformy Azure) w chmurze hello. Uwierzytelnianie użytkownika odbywa się za pośrednictwem jednego katalogu lokalnego tooyour połączenia sieci VPN/ExpressRoute.
* **Rozszerzenie sieci lokalnej domeny tooAzure:** można połączyć sieć lokalną tooyour dla sieci wirtualnej platformy Azure przy użyciu połączenia sieci VPN/ExpressRoute. Taka konfiguracja zapewnia toobe maszynach wirtualnych platformy Azure tooyour dołączonego do lokalnej usługi AD. Alternatywą jest toopromote replik kontrolerów domeny z domeny lokalnej na platformie Azure jako Maszynę wirtualną. Można następnie skonfigurować go tooreplicate za pośrednictwem katalogu lokalnego tooyour połączenia sieci VPN/ExpressRoute. W tym trybie wdrożenia rozszerza skutecznie tooAzure domeny użytkownika lokalnego.

> [!NOTE]
> Należy określić, czy opcja DIY lepiej nadaje się do wdrożenia przypadki użycia. Należy wziąć pod uwagę [udostępnianie opinii](active-directory-ds-contact-us.md) toohelp nam zrozumieć, jakie funkcje może pomóc w przyszłości hello wybrano usługi domenowe Azure AD. Ta opinia pomoże nam rozwijać hello usługi toobetter koloru potrzebne do wdrożenia i przypadki użycia.
>
>

Firma Microsoft opublikowano [wskazówki dotyczące wdrażania systemu Windows Server Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx) toohelp ułatwić DIY instalacji.

## <a name="related-content"></a>Powiązana zawartość
* [Funkcje — usługi domenowe Azure AD](active-directory-ds-features.md)
* [Scenariusze wdrażania - usługi domenowe Azure AD](active-directory-ds-scenarios.md)
* [Wskazówki dotyczące wdrażania systemu Windows serwer usługi Active Directory na maszynach wirtualnych Azure](https://msdn.microsoft.com/library/azure/jj156090.aspx)
