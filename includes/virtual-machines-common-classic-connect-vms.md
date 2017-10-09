

![Maszyny wirtualne w autonomicznej usługi w chmurze](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Jeśli w sieci wirtualnej maszyn wirtualnych, można zdecydować, zestawy dostępności i równoważenia obciążenia ma toouse dla ilu usługi w chmurze. Ponadto można organizować hello maszyn wirtualnych w podsieciach w hello sam sposób jak lokalnej sieci i połącz hello tooyour wirtualnej sieci lokalnej sieci. Oto przykład:

![Maszyny wirtualne w sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Sieci wirtualne są hello zalecany sposób maszyn wirtualnych tooconnect na platformie Azure. Witaj najlepszym rozwiązaniem jest tooconfigure każdej warstwy aplikacji w usłudze oddzielne chmury. Może jednak toocombine niektórych maszyn wirtualnych z warstwami inną aplikację do hello sam chmury tooremain usługi w ramach hello maksymalnie 200 usługi w chmurze na subskrypcję. tooreview to i inne ograniczenia, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Połączenie maszyn wirtualnych w sieci wirtualnej
tooconnect maszyn wirtualnych w sieci wirtualnej:

1. Utwórz sieć wirtualną hello w hello [portalu Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) i określ "classic deployment".
2. Utwórz zestaw hello usługi w chmurze dla Twojego tooreflect wdrażania projektu dla zestawów dostępności i równoważenie obciążenia. W hello portalu Azure, kliknij przycisk **nowe > obliczenia > Usługa w chmurze** dla każdej usługi w chmurze.

  W trakcie wypełniania szczegóły usługi w chmurze hello, wybierz hello sam _grupy zasobów_ używane z hello sieci wirtualnej.

3. toocreate każda nowa wirtualnego komputera, kliknij przycisk **nowy > obliczeniowe**, a następnie wybierz hello odpowiedni obraz maszyny Wirtualnej z hello **wyróżnionych aplikacji**.

  W hello maszyny Wirtualnej **podstawy** bloku, wybierz hello sam _grupy zasobów_ używane z hello sieci wirtualnej.

  ![Blok podstawowych ustawień maszyny Wirtualnej przy użyciu sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. W trakcie wypełniania hello wirtualna **ustawienia**, wybierz poprawny hello _usługi w chmurze_ lub _sieci wirtualnej_ dla hello maszyny Wirtualnej.

  Azure wybierze hello innych elementów zależności.

  ![Blok ustawień maszyny Wirtualnej przy użyciu sieci wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Połączenie maszyn wirtualnych w autonomicznej usługi w chmurze
maszyny wirtualne tooconnect w autonomicznej usługi w chmurze:

1. Utwórz usługę w chmurze hello w hello [portalu Azure](http://portal.azure.com). Kliknij przycisk **nowe > obliczenia > Usługa w chmurze**. Lub można utworzyć usługi w chmurze hello wdrożenia po utworzeniu pierwszej maszyny wirtualnej.
2. Podczas tworzenia maszyn wirtualnych hello wybierz hello używać tej samej grupie zasobów z usługi w chmurze hello.

  ![Dodawanie maszyny wirtualnej tooan istniejącej usługi w chmurze](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  W trakcie wypełniania hello szczegóły maszyny Wirtualnej, wybierz nazwę hello utworzonego w kroku pierwszego hello usługi w chmurze.

  ![Wybierając usługę chmury dla maszyny wirtualnej](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
