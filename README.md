# LoongArch CSR 和 IOCSR 整理

## CSR

### GTLBC (0x15, Guest TLB Control)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. GMTLBSZ: [5:0]
2. USETGID: [12], Enable TGID
3. TOTI: [13]
4. TGID: [23:16]

### TRGP (0x16, TLBR read guest info)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. GTLB: [0]
2. RID: [23:16]

### GSTAT (0x50, Guest status)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. VM: [0], In Virtual Machine
2. PVM: [1], Previous VM, for ERTN PVM=1 means to enter VM
3. GIDBIT: [9:4]
2. GID: [23:16], Guest ID, correspond to VPID(Virtual Processor ID) in KVM

### GCFG (0x51, Guest config)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. MATP_GUEST: [0]
2. MATP_ROOT: [1]
3. MATP_NEST: [2]
4. MATC: [5:4], 0=GUEST, 1=ROOT, 2=NEST
5. SITP: [6]
6. SIT: [7]
7. TITP: [8]
8. TIT: [9], Trap on timer
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

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

字段：

1. VIP: [7:0]
2. PIP: [15:8]
3. HC: [23:16]

### GCNTC (0x53, Guest timer offset)

来源：[Linux](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/arch/loongarch/include/asm/loongarch.h?h=v6.6)

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

TODO