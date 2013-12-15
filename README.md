beanulator
==========

  This project is designed from the ground up for cycle accuracy, flexibility, and modularity. It adopts the "isolated chip" design that has been employed to much success by other notable emulators. For years the cycle accuracy movement has been growing, and as processors have gotten faster and compilers have gotten smarter, this movement has gained a lot of support. But lets face facts, not all hardware can rationally be emulated in this fashion. Some systems are still, and will likely remain too fast to be emulated on a cycle level at playable speeds. This is where beanulator comes in.

  We need an emulation platform that allows for both approaches to thrive. HLE and LLE are both viable options for emulating most systems. Beanulator has been designed from the ground up to support both approaches, with the beginnings of an API that fully embraces LLE and cycle accuracy. This approach is also fully compatible with HLE and JIT cores. Don't think the LLE software rasterizer is getting the job done fast enough? Switch over to the HLE implementation! The ability to plug and play every component of a certain emulated system is a very desirable trait, and it is with this philosophy that beanulator will move forward.
  
  The above will be accomplished by isolating every component away from the others. This way, other components can be swapped in at a later time if necessary. This offers an amazing amount of flexibility, and it happens to be the way these systems are designed in the real world.
  
  "What about synchronization?", you may ask. Synchronization is the cause of most emulator woes, and it is the reason why after literal years of development, some emulators still have problems with some games. In beanulator, synchronization will be handled epxlicitly by "motherboard" and "clock generator" classes. This solves many problems, not the least of which is something coined as "bus hold delays". In reality, signals don't propagate instantaneously, they take a short while to stabilize or be sampled. Imagine the following example of the NES (Famicom):
  
  In the NES, there are 2 chips that communicate with each other, the PPU (Picture Processing Unit) and the CPU (Central Processing Unit). The PPU will assert the CPU's NMI line near the end of each frame, but this isn't instant, it takes a few cycles to happen. In an emulator you might say "just have it happen a few cycles later", and while this may work I consider it a hack. In beanulator the processors have no concept of the other, and the NMI signal will have to be sent from the PPU to the CPU by the motherboard class, effectively emulating the delay!
  
  This project is still in it's infancy, and needs experienced emulator developers and hardware aficionado's alike. To help craft the absolute best platform for both HLE and LLE implementations to thrive.