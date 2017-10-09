---
title: aaaEncrypt maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Ten dokument ułatwia tooencrypt maszyny wirtualnej platformy Azure po odebraniu alertu z Centrum zabezpieczeń Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Szyfrowanie maszyny wirtualnej platformy Azure
Jeśli masz maszyny wirtualne, które nie są szyfrowane, w Centrum zabezpieczeń Azure zostanie wyświetlony alert. Te alerty będą widoczne jako zalecenie o wysokim znaczeniu i hello jest tooencrypt tych maszyn wirtualnych.

![Zalecenia dotyczące szyfrowania dysków](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> informacje Hello w tym dokumencie dotyczą tooencrypting maszyn wirtualnych bez przy użyciu klucza szyfrowania klucza (który jest wymagany do tworzenia kopii zapasowych maszyn wirtualnych za pomocą usługi Kopia zapasowa Azure). Zobacz artykuł hello [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) informacji na temat toouse toosupport klucza szyfrowania klucza kopia zapasowa Azure zaszyfrowanych maszyn wirtualnych platformy Azure.
>
>

tooencrypt maszyn wirtualnych platformy Azure, które zostały zidentyfikowane przez Centrum zabezpieczeń Azure jako wymagające szyfrowania, zaleca się hello następujące kroki:

* Zainstaluj i skonfiguruj program Azure PowerShell. Pozwoli to toorun hello PowerShell polecenia wymagane tooset się hello wymagania wstępne wymagane tooencrypt maszyn wirtualnych platformy Azure.
* Uzyskaj i uruchom skrypt programu PowerShell systemu Azure wymagania wstępne szyfrowania dysków Azure hello
* Zaszyfruj maszyny wirtualne.

Witaj celem niniejszego dokumentu jest tooenable tooencrypt możesz maszyn wirtualnych, nawet jeśli masz niewielkiego lub żadnego tła w programie Azure PowerShell.
Tym dokumencie przyjęto założenie, że używasz systemu Windows 10 jako komputer kliencki hello, w którym będzie konfigurowane szyfrowanie dysków Azure.

Istnieje wiele metod, które mogą być używane toosetup hello wymagania wstępne dotyczące i tooconfigure szyfrowania maszyn wirtualnych platformy Azure. Jeśli użytkownik ma dużą wiedzę na temat programu Azure PowerShell lub interfejsu wiersza polecenia Azure, możesz wybrać toouse inne rozwiązania.

> [!NOTE]
> toolearn więcej informacji na temat podejścia alternatywnego tooconfiguring szyfrowania dla maszyn wirtualnych platformy Azure można znaleźć pod adresem [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Instalowanie i konfigurowanie programu Azure PowerShell
Na komputerze musi być zainstalowany program Azure PowerShell w wersji 1.2.1 lub nowszej. Artykuł Hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) zawiera wszystkie kroki hello należy tooprovision toowork Twojego komputera z programem Azure PowerShell. Najprostszym rozwiązaniem Hello jest toouse hello Instalator Web PI instalacji wspomnianego w tym artykule. Nawet jeśli masz już programu Azure PowerShell jest zainstalowany, zainstaluj go ponownie za pomocą metody sieci Web PI hello, dzięki czemu masz hello najnowszą wersję programu Azure PowerShell.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Uzyskaj i uruchom skrypt konfiguracji wymagań wstępnych szyfrowania dysków Azure hello
Witaj skrypt konfiguracji wymagań wstępnych szyfrowania dysków Azure zostaną skonfigurowane wszystkie hello wymagań wstępnych dotyczących szyfrowania maszyn wirtualnych platformy Azure.

1. Przejdź toohello GitHub strony, która ma hello [Azure dysku szyfrowania wymagań wstępnych Instalatora skryptu](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Na stronie GibHub powitania kliknij hello **Raw** przycisku.
3. Użyj **CTRL-A** tooselect wszystkie hello tekstu na stronie powitania, a następnie użyj **CTRL-C** toocopy wszystkie hello tekstu w Schowku toohello strony hello.
4. Otwórz **Notatnik** i Wklej skopiowany hello tekst do Notatnika.
5. Utwórz na dysku C: nowy folder o nazwie **AzureADEScript**.
6. Zapisz plik Notatnika hello — kliknij przycisk **pliku**, następnie kliknij przycisk **Zapisz jako**. W polu tekstowym Nazwa pliku hello, wprowadź **"ADEPrereqScript.ps1"** i kliknij przycisk **zapisać**. (Pamiętaj, aby umieścić nazwę hello hello cudzysłowu, w przeciwnym razie hello plik zostanie zapisany z rozszerzeniem txt).

Teraz, gdy zawartość skryptu hello jest zapisywana, Otwórz skrypt hello hello PowerShell ISE:

1. W Start Menu hello, kliknij przycisk **Cortana**. Poproś **Cortana** "PowerShell", wpisując **PowerShell** w polu tekstowym wyszukiwania Cortany hello.
2. Kliknij prawym przyciskiem myszy pozycję **Windows PowerShell ISE** i kliknij opcję **Uruchom jako administrator**.
3. W hello **Administrator: Windows PowerShell ISE** okna, kliknij przycisk **widoku** , a następnie kliknij przycisk **Pokaż okienko skryptu**.
4. Jeśli widzisz hello **polecenia** powitania kliknij w okienku po prawej stronie okna hello hello **"x"** w hello prawym górnym rogu tooclose okienko hello go. Jeśli tekst hello jest za mała dla wartości można toosee, użyj **CTRL + Add** ("Dodaj" hello jest "+" Zaloguj się). Jeśli tekst hello jest zbyt duży, użyj **CTRL + Subtract** (hello jest Subtract "-" logowania).
5. Kliknij menu **File** (Plik), a następnie kliknij pozycję **Open** (Otwórz). Przejdź toohello **C:\AzureADEScript** na powitania kliknij dwukrotnie folder i hello **ADEPrereqScript**.
6. Witaj **ADEPrereqScript** zawartości powinien zostać wyświetlony hello PowerShell ISE i jest oznaczone kolorami toohelp łatwiej Zobacz różne składniki, takie jak polecenia, parametry i zmienne.

Powinien zostać wyświetlony ekran podobny do hello na poniższej ilustracji.

![Okno programu PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

Górne okienko Hello jest hello tooas określonego "okienkiem skryptu" i hello dolne okienko jest hello tooas określonego "Konsola". Terminy te będą używane w dalszej części artykułu.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Uruchom polecenie programu PowerShell wymagań wstępnych szyfrowania dysków Azure hello
Witaj skryptu wymagań wstępnych szyfrowania dysków Azure pojawi się prośba o następujących informacji po uruchomieniu skryptu hello hello:

* **Nazwa grupy zasobów** — nazwa programu hello grupy zasobów, które mają tooput hello magazyn kluczy.  Będzie można utworzyć nową grupę zasobów o nazwie hello, wprowadzony, jeśli go nie już o tej nazwie utworzony. Jeśli masz już grupę zasobów, że toouse w ramach tej subskrypcji, a następnie wprowadź nazwę hello tej grupy zasobów.
* **Nazwa magazynu kluczy** — nazwa hello Key Vault, w których szyfrowania kluczy są toobe umieszczona. Jeśli magazyn kluczy o podanej nazwie nie istnieje, zostanie utworzony nowy magazyn kluczy o nazwie zgodnej z wprowadzoną. Jeśli masz już magazyn kluczy, które mają toouse, wprowadź nazwę hello hello istniejący magazyn kluczy.
* **Lokalizacja** -lokalizacji hello magazynu kluczy. Upewnij się, że toobe magazyn kluczy i maszyny wirtualne hello szyfrowane są hello tej samej lokalizacji. Jeśli nie znasz lokalizacji hello później w tym artykule opisano, jak są kroki toofind wychodzących.
* **Azure aplikacji Nazwa usługi Active Directory** — nazwa hello aplikacji usługi Azure Active Directory, które będzie używane toowrite kluczy tajnych toohello Key Vault. Jeśli taka aplikacja nie istnieje, zostanie utworzona nowa aplikacja o podanej nazwie. Jeśli masz już aplikację usługi Azure Active Directory, które mają toouse, wprowadź nazwę hello tej aplikacji usługi Azure Active Directory.

> [!NOTE]
> Jeśli zastanawiasz się jako toowhy należy toocreate aplikacji usługi Azure Active Directory, można znaleźć pod adresem *zarejestrować aplikację w usłudze Azure Active Directory* w artykule hello [wprowadzenie do korzystania z usługi Azure Key Vault](../key-vault/key-vault-get-started.md).
>
>

Wykonaj hello następujące kroki tooencrypt maszyny wirtualnej platformy Azure:

1. Jeśli hello PowerShell ISE został zamknięty, otwórz wystąpienie hello PowerShell ISE z podwyższonym poziomem uprawnień. Wykonaj instrukcje hello we wcześniejszej części tego artykułu, jeśli powitalne PowerShell ISE nie jest już otwarty. Jeśli skrypt hello został zamknięty, otwórz hello **ADEPrereqScript.ps1** kliknięcie **pliku**, następnie **Otwórz** i wybierając skrypt hello z hello **c:\ AzureADEScript** folderu. Jeśli zostały wykonane w tym artykule od początku hello, przejdź po prostu toohello następnego kroku.
2. W konsoli hello hello PowerShell ISE (hello w dolnym okienku hello PowerShell ISE), należy zmienić hello fokus toohello lokalne powitania skryptu, wpisując **cd c:\AzureADEScript** i naciśnij klawisz **ENTER**.
3. Ustaw zasady wykonywania hello na tym komputerze, co umożliwia uruchamianie skryptu hello. Typ **Set-ExecutionPolicy Unrestricted** w hello konsoli, a następnie naciśnij klawisz ENTER. Jeśli zobaczysz okno dialogowe z informacją o hello skutków hello zmiany tooexecution zasad, kliknij opcję **tak tooall** lub **tak** (Jeśli zostanie wyświetlony **tak tooall**, wybierz tę opcję, jeśli nie ma **tak tooall**, następnie kliknij przycisk **tak**).
4. Zaloguj się do konta platformy Azure. W konsoli hello wpisz **Login-AzureRmAccount** i naciśnij klawisz **ENTER**. Zostanie wyświetlone okno dialogowe, w którym należy wprowadzić poświadczenia (Upewnij się, że masz prawa toochange hello maszyn wirtualnych — Jeśli nie masz uprawnień, nie będzie możliwe tooencrypt je. Jeśli nie masz pewności, zapytaj właściciela subskrypcji lub administratora). Powinny być widoczne informacje dotyczące takich parametrów, jak **Environment**, **Account**, **TenantId**, **SubscriptionId** i **CurrentStorageAccount**. Kopiuj hello **SubscriptionId** tooNotepad. Będzie on potrzebny toouse w kroku #6.
5. Znajdź jaka subskrypcja maszyny wirtualnej należy tooand jego lokalizacji. Przejdź za[https://portal.azure.com](ttps://portal.azure.com) i zaloguj się.  W lewej części strony hello hello, kliknij polecenie **maszyn wirtualnych**. Zostanie wyświetlona lista maszyn wirtualnych i subskrypcje hello, które należą do.

   ![Maszyny wirtualne](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Zwraca toohello PowerShell ISE. Ustaw kontekst subskrypcji hello, w którym będzie uruchamiany hello skryptu. W konsoli hello wpisz **Select-AzureRmSubscription – SubscriptionId < id_subskrypcji >** (Zastąp **< id_subskrypcji >** ze swoim faktycznym Identyfikatorem subskrypcji) i naciśnij klawisz  **Wprowadź**. Zostaną wyświetlone informacje o środowisku hello **konta**, **TenantId**, **SubscriptionId** i **CurrentStorageAccount**.
7. Wszystko jest teraz gotowy toorun hello skryptu. Kliknij przycisk hello **Uruchom skrypt** przycisk lub naciśnij przycisk **F5** hello klawiatury.

   ![Wykonywanie skryptu programu PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. Witaj wyświetleniu zapytania o **resourceGroupName:** — wprowadź nazwę hello *grupy zasobów* ma toouse, naciśnij klawisz **ENTER**. Jeśli nie masz, wprowadź nazwę dla nowej mają toouse. Jeśli masz już *grupy zasobów* mają toouse (na przykład hello jedną należącego do maszyny wirtualnej), wprowadź nazwę hello hello istniejącej grupy zasobów.
9. Witaj wyświetleniu zapytania o **keyVaultName:** — wprowadź nazwę hello hello *Key Vault* toouse, a następnie naciśnij klawisz ENTER. Jeśli nie masz, wprowadź nazwę dla nowej mają toouse. Jeśli masz już magazyn kluczy, które mają toouse, wprowadź nazwę hello istniejących hello *Key Vault*.
10. Witaj wyświetleniu zapytania o **lokalizacji:** — wprowadź nazwę hello hello lokalizacji, w których hello znajduje się maszyna wirtualna ma tooencrypt, a następnie naciśnij klawisz **ENTER**. Jeśli nie pamiętasz lokalizacji hello, przejdź wstecz toostep #5.
11. Witaj wyświetleniu zapytania o **aadAppName:** — wprowadź nazwę hello hello *usługi Azure Active Directory* aplikacji ma toouse, naciśnij klawisz **ENTER**. Jeśli nie masz, wprowadź nazwę dla nowej mają toouse. Jeśli masz już *aplikacji usługi Azure Active Directory* mają toouse, wprowadź nazwę hello istniejących hello *aplikacji usługi Azure Active Directory*.
12. Zostanie wyświetlone okno dialogowe logowania. Podaj poświadczenia (tak, użytkownik zalogował się jeden raz, ale teraz trzeba toodo go ponownie).
13. Hello skrypt zostanie uruchomiony i po zakończeniu jego zapyta wartości hello toocopy hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**i **keyVaultResourceId**. Skopiuj każdy z tych wartości toohello Schowka i wklej je do Notatnika.
14. Zwraca toohello PowerShell ISE i umieść kursor hello na końcu hello hello ostatniego wiersza i naciśnij klawisz **ENTER**.

Hello dane wyjściowe skryptu hello powinien wyglądać podobnie jak na poniższym zrzucie ekranu hello:

![Dane wyjściowe programu PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Szyfrowanie hello maszyny wirtualnej platformy Azure
Użytkownik jest teraz gotowy tooencrypt maszyny wirtualnej. Jeśli Twoja maszyna wirtualna znajduje się w hello tej samej grupie zasobów co magazyn kluczy, można przenieść na toohello szyfrowania kroki sekcji. Jednak jeśli maszyna wirtualna nie jest w hello sam grupie zasobów co magazyn kluczy, potrzebne będą następujące hello tooenter w konsoli hello hello PowerShell ISE:

**$resourceGroupName = <’GZ_maszyny_wirtualnej’>**

Zastąp **< gz_maszyny_wirtualnej >** o nazwie hello hello grupy zasobów, w którym znajdują się maszyny wirtualne, ujętą w pojedynczy cudzysłów. Następnie naciśnij klawisz **ENTER**.
tooconfirm hello poprawna, że została podana nazwa grupy zasobów, wpisz poniżej hello hello konsoli programu PowerShell ISE:

**$resourceGroupName**

Naciśnij klawisz **ENTER**. Witaj nazwę grupy zasobów, które maszyny wirtualne znajdują się w powinna zostać wyświetlona. Na przykład:

![Dane wyjściowe programu PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Kroki szyfrowania
Najpierw należy tootell PowerShell hello nazwę maszyny wirtualnej hello ma tooencrypt. W konsoli hello wpisz:

**$vmName = <’nazwa_maszyny_wirtualnej’>**

Zastąp **<' nazwa_maszyny_wirtualnej' >** o nazwie hello maszyny wirtualnej (Upewnij się, hello ujętą w pojedynczy cudzysłów), a następnie naciśnij klawisz **ENTER**.

tooconfirm hello poprawna, że została podana nazwa maszyny Wirtualnej, wpisz:

**$vmName**

Naciśnij klawisz **ENTER**. Powinna zostać wyświetlona nazwa hello hello maszyny wirtualnej ma tooencrypt. Na przykład:

![Dane wyjściowe programu PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Istnieją dwie metody toorun hello szyfrowania polecenia tooencrypt wszystkie dyski na maszynie wirtualnej hello. Pierwsza metoda Hello jest hello tootype następujące polecenie w konsoli programu PowerShell ISE hello:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Po wpisaniu tego polecenia naciśnij klawisz **ENTER**.

Druga metoda Hello jest tooclick w okienku skryptów hello (hello górne okienko programu PowerShell ISE hello) i przewiń w dół toohello dolnej części skryptu hello. Wyróżnij polecenie hello wymienione powyżej i kliknij prawym przyciskiem myszy kliknij go, a następnie kliknij przycisk **Uruchom zaznaczenie** lub naciśnij klawisz **F8** hello klawiatury.

![Program PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Niezależnie od metody hello używasz, zostanie wyświetlone okno dialogowe informujące, że potrwa 10 – 15 minut toocomplete operacji hello. Kliknij przycisk **Yes** (Tak).

Podczas procesu szyfrowania hello odbywa się, można przywrócić toohello portalu Azure, a następnie sprawdź stan hello hello maszyny wirtualnej. W lewej części strony hello hello, kliknij polecenie **maszyn wirtualnych**, a następnie w hello **maszyn wirtualnych** bloku, kliknij nazwę hello hello maszyny wirtualnej, którą Szyfrujesz. W wyświetlonym bloku hello można zauważyć, że hello **stan** widoczna **aktualizacji**. Oznacza to, że szyfrowanie jest w toku.

![Więcej informacji na temat hello maszyny Wirtualnej](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Zwraca toohello PowerShell ISE. Po ukończeniu działania skryptu hello pojawi się na poniższej ilustracji hello wyświetlaną.

![Dane wyjściowe programu PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate, który hello maszyny wirtualnej jest teraz zaszyfrowana, zwracać toohello portalu Azure i kliknij przycisk **maszyn wirtualnych** na powitania po lewej stronie powitania strony. Kliknij nazwę hello hello maszyny wirtualnej, która została zaszyfrowana. W hello **ustawienia** bloku, kliknij przycisk **dysków**.

![Opcje ustawień](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Na powitania **dysków** bloku, zostanie wyświetlone **szyfrowania** jest **włączone**.

![Właściwości dysku](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Następne kroki
W tym dokumencie możesz przedstawiono sposób tooencrypt maszyny wirtualnej platformy Azure. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiedź
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
