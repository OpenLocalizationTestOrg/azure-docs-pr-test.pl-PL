---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello przy użyciu klasycznego portalu Azure hello
tooenable bezpieczny protokół LDAP, wykonaj następujące kroki konfiguracji hello:

1. Przejdź toohello  **[klasycznego portalu Azure](https://manage.windowsazure.com)**.
2. Wybierz hello **usługi Active Directory** węzła w okienku po lewej stronie powitania.
3. Wybierz katalog hello Azure AD (również określonego tooas "dzierżawy"), dla której włączono usługi domenowe Azure AD.

    ![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Kliknij przycisk hello **Konfiguruj** kartę.

    ![Karta Konfigurowanie w katalogu](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Przewiń w dół do sekcji toohello **usług domenowych w usłudze**. Powinny pojawić się opcję o nazwie **bezpiecznego protokołu LDAP (LDAPS)** pokazane na powitania po zrzut ekranu:

    ![Sekcja konfiguracji usług domenowych](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Kliknij przycisk hello **Konfigurowanie certyfikatu...**  toobring przycisk zapasowej hello **Konfigurowanie certyfikatu protokołu Secure LDAP** okna dialogowego.

    ![Konfigurowanie certyfikatu do bezpiecznego protokołu LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Kliknij następujące ikony folderu hello **certyfikat z pliku PFX** pliku PFX hello toospecify, który zawiera certyfikat hello mają toouse dla bezpiecznej toohello dostępu LDAP zarządzane domeny. Także wprowadzić hello hasło podczas eksportowania pliku PFX toohello certyfikatu hello. Następnie kliknij przycisk hello przycisk na dole hello gotowe.

    ![Określ plik LDAP PFX bezpiecznego i hasło](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę uzyskać wygaszone i znajduje się w hello **oczekujących...**  stanu kilka minut. W tym okresie hello LDAPS certyfikat został zweryfikowany dokładność i skonfigurowano bezpiecznego protokołu LDAP do domeny zarządzanej.

    ![Bezpieczny protokół LDAP — stan oczekiwania](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Trwa około 10 minut too15 tooenable bezpieczny protokół LDAP do domeny zarządzanej. Jeśli hello pod warunkiem, że bezpiecznego LDAP certyfikatu jest niezgodny hello wymagane kryteria, dla katalogu nie włączono bezpiecznego protokołu LDAP i zostanie wyświetlony błąd. Na przykład nazwa domeny hello jest niepoprawna, hello certyfikat już wygasł lub wkrótce wygaśnie.
   >
   >

9. Gdy pomyślnie włączono bezpiecznego protokołu LDAP do domeny zarządzanej, hello **oczekujących...**  powinien zniknąć wiadomości. Powinny pojawić się hello odcisk palca certyfikatu hello wyświetlane.

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Zadanie 4 — Włączanie bezpiecznego dostępu LDAP za pośrednictwem hello internet
**Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.

Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Powinny pojawić się opcja zbyt**hello włączyć bezpieczny LDAP dostęp za pośrednictwem INTERNETU** w hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** strony. Ta opcja jest ustawiona zbyt**nr** domyślnie ponieważ zarządzana toohello dostęp do Internetu domeny za pośrednictwem bezpiecznego protokołu LDAP jest domyślnie wyłączona.

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Przełącz **hello włączyć bezpieczny LDAP dostęp za pośrednictwem INTERNETU** za**tak**. Kliknij przycisk hello **ZAPISAĆ** przycisk na powitania dolny panel.
    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę uzyskać wygaszone i znajduje się w hello **oczekujących...**  stanu kilka minut. Po pewnym czasie domeny zarządzanej tooyour dostęp do Internetu za pośrednictwem bezpiecznego protokołu LDAP jest włączone.

    ![Bezpieczny protokół LDAP — stan oczekiwania](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Trwa około 10 minut dostęp do Internetu tooenable za pośrednictwem bezpiecznego protokołu LDAP do domeny zarządzanej.
   >
   >
4. Gdy bezpieczne tooyour dostępu LDAP zarządzane domeny przez internet został pomyślnie włączony hello, hello **oczekujących...**  powinien zniknąć wiadomości. Powinna zostać wyświetlona hello IP zewnętrznego adresu, który może być używane tooaccess katalogu za pośrednictwem LDAPS w polu hello **IP adres dla LDAPS dostępu zewnętrznego**.

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Zadanie 5 — konfigurowanie domeny zarządzanej hello tooaccess DNS z hello internet
**Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.

Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 4](#task-4---enable-secure-ldap-access-over-the-internet).

Po włączeniu bezpiecznego dostępu LDAP za pośrednictwem Internetu hello potrzeby domeny zarządzanej, należy tooupdate DNS tak, aby komputery klienckie można znaleźć tej domeny zarządzanej. Na końcu hello zadanie 4, zewnętrzny adres IP jest wyświetlany na powitania **Konfiguruj** karcie **IP adres dla LDAPS dostępu zewnętrznego**.

Konfigurowanie dostawcy usługi DNS zewnętrzne tej nazwy DNS hello hello zarządzane zewnętrzny adres IP toothis punktów domeny (na przykład "ldaps.contoso100.com"). W naszym przykładzie potrzebne są nam hello toocreate następującego wpisu DNS:

    ldaps.contoso100.com  -> 52.165.38.113

To wszystko — wszystko jest teraz gotowy tooconnect toohello zarządzane domeny przy użyciu bezpiecznego protokołu LDAP, za pośrednictwem hello internet.

> [!WARNING]
> Należy pamiętać, że komputery klienckie muszą ufać Witaj wystawca hello LDAPS certyfikatu toobe stanie tooconnect pomyślnie toohello zarządzane przy użyciu LDAPS domeny. Jeśli korzystasz z urzędu certyfikacji przedsiębiorstwa lub publicznie zaufany urząd certyfikacji, nie trzeba toodo niczego, ponieważ komputery klienckie ufać tych wystawców certyfikatów. Jeśli używasz certyfikatu z podpisem własnym należy tooinstall hello publicznego część hello certyfikatu z podpisem własnym do magazynu zaufanych certyfikatów hello na komputerze klienckim hello.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>LDAPS blokowanie dostępu tooyour domeny zarządzanej za pośrednictwem hello internet
> [!NOTE]
> **Opcjonalne zadania** — Jeśli nie włączono LDAPS domeny zarządzanej toohello dostępu ponad hello internet, pomiń to zadanie konfiguracji.
>
>

Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 4](#task-4---enable-secure-ldap-access-over-the-internet).

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
