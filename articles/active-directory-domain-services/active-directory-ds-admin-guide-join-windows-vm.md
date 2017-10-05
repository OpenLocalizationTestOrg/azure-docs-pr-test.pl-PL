---
title: "Azure Active Directory Domain Services: Dołącz Maszynę wirtualną systemu Windows Server do domeny zarządzanej | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Windows Server do usług domenowych Azure AD"
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
ms.openlocfilehash: 9f8d21f6964d26a2e17e31d1f2947e7eb07c177d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a>Przyłączanie maszyny wirtualnej z systemem Windows Server do domeny zarządzanej
> [!div class="op_single_selector"]
> * [Klasyczny portal Azure — systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell — systemu Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

W tym artykule przedstawiono sposób dołączenia maszyny wirtualnej z systemem Windows Server 2012 R2 do domeny zarządzanej usług domenowych Azure AD, przy użyciu klasycznego portalu Azure.

## <a name="step-1-create-the-windows-server-virtual-machine"></a>Krok 1: Tworzenie maszyny wirtualnej systemu Windows Server
Wykonaj instrukcje opisane w temacie [Utwórz maszynę wirtualną z systemem Windows w klasycznym portalu Azure](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) samouczka. Jest ważne upewnić się, że nowo utworzonej maszyny wirtualnej jest dołączony do tej samej sieci wirtualnej, w której włączono usługi domenowe Azure AD. Opcji "Szybkie tworzenie" nie umożliwiają dołączanie maszyny wirtualnej do sieci wirtualnej. W związku z tym należy użyć opcji "Z galerii" Aby utworzyć maszynę wirtualną.

Wykonaj poniższe kroki, aby utworzyć maszynę wirtualną systemu Windows przyłączone do sieci wirtualnej, w której włączono usługi domenowe Azure AD.

1. W klasycznym portalu Azure, na pasku poleceń w dolnej części okna kliknij **nowy**.
2. W obszarze **obliczeniowe**, kliknij przycisk **maszyny wirtualnej**, następnie kliknij przycisk **z galerii**.
3. Pierwszy ekran umożliwia **wybierz obraz** dla maszyny wirtualnej z listy dostępnych obrazów. Wybierz odpowiedni obraz.

    ![Wybierz obraz](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. Drugi ekranu umożliwia wybór nazwy komputera, rozmiar i nazwa użytkownika administratora i hasła. Skorzystaj z warstwy i rozmiar wymagany do uruchomienia z aplikacji lub obciążeń. Nazwa użytkownika, który wybrano tutaj jest użytkownika administratora lokalnego na komputerze. Nie należy wprowadzać poświadczenia konta użytkownika domeny, w tym miejscu.

    ![Konfigurowanie maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. Trzeci ekran umożliwia konfigurowanie zasobów sieci, magazynu i dostępności. Upewnij się, wybierz sieć wirtualną, w której włączono usługi domenowe Azure AD z **Region/koligacji grupy/wirtualnej sieci** listy rozwijanej. Określ **nazwa DNS usługi w chmurze** jako odpowiednie dla maszyny wirtualnej.

    ![Wybierz sieć wirtualną maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Upewnij się, Dołącz maszynę wirtualną do tej samej sieci wirtualnej, w której włączono usługi domenowe Azure AD. W związku z tym maszyny wirtualnej można wyświetlić domeny i wykonywanie zadań takich jak przyłączanie do domeny. Jeśli wybierzesz utworzyć maszynę wirtualną w innej sieci wirtualnej, należy połączyć z tej sieci wirtualnej do sieci wirtualnej, w której włączono usługi domenowe Azure AD.
   >
   >
6. Czwarty ekran umożliwia zainstalowanie agenta maszyny Wirtualnej i skonfigurowanie niektóre z dostępnych rozszerzeń.

    ![Gotowe](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Po utworzeniu maszyny wirtualnej, klasyczny portal Wyświetla nowej maszyny wirtualnej w ramach **maszyn wirtualnych** węzła. Zarówno maszyna wirtualna, jak i usługa w chmurze są uruchamiane automatycznie, a ich stany są wskazywane jako **Uruchomiono**.

    ![Maszyna wirtualna jest uruchomiona](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-to-the-windows-server-virtual-machine-using-the-local-administrator-account"></a>Krok 2: Łączenie z maszyną wirtualną systemu Windows Server przy użyciu konta administratora lokalnego
Teraz możemy połączyć się z nowo utworzonego maszyny wirtualnej systemu Windows Server, aby przyłączyć się do domeny. Użyj poświadczeń administratora lokalnego, określone podczas tworzenia maszyny wirtualnej, aby się z nim połączyć.

Wykonaj poniższe kroki, aby połączyć się z maszyną wirtualną.

1. Przejdź do **maszyn wirtualnych** węzła w portalu klasycznym. Wybierz maszyny wirtualne utworzone w kroku 1, a następnie kliknij przycisk **Connect** na pasku poleceń u dołu okna.

    ![Połącz z maszyną wirtualną systemu Windows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. Klasyczny portal wyświetli monit o otworzyć lub zapisać plik z rozszerzeniem "RDP", który jest używany do nawiązania połączenia z maszyną wirtualną. Kliknij, aby otworzyć plik, po zakończeniu pobierania.
3. W wierszu logowania wprowadź Twojej **poświadczenia administratora lokalnego**, która została określona podczas tworzenia maszyny wirtualnej. Na przykład możemy używano "localhost\mahesh" w tym przykładzie.

W tym momencie możesz powinny być rejestrowane nowo utworzonej maszyny wirtualnej systemu Windows przy użyciu poświadczeń administratora lokalnego. Następnym krokiem jest można dołączyć maszyny wirtualnej do domeny.

## <a name="step-3-join-the-windows-server-virtual-machine-to-the-aad-ds-managed-domain"></a>Krok 3: Sprzężenia maszyny wirtualnej systemu Windows Server do domeny zarządzanej DS usługi AAD
Wykonaj poniższe kroki, aby dołączyć maszyny wirtualnej systemu Windows Server do domeny zarządzanej usługi AAD DS.

1. Podłącz do systemu Windows Server, jak pokazano w kroku 2. Na ekranie startowym Otwórz **Menedżera serwera**.
2. Kliknij przycisk **lokalnego serwera** w lewym okienku okna Menedżera serwera.

    ![Uruchom Menedżera serwera na maszynie wirtualnej](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Kliknij przycisk **grupy roboczej** w obszarze **właściwości** sekcji. W **właściwości systemu** strony właściwości, kliknij przycisk **zmiany** do przyłączania do domeny.

    ![Strona właściwości systemu](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Określ nazwę domeny w domenie zarządzanej usług domenowych Azure AD w **domeny** pole tekstowe i kliknij przycisk **OK**.

    ![Określ domenę, która ma zostać umieszczony](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Monit o podanie poświadczeń w celu przyłączenia do domeny. Upewnij się, że **Określ poświadczenia dla użytkownika należącego do administratorów kontrolera domeny usługi AAD** grupy. Tylko członkowie tej grupy mają uprawnienia do przyłączania komputerów do domeny zarządzanej.

    ![Określ poświadczenia dla przyłączania do domeny](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Możesz określić poświadczenia w jednym z następujących sposobów:

   * Format nazwy UPN: Określ sufiks nazwy UPN dla konta użytkownika, zgodnie z konfiguracją w usłudze Azure AD. W tym przykładzie sufiks nazwy UPN użytkownika "bob" jest "bob@domainservicespreview.onmicrosoft.com".
   * SAMAccountName format: należy określić nazwę konta w formacie SAMAccountName. W tym przykładzie "bob" użytkownik musi wprowadzić "CONTOSO100\bob".

     > [!NOTE]
     > **Zaleca się przy użyciu formatu nazwy UPN, aby określić poświadczenia.** SAMAccountName może zostać wygenerowany automatycznie, jeśli prefiks nazwy UPN użytkownika jest zbyt długi (na przykład "joereallylongnameuser"). Jeśli wielu użytkowników ma tego samego prefiksu nazwy UPN (na przykład "bob") w dzierżawie usługi Azure AD, ich format SAMAccountName mogą być automatycznie generowane przez usługę. W takich przypadkach format nazwy UPN można niezawodnie logować się do domeny.
     >
     >
7. Po pomyślnym przyłączenie do domeny zostanie wyświetlony następujący komunikat powiadomieniem o przyjęciu do domeny. Uruchom ponownie maszynę wirtualną na zakończenie operacji sprzężenia domeny.

    ![Zapraszamy do domeny](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Rozwiązywanie problemów z przyłączania do domeny
### <a name="connectivity-issues"></a>Problemy z łącznością
Jeśli maszyna wirtualna nie może znaleźć domeny, można skorzystać z wykonać następujące kroki:

* Upewnij się, że maszyna wirtualna jest podłączony do tej samej sieci wirtualnej co włączeniu usług domenowych w. Jeśli nie, maszyny wirtualnej nie może połączyć się z domeną i dlatego nie można przyłączyć do domeny.
* Maszyna wirtualna jest podłączony do innej sieci wirtualnej, upewnij się, że ta sieć wirtualna jest podłączony do sieci wirtualnej, w której włączono usługi domenowe.
* Spróbuj wykonać polecenie ping domeny przy użyciu nazwy domeny zarządzanej domeny (na przykład "ping contoso100.com"). Jeśli to możliwe, spróbuj na polecenie ping adresów IP dla domeny wyświetlany na stronie w którym włączono usługi domenowe Azure AD (na przykład "ping 10.0.0.4"). Jeśli jesteś w stanie zbadać poleceniem ping adres IP, ale nie domenę, DNS może być niepoprawnie skonfigurowana. Może nie skonfigurowano adresów IP domeny jako serwery DNS dla sieci wirtualnej.
* Spróbuj opróżniania pamięci podręcznej programu rozpoznawania nazw DNS na maszynie wirtualnej ("ipconfig/flushdns").

Jeśli pojawi się okno dialogowe z monitem o podanie poświadczeń w celu przyłączenia do domeny, nie masz problemy z połączeniem.

### <a name="credentials-related-issues"></a>Problemy związane z poświadczeń
Zapoznaj się następujące kroki, jeśli występują problemy przy użyciu poświadczeń i nie można przyłączyć do domeny.

* Spróbuj użyć format nazwy UPN, aby określić poświadczenia. SAMAccountName dla Twojego konta może być automatycznie wygenerowany w przypadku wielu użytkowników z tego samego prefiksu nazwy UPN w dzierżawie, lub jeśli Twoje prefiks nazwy UPN jest zbyt długa. W związku z tym format SAMAccountName dla Twojego konta mogą być inne niż co oczekiwane lub użyć w domenie lokalnej.
* Spróbuj użyć poświadczenia konta użytkownika należącego do grupy "Administratorzy kontrolera domeny usługi AAD" do przyłączania komputerów do domeny zarządzanej.
* Upewnij się, że masz [włączoną synchronizację haseł](active-directory-ds-getting-started-password-sync.md) zgodnie z procedurą opisaną w przewodniku Wprowadzenie.
* Upewnij się, że używasz nazwy UPN użytkownika zgodnie z konfiguracją w usłudze Azure AD (na przykład "bob@domainservicespreview.onmicrosoft.com") do logowania.
* Upewnij się, że upłynął czas potrzebny wystarczająco długo na zakończenie określone w przewodniku wprowadzenie synchronizacji haseł.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
