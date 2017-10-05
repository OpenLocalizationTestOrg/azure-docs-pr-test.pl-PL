---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych z systemem Windows za pomocą portalu | Microsoft Docs"
description: "Azure: Szybki start — Tworzenie maszyn wirtualnych z systemem Windows za pomocą portalu"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 31ac18add9c3fd956e0d37b1e0c1a510265c22e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-portal"></a>Tworzenie maszyny wirtualnej z systemem Windows za pomocą witryny Azure Portal

Maszyny wirtualne platformy Azure można utworzyć za pomocą witryny Azure Portal. Ta metoda bazuje na opartym na przeglądarce interfejsie użytkownika umożliwiającym tworzenie i konfigurowanie maszyn wirtualnych oraz wszystkich pokrewnych zasobów. Ten przewodnik Szybki start opisuje proces tworzenia maszyny wirtualnej i instalowania serwera sieci Web na tej maszynie wirtualnej.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej

1. Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.

2. Wybierz pozycję **Wystąpienia obliczeniowe**, a następnie wybierz pozycję **Windows Server 2016 Datacenter**. 

3. Wprowadź informacje o maszynie wirtualnej. Nazwa użytkownika i hasło wprowadzone w tym miejscu są używane na potrzeby logowania się do maszyny wirtualnej. Po zakończeniu kliknij przycisk **OK**.

    ![Wprowadzanie podstawowych informacji o maszynie wirtualnej w bloku portalu](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Wybierz rozmiar maszyny wirtualnej. Aby wyświetlić więcej rozmiarów, wybierz pozycje **Wyświetl wszystkie** lub zmień filtr **Obsługiwany typ dysku**. 

    ![Zrzut ekranu przedstawiający rozmiary maszyn wirtualnych](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. W bloku ustawień pozostaw ustawienia domyślne i kliknij przycisk **OK**.

6. Na stronie podsumowania kliknij przycisk **OK**, aby rozpocząć wdrażanie maszyny wirtualnej.

7. Maszyna wirtualna zostanie przypięta do pulpitu nawigacyjnego witryny Azure Portal. Po zakończeniu wdrożenia zostanie automatycznie otwarty blok podsumowania maszyny wirtualnej.


## <a name="connect-to-virtual-machine"></a>Nawiązywanie połączenia z maszyną wirtualną

Utwórz połączenie pulpitu zdalnego z maszyną wirtualną.

1. Kliknij przycisk **Połącz** we właściwościach maszyny wirtualnej. Zostanie utworzony i pobrany plik Remote Desktop Protocol (rdp).

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. Aby połączyć się z maszyną wirtualną, otwórz pobrany plik RDP. Jeśli zostanie wyświetlony monit, kliknij przycisk **Połącz**. Na komputerze Mac należy skorzystać z klienta RDP, takiego jak ten [klient pulpitu zdalnego](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) ze sklepu Mac App Store.

3. Wprowadź nazwę użytkownika i hasło określone podczas tworzenia maszyny wirtualnej, a następnie kliknij przycisk **OK**.

4. Podczas procesu logowania może pojawić się ostrzeżenie o certyfikacie. Kliknij przycisk **Tak** lub **Kontynuuj**, aby kontynuować nawiązywanie połączenia.


## <a name="install-iis-using-powershell"></a>Instalowanie usług IIS przy użyciu programu PowerShell

Uruchom sesję programu PowerShell na maszynie wirtualnej i uruchom następujące polecenie, aby zainstalować usługi IIS.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Po zakończeniu zamknij sesję RDP i wróć do właściwości maszyny wirtualnej w witrynie Azure Portal.

## <a name="open-port-80-for-web-traffic"></a>Otwieranie portu 80 na potrzeby ruchu w sieci Web 

Sieciowa grupa zabezpieczeń zabezpiecza ruch przychodzący i wychodzący. Po utworzeniu maszyny wirtualnej z poziomu witryny Azure Portal na porcie 3389 jest tworzona reguła ruchu przychodzącego dla połączeń RDP. Ponieważ maszyna wirtualna hostuje serwer sieci Web, należy utworzyć regułę sieciowej grupy zabezpieczeń dla portu 80.

1. Na maszynie wirtualnej kliknij nazwę **grupy zasobów**.
2. Wybierz **sieciową grupę zabezpieczeń**. Sieciową grupę zabezpieczeń można zidentyfikować za pomocą kolumny **Typ**. 
3. W menu po lewej stronie, w obszarze ustawień, kliknij pozycję **Reguły zabezpieczeń dla ruchu przychodzącego**.
4. Kliknij pozycję **Dodaj**.
5. W polu **Nazwa** wpisz wartość **http**. Upewnij się, że w polu **Zakres portów** ustawiono wartość 80, a w polu **Akcja** — wartość **Zezwalaj**. 
6. Kliknij przycisk **OK**.


## <a name="view-the-iis-welcome-page"></a>Wyświetlanie strony powitalnej usług IIS

Po zainstalowaniu usług IIS i otwarciu portu 80 dla maszyny wirtualnej można uzyskać dostęp do serwera sieci Web z Internetu. Otwórz przeglądarkę internetową i wpisz publiczny adres IP maszyny wirtualnej. Publiczny adres IP można znaleźć w bloku maszyny wirtualnej w witrynie Azure Portal.

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć. W tym celu wybierz grupę zasobów z bloku maszyny wirtualnej, a następnie kliknij przycisk **Usuń**.

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web. Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Windows.

> [!div class="nextstepaction"]
> [Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows](./tutorial-manage-vm.md)
