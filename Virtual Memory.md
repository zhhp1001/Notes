# Virtual Memory



## VM as a Tool for Caching

- Conceptually, *virtual memory* is an array of N contiguous bytes stored on disk.
- The contents of the array on disk are cached in *physical memory (DRAM cache)*
  - And just like any cache the data is broken up into blocks.
  - And those blocks for virtual memory systems are called pages (4K bytes instead of 64K bytes).
  - A subset of those pages are stored in the physical DRAM memory



Page status

- Unallocated
- Uncached
- Cached

Most of the address space is **unallocated**. 



### Enabling Data Structure: Page Table

- A *page table* is an array of page table entries (PTEs) that maps virtual pages to physical pages.

  - The kernel maintains for as part of each process context. So every process has its own page table.
  - It's an array of so called page table entries or **PTE**s.
  - Where PTE k contains the physical address of physical page k in DRAM.

  

## VM as a Tool for Memory Management

The kernel implements this by giving each process its own separate page table in the context of that process, so it's just a data structure in the kernel that the kernel keeps for that process.

- It can view memory as a simple linear array.
- Map virtual pages to the same physical page is possible.



## VM as a Tool for Memory Protection

- Extend PTEs with permission bits.
- MMU checks these bits on each access



## VM Address Translation



### Summary of address Translation Symbols



- Basic Parameters
  - N = 2<sup>n</sup> : Number of addresses in virtual address space
  - M = 2<sup>m</sup> : Number of addresses in physical address space
  - P = 2<sup>p</sup> : Page size (bytes)  
- Components of the virtual address (VA)
  - TLBI : TLB index
  - TLBT : TLB tag
  - VPO : Virtual page offset
  - VPN : Virtual page number
- Components of the physical address (PA)
  - PPO : Physical page offset (same as VPO)
  - PPN : Physical page number
  - CO : Byte offset within cache line
  - CI : Cache index
  - CT : Cache tag



### Address Translation With a Page Table



The offset in a virtual block is going to be the same as the offset in a physical block. They are the same size blocks.



### Speeding up Translation with a TLB



- Page table entries (PTEs) are cached in L1 like any other memory word.
  - PTEs may be evicted by other data references
  - PTEs hit still requires a small L1 delay
- Solution: *Translation Lookaside Buffer (TLB)*
  - Small set-associative hardware cache in MMU
  - Maps virtual page numbers to physical page numbers
  - Contains complete page table entries for small number of pages

TLB is a **hardware cache** that caches is PTEs. It's just like any other 

TLB uses the VPN portion of the virtual address to access it.



## Multi-Level Page Tables



- Suppose: 
  - 4KB (2<sup>12</sup>)  page size, effective address space is 48 bits, 8-byte PTE
- Problem:
  - Would need 512GB page table!
    - 2<sup>48</sup> * 2<sup>-12</sup> *2<sup>3</sup> = 2<sup>39</sup> bytes





















