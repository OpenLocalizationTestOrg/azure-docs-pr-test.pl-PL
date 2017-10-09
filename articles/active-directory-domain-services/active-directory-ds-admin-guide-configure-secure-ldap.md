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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD
W tym artykule opisano, jak można włączyć bezpieczny Lightweight Directory dostępu protokołu (LDAPS) dla domeny zarządzanej usług domenowych Azure AD. Bezpiecznego protokołu LDAP jest także znana jako "dostępu protokołu LDAP (Lightweight Directory) za pośrednictwem Secure Sockets Layer (SSL) / zabezpieczeń TLS (Transport Layer)".

## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).
4. A **tooenable toobe używany certyfikat bezpieczny protokół LDAP**.

   * **Zalecane** -uzyskać certyfikat od zaufanego publicznego urzędu certyfikacji. Ta opcja konfiguracji jest bardziej bezpieczne.
   * Alternatywnie można też zbyt[Utwórz certyfikat z podpisem własnym](#task-1---obtain-a-certificate-for-secure-ldap) jak pokazano w dalszej części tego artykułu.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Wymagania dotyczące bezpiecznego certyfikatu LDAP hello
Uzyskać prawidłowy certyfikat na powitania następujące wytyczne, przed włączeniem bezpiecznego protokołu LDAP. Wystąpią błędy, Jeśli spróbujesz tooenable bezpieczny protokół LDAP do domeny zarządzanej za pomocą certyfikatu nieprawidłowa lub być niepoprawne.

1. **Zaufanych wystawców** -hello certyfikat musi być wystawiony przez urząd certyfikacji zaufany przez komputery łączenie toohello domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP. Ten urząd może być publiczny urząd certyfikacji zaufany przez te komputery.
2. **Okres istnienia** -hello certyfikatu musi być prawidłowy dla co najmniej hello kolejnych 3 – 6 miesięcy. Bezpieczne LDAP dostępu tooyour domeny zarządzanej jest zakłócona po wygaśnięciu certyfikatu hello.
3. **Nazwa podmiotu** -hello nazwa podmiotu certyfikatu hello musi być symbolem wieloznacznym dla domeny zarządzanej. Na przykład, jeśli domena ma nazwę "contoso100.com", nazwa podmiotu certyfikatu hello musi być "*. contoso100.com". Ustaw hello DNS (alternatywnej nazwy podmiotu) toothis symbolu wieloznacznego nazwa.
4. **Użycie klucza** - hello certyfikat musi być skonfigurowany dla używa powitania po - podpisy cyfrowe i szyfrowanie klucza.
5. **Cel certyfikatu** -hello certyfikatu musi być prawidłowy do uwierzytelniania serwera SSL.

> [!NOTE]
> **Urzędy certyfikacji przedsiębiorstwa:** usługi domenowe Azure AD nie obsługuje korzystania z bezpiecznego certyfikatów LDAP wystawiony przez urząd certyfikacji przedsiębiorstwa w organizacji. To ograniczenie obowiązuje, ponieważ hello usługi nie jest zaufany urząd certyfikacji jako główny urząd certyfikacji przedsiębiorstwa. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP
pierwszym zadaniem Hello obejmuje uzyskiwanie certyfikatu używany do bezpiecznego LDAP dostępu toohello domeny zarządzanej. Dostępne są dwie opcje:

* Uzyskaj certyfikat od urzędu certyfikacji. Urząd Hello może być publiczny urząd certyfikacji.
* Tworzenie certyfikatu z podpisem własnym.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Opcja (zalecane) — Uzyskaj certyfikat bezpiecznego LDAP z urzędu certyfikacji
Jeśli Twoja organizacja uzyskuje jego certyfikatów z publicznego urzędu certyfikacji, należy tooobtain hello bezpiecznego LDAP certyfikatu z tym publicznego urzędu certyfikacji.

Podczas żądania certyfikatu, upewnij się, że spełniają wszystkie wymagania hello opisane w temacie [wymagania dotyczące bezpiecznego certyfikatu LDAP hello](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Komputery klienckie, które wymagają tooconnect toohello domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP muszą ufać Witaj wystawca hello bezpiecznego LDAP certyfikatu.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Opcja B - Tworzenie certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP
Jeśli nie planujesz toouse certyfikatów z publicznego urzędu certyfikacji, można wybrać toocreate certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP.

**Tworzenie certyfikatu z podpisem własnym za pomocą programu PowerShell**

Na komputerze z systemem Windows, Otwórz nowe okno programu PowerShell jako **administratora** i typ hello następujące polecenia, toocreate nowego certyfikatu z podpisem własnym.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

W powyższej przykładowej hello, zastąp "*. contoso100.com" z nazwą domeny DNS hello domeny zarządzanej. For example, jeśli utworzono o nazwie "contoso100.onmicrosoft.com" domeny zarządzanej, zastąp "*. contoso100.com" w hello powyżej skryptu "*. contoso100.onmicrosoft.com").

![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

Witaj nowo utworzonego certyfikatu z podpisem własnym znajduje się w magazynie certyfikatów komputera lokalnego hello.


## <a name="next-step"></a>Następny krok
[Zadanie 2 — wyeksportować hello bezpiecznego tooa certyfikatu LDAP. Plik PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
