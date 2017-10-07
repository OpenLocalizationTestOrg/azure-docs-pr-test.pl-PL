---
title: aaaDeploy SAP S/4HANA lub BW/4HANA na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Wdrożenie SAP S/4HANA lub BW/4HANA na maszynie Wirtualnej platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Wdrożenie SAP S/4HANA lub BW/4HANA na platformie Azure
W tym artykule opisano, jak toodeploy S/4HANA na platformie Azure przy użyciu hello SAP chmury urządzenie biblioteki (SAP CAL) 3.0. toodeploy innych SAP HANA rozwiązań, takich jak BW/4HANA, wykonaj hello te same czynności.

> [!NOTE]
Aby uzyskać więcej informacji na temat hello SAP CAL Przejdź toohello [biblioteki urządzenia chmury SAP](https://cal.sap.com/) witryny sieci Web. SAP ma również blog o hello [SAP chmury urządzenia biblioteki 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Jak 29 maja 2017 za pomocą modelu wdrażania usługi Azure Resource Manager hello dodatkowo toohello preferowany bez wdrażania klasycznego modelu toodeploy hello SAP CAL. Firma Microsoft zaleca używanie hello nowego modelu wdrażania usługi Resource Manager i pominąć hello klasycznego modelu wdrażania.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Krok po kroku proces toodeploy hello rozwiązania

powitania po sekwencji zrzuty ekranu pokazuje, jak toodeploy S/4HANA na platformie Azure przy użyciu hello SAP CAL. proces Hello działa hello taki sam sposób dla innych rozwiązań, takich jak BW/4HANA.

Witaj **rozwiązań** strony przedstawiono niektóre hello SAP CAL HANA rozwiązań dostępnych na platformie Azure. **SAP S/4HANA 1610 FPS01, urządzenia Fully-Activated** znajduje się w wierszu środkowej hello:

![Rozwiązania CAL SAP](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Tworzenie konta w hello SAP CAL
1. toosign w toohello SAP licencji dostępu klienta na powitania po raz pierwszy, użyj użytkownika S SAP lub innego użytkownika w zarejestrowany SAP. Następnie zdefiniuj SAP CAL konta, które jest używane przez urządzenia toodeploy SAP CAL hello na platformie Azure. W definicji konta hello musisz:

    a. Wybierz model wdrożenia hello na platformie Azure (Resource Manager lub classic).

    b. Wprowadź subskrypcji platformy Azure. Konto SAP CAL można przypisać tylko tooone subskrypcji. Jeśli potrzebujesz więcej niż jedną subskrypcję, należy toocreate innego konta SAP CAL.

    c. Nadaj hello SAP CAL uprawnienia toodeploy do Twojej subskrypcji platformy Azure.

    > [!NOTE]
    Następne kroki Hello pokazują, jak konto toocreate CAL SAP do wdrożenia usługi Resource Manager. Jeśli masz już konto SAP CAL, które jest połączone toohello klasycznego modelu wdrażania, możesz *muszą* toofollow toocreate te kroki nowe konto SAP CAL. nowe konto SAP CAL Hello musi toodeploy hello modelu Resource Manager.

2. Utwórz nowe konto SAP CAL. Witaj **kont** strony zawiera trzy opcje dla platformy Azure: 

    a. **Microsoft Azure (klasyczne)** jest hello klasycznego modelu wdrażania i nie jest preferowany.

    b. **Microsoft Azure** jest hello nowego modelu wdrażania Menedżera zasobów.

    c. **Windows Azure obsługiwany przez 21Vianet** jest opcją w Chinach, który używa hello klasycznego modelu wdrażania.

    Wybierz toodeploy w modelu Resource Manager hello **Microsoft Azure**.

    ![Szczegóły konta CAL SAP](./media/cal-s4h/s4h-pic-2a.png)

3. Wprowadź hello Azure **identyfikator subskrypcji** znajdującymi się na powitania portalu Azure.

   ![Konta CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. Definicja tooauthorize hello SAP CAL toodeploy do hello subskrypcji platformy Azure, kliknij przycisk **autoryzacji**. powitania po stronie pojawia się na karcie przeglądarki hello:

   ![Logowania usług w chmurze programu Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Jeśli jest wymieniona więcej niż jednego użytkownika, wybierz konto Microsoft hello jest coadministrator hello toobe połączonego elementu hello subskrypcji platformy Azure, które wybrano. powitania po stronie pojawia się na karcie przeglądarki hello:

   ![Potwierdzenie usług w chmurze programu Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Kliknij przycisk **zaakceptować**. Jeśli autoryzacji hello zakończy się pomyślnie, hello definicji konta SAP CAL Wyświetla ponownie. Po pewnym czasie wyświetli się komunikat potwierdzający, pomyślnego hello procesu autoryzacji.

7. Witaj tooassign nowo utworzony użytkownik tooyour konta SAP CAL, wprowadź użytkownika **identyfikator użytkownika** w hello pola tekstowego na powitania prawo i kliknij przycisk **Dodaj**.

   ![Skojarzenie toouser konta](./media/cal-s4h/s4h-pic8a.png)

8. Kliknij konto użytkownika hello Użyj toosign w toohello SAP CAL tooassociate **przeglądu**. 
 
9. toocreate hello skojarzenie swoją nazwę użytkownika i hello nowo utworzone konto SAP CAL, kliknij przycisk **Utwórz**.

   ![Skojarzenie konta użytkownika tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

Pomyślnie utworzono konto SAP CAL, które jest w stanie:

- Użyj modelu wdrażania usługi Resource Manager hello.
- Wdrażanie systemów SAP do Twojej subskrypcji platformy Azure.

Teraz możesz rozpocząć toodeploy S/4HANA w subskrypcji użytkownika na platformie Azure.

> [!NOTE]
Przed kontynuowaniem należy sprawdzić, czy przydziały Azure core dla maszyn wirtualnych platformy Azure H serii. W momencie hello hello SAP CAL używa toodeploy H serii maszyn wirtualnych Azure niektórych rozwiązań hello SAP HANA. Subskrypcji platformy Azure może nie mieć żadnych przydziały core serii H H serii. Jeśli tak, może być konieczne toocontact pomocy technicznej platformy Azure tooget przydziału co najmniej 16 rdzeni H serii.

> [!NOTE]
Podczas wdrażania rozwiązania na platformie Azure w hello SAP CAL, może się okazać, że można wybrać tylko jeden region platformy Azure. toodeploy do regionów platformy Azure niż hello jedną sugerowanych hello SAP CAL, należy toopurchase CAL subskrypcji z SAP. Może okazać się również tooopen wiadomość z SAP toohave toodeliver konta użytkownika CAL do regionów platformy Azure niż hello początkowo sugerowane z nich.

### <a name="deploy-a-solution"></a>Wdrażanie rozwiązania

Umożliwia wdrażanie rozwiązania z hello **rozwiązań** strony hello SAP CAL. Witaj SAP CAL ma dwa toodeploy sekwencji:

- Podstawowe sekwencji, która korzysta z jednej strony toodefine hello systemu toobe wdrożony
- Zaawansowane sekwencji, zapewniająca niektórych opcji rozmiarów maszyny Wirtualnej 

Przedstawiony tutaj toodeployment podstawowa ścieżka hello.

1. Na powitania **szczegóły konta** strony, musisz:

    a. Wybierz konto SAP CAL. (Użyj konta, które jest skojarzone toodeploy z modelu wdrażania usługi Resource Manager hello).

    b. Wprowadź wystąpienia **nazwa**.

    c. Wybierz platformy Azure **Region**. Witaj SAP CAL sugeruje regionu. Jeśli nie masz subskrypcji SAP CAL wymagają innego regionu Azure, należy tooorder licencji CAL subskrypcji z SAP.

    d. Wprowadź wzorzec **hasło** hello rozwiązania z dziewięciu osiem znaków. hasło Hello jest używany dla administratorów hello hello różnych składników.

   ![Tryb CAL Basic SAP: Utworzenie wystąpienia](./media/cal-s4h/s4h-pic10a.png)

2. Kliknij przycisk **Utwórz**, a w polu wiadomość hello jest wyświetlana, kliknij przycisk **OK**.

   ![SAP CAL obsługiwane rozmiary maszyn wirtualnych](./media/cal-s4h/s4h-pic10b.png)

3. W hello **klucza prywatnego** okno dialogowe, kliknij przycisk **magazynu** toostore hello klucza prywatnego w hello SAP CAL. Ochrona za pomocą hasła toouse hello klucza prywatnego, kliknij przycisk **Pobierz**. 

   ![Klucz prywatny CAL SAP](./media/cal-s4h/s4h-pic10c.png)

4. Witaj odczytu SAP CAL **ostrzeżenie** komunikatów, a następnie kliknij przycisk **OK**.

   ![Ostrzeżenie CAL SAP](./media/cal-s4h/s4h-pic10d.png)

    Teraz hello wdrożenia ma miejsce. Po pewnym czasie, w zależności od rozmiaru hello i złożoność hello rozwiązania (hello SAP CAL zapewnia szacunkową) hello zostanie wyświetlony stan jako aktywne i gotowe do użycia.

5. maszyny wirtualne hello toofind zebranych przez hello innych skojarzonych zasobów w jednej grupie zasobów, odwiedź toohello portalu Azure: 

   ![Obiekty SAP CAL wdrożone w hello nowego portalu.](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. W portalu SAP CAL hello, hello stan jest wyświetlany jako **Active**. rozwiązanie toohello tooconnect, kliknij przycisk **Connect**. Różne opcje tooconnect toohello różnych składników są wdrażane w ramach tego rozwiązania.

   ![Wystąpienia CAL SAP](./media/cal-s4h/active_solution.png)

7. Zanim będzie możliwe użycie jednego z systemów toohello wdrożone tooconnect opcje hello, kliknij przycisk **Getting Started Guide**. 

   ![Połącz toohello wystąpienia](./media/cal-s4h/connect_to_solution.png)

    nazwy dokumentacji Hello hello użytkowników dla każdej z metod łączności hello. Hello hasła dla tych użytkowników są ustawione hasło główne toohello zdefiniowane przez użytkownika na początku hello hello procesu wdrażania. W dokumentacji hello innym użytkownikom bardziej funkcjonalny są wyświetlane z haseł, których można użyć toosign w toohello wdrożony system. 

    Na przykład jeśli używasz hello SAP graficznego interfejsu użytkownika, który jest preinstalowany na maszynie zdalnej pulpitu systemu Windows hello hello S/4 systemu może wyglądać następująco:

   ![SM50 w hello preinstalowany SAP graficznego interfejsu użytkownika](./media/cal-s4h/gui_sm50.png)

    Lub jeśli używasz hello DBACockpit wystąpienia hello może wyglądać następująco:

   ![SM50 w hello DBACockpit SAP graficznego interfejsu użytkownika](./media/cal-s4h/dbacockpit.png)

W ciągu kilku godzin dobrej kondycji urządzenia SAP S/4 jest wdrażana na platformie Azure.

Jeśli zakupiono subskrypcję SAP CAL SAP w pełni obsługuje wdrożeniami hello SAP CAL na platformie Azure. Kolejka Obsługa Hello jest BC-VCM-CAL.







