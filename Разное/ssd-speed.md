-> % sudo nvme list -v
Subsystem        Subsystem-NQN                                                                                    Controllers
---------------- ------------------------------------------------------------------------------------------------ ----------------
nvme-subsys0     nqn.2020-04.com.kingston:nvme:nvm-subsystem-sn-50026B7785D77B4E                                  nvme0
nvme-subsys1     nqn.2020-04.com.kingston:nvme:nvm-subsystem-sn-50026B728376F6BE                                  nvme1

Device           Cntlid SN                   MN                                       FR       TxPort Address        Slot   Subsystem    Namespaces
---------------- ------ -------------------- ---------------------------------------- -------- ------ -------------- ------ ------------ ----------------
nvme0    0      50026B7785D77B4E     KINGSTON SNV3S1000G                      ERFK1N.3 pcie   0000:02:00.0          nvme-subsys0 nvme0n1
nvme1    1      50026B728376F6BE     KINGSTON SFYRSK1000G                     EIFK51.2 pcie   0000:0e:00.0          nvme-subsys1 nvme1n1

Device            Generic           NSID       Usage                                             Format           Controllers
----------------- ----------------- ---------- ------------------------------------------------- ---------------- ----------------
/dev/nvme0n1      /dev/ng0n1        0x1          1.00 TB /   1.00 TB ( 931.51 GiB /  931.51 GiB) 512   B +  0 B   nvme0
/dev/nvme1n1      /dev/ng1n1        0x1          1.00 TB /   1.00 TB ( 931.51 GiB /  931.51 GiB) 512   B +  0 B   nvme1
max@arch-pc [05:30:57] [~]
-> % sudo lspci -vv -s 0000:02:00.0 | grep -E "LnkCap|LnkSta"
		LnkCap:	Port #1, Speed 16GT/s, Width x4, ASPM L1, Exit Latency L1 unlimited
		LnkSta:	Speed 16GT/s, Width x4
		LnkCap2: Supported Link Speeds: 2.5-16GT/s, Crosslink- Retimer+ 2Retimers+ DRS-
		LnkSta2: Current De-emphasis Level: -3.5dB, EqualizationComplete+ EqualizationPhase1+
max@arch-pc [05:32:43] [~]
-> % sudo lspci -vv -s 0000:0e:00.0 | grep -E "LnkCap|LnkSta"
		LnkCap:	Port #0, Speed 16GT/s, Width x4, ASPM L1, Exit Latency L1 <64us
		LnkSta:	Speed 16GT/s, Width x2 (downgraded)
		LnkCap2: Supported Link Speeds: 2.5-16GT/s, Crosslink- Retimer+ 2Retimers+ DRS-
		LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete+ EqualizationPhase1+
max@arch-pc [05:32:48] [~]
-> %




🧩 Результат по каждому SSD
🔹 0000:02:00.0

LnkCap: Speed 16GT/s, Width x4
LnkSta: Speed 16GT/s, Width x4

➡ PCIe 4.0 x4 (в полном режиме)
✅ Работает на максимальной поддерживаемой скорости
(16 GT/s = PCIe 4.0, x4 — 4 линии PCIe).
🔹 0000:0e:00.0

LnkCap: Speed 16GT/s, Width x4
LnkSta: Speed 16GT/s, Width x2 (downgraded)

➡ PCIe 4.0 x2 (ограничено до 2 линий)
⚠️ То есть диск поддерживает PCIe 4.0 x4, но сейчас работает только на x2.
🔍 Почему второе устройство работает на x2:

Возможные причины:

    🔧 Второй M.2 слот на материнской плате физически имеет только 2 линии PCIe (часто так делают, если первый слот подключен к CPU, а второй — к чипсету).

    🔌 В слот вставлен адаптер или райзер, ограничивающий количество линий.

    🧠 BIOS может быть настроен в режиме, ограничивающем линии (например, “PCIe bifurcation” или “Shared with GPU slot”).

💡 Вывод:
NVMe	PCIe версия	Линии	Состояние
0000:02:00.0	PCIe 4.0	x4	✅ Полная скорость
0000:0e:00.0	PCIe 4.0	x2	⚠️ Ограничено (в 2 раза медленнее по пропускной способности)

