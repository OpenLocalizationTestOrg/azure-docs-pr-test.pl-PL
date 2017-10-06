---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD

## <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, przeprowadzisz [zadanie 2 - eksportu hello bezpiecznego tooa certyfikatu LDAP. Plik PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Wybierz, czy toouse hello obsługi portalu Azure w wersji zapoznawczej lub hello Azure classic portal toocomplete to zadanie.
> [!div class="op_single_selector"]
> * **Portalu Azure (wersja zapoznawcza)**: [Włącz bezpieczny protokół LDAP przy użyciu hello portalu Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Klasyczny portal Azure**: [Włącz bezpieczny protokół LDAP przy użyciu klasycznego portalu Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello przy użyciu hello portalu Azure (wersja zapoznawcza)
tooenable bezpieczny protokół LDAP, wykonaj następujące kroki konfiguracji hello:

1. Przejdź toohello  **[portalu Azure](https://portal.azure.com)**.

2. Wyszukaj "usługi domeny" w hello **wyszukiwania zasobów** pola wyszukiwania. Wybierz **usług domenowych Azure AD** z hello wyników wyszukiwania. Witaj **usług domenowych Azure AD** bloku wymieniono domeny zarządzanej.

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Kliknij nazwę hello toosee domeny (na przykład "contoso100.com") hello zarządzane więcej szczegółów na temat hello domeny.

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. Kliknij przycisk **Secure LDAP** w okienku nawigacji hello.

    ![Usługi domenowe — blok bezpiecznego protokołu LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Domyślnie jest wyłączona bezpiecznego LDAP dostępu tooyour domeny zarządzanej. Przełącz **Secure LDAP** za**włączyć**.

    ![Włącz bezpieczny protokół LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Domyślnie bezpiecznego tooyour dostępu LDAP zarządzane domeny przy użyciu hello internet jest wyłączone. Przełącz **Zezwalaj bezpiecznego dostępu LDAP za pośrednictwem hello internet** za**włączyć**, jeśli to konieczne. 

6. Kliknij następujące ikony folderu hello **. Plik PFX o bezpiecznego certyfikatu LDAP**. Określ plik PFX toohello ścieżka hello z certyfikatem hello w celu bezpiecznego LDAP dostępu toohello domeny zarządzanej.

7. Określ hello **toodecrypt hasła. Plik PFX**. Podaj hello samo hasło użyte podczas eksportowania pliku PFX toohello certyfikatu hello.

8. Gdy wszystko będzie gotowe, kliknij przycisk hello **zapisać** przycisku.

9. Zostanie wyświetlone powiadomienie informujące, że dla domeny zarządzanej hello jest konfigurowany bezpiecznego protokołu LDAP. Do czasu ukończenia tej operacji nie można modyfikować inne ustawienia hello domeny.

    ![Konfigurowanie bezpiecznego protokołu LDAP do domeny zarządzanej hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Trwa około 10 minut too15 tooenable bezpieczny protokół LDAP do domeny zarządzanej. Jeśli hello pod warunkiem, że bezpiecznego LDAP certyfikatu jest niezgodny hello wymagane kryteria, dla katalogu nie włączono bezpiecznego protokołu LDAP i zostanie wyświetlony błąd. Na przykład nazwa domeny hello jest niepoprawna, hello certyfikat już wygasł lub wkrótce wygaśnie. W takim przypadku ponów próbę, używając prawidłowego certyfikatu.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Zadanie 4 — konfigurowanie domeny zarządzanej hello tooaccess DNS z hello internet
> [!NOTE]
> **Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.
>
>

Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Po włączeniu bezpiecznego dostępu LDAP za pośrednictwem Internetu hello potrzeby domeny zarządzanej, należy tooupdate DNS tak, aby komputery klienckie można znaleźć tej domeny zarządzanej. Na końcu hello zadanie 3, zewnętrzny adres IP jest wyświetlany na powitania **właściwości** bloku w **IP adres dla LDAPS dostępu zewnętrznego**.

Konfigurowanie dostawcy usługi DNS zewnętrzne tej nazwy DNS hello hello zarządzane zewnętrzny adres IP toothis punktów domeny (na przykład "ldaps.contoso100.com"). W naszym przykładzie potrzebne są nam hello toocreate następującego wpisu DNS:

    ldaps.contoso100.com  -> 52.165.38.113

To wszystko — wszystko jest teraz gotowy tooconnect toohello zarządzane domeny przy użyciu bezpiecznego protokołu LDAP, za pośrednictwem hello internet.

> [!WARNING]
> Należy pamiętać, że komputery klienckie muszą ufać Witaj wystawca hello LDAPS certyfikatu toobe stanie tooconnect pomyślnie toohello zarządzane przy użyciu LDAPS domeny. Jeśli używasz publicznie zaufany urząd certyfikacji, nie trzeba toodo niczego, ponieważ komputery klienckie ufać tych wystawców certyfikatów. Jeśli używasz certyfikatu z podpisem własnym, należy zainstalować hello publicznego część hello certyfikatu z podpisem własnym do magazynu zaufanych certyfikatów hello na komputerze klienckim hello.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Zadanie 5 - LDAPS blokowanie dostępu tooyour zarządzane domeny za pośrednictwem hello internet
> [!NOTE]
> **Opcjonalne zadania** — Jeśli nie włączono LDAPS domeny zarządzanej toohello dostępu ponad hello internet, pomiń to zadanie konfiguracji.
>
>

Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Udostępnianie domeny zarządzanej LDAPS dostępu za pośrednictwem hello internet reprezentuje zagrożenie bezpieczeństwa. Witaj domeny zarządzanej jest dostępny z hello internet na powitania port używany do bezpiecznego protokołu LDAP (to znaczy port 636). W związku z tym można toorestrict dostępu toohello zarządzane domeny toospecific znane adresy IP. Ze względów bezpieczeństwa należy utworzyć grupę zabezpieczeń sieci (NSG) i powiązać ją z podsieci hello, w której włączono usługi domenowe Azure AD.

Witaj poniższej tabeli przedstawiono przykład grupy NSG można skonfigurować toolock dół bezpiecznego dostępu LDAP na powitania internet. Hello NSG zawiera zestaw reguł, które zezwolić na przychodzący LDAPS dostęp za pośrednictwem portu TCP 636 tylko z określonego zestawu adresów IP. Hello domyślne "DenyAll" reguła ma zastosowanie tooall pozostały przychodzący ruch z hello internet. Witaj NSG reguły tooallow LDAPS dostęp za pośrednictwem hello internet z określonych adresów IP ma wyższy priorytet niż hello reguły DenyAll NSG.

![Przykład grupy NSG toosecure LDAPS dostęp za pośrednictwem hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Więcej informacji** - [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Zawartość pokrewna
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Administrowanie zasad grupy w domenie zarządzanej usług domenowych Azure AD](active-directory-ds-admin-guide-administer-group-policy.md)
* [Sieciowe grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md)
* [Utwórz grupę zabezpieczeń sieci](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
