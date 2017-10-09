Przed użyciem hello wiersza polecenia platformy Azure z Menedżera zasobów polecenia i szablony toodeploy Azure zasobów i obciążeń przy użyciu grup zasobów, musisz mieć konto platformy Azure. Jeśli nie posiadasz konta, możesz skorzystać z [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

Jeśli nie została jeszcze zainstalowana hello wiersza polecenia platformy Azure i połączone tooyour subskrypcji, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](../articles/cli-install-nodejs.md) Ustaw tryb hello zbyt`arm` z `azure config mode arm`i uzyskuj tooAzure hello `azure login` polecenia.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- Azure CLI 10 — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Podstawowe polecenia usługi Azure Resource Manager w interfejsie wiersza polecenia platformy Azure
W tym artykule omówiono podstawowe polecenia spowoduje mają toouse z toomanage wiersza polecenia platformy Azure i interakcji z zasobami (głównie maszyn wirtualnych) w Twojej subskrypcji platformy Azure.  Bardziej szczegółowe pomocy z przełącznikami określonego wiersza polecenia i opcjami, wpisując można użyć hello pomocy online polecenia i opcje `azure <command> <subcommand> --help` lub `azure help <command> <subcommand>`.

> [!NOTE]
> Te przykłady nie obejmują operacji opartych na szablonach, które są zazwyczaj zalecane w przypadku wdrożeń maszyn wirtualnych w usłudze Resource Manager. Aby uzyskać informacje, zobacz [hello Użyj wiersza polecenia platformy Azure z usługą Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) i [Wdróż i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Zadanie | Resource Manager |
| --- | --- | --- |
| Utwórz hello najbardziej podstawowa maszyna wirtualna |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Uzyskaj hello `image-urn` z hello `azure vm image list` polecenia. Zapoznaj się z przykładami w [tym artykule](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). |
| Tworzenie maszyny wirtualnej z systemem Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Tworzenie maszyny wirtualnej z systemem Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Wyświetlanie listy maszyn wirtualnych |`azure  vm list [options]` |
| Uzyskiwanie informacji o maszynie wirtualnej |`azure  vm show [options] <resource_group> <name>` |
| Uruchamianie maszyny wirtualnej |`azure vm start [options] <resource_group> <name>` |
| Zatrzymywanie maszyny wirtualnej |`azure vm stop [options] <resource_group> <name>` |
| Cofanie przydziału maszyny wirtualnej |`azure vm deallocate [options] <resource-group> <name>` |
| Ponowne uruchamianie maszyny wirtualnej |`azure vm restart [options] <resource_group> <name>` |
| Usuwanie maszyny wirtualnej |`azure vm delete [options] <resource_group> <name>` |
| Przechwytywanie maszyny wirtualnej |`azure vm capture [options] <resource_group> <name>` |
| Tworzenie maszyny wirtualnej na podstawie obrazu użytkownika |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Tworzenie maszyny wirtualnej na podstawie wyspecjalizowanego dysku |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Dodaj tooa dysku danych maszyny Wirtualnej |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Usuwanie dysku danych z maszyny wirtualnej |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Dodaj tooa ogólnego rozszerzenia maszyny Wirtualnej |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Dodaj tooa rozszerzenia dostępu do maszyny Wirtualnej maszyny Wirtualnej |`azure vm reset-access [options] <resource-group> <name>` |
| Dodaj Docker tooa rozszerzenia maszyny Wirtualnej |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Usuwanie rozszerzenia maszyny wirtualnej |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Używanie zasobów maszyny wirtualnej |`azure vm list-usage [options] <location>` |
| Pobieranie wszystkich rozmiarów maszyn wirtualnych |`azure vm sizes [options]` |

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać dodatkowe przykłady poleceń interfejsu wiersza polecenia hello wykraczające poza podstawowe możliwości zarządzania maszyny Wirtualnej, zobacz [hello Using Azure CLI z usługi Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
