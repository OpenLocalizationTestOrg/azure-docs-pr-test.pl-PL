---
title: "podręcznikowym ochronę tożsamości w usłudze Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Azure AD Identity Protection umożliwia zdolność hello toolimit tooexploit osoba atakująca, którego bezpieczeństwo zostało naruszone tożsamości lub urządzenie i toosecure tożsamości lub urządzenia, które wcześniej były toobe podejrzenia lub znanych naruszenia zabezpieczeń."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Azure podręcznikowym ochronę tożsamości w usłudze Active Directory
Tego podręcznika dotyczącego ułatwia:

* Wypełnij dane w środowisku Identity Protection hello symulowanie symulacje zdarzenia o podwyższonym ryzyku i luk w zabezpieczeniach
* Konfigurowanie zasad dostępu warunkowego opartego na ryzyko i testowanie wpływu hello tych zasad

## <a name="simulating-risk-events"></a>Symulacja zdarzeń o podwyższonym ryzyku
W tej sekcji przedstawiono kroki symulowanie hello następujące typy zdarzeń ryzyka:

* Logowania z anonimowych adresów IP (prosty)
* Logowania z nieznanych lokalizacji (umiarkowany)
* Niemożliwa podróż tooatypical lokalizacje (trudne)

Inne zdarzenia o podwyższonym ryzyku nie symulowane w bezpieczny sposób.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Logowania z anonimowych adresów IP
Ten typ zdarzenia ryzyka identyfikuje użytkowników, którzy zalogowali się pomyślnie z adresu IP, który został zidentyfikowany jako adres IP anonimowy serwer proxy. Te serwery proxy są używane przez osoby, które mają toohide adres IP swoich urządzeń i może służyć do złośliwymi działaniami.

**toosimulate logowania z anonimowych adresów IP, wykonaj następujące kroki hello**:

1. Pobierz hello [przeglądarki Tor](https://www.torproject.org/projects/torbrowser.html.en).
2. Przy użyciu przeglądarki Tor hello Przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Wprowadź poświadczenia hello hello konta tooappear w hello **logowania z anonimowych adresów IP** raportu.

Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 5 minut. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Logowania z nieznanych lokalizacji
Hello nieznanych lokalizacji ryzyko jest mechanizm oceny w czasie rzeczywistym logowania, który uwzględnia poza logowania w lokalizacji (IP, szerokości geograficznej / długości i ASN) toodetermine nowe / nieznanych lokalizacji. Hello system przechowuje poprzednie adresów IP, szerokości geograficznej / długości i numerów ASN użytkownika i traktuje te lokalizacje znanych toobe. Lokalizacja logowania jest uznawany za doświadczenia w pracy, jeśli hello lokalizacji logowania nie pasuje do żadnego z istniejącej lokalizacji znanych hello.

Ochrona tożsamości usługi Azure Active Directory:  

* ma okres learning początkowej 14 dni, w których nie Flaga wszelkie nowe lokalizacje jako nieznanych lokalizacji.
* ignoruje logowania z urządzeń znanych i lokalizacje, które są istniejącej lokalizacji znanych tooan geograficznie Zamknij.

toosimulate nieznanych lokalizacji i masz toosign w z lokalizacji i urządzenia, które konta hello nie zalogował się z przed. 

**toosimulate logowania z nieznanych lokalizacji, wykonaj hello następujące kroki**:

1. Wybierz konto, które ma co najmniej 14 dni historii logowania. 
2. Wykonaj jedną:
   
   a. Podczas korzystania z sieci VPN, przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com) i wprowadź poświadczenia hello hello konta toosimulate hello ryzyka zdarzenia.
   
   b. Poproś kojarzenie w innej lokalizacji toosign przy użyciu poświadczeń konta hello (niezalecane).

Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 5 minut.

### <a name="impossible-travel-tooatypical-location"></a>Niemożliwa podróż tooatypical lokalizacji
Symuluje warunku niemożliwa podróż hello jest trudne, ponieważ hello algorytm machine learning tooweed limit false alarmów, takich jak niemożliwa podróż ze znanych urządzeń lub logowania z sieci VPN, które są używane przez innych użytkowników w katalogu hello. Ponadto hello algorytm wymaga 3 dni too14 historię logowania dla użytkownika hello przed rozpoczęciem generowania zdarzeń o podwyższonym ryzyku.

**toosimulate niemożliwa podróż tooatypical lokalizacji, wykonaj hello następujące kroki**:

1. Za pomocą przeglądarki standardowe Przejdź zbyt[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Wprowadź poświadczenia hello hello konta, którego chcesz toogenerate niemożliwa podróż zdarzenie ryzyka dla.
3. Zmień agenta użytkownika. Można zmienić agenta użytkownika w programie Internet Explorer z Developer Tools, lub zmień agenta użytkownika przeglądarki Firefox lub Chrome przy użyciu dodatku przełącznik agenta użytkownika.
4. Zmienianie adresu IP. Adres IP można zmienić za pomocą sieci VPN, dodatek Tor, lub kręci się nowego komputera na platformie Azure w centrum danych.
5. Logowanie za[https://myapps.microsoft.com](https://myapps.microsoft.com) przy użyciu hello tych samych poświadczeń jako przed i za kilka minut po hello poprzedniej logowania.

Logowanie Hello będą widoczne na pulpicie nawigacyjnym Identity Protection hello w ciągu 2-4 godzin.<br>
Z powodu modeli zaangażowany uczenia maszynowego złożonych hello istnieje ryzyko, które nie ma pobrać pobierany się.<br> Możesz tooreplicate te kroki dla wielu kont usługi Azure AD.

## <a name="simulating-vulnerabilities"></a>Symuluje luk w zabezpieczeniach
Luki w zabezpieczeniach występują słabych w środowisku usługi Azure AD, które mogą być używane przez aktora nieprawidłowy. Obecnie 3 typy luk w zabezpieczeniach są udostępniane w Azure AD Identity Protection, zwiększają inne funkcje usługi Azure AD. Te luki w zabezpieczeniach zostanie wyświetlony na pulpicie nawigacyjnym Identity Protection hello automatycznie po skonfigurowaniu tych funkcji.

* Usługi Azure AD [uwierzytelnianie wieloskładnikowe?](../multi-factor-authentication/multi-factor-authentication.md)
* Usługi Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Usługi Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Ryzyko naruszenia zabezpieczeń użytkownika
**tootest ryzyko naruszenia zabezpieczeń użytkownika, wykonaj hello następujące kroki**:

1. Logowanie za[https://portal.azure.com](https://portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.
2. Przejdź za**Identity Protection**. 
3. Na powitania głównego **Azure AD Identity Protection** bloku, kliknij przycisk **ustawienia**. 
4. Na powitania **ustawienia portalu** bloku, w obszarze **reguły zabezpieczeń**, kliknij przycisk **ryzyko naruszenia zabezpieczeń użytkownika**. 
5. Na powitania **Zaloguj ryzyka** bloku, Włącz **Włącz regułę** wyłączone, a następnie kliknij przycisk **zapisać** ustawienia.
6. Symulowanie doświadczenia w pracy dla danego konta użytkownika, lokalizacji lub anonimowe zdarzenie ryzyka adresu IP. To spowoduje podniesienie poziomu hello poziom ryzyka użytkownika dla tego użytkownika za**średni**.
7. Poczekaj kilka minut, a następnie sprawdź tego poziomu użytkownika dla użytkownika jest **średni**.
8. Przejdź toohello **ustawienia portalu** bloku.
9. Na powitania **ryzyko naruszenia zabezpieczeń użytkownika** bloku, w obszarze **Włącz regułę**, wybierz pozycję **na** . 
10. Wybierz jedną z hello następujące opcje:
    
    a. tooblock, wybierz opcję **średni** w obszarze **Zaloguj bloku**.
    
    b. tooenforce zmiany bezpieczne hasło, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.
11. Kliknij pozycję **Zapisz**.
12. Teraz możesz przetestować dostępu warunkowego opartego na ryzyko, logując się przy użyciu użytkownik z poziomem ryzyka z podwyższonym poziomem uprawnień. Hello użytkownika ryzykiem w przypadku średniej, w zależności od konfiguracji hello zgodnie z zasadami, logowanie jest albo zablokowania lub zostało wymuszone toochange Twojego hasła. 
    <br><br>
    ![Podręcznikowym](./media/active-directory-identityprotection-playbook/201.png "Podręcznikowym")
    <br>

## <a name="sign-in-risk"></a>Ryzyko logowania
**tootest logowania ryzyko, należy wykonać hello następujące kroki:**

1. Logowanie za[https://portal.azure.com ](https://portal.azure.com) przy użyciu poświadczeń administratora globalnego dla dzierżawy.
2. Przejdź za**Identity Protection**.
3. Na powitania głównego **Azure AD Identity Protection** bloku, kliknij przycisk **ustawienia**. 
4. Na powitania **ustawienia portalu** bloku, w obszarze **reguły zabezpieczeń**, kliknij przycisk **Zaloguj ryzyka**.
5. Na powitania ** Zaloguj ryzyka ** bloku, wybierz opcję **na** w obszarze **Włącz regułę**. 
6. Wybierz jedną z hello następujące opcje:
   
   a. tooblock, wybierz opcję **średni** w obszarze **bloku Zaloguj**
   
   b. tooenforce zmiany bezpieczne hasło, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.
7. tooblock, wybierz nośnik w bloku logowania.
8. uwierzytelnianie wieloskładnikowe tooenforce, wybierz opcję **średni** w obszarze **wymusić uwierzytelnianie wieloskładnikowe**.
9. Kliknij przycisk **Zapisz**.
10. Teraz możesz przetestować dostępu warunkowego opartego na ryzyko symulując hello nieznanych lokalizacji lub anonimowe IP ryzyka zdarzeń, ponieważ są one zarówno **średni** ryzyka zdarzenia.


![Podręcznikowym](./media/active-directory-identityprotection-playbook/200.png "Podręcznikowym")


## <a name="see-also"></a>Zobacz też
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md)

