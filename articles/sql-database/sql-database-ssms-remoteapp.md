---
title: "tooSQL aaaConnect bazy danych przy użyciu programu SQL Server Management Studio w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Jak korzystać z tego samouczka toolearn toouse programu SQL Server Management Studio w usłudze Azure RemoteApp zabezpieczeń i wydajności podczas łączenia tooSQL bazy danych"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Użyj programu SQL Server Management Studio w usłudze Azure RemoteApp tooconnect tooSQL bazy danych

> [!IMPORTANT]
> Usługa Azure RemoteApp nie jest już obsługiwana. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
>

## <a name="introduction"></a>Wprowadzenie
W tym samouczku przedstawiono sposób toouse programu SQL Server Management Studio (SSMS) w usłudze Azure RemoteApp tooconnect tooSQL bazy danych. Go przeprowadzi Cię przez proces hello konfigurowania programu SQL Server Management Studio w usłudze Azure RemoteApp, opisano hello korzyści i zawiera funkcje zabezpieczeń, które są dostępne w usłudze Azure Active Directory.

**Szacowany czas toocomplete:** 45 minut

## <a name="ssms-in-azure-remoteapp"></a>SSMS w usłudze Azure RemoteApp
Usługa Azure RemoteApp jest usługą usług pulpitu zdalnego na platformie Azure, który zawiera aplikacje. Można uzyskać więcej informacji na ten temat tutaj: [co to jest RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS uruchomionych w usłudze Azure RemoteApp daje hello tego samego środowiska jako SSMS uruchomionej na komputerze lokalnym.

![Zrzut ekranu przedstawiający SSMS uruchomionych w usłudze Azure RemoteApp][1]

## <a name="benefits"></a>Korzyści
Istnieje wiele korzyści toousing SSMS w usłudze Azure RemoteApp w tym:

* Port 1433 na serwerze Azure SQL nie ma toobe widoczne na zewnątrz (poza platformą Azure).
* Nie konieczności tookeep Dodawanie i usuwanie adresów IP w zapory serwera Azure SQL hello.
* Wszystkie połączenia z usługą Azure RemoteApp odbywa się za pośrednictwem protokołu HTTPS przy użyciu portu 443 szyfrowane protokołu Remote Desktop protocol
* Jest wielu użytkowników i mogą być skalowane.
* Jest z konieczności SSMS w hello są bardziej wydajne tego samego regionu hello bazy danych SQL.
* Można przeprowadzić inspekcję korzystanie z usługi Azure RemoteApp z wersji Premium hello Azure Active Directory, która ma raporty aktywności użytkownika.
* Można włączyć uwierzytelnianie wieloskładnikowe (MFA).
* Dostęp SSMS dowolne miejsce w przypadku, gdy przy użyciu dowolnego hello obsługiwani klienci usługi Azure RemoteApp, w tym z systemem iOS, Android, Mac, Windows Phone i komputerach z systemem Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Utwórz kolekcję usługi Azure RemoteApp hello
Oto toocreate kroki hello kolekcji usługi Azure RemoteApp z SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Utwórz nową maszynę Wirtualną systemu Windows na podstawie obrazu
Użyj hello obrazu "Systemu Windows serwera zdalnego pulpitu sesji hosta systemu Windows Server 2012 R2" z toomake galerii hello nowej maszyny Wirtualnej.

### <a name="2-install-ssms-from-sql-express"></a>2. Zainstaluj narzędzia SSMS z SQL Express
Przejdź na hello nowej maszyny Wirtualnej, a następnie przejdź do strony pobierania toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Istnieje opcja pobierania tooonly SSMS. Po pobraniu przejdź do katalogu instalacyjnego hello i uruchom Instalator tooinstall SSMS.

Należy również tooinstall dodatku Service Pack 1 dla programu SQL Server 2014. Można go pobrać tutaj: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

Dodatek Service Pack 1 dla programu SQL Server 2014 r. obejmuje funkcje niezbędne do pracy z bazą danych SQL Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Uruchom skrypt weryfikacji i programu Sysprep
Na powitania pulpitu hello maszyny Wirtualnej jest skrypt programu PowerShell o nazwie weryfikacji. Uruchom tego klikając dwukrotnie. Zweryfikuje hello, że maszyna wirtualna jest gotowa toobe używany do zdalnego hostowania aplikacji. Po zakończeniu weryfikacji poprosi sysprep toorun — wybierz toorun go.

Po zakończeniu działania programu sysprep, wyłączy hello maszyny Wirtualnej.

toolearn więcej informacji o tworzeniu obrazu usługi Azure RemoteApp, zobacz: [jak toocreate szablonu usługi RemoteApp obrazu na platformie Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Przechwycenie obrazu
Gdy powitalne wirtualna przestała działać, znajdź go w bieżącym portalu hello i przechwyceniem go.

toolearn więcej informacji na temat przechwytywania obrazu, zobacz [przechwytywania obrazu systemu Windows Azure maszyny wirtualnej utworzone za pomocą hello klasycznego modelu wdrażania](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Dodaj tooAzure obrazy szablonów usługi RemoteApp
W hello sekcji hello bieżącym portalu usługi Azure RemoteApp przejdź na kartę obrazy szablonów toohello, a następnie kliknij przycisk Dodaj. W oknie podręcznym hello wybierz "Import obrazów z biblioteki maszyn wirtualnych", a następnie wybierz hello obrazu, który został właśnie utworzony.

### <a name="6-create-cloud-collection"></a>6. Tworzenie kolekcji w chmurze
W bieżącym portalu hello Utwórz nową kolekcję chmury Azure RemoteApp. Wybierz hello obrazu szablonu, który właśnie zaimportowany z SSMS na nim zainstalowany.

![Utwórz nową kolekcję w chmurze][2]

### <a name="7-publish-ssms"></a>7. Publikowanie programu SSMS
Na powitania publikowania kartę nowej kolekcji chmury, wybierz opcję publikowania aplikacji za pomocą hello Start Menu, a następnie wybierz pozycję Narzędzia SSMS z listy hello.

![Publikowanie aplikacji][5]

### <a name="8-add-users"></a>8. Dodawanie użytkowników
Na karcie dostęp użytkownika hello można wybrać hello użytkowników, którzy będą miały dostępu toothis usługi Azure RemoteApp kolekcję, która zawiera tylko SSMS.

![Dodaj użytkownika][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Zainstaluj aplikację kliencką hello Azure RemoteApp
Możesz pobrać i zainstalować klienta usługi Azure RemoteApp w tym miejscu: [Pobierz | Usługa Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Konfigurowanie serwera Azure SQL
Hello zapory hello jest włączona tylko konfiguracji potrzebne jest tooensure, czy usługi Azure. Jeśli używasz tego rozwiązania, następnie nie trzeba tooadd dowolnego adresu IP adresów tooopen hello zapory. Witaj ruchu sieciowego, który jest dozwolony toohello programu SQL Server jest z innymi usługami Azure.

![Zezwalaj na platformie Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Uwierzytelnianie wieloskładnikowe (MFA)
Uwierzytelnianie wieloskładnikowe można włączyć specjalnie dla tej aplikacji. Przejdź na kartę aplikacje toohello usługi Azure Active Directory. Wpis będą dostępne do funkcji RemoteApp systemu Microsoft Azure. Jeśli klikniesz tej aplikacji, a następnie skonfiguruj, zostanie wyświetlona strona hello poniżej której można włączyć usługę MFA dla tej aplikacji.

![Włączenie uwierzytelniania MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Inspekcja aktywności użytkownika za pomocą usługi Azure Active Directory — wersja Premium
Jeśli nie masz usługi Azure AD Premium, a następnie masz tooturn go na hello licencji części katalogu. Z Premium włączone można przypisywać użytkowników toohello poziom Premium.

Po przejściu tooa użytkownika w usłudze Azure Active Directory, możesz przejść toohello działania kartę toosee logowania informacji tooAzure programów RemoteApp.

## <a name="next-steps"></a>Następne kroki
Po zakończeniu wszystkich hello powyżej kroki, użytkownik zostanie klienta usługi Azure RemoteApp hello stanie toorun i dziennika za pomocą przypisany użytkownik. Użytkownik zobaczy SSMS jako jedna z aplikacji i można go uruchomić, jak w przypadku, jeśli zostały zainstalowane na komputerze z serwerem SQL tooAzure dostępu.

Aby uzyskać więcej informacji dotyczących sposobu toomake hello tooSQL połączenia bazy danych, zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).

To wszystko jest teraz. Owocnej pracy.

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png