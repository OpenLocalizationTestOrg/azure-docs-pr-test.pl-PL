---
title: "aaaCreate profil Menedżera ruchu na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate profilu Menedżera ruchu"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager

W tym artykule opisano sposób profil z **priorytet** tooroute użytkowników tootwo Azure Web Apps w punkty końcowe można utworzyć typu routingu. Za pomocą hello **priorytet** routing typu, cały ruch jest kierowany toohello pierwszym punktem końcowym z podczas hello drugi jest przechowywana jako kopii zapasowej. W związku z tym użytkownicy mogą być routingiem toohello drugiego punktu końcowego, jeśli pierwszym punktem końcowym hello staje się nieprawidłowy.

W tym artykule dwa punkty końcowe z wcześniej utworzonej aplikacji sieci Web platformy Azure są skojarzone toothis nowo utworzony profil Menedżera ruchu. więcej informacji na temat toolearn toocreate punktów końcowych aplikacji sieci Web platformy Azure, odwiedź stronę hello [stronę dokumentacji Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/). Można dodać żadnych punktów końcowych nazwę DNS i jest dostępny za pośrednictwem hello publicznej sieci internet i jako przykład korzystamy punkty końcowe aplikacji sieci Web Azure.

### <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager
1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli nie masz jeszcze konta, możesz przystąpić do [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/free/). 
2. Na powitania **Centrum** menu, kliknij przycisk **nowy** > **sieci** > **zobaczyć wszystkie**, kliknij przycisk **ruchu Menedżer** hello tooopen profilu **profilu usługi Traffic Manager utwórz** bloku, następnie kliknij przycisk **Utwórz**.
3. Na powitania **profilu usługi Traffic Manager utwórz** bloku ukończenia w następujący sposób:
    1. W polu **Nazwa** podaj nazwę profilu. Ta nazwa musi toobe unikatowa w ramach strefy trafficmanager.net hello i powoduje nazwy DNS hello <name>, trafficmanager.net, która jest używana tooaccess profil Menedżera ruchu.
    2. W **metody routingu**, wybierz pozycję hello **priorytet** metody routingu.
    3. W **subskrypcji**, wybierz hello subskrypcję toocreate tego profilu, w obszarze
    4. W **grupy zasobów**, Utwórz nowy tooplace grupy zasobów tego profilu.
    5. W **lokalizacja grupy zasobów**, wybierz lokalizację hello hello grupy zasobów. To ustawienie dotyczy lokalizacji toohello hello grupy zasobów i nie ma wpływu na powitania profilu Menedżera ruchu, który będzie wdrażany globalnie.
    6. Kliknij przycisk **Utwórz**.
    7. Po zakończeniu hello globalne wdrażania profilu usługi Traffic Manager znajduje się on w grupie zasobów odpowiednich jako jeden z zasobów hello.

    ![Tworzenie profilu usługi Traffic Manager](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Dodawanie punktów końcowych usługi Traffic Manager

1. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwy, który został utworzony w powyższej sekcji i kliknij profil Menedżera ruchu hello w hello hello wyniki tego hello wyświetlane.
2. W hello **profilu usługi Traffic Manager** bloku w hello **ustawienia** kliknij **punkty końcowe**.
3. W hello **punkty końcowe** bloku, który jest wyświetlany, kliknij przycisk **Dodaj**.
4. W hello **dodać punkt końcowy** bloku ukończenia w następujący sposób:
    1. Dla opcji **Typ** kliknij pozycję **Punkt końcowy platformy Azure**.
    2. Podaj **nazwa** za pomocą którego chcesz toorecognize tego punktu końcowego.
    3. Dla **typu zasobu docelowego**, kliknij przycisk **usługi aplikacji**.
    4. Dla **zasób docelowy**, kliknij przycisk **wybierz usługę aplikacji** tooshow hello lista hello aplikacje sieci Web w obszarze hello tej samej subskrypcji. W hello **zasobów** bloku, który jest wyświetlany, pobranie hello usługi aplikacji, które mają tooadd jako hello pierwszym punktem końcowym.
    5. Dla opcji **Priorytet** wybierz wartość **1**. Powoduje to całego ruchu kierowanego toothis punktu końcowego, jeśli jest w dobrej kondycji.
    6. Pozycję **Dodaj jako wyłączone** pozostaw niezaznaczoną.
    7. Kliknij przycisk **OK**.
5.  Powtórz kroki 3 i 4 dla punktu końcowego hello dalej aplikacje sieci Web Azure. Upewnij się, że tooadd go z jego **priorytet** ustawioną wartość **2**.
6.  Po zakończeniu dodawania hello oba punkty końcowe są wyświetlane w hello **profilu usługi Traffic Manager** bloku wraz z ich monitorowania statusu **Online**.

    ![Dodawanie punktu końcowego Menedżera ruchu](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Użyj hello profilu Menedżera ruchu
1.  Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwy utworzonego w powyższej sekcji hello. W wynikach hello, które są wyświetlane kliknij profil Menedżera ruchu hello.
2. W hello **profilu usługi Traffic Manager** bloku, kliknij przycisk **omówienie**.
3. Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu. Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello. W takim przypadku wszystkie żądania są routingiem toohello pierwszym punktem końcowym i w przypadku wykrycia przez Menedżera ruchu jest zła, ruch hello automatycznie przełącza toohello następnego punktu końcowego.

## <a name="delete-hello-traffic-manager-profile"></a>Usuwanie profilu Menedżera ruchu hello
Gdy nie są już potrzebne, usunięcie grupy zasobów hello i hello profilu Menedżera ruchu, który został utworzony. toodo tak, wybierz grupę zasobów hello z hello **profilu usługi Traffic Manager** bloku i kliknij przycisk **usunąć**.

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [routingu typy](traffic-manager-routing-methods.md).
- Dowiedz się więcej o typy punktów końcowych [typy punktów końcowych](traffic-manager-endpoint-types.md).
- Dowiedz się więcej o [monitorowania punktów końcowych](traffic-manager-monitoring.md).



