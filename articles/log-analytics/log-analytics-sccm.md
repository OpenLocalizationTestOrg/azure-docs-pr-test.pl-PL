---
title: aaaConnect tooLog programu Configuration Manager Analytics | Dokumentacja firmy Microsoft
description: "W tym artykule przedstawiono hello kroki tooconnect tooLog programu Configuration Manager, analizy i analizowanie danych rozpoczęcia."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Połącz Analytics tooLog programu Configuration Manager
Możesz połączyć System Center Configuration Manager tooLog Analytics OMS toosync urządzenia zbierania danych. Dzięki temu dane z hierarchii programu Configuration Manager dostępne w OMS.

## <a name="prerequisites"></a>Wymagania wstępne

Analiza dzienników obsługuje System Center Configuration Manager bieżącej gałęzi, wersja 1606 i wyższych.  

## <a name="configuration-overview"></a>Przegląd konfiguracji
Witaj, wykonaj czynności zawiera podsumowanie hello procesu tooconnect Analytics tooLog programu Configuration Manager.  

1. W portalu zarządzania Azure hello Zarejestruj programu Configuration Manager jako aplikację aplikacji sieci Web i/lub interfejs API sieci Web i upewnij się, że masz hello identyfikator i klienta klucza tajnego klienta z hello rejestracji z usługi Azure Active Directory. Zobacz [toocreate portalu aplikacji usługi Active Directory i nazwy głównej usługi, który ma dostęp do zasobów](../azure-resource-manager/resource-group-create-service-principal-portal.md) Aby uzyskać szczegółowe informacje o tym, jak wykonać ten krok.
2. W portalu zarządzania Azure, hello [Określ programu Configuration Manager (aplikacja sieci web w zarejestrowany hello) z uprawnieniem tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. W programie Configuration Manager [dodać połączenie przy użyciu hello Kreatora połączenia OMS Dodaj](#add-an-oms-connection-to-configuration-manager).
4. W programie Configuration Manager [zaktualizować właściwości połączenia hello](#update-oms-connection-properties) powitania klienta lub hasło klucza tajnego kiedykolwiek wygaśnie lub zostaną utracone.
5. Informacje z portalu OMS hello [pobrać i zainstalować agenta monitorowania firmy Microsoft hello](#download-and-install-the-agent) hello hello połączenia z usługą Configuration Manager z uruchomionym roli systemu lokacji punktu. Witaj, agent wysyła tooOMS danych programu Configuration Manager.
6. W przypadku analizy dzienników [zaimportować kolekcje z programu Configuration Manager](#import-collections) jako grupy komputerów.
7. W przypadku analizy dzienników wyświetlania danych z programu Configuration Manager jako [grup komputerów](log-analytics-computer-groups.md).

Więcej o nawiązywaniu połączeń tooOMS programu Configuration Manager w [synchronizowanie danych z programu Configuration Manager toohello programu Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Określ programu Configuration Manager z tooOMS uprawnień
Witaj Poniższa procedura zawiera hello portalu zarządzania Azure z tooaccess uprawnienia OMS. W szczególności należy udzielić hello *roli współautora* toousers w grupie zasobów hello w kolejności tooallow hello Azure Management Portal tooconnect tooOMS programu Configuration Manager.

> [!NOTE]
> Należy określić uprawnienia w OMS programu Configuration Manager. W przeciwnym razie zostanie wyświetlony komunikat o błędzie, korzystając z Kreatora konfiguracji hello w programie Configuration Manager.
>
>

1. Otwórz hello [portalu Azure](https://portal.azure.com/) i kliknij przycisk **Przeglądaj** > **analizy dzienników (OMS)** tooopen hello analizy dzienników (OMS) bloku.  
2. Na powitania **analizy dzienników (OMS)** bloku, kliknij przycisk **Dodaj** tooopen hello **obszarem roboczym pakietu OMS** bloku.  
   ![Blok OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. Na powitania **obszarem roboczym pakietu OMS** bloku, podaj hello następujące informacje, a następnie kliknij przycisk **OK**.

   * **Obszar roboczy OMS**
   * **Subskrypcja**
   * **Grupa zasobów**
   * **Lokalizacja**
   * **Warstwa cenowa**  
     ![Blok OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > w powyższym przykładzie Hello tworzy nową grupę zasobów. Grupa zasobów Hello jest tylko używane tooprovide programu Configuration Manager z obszarem roboczym pakietu OMS toohello uprawnienia w tym przykładzie.
     >
     >
4. Kliknij przycisk **Przeglądaj** > **grup zasobów** tooopen hello **grup zasobów** bloku.
5. W hello **grup zasobów** bloku, kliknij grupę zasobów hello utworzoną wcześniej tooopen hello &lt;Nazwa grupy zasobów&gt; bloku ustawienia.  
   ![bloku ustawienia grupy zasobów](./media/log-analytics-sccm/sccm-azure03.png)
6. W hello &lt;Nazwa grupy zasobów&gt; bloku ustawienia kliknij dostępu do formantu (IAM) tooopen hello &lt;Nazwa grupy zasobów&gt; blok użytkowników.  
   ![Blok użytkownicy w grupie zasobów](./media/log-analytics-sccm/sccm-azure04.png)  
7. W hello &lt;Nazwa grupy zasobów&gt; blok użytkowników, kliknij przycisk **Dodaj** tooopen hello **Dodawanie dostępu** bloku.
8. W hello **Dodawanie dostępu** bloku, kliknij przycisk **wybierz rolę**, a następnie wybierz hello **współautora** roli.  
   ![Wybierz rolę](./media/log-analytics-sccm/sccm-azure05.png)  
9. Kliknij przycisk **dodawania użytkowników**, wybierz hello użytkownika programu Configuration Manager, kliknij przycisk **wybierz**, a następnie kliknij przycisk **OK**.  
   ![Dodawanie użytkowników](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Dodaj tooConfiguration połączenia OMS Manager
W kolejności tooadd połączenia z usługą OMS, środowiska programu Configuration Manager musi mieć [punkt połączenia z usługą](https://technet.microsoft.com/library/mt627781.aspx) skonfigurowany dla trybu online.

1. W hello **administracji** obszaru roboczego programu Configuration Manager, wybierz **łącznik OMS**. Spowoduje to otwarcie hello **Kreatora dodawania pakietu OMS połączenia**. Wybierz **dalej**.
2. Na powitania **ogólne** ekranu, upewnij się, czy wykonano hello następujące akcje i czy masz szczegółów dla każdego elementu, a następnie wybierz **dalej**.

   1. W hello portalu zarządzania Azure, programu Configuration Manager został zarejestrowany jako aplikacji sieci Web, aplikacji i/lub interfejs API sieci Web i czy ma hello [identyfikator klienta z rejestracji hello](../active-directory/active-directory-integrating-applications.md).
   2. W portalu zarządzania Azure hello zostanie utworzona klucz tajny aplikacji hello aplikacji zarejestrowanych w usłudze Azure Active Directory.  
   3. W portalu zarządzania Azure hello podane hello aplikacji sieci web w zarejestrowany z uprawnieniem tooaccess OMS.  
      ![Strona kreatora Ogólne tooOMS połączenia](./media/log-analytics-sccm/sccm-console-general01.png)
3. Na powitania **usługi Azure Active Directory** ekranu, skonfigurować Twojej tooOMS ustawienia połączenia, zapewniając Twojej **dzierżawy** , **identyfikator klienta** , i **klucz tajny klienta**  , a następnie wybierz pozycję **dalej**.  
   ![Strona Kreatora usługi Azure Active Directory tooOMS połączenia](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Jeśli wykonano hello wszystkich innych procedur pomyślnie, hello informacji na temat hello **konfiguracji połączenia OMS** ekranu będzie automatycznie wyświetlane na tej stronie. Informacje dotyczące ustawień połączenia hello powinien zostać wyświetlony dla użytkownika **subskrypcji platformy Azure** , **grupy zasobów platformy Azure** , i **obszar roboczy usługi Operations Management Suite**.  
   ![Strona kreatora OMS połączenia tooOMS połączenia](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Kreator Hello łączy usługę toohello przy użyciu hello informacje, które zostały danych wejściowych. Wybierz kolekcje urządzeń hello mają toosync z OMS, a następnie kliknij przycisk **Dodaj**.  
   ![Wybierz kolekcje](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Sprawdź ustawienia połączenia na powitania **Podsumowanie** ekranu, a następnie wybierz **dalej**. Witaj **postępu** ekranu przedstawia stan połączenia hello, a następnie należy **Complete**.

> [!NOTE]
> Należy połączyć OMS toohello najwyższego poziomu lokacji w hierarchii. Jeśli możesz połączyć tooa OMS autonomiczną lokacją główną, a następnie dodać środowisku tooyour witryny Administracja centralna, będzie mieć toodelete i Utwórz ponownie połączenie OMS hello w nowej hierarchii hello.
>
>

Po połączeniu tooOMS programu Configuration Manager, możesz Dodaj lub usuń kolekcje i wyświetlić właściwości hello hello połączenia z usługą OMS.

## <a name="update-oms-connection-properties"></a>Zaktualizuj właściwości połączenia OMS
Jeśli kiedykolwiek klucza tajnego klienta lub hasło wygaśnie lub zostaną utracone, konieczne będzie właściwości połączenia toomanually aktualizacji hello OMS.

1. W programie Configuration Manager Przejdź zbyt**usługi w chmurze** , a następnie wybierz pozycję **łącznik OMS** tooopen hello **właściwości połączenia OMS** strony.
2. Na tej stronie, kliknij przycisk hello **usługi Azure Active Directory** karcie tooview Twojego **dzierżawy**, **identyfikator klienta**, **wygaśnięcia klucza tajnego klienta**. **Sprawdź** Twojego **klucza tajnego klienta** Jeśli wygasł.

## <a name="download-and-install-hello-agent"></a>Pobierz i zainstaluj agenta hello
1. W portalu OMS hello [plik Instalatora pobierania hello agenta z usługą OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Użyj jednej z hello następujące metody tooinstall i skonfigurować agenta hello na komputerze hello uruchomiona rola systemu lokacji punktu połączenia hello programu Configuration Manager service:
   * [Instalowanie agenta hello za pomocą Instalatora](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Instalowanie agenta hello za pomocą wiersza polecenia hello](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Zainstaluj agenta hello przy użyciu usługi Konfiguracja DSC automatyzacji Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importuj kolekcje
Po utworzeniu dodane tooConfiguration połączenia OMS Manager i zainstalowany hello agent hello hello połączenia z usługą Configuration Manager z uruchomionym roli systemu lokacji punktu, hello następnym krokiem jest tooimport kolekcji z programu Configuration Manager w OMS jak grupy komputerów.

Po włączeniu import, informacje o członkostwie w kolekcji hello jest pobierana co 3 godziny tookeep hello członkostwa w kolekcjach bieżącej. Można wybrać import toodisable w dowolnym momencie.

1. W portalu OMS hello, kliknij przycisk **ustawienia**.
2. Kliknij przycisk hello **grup komputerów** a następnie kliknij pozycję hello **SCCM** kartę.
3. Wybierz **członkostwa w kolekcji programu Configuration Manager importu** , a następnie kliknij przycisk **zapisać**.  
   ![Grupy komputerów — karta SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Wyświetlanie danych z programu Configuration Manager
Po utworzeniu dodane tooConfiguration połączenia OMS Manager i zainstalowany hello agent na powitania komputerze roli systemu lokacji punktu połączenia hello programu Configuration Manager usługi, dane od agenta hello są wysyłane tooOMS. W OMS, kolekcji programu Configuration Manager są wyświetlane jako [grup komputerów](log-analytics-computer-groups.md). Możesz wyświetlić hello grupy z hello **programu Configuration Manager** w obszarze **grup komputerów** w **ustawienia**.

Po powitalne kolekcje są importowane jest widoczny wykryto liczbę komputerów z członkostwa w kolekcji. Można również sprawdzić hello wielu kolekcji, które zostały zaimportowane.

![Grupy komputerów — karta SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Po kliknięciu jednej, otwiera wyszukiwania wyświetlanie: wszystkie hello zaimportowane grupy lub wszystkich komputerów, które należą do grupy tooeach. Przy użyciu [wyszukiwania dziennika](log-analytics-log-searches.md), możesz uruchomić dokładnych analiz danych programu Configuration Manager.

## <a name="next-steps"></a>Następne kroki
* Użyj [wyszukiwania dziennika](log-analytics-log-searches.md) tooview szczegółowe informacje na temat danych programu Configuration Manager.
