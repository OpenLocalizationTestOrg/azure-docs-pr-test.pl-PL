---
title: "Łączenie wielu domen aaaAzure AD"
description: "W tym dokumencie opisano instalowanie i konfigurowanie wielu domen najwyższego poziomu z usługi Office 365 i Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Obsługa wielu domen do federowania w usłudze Azure AD
Witaj następująca dokumentacja znajdują się wskazówki dotyczące toouse wiele domen najwyższego poziomu i poddomen podczas federowania z domenami usługi Office 365 lub Azure AD.

## <a name="multiple-top-level-domain-support"></a>Obsługa wielu domen najwyższego poziomu
Federowanie wielu, domeny najwyższego poziomu z usługą Azure AD wymaga dodatkowego skonfigurowania, który nie jest wymagany, gdy federowania z jednej domeny najwyższego poziomu.

Gdy domeny jest Sfederowane przy użyciu usługi Azure AD, kilka właściwości są ustawiane na powitania domeny na platformie Azure.  Jeden z nich ważne jest IssuerUri.  Jest to identyfikator URI, który jest używany przez usługi Azure AD tooidentify jest skojarzony z domeny hello hello tokenu.  Witaj identyfikatora URI nie musi tooresolve tooanything, ale musi być prawidłowym identyfikatorem URI.  Domyślnie usługi Azure AD ustawia wartość toohello identyfikator usługi federacyjnej hello w lokalnej usługi AD FS konfiguracji.

> [!NOTE]
> Identyfikator usługi federacyjnej Hello jest identyfikatorem URI, który unikatowo identyfikuje usługi federacyjnej.  Usługa federacyjna Hello jest wystąpienia usług AD FS tej funkcji jako hello usługi tokenu zabezpieczającego. 
> 
> 

Można wyświetlić IssuerUri za pomocą polecenia programu PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Problem występuje, gdy chcemy tooadd więcej niż jednej domeny najwyższego poziomu.  Na przykład, załóżmy, że masz konfiguracji federacji między usługą Azure AD oraz w lokalnym środowisku.  W tym dokumencie używam bmcontoso.com.  Po dodaniu drugiego najwyższego poziomu domeny, bmfabrikam.com.

![Domeny](./media/active-directory-multiple-domains/domains.png)

Gdy firma Microsoft spróbuje tooconvert naszych toobe domeny bmfabrikam.com federacyjnych, możemy komunikat o błędzie.  Witaj przyczyną tego błędu jest, usługa Azure AD ma ograniczenie, które nie zezwala na powitania hello toohave właściwości IssuerUri samą wartość dla więcej niż jedną domenę.  

![Błąd federacyjnego](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parametr SupportMultipleDomain
tooworkaround, potrzebujemy tooadd różnych IssuerUri, można to zrobić za pomocą hello `-SupportMultipleDomain` parametru.  Ten parametr jest używany z hello następującego polecenia cmdlet:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Ten parametr umożliwia usługi Azure AD, skonfiguruj hello IssuerUri, dzięki czemu jest on oparty na powitania nazwę domeny hello.  Są to unikatowy między katalogów w usłudze Azure AD.  Za pomocą parametru hello umożliwia toocomplete polecenia programu PowerShell hello pomyślnie.

![Błąd federacyjnego](./media/active-directory-multiple-domains/convert.png)

Patrzeć hello ustawienia naszej nowej domeny bmfabrikam.com można wyświetlić następujące hello:

![Błąd federacyjnego](./media/active-directory-multiple-domains/settings.png)

Należy pamiętać, że `-SupportMultipleDomain` hello nie powoduje zmiany innych punktów końcowych, które są nadal skonfigurowane usługi federacyjnej tooour toopoint na adfs.bmcontoso.com.

Innym czynnikiem który `-SupportMultipleDomain` jest jest ona sprawdza, czy hello AD FS systemu zawiera poprawną wartość wystawcy hello w tokenów wystawionych dla usługi Azure AD. Robi to przez pobranie hello domeny część użytkowników hello UPN i to ustawienie jako domeny hello w hello IssuerUri, tj. sufiks https://{upn} / adfs/services/zaufania. 

W związku z tym podczas uwierzytelniania tooAzure AD lub usługi Office 365, element IssuerUri hello w tokenie użytkownika hello jest używane toolocate hello domeny w usłudze Azure AD.  Jeśli nie można odnaleźć dopasowania, uwierzytelniania hello zakończą się niepowodzeniem. 

Na przykład, jeśli nazwy UPN użytkownika jest bsimon@bmcontoso.com, element IssuerUri hello hello tokenu usług AD FS problemy zostaną ustawione toohttp://bmcontoso.com/adfs/services/trust. To będzie odpowiadała konfiguracji usługi Azure AD hello i uwierzytelniania powiedzie się.

następujące Hello jest reguły oświadczeń dostosowane hello, który implementuje tę logikę:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> W kolejności toouse hello - SupportMultipleDomain Przełącz podczas próby tooadd nowych lub przekonwertować już dodane domeny, konieczne toohave Instalatora toosupport Twojego zaufania federacyjnego pierwotnie je.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Jak tooupdate hello zaufania między usługami AD FS a usługą Azure AD
Jeśli nie uaktualniono konfiguracji hello federacyjnych zaufania między usługami AD FS a wystąpieniem usługi Azure AD, może być konieczne toore-tworzenia tego zaufania.  To dlatego, gdy została pierwotnie bez hello `-SupportMultipleDomain` parametru hello IssuerUri jest ustawiona z wartością domyślną hello.  W hello zrzut ekranu poniżej można zauważyć, że hello IssuerUri ustawiono toohttps://adfs.bmcontoso.com/adfs/services/trust.

Teraz tak, jeśli firma Microsoft pomyślnie dodano nową domenę w portalu hello Azure AD, a następnie spróbuj tooconvert za pomocą `Convert-MsolDomaintoFederated -DomainName <your domain>`, uzyskujemy hello następujący błąd.

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust1.png)

Jeśli spróbujesz tooadd hello `-SupportMultipleDomain` przełącznika będzie Otrzymaliśmy hello następujący błąd:

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust2.png)

Po prostu próby toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` na powitania pierwotnej domeny również spowoduje błąd.

![Błąd federacyjnego](./media/active-directory-multiple-domains/trust3.png)

Wykonaj kroki hello poniżej tooadd dodatkowej domeny najwyższego poziomu.  Jeśli dodano już domeny i nie użyto hello `-SupportMultipleDomain` start parametru hello prostych kroków, usuwania i aktualizowania domenę oryginalnego.  Jeśli domeny najwyższego poziomu nie dodano jeszcze można uruchomić z poziomu hello kroki dodawania domeny przy użyciu programu PowerShell Azure AD Connect.

Użyj hello następujące kroki tooremove hello Online firmy Microsoft zaufania i zaktualizuj domenę oryginalnego.

1. Na serwerze federacyjnym usług AD FS Otwórz **Zarządzanie usługami AD FS.** 
2. Na powitania po lewej stronie rozwiń **relacje zaufania** i **zaufania jednostek uzależnionych**
3. Na powitania prawo, usunąć hello **Microsoft Office 365 tożsamość platformy** wpisu.
   ![Usuń Online firmy Microsoft](./media/active-directory-multiple-domains/trust4.png)
4. Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące hello: `$cred=Get-Credential`.  
5. Wprowadź hello użytkownika i hasło administratora globalnego dla domeny usługi Azure AD hello federowania w usłudze
6. W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`
7. W programie PowerShell wpisz `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Jest to hello pierwotnej domeny.  Za pomocą hello powyżej domen, które będzie:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Użyj hello następujące kroki tooadd hello nowej domeny najwyższego poziomu przy użyciu programu PowerShell

1. Na komputerze, na którym ma [Azure Active Directory modułu dla środowiska Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) zainstalowanym uruchom następujące hello: `$cred=Get-Credential`.  
2. Wprowadź hello użytkownika i hasło administratora globalnego dla domeny usługi Azure AD hello federowania w usłudze
3. W programie PowerShell wpisz:`Connect-MsolService -Credential $cred`
4. W programie PowerShell wpisz:`New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Użyj następujących hello kroki tooadd hello nowej domeny najwyższego poziomu za pomocą usługi Azure AD Connect.

1. Uruchamianie usługi Azure AD Connect z pulpitu hello lub menu start
2. Wybierz opcję "Dodaj dodatkowe domenowych Azure AD" ![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add1.png)
3. Wprowadź usługi Azure AD i poświadczeń usługi Active Directory
4. Wybierz domenę drugi hello mają tooconfigure dla Federacji.
   ![Dodawanie kolejnej domeny usługi Azure AD](./media/active-directory-multiple-domains/add2.png)
5. Kliknij przycisk Instaluj

### <a name="verify-hello-new-top-level-domain"></a>Sprawdź hello nowej domeny najwyższego poziomu
Za pomocą polecenia programu PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`można wyświetlić hello zaktualizowane IssuerUri.  Poniższy zrzut ekranu Hello pokazuje ustawienia Federacji hello zostały zaktualizowane na naszych oryginalnego http://bmcontoso.com/adfs/services/trust domeny

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Witaj IssuerUri naszej nowej domeny skonfigurowano toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Obsługa domen podrzędnych
Podczas dodawania domeny podrzędnej z powodu hello sposób usługi Azure AD obsługiwane domen, a będzie dziedziczyć ustawień hello hello nadrzędnej.  Oznacza to, że hello IssuerUri musi toomatch hello nadrzędnych.

Dlatego umożliwia Powiedz, na przykład, że I bmcontoso.com i następnie dodać corp.bmcontoso.com.  Oznacza to, że ten hello IssuerUri do użytkownika z corp.bmcontoso.com należy toobe **http://bmcontoso.com/adfs/services/trust.**  Jednak zaimplementowana reguła standardowe hello powyżej dla usługi Azure AD, spowoduje wygenerowanie tokenu z wystawcą jako **http://corp.bmcontoso.com/adfs/services/trust.** nie będzie odpowiadała wymaganej wartości hello domeny i uwierzytelnianie zakończy się niepowodzeniem.

### <a name="how-tooenable-support-for-sub-domains"></a>Jak tooenable obsługę poddomen
W kolejności toowork wokół tego hello usług AD FS dla witryny Microsoft Online zaufanie jednostki uzależnionej musi toobe aktualizacji.  toodo, niestandardowej reguły oświadczeń należy skonfigurować tak, aby taśmy Wyłącz wszelkie poddomen z sufiksem nazwy UPN użytkownika hello podczas konstruowania hello niestandardowej wartości wystawcy. 

Witaj następujące oświadczenie będzie wykonaj następujące czynności:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
numer ostatniej Hello w wyrażeniu regularnym hello ustawić hello ile domeny nadrzędnej istnieje w domenie katalogu głównego. W tym miejscu można mieć bmcontoso.com, niezbędne są dwie domeny nadrzędnej. Jeśli trzy nadrzędnego domeny zostały zachowane toobe (tj.: corp.bmcontoso.com), następnie numer hello byłby trzy. Mogą być wskazywane Eventualy zakresu, zawsze będą dopasowania hello toomatch hello maksymalna liczba domen. "{2,3}" będzie odpowiadała dwie domeny toothree (np.: bmfabrikam.com i corp.bmcontoso.com).

Użyj następujących hello kroki tooadd domenami podrzędnymi toosupport oświadczenia niestandardowego.

1. Zarządzanie usługami Otwórz AD FS
2. Zaufania Microsoft Online RP powitania kliknij prawym przyciskiem myszy i wybierz polecenie reguły Edycja oświadczeń
3. Wybierz hello trzeci reguły oświadczeń i Zastąp ![Edycja oświadczeń](./media/active-directory-multiple-domains/sub1.png)
4. Zastąp bieżący oświadczeń hello:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Zastąp oświadczeń](./media/active-directory-multiple-domains/sub2.png)

5. Kliknij przycisk Ok.  Kliknij przycisk Zastosuj.  Kliknij przycisk Ok.  Zamknij przystawkę zarządzania usługami AD FS.

