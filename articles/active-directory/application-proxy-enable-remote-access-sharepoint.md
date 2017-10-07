---
title: "aaaEnable tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstawy temat toointegrate lokalnego serwera programu SharePoint z serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Włącz tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD

W tym artykule omówiono sposób toointegrate lokalnego serwera programu SharePoint przy użyciu serwera Proxy aplikacji usługi Azure Active Directory (Azure AD).

tooenable tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD, należy wykonać hello sekcje w tym artykule krok po kroku.

## <a name="prerequisites"></a>Wymagania wstępne

W tym artykule założono, że już programu SharePoint 2013 lub nowszej w danym środowisku. Ponadto należy wziąć pod uwagę następujące wymagania wstępne hello:

* SharePoint obejmuje natywnej obsługi protokołu Kerberos. W związku z tym użytkownicy, którzy uzyskują dostęp do wewnętrznych witryn zdalnie za pośrednictwem serwera Proxy aplikacji usługi Azure AD można założyć toohave rejestracji jednokrotnej (SSO) wystąpić.

* Należy toomake kilka serwera SharePoint tooyour zmian konfiguracji. Firma Microsoft zaleca używanie środowiska przemieszczania. W ten sposób można dokonać aktualizacji tooyour najpierw przemieszczania serwera i następnie ułatwienia testowania cyklu przed przejściem do środowiska produkcyjnego.

* Przyjęto założenie, że już skonfigurowano protokół SSL dla programu SharePoint, ponieważ firma Microsoft wymaga protokołu SSL na powitania opublikowany adresu URL. Należy toohave włączony protokół SSL w witrynie wewnętrzny tooensure czy łącza są wysyłane/prawidłowo zamapowane. Jeśli nie skonfigurowano protokół SSL, zobacz [skonfigurować protokół SSL dla programu SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) instrukcje. Upewnij się również, tym hello łącznika maszyny zaufania hello certyfikat wystawiane. (hello certyfikat nie musi toobe publicznie wydanych).

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Krok 1: Konfigurowanie tooSharePoint rejestracji jednokrotnej

Naszym klientom mają hello najlepszych funkcji rejestracji jednokrotnej dla swoich aplikacji zaplecza programu SharePoint server w takim przypadku. Ten częsty scenariusz usługi Azure AD hello użytkownik jest uwierzytelniany tylko raz, ponieważ nie zostanie wyświetlony monit dla uwierzytelniania ponownie.

Dla aplikacji lokalnych, które wymagają lub uwierzytelniania systemu Windows można osiągnąć logowania jednokrotnego przy użyciu protokołu uwierzytelniania Kerberos hello i funkcję ograniczonego delegowania protokołu Kerberos (KCD). Delegowanie KCD, po skonfigurowaniu umożliwia tooobtain łącznika serwera Proxy aplikacji hello systemu windows biletu/token dla użytkownika, nawet jeśli hello użytkownik nie zalogował się tooWindows bezpośrednio. toolearn więcej informacji na temat KCD, zobacz [omówienie delegowania ograniczonego protokołu Kerberos](https://technet.microsoft.com/library/jj553400.aspx).

tooset się KCD programu SharePoint server, użyj procedury hello powitania po kolejnych sekcjach:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Upewnij się, że SharePoint działa w ramach konta usługi

Najpierw upewnij się, że SharePoint działa w ramach konta usługi zdefiniowanych — system lokalny, Usługa lokalna lub Usługa sieciowa. W tym tak, aby dołączyć prawidłowe konto tooa nazwy podmiotu zabezpieczeń (SPN) usługi. Nazwy SPN są jak hello protokołu Kerberos identyfikuje różnych usług. I będzie konieczne hello konta nowsze hello tooconfigure KCD.

tooensure witryn uruchomionych na koncie usługi zdefiniowane, należy wykonać hello następujące kroki:

1. Otwórz hello **Administracja centralna programu SharePoint 2013** lokacji.
2. Przejdź za**zabezpieczeń** i wybierz **Konfigurowanie kont usług**.
3. Wybierz **— SharePoint — 80. pula aplikacji sieci Web**. Opcje Hello mogą być nieco inne na podstawie nazwy hello puli sieci web, lub jeśli hello puli sieci web używa protokołu SSL, domyślnie.

  ![Opcje dotyczące konfigurowania konta usługi](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Jeśli **wybierz konto dla tego składnika** jest **Usługa lokalna** lub **usługi sieciowej**, należy toocreate konta. Jeśli nie, zakończeniu i przenieść toohello następnej sekcji.
5. Wybierz **rejestrowanie nowego zarządzanego konta**. Po utworzeniu konta, musisz ustawić **puli aplikacji sieci Web** przed użyciem hello konta.

> [!NOTE]
Należy toohave a wcześniej utworzone konto usługi Azure AD dla usługi hello. Zalecamy, aby umożliwić automatyczne zmienianie hasła. Aby uzyskać więcej informacji o hello pełny zestaw kroków i rozwiązywanie problemów, zobacz [skonfigurować automatyczne zmienianie hasła w programie SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Konfigurowanie programu SharePoint dla protokołu Kerberos

Użyj KCD tooperform pojedynczego logowania jednokrotnego toohello programu SharePoint server, a to działa tylko przy użyciu protokołu Kerberos.

tooconfigure witryny programu SharePoint do uwierzytelniania protokołu Kerberos:

1. Otwórz hello **Administracja centralna programu SharePoint 2013** lokacji.
2. Przejdź za**Zarządzanie aplikacjami**, wybierz pozycję **zarządzania aplikacjami sieci web**i wybierz pozycję witryny programu SharePoint. W tym przykładzie jest **SharePoint — 80**.

  ![Wybieranie hello witryny programu SharePoint](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Kliknij przycisk **dostawców uwierzytelniania** na powitania narzędzi.
4. W hello **dostawców uwierzytelniania** kliknij **strefa domyślna** tooview hello ustawienia.
5. W hello **Edytuj uwierzytelnianie** okno dialogowe pola, przewiń w dół, aż zostanie wyświetlony **typy uwierzytelniania oświadczeń** i upewnij się, że oba **włączyć uwierzytelnianie systemu Windows** i  **Zintegrowane uwierzytelnianie systemu Windows** są wybrane.
6. Upewnij się, że w polu listy rozwijanej hello **Negotiate (Kerberos)** jest zaznaczone.

  ![Okno dialogowe Edytowanie uwierzytelniania](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. U dołu hello hello **Edytuj uwierzytelnianie** okno dialogowe, kliknij przycisk **zapisać**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Ustaw nazwę główną usługi dla hello konto usługi programu SharePoint

Przed skonfigurowaniem hello KCD należy usługi SharePoint hello tooidentify uruchomione jako konto usługi hello, który został skonfigurowany. Można to zrobić przez ustawienie Nazwa SPN. Aby uzyskać więcej informacji, zobacz [główne nazwy usług](https://technet.microsoft.com/library/cc961723.aspx).

format nazwy SPN Hello jest:

```
<service class>/<host>:<port>
```

Format nazwy SPN hello:

* _usługi klasy_ jest unikatową nazwą hello usługi. Dla programu SharePoint, możesz użyć **HTTP**.

* _host_ jest hello FQDN lub nazwę NetBIOS hello hosta, który hello usługa jest uruchomiona na. Witryny programu SharePoint ten tekst może być konieczne toobe hello adres URL witryny hello, w zależności od wersji hello usług IIS, którego używasz.

* _port_ jest opcjonalna.

Jeśli hello nazwę FQDN serwera SharePoint hello jest:

```
sharepoint.demo.o365identity.us
```

Następnie hello SPN jest:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Konieczne może również tooset SPN dla określonych witryn na serwerze. Aby uzyskać więcej informacji, zobacz [uwierzytelnianie Kerberos skonfigurować](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Należy zwrócić szczególną uwagę toohello sekcji "Tworzenie główne nazwy usług dla aplikacji sieci Web przy użyciu uwierzytelniania Kerberos."

Hello najprościej tooset SPN jest toofollow hello SPN formatów, które mogą być już dostępne dla witryny. Skopiuj te tooregister SPN konta usługi hello. toodo to:

1. Przeglądaj witrynę toohello z hello SPN z innego komputera.
 Gdy hello odpowiedniego zbioru bilety Kerberos są buforowane na powitania maszyny. Bilety zawierają hello SPN hello lokacji docelowej, które zostały wybrane.

2. Hello SPN dla tej lokacji można pobierać za pomocą narzędzie [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). W oknie polecenia działającej w hello tego samego kontekstu jako użytkownik hello hello używanych witryn w przeglądarce hello, uruchom hello następujące polecenie:
```
Klist
```
Klist zwraca zbiór hello docelowej nazw SPN. W tym przykładzie wartość hello wyróżnione jest hello głównej nazwy usługi, które ma potrzebne:

  ![Przykład Klist wyników](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Teraz, gdy masz hello głównej nazwy usługi, należy się upewnić, że został on poprawnie skonfigurowany na koncie usługi hello skonfigurowanego dla aplikacji sieci web hello wcześniej toomake. Uruchom następujące polecenie w wierszu polecenia hello jako administrator domeny hello hello:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 To polecenie ustawia hello SPN dla usługi SharePoint hello konta uruchomiony jako _demo\sp_svc_.

 Zastąp _http/sharepoint.demo.o365identity.us_ z hello SPN serwera i _demo\sp_svc_ z kontem usługi hello w danym środowisku. polecenia Setspn Hello wyszukuje hello SPN, przed dodaniem go. W takim przypadku można napotkać **zduplikowane wartości nazwy SPN** błędu. Jeśli zostanie wyświetlony ten błąd, upewnij się, że wartość hello jest skojarzony z kontem usługi hello.

Możesz zweryfikować tego hello dodania nazwy SPN, uruchamiając polecenia Setspn hello z opcją -l hello. toolearn więcej informacji na temat tego polecenia, zobacz [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Upewnij się, że ten łącznik hello jest ustawiony jako tooSharePoint zaufanych delegata

Witaj KCD należy skonfigurować, tak aby hello usługi serwera Proxy aplikacji usługi Azure AD można delegować usługi SharePoint toohello tożsamości użytkownika. Aby to zrobić, włączenie łącznika serwera Proxy aplikacji hello biletów Kerberos tooretrieve dla użytkowników, którzy zostali uwierzytelnieni w usłudze Azure AD. Następnie ten serwer aplikacji docelowej toohello kontekstu hello lub SharePoint w takim przypadku.

Witaj tooconfigure KCD, powtórz hello następujące kroki dla każdego komputera łącznika:

1. Zaloguj się jako tooa administratora domeny, kontrolera domeny, a następnie otwórz **użytkownicy usługi Active Directory i komputery**.
2. Znajdź hello komputera, na którym hello łącznika jest uruchomiona na. W tym przykładzie go ma hello sam serwer programu SharePoint.
3. Kliknij dwukrotnie ikonę hello komputer, a następnie kliknij przycisk hello **delegowania** kartę.
4. Upewnij się, że ustawienia delegowania hello są ustawiane za**Ufaj temu komputerowi w toohello delegowania określonych usług tylko**, a następnie wybierz **Użyj dowolnego protokołu uwierzytelniania**.

  ![Ustawienia delegowania](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Kliknij przycisk hello **Dodaj** , kliknij **użytkowników lub komputerów**i Znajdź hello konta usługi.

  ![Dodawanie hello SPN konta usługi hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Hello listy nazw SPN wybierz hello został utworzony wcześniej hello konta usługi.
7. Kliknij przycisk **OK**. Kliknij przycisk **OK** ponownie toosave hello zmiany.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Krok 2: Włączanie tooSharePoint dostępu zdalnego

Została włączona programu SharePoint dla protokołu Kerberos i skonfigurowana KCD, możesz gotowe tooset się tooSharePoint rejestracji jednokrotnej. Następnie z łącznika hello można opublikować hello farmy programu SharePoint dla dostępu zdalnego za pośrednictwem serwera Proxy aplikacji usługi Azure AD.

Witaj tooperform następujące kroki, należy toobe członkiem hello rola administratora globalnego w organizacji konta usługi Azure Active Directory.

1. Zaloguj się toohello [portalu Azure](https://manage.windowsazure.com) i Znajdź dzierżawy usługi Azure AD.
2. Kliknij przycisk **aplikacji**, a następnie kliknij przycisk **Dodaj**.
3. Wybierz pozycję **Opublikuj aplikację dostępną spoza sieci**. Jeśli nie widzisz tej opcji upewnij się, że masz Azure AD podstawowa lub Premium, skonfiguruj w dzierżawie powitalnych.
4. Wykonaj każdą z opcji hello w następujący sposób:
 * **Nazwa**: Użyj żadnej wartości, które mają — na przykład **SharePoint**.
 * **Wewnętrzny adres URL**: jest to adres URL witryny SharePoint hello hello wewnętrznie, takich jak **https://SharePoint/**. W tym przykładzie, upewnij się, że toouse **https**.
 * **Metoda uwierzytelniania wstępnego**: Wybierz **usługi Azure Active Directory**.

  ![Opcje dodawania aplikacji](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Po opublikowaniu aplikacji hello kliknij hello **Konfiguruj** kartę.
6. Przewiń w dół opcji toohello **translacji adresów URL w nagłówkach**. Witaj, wartość domyślna to **tak**. Zmień ją za**nr**.

 SharePoint używa hello _nagłówek hosta_ toolook wartość hello witrynę. Generuje on również linki, na podstawie tej wartości. Efekt netto Hello jest toomake się, że każde łącze, które generuje programu SharePoint jest opublikowane adres URL, który jest ustawiony prawidłowo toouse hello zewnętrznego adresu URL. Ustawienie wartości hello zbyt**tak** również umożliwia hello łącznika tooforward hello żądania toohello zaplecza aplikacji. Jednak ustawienie wartości hello zbyt**nr** oznacza, że hello łącznik nie będzie wysyłać hello nazwy wewnętrznej hosta. Zamiast tego łącznika hello wysyła nagłówek hosta hello hello opublikowanych aplikacji zaplecza toohello adresu URL.

 Tooensure również, że SharePoint akceptuje ten adres URL należy toocomplete jeden dodatkowych czynności konfiguracyjnych na powitania serwera programu SharePoint. Należy to zrobić w następnej sekcji hello.

7. Zmień **metody uwierzytelniania wewnętrznego** za**zintegrowane uwierzytelnianie systemu Windows**. Jeśli dzierżawy usługi Azure AD używa nazwy UPN w chmurze hello, która różni się od hello UPN lokalnie, należy pamiętać o tooupdate **delegowane tożsamości logowania** również.
8. Ustaw **wewnętrzny SPN aplikacji** toohello wartość ustawiona wcześniej. Na przykład użyć **http/sharepoint.demo.o365identity.us**.
9. Przypisz tooyour aplikacji hello użytkowników docelowych.

Aplikacja powinna wyglądać podobnie toohello poniższy przykład:

  ![Zakończono aplikacji](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Krok 3: Upewnij się, że zna hello zewnętrznego adresu URL programu SharePoint

Z ostatnich tooensure krok, który programu SharePoint można znaleźć hello witryny opartej na powitania zewnętrzny adres URL, dzięki czemu będą zawierały łącza na podstawie tego zewnętrznego adresu URL. W tym celu Konfigurowanie mapowań dostępu alternatywnego hello witryny programu SharePoint.

1. Otwórz hello **Administracja centralna programu SharePoint 2013** lokacji.
2. W obszarze **ustawienia systemu**, wybierz pozycję **Konfigurowanie mapowań dostępu alternatywnego**.

 Spowoduje to otwarcie hello **mapowań dostępu alternatywnego** pole.

  ![Pole mapowań dostępu alternatywnego](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Hello listy rozwijanej obok **kolekcji mapowania dostępu alternatywnego**, wybierz pozycję **zmiany alternatywnego dostępu mapowania kolekcji**.
4. Wybierz lokację — na przykład **SharePoint — 80**.

  ![Wybieranie lokacji](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Można wybrać tooadd hello opublikowany adresu URL jako wewnętrzny adres URL lub publiczny adres URL. W tym przykładzie używa publicznego adresu URL jako hello ekstranetu.
6. Kliknij przycisk **Edytuj publiczne adresy URL** w hello **ekstranet** ścieżki, a następnie wprowadź hello ścieżkę hello opublikowane aplikacji, jak w poprzednim kroku hello. Na przykład wprowadź **https://sharepoint-iddemo.msappproxy.net**.

  ![Wprowadzanie ścieżki hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Kliknij pozycję **Zapisz**.

 Można teraz uzyskać dostęp do witryny programu SharePoint hello zewnętrznie za pośrednictwem serwera Proxy aplikacji usługi Azure AD.

## <a name="next-steps"></a>Następne kroki

- [Jak tooprovide bezpiecznego dostępu zdalnego tooon lokalnej aplikacji](active-directory-application-proxy-get-started.md)
- [Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
- [Publikowanie programu SharePoint 2016 i Office Online serwera za pomocą serwera Proxy aplikacji usługi Azure AD](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
