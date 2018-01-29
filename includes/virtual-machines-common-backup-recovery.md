
## <a name="azure-backup"></a>Azure Backup

Do tworzenia kopii zapasowych maszyn wirtualnych Azure uruchamiania obciążeń produkcyjnych, użyj kopii zapasowej Azure. Kopia zapasowa Azure obsługuje kopie zapasowe spójnych z aplikacją dla systemu Windows i maszyn wirtualnych systemu Linux. Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego. Po przywróceniu z punktu odzyskiwania, można przywrócić całej maszyny Wirtualnej lub po prostu określonych plików. 

Proste, praktyczne wprowadzenie do usługi Kopia zapasowa Azure dla maszyn wirtualnych platformy Azure, zobacz samouczek "kopii zapasowych maszyn wirtualnych platformy Azure" dla [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) lub [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).

Aby uzyskać więcej informacji na sposób działania usługi Kopia zapasowa Azure, zobacz [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej na platformie Azure](../articles/backup/backup-azure-vms-introduction.md)


## <a name="azure-site-recovery"></a>Azure Site Recovery

Usługa Azure Site Recovery chroni maszyn wirtualnych w przypadku poważnej awarii, gdy całego regionu ulegnie awarii z powodu poważne klęski lub powszechnie przerw w obsłudze. Można skonfigurować usługi Azure Site Recovery dla maszyn wirtualnych, dzięki czemu będzie można odzyskać aplikacji za pomocą jednego kliknięcia w kilku minut. Można replikować do regionu platformy Azure wybrane, nie jest ograniczone do sparowanego regionów. 

Testowanie odzyskiwania po awarii z na żądanie testu pracy w trybie Failover, można uruchomić bez wpływu na Twoje obciążeń produkcyjnych lub trwającej replikacji. Tworzenie planów odzyskiwania do organizowania trybu failover i powrotu po awarii całej aplikacji uruchomionych na wiele maszyn wirtualnych. Funkcja planu odzyskiwania jest zintegrowany z elementu runbook usługi Automatyzacja Azure.

Możesz rozpocząć pracę przez [replikowanie maszyn wirtualnych](https://aka.ms/a2a-getting-started). 

## <a name="managed-snapshots"></a>Zarządzane migawki 

W środowiskach programistycznych i testowych migawki zapewniają szybki i prosty opcji tworzenia kopii zapasowych maszyn wirtualnych, które używają dysków zarządzanych. Zarządzane migawka jest tylko do odczytu pełnej kopii dysku zarządzanego. Migawki istnieje niezależnie od dysku źródłowego i mogą służyć do tworzenia nowych dysków zarządzanych odbudowywania maszyny Wirtualnej. Są one rozliczane oparte na używane część dysku. Na przykład po utworzeniu migawki dysków zarządzanych z elastycznie pojemności 64 GB i rozmiaru rzeczywistego używanych danych wynosi 10 GB migawki będą naliczane tylko za używanych danych rozmiar 10 GB.  

Aby uzyskać więcej informacji na temat tworzenia migawek zobacz:

* [Tworzenie kopii wirtualnego dysku twardego przechowywanej jako dysk zarządzany przy użyciu migawek w systemie Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Tworzenie kopii wirtualnego dysku twardego przechowywanej jako dysk zarządzany przy użyciu migawek w systemie Linux](../articles/virtual-machines/linux/snapshot-copy-managed-disk.md)



## <a name="next-steps"></a>Kolejne kroki
Można wypróbować usługę kopia zapasowa Azure, postępując "Kopii zapasowej samouczek maszyn wirtualnych systemu Windows" dla [Linux](../articles/virtual-machines/linux/tutorial-backup-vms.md) lub [Windows](../articles/virtual-machines/windows/tutorial-backup-vms.md).
