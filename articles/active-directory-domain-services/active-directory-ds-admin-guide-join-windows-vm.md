---
title: "Azure Active Directory Domain Services: Przyłącz do domeny zarządzanej tooa maszyny Wirtualnej systemu Windows Server | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Windows Server usług domenowych w usłudze tooAzure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows Server
> [!div class="op_single_selector"]
> * [Klasyczny portal Azure — systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell — systemu Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

W tym artykule opisano sposób toojoin tooan systemu Windows Server 2012 R2 uruchomionej maszyny wirtualnej usługi domenowe Azure AD zarządzania domeny, za pomocą hello klasycznego portalu Azure.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Krok 1: Tworzenie maszyny wirtualnej systemu Windows Server hello
Wykonaj instrukcje hello opisane w hello [Utwórz maszynę wirtualną z systemem Windows w hello klasycznego portalu Azure](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) samouczka. Koniecznie tooensure, który jest nowo utworzona maszyna wirtualna przyłączone toohello tej samej sieci wirtualnej, w której włączono usługi domenowe Azure AD. opcji "Szybkie tworzenie" Hello nie włączać możesz toojoin hello maszyny wirtualnej tooa sieci wirtualnej. W związku z tym należy maszyny wirtualnej hello toocreate opcji toouse hello "Z galerii".

Wykonaj hello następujące kroki toocreate systemu Windows maszyny wirtualnej toohello przyłączone do sieci wirtualnej w której włączono usługi domenowe Azure AD.

1. W hello klasycznego portalu Azure, na pasku poleceń hello u dołu okna hello powitania kliknij **nowy**.
2. W obszarze **obliczeniowe**, kliknij przycisk **maszyny wirtualnej**, następnie kliknij przycisk **z galerii**.
3. pierwszym ekranie powitania umożliwia **wybierz obraz** dla maszyny wirtualnej z listy hello dostępnych obrazów. Wybierz odpowiedni obraz powitania.

    ![Wybierz obraz](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. drugim ekranie powitania umożliwia pobranie nazwy komputera, rozmiar i nazwa użytkownika administratora i hasła. Użyj hello warstwy i rozmiar wymagany toorun aplikację lub obciążenia. Nazwa użytkownika Hello wybrano tutaj jest użytkownika administratora lokalnego na komputerze hello. Nie należy wprowadzać poświadczenia konta użytkownika domeny, w tym miejscu.

    ![Konfigurowanie maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. trzeci ekranie powitania umożliwia konfigurowanie zasobów sieci, magazynu i dostępności. Upewnij się, wybierz sieć wirtualną hello, w której włączono usługi domenowe Azure AD z hello **Region/koligacji grupy/wirtualnej sieci** listy rozwijanej. Określ **nazwa DNS usługi w chmurze** odpowiednio hello maszyny wirtualnej.

    ![Wybierz sieć wirtualną maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Upewnij się, Dołącz do toohello maszyny wirtualnej hello tej samej sieci wirtualnej, w której włączono usługi domenowe Azure AD. W związku z tym hello maszyny wirtualnej można Zobacz hello domeny i wykonywanie zadań takich jak przyłączanie hello domeny. Jeśli maszyna wirtualna hello toocreate w innej sieci wirtualnej, należy połączyć z tej sieci wirtualnej toohello sieci wirtualnej w której włączono usługi domenowe Azure AD.
   >
   >
6. czwarty ekranie powitania pozwala zainstalować hello agenta maszyny Wirtualnej i skonfigurować niektóre hello dostępnych rozszerzeń.

    ![Gotowe](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Po utworzeniu maszyny wirtualnej hello hello klasyczny portal Wyświetla hello nowej maszyny wirtualnej w obszarze hello **maszyn wirtualnych** węzła. Witaj maszyny wirtualnej i usługi w chmurze są uruchamiane automatycznie i ich stan jest wyświetlany jako **systemem**.

    ![Maszyna wirtualna jest uruchomiona](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Krok 2: Łączenie maszyny wirtualnej systemu Windows Server toohello przy użyciu konta administratora lokalnego hello
Teraz możemy połączyć maszyny wirtualnej systemu Windows Server toohello nowo utworzony, toojoin go toohello domeny. Użyj poświadczeń administratora lokalnego hello określone podczas tworzenia maszyny wirtualnej hello, tooconnect tooit.

Wykonaj hello następującej maszyny wirtualnej toohello tooconnect czynności.

1. Przejdź za**maszyn wirtualnych** węzła w portalu klasycznym hello. Wybierz maszynę wirtualną hello utworzone w kroku 1, a następnie kliknij przycisk **Connect** na pasku poleceń hello u dołu okna hello hello.

    ![Połącz tooWindows maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klasyczny portal Hello monit tooopen lub Zapisz plik z rozszerzeniem "RDP", który jest maszyną wirtualną toohello tooconnect używane. Kliknij plik hello tooopen, po zakończeniu pobierania.
3. W wierszu hello logowania, wprowadź użytkownika **poświadczenia administratora lokalnego**, które określone podczas tworzenia maszyny wirtualnej hello. Na przykład możemy używano "localhost\mahesh" w tym przykładzie.

W tym momencie możesz powinny być rejestrowane toohello nowo tworzone maszyny wirtualnej systemu Windows przy użyciu poświadczeń administratora lokalnego. Witaj następnym krokiem jest toojoin hello maszyny wirtualnej toohello domeny.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Krok 3: Dołącz do domeny zarządzanej toohello AAD DS maszyny wirtualnej systemu Windows Server hello
Wykonaj hello następujące kroki toojoin hello systemu Windows Server maszyny wirtualnej toohello AAD DS domeny zarządzanej.

1. Podłącz toohello systemu Windows Server, jak pokazano w kroku 2. Na ekranie startowym hello Otwórz **Menedżera serwera**.
2. Kliknij przycisk **lokalnego serwera** w okienku po lewej stronie powitania hello okna Menedżera serwera.

    ![Uruchom Menedżera serwera na maszynie wirtualnej](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Kliknij przycisk **grupy roboczej** w obszarze hello **właściwości** sekcji. W hello **właściwości systemu** strony właściwości, kliknij przycisk **zmiany** toojoin hello domeny.

    ![Strona właściwości systemu](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Określ nazwę domeny hello domeny zarządzanej usług domenowych Azure AD w hello **domeny** pole tekstowe i kliknij przycisk **OK**.

    ![Określ przyłączone hello toobe domeny](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Możesz są tooenter zostanie wyświetlony monit o poświadczenia domeny hello toojoin. Upewnij się, że **Podaj poświadczenia użytkownika należące toohello Administratorzy kontrolera domeny usługi AAD hello** grupy. Tylko członkowie tej grupy mają domeny zarządzanej toohello maszyny toojoin uprawnienia.

    ![Określ poświadczenia dla przyłączania do domeny](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Możesz określić poświadczenia w jednym z hello następujące sposoby:

   * Format nazwy UPN: Określ hello sufiks głównej nazwy użytkownika dla konta użytkownika hello, zgodnie z konfiguracją w usłudze Azure AD. W tym przykładzie hello sufiks nazwy UPN użytkownika hello "bob" jest "bob@domainservicespreview.onmicrosoft.com".
   * SAMAccountName formatu: Nazwa konta hello można określić w formacie SAMAccountName hello. W tym przykładzie użytkownik hello "bob" potrzebny tooenter "CONTOSO100\bob".

     > [!NOTE]
     > **Zaleca się przy użyciu poświadczeń toospecify format nazwy UPN hello.** Witaj SAMAccountName mogą być automatycznie wygenerowany, jeśli prefiks nazwy UPN użytkownika jest zbyt długi (na przykład "joereallylongnameuser"). Jeśli wielu użytkowników ma tego samego prefiksu nazwy UPN (na przykład "bob") w dzierżawie usługi Azure AD, ich format SAMAccountName może być wygenerowana automatycznie przez usługę hello powitalne. W takich przypadkach format nazwy UPN hello można niezawodnie toolog w domenie toohello.
     >
     >
7. Po pomyślnym przyłączenie do domeny zostanie wyświetlony hello następującą wiadomości z powiadomieniem o przyjęciu toohello domeny. Uruchom ponownie maszynę wirtualną hello na powitania domeny sprzężenia operacji toocomplete.

    ![Domeny toohello-Zapraszamy!](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Rozwiązywanie problemów z przyłączania do domeny
### <a name="connectivity-issues"></a>Problemy z łącznością
Jeśli maszyna wirtualna hello jest toofind hello domeny, można znaleźć toohello następujące kroki rozwiązywania problemów:

* Upewnij się, czy maszyna wirtualna hello jest połączonych toohello tej samej sieci wirtualnej co włączeniu usług domenowych w. W przeciwnym razie hello maszyny wirtualnej jest tooconnect toohello domeny i dlatego toojoin hello domeny.
* Maszyna wirtualna hello jest tooanother połączonych sieci wirtualnej, upewnij się, że ta sieć wirtualna jest toohello połączonych sieci wirtualnej, w której włączono usługi domenowe.
* Spróbuj tooping hello domeny przy użyciu nazwy domeny hello hello zarządzanej domeny (na przykład "ping contoso100.com"). Jeśli toodo tak, spróbuj tooping hello adresów IP domeny hello wyświetlane na stronie powitania, gdzie są włączone usługi domenowe Azure AD (na przykład "ping 10.0.0.4"). Jeśli adres IP hello tooping może, ale nie hello domeny DNS może być niepoprawnie skonfigurowana. Może nie skonfigurowano adresów IP hello hello domeny jako serwery DNS dla sieci wirtualnej hello.
* Spróbuj opróżnianie hello pamięci podręcznej programu rozpoznawania nazw DNS na maszynie wirtualnej hello ("ipconfig/flushdns").

Jeśli pojawi się okno dialogowe toohello, która poprosi o podanie poświadczeń toojoin hello domeny, nie masz problemy z połączeniem.

### <a name="credentials-related-issues"></a>Problemy związane z poświadczeń
Zobacz toohello następujące kroki, jeśli występują problemy z poświadczeniami, a toojoin hello domeny.

* Spróbuj użyć hello UPN format toospecify poświadczeń. Hello SAMAccountName dla Twojego konta może zostać wygenerowany automatycznie w przypadku wielu użytkowników o hello tej samej nazwy UPN prefiksu w dzierżawie lub jeśli Twoje prefiks nazwy UPN jest zbyt długa. W związku z tym hello SAMAccountName formatu dla Twojego konta mogą być inne niż co oczekiwane lub użyć w domenie lokalnej.
* Spróbuj toouse hello poświadczenia konta użytkownika, które należy toohello "Administratorzy kontrolera domeny usługi AAD" grupy toojoin maszyny toohello zarządzanej domeny.
* Upewnij się, że masz [włączony synchronizacja haseł](active-directory-ds-getting-started-password-sync.md) zgodnie z hello kroki opisane w przewodniku wprowadzenie hello.
* Upewnij się, że używany hello nazwę UPN użytkownika hello zgodnie z konfiguracją w usłudze Azure AD (na przykład "bob@domainservicespreview.onmicrosoft.com") toosign w.
* Upewnij się, że upłynął czas potrzebny wystarczająco długi dla toocomplete synchronizacji hasło określone w przewodniku wprowadzenie hello.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
