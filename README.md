# LoongArch CSR 和 IOCSR 整理

## CSR

### GTLBC (0x15, Guest TLB Control)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.7-rc1)

字段：

1. GMTLBSZ: [5:0]
2. USETGID(renamed from USERID): [12], Use TGID, Enable using TGID
3. TOTI: [13], Trap on TLB instruction?
4. TGID(renamed from RID): [23:16], relevant to GSTAT.GID

When switching to guest: set TGID = GSTAT.GID; switching to host: set TGID = 0.

### TRGP (0x16, TLBR read guest info)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. GTLB: [0]
2. RID: [23:16]

unused in kernel

### GSTAT (0x50, Guest status)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. VM: [0], In Virtual Machine
2. PVM: [1], Previous VM, for ERTN PVM=1 means to enter VM, Set PVM bit to setup ertn to guest context, Disable PGM bit to enter root mode by default with next ertn
3. GIDBIT: [9:4]
2. GID: [23:16], Guest ID, correspond to VPID(Virtual Processor ID) in KVM

### GCFG (0x51, Guest config)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.7-rc1)

字段：

1. MATP_GUEST: [0], Memory Access Type?
2. MATP_ROOT: [1], Memory Access Type?
3. MATP_NEST: [2], Memory Access Type?
4. MATC: [5:4], 0=GUEST, 1=ROOT(Control guest page CCA attribute), 2=NEST
5. SITP: [6]
6. SIT: [7]
7. TITP: [8]
8. TIT: [9], Trap on timer, Disable guest use of hard timer
9. TOEP: [10]
10. TOE: [11], Trap on exception
11. TOPP: [12]
12. TOP: [13], Trap on privilege
13. TORUP: [14]
14. TORU: [15], Trap on root unimplemented
15. GCIP: [19:16], 0bxxx1=ALL, 0bxx1x=HIT, 0bx1xx=SECURE
16. GCI: [21:20], 0=ALL, 1=HIT, 2=SECURE(Trap on init or unimplemented cache instruction)
17. GPERF: [26:24]


### GINTC (0x52, Guest interrupt control)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6) [MIPS Virtualization Module](https://mips.com/products/architectures/ase/virtualization/)

字段：

1. VIP: [7:0] Virtual Interrupt Pending, write 1 to the bits in this field to inject the corresponding interrupt to the guest and 0 to clear it. See MIPS `GuestCtl2.VIP`.
2. PIP: [15:8] Pending Interrupt Passthrough, write 1 to the bits in this field to make the corresponding interrupt visible to the guest. See MIPS `GuestCtl0.PIP`.
3. HC: [23:16] Hardware Clear, set bits in this field to 1 to allow the the corresponding guest interrupt to be cleared by hardware and 0 to allow only manual clearing. See MIPS `GuestCtl2.HC`.

### GCNTC (0x53, Guest timer offset)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6) [MIPS Virtualization Module](https://mips.com/products/architectures/ase/virtualization/)

See MIPS `GTOffset`.

### IMPCTL1 (0x80, Loongson config1)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. DATAPRE: [0], Data Prefetch
2. INSTPRE: [1], Instruction Prefetch
3. STPRE: [3:2]
4. RASDIS: [4], Return Address Stack Disable
5. BRBTDIS: [5]
6. LLSYNC: [6]
7. LIFEP: [7]
8. STFILL: [8], Store Fill Buffer
9. AUTO_FLUSHSFB: [9]
10. ANTI_MISPEC: [10]
11. USERCAC: [11]
12. FASTLDQ: [12], Fast LD.Q
13. DCLRU: [13], Data Cache LRU
14. VCLRU: [14], Victim Cache LRU
15. DISVC: [15]
16. LLEXCL: [16]
17. SCRAND: [17]
18. SSEN: [18]
19. MISPEC: [27:20]

### IMPCTL2 (0x81, Loongson config2)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. MTLB: [0]
2. STLB: [1]
3. DTLB: [2]
4. ITLB: [3]
5. BTAC: [4]

### GNMI (0x82)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

### MCSR0 (0xC0, Shadow of CPUCFG0 and CPUCFG1)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG0: [31:0]
2. CPUCFG1: [63:32]

### MCSR1 (0xC1, Shadow of CPUCFG2 and CPUCFG3)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG2: [31:0]
2. CPUCFG3: [63:32]

### MCSR2 (0xC2, Shadow of CPUCFG4 and CPUCFG5)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG4: [31:0]
2. CPUCFG5: [63:32]

### MCSR3 (0xC3, Shadow of CPUCFG6)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG6: [31:0]

### MCSR8 (0xC8, Shadow of CPUCFG16 and CPUCFG17)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG16: [31:0]
2. CPUCFG17: [63:32]

### MCSR9 (0xC9, Shadow of CPUCFG18 and CPUCFG19)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG18: [31:0]
2. CPUCFG19: [63:32]

### MCSR10 (0xCA, Shadow of CPUCFG20)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG20: [31:0]

### MCSR24 (0xF0, Shadow of CPUCFG48)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. CPUCFG48: [31:0]

### UCAWIN (0x100-0x109, Uncached accelerate windows)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

## CPUCFG

### CPUCFG48

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. MCSRLOCK: [0]: MSR Lock
2. NAPEN: [1]
3. VFPUCG: [2]
4. RAMCG: [3]


## IOCSR

IOCSR 可以通过 IOCSR 指令读写，也可以通过 MMIO 读写，其中 MMIO 方式的基地址为 0x1fe00000 或者 0x1fe10000，按 CPU 的内部结点号决定。

参考：3A6000 用户手册、Linux `arch/loongarch/include/asm/loongarch.h`。

### 0x0000: Version

字段：

1. Version: [7:0], 0x14(3A6000)

### 0x0008: Features

字段：

1. Temperature: [0], IOCSR[0x428] is available
2. Node Counter: [1], IOCSR[0x408] is available
3. MSI(Message Signaled Interrupt): [2]
4. EXT IOI(External I/O Interrupt): [3]
5. CSR IPI(Inter Processor Interrupt): [4], Send IPI via per-core CSR
6. Frequency CSR: [5], Control frequency via per-core CSR
7. Frequency Scaling: [6]
8. DVFS V1: [7]
9. Temperature Sensor: [8]
10. EIO(External I/O) DECODE: [9]
11. Flat Mode: [10]
12. VM: [11]
13. Frequency Scale 16: [12]
14. Interrupt Remap: [13]
15. SE(Secure Element) enabled: [14]

### 0x0010: Vendor

### 0x0020: CPU Name

### 0x0180: Feature Configuration

字段：

1. MC0 Disable Configuration Space: [4]
2. MC0 Default Configuration Space: [5], Route all memory access to configuration space
3. MC0 Reset Negative: [7]
4. MC0 Clock Enable: [8]
5. MC1 Disable Configuration Space: [9]
6. MC1 Default Configuration Space: [10], Route all memory access to configuration space
7. MC1 Reset Negative: [12]
8. MC1 Clock Enable: [13]
9. HT Frequency Scaling Control: [26:24]
10. HT Clock Enable: [27]
11. Node Frequency Control: [42:40]
12. CPU Version: [63:56]

MC: Memory Controller
HT: HyperTransport

### 0x0188: Pin Configuration

字段：

1. HT Sideband: [19:16]
2. I2C: [23:20]
3. UART: [27:24]
4. SPI: [31:28]
5. GPIO: [35:32]
6. SE UART: [39:36]
7. SE SPI: [43:40]
8. SE I2C: [47:44]
9. SE SCI: [51:48]
10. SE RNG: [55:52]
11. SE GPIO: [59:56]

SE: Secure Element

### 0x0199: Config Pin Sampling

字段：

1. Chip Config: [37:32]
2. System Chip Config: [47:38]
3. Bad IP Core: [55:48]
4. Bad IP DDR: [57:56]
5. Bad IP HT: [61:60]

### 0x0198: Temperature Sampling

字段：

1. Do Test: [20]
2. Temperature Sensor 0 Overflow: [24]
3. Temperature Sensor 1 Overflow: [25]
4. Temperature Sensor 0 Output: [47:32]
5. Temperature Sensor 1 Output: [63:48]

### 0x01B0: Frequency Configuration

字段：

1. Select PLL for Node Clock: [0]
2. Allow Software to Set PLL: [2]
3. Bypass L1 PLL: [3]
4. Bypass L2 PLL: [4]
5. Enable VDDA LDO: [8]
6. Enable VDDO LDO: [9]
7. L2 Reset Negative: [12]
8. L2 Clock Output Enable: [13]
9. L2 Fractional Enable: [15]
10. L1 PLL Locked: [16]
11. L2 PLL Locked: [17]
12. Power Down L1: [19]
13. Power Down L2: [20]
14. Select L2 PLL: [22]
15. L1 PLL Reference Clock Cycles: [31:26]
16. L1 PLL Loop Cycles: [40:32]
17. L1 PLL Output Cycles: [47:42]
18. L2 PLL Reference Clock Cycles: [51:48]
19. L2 PLL Loop Cycles: [63:54]
20. L2 PLL Log 2 of Output Cycles: [66:64]
21. L2 PLL Fractional: [115:96]

PLL Output Frequency: (Input Clock / Reference Clock Cycles * Loop Cycles) / Output Cycles

### 0x01C0: Memory Frequency Configuration

字段：

1. Select Mem PLL Source: [0]
2. Allow Software to Set Mem PLL: [1]
3. Bypass Mem PLL: [2]
4. Memory Clock Division Reset Negative: [3]
5. Memory Clock Mode: [5:4]
6. Memory PLL Locked: [6]
7. Power DOwn Memory PLL: [7]
8. Mem PLL Reference Clock Cycles: [13:8]
9. Mem PLL Loop Cycles: [23:14]
10. Mem PLL Output Cycles: [29:24]
11. Node Clock Select: [30]

### 0x01D0: Core Frequency Configuration

字段：

1. Core 0 Frequency Control: [2:0]
2. Core 0 Clock Enable: [3]
3. Core 1 Frequency Control: [6:4]
4. Core 1 Clock Enable: [7]
5. Core 2 Frequency Control: [10:8]
6. Core 2 Clock Enable: [11]
7. Core 3 Frequency Control: [14:12]
8. Core 3 Clock Enable: [15]

### 0x01D8: Core Reset Configuration

字段：

1. Core 0 Pre-Reset Negative: [0]
2. Core 0 Reset Negative: [1]
3. Core 1 Pre-Reset Negative: [2]
4. Core 1 Reset Negative: [3]
5. Core 2 Pre-Reset Negative: [4]
6. Core 2 Reset Negative: [5]
7. Core 3 Pre-Reset Negative: [6]
8. Core 3 Reset Negative: [7]

Reset procedure:

1. Set Reset Negative to Zero
2. Set Pre-Reset Negative to Zero
3. Wait for 500us
4. Set Pre-Reset Negative to One
5. Set Reset Negative to One

### 0x0200: Shared Cache Lock Window 0 Address

字段：

1. Lock Window 0 Address: [47:0]
2. Lock Window 0 Valid: [63]

### 0x0208: Shared Cache Lock Window 1 Address

字段：

1. Lock Window 1 Address: [47:0]
2. Lock Window 1 Valid: [63]

### 0x0210: Shared Cache Lock Window 2 Address

字段：

1. Lock Window 2 Address: [47:0]
2. Lock Window 2 Valid: [63]

### 0x0218: Shared Cache Lock Window 3 Address

字段：

1. Lock Window 3 Address: [47:0]
2. Lock Window 3 Valid: [63]

### 0x0240: Shared Cache Lock Window 0 Mask

字段：

1. Lock Window 0 Mask: [47:0]

### 0x0248: Shared Cache Lock Window 1 Mask

字段：

1. Lock Window 1 Mask: [47:0]

### 0x0250: Shared Cache Lock Window 2 Mask

字段：

1. Lock Window 2 Mask: [47:0]

### 0x0258: Shared Cache Lock Window 3 Mask

字段：

1. Lock Window 3 Mask: [47:0]

### 0x0280: Shared Cache Configuration

字段：

1. LRU Enable: [0]
2. Prefetch Enable: [16]
3. Prefetch Config: [22:20]
4. Prefetch Lookahead: [26:24]
6. SC Stall DIRQ Cycle: [30:28]
7. MCC Store Fill Enable: [31]
8. MCC Clean Exclusive Replace: [35]
9. MCC Clean Shared Replace: [36]

### 0x0400: Routing Configuration

字段：

1. Shared Cache ID Selection: [3:0]
2. Disable 0x3FF00000: [9]
3. Shared Cache 1MB size: [14]
4. MC Enable: [31:30]
5. Memory Interleave Bit: [37:32]
6. Memory Interleave Enable: [39]
7. HT Control: [43:40]

### 0x0408: Node Counter

### 0x0420: Other Configuration

字段：

1. Disable JTAG: [0]
2. Disable Core JTAG: [1]
3. Disable LA132: [2]
4. Disable LA132 JTAG: [3]
5. Disable Anti Fuse 0: [4]
6. Disable Anti Fuse 1: [5]
7. Disable ID Modification: [6]
8. LA132 Reset Negative: [8]
9. LA132 Sleeping: [9]
10. LA132 Soft Interrupt: [15:10]
11. LA132 Frequency Scaling: [18:16]
12. LA132 Clock Enable: [19]
13. Stable Clock Reset Negative: [21]
14. Per Core Frequency Scaling: [22]
15. Per Core Clock Enable: [23]
16. Configuration Bus Timeout: [27:24]
17. Software HT Reset Negative: [29:28]
18. Core Clock Frequency Scaling Mode: [35:32]
19. Node Clock Frequency Scaling Mode: [36]
20. LA132 Clock Frequency Scaling Mode: [37]
21. HT Clock Frequency Scaling Mode: [39:38]
22. Stable Clock Frequency Scaling Mode: [40]
23. Stable Clock Frequency Scaling: [46:44]
24. Stable Clock Enable: [47]
25. EXT IOI Enable: [48]
26. Interrupt Decode: [49]
27. Interrupt Remap Enable: [51]
28. Temperature Sensor Select: [57:56]
29. Auto Scaling: [62:60]
30. Auto Scaling Status: [63]

### 0x0428: Temperature

字段：

1. Temperature: [7:0]

### 0x0438: SRAM Control

字段：

1. SRAM Control: [7:0]

### 0x0460: Fuse 0

### 0x0470: Fuse 1

### 0x0500: GPIO Output Enable

字段：

1. GPIO Output Enable Negative: [31:0]
2. GPIO Function Enable Negative: [63:32]

### 0x0508: GPIO I/O

字段：

1. GPIO Output: [31:0]
2. GPIO Input: [63:32]

### 0x0510: GPIO Interrupt

字段：

1. GPIO Interrupt Polarity: [31:0]
2. GPIO Interrupt Enable: [63:32]

### 0x0600: MC 0 ECC Control
### 0x0610: MC 0 ECC Counter
### 0x0618: MC 0 ECC Counter for each CS
### 0x0620: MC 0 ECC Code
### 0x0628: MC 0 ECC Address
### 0x0630: MC 0 ECC Data 0
### 0x0638: MC 0 ECC Data 1
### 0x0640: MC 0 ECC Data 2
### 0x0648: MC 0 ECC Data 3
### 0x0700: MC 1 ECC Control
### 0x0710: MC 1 ECC Counter
### 0x0718: MC 1 ECC Counter for each CS
### 0x0720: MC 1 ECC Code
### 0x0728: MC 1 ECC Address
### 0x0730: MC 1 ECC Data 0
### 0x0738: MC 1 ECC Data 1
### 0x0740: MC 1 ECC Data 2
### 0x0748: MC 1 ECC Data 3

### 0x1000: Core 0 IPI Status
### 0x1000: Per Core IPI Status
### 0x1004: Core 0 IPI Enable
### 0x1004: Per Core IPI Enable
### 0x1008: Core 0 IPI Set
### 0x1008: Per Core IPI Set
### 0x100C: Core 0 IPI Clear
### 0x100C: Per Core IPI Clear
### 0x1010: Per Core Interrupt Status Register
### 0x1020: Core 0 MailBox 0
### 0x1020: Per Core MailBox 0
### 0x1028: Core 0 MailBox 1
### 0x1028: Per Core MailBox 1
### 0x1030: Core 0 MailBox 2
### 0x1030: Per Core MailBox 2
### 0x1038: Core 0 MailBox 3
### 0x1038: Per Core MailBox 3

### 0x1040: IPI Send
### 0x1048: MailBox Send

### 0x1050: Per Core Frequency Scaling

字段：

1. Frequency Scaling: [2:0]
2. Clock Enable: [3]
3. Frequency Scaling Mode: [4]

### 0x1058: Frequency Send

### 0x1060: Timer Configuration

来源：Linux

### 0x1070: Timer Tick

来源：Linux

### 0x1100: Core 1 IPI Status
### 0x1104: Core 1 IPI Enable
### 0x1108: Core 1 IPI Set
### 0x110C: Core 1 IPI Clear
### 0x1120: Core 1 MailBox 0
### 0x1128: Core 1 MailBox 1
### 0x1130: Core 1 MailBox 2
### 0x1138: Core 1 MailBox 3
### 0x1140: External I/O Interrupt Send

### 0x1158: Any Send

### 0x1200: Core 2 IPI Status
### 0x1204: Core 2 IPI Enable
### 0x1208: Core 2 IPI Set
### 0x120C: Core 2 IPI Clear
### 0x1220: Core 2 MailBox 0
### 0x1228: Core 2 MailBox 1
### 0x1230: Core 2 MailBox 2
### 0x1238: Core 2 MailBox 3

### 0x1280: ECC Enable

### 0x1300: Core 3 IPI Status
### 0x1304: Core 3 IPI Enable
### 0x1308: Core 3 IPI Set
### 0x130C: Core 3 IPI Clear
### 0x1320: Core 3 MailBox 0
### 0x1328: Core 3 MailBox 1
### 0x1330: Core 3 MailBox 2
### 0x1338: Core 3 MailBox 3

### 0x1420: Interrupt Status Register
### 0x1424: Interrupt Enable Register
### 0x1428: Interrupt Enable Set
### 0x142c: Interrupt Enable Clear
### 0x1434: Interrupt Edge
### 0x1440: Interrupt Status Register for Core 0
### 0x1448: Interrupt Status Register for Core 1
### 0x1450: Interrupt Status Register for Core 2
### 0x1458: Interrupt Status Register for Core 3

### 0x1460: High Temperature Interrupt Control
### 0x1468: Low Temperature Interrupt Control
### 0x1470: Temperature Interrupt Status/Clear
### 0x1478: Temperature Interrupt High
### 0x1480: Temperature Frequency Scaling
### 0x1490: Temperature Frequency Scaling High
### 0x1498: Temperature Control

### 0x14A0-0x14BE: External I/O Node Type

### 0x14C0: External I/O Interrupt Mapping [31:0]
### 0x14C1: External I/O Interrupt Mapping [63:32]
### 0x14C2: External I/O Interrupt Mapping [95:64]
### 0x14C3: External I/O Interrupt Mapping [127:96]
### 0x14C4: External I/O Interrupt Mapping [159:128]
### 0x14C5: External I/O Interrupt Mapping [191:160]
### 0x14C6: External I/O Interrupt Mapping [223:192]
### 0x14C7: External I/O Interrupt Mapping [255:224]

### 0x1580: Temperature Sensor 0 Control
### 0x1588: Temperature Sensor 0 Data
### 0x1590: Temperature Sensor 1 Control
### 0x1598: Temperature Sensor 1 Data

### 0x1600: External I/O Interrupt Enable [63:0]
### 0x1608: External I/O Interrupt Enable [127:64]
### 0x1610: External I/O Interrupt Enable [191:128]
### 0x1618: External I/O Interrupt Enable [255:192]

### 0x1680: External I/O Interrupt Bounce [63:0]
### 0x1688: External I/O Interrupt Bounce [127:64]
### 0x1690: External I/O Interrupt Bounce [191:128]
### 0x1698: External I/O Interrupt Bounce [255:192]

### 0x1700: External I/O Interrupt Status Register [63:0]
### 0x1708: External I/O Interrupt Status Register [127:64]
### 0x1710: External I/O Interrupt Status Register [191:128]
### 0x1718: External I/O Interrupt Status Register [255:192]

### 0x1800: External I/O Interrupt Status Register for Core 0 [63:0]
### 0x1800: External I/O Interrupt Status Register Per Core [63:0]
### 0x1808: External I/O Interrupt Status Register for Core 0 [127:64]
### 0x1808: External I/O Interrupt Status Register Per Core [127:64]
### 0x1810: External I/O Interrupt Status Register for Core 0 [191:128]
### 0x1810: External I/O Interrupt Status Register Per Core [191:128]
### 0x1818: External I/O Interrupt Status Register for Core 0 [255:192]
### 0x1818: External I/O Interrupt Status Register Per Core [255:192]

### 0x1900: External I/O Interrupt Status Register for Core 1 [63:0]
### 0x1908: External I/O Interrupt Status Register for Core 1 [127:64]
### 0x1910: External I/O Interrupt Status Register for Core 1 [191:128]
### 0x1918: External I/O Interrupt Status Register for Core 1 [255:192]

### 0x1A00: External I/O Interrupt Status Register for Core 2 [63:0]
### 0x1A08: External I/O Interrupt Status Register for Core 2 [127:64]
### 0x1A10: External I/O Interrupt Status Register for Core 2 [191:128]
### 0x1A18: External I/O Interrupt Status Register for Core 2 [255:192]

### 0x1B00: External I/O Interrupt Status Register for Core 3 [63:0]
### 0x1B08: External I/O Interrupt Status Register for Core 3 [127:64]
### 0x1B10: External I/O Interrupt Status Register for Core 3 [191:128]
### 0x1B18: External I/O Interrupt Status Register for Core 3 [255:192]

### 0x1C00 - 0x1CFF: External I/O Interrupt Mapping for Cores